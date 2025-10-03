# open-vpn-client-instllation-on-ubntu-server-
open vpn client
step-by-step guide for setting up an OpenVPN client on Ubuntu, based on your information:
1. Update and Install OpenVPN
First, update your system’s package list and install OpenVPN:
```
sudo apt update
sudo apt install openvpn -y
```
2. Copy the OpenVPN Configuration File

Copy your OpenVPN configuration file (wa-openvpn-2.ovpn) to the OpenVPN client directory:
```
sudo cp -v wa-openvpn-2.ovpn /etc/openvpn/client/
```
3. Test the OpenVPN Client Connection

To test the connection, run the following command:
```
sudo openvpn --client --config /etc/openvpn/client/wa-openvpn-2.ovpn
```
This command will attempt to connect to the VPN server using the provided configuration file. Look for Initialization Sequence Completed to verify a successful connection.
4. Create a Symlink for the OpenVPN Client Configuration

Create a symbolic link to make it easier for the system to manage the client configuration file:
```

sudo ln -s /etc/openvpn/client/wa-openvpn-2.ovpn /etc/openvpn/client.conf
```
5. Configure the OpenVPN Service to Use Your Configuration

Edit the OpenVPN service to ensure it uses the correct configuration file:
```


sudo systemctl edit openvpn@client.service
```
When the editor opens, add the following line:
```

ExecStart=/usr/sbin/openvpn --config /etc/openvpn/client/wa-openvpn-2.ovpn
```
Save and exit.
6. Start and Enable the OpenVPN Service

Start the OpenVPN client service and enable it to run on startup:
```

sudo systemctl restart openvpn@client
sudo systemctl enable openvpn@client
```
7. Check the VPN Status

To confirm the VPN client is running correctly:

```

sudo systemctl status openvpn@client
```
You should see the status as active (running). Look for logs like "VERIFY OK" and "Initialization Sequence Completed" to confirm the connection.
8. Verify the VPN Connection

To confirm your IP address has changed to the VPN server’s IP address, use the following command:

```
curl -L ifconfig.me
```
If connected successfully, the output should display the IP address assigned by the VPN server.
