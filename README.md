# Lab Work

## 1. Component Diagram
![Component Diagram](images/component.png)

---

## 2. Sequence Diagram
![Sequence Diagram](images/sequence.jpg)

---

## 3. State Diagram
![State Diagram](images/state.jpg)

---

## ADR-001: End-to-End Encryption for Message Privacy

### Status
Accepted

---

### Context
The system is designed as a messaging platform where users exchange messages through a server (API + delivery service).  
A key requirement is that message content must remain private even from the server infrastructure.

Users may be online or offline, and messages are stored or forwarded through backend services.

---

### Decision
We implement **End-to-End Encryption (E2EE)**:

- Messages are encrypted on the sender’s client using the recipient’s public key
- Only the recipient’s client can decrypt messages using their private key
- Encryption and decryption happen exclusively on client devices
- Server-side components (API, delivery service, storage) handle only encrypted data (ciphertext)

---

### Alternatives Considered

- **Server-side encryption/decryption** — rejected because the server would access plaintext messages, violating privacy requirements  
- **No encryption** — rejected due to security risks  
- **Hybrid model with server key access** — rejected because it breaks end-to-end privacy guarantees  

---

### Consequences

#### Positive
- Strong privacy: server cannot read messages
- Protection against server breaches
- Increased user trust and security model

#### Negative
- More complex client implementation
- Key management is fully client-side responsibility
- No server-side message content processing (e.g., moderation/search)
- Risk of message loss if private key is lost
