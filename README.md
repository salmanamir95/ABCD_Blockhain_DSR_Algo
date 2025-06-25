# MANET Blockchain Routing Protocol (PoPW-Based)

## 📌 Project Title:

**Energy-Aware Trust-Driven Lightweight Blockchain Routing Protocol for Mobile Ad-Hoc Networks**

## 📘 Abstract:

This protocol defines a lightweight, secure, and decentralized blockchain framework for routing in Mobile Ad-hoc Networks (MANETs). It integrates energy awareness (Logical Battery), trust evaluation, and efficient pathworthiness scoring to make routing decisions while maintaining security through cryptographic primitives and node-level blockchain synchronization.

---

## 🧱 Architecture Overview

### 🔷 Sub-Network Cluster Design:

* The total MANET (`n` nodes) is divided into **n/4 subnetworks**.

  * Each subnetwork contains **>= 4 nodes**.
  * One node in each subnetwork becomes the **Head Blockchain Node (HBN)**.

### 🧠 Responsibilities of Head Blockchain Node (HBN):

* Maintain the **local blockchain ledger**:

  * Node join/leave logs
  * Path trust records
  * Logical Battery status of all nodes
  * Packet tracking via hashes
* Respond to **routing requests** from local nodes.
* Handle **inter-subnet routing** with abstraction.
* Monitor health and perform **leadership transfer** when needed.

### 👥 Shadow Blockchain Nodes:

* The two nodes with the lowest value of:

  `f(LogicalBattery) × f(Trust)`

  are chosen as **shadow nodes**.
* Shadow nodes replicate the HBN ledger.
* When HBN reaches **<= 3/4 LogicalBattery**, a **handover** occurs.

### 🔄 Trust Model:

```
Trust = Acks - NAcks - 3 × FalseAcks - LeaveCount
```

* Trust is dynamic and updated with real-time feedback.

### 🔋 Logical Battery:

* Every 100 seconds:

  * HBN sends beacon packets to all subnet nodes.
  * If a node does not respond, LogicalBattery reduces:

    * Normal node: `−1/10`
    * HBN: `−1/15`

### 📦 Routing Process:

* Node requests path from HBN.
* HBN calculates PoPW score:

```
Score = f(minLogicalBattery) × f(minTrust) × ((TotalTrust/NodeCount) × hops/(1 + hops))
```

* Assigns a **hash ID** to the packet.
* Monitors for delivery feedback via hash-based acknowledgment.
* For inter-subnet routing:

  * HBNs exchange abstracted messages, hiding node identities and topology.

---

## 🔐 Cryptographic Stack

| Component  | Algorithm         |
| ---------- | ----------------- |
| Hashing    | BLAKE3            |
| Encryption | ChaCha20-Poly1305 |
| Signing    | Ed25519           |
| Encoding   | CBOR / Protobuf   |

---

## 🔧 Technology Stack

| Layer                 | Tool / Framework            |
| --------------------- | --------------------------- |
| Language              | Rust / Go                   |
| Communication         | UDP / DTN / Gossip Protocol |
| Blockchain Data Store | Custom lightweight ledger   |
| Packet Encoding       | CBOR / JSON / Protobuf      |
| Testing & Simulation  | Python + ns-3 (optional)    |

---

## 📐 System Diagrams

### 🔸 Sub-Network and Role Assignment

![Subnet Role Diagram](images/subnet_roles.png)

### 🔸 Blockchain Lifecycle and Handover

![Blockchain Handover](images/blockchain_handover.png)

### 🔸 Routing and Pathworthiness Flow

![Routing Flow](images/routing_flow.png)

---

## 🧠 Key Protocol Benefits

| Benefit                | Explanation                                    |
| ---------------------- | ---------------------------------------------- |
| 🔄 Dynamic Leadership  | HBN role is rotated based on battery health    |
| ⚖️ Trust-Based Routing | Avoids malicious/unreliable nodes              |
| 🛡️ Privacy Respecting | Abstracts topology in inter-subnet routing     |
| 💾 Lightweight Ledger  | Rolling blockchain model reduces storage needs |
| 🔐 Secure by Design    | Modern cryptographic primitives used           |

---

## 🔚 Conclusion

This protocol provides an efficient, secure, and lightweight blockchain routing strategy for highly dynamic MANETs. It avoids traditional heavyweight consensus models, leverages node-level awareness, and enforces routing reliability through path trustworthiness, all while being energy-efficient.

> ✅ Ready for implementation in simulation environments and hardware testbeds.

---

## 📁 Suggested README.md Usage

To embed diagrams:

```markdown
![Subnet Role Diagram](images/subnet_roles.png)
![Blockchain Handover](images/blockchain_handover.png)
![Routing Flow](images/routing_flow.png)
```

Make sure to place the `images/` folder next to your README.

Would you like help generating these image diagrams next?
