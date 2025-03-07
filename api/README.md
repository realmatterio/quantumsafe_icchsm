<div align="center">
  <img src="../Logo - IronCAP and Real Matter.png" alt="IronCAP and Real Matter Logo" width="100%">
  <h2><strong>Pioneering Quantum-Safe Security for Financial Systems</strong></h2><br>
  <a href="https://quantumsafe-multisig.web.app">
  <img src="../quantumsafe-multisig.web.app(slide).png" alt="QuantumSafe Multisig Web App" width="100%">
  <a href="https://quantumsafe-multisig.web.app">Visit Quantum-Safe ICCHSM Demo</a>
</div>
<br>

<div align="right">
  <h3>Jump to > <a href="../README.md">Quantum-Safe ICCHSM Demo Menu</a></h3><br>
</div>

<div align="center">
  <h1> Quantum-Safe ICCHSM API Documentation </h1>
</div>

## Overview
The Quantum-Safe ICCHSM (IronCAP Cryptographic Hardware Security Module) API provides endpoints for quantum-safe cryptographic operations including key management, digital signatures, encryption/decryption, and blockchain integration.

## Base URL
All endpoints are accessible via Firebase Cloud Functions with the base URL:
`https://{function-name}-kez6dpnjlq-uc.a.run.app`

## Authentication
All endpoints accept POST requests with form-encoded data. No authentication header is required, but operations using the HSM require a valid slot ID and PIN.

## Endpoints

### 1. Message Management

