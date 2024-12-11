# r720-speedfans

This repository provides scripts and configurations to manage and control fan speeds on Dell PowerEdge R720 servers using IPMI (Intelligent Platform Management Interface). By adjusting fan speeds based on system temperatures, users can optimize cooling efficiency and reduce noise levels.

## Features

- **Automatic Fan Control**: Dynamically adjusts fan speeds according to real-time temperature readings.
- **Manual Fan Control**: Allows users to set specific fan speeds as needed.
- **Service Integration**: Includes a systemd service file for seamless integration and automatic management.

## Requirements

- Dell PowerEdge R720 server
- IPMI enabled and configured
- `ipmitool` installed on the server

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/WizardCody/r720-speedfans.git
   cd r720-speedfans
   ```
2. **Install ipmitool**:
```
# For Debian/Ubuntu
sudo apt-get install ipmitool

# For CentOS/RHEL
sudo yum install ipmitool
```
3. **Configure IPMI**:
- Ensure IPMI is enabled in the iDRAC settings:
- Navigate to iDRAC Settings > Network > IPMI Settings.
- Enable IPMI over LAN.
- Set the Channel Privilege Level Limit to Administrator.
- Create a dedicated user with IPMI permissions under iDRAC Settings > User Authentication.

4. **Edit Configuration:**
- Modify the speedfans script to include your iDRAC IP, username, and password:
```
IPMIHOST=your_idrac_ip
IPMIUSER=your_username
IPMIPW=your_password
```
5. **Set Up the Service:**
- Copy the speedfans.service file to the systemd directory:
```
sudo cp speedfans.service /etc/systemd/system/
```
- Reload systemd to recognize the new service:
```
sudo systemctl daemon-reload
```
- Enable and start the service:
```
sudo systemctl enable speedfans
sudo systemctl start speedfans
```

# Usage
- **Check Service Status:**
```
sudo systemctl status speedfans
```
- **View Logs:**
```
sudo journalctl -u speedfans
```

# Safety Notice
Improper configuration of fan speeds can lead to overheating and potential hardware damage. Ensure that temperature thresholds and fan speed settings are appropriate for your server's operating environment. Regularly monitor system temperatures to maintain hardware integrity.

# Acknowledgements
This project is inspired by various community contributions aimed at optimizing fan control for Dell PowerEdge servers. Notable references include:

- [Dell PowerEdge R710 R720 Fan Noise Control Script](https://gist.github.com/kaysond/35f63c32a0a11daa9e0a53a9c200c1a4)
- [Bash script to make Dell R720xd fans a bit quieter](https://github.com/astraliens/Dell-R720xd-server-silent-fans)
- [Fan control script for Dell PowerEdge R720 (BSD/IPMI)](https://github.com/lareira-digital/fancontrol_r720)

These resources provided valuable insights into effective fan management on Dell servers.

# License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
