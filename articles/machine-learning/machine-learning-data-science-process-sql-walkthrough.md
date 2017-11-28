---
title: "aaaBuild 和部署 Azure VM 上使用 SQL Server 的機器學習模型 |Microsoft 文件 '"
description: "進階分析程序和技術實務"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="23745-103">在動作中的 hello 小組資料科學程序： 使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="23745-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="23745-104">在此教學課程中，您逐步進行建置和部署的機器學習模型 hello 程序使用 SQL Server 和公開可用的資料集-hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集。</span><span class="sxs-lookup"><span data-stu-id="23745-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="23745-105">hello 程序會遵循標準資料科學工作流程： 內嵌和瀏覽 hello 資料、 工程功能 toofacilitate 學習 」 中，然後建立及部署模型。</span><span class="sxs-lookup"><span data-stu-id="23745-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="23745-106"><a name="dataset"></a>NYC 計程車車程資料集</span><span class="sxs-lookup"><span data-stu-id="23745-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="23745-107">hello NYC 計程車路線資料約 20 GB 的壓縮的 CSV 檔案 (~ 48 GB 未壓縮)，可包含多個 173 百萬個個別的往返和 hello fares 支付每往返作業。</span><span class="sxs-lookup"><span data-stu-id="23745-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="23745-108">每個往返記錄包括 hello 收取和下車位置和時間、 匿名的 hack (driver) 授權編號和 medallion (計程車的唯一 id) 數目。</span><span class="sxs-lookup"><span data-stu-id="23745-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="23745-109">hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:</span><span class="sxs-lookup"><span data-stu-id="23745-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="23745-110">hello 'trip_data' CSV 包含路線詳細資料，例如乘客、 收取和 dropoff 點數目、 路線持續時間，以及路線長度。</span><span class="sxs-lookup"><span data-stu-id="23745-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="23745-111">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="23745-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="23745-112">hello 'trip_fare' CSV 包含 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="23745-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="23745-113">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="23745-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="23745-114">hello 唯一索引鍵 toojoin 路線\_資料和路線\_價位組成 hello 欄位： medallion 具 「 可回復\_授權與收取\_日期時間。</span><span class="sxs-lookup"><span data-stu-id="23745-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="23745-115"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="23745-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="23745-116">我們會編寫根據 hello 的三個預測問題*提示\_量*，也就是：</span><span class="sxs-lookup"><span data-stu-id="23745-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="23745-117">二元分類：預測是否已支付某趟車程的小費，例如大於美金 $0 元的 *tip\_amount* 為正面範例，而等於美金 $0 元的 *tip\_amount* 為負面範例。</span><span class="sxs-lookup"><span data-stu-id="23745-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="23745-118">多級分類： hello 路線支付 toopredict hello 範圍的提示。</span><span class="sxs-lookup"><span data-stu-id="23745-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="23745-119">我們將 hello*提示\_量*到五個紙匣或類別：</span><span class="sxs-lookup"><span data-stu-id="23745-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="23745-120">迴歸工作： toopredict hello 數量提示支付路線。</span><span class="sxs-lookup"><span data-stu-id="23745-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="23745-121"><a name="setup"></a>正在設定 hello Azure 資料科學環境中執行進階分析</span><span class="sxs-lookup"><span data-stu-id="23745-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="23745-122">您可以看到從 hello[規劃您的環境](machine-learning-data-science-plan-your-environment.md)指南中，有數個選項 toowork 與 Azure 中的 hello NYC 計程車往返資料集：</span><span class="sxs-lookup"><span data-stu-id="23745-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="23745-123">使用 Azure blob 中的 hello 資料然後 Azure Machine Learning 中的模型</span><span class="sxs-lookup"><span data-stu-id="23745-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="23745-124">Hello 資料載入 SQL Server 資料庫，然後在 Azure Machine Learning 中的模型</span><span class="sxs-lookup"><span data-stu-id="23745-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="23745-125">在本教學課程中，我們將示範平行大量匯入的 hello 資料 tooa SQL Server 資料瀏覽、 功能工程和取樣向使用 SQL Server Management Studio，以及使用 IPython 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="23745-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="23745-126">[指令碼範例](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)和 [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) 在 GitHub 中共用。</span><span class="sxs-lookup"><span data-stu-id="23745-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="23745-127">使用 Azure blob 中的 hello 資料的範例 IPython 筆記型電腦 toowork 也會提供 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="23745-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="23745-128">Azure 資料科學環境 tooset:</span><span class="sxs-lookup"><span data-stu-id="23745-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="23745-129">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="23745-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="23745-130">建立 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="23745-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="23745-131">[佈建資料科學虛擬機器](machine-learning-data-science-setup-sql-server-virtual-machine.md)，這樣會提供 SQL Server 和 IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="23745-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23745-132">hello 範例指令碼和 IPython notebook 下載的 tooyour 資料 Science 虛擬機器期間將 hello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="23745-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="23745-133">Hello VM 安裝後指令碼完成時，hello 範例會將 VM 的文件庫中：</span><span class="sxs-lookup"><span data-stu-id="23745-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="23745-134">指令碼範例：`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="23745-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="23745-135">IPython Notebook 範例：`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="23745-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="23745-136">where `<user_name>` 是 VM 的 Windows 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="23745-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="23745-137">我們將 toohello 範例資料夾，做為**範例指令碼**和**範例 IPython Notebook**。</span><span class="sxs-lookup"><span data-stu-id="23745-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="23745-138">根據 hello 資料集的大小、 資料來源位置，以及 hello 選 Azure 目標環境，這種情況下太類似[案例\#5： 在本機檔案中，大型資料集目標 Azure VM 中的 SQL Server](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb)。</span><span class="sxs-lookup"><span data-stu-id="23745-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="23745-139"><a name="getdata"></a>從公用來源取得 hello 資料</span><span class="sxs-lookup"><span data-stu-id="23745-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="23745-140">tooget hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)從公用位置的資料集，您可以使用任何 hello 方法中所述[從 Azure Blob 儲存體移動資料 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 資料 tooyour 新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23745-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="23745-141">使用 AzCopy toocopy hello 資料：</span><span class="sxs-lookup"><span data-stu-id="23745-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="23745-142">登入 tooyour 虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="23745-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="23745-143">建立新的目錄中 hello VM 資料磁碟 (注意： 不要使用 hello hello 當做資料磁碟的 VM 所隨附的暫存磁碟)。</span><span class="sxs-lookup"><span data-stu-id="23745-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="23745-144">在命令提示字元視窗中，執行下列 Azcopy 命令列中，< path_to_data_folder > 取代為您資料的資料夾中 (2) 建立 hello:</span><span class="sxs-lookup"><span data-stu-id="23745-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="23745-145">24 總數 hello AzCopy 完成時，壓縮 CSV 檔案 (12 路線\_資料而 12 路線\_價位) 應該在 hello 資料資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="23745-146">將下載的 hello 檔解壓縮。</span><span class="sxs-lookup"><span data-stu-id="23745-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="23745-147">請注意 hello hello 未壓縮檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="23745-148">這個資料夾將會參考的 tooas hello < 路徑\_至\_資料\_檔案\>。</span><span class="sxs-lookup"><span data-stu-id="23745-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="23745-149"><a name="dbload"></a>將資料大量匯入到 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="23745-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="23745-150">hello 的載入/傳輸大量資料 tooan SQL database 和後續查詢，便可改善效能使用*分割資料表和檢視表*。</span><span class="sxs-lookup"><span data-stu-id="23745-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="23745-151">在本節中，我們會遵循 hello 指示中所述[平行大量匯入使用 SQL 資料分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)toocreate 新資料庫和負載 hello 的資料分割的資料表，以平行方式。</span><span class="sxs-lookup"><span data-stu-id="23745-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="23745-152">登入 tooyour VM，啟動**SQL Server Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="23745-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="23745-153">使用 Windows 驗證進行連接。</span><span class="sxs-lookup"><span data-stu-id="23745-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS 連線][12]
3. <span data-ttu-id="23745-155">如果您有尚未變更 hello SQL Server 驗證模式，並建立新的 SQL 登入使用者，開啟名為 hello 指令碼檔案**變更\_auth.sql**在 hello**範例指令碼**資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="23745-156">變更 hello 預設使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="23745-156">Change hello  default user name and password.</span></span> <span data-ttu-id="23745-157">按一下**！執行**hello 工具列 toorun hello 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="23745-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![執行指令碼][13]
4. <span data-ttu-id="23745-159">確認及/或變更 hello SQL Server 預設資料庫和記錄檔資料夾 tooensure 新建的資料庫，將會儲存在資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="23745-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="23745-160">datawarehousing 負載是適合 hello SQL Server VM 映像已預先設定資料和記錄磁碟使用的。</span><span class="sxs-lookup"><span data-stu-id="23745-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="23745-161">如果您的 VM 未包含資料磁碟，您將新的虛擬硬碟新增 hello VM 安裝程序期間變更 hello 預設資料夾，如下所示：</span><span class="sxs-lookup"><span data-stu-id="23745-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="23745-162">以滑鼠右鍵按一下 hello SQL Server 名稱中左面板，然後按一下的 hello**屬性**。</span><span class="sxs-lookup"><span data-stu-id="23745-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![SQL Server 屬性][14]
   * <span data-ttu-id="23745-164">選取**資料庫設定**從 hello**選取頁面**toohello 左邊的清單。</span><span class="sxs-lookup"><span data-stu-id="23745-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="23745-165">驗證和/或變更 hello**資料庫預設位置**toohello**資料磁碟**您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="23745-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="23745-166">這是如果 hello 預設位置設定以建立新的資料庫所在的位置。</span><span class="sxs-lookup"><span data-stu-id="23745-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![SQL Database 的預設值][15]  
