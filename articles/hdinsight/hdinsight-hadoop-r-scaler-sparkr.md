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
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="5ae99-103">在 HDInsight 中結合 ScaleR 與 SparkR</span><span class="sxs-lookup"><span data-stu-id="5ae99-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="5ae99-104">本文將說明如何 toopredict 飛行到達延遲使用**ScaleR**羅吉斯迴歸模型，從航班延誤和天氣資料與聯結**SparkR**。</span><span class="sxs-lookup"><span data-stu-id="5ae99-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="5ae99-105">這個案例示範如何使用 Microsoft R Server 用於分析的 Spark 上的資料操作 ScaleR hello 功能。</span><span class="sxs-lookup"><span data-stu-id="5ae99-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="5ae99-106">hello 組合這些技術可讓您在分散式處理 tooapply hello 最新功能。</span><span class="sxs-lookup"><span data-stu-id="5ae99-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="5ae99-107">雖然這兩個封裝會在 Hadoop 的 Spark 執行引擎上執行，但它們無法共用記憶體內部資料，因為它們需要自己個別的 Spark 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5ae99-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="5ae99-108">R Server 的未來版本中，解決這個問題，直到 hello 因應措施是 toomaintain 非重疊的 Spark 工作階段和 tooexchange 資料透過中繼檔案。</span><span class="sxs-lookup"><span data-stu-id="5ae99-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="5ae99-109">這裡的 hello 指示顯示這些需求都是直接 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="5ae99-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="5ae99-110">我們使用範例這裡一開始在分層 2016年 talk 中伊 Inchiosa 和共用，同時也是可透過 hello 網路研討會 Roni Burd[建置可擴充的資料科學平台，以及 R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio)。 hello 範例會使用 SparkR toojoin hello已知 airlines 到達延遲資料集具有出發與抵達機場的天氣資料。</span><span class="sxs-lookup"><span data-stu-id="5ae99-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="5ae99-111">hello 資料聯結將做輸入的 tooa ScaleR 羅吉斯迴歸模型來預測班機抵達延遲。</span><span class="sxs-lookup"><span data-stu-id="5ae99-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="5ae99-112">hello 程式碼我們逐步解說原本針對在 Azure 上的 HDInsight 叢集上的 Spark 執行的 R 伺服器所撰寫。</span><span class="sxs-lookup"><span data-stu-id="5ae99-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="5ae99-113">但 hello 概念混合 hello SparkR 和 ScaleR 中的使用一個指令碼也是在內部部署環境的 hello 內容中無效。</span><span class="sxs-lookup"><span data-stu-id="5ae99-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="5ae99-114">在 hello 下列程式碼，我們假設為中介層級的相關知識的 R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)的 R 伺服器程式庫。</span><span class="sxs-lookup"><span data-stu-id="5ae99-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="5ae99-115">在逐步解說此案例，同時會介紹 [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) 的使用。</span><span class="sxs-lookup"><span data-stu-id="5ae99-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="5ae99-116">hello airline 和天氣資料集</span><span class="sxs-lookup"><span data-stu-id="5ae99-116">hello airline and weather datasets</span></span>

