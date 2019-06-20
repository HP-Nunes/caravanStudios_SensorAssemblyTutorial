<a href="https://www.caravanstudios.org/about" target=_blank title="Caravan Studios"><img align="left" width="200" height="200" src="img/csLogo.png" target=_blank/>
# <center>How to build your own low-cost air monitoring sensor: A Step-by-Step Tutorial</center>
<br>
<br>

## Open-source Software and Hardware Collaborators
<div>
<a href="https://luftdaten.info/kontakt/" target=_blank title="Luftdaten's contact page" target=_blank><img align="center" src="img/luftdatenLogo.png" width="200"/></a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href="https://www.arduino.cc/en/Main/FAQ#toc2" target=_blank><img align="center" src="img/ArduinoCommunityLogo.png" width="250" title="Arduino" target=_blank/></a> 
</div>
  
## Objective
Using the Arduino's ESP8266 Board, an SDH11 Dust Sensor, and a DHT22 Humidity Sensor, flash firmware from <a href="https://luftdaten.info/en/home-en/" target=_blank>Luftdaten</a>--a Code for Germany project--to collect air particle pollution (PM) data.

## About Fine Particle Pollution
Background on <b>PM</b> from the <a href="https://www.airnow.gov/index.cfm?action=aqibasics.particle" target=_blank>EPA</a>:
> Particle pollution, also called particulate matter or PM, is a mixture of solids and liquid droplets floating in the air. Some particles are released directly from a specific source, while others form in complicated chemical reactions in the atmosphere.
Particles come in a wide range of sizes. Particles less than or equal to 10 micrometers in diameter are so small that they can get into the lungs, potentially causing serious health problems. Ten micrometers is less than the width of a single human hair.
>* Coarse dust particles (PM10) are 2.5 to 10 micrometers in diameter. Sources include crushing or grinding operations and dust stirred up by vehicles on roads.
>* Fine particles (PM2.5) are 2.5 micrometers in diameter or smaller, and can only be seen with an electron microscope. Fine particles are produced from all types of combustion, including motor vehicles, power plants, residential wood burning, forest fires, agricultural burning, and some industrial processes.

<a href="https://www.airnow.gov/index.cfm?action=aqibasics.particle" target=_blank title="AirNow"><img align='center' width="500" height="400" src="https://www.airnow.gov/images/pmwidthgraphic.jpg">

## Materials Needed and Cost Estimates
### <center>Estimated Cost (U.S. Dollar, 2019)</center>

