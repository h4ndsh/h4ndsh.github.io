# DIY LAN Turtle - Building a Stealth Remote Access Device


# Summary

This post details how to build a DIY stealth remote access device using the Luckfox Pico Max RV1106, inspired by the commercial LAN Turtle but at a fraction of the cost. We'll cover everything from hardware selection and OS installation to setting up secure remote access using Twingate VPN, making it perfect for security professionals and network administrators who need reliable remote access without complex port forwarding or traditional VPN setups.

# Introduction 🎯

Every security professional knows the value of reliable remote access to local networks. While solutions like port forwarding and traditional VPNs exist, they often come with their own set of complications and security concerns. This project was born from the need to access local networks remotely without the hassle of router configuration or complex VPN server setups.

The commercial [LAN Turtle](https://shop.hak5.org/products/lan-turtle) already offers these capabilities, but at a premium price point. This project aims to create a similar solution at a more affordable price while providing an excellent learning opportunity. After all, the best way to understand a tool is to build one yourself! 

# Hardware Selection 🛠️

After careful consideration, I chose the [Luckfox Pico Max RV1106](https://www.luckfox.com/EN-Luckfox-Pico-Max) as the heart of this project. This compact powerhouse offers an impressive set of features at a remarkably affordable price point.

## Specifications

| **Component**         | **Details**                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **Processor**         | Cortex A7 @ 1.2GHz                                                         |
| **NPU**               | **Pro:** 0.5 TOPS, supports int4, int8, and int16                         |
|                       | **Max:** 1 TOPS, supports int4, int8, and int16                           |
| **ISP**               | Input 5M @30fps (Max)                                                     |
| **Memory**            | **Pro:** 128MB DDR2                                                       |
|                       | **Max:** 256MB DDR2                                                       |
| **USB**               | USB 2.0 Host/Device                                                       |
| **Camera**            | MIPI CSI 2-lane                                                           |
| **GPIO**              | 26 × GPIO pins                                                            |
| **Ethernet Port**     | 10/100M Ethernet controller and embedded PHY                              |
| **Default Storage**   | SPI NAND FLASH (256MB)                                                    |

While it lacks some features like PoE and Gigabit Ethernet, the price-to-performance ratio makes it an excellent choice for this project.

![LuckFox GPIO](Luckfox-Pico-Pro-details-inter.jpg "LuckFox GPIO")

## Shopping List 🛍️

- [Luckfox Pico Max RV1106](https://www.luckfox.com/EN-Luckfox-Pico-Max) - €18
- 64GB microSD card - €10
- microSD to USB adapter - €2

## Alternative Hardware Options 

For those looking to experiment with different hardware, consider these alternatives:

- [Raspberry Pi Zero W](https://www.raspberrypi.org/products/raspberry-pi-zero-w/) + USB Ethernet
- [Orange Pi Zero 3](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-Zero-3.html)
- [GL.iNet GL-MT300N V2](https://www.gl-inet.com/products/gl-mt300n-v2/)

# Getting Started 🚀

Let's dive into setting up our device. All testing was performed on Linux, but the process should be similar on other operating systems.

## Setting Up the SDK

First, we need to prepare our development environment. Follow these steps to get the SDK ready:

```bash
sudo apt update

sudo apt-get install -y git ssh make gcc gcc-multilib g++-multilib module-assistant expect g++ gawk texinfo libssl-dev bison flex fakeroot cmake unzip gperf autoconf device-tree-compiler libncurses5-dev pkg-config bc python-is-python3 passwd openssl openssh-server openssh-client vim file cpio rsync
```

```bash
git clone https://github.com/LuckfoxTECH/luckfox-pico.git
cd luckfox-pico
./build.sh lunch
```

When running the lunch script, select:
- RV1106 board [6]
- SD Card boot [0]
- Ubuntu OS [1]

## Building the Operating System ⚙️

A special note: The default kernel needs modification to support our VPN service. Here's how to enable the required UTS namespace:

```bash
./build.sh kernelconfig
```

Navigate to:
```bash
-> General setup
-> Namespaces support (NAMESPACES [=Y])  
[*] UTS namespace (NEW) 
```

Save the configuration and build the kernel. The output files will be stored in `luckfox-pico/output/image/`.

## OS Installation 💾

I've provided the compiled files [here](./image.tar.xz) for convenience. Extract them with:
```bash
tar -xvf image.tar.xz
```

For installation, I used a Windows VM and the `SocToolKit` software provided in the SDK (`luckfox-pico/tools/windows/SocToolKit`). The interface is straightforward - just select your compiled image files and target microSD card. For detailed instructions, check the [official documentation](https://wiki.luckfox.com/Luckfox-Pico/Luckfox-Pico-quick-start/SD-Card-burn-image).

## VPN Setup 🔒

![Twingate](./Twingate_Logo.jpeg "Twingate")

For remote access, we're using [Twingate](https://www.twingate.com), which offers a generous free tier perfect for this project.

1. Create a Twingate account
2. Create a new Network [(Network > Remote Networks > + Remote Network - select "other")](https://h4ndsh.twingate.com/networks?sortBy=name)
3. Add a Connector (Network > "network name" > + Add Connector)
4. Install the Connector on your Luckfox Pico ("Inside Connector" > Linux > Generate Tokens > Copy Command)
5. SSH into the Luckfox Pico and run:

```bash
curl "https://binaries.twingate.com/connector/setup.sh" | sudo TWINGATE_ACCESS_TOKEN="" TWINGATE_REFRESH_TOKEN="" TWINGATE_NETWORK="h4ndsh" TWINGATE_LABEL_DEPLOYED_BY="linux" bash
```

## Client Setup 💻

1. Install the client:
```bash
curl -s https://binaries.twingate.com/client/linux/install.sh | sudo bash
```

2. Configure:
```bash
twingate setup
```

3. Start the service:
```bash
twingate start
```

## Resources Configuration 🎯

Add resources through the Twingate dashboard [(Network > Resources > + Resource)](https://h4ndsh.twingate.com/resources?sortBy=name)

# Testing Your Setup 🧪

Start by adding SSH access to your Luckfox Pico as a resource. Then, scan your network for potential targets:

```bash
nmap -sn -Sv x.x.x.x/24
```

Add additional resources like RDP or VNC as needed.

# 3D Printed Case 🖨️

To protect your device and make it more portable, consider printing a case. Here are some great options:

- [Thingiverse Model](https://www.thingiverse.com/thing:6670447)
- [Printables Model](https://www.printables.com/model/945919-luckfox-pico-promax-rv1106-case-pico-plusmini-rv11?lang=en)

# Future Improvements 🚀

- [ ] ESP32 integration
- [ ] Battery installation
- [ ] RTC implementation
- [ ] Penetration testing scripts
- [ ] Custom OS with ESP32, security tools, and testing scripts

</br>

<center>
  <img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExdXFxNWN6YnN0dmtjcHJjOGVzYzF6MnRqZTU0MG5oY3B1N2p1Y3QxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/mQG644PY8O7rG/giphy.gif" width="60%" height="60%" class="center"/>
</center>
