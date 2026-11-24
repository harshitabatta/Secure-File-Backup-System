# Secure File Backup System

A Python-based client-server file backup system developed as a **Computer Networks (CN) project**. The application enables clients to upload, manage, back up, and restore files and folders over a network using TCP sockets secured with SSL/TLS.

The project explores network communication, secure data transfer, client-server architecture, file-system monitoring, and automated backup mechanisms.

## Overview

The system consists of a client and a server communicating over a TCP connection secured using SSL/TLS.

The client can interact with the backup server to upload files and folders, browse stored backups, restore files to a specified destination, and automate backup operations. It also supports monitoring a directory for newly created files and uploading them automatically.

## Features

- **Secure Client-Server Communication:** TCP socket communication secured using SSL/TLS certificates.
- **File Upload:** Upload individual files to the backup server.
- **Folder Backup:** Upload folders and their contents.
- **Recursive Folder Upload:** Traverse folders recursively and upload their files while preserving relative paths.
- **Scheduled Backups:** Automate recurring backup operations using Python's `schedule` library.
- **File-System Monitoring:** Monitor directories for newly created files using `watchdog` and automatically upload them.
- **File Listing:** Request a listing of files stored on the backup server.
- **File Restoration:** Restore backed-up files and folders to a specified local destination.
- **File Deletion:** Delete files from the backup server.
- **Command-Based Interface:** Interact with the server using commands through a terminal-based client.

## Architecture

```text
                CLIENT
        ┌──────────────────────┐
        │   Python Client      │
        │                      │
        │  File Upload         │
        │  Folder Backup       │
        │  Scheduled Backup    │
        │  File Monitoring     │
        │  File Restoration    │
        └──────────┬───────────┘
                   │
                   │ TCP Socket
                   │ SSL/TLS Encryption
                   │ Port 4456
                   │
        ┌──────────▼───────────┐
        │   Backup Server     │
        │                      │
        │  Receive Files      │
        │  Manage Backups     │
        │  List Files         │
        │  Delete Files       │
        │  Restore Files      │
        └──────────────────────┘
```

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application logic |
| Socket | Client-server network communication |
| SSL/TLS | Secure communication |
| Watchdog | File-system event monitoring |
| Schedule | Scheduled backup execution |
| OS | File and directory management |
| Glob | Recursive file discovery |

## Commands

The client supports the following commands:

| Command | Description |
|---|---|
| `HELP` | Request available commands |
| `LOGOUT` | Disconnect from the server |
| `FILES_LIST` | Request the list of backed-up files |
| `LIST` | List available backup contents |
| `UPLOAD <path>` | Upload a file or folder |
| `FOLDER_RECURSIVE_UPLOAD <path>` | Recursively upload files from a folder |
| `RESTORE <server_path> <destination_path>` | Restore a backup to a specified local path |
| `DELETE <path>` | Delete a file from the backup server |
| `BACKUP` | Schedule recurring backup operations |
| `WATCH <path>` | Monitor a directory and automatically upload newly created files |

## How It Works

### 1. Secure Connection

The client establishes a TCP connection to the server and wraps the socket using an SSL context.

Certificate-based authentication and encryption are configured through certificate and key files.

### 2. File Upload

The client reads the requested file and sends the upload command along with the filename and file contents to the server.

### 3. Recursive Folder Backup

The client traverses the selected folder recursively using `glob` and uploads individual files while maintaining their relative paths.

### 4. Scheduled Backup

The application uses the Python `schedule` library to periodically execute a backup operation.

The current client implementation schedules recursive uploads at a 20-second interval.

### 5. Automatic File Monitoring

The client uses `watchdog` to monitor a selected directory.

When a new file is created, the event handler reads the file and sends it to the server automatically.

### 6. File Restoration

The client requests a file or folder from the server and specifies the destination path.

The restoration logic creates the necessary directories and writes the restored file to the requested location.

## Project Structure

```text
Secure-File-Backup-System/
│
├── client.py       # Client-side operations and network communication
├── server.py       # Server-side communication and backup handling
├── README.md
│
├── server.crt      # Server certificate
├── client.crt      # Client certificate
├── client.key      # Client private key
```

> Certificate files and private keys should not be committed to a public repository. Generate or configure your own certificates before running the application.

## Prerequisites

- Python 3
- OpenSSL
- Required Python packages:
  - `schedule`
  - `watchdog`

Install dependencies:

```bash
pip install schedule watchdog
```

## Configuration

The client currently uses the following network configuration:

- **Port:** `4456`
- **Protocol:** TCP
- **Encoding:** UTF-8
- **SSL/TLS:** Enabled
- **Server hostname:** Configured through `server_sni_hostname`

Certificate configuration is defined in the client code and should be updated according to your local environment.

## Running the Project

The project requires both the server and client applications to be configured and running.

### 1. Configure SSL Certificates

Configure the required server and client certificate files and private keys.

### 2. Start the Server

Run the server application on the machine that will store the backups.

```bash
python server.py
```

### 3. Start the Client

On the client machine, run:

```bash
python client.py
```

### 4. Interact With the Backup System

Use the available terminal commands to upload files, manage backups, schedule backup operations, monitor folders, or restore files.

## Computer Networks Concepts

This project demonstrates practical applications of:

- Client-server architecture
- TCP socket programming
- Network communication
- SSL/TLS encryption
- Secure data transmission
- Port-based communication
- File transfer over a network
- Network protocol design
- Connection handling

## Additional Concepts

- File-system event monitoring
- Recursive directory traversal
- Automated task scheduling
- File and directory management
- Backup and recovery mechanisms

## Academic Context

- **Project Type:** Computer Networks Mini Project
- **Programming Language:** Python
- **Architecture:** Client-Server
- **Communication Protocol:** TCP
- **Security:** SSL/TLS
- **Objective:** Implement a secure network-based file backup and restoration system

---

Developed as part of a Computer Networks project to explore secure client-server communication and automated file backup mechanisms.