5. <span data-ttu-id="23745-168">toocreate 新的資料庫和一組檔案群組 toohold hello 資料分割的資料表，請開啟 hello 範例指令碼**建立\_db\_default.sql**。</span><span class="sxs-lookup"><span data-stu-id="23745-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="23745-169">hello 指令碼會建立新的資料庫名為**TaxiNYC**和 12 hello 預設資料位置的檔案群組。</span><span class="sxs-lookup"><span data-stu-id="23745-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="23745-170">每個檔案群組都將保留一個月內的 trip\_data 和 trip\_fare 資料。</span><span class="sxs-lookup"><span data-stu-id="23745-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="23745-171">視需要修改 hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="23745-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="23745-172">按一下**！執行**toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="23745-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="23745-173">接下來，建立兩個資料分割資料表，一個用於 hello 路線\_資料，另一個用於 hello 路線\_價位。</span><span class="sxs-lookup"><span data-stu-id="23745-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="23745-174">開啟 hello 範例指令碼**建立\_分割\_table.sql**，這將會：</span><span class="sxs-lookup"><span data-stu-id="23745-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="23745-175">建立資料分割函數 toosplit hello 資料依月份。</span><span class="sxs-lookup"><span data-stu-id="23745-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="23745-176">建立資料分割配置 toomap 每月資料 tooa 不同檔案群組。</span><span class="sxs-lookup"><span data-stu-id="23745-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="23745-177">建立兩個資料分割的資料表對應的 toohello 資料分割配置： **nyctaxi\_路線**會保留 hello 路線\_資料和**nyctaxi\_價位**會保留 hello 路線\_再見資料。</span><span class="sxs-lookup"><span data-stu-id="23745-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="23745-178">按一下**！執行**toorun hello 指令碼，並建立 hello 分割資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="23745-179">在 hello**範例指令碼**資料夾中，有兩個範例 PowerShell 指令碼提供 toodemonstrate 資料 tooSQL 伺服器資料表的平行大量匯入。</span><span class="sxs-lookup"><span data-stu-id="23745-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="23745-180">**bcp\_平行\_generic.ps1**是泛型指令碼 tooparallel 大量匯入資料到資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="23745-181">修改此指令碼 tooset hello 輸入和目標變數 hello 註解行 hello 指令碼中所示。</span><span class="sxs-lookup"><span data-stu-id="23745-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="23745-182">**bcp\_平行\_nyctaxi.ps1** hello 泛型指令碼的預先設定的版本而且可以使用的 tootooload hello NYC 計程車往返資料的兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="23745-183">以滑鼠右鍵按一下 hello **bcp\_平行\_nyctaxi.ps1**指令碼名稱，然後按一下**編輯**tooopen 它在 PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="23745-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="23745-184">檢閱 hello 預設變數及修改相應 tooyour 選取的資料庫名稱、 輸入的資料資料夾中，目標記錄檔資料夾，以及路徑 toohello 範例格式檔案**nyctaxi_trip.xml**和**nyctaxi\_fare.xml** (hello 中提供**範例指令碼**資料夾)。</span><span class="sxs-lookup"><span data-stu-id="23745-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![大量匯入資料][16]
   
    <span data-ttu-id="23745-186">您也可以選取 hello 驗證模式、 預設值是 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="23745-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="23745-187">按一下 hello 工具列 toorun hello 綠色箭號。</span><span class="sxs-lookup"><span data-stu-id="23745-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="23745-188">hello 指令碼將會啟動 24 大量匯入作業在平行 12 的每個資料分割的資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="23745-189">您可能會藉由開啟 hello SQL Server 預設資料夾為上述設定監視 hello 資料匯入進度。</span><span class="sxs-lookup"><span data-stu-id="23745-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="23745-190">hello PowerShell 指令碼報告 hello 開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="23745-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="23745-191">當所有大量匯入完成時，會回報 hello 結束時間。</span><span class="sxs-lookup"><span data-stu-id="23745-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="23745-192">檢查 hello 目標記錄檔資料夾 tooverify hello 大量匯入成功，亦即，hello 目標記錄檔資料夾中報告任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="23745-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="23745-193">您的資料庫已準備好進行探索、功能工程，以及所需的其他作業。</span><span class="sxs-lookup"><span data-stu-id="23745-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="23745-194">因為 hello 資料表已分割，根據 toohello**收取\_datetime**欄位，包括查詢**收取\_datetime**條件 hello **其中**子句將受益於 hello 分割區配置。</span><span class="sxs-lookup"><span data-stu-id="23745-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="23745-195">在**SQL Server Management Studio**，瀏覽 hello 提供範例指令碼**範例\_queries.sql**。</span><span class="sxs-lookup"><span data-stu-id="23745-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="23745-196">toorun hello 範例查詢，反白顯示 hello 的任何查詢線條，然後按一下  **！執行**hello 工具列中。</span><span class="sxs-lookup"><span data-stu-id="23745-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="23745-197">hello NYC 計程車往返資料會載入兩個資料表中。</span><span class="sxs-lookup"><span data-stu-id="23745-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="23745-198">tooimprove 聯結作業，強烈建議 tooindex hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="23745-199">hello 範例指令碼**建立\_分割\_index.sql** hello 複合聯結索引鍵上建立資料分割的索引**medallion 具 「 可回復\_授權及收取\_datetime**。</span><span class="sxs-lookup"><span data-stu-id="23745-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="23745-200"><a name="dbexplore"></a>SQL Server 中的資料探索和功能工程</span><span class="sxs-lookup"><span data-stu-id="23745-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="23745-201">本節中，我們將會執行產生的資料探索和功能，藉由執行 SQL 查詢，直接在 hello **SQL Server Management Studio**先前使用 hello SQL Server 資料庫建立。</span><span class="sxs-lookup"><span data-stu-id="23745-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="23745-202">範例指令碼名為**範例\_queries.sql**所提供的 hello**範例指令碼**資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="23745-203">修改 hello 指令碼 toochange hello 資料庫名稱，如果 hello 預設值不同： **TaxiNYC**。</span><span class="sxs-lookup"><span data-stu-id="23745-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="23745-204">在這個練習中，我們將：</span><span class="sxs-lookup"><span data-stu-id="23745-204">In this exercise, we will:</span></span>

