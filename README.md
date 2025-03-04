# tool_get_famous_scenery_station_airport_and_their_scws_tokens
Get famous scenery/stations/airports list of China and Taiwan, then input these names to libscws to get tokens

# The input raw datas
I manually collected 100 most popular Scenery/Stations/Airport from below website for both China/Taiwan, then  put them to several raw data files:  
[China POIs]  
100 most popular scenery:  
http://chuansong.me/n/1125107  
  
[Taiwan POIs]  
100 most popular scenery:  
http://blog.xuite.net/jeanson61/xuite/41983306-%5B100%E5%B9%B4%5D%E7%99%BE%E5%B9%B4%E7%9A%84100%E5%A4%A7,+%E7%99%BE%E5%A4%A7%E6%99%AF%E9%BB%9E  
http://blog.xuite.net/tolarku/blog/43392927-%E5%8F%B0%E7%81%A3%E7%99%BE%E5%A4%A7%E6%99%AF%E9%BB%9E  
  
[China stations]  
https://zh.wikipedia.org/wiki/Category:%E4%B8%AD%E5%9C%8B%E9%90%B5%E8%B7%AF%E8%BB%8A%E7%AB%99  
https://zh.wikipedia.org/wiki/Category:%E7%89%B9%E7%AD%89%E7%AB%99  
https://zh.wikipedia.org/wiki/Category:%E4%B8%80%E7%AD%89%E7%AB%99  
  
[Taiwan stations]  
https://zh.wikipedia.org/wiki/Category:%E5%8F%B0%E7%81%A3%E9%90%B5%E8%B7%AF%E8%BB%8A%E7%AB%99  
https://zh.wikipedia.org/wiki/Category:%E8%87%BA%E7%81%A3%E9%90%B5%E8%B7%AF%E7%AE%A1%E7%90%86%E5%B1%80%E8%BB%8A%E7%AB%99  
https://zh.wikipedia.org/wiki/%E7%89%B9%E7%AD%89%E7%AB%99_(%E5%8F%B0%E9%90%B5)  
https://zh.wikipedia.org/wiki/%E4%B8%80%E7%AD%89%E7%AB%99_(%E5%8F%B0%E9%90%B5)  
  
[China airports]  
https://zh.wikipedia.org/wiki/%E4%B8%AD%E5%8D%8E%E4%BA%BA%E6%B0%91%E5%85%B1%E5%92%8C%E5%9B%BD%E6%9C%BA%E5%9C%BA%E5%88%97%E8%A1%A8  
https://zh.wikipedia.org/zh-cn/%E4%B8%AD%E5%8D%8E%E4%BA%BA%E6%B0%91%E5%85%B1%E5%92%8C%E5%9B%BD%E6%9C%BA%E5%9C%BA%E8%BF%90%E8%90%A5%E7%BB%9F%E8%AE%A1%E5%88%97%E8%A1%A8  
  
[Taiwan airports]  
https://zh.wikipedia.org/wiki/%E8%87%BA%E7%81%A3%E6%A9%9F%E5%A0%B4  
 
[Raw data files]
```sh
./inputs/airports/taiwan_airports_raw.txt
./inputs/airports/china_airports_raw.txt
./inputs/scenery/china_scenery_raw.txt
./inputs/scenery/taiwan_scenery_raw.txt
./inputs/stations/china_stations_raw.txt
./inputs/stations/taiwan_stations_raw.txt
```

# Get names
I create some python scripts to extract Scenery/Station/Airport names from the raw data files :  
```sh
./inputs/airports/extract_taiwan_airports_raw.py
./inputs/airports/extract_china_airports_raw.py
./inputs/scenery/extract_taiwan_scenery_raw.py
./inputs/scenery/extract_china_scenery_raw.py
./inputs/stations/extract_taiwan_station_raw.py
./inputs/stations/extract_china_station_raw.py
```
You can run gen_data.sh directly to get the outputs :  
```sh
$ ./gen_data.sh
$ find . -name "*_raw.txt.dump" 
./inputs/airports/taiwan_airports_raw.txt.dump
./inputs/airports/china_airports_raw.txt.dump
./inputs/scenery/taiwan_scenery_raw.txt.dump
./inputs/scenery/china_scenery_raw.txt.dump
./inputs/stations/china_stations_raw.txt.dump
./inputs/stations/taiwan_stations_raw.txt.dump
```

# Get tokens
After get Scenery/Station/Airport names, I would like to input these names to [SCWS](https://github.com/hightman/scws) to get their tokens, below are steps :  
1. Clean all previous files  
```sh
./build.sh clean
```
2. Build executable  
```sh
./build.sh
```
Executable path :  
build/scws_get_tokens  

3. Build input datas (will invoke gen_data.sh)  
```sh
./build.sh build-data
```
Input data path :  
inputs/airports/china_airports_raw.txt.dump  
inputs/airports/taiwan_airports_raw.txt.dump  
inputs/scenery/china_scenery_raw.txt.dump  
inputs/scenery/taiwan_scenery_raw.txt.dump  
inputs/stations/china_stations_raw.txt.dump  
inputs/stations/taiwan_stations_raw.txt.dump  

4. Execute
```sh
cd build
./scws_get_tokens taiwan
./scws_get_tokens china
```
Output data path :  
outputs/china/china_airports.csv  
outputs/china/china_scenery.csv  
outputs/china/china_stations.csv  
outputs/taiwan/taiwan_airports.csv  
outputs/taiwan/taiwan_scenery.csv  
outputs/taiwan/taiwan_stations.csv  

