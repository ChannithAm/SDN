ស្វែងយល់អំពី**tcpdump**
==========================

## <a name="pre">១. មាតិការ</a>


## <a name="def">២. អ្វីទៅជាtcpdump?</a>

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

- 























## <a name="ref">ឯកសារយោង</a>

[1] https://en.wikipedia.org/wiki/Tcpdump

[2] http://www.thegeekstuff.com/2010/08/tcpdump-command-examples

[3] https://www.hugeserver.com/kb/install-use-tcpdump-capture-packets/

[4] http://www.tcpdump.org/manpages/tcpdump.1.html

[5] https://www.cs.kau.se/cs/education/courses/dvad05/09p1/uploads/Content/dvad05-L13.pdf
