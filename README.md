# DejTunnel: Tinc Mesh VPN Management Panel

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Bash Script](https://img.shields.io/badge/Language-Bash-blue)](https://www.gnu.org/software/bash/)
[![Python](https://img.shields.io/badge/Backend-Flask-green)](https://flask.palletsprojects.com/)
[![Frontend](https://img.shields.io/badge/UI-Tailwind%20CSS-cyan)](https://tailwindcss.com/)

DejTunnel is a powerful, self-hosted web panel designed to simplify the creation and management of **Tinc VPN** mesh networks. It automates the entire setup process, from server provisioning to node configuration, through a single, easy-to-use installation script and provides a clean, modern web interface for ongoing management.

Say goodbye to complex manual configurations. With DejTunnel, you can deploy a full-featured, secure mesh VPN in minutes.

### 📸 Dashboard Preview

*(Note: Replace this with a real screenshot of your dashboard)*
![OVPN Manager Dashboard](https://uploadkon.ir/uploads/048b11_25dejtunnel.png)
---

## ✨ Key Features

* **🚀 One-Command Installation**: A single bash script handles all dependencies, configures the main server, sets up the web panel, and starts all necessary services.
* **💻 Intuitive Web Dashboard**: A clean, responsive UI built with Flask and Tailwind CSS to monitor and manage your entire Tinc network.
* **🔗 Full Node Lifecycle Management**:
    * **Add Nodes**: Easily provision new remote servers. The panel automatically installs Tinc, exchanges keys, and connects the node to the mesh.
    * **Delete Nodes**: Gracefully remove nodes from the network, cleaning up all related configurations.
    * **Restart Nodes**: Restart the Tinc service on the main server or any remote node directly from the UI.
* **👁️ Real-time Status & Logs**:
    * View the online/offline status of all nodes at a glance.
    * Access and view Tinc service logs for both the main and remote nodes in a clean terminal interface within the browser.
* **⚙️ Async Task Processing**: All heavy operations (like adding or deleting nodes) run as background tasks, allowing you to monitor their progress in real-time without blocking the UI.
* **🔧 Easy Configuration Management**:
    * **Change Main Server IP**: If your main server's public IP changes, update it from the settings panel, and DejTunnel will automatically reconfigure all nodes.
    * **Import/Export Nodes**: Export your entire list of remote nodes to a JSON file for backup, or import a JSON file to batch-provision multiple nodes at once.
* **🔐 Secure**:
    * Password-protected login for the web panel.
    * Uses `sshpass` for automated, non-interactive SSH configuration of remote nodes.

---

## 🛠️ Tech Stack

* **Backend**: Flask (Python)
* **VPN**: Tinc
* **Web Server**: Nginx (as a reverse proxy)
* **Application Server**: Gunicorn
* **Frontend**: Tailwind CSS, Vanilla JavaScript
* **Core Logic**: Bash Script, `sshpass`, `systemctl`

---

## 🚀 Getting Started

Installation is designed to be as simple as possible. You just need a fresh server running a Debian-based OS (like Ubuntu or Debian).

### Prerequisites

* A server with a public IP address.
* **Ubuntu 20.04/22.04** or **Debian 10/11** is recommended.
* Root or `sudo` access.

### Installation

1.  SSH into your server.

2.  Download the installation script:
    ```bash
    wget -q -O /root/DejTunnel.sh https://raw.githubusercontent.com/eylandoo/DejTunnel/main/DejTunnel.sh && chmod +x /root/DejTunnel.sh && /root/DejTunnel.sh
    ```

The script will launch an interactive menu. Select **"1) Install DejTunnel"**. You will be prompted to enter the necessary configuration details:
* Your server's public IP address.
* A port for the web panel (e.g., 80).
* A username and password for the panel administrator.
* Details for your Tinc network (network name, node name, private IP range).

The script will then handle everything else automatically. Once finished, it will display the URL and credentials to access your new DejTunnel panel.

---

## 📖 How to Use

### 1. Initial Login

Navigate to `http://<your_server_ip>:<port>` in your web browser. Log in with the administrator credentials you created during installation.

### 2. Dashboard Overview

The dashboard provides a central view of your network:
* **Main Server Status**: Shows the status, name, and IP addresses of your main Tinc node.
* **Remote Nodes**: A list of all connected remote nodes, their online/offline status, and their IP details.

### 3. Adding a New Node

1.  Click the **"Add Node"** button.
2.  Fill in the details for the new remote server:
    * **Node Name**: A unique name (e.g., `germanynode`). Must be alphanumeric.
    * **Public IP Address**: The public IP of the server you want to add.
    * **Tinc Private IP**: The unique private IP this node will have within the VPN (e.g., `10.20.0.2`).
    * **SSH Username & Password**: Credentials for the panel to access and configure the new server.
3.  Click **"Add & Provision"**. A log window will appear, showing the real-time progress of the configuration.

### 4. Managing Nodes

For each node (both main and remote), you have several options:
* **View Log**: Opens a terminal window showing the latest Tinc service logs for that specific node.
* **Restart**: Restarts the Tinc service on that node.
* **Delete** (Remote nodes only): Removes the node from the mesh, uninstalls Tinc from the remote server, and updates all other nodes.

### 5. Settings Panel

Click the gear icon in the top navigation bar to access the settings modal:
* **Change Main Server IP**: If your main server's IP changes, update it here to automatically reconfigure the entire network.
* **Export/Import Nodes**: Use these buttons to back up your node list or to add multiple nodes at once from a JSON file.

### 6. The Management Script

To manage your installation itself (reinstall, uninstall, or change the admin password/port), simply run the script again on your server:

```bash
sudo ./DejTunnel.sh
