# SSH-Remote-Server-Connection

Created multiple Ec2 servers on AWS

Created one of the server as the Main server, Connected to the Main server through SSH Connection using the .pem key.

Generated the SSH keys in the Main server to connect the remote servers (target servers), copied the pub file from the Main server and pasted in the target servers in .ssh/authorized_keys file.

Created "server_list.conf" file, Inside that we kept multiple IP's of remote server.

🔐 SSH Remote Server Connection Setup

📌 Scenario:


You created multiple EC2 servers on AWS.

One acts as the Main Server (Jump Host).

From the Main Server, you want to connect to other remote target servers via SSH.

⚙️ Step 1: Launch EC2 Instances

Create multiple EC2 servers on AWS.

One server will be the Main Server (Jump server).

Others are Target Servers.

🖼️ Diagram:

⚙️ Step 2: Connect to the Main Server

Use your .pem key from your local machine to connect to the Main Server:

ssh -i my-key.pem ubuntu@<MAIN_SERVER_PUBLIC_IP>


🔑 ✅ Now you’re inside the Main Server.

⚙️ Step 3: Generate SSH Keys in Main Server

Inside the Main Server, generate a new SSH key pair:

ssh-keygen -t rsa -b 4096


Press Enter for defaults → it creates:

Private Key: ~/.ssh/id_rsa

Public Key: ~/.ssh/id_rsa.pub

🖼️ Diagram:

⚙️ Step 4: Copy Public Key to Remote (Target) Servers

Copy the public key (id_rsa.pub) to each Target Server.

ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@<TARGET_SERVER_IP>


OR manually copy contents of id_rsa.pub and paste into:

~/.ssh/authorized_keys


on each target server.

🔑 This allows passwordless SSH login from Main Server → Target Servers.

🖼️ Diagram:

⚙️ Step 5: Create Server List File

On the Main Server, create a file server_list.conf and add all Target Server IPs:

nano server_list.conf


Example content:

192.168.1.10
192.168.1.11
192.168.1.12

⚙️ Step 6: Test Connections

From the Main Server, you can now connect to any target server directly:

ssh ubuntu@192.168.1.10


✔️ No password required 🚀
