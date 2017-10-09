---
title: "在動作中的 hello 小組資料科學程序： 使用 SQL 資料倉儲 |Microsoft 文件"
description: "進階分析程序和技術實務"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="9c1fc-103">在動作中的 hello 小組資料科學程序： 使用 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9c1fc-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="9c1fc-104">在本教學課程中，我們會逐步引導您建立及部署使用 SQL 資料倉儲 (SQL DW) 的機器學習模型公開可用的資料集-hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="9c1fc-105">建構的 hello 二元分類模型會預測提示支付路線，以及多級分類和迴歸模型，也會探討預測 hello 發佈 hello 提示金額付費。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="9c1fc-106">hello 程序會遵循 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)工作流程。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="9c1fc-107">我們會示範如何 toosetup 資料科學環境中，如何 tooload hello 資料到 SQL DW 及如何使用 SQL DW 或 IPython 筆記型電腦 tooexplore hello 資料和工程師功能 toomodel。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="9c1fc-108">然後顯示如何 toobuild 和部署 Azure 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="9c1fc-109"><a name="dataset"></a>hello NYC 計程車往返的資料集</span><span class="sxs-lookup"><span data-stu-id="9c1fc-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="9c1fc-110">hello NYC 計程車路線資料包含約 20 GB 的壓縮的 CSV 檔案 (~ 48 GB 未壓縮)，錄製超過 173 百萬個個別的往返和 hello fares 支付每往返作業。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="9c1fc-111">每個往返記錄包括 hello 收取和下車位置以及時間、 匿名 hack (driver) 授權編號，並重新 hello medallion (計程車的唯一 id) 數目。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="9c1fc-112">hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c1fc-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="9c1fc-113">hello **trip_data.csv**檔案包含路線詳細資料，例如乘客、 收取和 dropoff 點、 路線期間與路線長度的數目。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="9c1fc-114">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="9c1fc-115">hello **trip_fare.csv**檔案包含的 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="9c1fc-116">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="9c1fc-117">hello**唯一索引鍵**用 toojoin 路線\_資料和路線\_價位組成 hello 下列三個欄位：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="9c1fc-118">medallion、</span><span class="sxs-lookup"><span data-stu-id="9c1fc-118">medallion,</span></span>
* <span data-ttu-id="9c1fc-119">hack\_license 和</span><span class="sxs-lookup"><span data-stu-id="9c1fc-119">hack\_license and</span></span>
* <span data-ttu-id="9c1fc-120">pickup\_datetime。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-120">pickup\_datetime.</span></span>

## <span data-ttu-id="9c1fc-121"><a name="mltasks"></a>處理三種類型的預測工作</span><span class="sxs-lookup"><span data-stu-id="9c1fc-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="9c1fc-122">我們制訂根據 hello 的三個預測問題*提示\_量*tooillustrate 三種模型化工作：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="9c1fc-123">**二元分類**: toopredict 是否提示支付路線，也就是*提示\_量*大比 $0 為正數的範例，而*提示\_量* $0 是負的範例。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="9c1fc-124">**多級分類**: hello 路線支付 toopredict hello 範圍的提示。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="9c1fc-125">我們將 hello*提示\_量*到五個紙匣或類別：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="9c1fc-126">**迴歸工作**: toopredict hello 數量提示支付路線。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="9c1fc-127"><a name="setup"></a>設定進階分析 hello Azure 資料科學環境</span><span class="sxs-lookup"><span data-stu-id="9c1fc-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="9c1fc-128">tooset Azure 資料科學環境，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="9c1fc-129">**建立自己的 Azure Blob 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="9c1fc-130">當您佈建您自己的 Azure blob 儲存體時，選擇 Azure blob 儲存體中或盡可能接近的地理位置太**美國中南部**，這是儲存 hello NYC 計程車資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="9c1fc-131">會使用您自己的儲存體帳戶中所提供的 hello 公用 blob 儲存體容器 tooa 容器 AzCopy 複製 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="9c1fc-132">hello 接近您的 Azure blob 儲存體是 tooSouth 美國中部、 hello 速度 (步驟 4)，這項工作將會完成。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="9c1fc-133">toocreate 您自己的 Azure 儲存體帳戶，步驟所述，在後續 hello[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="9c1fc-134">在此逐步解說稍後會需要這些是確定 toomake 注意事項 hello 值，如下列儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="9c1fc-135">**儲存體帳戶名稱**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="9c1fc-136">**儲存體帳戶金鑰**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="9c1fc-137">**容器名稱**（其中要儲存在 hello Azure blob 儲存體中的 hello 資料 toobe）</span><span class="sxs-lookup"><span data-stu-id="9c1fc-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="9c1fc-138">**佈建 Azure SQL DW 執行個體。**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="9c1fc-139">請遵循 hello 文件，網址[建立 SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)tooprovision SQL 資料倉儲執行個體。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="9c1fc-140">請確定您遵循 SQL 資料倉儲的認證將用於在稍後步驟中的 hello 上進行標記法。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="9c1fc-141">**伺服器名稱**：<server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="9c1fc-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="9c1fc-142">**SQLDW (資料庫) 名稱**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="9c1fc-143">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-143">**Username**</span></span>
* <span data-ttu-id="9c1fc-144">**密碼**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-144">**Password**</span></span>

