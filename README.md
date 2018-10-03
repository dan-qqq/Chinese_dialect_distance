# 汉语方言距离
[中文](#汉语方言距离)  [Eng](#chinese-dialectal-distance)  
统计了中国全部县级行政区的方言所属，以语言树的分支距离计算各县方言片之间的方言距离，再以人口加权法计算各地级行政区之间的方言距离。
代码见“DialectDist.ipynb"，具体方法和对应的输出结果文件见下文。

## 数据来源
* [汉语方言大词典 the Chinese Dialect Dictionary (CDD, 1991)](https://book.douban.com/subject/1021870/)
* [中国语言地图集 the Language Atlas of China(LAC, 2012)](https://book.douban.com/subject/3302955/)
* [中国行政区划表 modood](https://github.com/modood/Administrative-divisions-of-China)
* [第六次中国人口普查数据 Census](http://www.stats.gov.cn/tjsj/pcsj/rkpc/6rp/indexch.htm)

## 地级市间的方言距离：人口加权法
1. 统计各县的方言片，先计算县与县之间的方言距离，再用人口加权得到地级市之间的方言距离。两县之间方言距离的赋值规则如下：
    * 当两县同属一个方言片，距离为0；
    * 同一方言区不同方言片，距离为1；
    * 同一方言大区不同方言区，距离为2；
    * 同一语族不同方言大区，距离为3；
    * 同语系不同语族，距离为4
2. 用第六次人口普查数据计算得到各地级市内各县人口比例，用下方公式（Liu et al.(2015)）加权得到两两地级市间的方言距离： 
![formular](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/formula.png)
S_Ai为A市中i县的人口比例，S_Bj为B市中j县的人口比例，d_ij为两县的方言距离。 
求得的方言距离d(A,B)表示任意一个A市的人与任意一个B市的人之间方言距离的期望。

输出结果：
* [汉语方言表](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/Chinese_dialectdict_compl.csv)
* [各县方言所属](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/CH_dialect_county_compl.csv)
* [方言片间的方言距离](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/Chinese_dialect_distance.csv)
* [地级行政区间方言距离](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/CH_pref_diadist.csv)

## 参考文献
Liu, Y., Xu, X. and Xiao, Z., 2015. The Pattern of Labor Cross-dialects Migrantion_劳动力跨方言流动的倒U型模式. Economic Research Journal, (10).

## 其它涉及汉语方言亲疏关系的算法
[方言互通性指数（郑锦全，1997）](http://www.blyt.net/DOC/DOCUSE7.pdf)

# Chinese dialectal distance
Dialects for county-level divisions in China. Get dialectal distance between counties by calculating branch distance of linguistic trees, and then calculate dialectal distance between prefectures with population weighted method.
Code in "DialectDist.ipynb".

## Data source
* [汉语方言大词典 the Chinese Dialect Dictionary (CDD, 1991)](https://book.douban.com/subject/1021870/)
* [中国语言地图集 the Language Atlas of China(LAC, 2012)](https://book.douban.com/subject/3302955/)
* [中国行政区划表 modood](https://github.com/modood/Administrative-divisions-of-China)
* [第六次中国人口普查数据 Census](http://www.stats.gov.cn/tjsj/pcsj/rkpc/6rp/indexch.htm)

## Population weighted method
1. Extract county population data from census and calculate the proportion of county population in each prefecture.
2. Generate combinations of all counties and for each combination, we calculate the dialectal distance based on the following assignment rules:
* If two counties belong to the same sub-dialect group, the distance is 0 
* If two counties belong to the same dialect group, but different sub-dialect groups, the distance is 1 
* If two counties belong to the same super dialect group, but different dialect groups, then the distance is 2 
* If two counties belong to the same language branch, but different super dialect groups, the distance is 3 
* If two counties belong to different branches, the distance is then 4
3. The population proportion of county i in prefecture A is denoted by SAi, and the population proportion of county j in prefecture B by SBj. With the dialectal distance between county i and county j denoted by dij, the dialectal distance between prefecture A and prefecture B is then:
![formular](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/formula.png)
The calculated value d(A,B) can be interpreted as the expectation of dialectal distance between a random resident from prefecture A and that from prefecture B.

Outputs:
* [Chinese Dialect List](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/Chinese_dialectdict_compl.csv)
* [Dialects of counties in China](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/CH_dialect_county_compl.csv)
* [Dialectal distance between sub-dialect groups](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/Chinese_dialect_distance.csv)
* [Dialectal distance between prefectures](https://github.com/QindanUCL/Chinese_dialect_distance/blob/master/data/CH_pref_diadist.csv)

## Reference
Liu, Y., Xu, X. and Xiao, Z., 2015. The Pattern of Labor Cross-dialects Migrantion_劳动力跨方言流动的倒U型模式. Economic Research Journal, (10).

## Other dialectal distance methods
[Chinese Dialect Affinity (Cheng,1997)](http://www.blyt.net/DOC/DOCUSE7.pdf)