ID | Components | [Amazon](https://www.amazon.com/) | [AliExpress](https://www.aliexpress.com/) | [Bang Good](https://www.banggood.com/)
---------- | ---------- | ---------- | ---------- | ----------
1 |**ESP8266 NodeMCU** | [8.39](https://www.amazon.com/HiLetgo-Internet-Development-Wireless-Micropython/dp/B010N1SPRK/ref=sr_1_fkmr1_1?ie=UTF8&qid=1531435207&sr=8-1-fkmr1&keywords=NodeMCU+ESP8266%2C+CPU%2FWLAN) | [2.10](https://www.aliexpress.com/item/V2-4M-4FLASH-NodeMcu-Lua-WIFI-Networking-development-board-Based-ESP8266/32647690484.html?spm=2114.search0104.3.3.4b42611dnjxtKv&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=183e6096-c759-41fc-852d-729d2a62f662-0&algo_pvid=183e6096-c759-41fc-852d-729d2a62f662&transAbTest=ae803_3) | [6.33](https://www.banggood.com/NodeMcu-Lua-WIFI-Internet-Things-Development-Board-Based-ESP8266-CP2102-Wireless-Module-p-1097112.html?rmmds=search&cur_warehouse=USA)
2 |**Nova PM Sensor SDS01** | [40.38](https://www.amazon.com/SHAPB-Precision-Quality-Detection-Sensors/dp/B07P8THRKF/ref=sr_1_fkmr0_1?keywords=Nova+PM+Sensor+SDS01&qid=1557251736&s=gateway&sr=8-1-fkmr0) | [16.40](https://www.aliexpress.com/item/Nova-PM-sensor-SDS011-High-precision-laser-pm2-5-air-quality-detection-sensor-module-Super-dust/32894938003.html?spm=2114.search0104.3.2.3e406beb9tLZpo&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=c2725975-415a-4c8e-a391-d06089ff037a-0&algo_pvid=c2725975-415a-4c8e-a391-d06089ff037a&transAbTest=ae803_3) | [19.99](https://www.banggood.com/Geekcreit-Nova-PM-Sensor-SDS011-High-Precision-Laser-PM2_5-Air-Quality-Detection-Sensor-Module-Tester-p-1144246.html?akmClientCountry=America&stayold=1&cur_warehouse=CN)
3 |**DHT22 Temperature Humidity Sensor** |[12.90](https://www.amazon.com/Gowoops-Temperature-Humidity-Measurement-Raspberry/dp/B073F472JL/ref=sr_1_3?ie=UTF8&qid=1531772763&sr=8-3&keywords=DHT22%2C+temperature+%26+humidity) | [2.45](https://www.aliexpress.com/item/Digital-Temperature-and-Humidity-Sensor-DHT11-DHT22-AM2302B-AM2301-AM2320-Temperature-and-Humidity-Sensor-For-Arduino/32901733917.html?spm=2114.search0104.3.3.743c28ectzbY9s&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=d8fa3558-d481-43e4-bb6c-8a76ee6f36d9-0&algo_pvid=d8fa3558-d481-43e4-bb6c-8a76ee6f36d9&transAbTest=ae803_3)|[6.53](https://www.banggood.com/Wholesale-DHT22-AM2302-Digital-Temperature-Humidity-Sensor-Replace-SHT11-SHT15-Logger-p-47240.html?rmmds=search&cur_warehouse=USA)
4 |**Dupont Cables (female-to-female)** |[6.98](https://www.amazon.com/EDGELEC-Breadboard-Optional-Assorted-Multicolored/dp/B07GD312VG/ref=sr_1_3?keywords=dupont%2Bcables%2Bfemale&qid=1555004496&s=gateway&sr=8-3&th=1) | [0.45](https://www.aliexpress.com/item/Dupont-Jumper-wire-10CM-20CM-30CM-Male-to-Male-Female-to-Male-Female-to-Female-Jumper/32962785036.html?spm=2114.search0104.3.3.b1917b69tJuUn7&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=0522aa0a-90d1-49b4-b960-2457aa198629-0&algo_pvid=0522aa0a-90d1-49b4-b960-2457aa198629&transAbTest=ae803_3)|[3.96](https://www.banggood.com/40pcs-20cm-Female-to-Female-Jumper-Cable-Dupont-Wire-For-Arduino-p-75612.html?rmmds=search&cur_warehouse=USA)
5 |**Flat Micro USB Cable 2.1A (< 1m)** |[2.27](https://www.amazon.com/gp/offer-listing/B07RDKT23C/ref=dp_olp_0?ie=UTF8&condition=all&qid=1557254394&sr=8-1) | [1.00](https://www.aliexpress.com/item/Essager-Flat-Micro-USB-Cable-For-Xiaomi-Redmi-Samsung-2-4A-Fast-Charging-Microusb-Data-Charger/32902424617.html?spm=2114.search0104.3.3.4eee4e5f5LscMj&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=a32e3f37-73a0-448a-9893-e4596054bbdb-0&algo_pvid=a32e3f37-73a0-448a-9893-e4596054bbdb&transAbTest=ae803_3)|[3.22](https://www.banggood.com/Blitzwolf-BW-MT2-Micro-USB-Flat-Fast-Charging-Data-Cable-With-Type-C-Adapter-For-Phone-Tablet-p-1383475.html?rmmds=search&ID=45763&cur_warehouse=CN)
5 |**Flat Micro USB Cable 2.1A (Nylon, >=2m)** |[9.69](https://www.amazon.com/iSeekerKit-charger-Charging-Samsung-Motorola/dp/B01EL6YDUQ/ref=sr_1_4?keywords=Flat+Micro+USB+Cable+2.1A+nylon&qid=1557254554&s=gateway&sr=8-4) | [3.99](https://www.aliexpress.com/item/Remax-Flat-Micro-USB-Cable-2-1A-1m-Fast-Charging-Nylon-USB-Sync-Data-Mobile-Phone/32951139559.html?spm=2114.search0104.3.3.70254a02LR9JFY&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=de539cc2-1a41-40a7-b136-b7457831da1c-0&algo_pvid=de539cc2-1a41-40a7-b136-b7457831da1c&transAbTest=ae803_3)|[2.89](https://www.banggood.com/--p-1459267.html?akmClientCountry=America&rmmds=search&ID=22444706&cur_warehouse=CN)
6 |**USB to Wall Charger** |[10.99](https://www.amazon.com/Charger-3-Pack-Adapter-Samsung-Motorola/dp/B07437M5QQ/ref=sr_1_4?ie=UTF8&qid=1531775014&sr=8-4&keywords=usb+power+adapter) |[1.28](https://www.aliexpress.com/item/Dual-USB-Cell-Mobile-Phone-Charger-5V2-1A-1A-EU-US-Plug-Wall-Power-Adapter-for/32807780731.html?spm=2114.search0104.3.123.27695189gevSGp&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=b8328427-a08d-4bed-9a42-50d1345ca12b-16&algo_pvid=b8328427-a08d-4bed-9a42-50d1345ca12b&transAbTest=ae803_3)|[3.60](https://www.banggood.com/Mini-USB-5V1A-Home-Travel-Wall-Charger-Power-Charging-Adapter-US-plug-p-1017168.html?rmmds=search&ID=513872&cur_warehouse=USA)
7 |**10 X 12mm Silicone Tube** |[5.99](https://www.amazon.com/uxcell-Silicone-Flexible-Translucent-Transfer/dp/B01N3YIQ0Y/ref=sr_1_9?keywords=silicone+tube&qid=1555955060&s=gateway&sr=8-9) | [6.21](https://www.aliexpress.com/item/6-4-7-8-9-10-mm-x-9-10-11-12-13-14-mm-Transparent/32988340459.html?spm=2114.search0104.3.8.5f7e26350wWfig&ws_ab_test=searchweb0_0,searchweb201602_4_10065_10130_10068_10890_10547_319_10546_317_10548_10545_10696_453_10084_454_10083_10618_10307_537_536_10059_10884_10887_321_322_10103,searchweb201603_52,ppcSwitch_0&algo_expid=9c7ca7c6-680b-43f8-859b-ef04f86b21cb-1&algo_pvid=9c7ca7c6-680b-43f8-859b-ef04f86b21cb&transAbTest=ae803_3) | [5.53](https://www.banggood.com/5M-Silicon-Tube-5mm8mm10mm12mm15mm-for-WS2812B-5050-3528-2835-5630-LED-Strip-Light-p-1007818.html?rmmds=search&ID=3632&cur_warehouse=CN)
8 |**90° PVC Pipes (3 inch / 2.55 cm)** |[8.07](https://www.amazon.com/NDS-3P02-3-Inch-Sewer-90-Degree/dp/B00HXHALO8/ref=sr_1_1?s=lawn-garden&ie=UTF8&qid=1531767949&sr=1-1&keywords=90+Degree+PVC+Pipe+3inch) | N/A|N/A
<br>

The total may range from an estimated minimum of <b>40.17</b> to an estimated maximum of <b>106.61</b> US Dollars (not including shipping).

## 
<img align="center" width="600" height="600" src="img/goodjob1.gif">
