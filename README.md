Ze-filter
=========

Sample Etterfilter script to inject additional html code on LAN traffic. The etterfilter utility is used to compile source filter files into binary filter files that can be interpreted by the JIT interpreter in the ettercap filter engine. You have to compile your filter scripts in order to use them in ettercap. All syntax/parse errors will be checked at compile time, so you will be sure to produce a correct binary filter for ettercap. 

Deps:
----------
Ettercap (Installing Ettercap will include ettercapfilter). Ettercap is sort of the Swiss army knife of ARP poisoning and network sniffing. Ettercap can be extended by using filters and plug-ins, making it able to do all sorts of neat network tasks.

What ftw! iz teh sample script?
----------------------------
The script is to demo the ability to use Etterfilter as a Social Engeniering tool while doing a simple Pentest. 
Assume you want to present a trojan to a victim, make him/her install it as to gain access into their machine.

While in the same network with the victim(s), you can add some additional html code to any webpage they visit. So, for instance, we can tell the victims their "Adobe Flash Player" is outdated and provide our trojan as the updated version of adobe flash player for download? Why not :) ?

How to test the script
--------------------------
There are two approches to test the concept above.

1. We can aim to replace any ``` "</title>" with "</title><then our additional HTML goes here>" ```
2. Or simply write a separate html file with the additional code e.g. some form and aim to 
    replace any ```"</title>" with "</title><iframe src=the-file.html></iframe>"```

To test for the first approach, use the content in *form folder* and to test for the second approach, use content in *iframe folder*

Compiling
-------------
The file with .filter extention is the one to be compiled. Open it with your fav editor and make common changes like the IP address, the image source and the executable source... You can host the files in a local webserver or have them served by free online file servers.

After editing and saving the changes: Use etterfilter command to compile the file.  

*etterfilter file.filter -o file.ef* 


file.flter is the input file and -o file.ef is the output file. The compiled output file is what we are going to load with Ettercap using switch F (-F).


Runing the Script
-----------------
To run the sample filter script, just open a terminal and do: <br>

*ettercap -T -q -F file.ef -M ARP /10.0.0.6/ //*  <br> To target a specific victim  <br>

*ettercap -T -q -F file.ef -M ARP // //* <br> To target all clients in a LAN ( which is very noisy & rude :D)

![Screen Shot](./screen-shot.png)
