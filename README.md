IoTRaspberryPiBluemix
=====================

Connect Raspberry Pi to IBM Internet of Things in Bluemix

see Bluemix.net

1 Connect:

Download the installer from GitHub:

curl -LO https://github.com/ibm-messaging/iot-raspberrypi/releases/download/1.0.1/iot_1.0-1_armhf.deb

Install the package with:
sudo dpkg -i iot_1.0-1_armhf.deb

The iot process starts and publishes events to  IBM IoT Cloud. 
The process runs as a system service, and starts whenever Raspberry Pi starts. 
To verify the process is running, use the command:

service iot status

You can stop the iot process with the following command:

sudo service iot stop

To uninstall the package, run:

sudo dpkg -P iot

troubleshooting:  /var/log/syslog

2 Visualize

get MAC address of  Raspberry Pi with this command:

service iot getdeviceid

Enter your MAC address on this page https://developer.ibm.com/iot/recipes/simulator/


3 Connect 

Register for the IoT Beta and  add a device into an organisation

During  device registration you get file configuration information, copy these when you get them:
◦ Organization ID
◦ Device Type ID
◦ Device ID
◦ Authentication Method
◦ Authentication Token

Stop the iot process

sudo service iot stop

Type in the following command:

sudo nano /etc/iotsample-raspberrypi/device.cfg

Create a new device.cfg file at /etc/iotsample-raspberrypi, fill in  configuration file with  details 
when registering the device. 

#Device configuration file
    org = yourOrganizationCode
    type = iotsample-raspberrypi
    id = b827eba84426
    auth-method = token
    auth-token = yourAuthToken
#End of Configuration file

pres CTRL-X to save, follow steps on screen.

Start iot process for  device to start in registered mode.

sudo service iot start

4 Command Support
Now  Raspberry Pi is running in registered mode and supports receipt of commands sent by an application.

Raspberry Pi supports the Reboot Command

An application should send the command with the following details

Topic : iot-2/type/<type>/id/<id>/cmd/reboot/fmt/json
            
Payload:
        {
            delay:<numberOfMinutes>
         }

numberOfMinutes : minutes to wait before reboot of the device. If no  value, device will reboot immediately.
