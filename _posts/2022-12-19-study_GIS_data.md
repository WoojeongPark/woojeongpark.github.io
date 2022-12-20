---
title:  "[GIS] GIS data structure and analysis"
excerpt: "스터디-수학 위상수학 정리 "

categories: [Study, GIS]
tags:
  - [GIS, geography, shp, gwr, ols]

toc: true
toc_sticky: true
 
date: 2022-12-19
last_modified_at: 2022-12-19
math: true
comments : true
mermaid: true
---


# GIS data - preliminary and basic data structure

## Intro

도시공학적 측면에서 데이터를 기반으로 접근할 때 공간데이터(지리정보데이터)를 다뤄야 할 때가 많다.

__GIS(Geospatial Information System)__ 란, 우리가 흔히 하는 데이터가 위치에 대한 정보를 갖고 있는 것이라고 할 수 있는데 도시의 건축물 좌표(Point)나, 도로(Line), 시군구 법정동에 해당하는 영역(Polygon)이 될 수 있다.

도시 공간이라는 것은 단순히 수치적으로 파악하는 것 외에도, 지리적 위치에 따라 다른 시각으로 접근할 수 있기 때문에 공간데이터를 이해하는 것이 상당히 중요하다.

예를들어 서울특별시의 읍면동별 각종 통계자료를 갖고 있다면, 단순히 읍면동별 차이만 보는 것 보다 지도에 mapping하여 인접한 읍면동이 어디인지(지리적 인접성), 주로 어떤 구에서 어떤 특징이 관찰되는지(시장성)를 같이 확인할 수 있다면 더 나은 인사이트를 도출 할 수 있을 것이다.


## GIS data
이렇게 위치정보를 포함하고 있는 데이터는 크게 

__Vector__ 

와 

__Raster__ 

가 있다. Raster는 우리가 흔히 아는 이미지 형태의 데이터 이고, Vector는 대표적인 세 가지 유형의 데이터가 있다.

![](/assets/img/2022-12-19-13-45-27.png)

- __Point(점)__ : 주로 어떤 도시기반시설, 건물, 교차로(node) 등을 나타낼 때 사용한다.
- __Line(선)__ : 주로 도로, 경로, 네트워크, 어떤 면의 중심선, 철도 등을 나타낼 때 사용한다.
- __Polygon(다각형)__ : 주로 어떤 지역, 군, 영역등을 나타낼 때 사용한다.


## Tool
- __QGIS__ : 가장 초기에 지도에 뿌려 공간마다 시각적으로 확인해보는 EDA과정이나, 모든 과정이 끝난 후 결과물을 시각화 하여 레포트를 작성하는데 사용한다.
- __Python__ : 공간 데이터 전처리, 분석, 시뮬레이션 등 거의 모든 프로세스에 활용이 가능하고 특히 `geopandas, networkx, shapely, finona` 등 편리한 라이브러리가 많이 나와있어 유용하게 사용하고 있다.


## Geopandas

geopandas는 pandas와 유사한 라이브러리로, 공간정보를 가진 데이터프레임을 다루는데 유용한 패키지로 가장많이 활용한다.

pandas와 마찬가지로 `GeoSeries, GeoDataFrame`의 타입으로 다루며 function이나 attribute들도 큰 차이가 없다.

### practice
`shapely`를 이용하여 시각화해보자.

```python
# Vector의 3가지 타입을 임포트
import geopandas as gpd
from shapely.geometry import Polygon, LineString, Point

# xy평면에 4개의 좌표 정의
x1 ,y1 = 1,2
x2, y2 = 2,2
x3, y3 = 2,3
x4, y4 = 1,3

# 포인트 찍는 방법
Point([x1,y1])

# 선을 그리는 방법
LineString([(x1,y1),(x3,y3)])

# 다각형 그리는 방법 -> 네모
Polygon([(x1,y1),(x2,y2),(x3,y3),(x4,y4)])

# 다각형을 그릴 때에는 순서를 잘 지켜주어야 한다. 
# 아래를 그리면? (1,2) -> (1,3) -> (2,2) -> (2,3) -> (1,2) 순으로 그림
Polygon(sorted([(x1,y1),(x2,y2),(x4,y4),(x3,y3)]))
```

