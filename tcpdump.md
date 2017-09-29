ស្វែងយល់អំពី**tcpdump**
==========================

![tcpdump](/img/tcpdump.png)

## <a name="pre">មាតិការ</a>

* [១. អ្វីទៅជាtcpdump?](#def)
* [២. ប្រវត្តិខ្លះៗនៃtcpdump](#history)
* [៣. គោលបំនងនៃការប្រើប្រាស់tcpdump](#uses)
* [៤. តំឡើង(install)](#install)
* [៥. ការប្រើប្រាស់គំរូខ្លះៗ](#basic)

## <a name="def">១. អ្វីទៅជាtcpdump?</a>

- **tcpdump** គឺជាpacket analyzerសាមញ្ញមួយ ដែលដំណើរការដោយcommand line។ វាអាចអោយអ្នកប្រើប្រាស់បង្ហាញ TCP/IP ហើយនឹង packets ផ្សេងទៀតដែល​ត្រូវបានបញ្ជូន​ ឫក៏ទទួលពីnetworkដែលកុំព្យូទ័រនោះភ្ជាប់ជាមួយ។
- **tcpdump**​ បង្កើតឡើងក្រោម BCD license។
- **tcpdump** អាចដំណើរការយ៉ាងល្អជាមួយប្រព័ន្ធប្រតិបត្តិការ `Unix-like` (Linux, Solaris, BSD, macOS, HP-UX, Android & AIX) ដោយប្រើប្រាស់​បណ្ណាល័យ(library)​ **libcap**ដើម្បីcapture packets។ ចំនែកឯtcpdump​ប្រើសំរាប់​Windowsវិញគឺ `WinDump` ដែលប្រើWinPcap​ ជាWindows portរបស់​libcap។


## <a name="history">២. ប្រវត្តិខ្លះៗនៃtcpdump</a>

កម្មវិធីនេះត្រូវបានសរសេរនៅឆ្នាំ១៩៨៨ ដោយ Van Jacobson, Sally Floyd, Vern Paxson និង Steven McCane ដែលនៅពេលនោះធ្វើការនៅ Lawrence Berkeley Laboratory Network Research Group។

## <a name="uses">៣. គោលបំនងនៃការប្រើប្រាស់tcpdump</a>
- tcpdump វាprintចេញនូវសាចរឿង(content)ដែលមាននៅក្នុងnetwork packets។ វាអាចអាន(read)packetពីnetwork interface card ឫពីpacket fileដែលរក្សា ទុក ពីមុន​មក។ tcpdumpអាចសរសេរ(write)packetទៅជាfileស្តង់ដារមួយ។
- tcpdump ក៏ត្រូវបានប្រើនៅក្នុងគោលបំនងជាក់លាក់ផងដែរ ដូចជាការចាប់យក(intercepting) និងបង្ហាញ(displaying)ការទំនាក់ទំនងរវាងអ្នកប្រើប្រាស់ ឫកុំព្យូទ័រផ្សេងៗ។​ អ្នកប្រើប្រាស់ត្រូវមានឯកសិទ្ធ(privileges) ធ្វើសកម្មភាព​នៅក្នុង​system​ ។ តាមរយៈrouter ឫ gatewayដែលunencrypted trafficដូចជាTelnet or HTTPឆ្លងកាត់ អាចប្រើtcpdumpដើម្បីមើល login IDs, password, URLs ហើយនិង​អត្ថបទ(content)នៅក្នុងwebsiteក៏ត្រូវបានមើលផងដែរ ឫក៏ជាunencryptied informationផ្សេងៗទៀត។
- អ្នកប្រើប្រាស់មានជំរើស(optionally)apply BPF-based filterដើម្បីកំនត់ចំនួន​packetsដែលអាចចាប់ដោយtcpdump។ វិធីនេះ វាrenders outputដែលអាចប្រើប្រាស់​បាននៅលើnetworkដែលមានកំរិតtrafficខ្ពស់។

## <a name="install">៤. តំឡើង(install)</a>

យើងអាចដំឡើងពី source code​ ឫប្រើប្រាស់toolដំឡើងរបស់បណ្ដារdistro Linux។ ខាងក្រោមនេះជារបៀបដំឡើងលើ Ubuntu Desktop 14.04:
```
sudo apt-get install tcpdump
```

## <a name="basic">៥. ការប្រើប្រាស់គំរូខ្លះៗ</a>

```
Note: រាល់ពេលអនុវត្តន៍អ្នកត្រូវមានសិទ្ធជា supperuser ($ sudo -i)។
```

- Capture packets
```
tcpdump
```

បន្ទប់មកអ្នកចុច `ctrl + c` ដើម្បីបញ្ឈប់។ 

*  ខាងក្រោមនេះជាកំណត់ចំនាំដែល​អ្នក​គួ​តែ​អាន​វាដើម្បីងាយយល់ពាក្យគន្លឹះមួយចំនួន:
  * When tcpdump finishes capturing packets, it will report counts of:
    * packets captured (this is the number of packets that tcpdump has received and processed);
    * packets received by filter (the meaning of this depends on the OS on which you're running tcpdump, and possibly on the way the OS was configured - if a filter was specified on the command line, on some OSes it counts packets regardless of whether they were matched by the filter expression and, even if they were matched by the filter expression, regardless of whether tcpdump has read and processed them yet, on other OSes it counts only packets that were matched by the filter expression regardless of whether tcpdump has read and processed them yet, and on other OSes it counts only packets that were matched by the filter expression and were processed by tcpdump);
    * packets dropped by kernel (this is the number of packets that were dropped, due to a lack of buffer space, by the packet capture mechanism in the OS on which tcpdump is running, if the OS reports that information to applications; if not, it will be reported as 0).
    * And there's a mailing list entry from 2009 explaining:
      * The "packets received by filter" number is the ps_recv number from a call to pcap_stats(); with BPF, that's the bs_recv number from the BIOCGSTATS ioctl. That count includes all packets that were handed to BPF; those packets might still be in a buffer that hasn't yet been read by libpcap (and thus not handed to tcpdump), or might be in a buffer that's been read by libpcap but not yet handed to tcpdump, so it can count packets that aren't reported as "captured".
![source](https://unix.stackexchange.com/questions/29367/tcpdump-packets-captured-vs-packets-received-by-filter)


- Capture ទៅលើinterfaceជាក់លាក់ណាមួយ ដោយប្រើប្រាស់flag `-i` ហើយ​ខាងក្រោយវាអ្នកវាយបញ្ចូលinterfaceដែលអ្នកចង់capture, ឧទាហរណ៍interface eth0
```
tcpdump -i eth0
```

- ប្រើប្រាស់flag `-c` ដើម្បីកំណត់ចំនួនpacketsដែលអ្នកចង់capture ហើយបន្ថែម​ចំនួនpacketsនៅខាងក្រោយវា
```
tcpdump -i eth0 -c 20
```

- Print captured packets in ASCII, អ្នកប្រើប្រាស់flag `-A` ដើម្បីបង្ហាញpacketជាទំរង់កូដASCII
```
tcpdump -i eth0 -A
```

- បង្ហាញinterfaceដែលអ្នកអាចធ្វើការcaptureនៅលើកុំព្យូទ័ររបស់អ្នក
```
tcpdump -D
```

- Capture ហើយរក្សាpacketsនៅក្នុងfile, tcpdump​មានសម្ថភាពcapture​ ហើយរក្សាលទ្ធផលរបស់វានៅក្នុងfile ` .pcap` ដោយប្រើflag `-w` បន្ទាប់មក​ឈ្មោះfileដែលអ្នកចប់រក្សា
```
tcpdump -i eth0 -w file_name.pcap
```

- Caputure IP address packets: ប្រសិនបើអ្នកចង់capture network interface​របស់អ្នក ហើយវិភាគទៅលើIP address អ្នកអាចប្រើflag `-n ` នោះវានឹងឈប់បក​ប្រែ(translate)​ IP address ទៅជាHostnames ហើយនេះអាចជៀសវាង DNS lookups
```
tcpdump -n -i eth0
```

- capture only TCP packets ដោយបន្ថែម `tcp`នៅក្នុងcommand
```
tcpdump -i eth0 -c 20 -w tcpanalyze.pcap tcp
```

- Capture packets ពីportជាក់លាក់ណាមួយ, ឧបមាថាចង់captureនៅport​ ៨០
```
tcpdump -i eth0 port 80
```

- Captureដោយយកតែ source & destination IP

Capture packets ពីIPដែលមានប្រភពមកពី IP:
```
tcpdump -i eth0 src 192.168.1.1
```
Capture packets ពីdestination IP:
```
tcpdump -i eth0 dst 192.168.1.1
```



## <a name="ref">៦. ឯកសារយោង</a>

[1] https://en.wikipedia.org/wiki/Tcpdump

[2] http://www.thegeekstuff.com/2010/08/tcpdump-command-examples

[3] https://www.hugeserver.com/kb/install-use-tcpdump-capture-packets/

[4] http://www.tcpdump.org/manpages/tcpdump.1.html

[5] https://www.cs.kau.se/cs/education/courses/dvad05/09p1/uploads/Content/dvad05-L13.pdf