<span data-ttu-id="9c1fc-145">**安裝 Visual Studio 和 SQL Server Data Tools。**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="9c1fc-146">如需指示，請參閱 [安裝適用於 SQL 資料倉儲的 Visual Studio 2015 及/或 SSDT (SQL Server Data Tools)](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md)中概述的步驟。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="9c1fc-147">**使用 Visual Studio 中連接 tooyour Azure SQL DW。**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="9c1fc-148">如需指示，請參閱 < 步驟 1 和 2 中的[連接 Visual Studio 中的 SQL 資料倉儲 tooAzure](../sql-data-warehouse/sql-data-warehouse-connect-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-149">執行 hello 下列在您的 SQL 資料倉儲中建立 hello 資料庫上的 SQL 查詢 （而不是所提供的 hello 步驟 3 中的 hello 查詢連接 > 主題） 太**建立主要金鑰**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="9c1fc-150">**在 Azure 訂用帳戶下建立 Azure Machine Learning 工作區。**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="9c1fc-151">如需指示，請參閱 [建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)中概述的步驟。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="9c1fc-152"><a name="getdata"></a>Hello 資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9c1fc-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="9c1fc-153">開啟 Windows PowerShell 命令主控台。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="9c1fc-154">執行 hello 下列 PowerShell 命令 toodownload hello 範例 SQL 指令碼檔案我們與您共用 GitHub tooa 本機目錄上您指定與 hello 參數*-DestDir*。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="9c1fc-155">您可以變更參數值 hello *-DestDir* tooany 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="9c1fc-156">如果*-DestDir*不存在，則會建立由 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-157">您可能需要**系統管理員身分執行**執行下列 PowerShell 指令碼，如果 hello 時您*DestDir*需系統管理員權限 toocreate 或 toowrite tooit 目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="9c1fc-158">成功執行之後，您目前的工作目錄太變更*-DestDir*。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="9c1fc-159">您應該會類似如下的 toosee 螢幕：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="9c1fc-160">在您*-DestDir*，執行下列 PowerShell 指令碼，以系統管理員模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c1fc-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="9c1fc-161">當 hello PowerShell 指令碼執行 hello 第一次時，您會從您的 Azure SQL DW 和 Azure blob 儲存體帳戶要求 tooinput hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="9c1fc-162">這個 PowerShell 指令碼完成時執行第一次，hello 認證 hello 您輸入將已經寫入 tooa 組態檔 SQLDW.conf hello 存在的工作目錄中。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="9c1fc-163">hello 未來執行這個 PowerShell 指令碼檔案有 hello 選項 tooread 所需的所有參數從這個組態檔。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="9c1fc-164">如果您需要 toochange 某些參數時，您可以選擇 tooinput hello 囉 」 畫面時刪除這個組態檔，並在出現提示時輸入 hello 參數值的提示字元或 toochange hello 參數值的參數，藉由編輯 hello SQLDW.conf 檔案在您*-DestDir*目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-165">在訂單 tooavoid 結構描述名稱衝突與已存在於 Azure SQL DW 中，直接從 hello SQLDW.conf 檔案讀取參數時，3 位數的隨機數字加入 toohello 結構描述名稱從 hello SQLDW.conf 檔案做為 hello 預設結構描述名稱每次執行。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="9c1fc-166">hello PowerShell 指令碼可能會提示您輸入的結構描述名稱： hello 名稱可指定使用者自行決定。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="9c1fc-167">這**PowerShell 指令碼**檔完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c1fc-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="9c1fc-168">如果尚未安裝 AzCopy，請**下載並安裝 AzCopy**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="9c1fc-169">**複製資料 tooyour 私用 blob 儲存體帳戶**從利用 azcopy 進行 hello 公用 blob</span><span class="sxs-lookup"><span data-stu-id="9c1fc-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="9c1fc-170">**載入資料，使用 Polybase （藉由執行 LoadDataToSQLDW.sql） tooyour Azure SQL DW**從私用 blob 儲存體帳戶以 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="9c1fc-171">建立結構描述</span><span class="sxs-lookup"><span data-stu-id="9c1fc-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="9c1fc-172">建立資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="9c1fc-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="9c1fc-173">建立 Azure 儲存體 Blob 的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="9c1fc-174">建立 CSV 檔案的外部檔案格式。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="9c1fc-175">未壓縮的資料，並以 hello 管道字元分隔的欄位。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="9c1fc-176">為 Azure Blob 儲存體的 NYC 計程車資料集建立外部 fare 和 trip 資料表。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="9c1fc-177">從 Azure blob 儲存體 tooSQL 資料倉儲內的外部資料表載入資料</span><span class="sxs-lookup"><span data-stu-id="9c1fc-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="9c1fc-178">建立範例資料表 (NYCTaxi_Sample) 並插入資料 tooit 選取 hello 行程及價位資料表上的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="9c1fc-179">（這個逐步解說的部分步驟需要 toouse 這個範例資料表。）</span><span class="sxs-lookup"><span data-stu-id="9c1fc-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="9c1fc-180">hello 的儲存體帳戶的地理位置會影響載入時間。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-181">根據 hello 私用 blob 儲存體帳戶的地理位置、 公用 blob tooyour 私人儲存體帳戶複製資料 hello 程序需要大約 15 分鐘的時間，或甚至更久，與 hello 程序的儲存體帳戶中的資料載入Azure SQL DW tooyour 花費 20 分鐘或更長。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="9c1fc-182">您必須 toodecide 如果您有重複的來源和目的地檔案該怎麼做。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-183">如果已經從 hello 公用 blob 儲存體 tooyour 私用 blob 儲存體帳戶複製 hello.csv 檔案 toobe 存在於私用 blob 儲存體帳戶，AzCopy 會詢問您是否要 toooverwrite 它們。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="9c1fc-184">如果您不想 toooverwrite 它們，請輸入 **n** 出現提示時。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="9c1fc-185">如果您想 toooverwrite**所有**項目，請輸入出現提示時。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="9c1fc-186">您也可以輸入**y** toooverwrite.csv 個別檔案。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![圖 #21][21]

<span data-ttu-id="9c1fc-188">您可以使用自己的資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-188">You can use your own data.</span></span> <span data-ttu-id="9c1fc-189">如果您的資料位於內部部署電腦應用程式的真實生活中，您仍然可以使用 AzCopy tooupload 在內部部署資料 tooyour 私用的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="9c1fc-190">您只需要 toochange hello**來源**位置， `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`，在 hello hello PowerShell 指令碼檔案 toohello 本機目錄，包含資料的 AzCopy 命令。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="9c1fc-191">如果您的資料已在您應用程式的真實生活中的私用的 Azure blob 儲存體中，您可以略過的 hello AzCopy hello PowerShell 指令碼中的步驟，並直接上傳 hello 資料 tooAzure SQL DW。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="9c1fc-192">這將需要其他編輯的 hello 指令碼 tootailor 它 toohello 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="9c1fc-193">這個 Powershell 指令碼也插入 hello Azure SQL DW 資訊至 hello 資料瀏覽範例檔案 SQLDW_Explorations.sql，SQLDW_Explorations.ipynb 和 SQLDW_Explorations_Scripts.py 如此這三個檔案會立即嘗試準備 toobehello PowerShell 指令碼完成。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="9c1fc-194">成功執行之後，您會看到如下畫面：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="9c1fc-195"><a name="dbexplore"></a>Azure SQL 資料倉儲中的資料探索和特徵工程</span><span class="sxs-lookup"><span data-stu-id="9c1fc-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9c1fc-196">在本節中，我們會使用 **Visual Studio Data Tools**直接對 Azure SQL DW 執行 SQL 查詢，以探索資料和產生特徵。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="9c1fc-197">使用本節中的所有 SQL 查詢可以都在 hello 範例指令碼名為*SQLDW_Explorations.sql*。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="9c1fc-198">這個檔案已下載的 tooyour hello PowerShell 指令碼的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="9c1fc-199">您也可以從 [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql) 擷取此檔案。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="9c1fc-200">但在 GitHub 中的 hello 檔案沒有 hello Azure SQL DW 資訊插入。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="9c1fc-201">連接 tooyour Azure SQL DW hello SQL DW 登入名稱和密碼使用 Visual Studio，並開啟 hello **SQL 物件總管**tooconfirm hello 資料庫和資料表已匯入。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="9c1fc-202">擷取 hello *SQLDW_Explorations.sql*檔案。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="9c1fc-203">tooopen Parallel Data Warehouse (PDW) 查詢編輯器中，使用 hello**新查詢**命令，讓您 PDW 中 hello 選取**SQL 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="9c1fc-204">PDW 不支援 hello 標準 SQL 查詢編輯器。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="9c1fc-205">以下是 hello 類型的資料探索和功能產生的工作執行這一節：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="9c1fc-206">在變動的時間範圍中探索數個欄位的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="9c1fc-207">調查 hello 經度和緯度欄位的資料品質。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="9c1fc-208">產生二進位和多級分類標籤根據 hello**提示\_量**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="9c1fc-209">產生功能，並計算或比較車程距離。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="9c1fc-210">聯結 hello 兩個資料表，和擷取將會使用的 toobuild 模型的隨機取樣。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="9c1fc-211">資料匯入驗證</span><span class="sxs-lookup"><span data-stu-id="9c1fc-211">Data import verification</span></span>
<span data-ttu-id="9c1fc-212">這些查詢提供快速驗證數目的資料列和資料行中 hello 資料表填入先前使用 Polybase 的平行大量匯入，hello</span><span class="sxs-lookup"><span data-stu-id="9c1fc-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="9c1fc-213">**輸出：** 您應該有 173,179,759 個資料列和 14 個資料行。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="9c1fc-214">探索：依據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="9c1fc-215">這個範例查詢會識別特定的時間週期內完成超過 100 個往返的 hello medallions （計程車數字）。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="9c1fc-216">hello 查詢獲益 hello 分割資料表的存取因為它由 hello 分割區配置所**收取\_datetime**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="9c1fc-217">查詢 hello 完整資料集也會進行 hello 資料分割資料表的使用及/或索引掃描。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="9c1fc-218">**輸出：** hello 查詢應該傳回具有指定 hello 13,369 medallions (taxis) 的資料列的資料表和 hello 路線 2013年中已完成的數目。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="9c1fc-219">hello 最後一個資料行包含 hello 的往返次數已完成的 hello 的計數。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="9c1fc-220">探索：依據 medallion 和 hack_license 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="9c1fc-221">這個範例會識別 hello medallions （計程車數字） 和 hack_license 數字 （驅動程式） 完成的多個 100 往返指定的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="9c1fc-222">**輸出：** hello 查詢應該傳回 13,369 指定 hello 13,369 汽車/驅動程式已完成多該 100 往返 2013年中的識別碼的資料列的資料表。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="9c1fc-223">hello 最後一個資料行包含 hello 的往返次數已完成的 hello 的計數。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="9c1fc-224">資料品質評估：驗證含有不正確經度和/或緯度的記錄</span><span class="sxs-lookup"><span data-stu-id="9c1fc-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="9c1fc-225">此範例中，以調查如果任一個 hello 經度和/或緯度的欄位可能包含無效的值 （弧度角度應該介於-90 到 90 之間），或具有 （0，0） 座標。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="9c1fc-226">**輸出：** hello 查詢會傳回具有無效的經度和/或緯度欄位 837,467 往返。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="9c1fc-227">探索：已支付小費和未支付小費的車程分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="9c1fc-228">此範例會尋找 hello 已傾斜與 hello 數目，已不傾斜指定的時間內 （或在 hello 完整資料集，如果它已設定此處涵蓋 hello 完整的年份） 的往返次數。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="9c1fc-229">此分佈會反映 hello 二進位標籤發佈 toobe 稍後用於二元分類模型。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="9c1fc-230">**輸出：** hello 查詢應該傳回 hello 下列秘訣頻率 hello 年份 2013年: 90,447,622 傾斜和 82,264,709 not 傾斜。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="9c1fc-231">探索：小費類別/範圍分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="9c1fc-232">此範例會計算 hello 布提示範圍中指定的時間週期 （或在 hello 完整資料集，如果涵蓋 hello 完整年）。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="9c1fc-233">這是 hello 發佈的 hello 標籤類別會用於多級分類模型的更新版本。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="9c1fc-234">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="9c1fc-234">**Output:**</span></span>

| <span data-ttu-id="9c1fc-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="9c1fc-235">tip_class</span></span> | <span data-ttu-id="9c1fc-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="9c1fc-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="9c1fc-237">1</span><span class="sxs-lookup"><span data-stu-id="9c1fc-237">1</span></span> |<span data-ttu-id="9c1fc-238">82230915</span><span class="sxs-lookup"><span data-stu-id="9c1fc-238">82230915</span></span> |
| <span data-ttu-id="9c1fc-239">2</span><span class="sxs-lookup"><span data-stu-id="9c1fc-239">2</span></span> |<span data-ttu-id="9c1fc-240">6198803</span><span class="sxs-lookup"><span data-stu-id="9c1fc-240">6198803</span></span> |
| <span data-ttu-id="9c1fc-241">3</span><span class="sxs-lookup"><span data-stu-id="9c1fc-241">3</span></span> |<span data-ttu-id="9c1fc-242">1932223</span><span class="sxs-lookup"><span data-stu-id="9c1fc-242">1932223</span></span> |
| <span data-ttu-id="9c1fc-243">0</span><span class="sxs-lookup"><span data-stu-id="9c1fc-243">0</span></span> |<span data-ttu-id="9c1fc-244">82264625</span><span class="sxs-lookup"><span data-stu-id="9c1fc-244">82264625</span></span> |
| <span data-ttu-id="9c1fc-245">4</span><span class="sxs-lookup"><span data-stu-id="9c1fc-245">4</span></span> |<span data-ttu-id="9c1fc-246">85765</span><span class="sxs-lookup"><span data-stu-id="9c1fc-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="9c1fc-247">探索：計算並比較車程距離</span><span class="sxs-lookup"><span data-stu-id="9c1fc-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="9c1fc-248">這個範例會將轉換 hello 收取和下車經度和緯度 tooSQL geography 點、 計算 hello 旅行距離使用 SQL geography 點差異，並傳回隨機取樣的 hello 比較結果。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="9c1fc-249">hello 範例限制 hello toovalid 協調只能使用稍早討論的 hello 資料品質評估查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="9c1fc-250">使用 SQL 函式的功能工程</span><span class="sxs-lookup"><span data-stu-id="9c1fc-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="9c1fc-251">有時 SQL 函式會是有效率進行功能工程的合適選項。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="9c1fc-252">在本逐步解說中，我們會定義 SQL 函式 toocalculate hello 直接之間的距離 hello 收取和 dropoff 位置。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="9c1fc-253">您可以執行下列 SQL 指令碼中的 hello **Visual Studio Data Tools**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="9c1fc-254">以下是定義 hello 距離函式的 hello SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="9c1fc-255">以下是範例 toocall 此函式 toogenerate 功能在 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="9c1fc-256">**輸出：**收取和 dropoff 經緯度與此查詢會產生的資料表 （含 2,803,538 資料列） 和您該與 hello 對應導向英里內的距離。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="9c1fc-257">前 3 個資料列的 hello 結果如下：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="9c1fc-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="9c1fc-258">pickup_latitude</span></span> | <span data-ttu-id="9c1fc-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="9c1fc-259">pickup_longitude</span></span> | <span data-ttu-id="9c1fc-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="9c1fc-260">dropoff_latitude</span></span> | <span data-ttu-id="9c1fc-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="9c1fc-261">dropoff_longitude</span></span> | <span data-ttu-id="9c1fc-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="9c1fc-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9c1fc-263">1</span><span class="sxs-lookup"><span data-stu-id="9c1fc-263">1</span></span> |<span data-ttu-id="9c1fc-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="9c1fc-264">40.731804</span></span> |<span data-ttu-id="9c1fc-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="9c1fc-265">-74.001083</span></span> |<span data-ttu-id="9c1fc-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="9c1fc-266">40.736622</span></span> |<span data-ttu-id="9c1fc-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="9c1fc-267">-73.988953</span></span> |<span data-ttu-id="9c1fc-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="9c1fc-268">.7169601222</span></span> |
| <span data-ttu-id="9c1fc-269">2</span><span class="sxs-lookup"><span data-stu-id="9c1fc-269">2</span></span> |<span data-ttu-id="9c1fc-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="9c1fc-270">40.715794</span></span> |<span data-ttu-id="9c1fc-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="9c1fc-271">-74,010635</span></span> |<span data-ttu-id="9c1fc-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="9c1fc-272">40.725338</span></span> |<span data-ttu-id="9c1fc-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="9c1fc-273">-74.00399</span></span> |<span data-ttu-id="9c1fc-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="9c1fc-274">.7448343721</span></span> |
| <span data-ttu-id="9c1fc-275">3</span><span class="sxs-lookup"><span data-stu-id="9c1fc-275">3</span></span> |<span data-ttu-id="9c1fc-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="9c1fc-276">40.761456</span></span> |<span data-ttu-id="9c1fc-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="9c1fc-277">-73.999886</span></span> |<span data-ttu-id="9c1fc-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="9c1fc-278">40.766544</span></span> |<span data-ttu-id="9c1fc-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="9c1fc-279">-73.988228</span></span> |<span data-ttu-id="9c1fc-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="9c1fc-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="9c1fc-281">準備資料以進行模型建置</span><span class="sxs-lookup"><span data-stu-id="9c1fc-281">Prepare data for model building</span></span>
<span data-ttu-id="9c1fc-282">hello 下列查詢會聯結 hello **nyctaxi\_路線**和**nyctaxi\_價位**資料表時，會產生二進位分類標籤**傾斜**、多級分類標籤**提示\_類別**，然後從 hello 完整聯結的資料集擷取的範例。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="9c1fc-283">hello 取樣是擷取 hello 往返收取時間為基礎的子集。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="9c1fc-284">此查詢可以複製，然後直接在 hello 貼入[Azure Machine Learning Studio](https://studio.azureml.net) [匯入資料][ import-data] hello SQL 資料庫執行個體中的直接資料擷取的模組在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="9c1fc-285">hello 查詢排除具有不正確的記錄 （0，0） 座標。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="9c1fc-286">當您準備好 tooproceed tooAzure 機器學習服務，您可以：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="9c1fc-287">儲存 hello 最終 SQL 查詢 tooextract 和範例 hello 資料和複製-貼上 hello 查詢直接[匯入資料][ import-data]模組在 Azure Machine Learning 中，或</span><span class="sxs-lookup"><span data-stu-id="9c1fc-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="9c1fc-288">保存取樣的 hello 與工程的資料您計劃 toouse 模型建立新的 SQL DW 中的資料表，並在 hello 使用 hello 新資料表[匯入資料][ import-data] Azure Machine Learning 中的模組。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="9c1fc-289">hello PowerShell 指令碼，在先前步驟中所做的這。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="9c1fc-290">您可以直接從這個資料表 hello 資料匯入模組中讀取。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="9c1fc-291"><a name="ipnb"></a>IPython Notebook 中的資料探索和特徵工程設計</span><span class="sxs-lookup"><span data-stu-id="9c1fc-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="9c1fc-292">在本節中，我們將會執行資料探索和使用這兩個 Python 的功能產生並稍早建立 hello SQL DW 的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="9c1fc-293">名為範例 IPython 筆記型電腦**SQLDW_Explorations.ipynb**和 Python 指令碼檔案**SQLDW_Explorations_Scripts.py**已下載的 tooyour 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="9c1fc-294">您也可以在 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW)上取得這兩個檔案。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="9c1fc-295">在 Python 指令碼中，這兩個檔案是相同的。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="9c1fc-296">如果您沒有 IPython Notebook 伺服器，會提供 tooyou hello Python 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="9c1fc-297">這兩個範例 Python 檔案是以 **Python 2.7**設計。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="9c1fc-298">hello hello 範例 IPython 筆記型電腦中所需的 Azure SQL DW 資訊和 hello 的 Python 指令碼檔案下載的 tooyour 本機電腦已插入 hello PowerShell 指令碼之前。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="9c1fc-299">因此，不必進行任何修改就可以執行。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-299">They are executable without any modification.</span></span>

<span data-ttu-id="9c1fc-300">如果您已經設定 AzureML 工作區，您就可以直接上傳 hello 範例 IPython 筆記型電腦 toohello AzureML IPython 筆記型電腦服務，並開始執行。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="9c1fc-301">以下是 hello 步驟 tooupload tooAzureML IPython 筆記型電腦服務：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="9c1fc-302">登入 tooyour AzureML 工作區，在 hello 頂端，按一下 「 Studio 」 然後按一下 [筆記型電腦] 左側 hello hello 網頁。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![圖 #22][22]
2. <span data-ttu-id="9c1fc-304">Hello 左下角的 hello 網頁上，按一下 [新增]，然後選取 「 Python 2"。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="9c1fc-305">接著，提供名稱 toohello 筆記本，然後按一下 hello 核取記號 toocreate hello 新空白 IPython 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![圖 #23][23]
3. <span data-ttu-id="9c1fc-307">按一下 hello"Jupyter"符號 hello 左角 hello 新 IPython 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![圖 #24][24]
4. <span data-ttu-id="9c1fc-309">拖曳和卸除 hello 範例 IPython 筆記型電腦 toohello**樹狀**您 AzureML IPython 筆記型電腦服務，然後按一下頁面**上傳**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="9c1fc-310">然後，hello 範例 IPython 筆記型電腦將上傳的 toohello AzureML IPython 筆記型電腦服務。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![圖 #25][25]

<span data-ttu-id="9c1fc-312">在訂單 toorun hello 範例 IPython 筆記型電腦或 hello Python 指令碼檔案，hello 下列 Python 封裝所需。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="9c1fc-313">如果您使用 hello AzureML IPython 筆記型電腦服務，已預先安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="9c1fc-314">pandas</span><span class="sxs-lookup"><span data-stu-id="9c1fc-314">pandas</span></span>
    - <span data-ttu-id="9c1fc-315">numpy</span><span class="sxs-lookup"><span data-stu-id="9c1fc-315">numpy</span></span>
    - <span data-ttu-id="9c1fc-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="9c1fc-316">matplotlib</span></span>
    - <span data-ttu-id="9c1fc-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="9c1fc-317">pyodbc</span></span>
    - <span data-ttu-id="9c1fc-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="9c1fc-318">PyTables</span></span>

<span data-ttu-id="9c1fc-319">hello AzureML 上建立進階分析解決方案，大型資料時，建議順序為 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="9c1fc-320">在 hello 資料的小型範例讀入記憶體中的資料框架。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="9c1fc-321">執行一些視覺效果，並使用瀏覽 hello 取樣的資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="9c1fc-322">實驗功能使用 hello 取樣資料的工程團隊。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="9c1fc-323">對於較大的資料瀏覽、 資料操作和特徵設計使用 Python tooissue SQL 查詢，直接對 SQL DW hello。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="9c1fc-324">決定 hello 範例大小 toobe 適用於 Azure 機器學習模型建立。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="9c1fc-325">hello 以下是幾個資料探索、 資料視覺效果和功能工程範例。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="9c1fc-326">Hello 範例 IPython 筆記型電腦與 hello 範例 Python 指令碼檔案中可以找到更多的資料瀏覽。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="9c1fc-327">初始化資料庫認證</span><span class="sxs-lookup"><span data-stu-id="9c1fc-327">Initialize database credentials</span></span>
<span data-ttu-id="9c1fc-328">初始化 hello 下列變數中的資料庫連線設定：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="9c1fc-329">建立資料庫連接</span><span class="sxs-lookup"><span data-stu-id="9c1fc-329">Create database connection</span></span>
<span data-ttu-id="9c1fc-330">以下是 hello 建立 hello 連線 toohello 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="9c1fc-331">報告資料表 <nyctaxi_trip> 中資料列和資料行的數目</span><span class="sxs-lookup"><span data-stu-id="9c1fc-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="9c1fc-332">資料列總數 = 173179759</span><span class="sxs-lookup"><span data-stu-id="9c1fc-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="9c1fc-333">資料行總數 = 14</span><span class="sxs-lookup"><span data-stu-id="9c1fc-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="9c1fc-334">報告資料表 <nyctaxi_fare> 中資料列和資料行的數目</span><span class="sxs-lookup"><span data-stu-id="9c1fc-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="9c1fc-335">資料列總數 = 173179759</span><span class="sxs-lookup"><span data-stu-id="9c1fc-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="9c1fc-336">資料行總數 = 11</span><span class="sxs-lookup"><span data-stu-id="9c1fc-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="9c1fc-337">讀取在小型資料中的範例 hello SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="9c1fc-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="9c1fc-338">時間 tooread hello 範例資料表為 14.096495 秒。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="9c1fc-339">擷取的資料列和資料行數目 = (1000, 21)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="9c1fc-340">描述性統計資料</span><span class="sxs-lookup"><span data-stu-id="9c1fc-340">Descriptive statistics</span></span>
<span data-ttu-id="9c1fc-341">現在您已準備好 tooexplore hello 取樣資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="9c1fc-342">我們以查看一些描述性統計資料的 hello 開頭**路線\_距離**（或任何其他欄位選擇 toospecify）。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="9c1fc-343">視覺效果：盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="9c1fc-343">Visualization: Box plot example</span></span>
<span data-ttu-id="9c1fc-344">我們會審視 hello 盒狀圖 hello 旅行距離 toovisualize hello 分位數下一步。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![圖 #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="9c1fc-346">視覺效果：分佈的盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="9c1fc-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="9c1fc-347">視覺化 hello 發佈和 hello 長條圖的繪圖取樣旅行距離。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![圖 #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="9c1fc-349">視覺效果：長條圖和折線圖</span><span class="sxs-lookup"><span data-stu-id="9c1fc-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="9c1fc-350">在此範例中，我們可以分類收納成五個分類收納 hello 旅行距離和視覺化 hello 分類收納的結果。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="9c1fc-351">我們可以繪製 hello 上方列中的分類收納發佈或線條繪圖與：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![圖 #3][3]

<span data-ttu-id="9c1fc-353">和</span><span class="sxs-lookup"><span data-stu-id="9c1fc-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![圖 #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="9c1fc-355">視覺效果：散佈圖範例</span><span class="sxs-lookup"><span data-stu-id="9c1fc-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="9c1fc-356">我們顯示散佈圖之間**路線\_時間\_中\_秒**和**路線\_距離**toosee 如果有任何相互關聯</span><span class="sxs-lookup"><span data-stu-id="9c1fc-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![圖 #6][6]

<span data-ttu-id="9c1fc-358">同樣地，我們可以檢查 hello 之間的關聯性**速率\_程式碼**和**路線\_距離**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![圖 #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="9c1fc-360">在 IPython Notebook 中使用 SQL 查詢對取樣資料進行資料探索</span><span class="sxs-lookup"><span data-stu-id="9c1fc-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="9c1fc-361">在本節中，我們會探討使用保存 hello 前面所建立的新資料表中的 hello 取樣資料的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="9c1fc-362">請注意，可以使用 hello 原始資料表執行類似的瀏覽。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="9c1fc-363">瀏覽： 報表數目資料列和資料行中 hello 取樣的資料表</span><span class="sxs-lookup"><span data-stu-id="9c1fc-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="9c1fc-364">探索：已支付小費/未支付小費的分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="9c1fc-365">探索：小費類別分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="9c1fc-366">瀏覽： 繪製 hello 提示發佈由類別</span><span class="sxs-lookup"><span data-stu-id="9c1fc-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![圖 #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="9c1fc-368">探索：車程的每日分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="9c1fc-369">探索：根據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="9c1fc-370">探索：依據計程車牌照和計程車駕照的車程分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="9c1fc-371">探索：車程時間分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="9c1fc-372">探索：車程距離分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="9c1fc-373">探索：付款類型分佈</span><span class="sxs-lookup"><span data-stu-id="9c1fc-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="9c1fc-374">確認 hello 最終格式的 hello 特徵化資料表</span><span class="sxs-lookup"><span data-stu-id="9c1fc-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="9c1fc-375"><a name="mlmodel"></a>在 Azure Machine Learning 中建置模型</span><span class="sxs-lookup"><span data-stu-id="9c1fc-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="9c1fc-376">現在，我們已準備好 tooproceed toomodel 建置和中的模型部署[Azure Machine Learning](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="9c1fc-377">hello 資料是用在 hello 預測問題，也就是先前定義的任何準備好 toobe:</span><span class="sxs-lookup"><span data-stu-id="9c1fc-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="9c1fc-378">**二元分類**: toopredict 提示是否支付路線。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="9c1fc-379">**多級分類**: toopredict hello 範圍的提示，根據 toohello 先前定義的類別。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="9c1fc-380">**迴歸工作**: toopredict hello 數量提示支付路線。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="9c1fc-381">toobegin hello 模型練習中，登入 tooyour **Azure Machine Learning**工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="9c1fc-382">如果您尚未建立機器學習服務工作區，請參閱「 [建立 Azure ML 工作區](machine-learning-create-workspace.md)」。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="9c1fc-383">tooget 開始使用 Azure Machine Learning 中，請參閱[什麼是 Azure Machine Learning Studio？](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="9c1fc-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="9c1fc-384">登入太[Azure Machine Learning Studio](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="9c1fc-385">hello Studio 首頁上提供豐富的資訊、 視訊、 教學課程中，連結 toohello 模組參考和其他資源。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="9c1fc-386">如需有關 Azure Machine Learning 的詳細資訊，請參閱 hello [Azure 機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="9c1fc-387">典型的訓練實驗組成 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="9c1fc-388">建立 **+NEW** 實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="9c1fc-389">進入 Azure ML hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="9c1fc-390">前置處理、 轉換和視需要處理 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="9c1fc-391">視需要產生功能。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-391">Generate features as needed.</span></span>
5. <span data-ttu-id="9c1fc-392">Hello 資料分割為訓練/驗證/測試資料集 (或有個別的資料集的每個)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="9c1fc-393">選取一或多個機器學習演算法根據學習問題 toosolve hello。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="9c1fc-394">例如，二進位分類、多類別分類、迴歸。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="9c1fc-395">培訓使用 hello 定型資料集的一或多個模型。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="9c1fc-396">得分 hello 驗證資料集使用 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="9c1fc-397">評估 hello 模型 toocompute hello 相關的度量 hello 學習問題。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="9c1fc-398">微調 hello 模型和選取 hello 最佳模型 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="9c1fc-399">在此練習中，我們已經瀏覽和工程 hello SQL 資料倉儲中的資料，並在 Azure ML hello 範例大小 tooingest 決定。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="9c1fc-400">一或多個 hello 預測模型，以下是 hello 程序 toobuild:</span><span class="sxs-lookup"><span data-stu-id="9c1fc-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="9c1fc-401">Hello 資料送入使用 hello Azure ML[匯入資料][ import-data]模組，用於 hello**資料輸入和輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="9c1fc-402">如需詳細資訊，請參閱 hello[匯入資料][ import-data]模組參考頁面。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Azure ML 匯入資料][17]
2. <span data-ttu-id="9c1fc-404">選取**Azure SQL Database**為 hello**資料來源**在 hello**屬性**面板。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="9c1fc-405">輸入 hello 資料庫 DNS 名稱在 hello**資料庫伺服器名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="9c1fc-406">格式： `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="9c1fc-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="9c1fc-407">輸入 hello**資料庫名稱**hello 對應欄位中。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="9c1fc-408">輸入 hello *SQL 使用者名稱*在 hello**伺服器使用者帳戶名稱**，和 hello*密碼*在 hello**伺服器使用者帳戶密碼**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="9c1fc-409">檢查 hello**接受任何伺服器憑證**選項。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="9c1fc-410">在 hello**資料庫查詢**編輯文字區域中，貼上 hello 查詢 hello 必要資料庫欄位 （包括任何計算的欄位，例如 hello 標籤） 和向下會擷取範例 hello 資料所需的 toohello 取樣大小。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="9c1fc-411">二元分類實驗，直接從 hello SQL 資料倉儲資料庫讀取資料的範例是在 hello 圖中 (請記住 tooreplace hello 資料表名稱 nyctaxi_trip 及 nyctaxi_fare hello 結構描述名稱和 hello 資料表名稱中使用程式逐步解說）。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="9c1fc-412">您可以針對多類別分類和迴歸問題建構類似的實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML 訓練][10]

> [!IMPORTANT]
> <span data-ttu-id="9c1fc-414">在 hello 模型化資料擷取和取樣的查詢範例提供上一節， **hello 三個模型練習的所有標籤都包含在 hello 查詢**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="9c1fc-415">（必要） 的重要步驟，在每個模型化練習 hello 太**排除**hello hello 不必要的標籤，其他兩個問題，以及任何其他**目標遺漏**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="9c1fc-416">當使用二元分類，例如，使用 hello 標籤**傾斜**和排除 hello 欄位**提示\_類別**，**提示\_量**，和**總\_量**。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="9c1fc-417">hello 後者目標流失，因為它們意指 hello 提示付費。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="9c1fc-418">tooexclude 任何不必要的資料行或目標流失，您可以使用 hello[資料集中選取的資料行][ select-columns]模組或 hello[編輯中繼資料][ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="9c1fc-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="9c1fc-419">如需詳細資訊，請參閱[選取資料集中的資料行][select-columns]和[編輯中繼資料][edit-metadata]參考頁面。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="9c1fc-420"><a name="mldeploy"></a>在 Azure Machine Learning 中部署模型</span><span class="sxs-lookup"><span data-stu-id="9c1fc-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="9c1fc-421">準備您的模型時，可以輕鬆地將它部署為 web 服務，直接從 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="9c1fc-422">如需關於部署 Azure ML Web 服務的詳細資訊，請參閱 [部署 Azure 機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="9c1fc-423">toodeploy 新的 web 服務，您要：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="9c1fc-424">建立計分實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="9c1fc-425">部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-425">Deploy hello web service.</span></span>

<span data-ttu-id="9c1fc-426">從計分實驗的 toocreate**已經完成**定型實驗，按一下**建立計分實驗**hello 較低的動作列中。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Azure 評分][18]

<span data-ttu-id="9c1fc-428">Azure Machine Learning 會嘗試 toocreate hello 定型實驗 hello 元件為基礎的計分實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="9c1fc-429">特別是，它將：</span><span class="sxs-lookup"><span data-stu-id="9c1fc-429">In particular, it will:</span></span>

1. <span data-ttu-id="9c1fc-430">儲存 hello 定型的模型，並移除 hello 模型定型模組。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="9c1fc-431">找出邏輯**輸入連接埠**toorepresent hello 預期輸入的資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="9c1fc-432">找出邏輯**輸出連接埠**toorepresent hello 預期的 web 服務輸出結構描述。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="9c1fc-433">建立 hello 計分實驗時，檢閱它，並進行視需要調整。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="9c1fc-434">因為這些不會使用呼叫 hello 服務時，一般調整是 tooreplace hello 輸入資料集和 （或） 查詢，其中包含一個排除標籤欄位。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="9c1fc-435">它也是很好的作法 tooreduce hello 大小 hello 的輸入資料集和 （或) 查詢 tooa 少數的記錄，剛好足夠 tooindicate hello 輸入結構描述。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="9c1fc-436">Hello 輸出連接埠，它是一般 tooexclude 所有輸入的欄位，只包含 hello**計分標籤**和**計分機率**中輸出使用 hello hello[資料集中選取的資料行] [ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="9c1fc-437">在 hello 圖中有提供範例計分實驗。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="9c1fc-438">一切就緒後 toodeploy，按一下 hello**發佈 WEB 服務**hello 較低的動作列中按鈕。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure ML 發佈][11]

## <a name="summary"></a><span data-ttu-id="9c1fc-440">摘要</span><span class="sxs-lookup"><span data-stu-id="9c1fc-440">Summary</span></span>
<span data-ttu-id="9c1fc-441">toorecap 我們已完成此逐步解說的教學課程中，您已建立的 Azure 資料科學環境中，使用過大的公用資料集，使其透過 hello 小組資料科學程序，從資料擷取 toomodel 定型，所有的 hello 方法，然後在 Azure Machine Learning web 服務的 toohello 部署。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="9c1fc-442">授權資訊</span><span class="sxs-lookup"><span data-stu-id="9c1fc-442">License information</span></span>
<span data-ttu-id="9c1fc-443">此範例逐步解說，以及其隨附的指令碼和 IPython notebook(s) 共用的 Microsoft hello MIT 授權。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="9c1fc-444">請 hello 目錄中的 hello 範例程式碼在 GitHub 上如需詳細資訊，在檢查 hello LICENSE.txt 檔。</span><span class="sxs-lookup"><span data-stu-id="9c1fc-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="9c1fc-445">參考</span><span class="sxs-lookup"><span data-stu-id="9c1fc-445">References</span></span>
<span data-ttu-id="9c1fc-446">•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="9c1fc-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="9c1fc-447">•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="9c1fc-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="9c1fc-448">•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="9c1fc-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
