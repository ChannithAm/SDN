## បញ្ជីមុខអត្ថបទ
### 1. Mininet
- គឺជាកម្មវិធីសំរាប់ធ្វើត្រាប់តាមបណ្ដាញជាក់ស្ដែង (Network Emulatior)​ ដែលអាចអោយអ្នកសិក្សាស្រាវជ្រាវ ធ្វើតេស្តសាកល្បង អភិវឌ្ឍន៍ បណ្ដារបណ្ដាញធំៗ នៅលើកុំព្យូទ័រតែមួយ។ Mininet​ ដំណើរការទាំង end-hosts, switches, router ហើយនឹង Links នៅលើប្រពន្ធ័ប្រតិបត្តិការតែមួយ ដែលមានលក្ខណៈដូចទៅនឹងម៉ាសុីនជាក់ស្ដែង ដោយយើងអាច `ssh`​ ទៅលើ hosts នីមួយៗបាន។
- និយាយជារួមទៅ mininet អាចនិមិត្តកម្ម hosts, switches, links និង controllers នៅលើកុំព្យូទ័តែមួយ​ -គ្រាន់តែប្រើប្រាស់ software ជំនួស hardware។ សំរាប់លក្ខណៈរបស់ឧបករណ៍និមួយៗ វាមានភាពស្រដៀងគ្នាទៅនឹងឧបករណ៍ពិតៗតែម្ដង ហើយយើងមានភាពងាយស្រួលនឹងសាកល្បងបង្កើតទំរង់បណ្ដាញ (topo) ផ្សេងៗគ្នា។

### 2. ភាពងាយស្រួលរបស់Mininet:
  * វាលឿន -ចាប់ផ្ដើមជាមួយនឹងបណ្ដាញសាមញ្ញជាមួយនឹងពេលវេលាយ៉ាងខ្លី។ មានន័យថាអ្នកអាចដំណើការ ឫក៏ debug យ៉ាងឆាប់រហ័ស។
  * បង្កើត custom topologies: switch 1, larger internet-like topologies, a data center, ឫក៏ទំរង់ណាមួយដែលអ្នកត្រូវការ។
  * ដំណើរការកម្មវិធីពិត: អ្វីដែលដំណើរការនៅលើប្រពន្ធតិបត្តិការ Linux គឺអាចធ្វើបាន។ ពីWeb servers ទៅកាន់ TCP window ដំឡើង Wireshark ដើម្បីវិភាគពត័មាន។
  * កែ packet forwarding: Switches​ របស់ Mininet គឺអាចសរសេរកម្មវិធី ដោយប្រើប្រាស់ Openflow protocol។
  * Minient គឺជាOpen source project ដែលអាចទាញយកកូដពី https://github.com/mininet ហើយអ្នកអាចកែប្រែ​(modify it), fix bugs, file issues/feature request, and submit patches/pull request។
  * ងាយស្រួលដំឡើង: អ្នកអាចដំឡើងវានៅលើកុំព្យូទ័ររបស់អ្នក។ ដោយប្រើប្រាស់ VM (Virtual Machine) ឫដំឡើងផ្ទាល់នៅលើកុំព្យូទ័រដែលមានប្រពន្ធប្រតិបត្តិការ Linux។
  * អាចយកប្រពន្ធ័ទាំងនេះមកអនុវត្តផ្ទាល់នៅលើបណ្ដាញជាក់ស្ដែង ដោយមិនចាំបាច់កែកូដនៅឡើយ។
  * Mininet មានផ្ដល់នៅ Python API ងាយប្រើប្រាស់ និងអាចពង្រីកបន្ថែម។
### 3. ចំនុចខ្វះខាត ឫភាពមានកំណត់របស់ Mininet
(មានពេលនឹងបន្ត...)
### 4. របៀបដំឡើងMininet
...យើងអាចដំឡើងបាន៤របៀប តែខ្ញុំសូមលើកយកមួយរបៀបមួយគឺ ដំឡើងពីsource នៅលើUbuntu 16.04
(សំរាប់សេចក្ដីលំអិតសូមចូលទៅកាន់[ទីនេះ](http://mininet.org/download/))
  * Install git
> sudo apt-get install git
  * Get the source code
> git clone git://github.com/mininet/mininet
  * ចូលទៅកាន់mininet directory
> cd mininet

> git tag #ដើម្បីមើលជំនាន់ដែលអាចដំឡើង

> git checkout -b 2.2.1 2.2.1  # ឫក៏ជំនាន់ណាមួយដែលអ្នកចង់បាន

> cd ..

  * Install Mininet
> mininet/util/install.sh -a
  * សាកល្បងបង្កើតtopo
> sudo mn --test pingall

### <a namme="command">៥. The mininet command cheat sheet</a>
- Runs the default minimal topology which include the Openflow kernel switch connected two hostss with the reference controller:
> Mininet> sudo mn

- To get the help
> Mininet> help

- To displays the nodes of the network:
> Minint> nodes

- To displays the links of a network
> Mininet> net

- To dump information about all nodes
> Mininet> dump

-To test connectivity between hosts
> Mininet> h1 `ping` c1 h2

- To separate terminals for node h1 and h2
> Mininet> xterm h1 h2

- To open the Wireshark network packet analyzer tool to monitor and analyse the behaviour of incoming and outgoing packets
> Mininet> wireshark &

- A few performance modeling commands in Mininet
```
  * The folowing command establishes the transmission controll link with the CPU limited hosts:

  net = Mininet(link=TCLink, host=CPULimitedHost)
  # កំណត់ link bandwidth និង add delay

  * To set the links bandwidth and delay timing
  
  net.addLink(h2, s1, bw=10, delay=50ms)

```

- To exit from the command line interface (CLI)
> Mininet> exit

- To clean up the Mininet network configuration
> Mininet> sudo mn -c






















*References*

[1] http://netseminar.stanford.edu/seminars/11_14_13.pdf

[2] http://conferences.sigcomm.org/sigcomm/2014/doc/slides/mininet-intro.pdf

[3] https://github.com/mininet/mininet/wiki/Introduction-to-Mininet

[4] http://costiser.ro/2014/08/07/sdn-lesson-1-introduction-to-mininet/#.WYA_gCdLdxA

[5] http://opensourceforu.com/2015/10/mininet-an-emulator-for-prototyping-large-network-topologies-on-a-single-machine/
