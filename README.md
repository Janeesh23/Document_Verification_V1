# Document Verification using Blockchain

This is a full-stack decentralized application (DApp) for verifying documents on the Ethereum blockchain. Instead of storing the actual document, it securely stores the **SHA-256 hash** of the document. This ensures tamper-proof verification while keeping user data private.

---

## Features

- Store only **document hash**, not the document itself  
- Register document hashes securely on-chain  
- Verify documents based on their SHA-256 hash  
- MetaMask-based wallet interaction  
- Truffle + Ganache for local Ethereum testing  

---

## Tech Stack

| Layer          | Technology                 |
|----------------|-----------------------------|
| Smart Contract | Solidity (`^0.8.0`)         |
| Blockchain     | Ganache (Local Ethereum)    |
| Deployment     | Truffle                     |
| Backend        | Python (Flask), Web3.py     |
| Frontend       | HTML, Bootstrap, JavaScript |
| Wallet         | MetaMask                    |

---
## Setup Instructions

### 1. Prerequisites

- [Node.js](https://nodejs.org/)
- [Ganache](https://trufflesuite.com/ganache/)
- [MetaMask](https://metamask.io/)
- Python 3.x

Install required Python libraries:

```bash
pip install flask web3
```

---

### 2. Deploy Smart Contract

Start Ganache on port `8545`, then:

```bash
# Install Truffle if not already
npm install -g truffle

# Compile and migrate the contract
truffle compile
truffle migrate --network development
```

After deploying, copy the deployed contract address and paste it in `app.py`:

```python
contract_address = "0xYourDeployedContractAddress"
```

---

### 3. Start Flask Backend

```bash
python app.py
```

Server will run at:  
`http://127.0.0.1:5000`

---

### 4. Interact with the Frontend

1. Open [http://127.0.0.1:5000](http://127.0.0.1:5000)
2. Connect MetaMask to the local Ganache network
3. Upload a document to register its hash
4. Upload the same document later to verify

---

## How It Works

- Document is **never stored** on-chain  
- A **SHA-256 hash** is computed from the uploaded file  
- This hash is stored in a smart contract with a timestamp  
- Later, any file can be re-uploaded to verify if its hash matches  

---

## Smart Contract: `DocumentVerification.sol`

```solidity
function addDocument(string memory _fileHash) public;
function verifyDocument(string memory _fileHash) public view returns (bool, uint256);
```

- Prevents duplicate document registrations  
- Emits a `DocumentAdded` event  
- Stores timestamp of registration for audit  

---

## MetaMask Transaction Flow

1. User uploads a file  
2. Flask hashes it and checks for duplication  
3. If not found, it builds a transaction  
4. Transaction is signed via MetaMask  
5. The document hash is registered on-chain  

---

## Future Enhancements

- Add decentralized file storage (e.g. IPFS or S3)  
- Integrate email or QR code-based verification  
- Deploy to public Ethereum testnets (Goerli, Sepolia)  
- Add drag-and-drop support + better file previews  

---