#### Write Message
- **URL**: `https://writemessage-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `message` (string, required): The message to store for signing or encryption
- **Response**:
  ```json
  {
    "status": "Message saved successfully"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://writemessage-kez6dpnjlq-uc.a.run.app \
    -d "message=This is a test message for quantum-safe encryption"
  ```

#### Hash Message
- **URL**: `https://hashmessage-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**: None (uses previously stored message)
- **Response**:
  ```json
  {
    "binary_content": "hash_value_string"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://hashmessage-kez6dpnjlq-uc.a.run.app
  ```

### 2. Key Management

#### Show Key
- **URL**: `https://showkey-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `slot` (string, required): HSM slot ID (e.g., "1209011109" or "1661660599")
  - `pin` (string, required): PIN for the HSM slot
- **Response**:
  ```json
  {
    "console_log": "Key information output"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://showkey-kez6dpnjlq-uc.a.run.app \
    -d "slot=1209011109" \
    -d "pin=your_pin_here"
  ```

### 3. Signature Operations

#### Sign Message
- **URL**: `https://signmessage-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `slot` (string, required): HSM slot ID
  - `pin` (string, required): PIN for the HSM slot
  - `id` (string, required): Key ID (e.g., "322601A")
  - `mechanism` (string, required): Selected quantum-safe mechanism (e.g., "ckm-icc-shake256-mm-sphincsplus-simple")
- **Response**:
  ```json
  {
    "console_log": "Signature operation output"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://signmessage-kez6dpnjlq-uc.a.run.app \
    -d "slot=1209011109" \
    -d "pin=your_pin_here" \
    -d "id=322601A" \
    -d "mechanism=ckm-icc-shake256-mm-sphincsplus-simple"
  ```

#### Read Signature
- **URL**: `https://readsignature-kez6dpnjlq-uc.a.run.app`
- **Method**: `GET`
- **Parameters**: None
- **Response**:
  ```json
  {
    "content": "signature_value"
  }
  ```
- **curl Example**:
  ```bash
  curl -X GET https://readsignature-kez6dpnjlq-uc.a.run.app
  ```

#### Verify Signature
- **URL**: `https://verifysignature-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `slot` (string, required): HSM slot ID
  - `pin` (string, required): PIN for the HSM slot
  - `id` (string, required): Key ID
  - `mechanism` (string, required): Selected quantum-safe mechanism
- **Response**:
  ```json
  {
    "console_log": "Verification result output"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://verifysignature-kez6dpnjlq-uc.a.run.app \
    -d "slot=1209011109" \
    -d "pin=your_pin_here" \
    -d "id=322601A" \
    -d "mechanism=ckm-icc-shake256-mm-sphincsplus-simple"
  ```

### 4. Encryption Operations

#### Encrypt Message
- **URL**: `https://encryptmessage-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `slot` (string, required): HSM slot ID
  - `pin` (string, required): PIN for the HSM slot
  - `id` (string, required): Key ID
  - `mechanism` (string, required): Selected quantum-safe mechanism
- **Response**:
  ```json
  {
    "console_log": "Encryption operation output"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://encryptmessage-kez6dpnjlq-uc.a.run.app \
    -d "slot=1209011109" \
    -d "pin=your_pin_here" \
    -d "id=322601A" \
    -d "mechanism=ckm-icc-shake256-mm-modern-mceliece"
  ```

#### Read Encrypted Content
- **URL**: `https://readencrypted-kez6dpnjlq-uc.a.run.app`
- **Method**: `GET`
- **Parameters**: None
- **Response**:
  ```json
  {
    "content": "encrypted_content"
  }
  ```
- **curl Example**:
  ```bash
  curl -X GET https://readencrypted-kez6dpnjlq-uc.a.run.app
  ```

#### Decrypt Message
- **URL**: `https://decryptmessage-kez6dpnjlq-uc.a.run.app`
- **Method**: `POST`
- **Parameters**:
  - `slot` (string, required): HSM slot ID
  - `pin` (string, required): PIN for the HSM slot
  - `id` (string, required): Key ID
  - `mechanism` (string, required): Selected quantum-safe mechanism
- **Response**:
  ```json
  {
    "console_log": "Decryption operation output"
  }
  ```
- **curl Example**:
  ```bash
  curl -X POST https://decryptmessage-kez6dpnjlq-uc.a.run.app \
    -d "slot=1209011109" \
    -d "pin=your_pin_here" \
    -d "id=322601A" \
    -d "mechanism=ckm-icc-shake256-mm-modern-mceliece"
  ```

#### Read Decrypted Content
- **URL**: `https://readdecrypted-kez6dpnjlq-uc.a.run.app`
- **Method**: `GET`
- **Parameters**: None
- **Response**:
  ```json
  {
    "content": "decrypted_content"
  }
  ```
- **curl Example**:
  ```bash
  curl -X GET https://readdecrypted-kez6dpnjlq-uc.a.run.app
  ```

### 5. Blockchain Integration

#### Publish to Blockchain
- **URL**: `https://us-central1-quantumsafe-multisig.cloudfunctions.net/publishBlockchain`
- **Method**: `PUT`
- **Content-Type**: `application/json`
- **Request Body**:
  ```json
  {
    "command": "createVc",
    "dMessage": {
      "@context": "ICCHSM Multisig Credential V1 JS",
      "cName": "Quantum-Safe Multisig",
      "claim": {
        "did-icchsm-rsa": "hashed_content",
        "muitiSig": "sign_console_output",
        "quantumKey": "quantum_key"
      },
      "contract": {
        "method": "Description of the method",
        "developer": "Developer information"
      },
      "proofSignature": "signature_content",
      "publicKey": "public_key"
    },
    "from": "quantumeum",
    "to": "did-icchsm-rsa-hashed_content",
    "zHash": "hashed_content",
    "zSignature": "signature_content"
  }
  ```
- **Response**:
  ```json
  {
    "transaction_details": "Blockchain transaction information"
  }
  ```
- **curl Example**:
  ```bash
  curl -X PUT https://us-central1-quantumsafe-multisig.cloudfunctions.net/publishBlockchain \
    -H "Content-Type: application/json" \
    -d '{
      "command": "createVc",
      "dMessage": {
        "@context": "ICCHSM Multisig Credential V1 JS",
        "cName": "Quantum-Safe Multisig",
        "claim": {
          "did-icchsm-rsa": "7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c",
          "muitiSig": "Signature operation completed successfully...",
          "quantumKey": "322601A"
        },
        "contract": {
          "method": "SPHINCS+ with Modern McEliece",
          "developer": "Quantum-Safe ICCHSM Demo"
        },
        "proofSignature": "a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6",
        "publicKey": "d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2"
      },
      "from": "quantumeum",
      "to": "did-icchsm-rsa-7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c",
      "zHash": "7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b2c",
      "zSignature": "a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6"
    }'
  ```

## Error Responses
All endpoints may return the following error responses:

- **Status 405**: Method Not Allowed (if incorrect HTTP method is used)
- **Status 504**: Gateway Timeout (if target server doesn't respond)
- **Status 500**: Internal Server Error (for general errors)

Error response format:
```json
{
  "error": "Error type",
  "details": "Error details"
}
```

## Technology Partners

This toolkit is a collaboration between:
- **01 Communique Laboratory** - Provider of IronCAP™ Quantum-Safe cryptography
- **Real Matter Technology** - Provider of Chip-Level Blockchain technology

For more information, visit:
- [IronCAP™](https://ironcap.ca)
- [Real Matter Technology](https://www.realmatter.io)
- [Quantumatter Blockchain](https://quantumatter-blockchain.web.app)

<div align="center">
  <h2></h2><br>
  <h2><i>Seamless Integration of Quantum-Safe HSM Module & Lattice-Based Chip Entropy for PQC Next-Gen Security</i></h2>
</div>
