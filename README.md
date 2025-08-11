<p align="center">
  <img src="./assets/avatar.jpeg" alt="Persistent SSH Connection Manager Logo" width="200">
</p>

# Persistent SSH Connection Manager

This repository contains a powerful Bash script designed to establish and maintain a robust, persistent SSH connection to a remote server. It automates the initial setup process and ensures you stay connected by automatically attempting to reconnect if the connection is lost.

## Overview

Connecting to a remote server via SSH is a daily task for many developers and system administrators. However, connections can be brittle, dropping due to network issues or server timeouts. This script solves that problem by wrapping the SSH command in a persistent loop.

It is particularly useful for:
*   **Unstable Networks:** Working from a location with unreliable Wi-Fi or cellular data.
*   **Long-Running Sessions:** Preventing timeouts during long compilation jobs, data transfers, or remote development sessions.
*   **Simplified Setup:** Automating the often-tedious process of key generation, key installation (`ssh-copy-id`), and `known_hosts` management for new connections.
*   **Convenience:** Providing a single, executable command to connect to a frequently used server without remembering IP addresses or flags.

### Features

*   **Easy User/IP Configuration:** Set your username and server IP address directly in the script.
*   **Automatic SSH Key Generation:** If no SSH public key is found, the script offers to generate one for you.
*   **Automated Key Installation:** Uses `ssh-copy-id` to securely install your public key on the server for passwordless login, prompting for a password only on the very first connection.
*   **Secure `known_hosts` Management:** Automatically adds the server's fingerprint to `~/.ssh/known_hosts` to prevent man-in-the-middle warnings.
*   **Persistent Connection Loop:** If the SSH connection drops, the script will automatically try to reconnect after a configurable delay.
*   **Customizable Timeouts:** Configure keep-alive intervals and probes to fine-tune how the script detects a dead connection.
*   **Terminal Title Update:** Sets the terminal window title to `username@server_ip` for easy identification when managing multiple connections.
*   **Pure Bash:** Runs in any modern Linux/Unix environment with no external dependencies beyond standard SSH core utilities.

## Prerequisites

*   A Unix-like operating system (e.g., Ubuntu 24.04, macOS).
*   Bash (Bourne-Again SHell).
*   Standard command-line utilities: `ssh`, `ssh-keygen`, `ssh-keyscan`, `ssh-copy-id`.

## Setup & Configuration

1.  **Rename the Script:**
    It's recommended to rename the example file to something simple for your server.
    ```bash
    mv username@ip-title.sh.example your_username@your_server_ip-something-to-remember.sh
    ```

2.  **Make it Executable:**
    Open your terminal and grant execute permissions to the script:
    ```bash
    chmod +x your_username@your_server_ip-something-to-remember.sh
    ```

3.  **Configure the Script:**
    Open `your_username@your_server_ip-something-to-remember.sh` with a text editor and modify the variables in the **Primary Server Configuration** and **Connection & Reconnect Behavior Configuration** sections at the top.

    ```bash
    # ===================================================================
    # Primary Server Configuration
    # ===================================================================
    USERNAME="your_username"         # Replace with your username
    SERVER_IP="your_server_ip"       # Replace with your server's IP address

    # ===================================================================
    # Connection & Reconnect Behavior Configuration
    # ===================================================================
    INITIAL_CONNECT_TIMEOUT=5
    KEEP_ALIVE_INTERVAL=15
    # ... and other settings
    ```

## How to Run

With the configuration in place, simply execute the script from your terminal:

```bash
./your_username@your_server_ip-something-to-remember.sh
```

The script will guide you through any first-time setup (like key generation or password entry for `ssh-copy-id`) and then establish the connection. To terminate the session and the script permanently, simply type `exit` or `logout` in the remote server's shell.

## Project Structure

```
.
├── your_username@your_server_ip-something-to-remember.sh     # The main executable script (renamed from .example)
└── README.md               # This file
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
*Authored by Reza 'Sam' Aghamohamadi (Hacknitive)*