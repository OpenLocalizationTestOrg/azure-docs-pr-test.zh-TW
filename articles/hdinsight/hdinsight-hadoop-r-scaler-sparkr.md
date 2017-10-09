---
title: "aaaUse ScaleR 和使用 Azure HDInsight SparkR |Microsoft 文件"
description: "使用 ScaleR 與 SparkR 搭配 R Server 與 HDInsight"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>在 HDInsight 中結合 ScaleR 與 SparkR

本文將說明如何 toopredict 飛行到達延遲使用**ScaleR**羅吉斯迴歸模型，從航班延誤和天氣資料與聯結**SparkR**。 這個案例示範如何使用 Microsoft R Server 用於分析的 Spark 上的資料操作 ScaleR hello 功能。 hello 組合這些技術可讓您在分散式處理 tooapply hello 最新功能。

雖然這兩個封裝會在 Hadoop 的 Spark 執行引擎上執行，但它們無法共用記憶體內部資料，因為它們需要自己個別的 Spark 工作階段。 R Server 的未來版本中，解決這個問題，直到 hello 因應措施是 toomaintain 非重疊的 Spark 工作階段和 tooexchange 資料透過中繼檔案。 這裡的 hello 指示顯示這些需求都是直接 tooachieve。

我們使用範例這裡一開始在分層 2016年 talk 中伊 Inchiosa 和共用，同時也是可透過 hello 網路研討會 Roni Burd[建置可擴充的資料科學平台，以及 R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio)。 hello 範例會使用 SparkR toojoin hello已知 airlines 到達延遲資料集具有出發與抵達機場的天氣資料。 hello 資料聯結將做輸入的 tooa ScaleR 羅吉斯迴歸模型來預測班機抵達延遲。

hello 程式碼我們逐步解說原本針對在 Azure 上的 HDInsight 叢集上的 Spark 執行的 R 伺服器所撰寫。 但 hello 概念混合 hello SparkR 和 ScaleR 中的使用一個指令碼也是在內部部署環境的 hello 內容中無效。 在 hello 下列程式碼，我們假設為中介層級的相關知識的 R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)的 R 伺服器程式庫。 在逐步解說此案例，同時會介紹 [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) 的使用。

## <a name="hello-airline-and-weather-datasets"></a>hello airline 和天氣資料集

