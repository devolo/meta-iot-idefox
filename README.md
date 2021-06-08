# devolo IoT Gateway (Idefox)

![devolo IoI Gateway top](/docs/images/idefox_product_image_top.png)


## What?

The devolo IoT Gateway is a smart gateway for industrial IoT solutions. Running Linux on a NXP i.MX7 SoC, it provides enough agility and horsepower for versatile application in connecting your plants or devices to the internet and the cloud securely. Whether as a secure gateway to restrict access to devices in highly secure areas, or as a local data aggregator processing and forwarding machine data, or even autonomously controlling local systems, with 1GB of RAM and a 4GB eMMC flash drive, it provides the platform for you to implement your concepts for the digital transformation of your plants and facilities. It comes with three ethernet ports and offers a LTE variant for mobile communication. The local connectivity is enriched with a RS-485 bus and wMBus interface.


## Why?

Industry 4.0, smart cities, smart buildings, new mobility ... there are many areas driving the digital transformation of our world, connecting many "things" with each other and the cloud. At the same time the threat of cyber attacks is ever increasing. To take part and bring your systems into the future, you will need a gate keeper, a secure way to connect your devices, your facilities, your plants, your buildings. But it is your individual story, your application and you know it best.

The devolo IoT Gateway gives you a versatile platform to easily implement your solution. With industrial-grade hardware in a small form factor, but packing enough punch to run serious applications. It can be as easy as developing an application for a Debian-based Linux. With 4GB, there is enough flash space to install your applications, to collect measurements, logs, what ever you have. Or, if you require to run a different Linux system, maybe because you already use a different distribution, you have the freedom to adjust the system to your needs. The flexibilty is yours.

If you need tighter security, you can contact us for options. For example, the hardware has an optional security module that we can enable for your project.


## How?

To connect to the device you can SSH into it. The gateway is configured with a static IP address 192.168.137.110 on the port labelled "WAN-1". Alternatively, you can assign a dynamic IP address via DHCP to the port labelled "CLS". Then log in with SSH as the user "root" with the password "root".


The devolo IoT Gateway comes with a Debian Linux based on [ISAR](https://github.com/ilbers/isar/blob/master/doc/user_manual.md). When it has internet connection, adding a package is as easy as a "apt-get install tcpdump".


To develop your own application to run on the gateway, we provide you with a Linux SDK. The [SDK](https://github.com/ilbers/isar/blob/master/doc/user_manual.md#create-an-isar-sdk-root-filesystem) is a tarball that you unpack on your development PC. It contains a debian root filesystem which includes a cross-compiler toolchain, target libraries and headers. By simply `chroot`'ing into this, you can develop and cross-compile your application like under a normal Linux system.

#### How to?
Download the SDK tarball from the [releases](https://github.com/devolo/meta-iot-idefox/releases/latest). Create a new directory and unpack the tarball into that directory. (The tarball does *not* include a top directory.)

```bash
user@linux:~$ mkdir idefox-sdk
user@linux:~$ cd idefox-sdk
user@linux:~/idefox-sdk$ sudo tar xf ../sdk-idefox-stretch-0.1.0.tar.xz
```

Chroot into the new SDK directory after mounting the necessary runtime filesystems.
```bash
user@linux:~/idefox-sdk$ sudo ./mount_chroot.sh .
user@linux:~/idefox-sdk$ sudo chroot .
```

Let's say you are missing someting in your dev environment. You can simply install Debian packages.
```bash
root@linux:~# apt-get update
root@linux:~# apt-get install vim
root@linux:~# apt-get install libhello-dev:armhf
```

As an example let's compile `htop` to add to our gateway. Get the sources, configure for cross-compiling and then copy the resulting binary onto the device.
```bash
root@linux:~# wget --no-check-certificate https://hisham.hm/htop/releases/2.2.0/htop-2.2.0.tar.gz
root@linux:~# tar xf htop-2.2.0.tar.gz; cd htop-2.2.0
root@linux:~/htop-2.2.0# ./configure CC=arm-linux-gnueabihf-gcc --host=arm-linux-gnueabihf
root@linux:~/htop-2.2.0# make
root@linux:~/htop-2.2.0# scp htop root@192.168.137.110:
```

## Where?
If you now desire to get you hands on this new device, you can get one in the [devolo web shop](https://www.devolo.de/iot-gateway). The web page also provides more information, use cases and a data sheet. Or email us at smart@devolo.de and tell us what you need. Ask us anything and let's discuss how we can assist you to reach your goals.
