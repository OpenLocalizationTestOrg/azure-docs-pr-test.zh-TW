---
title: "搭配 Azure HDInsight 使用 ScaleR 與 SparkR | Microsoft Docs"
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
ms.openlocfilehash: 29733f6f6b725dd4735219ed221431805558a5e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="f0f93-103">在 HDInsight 中結合 ScaleR 與 SparkR</span><span class="sxs-lookup"><span data-stu-id="f0f93-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="f0f93-104">本文說明如何透過以 **SparkR** 聯結的班機延誤和天氣資料來使用 **ScaleR** 羅吉斯迴歸模型，以預測班機抵達延誤。</span><span class="sxs-lookup"><span data-stu-id="f0f93-104">This article shows how to predict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="f0f93-105">本案例說明搭配使用 Spark 上用於資料操作的 ScaleR 功能與用於分析的 Microsoft R Server。</span><span class="sxs-lookup"><span data-stu-id="f0f93-105">This scenario demonstrates the capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="f0f93-106">這些技術的結合可讓您套用分散式處理的最新功能。</span><span class="sxs-lookup"><span data-stu-id="f0f93-106">The combination of these technologies enables you to apply the latest capabilities in distributed processing.</span></span>

<span data-ttu-id="f0f93-107">雖然這兩個封裝會在 Hadoop 的 Spark 執行引擎上執行，但它們無法共用記憶體內部資料，因為它們需要自己個別的 Spark 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f0f93-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="f0f93-108">在後續的 R Server 版本處理此問題之前，其因應措施是維護不重疊的 Spark 工作階段，並透過中繼檔案交換資料。</span><span class="sxs-lookup"><span data-stu-id="f0f93-108">Until this issue is addressed in an upcoming version of R Server, the workaround is to maintain non-overlapping Spark sessions, and to exchange data through intermediate files.</span></span> <span data-ttu-id="f0f93-109">此處的指示說明這些需求是可直接達成的。</span><span class="sxs-lookup"><span data-stu-id="f0f93-109">The instructions here show that these requirements are straightforward to achieve.</span></span>

<span data-ttu-id="f0f93-110">我們在此一開始會使用 Mario Inchiosa 和 Roni Burd 在 Strata 2016 演講 (也可透過 [使用 R 建置可擴充的資料科學平台](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio) \(Building a Scalable Data Science Platform with R\) 網路研討會觀看) 中分享的範例進行示範。此範例使用 SparkR 聯結已知的航班抵達延誤資料集，和起飛及抵達機場的天氣資料。</span><span class="sxs-lookup"><span data-stu-id="f0f93-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through the webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). The example uses SparkR to join the well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="f0f93-111">聯結的資料將作為 ScaleR 羅吉斯迴歸模型的輸入，以預測班機抵達延誤。</span><span class="sxs-lookup"><span data-stu-id="f0f93-111">The data joined is then used as input to a ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="f0f93-112">我們所解說的程式碼原先是針對 Azure HDInsight 叢集中的 Spark 上所執行的 R Server 所編寫。</span><span class="sxs-lookup"><span data-stu-id="f0f93-112">The code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="f0f93-113">但是，以一個指令碼混合使用 SparkR 和 ScaleR 的概念在內部部署環境的內容中同樣有效。</span><span class="sxs-lookup"><span data-stu-id="f0f93-113">But the concept of mixing the use of SparkR and ScaleR in one script is also valid in the context of on-premises environments.</span></span> <span data-ttu-id="f0f93-114">接下來，我們假設對於 R 和 R Server 的 [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) 程式庫有中階了解程度。</span><span class="sxs-lookup"><span data-stu-id="f0f93-114">In the following, we presume an intermediate level of knowledge of R and R the [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="f0f93-115">在逐步解說此案例，同時會介紹 [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) 的使用。</span><span class="sxs-lookup"><span data-stu-id="f0f93-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="the-airline-and-weather-datasets"></a><span data-ttu-id="f0f93-116">航線和天氣資料集</span><span class="sxs-lookup"><span data-stu-id="f0f93-116">The airline and weather datasets</span></span>

