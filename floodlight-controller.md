Floodlight controller
=====================

មាតិការអត្ថបទ
=============


## ១.សេចក្ដីណែនាំអំពីfloodlight

នៅពេលដែលអ្នកចាប់ផ្ដើមស្រាវជ្រាវអំពី Software-Defined Networking (SDN) នោះអ្នកនឹងត្រូវស្វែងយល់អំពីcontroller។ SDN សព្វថ្ងៃមានcontroller ជាច្រើន​ ហើយក្នុងនោះដែក៏មានfloodlight។

Floodlight ជាopensource SDN controllerឈានមុខមួយ។ Floodlight គាំទ្រដោយសមាគមន៍នៃអ្នកអភិវឌ្ឍមួយ ក្នុងនោះក៏មានវិស្វករមួយចំនួនមកពី Big Switch Networks (http://www.bigswitch.com/)។

OpenFlow ជាopen standard គ្រប់គ្រងដោយ Open Networking Foundation (ONF)។ វាជាprotocolជាក់លាក់មួយតាមរយៈswitch គឺremote controller​ ក៏អាចmodifyសកម្មភាពបស់ឧបករណ៍បណ្ដាញ ដែលកំណត់ដោយ "forwarding instruction set"។ Floodlight ត្រូវបានបង្កើតឡើងដើម្បីជួយក្នងការដែលមានភាពកើនឡើងនៃ switches, routers, virtual switches & access points ដែលsupport the OpenFlow standard។

Floodlight v.12 ចេញមកក្រោយពីពេល មានកំណែរលំអ v1.1 មានដូចជា​ម៉ូឌុលcoreមានភាពប្រសើឡើង ដោយមានបូកបញ្ចូលនឹងមុខងារជាច្រើន ដូចជាម៉ូឌុលឧបករណ៍ topology ហើយនឹងម៉ូឌុលForwarding ត្រូវបានសរសេរឡើងវិញ។ ម៉ូឌុលStatisticsផ្ដល់អោយនូវចំនួនទិន្ន័យស្ថិតិពី​bandwidtរបស់port ព្រមទាំងmultithreading ហើយនឹងការប្រមូលស្ថិតិ ដូជា IPv6, Link-latency, OF-DPA, message listeners នឹងមុខងារផ្សេងទៀតត្រូវបានលើកឡើង។ ជំនាន់នេះអ្នកអាចរកឃើញនៅ៖

https://floodlight.atlassian.net/wiki/display/floodlightcontroller/Floodlight+v1.2

Floodlight v1.2 supportទាំស្រុងសំរាប់ OpenFlow 1.0 និង 1.3។ ស្របពេលនោះដែរ ក៏supportជាលក្ខណៈតេស្តសំរាប់ OpenFlow version 1.1, 1.2, & 1.4។ ខាងក្រោមនេះ ជាចំនុចសំខាន់ៗ​ចំនួនសំរាប់​Floodlight v1.2 ផ្ដល់អោយ និងរបៀបដែលអ្នកអាចប្រើប្រាស់វា៖

* គោលសំខាន់របស់OpenFlowJ-Loxigen (ឫ OpenFlowJ-Loxi) ត្រូវបានបង្កើតឡើងដោយបណ្ណល័យ (library) Java ដែលក្នុងចំនោមផ្នែកដែលមានសក្ដានុពលជាច្រើនទាញយកកំណែ OpenFlow នៅពីក្រោយAPIរួម។ Loxigenធ្វើការដោយវិភាគទៅលើសញ្ញាណ​OpenFlowដែលត្រូវបានកំណត់ជារចនាសម្ពន្ធនៅក្នុងសំណុំinput files។ បន្ទាប់់មកវាបង្កើតជាសំណុំបណ្ណល័យ Java, Python, & C​ សំរាប់ប្រើនៅក្នុងOpenFlow application។ បណ្ណាល័យដែលបង្កើតដោយ Loxigenប្រមូលផ្ដុំពត័មានlow-levelដោយលំអិត និងផ្ដល់បទពិសោធន៍ hight-level programming សំរាប់អ្នកអភិវឌ្ឍន៍។ ដំណើរកំណត់OpenFlow versionនៅក្នុងLoxigen's input fileក្លាយជាមានភាពងាយស្រួលជាង ហើយជំនាន់OpenFlowនិមួយៗត្រូវបានបង្ហាញតាមរយៈAPIរួម។ គំរោងLoxigen ជាopensource ហើយក៏អាចស្វែងរកនៅលើGitHub (http://github.com/floodlight/loxigen/wiki/OpenFlowJ-Loxi)។


## ឯកាសារយោង

[1] https://github.com/floodlight/floodlight

