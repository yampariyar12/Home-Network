# Home-Network
I build the file share system which can be accessed from both home network and outside network using raspberry pi

First make sure your Raspberry pi is functioning properly
The following protocol i used to implement the project:
1.OpenVPN
2.Samba
3.NFS

SETUP OPENVPN
To set up the OpenVPN. First go to pivpn website which is www.pivpn.io. You will see the url for the installation of the OpenVPN. Copy the installation. Paste the url in the terminal of the RaspberryPi. After you enter the url in the terminal , it install the package of the OpenVPN. 
Since, we are using Pi as a server, we need static IP address. In the next step, we are given the option to set up the static IP address. After setting up the Static IP address, do not forget to copy the IP address of the IP address. It will be later used to configure your router. 
After this, you will be given the option to pick the user, select the user as you want which will hold your ovpn configuration. After this, you will be asked what protocol you can use. You have option to pick UDP or TCP. Write the port number which you select. You will be asked to select the type of the encryption. The higer bit you go, the more secure you will be. You can use 256 bit which is secure. 
The next question you will be asked is important. It will asked you to select the public DNS or this public IP to connect to server. If you choose the public DNS, you need to set up your roter to public DNS provider. Most of the DNS prover charge you fees. You can use www.noip.com DNS provider for free. If you set up your hostname in one of the DNS provider, you also need to set up your Dynamic DNS of the router. 
After few configuration, you will be asked to reboot your pi. After you reboot, you successfully configured OpenVPN.
ADD THE USER
pivpn -a  #type in this command, you will be prompted to enter name and password
Enter a Name for the Client: <enter the name
Enter the password for the Client: <enter the password>

You have successfully created <your user name>.ovpn. It also create a ovpn file. This file is a certificate which is used to connect your client to the Pi using VPN tunnel. 
You can locate the file in /home/pi/opvpn. Save the certificate for later use. 
PORT FORWARDING
The port which we use for the VPN which is either TCP and UDP should be opened in the router. 

INSTALL OpenVPN IN THE CLIENT COMPUTER
After you install the OpenVPN, import the certificate you saved. You can now use username and password to connect to the PI server. 

INSTALL Samba File Share in PI and access from WINDOWS
To set up a shared folder on a Linux that Windows to access, start with installing Samba (software that provides access to SMB/CIFS protocols used by Windows). At the terminal, use the following command:
sudo apt-get install samba
smbpasswd -a <username>
New SMB password:
Retype new SMB password:

Create the directory that you’d like to share out to your Windows computer.  We’re just going to put a folder on our /home/pi/Share.
mkdir ~/home/pi/Share

Now, use your favorite editor to configure the smb.conf file. We’re using Vi here.
sudo vi /etc/smb.conf

Scroll down to the end of the file and add these lines:
Obviously, you’ll need to replace some of the values with your personal settings.  It should look something like this:
[Share]
path = /home/pi/Share
available = yes
valid users = pi
read only = no
browsable = yes
writable = yes

Save the file and close your editor.  Now, you just need to restart the SMB service for the changes to take effect.
sudo service smbd restart

To access the share from the window device
\\IP address of the Pi\Share

INSTALL XRDP and VNC and VPN TO ACCESS DESKTOP OF PI
VNC
Enter sudo raspi-config at the command prompt to access it.
Then select “Interfacing Options” from the menu.
Then select “VNC”, to enable VNC.
Install VNC Viewer in the client computer to access the PI interface. 
XRDP
Enter sudo apt-get install xrdp to install the XRDP service.
Now, on your Windows computer, open up the Remote Desktop Connection application. This is a Windows app, so it should already be on your computer. Now enter the local IP address of your Raspberry Pi to connect to the PI.