<span data-ttu-id="f0f93-117">**AirOnTime08to12CSV** 航線公用資料集包含有關美國境內所有商業班機的班機抵達和起飛詳細資料 (從 1987 年 10 月至 2012 年 12 月)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-117">The **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within the USA, from October 1987 to December 2012.</span></span> <span data-ttu-id="f0f93-118">這是大型資料集︰總計有將近 1 億 5 千萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="f0f93-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="f0f93-119">解壓縮後，不超過 4 GB。</span><span class="sxs-lookup"><span data-stu-id="f0f93-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="f0f93-120">您可以從[美國政府檔案庫](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236) \(U.S. government archives\) 取得。</span><span class="sxs-lookup"><span data-stu-id="f0f93-120">It is available from the [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="f0f93-121">而 zip 檔案 (AirOnTimeCSV.zip) 較為方便，其中包含 [Revolution Analytics 資料集存放庫](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/) \(Revolution Analytics dataset repository\) 中的一組 303 個個別每月 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="f0f93-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from the [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="f0f93-122">若要了解天氣對於班機延誤的影響，我們也需要每個機場的天氣資料。</span><span class="sxs-lookup"><span data-stu-id="f0f93-122">To see the effects of weather on flight delays, we also need the weather data at each of the airports.</span></span> <span data-ttu-id="f0f93-123">您可以依照月份從[美國國家海洋與大氣層管理局存放庫](http://www.ncdc.noaa.gov/orders/qclcd/) \(National Oceanic and Atmospheric Administration repository\) 下載此資料 (未經處理格式的 zip 檔案)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-123">This data can be downloaded as zip files in raw form, by month, from the [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="f0f93-124">基於本範例的目的，我們提取 2007 年 5 月至 2012 年 12 月的天氣資料，並使用 68 個每月 zip 檔內的每小時資料檔案。</span><span class="sxs-lookup"><span data-stu-id="f0f93-124">For the purposes of this example, we pull weather data from May 2007 – December 2012 and used the hourly data files within each of the 68 monthly zips.</span></span> <span data-ttu-id="f0f93-125">每月 zip 檔案也包含天氣觀測站識別碼 (WBAN)、相關聯的機場 (CallSign) 以及機場與 UTC 的時差 (TimeZone) 之間的對應 (YYYYMMstation.txt)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-125">The monthly zip files also contain a mapping (YYYYMMstation.txt) between the weather station ID (WBAN), the airport that it is associated with (CallSign), and the airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="f0f93-126">這些都是聯結航班延誤和天氣資料時所需的資料。</span><span class="sxs-lookup"><span data-stu-id="f0f93-126">All of this information is needed when joining with the airline delay and weather data.</span></span>

## <a name="setting-up-the-spark-environment"></a><span data-ttu-id="f0f93-127">設定 Spark 環境</span><span class="sxs-lookup"><span data-stu-id="f0f93-127">Setting up the Spark environment</span></span>

<span data-ttu-id="f0f93-128">第一步是設定 Spark 環境。</span><span class="sxs-lookup"><span data-stu-id="f0f93-128">The first step is to set up the Spark environment.</span></span> <span data-ttu-id="f0f93-129">首先，指向包含輸入資料目錄的目錄、建立 Spark 計算內容，並建立可將資訊記錄至主控台的記錄函式︰</span><span class="sxs-lookup"><span data-stu-id="f0f93-129">We begin by pointing to the directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging to the console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session to reduce startup times 
#   (remember to stop it later!)
 
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

<span data-ttu-id="f0f93-130">接下來，我們將 “Spark_Home” 新增至 R 套件的搜尋路徑，以便使用 SparkR，並且初始化 SparkR 工作階段：</span><span class="sxs-lookup"><span data-stu-id="f0f93-130">Next we add “Spark_Home” to the search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

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

## <a name="preparing-the-weather-data"></a><span data-ttu-id="f0f93-131">準備天氣資料</span><span class="sxs-lookup"><span data-stu-id="f0f93-131">Preparing the weather data</span></span>

<span data-ttu-id="f0f93-132">為準備天氣資料，我們將資料細分為以下建立模型所需的資料行：</span><span class="sxs-lookup"><span data-stu-id="f0f93-132">To prepare the weather data, we subset it to the columns needed for modeling:</span></span> 

- <span data-ttu-id="f0f93-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="f0f93-133">"Visibility"</span></span>
- <span data-ttu-id="f0f93-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="f0f93-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="f0f93-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="f0f93-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="f0f93-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="f0f93-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="f0f93-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="f0f93-137">"WindSpeed"</span></span>
- <span data-ttu-id="f0f93-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="f0f93-138">"Altimeter"</span></span>

<span data-ttu-id="f0f93-139">然後，我們加入與天氣觀測站相關聯的機場代碼，並將度量單位從當地時間轉換成 UTC。</span><span class="sxs-lookup"><span data-stu-id="f0f93-139">Then we add an airport code associated with the weather station and convert the measurements from local time to UTC.</span></span>

<span data-ttu-id="f0f93-140">我們首先建立一個可將天氣觀測站 (WBAN) 資訊對應至機場代碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="f0f93-140">We begin by creating a file to map the weather station (WBAN) info to an airport code.</span></span> <span data-ttu-id="f0f93-141">我們可以從天氣資料隨附的對應檔取得此關聯性。</span><span class="sxs-lookup"><span data-stu-id="f0f93-141">We could get this correlation from the mapping file included with the weather data.</span></span> <span data-ttu-id="f0f93-142">將天氣資料檔案中的*呼號* (例如 LAX) 欄位對應至航班資料中的*出發地*。</span><span class="sxs-lookup"><span data-stu-id="f0f93-142">By mapping the *CallSign* (for example, LAX) field in the weather data file to *Origin* in the airline data.</span></span> <span data-ttu-id="f0f93-143">不過，我們手邊剛好有另一個已儲存至 CSV 檔案 (“wban-to-airport-id-tz.CSV”) 的可用對應，它將 *WBAN* 對應至 *AirportID* (例如，12892 代表 LAX) ，並且包含 *TimeZone*。</span><span class="sxs-lookup"><span data-stu-id="f0f93-143">However, we just happened to have another mapping on hand that maps *WBAN* to *AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved to a CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="f0f93-144">例如：</span><span class="sxs-lookup"><span data-stu-id="f0f93-144">For example:</span></span>

| <span data-ttu-id="f0f93-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="f0f93-145">AirportID</span></span> | <span data-ttu-id="f0f93-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="f0f93-146">WBAN</span></span> | <span data-ttu-id="f0f93-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="f0f93-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="f0f93-148">10685</span><span class="sxs-lookup"><span data-stu-id="f0f93-148">10685</span></span> | <span data-ttu-id="f0f93-149">54831</span><span class="sxs-lookup"><span data-stu-id="f0f93-149">54831</span></span> | <span data-ttu-id="f0f93-150">-6</span><span class="sxs-lookup"><span data-stu-id="f0f93-150">-6</span></span>
| <span data-ttu-id="f0f93-151">14871</span><span class="sxs-lookup"><span data-stu-id="f0f93-151">14871</span></span> | <span data-ttu-id="f0f93-152">24232</span><span class="sxs-lookup"><span data-stu-id="f0f93-152">24232</span></span> | <span data-ttu-id="f0f93-153">-8</span><span class="sxs-lookup"><span data-stu-id="f0f93-153">-8</span></span>
| <span data-ttu-id="f0f93-154">..</span><span class="sxs-lookup"><span data-stu-id="f0f93-154">..</span></span> | <span data-ttu-id="f0f93-155">..</span><span class="sxs-lookup"><span data-stu-id="f0f93-155">..</span></span> | <span data-ttu-id="f0f93-156">..</span><span class="sxs-lookup"><span data-stu-id="f0f93-156">..</span></span>

<span data-ttu-id="f0f93-157">下列程式碼會讀取每個每小時未經處理的天氣資料檔案、細分為我們所需的資料行、合併天氣觀測站對應檔案、將度量單位的日期時間調整為 UTC，然後將資料寫到新版的檔案：</span><span class="sxs-lookup"><span data-stu-id="f0f93-157">The following code reads each of the hourly raw weather data files, subsets to the columns we need, merges the weather station mapping file, adjusts the date times of measurements to UTC, and then writes out a new version of the file:</span></span>

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

## <a name="importing-the-airline-and-weather-data-to-spark-dataframes"></a><span data-ttu-id="f0f93-158">將航線和天氣資料匯入至 Spark DataFrames</span><span class="sxs-lookup"><span data-stu-id="f0f93-158">Importing the airline and weather data to Spark DataFrames</span></span>

<span data-ttu-id="f0f93-159">現在我們使用 SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) 函式，將天氣和航線資料匯入到 Spark DataFrame。</span><span class="sxs-lookup"><span data-stu-id="f0f93-159">Now we use the SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function to import the weather and airline data to Spark DataFrames.</span></span> <span data-ttu-id="f0f93-160">如同其他許多 Spark 方法一樣，這個函式會延遲執行，意思就是排入佇列等候執行，但等到必要時才會執行。</span><span class="sxs-lookup"><span data-stu-id="f0f93-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for the airline data

logmsg('create a SparkR DataFrame for the airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for the weather data

logmsg('create a SparkR DataFrame for the weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="f0f93-161">資料清理和轉換</span><span class="sxs-lookup"><span data-stu-id="f0f93-161">Data cleansing and transformation</span></span>

<span data-ttu-id="f0f93-162">接下來，我們清理一些已匯入的航線資料，以重新命名資料行。</span><span class="sxs-lookup"><span data-stu-id="f0f93-162">Next we do some cleanup on the airline data we’ve imported to rename columns.</span></span> <span data-ttu-id="f0f93-163">我們只保留需要的變數，並將預定的起飛時間四捨五入到最接近的時間，以將起飛時的最新天氣資料合併：</span><span class="sxs-lookup"><span data-stu-id="f0f93-163">We only keep the variables needed, and round scheduled departure times down to the nearest hour to enable merging with the latest weather data at departure:</span></span>

```
logmsg('clean the airline data') 
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

# Select desired columns from the flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time to full hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="f0f93-164">現在，我們將對天氣資料執行類似作業︰</span><span class="sxs-lookup"><span data-stu-id="f0f93-164">Now we perform similar operations on the weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean the weather data') 
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

## <a name="joining-the-weather-and-airline-data"></a><span data-ttu-id="f0f93-165">聯結天氣與航線資料</span><span class="sxs-lookup"><span data-stu-id="f0f93-165">Joining the weather and airline data</span></span>

<span data-ttu-id="f0f93-166">現在，我們將使用 SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) 函式進行航線與天氣資料的左方外部聯結 (依照起飛 AirportID 和日期時間)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-166">We now use the SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function to do a left outer join of the airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="f0f93-167">外部聯結讓我們能保留所有的航線資料記錄 (即使沒有相符的天氣資料)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-167">The outer join allows us to retain all the airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="f0f93-168">聯結之後，我們會移除一些多餘的資料行，而將保留的資料行重新命名，以移除聯結所引入的內送 DataFrame 前置詞。</span><span class="sxs-lookup"><span data-stu-id="f0f93-168">Following the join, we remove some redundant columns, and rename the kept columns to remove the incoming DataFrame prefix introduced by the join.</span></span>

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

<span data-ttu-id="f0f93-169">我們將以類似的方式，根據抵達 AirportID 和日期時間聯結天氣與航線資料：</span><span class="sxs-lookup"><span data-stu-id="f0f93-169">In a similar fashion, we join the weather and airline data based on arrival AirportID and datetime:</span></span>

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

## <a name="save-results-to-csv-for-exchange-with-scaler"></a><span data-ttu-id="f0f93-170">將結果儲存為 CSV 以便與 ScaleR 交換</span><span class="sxs-lookup"><span data-stu-id="f0f93-170">Save results to CSV for exchange with ScaleR</span></span>

<span data-ttu-id="f0f93-171">SparkR 需要進行的聯結便已完成。</span><span class="sxs-lookup"><span data-stu-id="f0f93-171">That completes the joins we need to do with SparkR.</span></span> <span data-ttu-id="f0f93-172">我們會將最終 Spark DataFrame “joinedDF5” 中的資料儲存為 CSV，以便輸入至 ScaleR，然後關閉 SparkR 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f0f93-172">We save the data from the final Spark DataFrame “joinedDF5” to a CSV for input to ScaleR and then close out the SparkR session.</span></span> <span data-ttu-id="f0f93-173">我們明確告訴 SparkR 在 80 個不同的資料分割中儲存結果產生的 CSV，以在 ScaleR 處理中啟用足夠的平行處理原則：</span><span class="sxs-lookup"><span data-stu-id="f0f93-173">We explicitly tell SparkR to save the resultant CSV in 80 separate partitions to enable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output the joined data from Spark to CSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result to directory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down the SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-to-xdf-for-use-by-scaler"></a><span data-ttu-id="f0f93-174">匯入至 XDF 以供 ScaleR 使用</span><span class="sxs-lookup"><span data-stu-id="f0f93-174">Import to XDF for use by ScaleR</span></span>

<span data-ttu-id="f0f93-175">我們可以依原樣使用聯結航線和天氣資料的 CSV 檔案，以透過 ScaleR 文字資料來源建立模型。</span><span class="sxs-lookup"><span data-stu-id="f0f93-175">We could use the CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="f0f93-176">但我們首先將它匯入 XDF，因為在資料集上執行多個作業時它的效益更高：</span><span class="sxs-lookup"><span data-stu-id="f0f93-176">But we import it to XDF first, since it is more efficient when running multiple operations on the dataset:</span></span>

```
logmsg('Import the CSV to compressed, binary XDF format') 

# set the Spark compute context for R Server 
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

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="f0f93-177">分割資料以供訓練和測試</span><span class="sxs-lookup"><span data-stu-id="f0f93-177">Splitting data for training and test</span></span>

<span data-ttu-id="f0f93-178">我們使用 rxDataStep 分出 2012 年資料進行測試，並保留其餘資料以供訓練：</span><span class="sxs-lookup"><span data-stu-id="f0f93-178">We use rxDataStep to split out the 2012 data for testing and keep the rest for training:</span></span>

```
# split out the training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out the testing data

logmsg('split out the test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="f0f93-179">訓練和測試羅吉斯迴歸模型</span><span class="sxs-lookup"><span data-stu-id="f0f93-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="f0f93-180">現在我們已準備好要建置模型。</span><span class="sxs-lookup"><span data-stu-id="f0f93-180">Now we are ready to build a model.</span></span> <span data-ttu-id="f0f93-181">為了解天氣對抵達時間延誤的影響，我們使用 ScaleR 的羅吉斯迴歸常式。</span><span class="sxs-lookup"><span data-stu-id="f0f93-181">To see the influence of weather data on delay in the arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="f0f93-182">我們使用它來說明超過 15 分鐘的抵達延誤是否受起飛和抵達機場的天氣影響：</span><span class="sxs-lookup"><span data-stu-id="f0f93-182">We use it to model whether an arrival delay of greater than 15 minutes is influenced by the weather at the departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use the scalable rxLogit() function but set max iterations to 3 for the purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="f0f93-183">我們現在進行一些預測並查看 ROC 和 AUC，看看這對於測試資料的作用。</span><span class="sxs-lookup"><span data-stu-id="f0f93-183">Now let’s see how it does on the test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over the test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use the scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under the Curve (AUC).

logmsg('calculate the roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="f0f93-184">在其他位置進行評分</span><span class="sxs-lookup"><span data-stu-id="f0f93-184">Scoring elsewhere</span></span>

<span data-ttu-id="f0f93-185">我們也可以在另一個平台上使用模型對資料評分。</span><span class="sxs-lookup"><span data-stu-id="f0f93-185">We can also use the model for scoring data on another platform.</span></span> <span data-ttu-id="f0f93-186">透過將模型儲存至 RDS 檔案，然後將該 RDS 傳送和匯入目的地評分環境 (例如 SQL Server R 服務)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-186">By saving it to an RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="f0f93-187">請務必確保要評分的資料因子層級符合此模型的建置因子層級。</span><span class="sxs-lookup"><span data-stu-id="f0f93-187">It is important to ensure that the factor levels of the data to be scored match those on which the model was built.</span></span> <span data-ttu-id="f0f93-188">透過 ScaleR 的 `rxCreateColInfo()` 函式擷取和儲存與模型化資料相關聯的資料行資訊，然後將該資料行資訊套用至可供預測的輸入資料來源，即可達到此目的。</span><span class="sxs-lookup"><span data-stu-id="f0f93-188">That match can be achieved by extracting and saving the column infomation associated with the modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information to the input data source for prediction.</span></span> <span data-ttu-id="f0f93-189">在下列範例中，我們會儲存測試資料集的幾個資料列，而且會擷取此範例中的資料行資訊並使用於預測指令碼中：</span><span class="sxs-lookup"><span data-stu-id="f0f93-189">In the following we save a few rows of the test dataset and extract and use the column information from this sample in the prediction script:</span></span>

```
# save the model and a sample of the test dataset 

logmsg('save serialized version of the model and a sample of the test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop the spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="f0f93-190">摘要</span><span class="sxs-lookup"><span data-stu-id="f0f93-190">Summary</span></span>

<span data-ttu-id="f0f93-191">在本文中，我們已示範如何在 Hadoop Spark 中結合使用用於資料操作的 SparkR 和用於模型開發的 ScaleR。</span><span class="sxs-lookup"><span data-stu-id="f0f93-191">In this article, we’ve shown how it’s possible to combine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="f0f93-192">此案例需要維護個別的 Spark 工作階段 (一次僅執行一個工作階段)，並透過 CSV 檔案交換資料。</span><span class="sxs-lookup"><span data-stu-id="f0f93-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="f0f93-193">雖然很簡單，但是當 SparkR 和 ScaleR 可以共用 Spark 工作階段和 Spark DataFrame 時，在後續發行的 R Server 中，此程序應會變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="f0f93-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="f0f93-194">後續步驟和更多資訊</span><span class="sxs-lookup"><span data-stu-id="f0f93-194">Next steps and more information</span></span>

- <span data-ttu-id="f0f93-195">如需在 Spark 上使用 R Server 的詳細資訊，請參閱 [MSDN 上的使用者入門指南](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-195">For more information on use of R Server on Spark, see the [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="f0f93-196">如需 R Server 的一般資訊，請參閱[開始使用 R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) 一文。</span><span class="sxs-lookup"><span data-stu-id="f0f93-196">For general information on R Server, see the [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="f0f93-197">如需 HDInsight 上之 R Server 的詳細資訊，請參閱 [Azure HDInsight 上的 R Server 概觀](hdinsight-hadoop-r-server-overview.md)和 [Azure HDInsight 上的 R Server](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f0f93-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="f0f93-198">如需使用 SparkR 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f0f93-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="f0f93-199">Apache SparkR 文件</span><span class="sxs-lookup"><span data-stu-id="f0f93-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="f0f93-200">Databricks 提供的 [SparkR 概觀](https://docs.databricks.com/spark/latest/sparkr/overview.html)</span><span class="sxs-lookup"><span data-stu-id="f0f93-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