hello **AirOnTime08to12CSV** airlines 公用資料集包含班機抵達和離開詳細資料的內 hello 先是美國，所有商業班機的相關資訊，從年 10 月 1987 tooDecember 2012。 這是大型資料集︰總計有將近 1 億 5 千萬筆記錄。 解壓縮後，不超過 4 GB。 它是可從 hello[美國政府封存](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)。 更方便，它可做為包含一組 303 不同每月的 CSV 檔案從 hello 的 zip 檔案 (AirOnTimeCSV.zip) [Revolution Analytics 資料集儲存機制](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee hello 的效果天氣航班延誤，我們也需要在每個 hello 機場 hello 天氣資料。 此資料可以下載為 zip 檔，以未經處理格式，依月份，從 hello [Oceanic 國家 （地區) 和 Atmospheric 管理的儲存機制](http://www.ncdc.noaa.gov/orders/qclcd/)。 基於 hello 此範例中，我們提取從 2007 年 – 2012 年 12 月的天氣資料，而且使用中每個 hello 68 每月 zips hello 每小時資料檔案。 hello 每月的 zip 檔案也包含 hello 天氣站台識別碼 (WBAN)，它是 （呼叫名稱） 相關聯的 hello 機場之間的對應 (YYYYMMstation.txt) 和 hello 機場的時區時差的 UTC （時區）。 聯結 hello airline 延遲和天氣資料時，就需要這項資訊的所有項目。

## <a name="setting-up-hello-spark-environment"></a>設定 hello Spark 環境

hello 第一個步驟是 tooset hello Spark 環境。 我們開始，請指向 toohello 目錄，其中包含我們的輸入的資料目錄、 建立 Spark 計算內容，建立參考記錄 toohello 主控台記錄函式：

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

接下來我們新增 R 封裝 「 Spark_Home"toohello 搜尋路徑，讓我們能夠使用 SparkR，並初始化 SparkR 工作階段：

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>正在準備 hello 天氣資料

tooprepare hello 天氣資料，我們子集它 toohello 模型所需的資料行： 

- "Visibility"
- "DryBulbCelsius"
- "DewPointCelsius"
- "RelativeHumidity"
- "WindSpeed"
- "Altimeter"

然後我們新增 hello 天氣站台相關聯的機場代碼，並從本地時間 tooUTC 轉換 hello 度量單位。

我們先建立的檔案 toomap hello 天氣站台 (WBAN) 資訊 tooan 機場代碼。 我們無法從 hello hello 天氣資料所包含的對應檔來取得此相互關聯。 由對應 hello*呼叫名稱*（例如 LAX） 太 hello 天氣資料檔中欄位*原點*hello airline 資料中。 不過，我們剛好 toohave 另一個對應手邊對應*WBAN*太*AirportID* (例如，針對 LAX 12892)，並包含*時區*的已儲存 tooaCSV 檔案稱為 「 wban-到-機場-id-tz。CSV 」，我們可以使用。 例如：

| AirportID | WBAN | TimeZone
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

下列程式碼讀取每個 hello 每小時的未經處理的天氣資料的 hello 檔案子集 toohello 資料行我們需要、 合併 hello 氣象對應檔案、 日期時間的度量單位 tooUTC 調整 hello，然後寫出 hello 檔案的新版本：

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>匯入 hello airline 和天氣資料 tooSpark 資料框架

現在我們使用 hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello 天氣與 airline 資料 tooSpark 資料框架的函式。 如同其他許多 Spark 方法一樣，這個函式會延遲執行，意思就是排入佇列等候執行，但等到必要時才會執行。

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>資料清理和轉換

接下來我們進行一些清除 hello airline 資料我們已匯入 toorename 資料行。 我們只保留所需，hello 變數，並捨入下 toohello 最接近的小時 tooenable 合併在離開 hello 最新的天氣資料的排程的離開時間：

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

現在，我們會執行類似作業 hello 天氣資料：

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>聯結 hello 天氣與 airline 資料

我們現在使用 hello SparkR [join （)](https://docs.databricks.com/spark/latest/sparkr/functions/join.html)函式 toodo 左方外部聯結的 hello airline 和天氣資料離開 AirportID 和日期時間。 hello 外部聯結可讓我們 tooretain hello 班機的所有資料都記錄，即使沒有相符的天氣資料。 Hello 聯結我們移除一些重複的資料行，而重新命名 hello 保留資料行 tooremove hello 內送資料框架前置詞 hello 聯結所導入。

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

以類似的方式，我們將 hello 天氣與 airline 資料抵達 AirportID 和日期時間為基礎：

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>儲存 exchange 的結果 tooCSV ScaleR

我們需要與 SparkR toodo hello 聯結動作會完成。 我們從 hello 最終 Spark 資料框架 」 joinedDF5"tooa CSV 的輸入 tooScaleR 儲存 hello 資料，然後再關閉出 hello SparkR 工作階段。 我們明確告訴 SparkR toosave hello 結果 CSV 80 不同的磁碟分割 tooenable 足夠中平行處理原則 ScaleR 處理中：

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>匯入供 ScaleR tooXDF

我們可以使用的聯結的 airline 和天氣資料，做為 hello CSV 檔案-適用於透過 ScaleR 文字資料來源的模型。 但是，我們先匯入它 tooXDF，因為它是更有效率地執行 hello 資料集上的多個作業時：

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>分割資料以供訓練和測試

我們使用 rxDataStep toosplit 出 hello 2012 資料進行測試，並保留定型的 hello rest:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>訓練和測試羅吉斯迴歸模型

現在我們已經準備好 toobuild 模型。 toosee hello 影響力的天氣資料 hello 抵達時間的延遲，我們使用 ScaleR 的羅吉斯迴歸常式。 我們使用 toomodel 是否大於 15 分鐘的到達時延遲會受到在 hello 出發與抵達機場 hello 天氣：

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

現在讓我們來看看如何但未在 hello 測試資料進行一些預測，並查看 ROC 和 AUC。

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>在其他位置進行評分

我們也可以使用 hello 模型計分的資料，另一個平台。 儲存 tooan RDS 檔案，然後傳送再將匯入該 RDS 計分環境，例如 SQL Server R Services 的目的地。 Hello 因素層級的 hello 資料 toobe 評分符合哪些 hello 上模型內建的重要 tooensure 它。 相符項目可藉由擷取，並儲存 hello 資料行資訊相關聯 hello 透過 ScaleR 的資料模型化`rxCreateColInfo()`函式，然後將套用預測該資料行資訊 toohello 輸入的資料來源。 在 hello 下列我們儲存 hello 測試資料集的少數資料列，將擷取並使用 hello 預測指令碼中的 hello 與此範例的資料行資訊：

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>摘要

在本文中，顯示了很可能 toocombine 用於的 SparkR ScaleR Hadoop Spark 中模型開發的資料操作的方式。 此案例需要維護個別的 Spark 工作階段 (一次僅執行一個工作階段)，並透過 CSV 檔案交換資料。 雖然很簡單，但是當 SparkR 和 ScaleR 可以共用 Spark 工作階段和 Spark DataFrame 時，在後續發行的 R Server 中，此程序應會變得更加容易。

## <a name="next-steps-and-more-information"></a>後續步驟和更多資訊

- 如需使用上的 Spark R Server 的詳細資訊，請參閱 hello [MSDN 上的使用者入門指南](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- 如需 R Server 的一般資訊，請參閱 hello[開始使用 R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)發行項。

- 如需 HDInsight 上之 R Server 的詳細資訊，請參閱 [Azure HDInsight 上的 R Server 概觀](hdinsight-hadoop-r-server-overview.md)和 [Azure HDInsight 上的 R Server](hdinsight-hadoop-r-server-get-started.md)。

如需使用 SparkR 的詳細資訊，請參閱：

- [Apache SparkR 文件](https://spark.apache.org/docs/2.1.0/sparkr.html)

- Databricks 提供的 [SparkR 概觀](https://docs.databricks.com/spark/latest/sparkr/overview.html)