<span data-ttu-id="5ae99-117">hello **AirOnTime08to12CSV** airlines 公用資料集包含班機抵達和離開詳細資料的內 hello 先是美國，所有商業班機的相關資訊，從年 10 月 1987 tooDecember 2012。</span><span class="sxs-lookup"><span data-stu-id="5ae99-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="5ae99-118">這是大型資料集︰總計有將近 1 億 5 千萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="5ae99-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="5ae99-119">解壓縮後，不超過 4 GB。</span><span class="sxs-lookup"><span data-stu-id="5ae99-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="5ae99-120">它是可從 hello[美國政府封存](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236)。</span><span class="sxs-lookup"><span data-stu-id="5ae99-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="5ae99-121">更方便，它可做為包含一組 303 不同每月的 CSV 檔案從 hello 的 zip 檔案 (AirOnTimeCSV.zip) [Revolution Analytics 資料集儲存機制](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="5ae99-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="5ae99-122">toosee hello 的效果天氣航班延誤，我們也需要在每個 hello 機場 hello 天氣資料。</span><span class="sxs-lookup"><span data-stu-id="5ae99-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="5ae99-123">此資料可以下載為 zip 檔，以未經處理格式，依月份，從 hello [Oceanic 國家 （地區) 和 Atmospheric 管理的儲存機制](http://www.ncdc.noaa.gov/orders/qclcd/)。</span><span class="sxs-lookup"><span data-stu-id="5ae99-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="5ae99-124">基於 hello 此範例中，我們提取從 2007 年 – 2012 年 12 月的天氣資料，而且使用中每個 hello 68 每月 zips hello 每小時資料檔案。</span><span class="sxs-lookup"><span data-stu-id="5ae99-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="5ae99-125">hello 每月的 zip 檔案也包含 hello 天氣站台識別碼 (WBAN)，它是 （呼叫名稱） 相關聯的 hello 機場之間的對應 (YYYYMMstation.txt) 和 hello 機場的時區時差的 UTC （時區）。</span><span class="sxs-lookup"><span data-stu-id="5ae99-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="5ae99-126">聯結 hello airline 延遲和天氣資料時，就需要這項資訊的所有項目。</span><span class="sxs-lookup"><span data-stu-id="5ae99-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="5ae99-127">設定 hello Spark 環境</span><span class="sxs-lookup"><span data-stu-id="5ae99-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="5ae99-128">hello 第一個步驟是 tooset hello Spark 環境。</span><span class="sxs-lookup"><span data-stu-id="5ae99-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="5ae99-129">我們開始，請指向 toohello 目錄，其中包含我們的輸入的資料目錄、 建立 Spark 計算內容，建立參考記錄 toohello 主控台記錄函式：</span><span class="sxs-lookup"><span data-stu-id="5ae99-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

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

<span data-ttu-id="5ae99-130">接下來我們新增 R 封裝 「 Spark_Home"toohello 搜尋路徑，讓我們能夠使用 SparkR，並初始化 SparkR 工作階段：</span><span class="sxs-lookup"><span data-stu-id="5ae99-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

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

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="5ae99-131">正在準備 hello 天氣資料</span><span class="sxs-lookup"><span data-stu-id="5ae99-131">Preparing hello weather data</span></span>

<span data-ttu-id="5ae99-132">tooprepare hello 天氣資料，我們子集它 toohello 模型所需的資料行：</span><span class="sxs-lookup"><span data-stu-id="5ae99-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="5ae99-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="5ae99-133">"Visibility"</span></span>
- <span data-ttu-id="5ae99-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="5ae99-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="5ae99-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="5ae99-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="5ae99-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="5ae99-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="5ae99-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="5ae99-137">"WindSpeed"</span></span>
- <span data-ttu-id="5ae99-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="5ae99-138">"Altimeter"</span></span>

<span data-ttu-id="5ae99-139">然後我們新增 hello 天氣站台相關聯的機場代碼，並從本地時間 tooUTC 轉換 hello 度量單位。</span><span class="sxs-lookup"><span data-stu-id="5ae99-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="5ae99-140">我們先建立的檔案 toomap hello 天氣站台 (WBAN) 資訊 tooan 機場代碼。</span><span class="sxs-lookup"><span data-stu-id="5ae99-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="5ae99-141">我們無法從 hello hello 天氣資料所包含的對應檔來取得此相互關聯。</span><span class="sxs-lookup"><span data-stu-id="5ae99-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="5ae99-142">由對應 hello*呼叫名稱*（例如 LAX） 太 hello 天氣資料檔中欄位*原點*hello airline 資料中。</span><span class="sxs-lookup"><span data-stu-id="5ae99-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="5ae99-143">不過，我們剛好 toohave 另一個對應手邊對應*WBAN*太*AirportID* (例如，針對 LAX 12892)，並包含*時區*的已儲存 tooaCSV 檔案稱為 「 wban-到-機場-id-tz。CSV 」，我們可以使用。</span><span class="sxs-lookup"><span data-stu-id="5ae99-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="5ae99-144">例如：</span><span class="sxs-lookup"><span data-stu-id="5ae99-144">For example:</span></span>

| <span data-ttu-id="5ae99-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="5ae99-145">AirportID</span></span> | <span data-ttu-id="5ae99-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="5ae99-146">WBAN</span></span> | <span data-ttu-id="5ae99-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="5ae99-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="5ae99-148">10685</span><span class="sxs-lookup"><span data-stu-id="5ae99-148">10685</span></span> | <span data-ttu-id="5ae99-149">54831</span><span class="sxs-lookup"><span data-stu-id="5ae99-149">54831</span></span> | <span data-ttu-id="5ae99-150">-6</span><span class="sxs-lookup"><span data-stu-id="5ae99-150">-6</span></span>
| <span data-ttu-id="5ae99-151">14871</span><span class="sxs-lookup"><span data-stu-id="5ae99-151">14871</span></span> | <span data-ttu-id="5ae99-152">24232</span><span class="sxs-lookup"><span data-stu-id="5ae99-152">24232</span></span> | <span data-ttu-id="5ae99-153">-8</span><span class="sxs-lookup"><span data-stu-id="5ae99-153">-8</span></span>
| <span data-ttu-id="5ae99-154">..</span><span class="sxs-lookup"><span data-stu-id="5ae99-154">..</span></span> | <span data-ttu-id="5ae99-155">..</span><span class="sxs-lookup"><span data-stu-id="5ae99-155">..</span></span> | <span data-ttu-id="5ae99-156">..</span><span class="sxs-lookup"><span data-stu-id="5ae99-156">..</span></span>

<span data-ttu-id="5ae99-157">下列程式碼讀取每個 hello 每小時的未經處理的天氣資料的 hello 檔案子集 toohello 資料行我們需要、 合併 hello 氣象對應檔案、 日期時間的度量單位 tooUTC 調整 hello，然後寫出 hello 檔案的新版本：</span><span class="sxs-lookup"><span data-stu-id="5ae99-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

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

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="5ae99-158">匯入 hello airline 和天氣資料 tooSpark 資料框架</span><span class="sxs-lookup"><span data-stu-id="5ae99-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="5ae99-159">現在我們使用 hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello 天氣與 airline 資料 tooSpark 資料框架的函式。</span><span class="sxs-lookup"><span data-stu-id="5ae99-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="5ae99-160">如同其他許多 Spark 方法一樣，這個函式會延遲執行，意思就是排入佇列等候執行，但等到必要時才會執行。</span><span class="sxs-lookup"><span data-stu-id="5ae99-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

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

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="5ae99-161">資料清理和轉換</span><span class="sxs-lookup"><span data-stu-id="5ae99-161">Data cleansing and transformation</span></span>

<span data-ttu-id="5ae99-162">接下來我們進行一些清除 hello airline 資料我們已匯入 toorename 資料行。</span><span class="sxs-lookup"><span data-stu-id="5ae99-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="5ae99-163">我們只保留所需，hello 變數，並捨入下 toohello 最接近的小時 tooenable 合併在離開 hello 最新的天氣資料的排程的離開時間：</span><span class="sxs-lookup"><span data-stu-id="5ae99-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

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

<span data-ttu-id="5ae99-164">現在，我們會執行類似作業 hello 天氣資料：</span><span class="sxs-lookup"><span data-stu-id="5ae99-164">Now we perform similar operations on hello weather data:</span></span>

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

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="5ae99-165">聯結 hello 天氣與 airline 資料</span><span class="sxs-lookup"><span data-stu-id="5ae99-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="5ae99-166">我們現在使用 hello SparkR [join （)](https://docs.databricks.com/spark/latest/sparkr/functions/join.html)函式 toodo 左方外部聯結的 hello airline 和天氣資料離開 AirportID 和日期時間。</span><span class="sxs-lookup"><span data-stu-id="5ae99-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="5ae99-167">hello 外部聯結可讓我們 tooretain hello 班機的所有資料都記錄，即使沒有相符的天氣資料。</span><span class="sxs-lookup"><span data-stu-id="5ae99-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="5ae99-168">Hello 聯結我們移除一些重複的資料行，而重新命名 hello 保留資料行 tooremove hello 內送資料框架前置詞 hello 聯結所導入。</span><span class="sxs-lookup"><span data-stu-id="5ae99-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

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

<span data-ttu-id="5ae99-169">以類似的方式，我們將 hello 天氣與 airline 資料抵達 AirportID 和日期時間為基礎：</span><span class="sxs-lookup"><span data-stu-id="5ae99-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

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

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="5ae99-170">儲存 exchange 的結果 tooCSV ScaleR</span><span class="sxs-lookup"><span data-stu-id="5ae99-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="5ae99-171">我們需要與 SparkR toodo hello 聯結動作會完成。</span><span class="sxs-lookup"><span data-stu-id="5ae99-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="5ae99-172">我們從 hello 最終 Spark 資料框架 」 joinedDF5"tooa CSV 的輸入 tooScaleR 儲存 hello 資料，然後再關閉出 hello SparkR 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5ae99-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="5ae99-173">我們明確告訴 SparkR toosave hello 結果 CSV 80 不同的磁碟分割 tooenable 足夠中平行處理原則 ScaleR 處理中：</span><span class="sxs-lookup"><span data-stu-id="5ae99-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

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

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="5ae99-174">匯入供 ScaleR tooXDF</span><span class="sxs-lookup"><span data-stu-id="5ae99-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="5ae99-175">我們可以使用的聯結的 airline 和天氣資料，做為 hello CSV 檔案-適用於透過 ScaleR 文字資料來源的模型。</span><span class="sxs-lookup"><span data-stu-id="5ae99-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="5ae99-176">但是，我們先匯入它 tooXDF，因為它是更有效率地執行 hello 資料集上的多個作業時：</span><span class="sxs-lookup"><span data-stu-id="5ae99-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

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

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="5ae99-177">分割資料以供訓練和測試</span><span class="sxs-lookup"><span data-stu-id="5ae99-177">Splitting data for training and test</span></span>

<span data-ttu-id="5ae99-178">我們使用 rxDataStep toosplit 出 hello 2012 資料進行測試，並保留定型的 hello rest:</span><span class="sxs-lookup"><span data-stu-id="5ae99-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

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

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="5ae99-179">訓練和測試羅吉斯迴歸模型</span><span class="sxs-lookup"><span data-stu-id="5ae99-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="5ae99-180">現在我們已經準備好 toobuild 模型。</span><span class="sxs-lookup"><span data-stu-id="5ae99-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="5ae99-181">toosee hello 影響力的天氣資料 hello 抵達時間的延遲，我們使用 ScaleR 的羅吉斯迴歸常式。</span><span class="sxs-lookup"><span data-stu-id="5ae99-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="5ae99-182">我們使用 toomodel 是否大於 15 分鐘的到達時延遲會受到在 hello 出發與抵達機場 hello 天氣：</span><span class="sxs-lookup"><span data-stu-id="5ae99-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

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

<span data-ttu-id="5ae99-183">現在讓我們來看看如何但未在 hello 測試資料進行一些預測，並查看 ROC 和 AUC。</span><span class="sxs-lookup"><span data-stu-id="5ae99-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

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

## <a name="scoring-elsewhere"></a><span data-ttu-id="5ae99-184">在其他位置進行評分</span><span class="sxs-lookup"><span data-stu-id="5ae99-184">Scoring elsewhere</span></span>

<span data-ttu-id="5ae99-185">我們也可以使用 hello 模型計分的資料，另一個平台。</span><span class="sxs-lookup"><span data-stu-id="5ae99-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="5ae99-186">儲存 tooan RDS 檔案，然後傳送再將匯入該 RDS 計分環境，例如 SQL Server R Services 的目的地。</span><span class="sxs-lookup"><span data-stu-id="5ae99-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="5ae99-187">Hello 因素層級的 hello 資料 toobe 評分符合哪些 hello 上模型內建的重要 tooensure 它。</span><span class="sxs-lookup"><span data-stu-id="5ae99-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="5ae99-188">相符項目可藉由擷取，並儲存 hello 資料行資訊相關聯 hello 透過 ScaleR 的資料模型化`rxCreateColInfo()`函式，然後將套用預測該資料行資訊 toohello 輸入的資料來源。</span><span class="sxs-lookup"><span data-stu-id="5ae99-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="5ae99-189">在 hello 下列我們儲存 hello 測試資料集的少數資料列，將擷取並使用 hello 預測指令碼中的 hello 與此範例的資料行資訊：</span><span class="sxs-lookup"><span data-stu-id="5ae99-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

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

## <a name="summary"></a><span data-ttu-id="5ae99-190">摘要</span><span class="sxs-lookup"><span data-stu-id="5ae99-190">Summary</span></span>

<span data-ttu-id="5ae99-191">在本文中，顯示了很可能 toocombine 用於的 SparkR ScaleR Hadoop Spark 中模型開發的資料操作的方式。</span><span class="sxs-lookup"><span data-stu-id="5ae99-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="5ae99-192">此案例需要維護個別的 Spark 工作階段 (一次僅執行一個工作階段)，並透過 CSV 檔案交換資料。</span><span class="sxs-lookup"><span data-stu-id="5ae99-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="5ae99-193">雖然很簡單，但是當 SparkR 和 ScaleR 可以共用 Spark 工作階段和 Spark DataFrame 時，在後續發行的 R Server 中，此程序應會變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="5ae99-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="5ae99-194">後續步驟和更多資訊</span><span class="sxs-lookup"><span data-stu-id="5ae99-194">Next steps and more information</span></span>

- <span data-ttu-id="5ae99-195">如需使用上的 Spark R Server 的詳細資訊，請參閱 hello [MSDN 上的使用者入門指南](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="5ae99-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="5ae99-196">如需 R Server 的一般資訊，請參閱 hello[開始使用 R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)發行項。</span><span class="sxs-lookup"><span data-stu-id="5ae99-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="5ae99-197">如需 HDInsight 上之 R Server 的詳細資訊，請參閱 [Azure HDInsight 上的 R Server 概觀](hdinsight-hadoop-r-server-overview.md)和 [Azure HDInsight 上的 R Server](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5ae99-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="5ae99-198">如需使用 SparkR 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5ae99-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="5ae99-199">Apache SparkR 文件</span><span class="sxs-lookup"><span data-stu-id="5ae99-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="5ae99-200">Databricks 提供的 [SparkR 概觀](https://docs.databricks.com/spark/latest/sparkr/overview.html)</span><span class="sxs-lookup"><span data-stu-id="5ae99-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