shapely를 활용하여 생성한 공간 데이터를 시각화를 할때는 geopandas를 사용하면 쉽게 그릴 수 있다.
```python
import matplotlib.pyplot as plt

point = Point([x1,y1])
line = LineString([(x1,y1),(x3,y3)])
polygon = Polygon([(x1,y1),(x2,y2),(x3,y3),(x4,y4)])

ax = gpd.GeoSeries(polygon).plot( color='black', alpha=0.5)
gpd.GeoSeries(line).plot(ax=ax, linewidth=3, color='white')
gpd.GeoSeries(point).plot(ax=ax, color='red', markersize=100)
plt.axis('off')
plt.show()
print(point.geom_type)
print(line.geom_type)
print(polygon.geom_type)
```

### data structure
> ### Point
> `*.csv`

> ### Polygon
> `*.dbf`, `*.prj`, `*.shp`, `*.shx`
> `dbf` : dBase 데이터베이서 파일로, 데이터프레임 형태의 정보를 갖고 있다.
> `prj` : 공간 데이터의 좌표정보(좌표계)를 갖고 있으며, 좌표정의가 되어 있지 않을 경우 이 파일이 없을 수 있다.
> `shp` : vector 타입의 도형 및 정보를 담고 있다.
> `shx` : shp와 마찬가지이며, Auto CAD에서 주로 활용된다.

## 좌표계의 정의와 변환
공간데이터를 다룰때는 좌표계를 이해하는것이 상당히 중요하다. 서로다른 데이터의 좌표계를 통일 시키거나 변환할때는, 먼저 해당 데이터가 정의된 좌표계가 어떤 것인지 알아야 한다.

대표적으로 위경도, 미터좌표계가 있는데 국내에서는 주로 아래 좌표계를 사용한다.

- __EPSG4326(WGS84)__ : 위경도, 기본좌표계
- __EPSG5179(TM)__ : 미터 좌표계
- __EPSG5174(TM)__ : 미터 좌표계
- __EPSG5181(TM)__ : 미터 좌표계
데이터를 받아올때 꼭 어떤 좌표계로 만들어진 데이터 인지를 확인해야 그 데이터를 활용할 수 있다(좌표계를 모르면 못쓰는 데이터라고 해도 무방하다).

### 좌표계의 종류
- 지리좌표계 : 경도, 위도
- 투영좌표계 : 미터

#### 지리좌표계
지구상에 위치를 좌표로 표현하기 위해 __3차원의 구면을 이용하는 좌표계__ 를 의미한다. 한 지점은 경도(longitude)와 위도(latitude)로 표현되며 이 단위는 도(degree)로 표시된다.

> 경도(x)와 위도(y)를 갖고 있는 데이터라면 __WGS84좌표__ 라고 생각하면 된다.


#### 투영좌표계
3차원 위경도 좌표를 2차원 평면 상으로 나타내기 위해 투영(projection)이라는 과정을 거치게 되는데 이 투영된 좌표를 투영좌표계라고 한다.

이 투영방법에 따라서도 여러가지 체계로 분류가 되는데, 크게 2가지로 분류한다.

- __TM(Transverse meractor)__ : 횡단원통등각투영법
- __UTM(Universal Transcerse Mercator)__

두 투영방법은 같은 계산법을 거치지만 상수가 다를 뿐이다. __우리나라의 경우 TM좌표계를 기반으로 국가 기본도를 제작__ 하고 있으며, UTM은 군사지도나 단일원점을 사용하는 일부 부처에서 부분적으로 사용한다.

> 투영좌표계 : 미터 좌표계, 2차원, __TM또는 UTM__

### EPSG 코드
> 지리좌표계 : WGS84 => `EPSG4326`
> 투영좌표계 : GRS80타원체를 UTM-k로 투영한 좌표계 => `EPSG5179`



### 구현
기본적으로 python이나 qgis에 내장된 각 좌표계를 사용해도 큰 문제는 없지만 보정좌표 등을 정확하게 정의해 주기 위해서는 직접 해당 좌표계를 정의해주는게 좋다

