Got it! Here’s a rewritten, polished version of your **README** that keeps all the technical details but makes it cleaner, professional, and easier to follow:

---

# Final Project 026 – Network File System (NFS)

## Overview

This project implements a **distributed Network File System (NFS)** that allows seamless file access across a network.
The system is composed of three core components:

* **Clients** – request file operations
* **Naming Server (NM)** – manages metadata and coordinates requests
* **Storage Servers (SS)** – store and retrieve actual files

Together, they form a fault-tolerant, scalable, and efficient file system.

---

## System Components

### Clients

* **Role:** Act as the entry point for users or applications.
* **Functions:** Initiate operations like reading, writing, creating, deleting, and listing files/folders.
* **Importance:** Provide the main interface for interacting with the NFS.

### Naming Server (NM)

* **Role:** Central coordinator between clients and storage servers.
* **Functions:**

  * Maintain directory structure and file-to-server mapping.
  * Direct clients to the correct storage server.
* **Importance:** Ensures efficient file access and accurate request handling.

### Storage Servers (SS)

* **Role:** Handle persistence of files and directories.
* **Functions:**

  * Store, retrieve, and manage file data.
  * Enforce security and distribution.
* **Importance:** Backbone of the NFS, ensuring reliable storage and retrieval.

---

## Supported File Operations

Clients can perform the following operations within the NFS:

1. **Create File/Folder** – Allocate storage and initialize metadata.
2. **Write File/Folder** – Create or update contents dynamically.
3. **Read File** – Retrieve file contents.
4. **Delete File/Folder** – Remove unnecessary files/folders and free space.
5. **List Directory** – Get all files/subfolders in a directory.
6. **Get File Info** – Retrieve metadata such as size, permissions, and timestamps.

---

## System Specifications

### 1. Naming & Storage Server Initialization

* **Naming Server (NM):** First component to initialize, manages file directory mapping.

* **Storage Servers (SS):** On startup, each SS registers with the NM by sending:

  * IP address
  * Port for NM communication
  * Port for client requests
  * List of accessible paths

* **Dynamic Registration:** New SS can join at runtime.

* **Client Access:** Once all servers are registered, NM begins serving client requests.

---

### 2. Storage Server Responsibilities

* **Server Commands (via NM):**

  * Create empty file/directory
  * Delete file/directory
  * Copy files/directories across servers

* **Client Interactions:**

  * Read file
  * Write file
  * Get size and permissions

---

### 3. Concurrent Access

* **Multiple Clients:** NM supports simultaneous requests.
* **Acknowledgment System:**

  * Initial ACK confirms request received.
  * Final ACK from SS confirms completion.
* **Non-blocking Behavior:** NM continues serving other clients while processing.

---

### 4. File Access Rules

* **Concurrent Reads:** Multiple clients can read the same file simultaneously.
* **Write Locking:** Only one client can write to a file at a time to maintain consistency.

---

### 5. Optimized Search (on NM)

* **Efficient Lookup:** Uses **Tries** or **Hashmaps** instead of linear search.
* **LRU Caching:** Stores recent queries to speed up repeated lookups.

---

### 6. Failure Detection

* **Monitoring:** NM continuously monitors storage server health.
* **Failure Response:** If an SS fails, NM quickly reroutes requests.

---

### 7. Data Redundancy & Replication

* **Replication Strategy:**

  * Each file is duplicated across at least 2 other servers (if more than 2 SS exist).
  * Replicas are **read-only**.
* **Failure Handling:** If a server goes down, NM retrieves data from replicas.
* **Recovery:** When a server rejoins, its replicas are reconciled with the original.

---

### 8. Asynchronous Duplication

* **Write Operations:** Duplicated across replicas asynchronously.
* **Non-blocking:** NM does not wait for confirmation to avoid delays.
* **Fault Tolerance:** Ensures durability while keeping system responsive.

---

## Getting Started

1. **Start the Naming Server (NM).**
2. **Initialize Storage Servers (SS).** Each server will auto-register with NM.
3. **Run Clients** to perform file operations via NM.

---
