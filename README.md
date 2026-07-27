*This project was created as part of the 42 curriculum by vgoh*

# NetPractice #

## Description ###

NetPractice is a project focused on understanding TCP/IP addressing works in a network that includes routers and switches, where learners have to complete 10 levels, each with a non-functioning network diagram displayed. The goal of each level is to adjust the available configuration so that the network functions properly.

### TCP/IP and OSI Models ###

Transmission Control Protocol (TCP) and OSI (Open Systems Interconnection) are frameworks for organizing networking into layers, with the former being the real world architecture and the latter being a teaching/reference model. Layers are counted from the bottom up.
  ```
                                                   TCP                OSI
                                                
            Covers the first 3 OSI layers  ——  Application        Application  —— Creates the data (HTTP, FTP, SMTP)
                                                    |                  |
                                  TCP, UDP  ——  Transport         Presentation  —— Encrypts or formats data for the receiving device
                                                    |                  |
            Finds address using IP, Routers  ——  Network            Session  ——    Maintains connection between two devices
                                                    |                  |
           Ethernet, Switches, MAC Address  ——  Data Link          Transport  ——  Navigates to the app asking for or sending the data (TCP, UDP)
                                                    |                  |
                                     Cables  ——  Physical           Network  ——  Finds address using IP, Routers
                                                                       |
                                                                   Data Link ——  Ethernet, Switches, MAC Address
                                                                       |
                                                                    Physical  ——  Cables

```
When transferring data from one host to another, every layer adds its own bit of information from the application down to the physical layer, which is called **encapsulation**. Likewise, when data is received by another host, data will be slowly unpacked up to the application layer, known as **decapsulation**. Basically, data is transferred from one host to another through the physical layer because that's where the cables are.

### IP Addresses and Subnet Masks ###
- **IP address** - Short for Internet Protocol addresses, they are separated into two parts - a network address and a host address, and the part that belongs to each is determined by a subnet mask. NetPractice only covers IPv4 addresses. An example of an IP address is `192.168.0.2`.
- **Subnet mask** - A subnet mask reveals how many bits in an IP address are used for the network by masking the respective portion of the address. An example would be `255.255.255.0`.

Visual demonstration:
```
IP address        Binary representation (Total 32 bits)
192.168.0.2       11000000.10101000.00000000.00000010
                           Network             
Subnet mask       |||||||| |||||||| ||||||||   Host
255.255.255.0     11111111.11111111.11111111.00000000
                      └── Each segment that is separated by a '.' is called an octet
```

Essentially this means that hosts ``192.168.0.1, 192.168.0.2, 192.168.0.3...`` exist on the `192.168.0` network while remaining number is reserved for their resepective host addresses.

**CIDR notation** - Classless Inter-Domain Routing (CIDR) is a simplified way of writing subnet masks. The subnet mask `255.255.255.0` can be represented as `/24` which means 24 bits are used for the network and the remaining 8 are used for the host. The quickest way to calculate how many usable addresses a mask gives is `2^(32-CIDR number)`. With `/24` that means you have 2⁸ = 256 addresses. To represent an IP address along with its subnet mask it can be written for example as `192.168.1.0/24`.

| Subnet | Host | Subnet Mask | 
| :--- | :--- | :--- |
| 1 | 256 | /24 |
| 2 | 128 | /25 |
| 4 | 64 | /26 |
| 8 | 32 | /27 |
| 16 | 16 | /28 |
| 32 | 8 | /29 |
| 64 | 4 | /30 |
| 128 | 2 | /31 |
| 256 | 1 | /32 |

Example for ``192.168.4.0/26``:

| Network ID | Subnet Mask | Host ID Range | # of Usable Host | Broadcast ID |
|---|---|---|---|---|
| 192.168.4.0 | /26 | 192.168.4.1 - 192.168.4.62 | 62 | 192.168.4.63 |
| 192.168.4.64 | /26 | 192.168.4.65 - 192.168.4.126 | 62 | 192.168.4.127 |
| 192.168.4.128 | /26 | 192.168.4.129 - 192.168.4.190 | 62 | 192.168.4.191 |
| 192.168.4.192 | /26 | 192.168.4.193 - 192.168.4.254 | 62 | 192.168.4.255 |

``192.168.4.0`` and ``192.168.4.256`` are considered unusable addresses since the former is the network ID and the latter is the broadcast ID.

### Switches ###
A switch connects multiple devices on a single network which it cannot communicate outside of. They work on OSI layer 2, which is the data link layer, and exchange data based on MAC addresses.

### Routers ###
A router is a device that connects two different networks, acting as a gateway for a host on one network to communicate with a host on a separate network. They work on the OSI layer 3, which is the network layer, and forward data based on IP addresses.

### Default gateways ###
In most cases, a default gateway is the same thing as a router. It connects devices from two different networks, allowing them to communicate with each other. 'Default' just means that when data needs to exit a network, it is the first to be designated device to be looked at.

## Instructions

A training interface is provided on the student intra project page as well as during evaluations and requires a 42 student login to be accessed.

1. Download ``net_practice.1.9.tgz``  and extract the files with the command ``tar -xzf net_practice.1.9.tgz`` into the directory of your choice.
2. Input the command ``bash run.sh`` in the terminal. This shell script will launch a web server and open your preferred web browser to the dedicated page.
3. For each level, a non-functioning network diagram is displayed.
  At the top of your window, you will see one or more objectives that you must achieve by adjusting the available configuration so that the network functions properly.
  There are two buttons you can use:
   - ``[Check again]`` to verify whether your configuration is correct.
   - ``[Get my config]`` to download your configuration whenever you need to. This prompts a download of a .json file with the configuration made by the student.
4.  A  ``[Next level]`` button will appear next to the two buttons if the correct network configuration has been achieved. Once the 10 levels are completed, the student may choose to do evaluation preparation with randomized configuration exercises from the existing pool.

### Submission Details 

The .json config files created for each of the 10 levels are required to be included at the root of the learner's repository upon submission of the project.

## Resources

- [CertBros - OSI Model Explained | Real World Example](https://youtu.be/LANW3m7UgWs?si=KruXDKflZIFPVfLN)
- [CertBros - TCP/IP Model Explained | Cisco CCNA 200-301](https://youtu.be/OTwp3xtd4dg?si=3Snwca5KhppTxDvr)
- [Drunk Engineer - OSI and TCP IP Models - Best Explanation](https://youtu.be/3b_TAYtzuho?si=kVmebpFOe0FM2muy)
- [QSFPTEK- Router vs Switch, Whats the Difference?](https://youtu.be/AjOyXHWG_x0?si=HCeaQxNtvGws2M7e)
- [PowerCert Animated Videos - Default Gateway Explained](https://youtu.be/pCcJFdYNamc?si=-hPc9t30WpoEPSrk)
- [Sunny Classroom - subnetting is simple](https://youtu.be/ecCuyq-Wprc?si=ITWq0Tku3mSKx-LV)
