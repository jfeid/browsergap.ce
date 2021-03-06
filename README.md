# BrowserGap Community Edition

Simple remote browser isolation application

The Community Edition version of the cloud-based internet isolation solution at https://browsergap.xyz

[We're on HN](https://news.ycombinator.com/item?id=21561613) :tada: 

If you're having service issues, publicly shame us [on Twitter](https://twitter.com/browsergap)

Coming here from [Awesome Chrome DevTools](https://github.com/ChromeDevTools/awesome-chrome-devtools)? Take a look at the ["Zombie Lord" connection](https://github.com/dosycorp/browsergap.ce/blob/master/zombie-lord/connection.js) and ["Translate Voodoo CRDP"](https://github.com/dosycorp/browsergap.ce/blob/master/public/translateVoodooCRDP.js) for the two files with the largest concentrations of CRDTP code.

## What is BrowserGap and Remote Browser isolation?

BrowserGap is a [remote browser isolation](https://en.wikipedia.org/wiki/Browser_isolation) product. RBI means accessing the public internet through a browser that runs in the cloud, rather than through a browser that runs on your device. This helps protect you from attacks on the web.

This protects you from nearly all web-based hacks, such as viruses, ransomware, browser and device zero day exploits, and also helps protect you from tracking, by changing your device fingerprint and IP address. 

In more detail, the browser, normally is an executable application that runs on your device (phone, laptop). In RBI, instead you connect to a thin client web application that provides an interface to a browser that runs remotely. Remotely can mean in a VPS or VPC, in a physical box, or the public cloud. 

## Why is RBI significant?

And, if you're interested, read on for more detail.

It works by providing a thin client over the web that you connect your regular browser to. The thin client provides an interface to a remote browser that you interact with the browser the public internet.

This is significant because the internet is a cesspool of attacks. Malware, ransomware, virii, tracking, exploited PDFs, ways to deliver device zero days over the web, browser zero days. All these things can lead to the security of your device and network being compromised, causing significant inconvenience, distress and loss for you.

BrowserGap and the RBI methodology acknowledges that not all threats can be detected and neutralized (such as by virus scanners), in order to face that reality, RBI adopts a "isolation" posture towards threats, effectively isolating them in the remote machine and preventing them from reaching your device.

With BrowserGap, in order to render the content of a web page, the only thing we send to your device from the remote page is pixels. So no HTML, CSS, JavaScript, etc from your browsing is ever executed on your device.

[Cloud-based internet isolation](https://www.disa.mil/-/media/Files/DISA/Fact-Sheets/Cloud-Based-Internet-Isolation-CBII-Fact-Sheet20190721.ashx?la=en&hash=5DFC2594478284991F4B005AFA41DE26AC73D84A) is another name for this security practice and it is an emerging industry. Symantec recently acquired a company in this space, and Menlo Security [was awarded](https://www.menlosecurity.com/press-releases-blog/disa-cloud-based-internet-isolation-cbii-awarded-to-the-by-light-professional-it-services-llc-and-menlo-security-team) an agreement to build a CBII prototype for DISA, after a June 2018 request for RBI solutions that could eventually serve [60% of DoD's](https://secureview.cloudbrowser.xyz/uploads/fileajqk.kkpgdih.pdf.html)[~ 3 million users](https://en.wikipedia.org/wiki/Browser_isolation).

## Use

Download the repository and self-host on your own machine (at home, or in a VPS, VPC or the public cloud)

### E.g on Debian

```sh
sudo apt update && sudo apt -y upgrade
sudo apt install -y curl git wget
git clone https://github.com/dosycorp/browsergap.ce.git
cd browsergap.ce
./setup_machine.sh
npm test
```

Or (using docker build yourself)

```sh
sudo apt update && sudo apt -y upgrade
sudo apt install -y curl git wget
git clone https://github.com/dosycorp/browsergap.ce.git
cd browsergap.ce
./buld_docker.sh
./run_docker.sh 
```

Or (using docker pull from hub)

```sh
docker pull dosyago/browsergapce:1.0
curl -o chrome.json https://raw.githubusercontent.com/dosycorp/browsergap.ce/master/chrome.json
sudo su -c "echo 'kernel.unprivileged_userns_clone=1' > /etc/sysctl.d/00-local-userns.conf"
sudo su -c "echo 'net.ipv4.ip_forward=1' > /etc/sysctl.d/01-network-ipv4.conf"
sudo sysctl -p
sudo docker run -d -p 8002:8002 --security-opt seccomp=$(pwd)/chrome.json browsergapce:1.0
```

And visit http://<your ip>:8002 to see it up.

Or

Try for free at https://free.cloudbrowser.xyz

Or https://hk.cloudbrowser.xyz (if you're in Asia-Pac this is probably faster)

Are you unwilling to invest more time in your security? 

Please email me at cris@dosyago.com if you want to spend more time on your security.

### Detailed Instructions

An annotated transcript of an install is available at [this gist](https://gist.github.com/crislin2046/2fcd103234f93376c44d110d6295f32a).
