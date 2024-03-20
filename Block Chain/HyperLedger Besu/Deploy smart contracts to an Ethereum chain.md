---
tags:
  - HyperLedgerBesu
  - BlockChain
date: 2024-03-20
---

## 전제 조건

- Private Network


## `eth_sendSignedTransaction`

### 예시 코드

### `compile.js

``` javascript
const fs = require("fs").promises;
const solc = require("solc");

async function main() {
  // Load the contract source code
  const sourceCode = await fs.readFile("SimpleStorage.sol", "utf8");
  // Compile the source code and retrieve the ABI and bytecode
  const { abi, bytecode } = compile(sourceCode, "SimpleStorage");
  // Store the ABI and bytecode into a JSON file
  const artifact = JSON.stringify({ abi, bytecode }, null, 2);
  await fs.writeFile("SimpleStorage.json", artifact);
}

function compile(sourceCode, contractName) {
  // Create the Solidity Compiler Standard Input and Output JSON
  const input = {
    language: "Solidity",
    sources: { main: { content: sourceCode } },
    settings: { outputSelection: { "*": { "*": ["abi", "evm.bytecode"] } } },
  };
  // Parse the compiler output to retrieve the ABI and bytecode
  const output = solc.compile(JSON.stringify(input));
  const artifact = JSON.parse(output).contracts.main[contractName];
  return {
    abi: artifact.abi,
    bytecode: artifact.evm.bytecode.object,
  };
}

main().then(() => process.exit(0));
```

node를 사용해서 할 경우, 다음과 같이 소스 코드를 작성하여 아래의 명령어를 실행
```bash
node compile.js
```
혹은 `solc` 를 이용해서 contract의 bytecode와 ABI 파일을 받습니다.
```bash
solc SimpleStorage.sol --bin --abi
```
실행 결과 `SimpleStorage.bin`과 `SimpleStorage.abi` 파일이 생성이 됩니다.

transaction을 전송하기 위해서 사용되는 예시 코드는 아래와 같습니다.
```javascript
const web3 = new Web3(host);
// use an existing account, or make an account
const privateKey =
  "0x8f2a55949038a9610f50fb23b5883af3b4ecb3c3bb792cbcefbd1542c692be63";
const account = web3.eth.accounts.privateKeyToAccount(privateKey);

// read in the contracts
const contractJsonPath = path.resolve(__dirname, "SimpleStorage.json");
const contractJson = JSON.parse(fs.readFileSync(contractJsonPath));
const contractAbi = contractJson.abi;
const contractBinPath = path.resolve(__dirname, "SimpleStorage.bin");
const contractBin = fs.readFileSync(contractBinPath);
// initialize the default constructor with a value `47 = 0x2F`; this value is appended to the bytecode
const contractConstructorInit =
  "000000000000000000000000000000000000000000000000000000000000002F";

// get txnCount for the nonce value
const txnCount = await web3.eth.getTransactionCount(account.address);

const rawTxOptions = {
  nonce: web3.utils.numberToHex(txnCount),
  from: account.address,
  to: null, //public tx
  value: "0x00",
  data: "0x" + contractBin + contractConstructorInit, // contract binary appended with initialization value
  gasPrice: "0x0", //ETH per unit of gas
  gasLimit: "0x24A22", //max number of gas units the tx is allowed to use
};
console.log("Creating transaction...");
const tx = new Tx(rawTxOptions);
console.log("Signing transaction...");
tx.sign(privateKey);
console.log("Sending transaction...");
var serializedTx = tx.serialize();
const pTx = await web3.eth.sendSignedTransaction(
  "0x" + serializedTx.toString("hex").toString("hex"),
);
console.log("tx transactionHash: " + pTx.transactionHash);
console.log("tx contractAddress: " + pTx.contractAddress);
```

jb bj nknbbb 