* <span data-ttu-id="23745-205">連接太**SQL Server Management Studio**使用 Windows 驗證，或使用 SQL 驗證，而且 hello SQL 登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="23745-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="23745-206">在變動的時間範圍中探索數個欄位的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="23745-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="23745-207">調查 hello 經度和緯度欄位的資料品質。</span><span class="sxs-lookup"><span data-stu-id="23745-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="23745-208">產生二進位和多級分類標籤根據 hello**提示\_量**。</span><span class="sxs-lookup"><span data-stu-id="23745-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="23745-209">產生功能，並計算或比較車程距離。</span><span class="sxs-lookup"><span data-stu-id="23745-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="23745-210">聯結 hello 兩個資料表，和擷取將會使用的 toobuild 模型的隨機取樣。</span><span class="sxs-lookup"><span data-stu-id="23745-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="23745-211">當您準備好 tooproceed tooAzure 機器學習服務，您可以：</span><span class="sxs-lookup"><span data-stu-id="23745-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="23745-212">儲存 hello 最終 SQL 查詢 tooextract 和範例 hello 資料和複製-貼上 hello 查詢直接[匯入資料][ import-data]模組在 Azure Machine Learning 中，或</span><span class="sxs-lookup"><span data-stu-id="23745-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="23745-213">保存取樣的 hello 與工程的資料您計劃 toouse 模型建立新的資料庫中的資料表，並在 hello 使用 hello 新資料表[匯入資料][ import-data] Azure Machine Learning 中的模組。</span><span class="sxs-lookup"><span data-stu-id="23745-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="23745-214">本節中，我們將儲存 hello 最終查詢 tooextract 和範例 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="23745-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="23745-215">hello 第二個方法所示 hello[資料探索和 IPython 筆記型電腦功能工程](#ipnb)> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="23745-216">Hello 數目資料列和資料行中 hello 快速驗證資料表填入先前使用平行大量匯入，</span><span class="sxs-lookup"><span data-stu-id="23745-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="23745-217">探索：依據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="23745-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="23745-218">這個範例會在給定的時間間隔內識別超過 100 個往返 hello medallion （計程車數字）。</span><span class="sxs-lookup"><span data-stu-id="23745-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="23745-219">hello 查詢獲益 hello 分割資料表的存取因為它由 hello 分割區配置所**收取\_datetime**。</span><span class="sxs-lookup"><span data-stu-id="23745-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="23745-220">查詢 hello 完整資料集也會進行 hello 資料分割資料表的使用及/或索引掃描。</span><span class="sxs-lookup"><span data-stu-id="23745-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="23745-221">探索：依據 medallion 和 hack_license 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="23745-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="23745-222">資料品質評估：驗證含有不正確經度和/或緯度的記錄</span><span class="sxs-lookup"><span data-stu-id="23745-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="23745-223">此範例中，以調查如果任一個 hello 經度和/或緯度的欄位可能包含無效的值 （弧度角度應該介於-90 到 90 之間），或具有 （0，0） 座標。</span><span class="sxs-lookup"><span data-stu-id="23745-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="23745-224">探索：已支付小費和未支付小費的車程分佈</span><span class="sxs-lookup"><span data-stu-id="23745-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="23745-225">此範例會尋找已與不傾斜中指定的時間週期 （或在 hello 完整資料集，如果涵蓋 hello 完整的年份） 傾斜的往返的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="23745-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="23745-226">此分佈會反映 hello 二進位標籤發佈 toobe 稍後用於二元分類模型。</span><span class="sxs-lookup"><span data-stu-id="23745-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="23745-227">探索：小費類別/範圍分佈</span><span class="sxs-lookup"><span data-stu-id="23745-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="23745-228">此範例會計算 hello 布提示範圍中指定的時間週期 （或在 hello 完整資料集，如果涵蓋 hello 完整年）。</span><span class="sxs-lookup"><span data-stu-id="23745-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="23745-229">這是 hello 發佈的 hello 標籤類別會用於多級分類模型的更新版本。</span><span class="sxs-lookup"><span data-stu-id="23745-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="23745-230">探索：計算並比較車程距離</span><span class="sxs-lookup"><span data-stu-id="23745-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="23745-231">這個範例會將轉換 hello 收取和下車經度和緯度 tooSQL geography 點、 計算 hello 旅行距離使用 SQL geography 點差異，並傳回隨機取樣的 hello 比較結果。</span><span class="sxs-lookup"><span data-stu-id="23745-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="23745-232">hello 範例限制 hello toovalid 協調只能使用稍早討論的 hello 資料品質評估查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="23745-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="23745-233">SQL 查詢中的功能工程</span><span class="sxs-lookup"><span data-stu-id="23745-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="23745-234">hello 標籤的產生和地理位置轉換瀏覽查詢也可以使用的 toogenerate 標籤/功能藉由移除 hello 計算組件。</span><span class="sxs-lookup"><span data-stu-id="23745-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="23745-235">Hello 會提供額外的功能工程 SQL 範例[資料探索和 IPython 筆記型電腦功能工程](#ipnb)> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="23745-236">它是更有效率 toorun hello 功能產生的查詢上 hello 完整資料集或大型子集使用直接在 hello SQL Server 資料庫執行個體執行的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="23745-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="23745-237">在中，可能會執行 hello 查詢**SQL Server Management Studio**，IPython 筆記型電腦或任何開發工具/環境可以存取 hello 資料庫在本機或遠端。</span><span class="sxs-lookup"><span data-stu-id="23745-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="23745-238">準備資料以進行模型建置</span><span class="sxs-lookup"><span data-stu-id="23745-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="23745-239">hello 下列查詢會聯結 hello **nyctaxi\_路線**和**nyctaxi\_價位**資料表時，會產生二進位分類標籤**傾斜**、多級分類標籤**提示\_類別**，然後從 hello 完整聯結的資料集擷取 %1 的隨機取樣。</span><span class="sxs-lookup"><span data-stu-id="23745-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="23745-240">此查詢可以複製，然後直接在 hello 貼入[Azure Machine Learning Studio](https://studio.azureml.net) [匯入資料][ import-data]從 hello SQL Server 資料庫的直接資料擷取的模組在 Azure 中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23745-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="23745-241">hello 查詢排除具有不正確的記錄 （0，0） 座標。</span><span class="sxs-lookup"><span data-stu-id="23745-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="23745-242"><a name="ipnb"></a>IPython Notebook 中的資料探索和功能工程</span><span class="sxs-lookup"><span data-stu-id="23745-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="23745-243">在本節中，我們將會執行資料瀏覽功能使用和產生 hello 稍早建立的 SQL Server 資料庫的 Python 和 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="23745-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="23745-244">名為範例 IPython 筆記型電腦**machine-Learning-data-science-process-sql-story.ipynb**所提供的 hello**範例 IPython Notebook**資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="23745-245">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)也提供此 Notebook。</span><span class="sxs-lookup"><span data-stu-id="23745-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="23745-246">hello 巨量資料使用時，建議順序為 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="23745-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="23745-247">在 hello 資料的小型範例讀入記憶體中的資料框架。</span><span class="sxs-lookup"><span data-stu-id="23745-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="23745-248">執行一些視覺效果，並使用瀏覽 hello 取樣的資料。</span><span class="sxs-lookup"><span data-stu-id="23745-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="23745-249">實驗功能使用 hello 取樣資料的工程團隊。</span><span class="sxs-lookup"><span data-stu-id="23745-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="23745-250">針對較大的資料瀏覽、 資料操作與特徵設計會使用 Python tooissue SQL 查詢，直接對 hello SQL Server 資料庫 hello Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="23745-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="23745-251">決定 hello 範例大小 toouse Azure 機器學習模型建立的。</span><span class="sxs-lookup"><span data-stu-id="23745-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="23745-252">一切就緒後 tooproceed tooAzure 機器學習服務，您也可以：</span><span class="sxs-lookup"><span data-stu-id="23745-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="23745-253">儲存 hello 最終 SQL 查詢 tooextract 和範例 hello 資料和複製-貼上 hello 查詢直接[匯入資料][ import-data] Azure Machine Learning 中的模組。</span><span class="sxs-lookup"><span data-stu-id="23745-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="23745-254">這個方法會示範 hello [Azure Machine Learning 中建立模型](#mlmodel)> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="23745-255">保存取樣的 hello 與工程的資料您計劃 toouse 模型建置在新的資料庫資料表，然後用 hello hello 新資料表[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="23745-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="23745-256">hello 以下是幾個資料探索、 資料視覺效果和工程範例的功能。</span><span class="sxs-lookup"><span data-stu-id="23745-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="23745-257">如需其他範例，請參閱 hello 範例 SQL IPython 筆記型電腦在 hello**範例 IPython Notebook**資料夾。</span><span class="sxs-lookup"><span data-stu-id="23745-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="23745-258">初始化資料庫認證</span><span class="sxs-lookup"><span data-stu-id="23745-258">Initialize Database Credentials</span></span>
<span data-ttu-id="23745-259">初始化 hello 下列變數中的資料庫連線設定：</span><span class="sxs-lookup"><span data-stu-id="23745-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="23745-260">建立資料庫連接</span><span class="sxs-lookup"><span data-stu-id="23745-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="23745-261">報告資料表 nyctaxi_trip 中資料列和資料行的數目</span><span class="sxs-lookup"><span data-stu-id="23745-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="23745-262">資料列總數 = 173179759</span><span class="sxs-lookup"><span data-stu-id="23745-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="23745-263">資料行總數 = 14</span><span class="sxs-lookup"><span data-stu-id="23745-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="23745-264">讀取在小型資料中的範例 hello 的 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="23745-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="23745-265">時間 tooread hello 範例資料表為 6.492000 秒</span><span class="sxs-lookup"><span data-stu-id="23745-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="23745-266">擷取的資料列和資料行數目 = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="23745-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="23745-267">描述性統計資料</span><span class="sxs-lookup"><span data-stu-id="23745-267">Descriptive Statistics</span></span>
<span data-ttu-id="23745-268">現在已準備好 tooexplore hello 取樣資料。</span><span class="sxs-lookup"><span data-stu-id="23745-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="23745-269">我們開始查看 hello 的描述性統計資料**路線\_距離**（或任何其他） 個欄位：</span><span class="sxs-lookup"><span data-stu-id="23745-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="23745-270">視覺效果：盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="23745-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="23745-271">下一步，我們會審視 hello 盒狀圖 hello 旅行距離 toovisualize hello 分位數</span><span class="sxs-lookup"><span data-stu-id="23745-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![圖 #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="23745-273">視覺效果：分佈的盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="23745-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![圖 #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="23745-275">視覺效果：橫條和折線圖</span><span class="sxs-lookup"><span data-stu-id="23745-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="23745-276">在此範例中，我們可以分類收納成五個分類收納 hello 旅行距離和視覺化 hello 分類收納的結果。</span><span class="sxs-lookup"><span data-stu-id="23745-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="23745-277">我們可以繪製 hello 上方列中的分類收納發佈或線條，如下所示的繪圖</span><span class="sxs-lookup"><span data-stu-id="23745-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![圖 #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![圖 #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="23745-280">視覺效果：散佈圖範例</span><span class="sxs-lookup"><span data-stu-id="23745-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="23745-281">我們顯示散佈圖之間**路線\_時間\_中\_秒**和**路線\_距離**toosee 如果有任何相互關聯</span><span class="sxs-lookup"><span data-stu-id="23745-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![圖 #6][6]

<span data-ttu-id="23745-283">同樣地，我們可以檢查 hello 之間的關聯性**速率\_程式碼**和**路線\_距離**。</span><span class="sxs-lookup"><span data-stu-id="23745-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![圖 #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="23745-285">子取樣 hello SQL 中的資料</span><span class="sxs-lookup"><span data-stu-id="23745-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="23745-286">當您準備資料模型中建置[Azure Machine Learning Studio](https://studio.azureml.net)，您可能決定在 hello**直接在 hello 資料匯入模組中的 SQL 查詢 toouse**或保存 hello 工程和取樣在新的資料表，您可以使用在 hello 資料[匯入資料][ import-data]模組使用簡單**選取 * FROM < 您\_新\_資料表\_名稱 >**。</span><span class="sxs-lookup"><span data-stu-id="23745-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="23745-287">本節會建立新的資料表 toohold hello 取樣工程和資料。</span><span class="sxs-lookup"><span data-stu-id="23745-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="23745-288">直接 SQL 查詢的模型建立的範例中 hello[資料探索和 SQL Server 功能工程](#dbexplore)> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="23745-289">建立範例資料表與填入有 1%的 hello 聯結資料表。</span><span class="sxs-lookup"><span data-stu-id="23745-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="23745-290">如果資料表存在，請先卸除它。</span><span class="sxs-lookup"><span data-stu-id="23745-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="23745-291">在本節中，我們加入 hello 資料表**nyctaxi\_路線**和**nyctaxi\_價位**、 擷取 1%隨機取樣，並在新的資料表名稱中的 hello 取樣資料保存在**nyctaxi\_一個\_百分比**:</span><span class="sxs-lookup"><span data-stu-id="23745-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="23745-292">在 IPython Notebook 中使用 SQL 查詢進行資料探索</span><span class="sxs-lookup"><span data-stu-id="23745-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="23745-293">在本節中，我們會探討使用保存 hello 前面所建立的新資料表中的 hello 1%的取樣資料的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="23745-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="23745-294">請注意，可以使用 hello 原始資料表，您可以選擇使用執行類似的瀏覽**TABLESAMPLE** toolimit hello 瀏覽範例，或是藉由限制 hello 結果指定時間內使用 hello tooa**收取\_datetime**分割，如所述 hello[資料探索和 SQL Server 功能工程](#dbexplore)> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="23745-295">探索：車程的每日分佈</span><span class="sxs-lookup"><span data-stu-id="23745-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="23745-296">探索：根據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="23745-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="23745-297">在 IPython Notebook 中使用 SQL 查詢進行的功能工程</span><span class="sxs-lookup"><span data-stu-id="23745-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="23745-298">這一節中，我們將產生的新標籤，並直接使用 SQL 查詢的功能，hello 1%範例資料表上運作我們建立 hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="23745-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="23745-299">標籤產生：產生類別標籤</span><span class="sxs-lookup"><span data-stu-id="23745-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="23745-300">在下列範例的 hello，我們會產生兩組標籤 toouse 用於模型化：</span><span class="sxs-lookup"><span data-stu-id="23745-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="23745-301">二進位類別標籤 **tipped** (預測是否將給予小費)</span><span class="sxs-lookup"><span data-stu-id="23745-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="23745-302">多級標籤**提示\_類別**（預測 hello 提示 bin 或範圍）</span><span class="sxs-lookup"><span data-stu-id="23745-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="23745-303">功能工程：適用於類別資料行的計數功能</span><span class="sxs-lookup"><span data-stu-id="23745-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="23745-304">這個範例將 hello 計數的 hello 資料中其項目取代成每個類別目錄轉換成數值欄位的類別目錄欄位。</span><span class="sxs-lookup"><span data-stu-id="23745-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="23745-305">功能工程：適用於數字資料行的收納組功能</span><span class="sxs-lookup"><span data-stu-id="23745-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="23745-306">此範例會將連續的數值欄位轉換成預設的類別範圍，亦即，將數值欄位轉換到類別欄位。</span><span class="sxs-lookup"><span data-stu-id="23745-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="23745-307">功能工程：從十進位經緯度擷取位置功能</span><span class="sxs-lookup"><span data-stu-id="23745-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="23745-308">此範例中分成 hello 緯度和/或經度欄位的十進位表示法多個地區欄位的不同資料粒度，例如，國家/地區、 縣 （市）、 城鎮、 區塊和其他內容。請注意，hello 新地理欄位不對應 tooactual 位置。</span><span class="sxs-lookup"><span data-stu-id="23745-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="23745-309">如需對應地理編碼位置的資訊，請參閱 [Bing 地圖服務 REST 服務](https://msdn.microsoft.com/library/ff701710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="23745-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="23745-310">確認 hello 最終格式的 hello 特徵化資料表</span><span class="sxs-lookup"><span data-stu-id="23745-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="23745-311">現在，我們已準備好 tooproceed toomodel 建置和中的模型部署[Azure Machine Learning](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="23745-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="23745-312">hello 資料已準備好 hello 預測問題，也就是先前定義的任何項目：</span><span class="sxs-lookup"><span data-stu-id="23745-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="23745-313">二元分類： toopredict 提示是否支付路線。</span><span class="sxs-lookup"><span data-stu-id="23745-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="23745-314">多級分類： toopredict hello 範圍的提示，根據 toohello 先前定義的類別。</span><span class="sxs-lookup"><span data-stu-id="23745-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="23745-315">迴歸工作： toopredict hello 數量提示支付路線。</span><span class="sxs-lookup"><span data-stu-id="23745-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="23745-316"><a name="mlmodel"></a>在 Azure Machine Learning 中建置模型</span><span class="sxs-lookup"><span data-stu-id="23745-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="23745-317">toobegin hello 模型練習，請在 tooyour Azure Machine Learning 工作區中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="23745-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="23745-318">如果您尚未建立機器學習服務工作區，請參閱 [建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="23745-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="23745-319">tooget 開始使用 Azure Machine Learning 中，請參閱[什麼是 Azure Machine Learning Studio？](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="23745-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="23745-320">登入太[Azure Machine Learning Studio](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="23745-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="23745-321">hello Studio 首頁上提供豐富的資訊、 視訊、 教學課程中，連結 toohello 模組參考和其他資源。</span><span class="sxs-lookup"><span data-stu-id="23745-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="23745-322">如需有關 Azure Machine Learning 的詳細資訊，請參閱 hello [Azure 機器學習服務文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="23745-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="23745-323">典型的訓練實驗組成 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="23745-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="23745-324">建立 **+NEW** 實驗。</span><span class="sxs-lookup"><span data-stu-id="23745-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="23745-325">收到 hello 資料 tooAzure 機器學習。</span><span class="sxs-lookup"><span data-stu-id="23745-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="23745-326">前置處理、 轉換和視需要處理 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="23745-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="23745-327">視需要產生功能。</span><span class="sxs-lookup"><span data-stu-id="23745-327">Generate features as needed.</span></span>
5. <span data-ttu-id="23745-328">Hello 資料分割為訓練/驗證/測試資料集 (或有個別的資料集的每個)。</span><span class="sxs-lookup"><span data-stu-id="23745-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="23745-329">選取一或多個機器學習演算法根據學習問題 toosolve hello。</span><span class="sxs-lookup"><span data-stu-id="23745-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="23745-330">例如，二進位分類、多類別分類、迴歸。</span><span class="sxs-lookup"><span data-stu-id="23745-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="23745-331">培訓使用 hello 定型資料集的一或多個模型。</span><span class="sxs-lookup"><span data-stu-id="23745-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="23745-332">得分 hello 驗證資料集使用 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="23745-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="23745-333">評估 hello 模型 toocompute hello 相關的度量 hello 學習問題。</span><span class="sxs-lookup"><span data-stu-id="23745-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="23745-334">微調 hello 模型和選取 hello 最佳模型 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="23745-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="23745-335">在此練習中，我們已經瀏覽和工程 hello 的 SQL Server 資料，並決定在 Azure Machine Learning 中的 hello 範例大小 tooingest 上。</span><span class="sxs-lookup"><span data-stu-id="23745-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="23745-336">我們決定 toobuild 一或多個 hello 預測模型：</span><span class="sxs-lookup"><span data-stu-id="23745-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="23745-337">取得 hello 資料 tooAzure Machine Learning 使用 hello[匯入資料][ import-data]模組，用於 hello**資料輸入和輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="23745-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="23745-338">如需詳細資訊，請參閱 hello[匯入資料][ import-data]模組參考頁面。</span><span class="sxs-lookup"><span data-stu-id="23745-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Azure Machine Learning 匯入資料][17]
2. <span data-ttu-id="23745-340">選取**Azure SQL Database**為 hello**資料來源**在 hello**屬性**面板。</span><span class="sxs-lookup"><span data-stu-id="23745-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="23745-341">輸入 hello 資料庫 DNS 名稱在 hello**資料庫伺服器名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="23745-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="23745-342">格式： `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="23745-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="23745-343">輸入 hello**資料庫名稱**hello 對應欄位中。</span><span class="sxs-lookup"><span data-stu-id="23745-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="23745-344">輸入 hello **SQL 使用者名稱**hello 中 * * 伺服器使用者 aqccount 名稱和密碼 hello hello**伺服器使用者帳戶密碼**。</span><span class="sxs-lookup"><span data-stu-id="23745-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="23745-345">選取 [ **接受任何伺服器憑證** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="23745-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="23745-346">在 hello**資料庫查詢**編輯文字區域中，貼上 hello 查詢 hello 必要資料庫欄位 （包括任何計算的欄位，例如 hello 標籤） 和向下會擷取範例 hello 資料所需的 toohello 取樣大小。</span><span class="sxs-lookup"><span data-stu-id="23745-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="23745-347">二元分類實驗 hello SQL Server 資料庫中直接讀取資料的範例是在 hello 圖中。</span><span class="sxs-lookup"><span data-stu-id="23745-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="23745-348">您可以針對多類別分類和迴歸問題建構類似的實驗。</span><span class="sxs-lookup"><span data-stu-id="23745-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning 訓練][10]

> [!IMPORTANT]
> <span data-ttu-id="23745-350">在 hello 模型化資料擷取和取樣的查詢範例提供上一節， **hello 三個模型練習的所有標籤都包含在 hello 查詢**。</span><span class="sxs-lookup"><span data-stu-id="23745-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="23745-351">（必要） 的重要步驟，在每個模型化練習 hello 太**排除**hello hello 不必要的標籤，其他兩個問題，以及任何其他**目標遺漏**。</span><span class="sxs-lookup"><span data-stu-id="23745-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="23745-352">例如，當使用二元分類，用於 hello 標籤**傾斜**和排除 hello 欄位**提示\_類別**，**提示\_量**，和**總\_量**。</span><span class="sxs-lookup"><span data-stu-id="23745-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="23745-353">hello 後者目標流失，因為它們意指 hello 提示付費。</span><span class="sxs-lookup"><span data-stu-id="23745-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="23745-354">tooexclude 不必要的資料行及 （或） 目標流失，您可以使用 hello[資料集中選取的資料行][ select-columns]模組或 hello[編輯中繼資料][ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="23745-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="23745-355">如需詳細資訊，請參閱[選取資料集中的資料行][select-columns]和[編輯中繼資料][edit-metadata]參考頁面。</span><span class="sxs-lookup"><span data-stu-id="23745-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="23745-356"><a name="mldeploy"></a>在 Azure Machine Learning 中部署模型</span><span class="sxs-lookup"><span data-stu-id="23745-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="23745-357">準備您的模型時，可以輕鬆地將它部署為 web 服務，直接從 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="23745-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="23745-358">如需關於部署 Azure Machine Learning Web 服務的詳細資訊，請參閱 [部署 Azure 機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="23745-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="23745-359">toodeploy 新的 web 服務，您要：</span><span class="sxs-lookup"><span data-stu-id="23745-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="23745-360">建立計分實驗。</span><span class="sxs-lookup"><span data-stu-id="23745-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="23745-361">部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="23745-361">Deploy hello web service.</span></span>

<span data-ttu-id="23745-362">從計分實驗的 toocreate**已經完成**定型實驗，按一下**建立計分實驗**hello 較低的動作列中。</span><span class="sxs-lookup"><span data-stu-id="23745-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Azure 評分][18]

<span data-ttu-id="23745-364">Azure Machine Learning 會嘗試 toocreate hello 定型實驗 hello 元件為基礎的計分實驗。</span><span class="sxs-lookup"><span data-stu-id="23745-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="23745-365">特別是，它將：</span><span class="sxs-lookup"><span data-stu-id="23745-365">In particular, it will:</span></span>

1. <span data-ttu-id="23745-366">儲存 hello 定型的模型，並移除 hello 模型定型模組。</span><span class="sxs-lookup"><span data-stu-id="23745-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="23745-367">找出邏輯**輸入連接埠**toorepresent hello 預期輸入的資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="23745-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="23745-368">找出邏輯**輸出連接埠**toorepresent hello 預期的 web 服務輸出結構描述。</span><span class="sxs-lookup"><span data-stu-id="23745-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="23745-369">建立 hello 計分實驗時，檢閱它，並視需要調整。</span><span class="sxs-lookup"><span data-stu-id="23745-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="23745-370">因為這些不會使用呼叫 hello 服務時，一般調整是 tooreplace hello 輸入資料集和 （或） 查詢，其中包含一個排除標籤欄位。</span><span class="sxs-lookup"><span data-stu-id="23745-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="23745-371">它也是很好的作法 tooreduce hello 大小 hello 的輸入資料集和 （或) 查詢 tooa 少數的記錄，剛好足夠 tooindicate hello 輸入結構描述。</span><span class="sxs-lookup"><span data-stu-id="23745-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="23745-372">Hello 輸出連接埠，它是一般 tooexclude 所有輸入的欄位，只包含 hello**計分標籤**和**計分機率**中輸出使用 hello hello[資料集中選取的資料行] [ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="23745-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="23745-373">計分實驗範例是在 hello 圖中。</span><span class="sxs-lookup"><span data-stu-id="23745-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="23745-374">一切就緒後 toodeploy，按一下 hello**發佈 WEB 服務**hello 較低的動作列中按鈕。</span><span class="sxs-lookup"><span data-stu-id="23745-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure Machine Learning 發佈][11]

<span data-ttu-id="23745-376">toorecap，本逐步解說教學課程中，您已建立的 Azure 資料科學環境中，使用過大的公用資料集從資料擷取 toomodel 定型集和部署在 Azure Machine Learning web 服務的所有 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="23745-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="23745-377">授權資訊</span><span class="sxs-lookup"><span data-stu-id="23745-377">License Information</span></span>
<span data-ttu-id="23745-378">此範例逐步解說，以及其隨附的指令碼和 IPython notebook(s) 共用的 Microsoft hello MIT 授權。</span><span class="sxs-lookup"><span data-stu-id="23745-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="23745-379">請 hello 目錄中的 hello 範例程式碼在 GitHub 上如需詳細資訊，在檢查 hello LICENSE.txt 檔。</span><span class="sxs-lookup"><span data-stu-id="23745-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="23745-380">參考</span><span class="sxs-lookup"><span data-stu-id="23745-380">References</span></span>
<span data-ttu-id="23745-381">•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="23745-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="23745-382">•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="23745-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="23745-383">•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="23745-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