#### 좌표계의 확인
```python
# 국가데이터로 받아온 seoul_area의 crs함수를 이용한 좌표계의 확인
print(seoul_area.crs) #{'init': 'epsg:5179'}

# 새로 생선한 pt_119라는 것은 당연히 정의가 안되어있음.
print(pt_119.crs) ##None

# 이렇게 하면 정의할 수 있음
pt_119.crs = {'init':'epsg:4326'}
print(pt_119.crs) #{'init': 'epsg:4326'}

# 미터단위 변환하기 위해 epsg5179로 해보자.
pt_119 = pt_119.to_crs({'init':'epsg:5179'})
```

#### 좌표계의 정의
```python
# 초기세팅
import pandas as pd
import geopandas as gpd
from shapely.geometry import Point, Polygon, LineString

seoul_area = gpd.GeoDataFrame.from_file('data/LARD_ADM_SECT_SGG_11.shp', encoding='cp949')
pt_119 = pd.read_csv('data/서울시 안전센터관할 위치정보 (좌표계_ WGS1984).csv', encoding='cp949', dtype=str)
pt_119['경도'] = pt_119['경도'].astype(float)
pt_119['위도'] = pt_119['위도'].astype(float)
pt_119['geometry'] = pt_119.apply(lambda row : Point([row['경도'], row['위도']]), axis=1)
pt_119 = gpd.GeoDataFrame(pt_119, geometry='geometry')


# Geopandas는 shapely(공간객체 담당)와 fiona(좌표담당)를 같이 활용한다.
# 좌표계는 fiona.crs의 from_string을 통해 생성할 수 있다
from fiona.crs import from_string
epsg4326 = from_string("+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs")


```
> 경도 좌표계는 일반적으로 EPSG4326(WGS84) 좌표계를 적용하면 되지만, 위 서울특별시 법정동 경계(seoul_area)와 같이 투영좌표계(TM)는 구득하려는 사이트나 제공기관에서 어떤 좌표계를 사용해 생성된 공간 데이터인지를 정확하게 인지하고, 그에 맞게 적용해줘야 한다.


### 좌표계 변환
일반적으로 공간분석은 도(degree)단위가 아닌 미터(meter)단위로 작업을 하기 때문에, 투영좌표계(TM)로 통일시켜주는게 좋다.

#### to_crs
```python
# 좌표 생성
epsg5179 = from_string("+proj=tmerc +lat_0=38 +lon_0=127.5 +k=0.9996 +x_0=1000000 +y_0=2000000 +ellps=GRS80 +units=m +no_defs")

# 변환
pt_119 = pt_119.to_crs(epsg5179)
pt_119["geometry"].head()
```

그러면

```python
0     POINT (944285.707763575 1947726.390537433)
1    POINT (964384.6573976473 1956833.993247274)
2    POINT (957313.2935830182 1943279.262784532)
3     POINT (952138.2406865631 1947752.94696052)
4     POINT (954174.228813116 1949633.598265431)
Name: geometry, dtype: object
```

를 얻는다.

Geometry를 확인해보면 위경도(127…., 37….)의 단위가 미터단위로 변경된 것을 확인할 수 있다.

![](/assets/img/2022-12-19-15-48-01.png)


#### 좌표가 정확히 안맞는 문제

위 방법처럼 정확하게 좌표를 정의하고, 동일하게 변환해주었음에도 딱 안맞는 경우가 생긴다.

경험적으로 알게된 사실이지만 통일해야할 좌표계 중 EPSG5174,5186,KOTI-KATEC가 존재하는 경우, 단순하게 좌표변환만 실시하게 되면 약 30m정도의 이격이 발생한다.


이럴때 위 좌표계로 통일시켜주면 정확히 맞는다.

```python
epsg5181_qgis = from_string("+proj=tmerc +lat_0=38 +lon_0=127 +k=1 +x_0=200000 +y_0=500000 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs")
```

위는 QGIS에서 제공하는 EPSG5181좌표계로 정식 좌표 문자열과 달리 `+towgs84=0,0,0,0,0,0,0`가 추가되어 있다. 정확한 이유는 아직 잘 모르지만 해당 좌표계로 통일시켜주면 맞는다.