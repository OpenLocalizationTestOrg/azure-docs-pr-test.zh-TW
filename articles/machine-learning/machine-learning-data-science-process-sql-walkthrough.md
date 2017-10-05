---
title: "使用 Azure VM 上的 SQL Server 建置與部署機器學習模型 | Microsoft Docs"
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
ms.openlocfilehash: 6c5361c7e47209c8eb4d5630b44b3dcfeedeaf01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="18517-103">Team Data Science Process 實務：使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="18517-103">The Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="18517-104">在這個教學課程中，您將遵循逐步解說，使用 SQL Server 和可公開取得的資料集 ([NYC Taxi Trips (NYC 計程車車程)](http://www.andresmh.com/nyctaxitrips/) 資料集)，完成建置和部署機器學習服務模型的程序。</span><span class="sxs-lookup"><span data-stu-id="18517-104">In this tutorial, you walk through the process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="18517-105">程序會遵循標準的資料科學工作流程︰包括擷取和瀏覽資料，以及設計功能以加快學習，接著建置和部署模型。</span><span class="sxs-lookup"><span data-stu-id="18517-105">The procedure follows a standard data science workflow: ingest and explore the data, engineer features to facilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="18517-106"><a name="dataset"></a>NYC 計程車車程資料集</span><span class="sxs-lookup"><span data-stu-id="18517-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="18517-107">「NYC 計程車車程」資料大約是 20GB 的 CSV 壓縮檔 (未壓縮時可達 48GB)，其中包含超過 1 億 7300 萬筆個別車程及針對每趟車程支付的費用。</span><span class="sxs-lookup"><span data-stu-id="18517-107">The NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="18517-108">每趟車程記錄包括上車和下車的位置與時間、匿名的計程車司機駕照號碼，以及圓形徽章 (計程車的唯一識別碼) 號碼。</span><span class="sxs-lookup"><span data-stu-id="18517-108">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="18517-109">資料涵蓋 2013 年的所有車程，並且每月會在下列兩個資料集中加以提供：</span><span class="sxs-lookup"><span data-stu-id="18517-109">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="18517-110">「trip_data」CSV 檔案包含車程的詳細資訊，例如，乘客數、上車和下車地點、車程持續時間，以及車程長度。</span><span class="sxs-lookup"><span data-stu-id="18517-110">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="18517-111">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="18517-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="18517-112">「trip_fare」CSV 檔案包含針對每趟車程所支付之費用的詳細資訊，例如付款類型、費用金額、銷售稅和稅金、小費和服務費，以及支付的總金額。</span><span class="sxs-lookup"><span data-stu-id="18517-112">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="18517-113">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="18517-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="18517-114">聯結 trip\_data 和 trip\_fare 的唯一索引鍵是由下列欄位組成：medallion、hack\_licence、pickup\_datetime。</span><span class="sxs-lookup"><span data-stu-id="18517-114">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="18517-115"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="18517-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="18517-116">我們將根據 *tip\_amount* 編寫三個預測問題的公式，公式如下：</span><span class="sxs-lookup"><span data-stu-id="18517-116">We will formulate three prediction problems based on the *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="18517-117">二元分類：預測是否已支付某趟車程的小費，例如大於美金 $0 元的 *tip\_amount* 為正面範例，而等於美金 $0 元的 *tip\_amount* 為負面範例。</span><span class="sxs-lookup"><span data-stu-id="18517-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="18517-118">多類別分類：預測已針對該車程支付的小費的金額範圍。</span><span class="sxs-lookup"><span data-stu-id="18517-118">Multiclass classification: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="18517-119">我們將 tip\_amount 分成五個分類收納組或類別：</span><span class="sxs-lookup"><span data-stu-id="18517-119">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="18517-120">迴歸工作：預測已針對某趟車程支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="18517-120">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="18517-121"><a name="setup"></a>設定適用於進階分析的 Azure 資料科學環境</span><span class="sxs-lookup"><span data-stu-id="18517-121"><a name="setup"></a>Setting Up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="18517-122">誠如您在《 [規劃您的環境](machine-learning-data-science-plan-your-environment.md) 》指南中所見，在 Azure 中使用「NYC 計程車車程」資料集時，有數個選項可以採用：</span><span class="sxs-lookup"><span data-stu-id="18517-122">As you can see from the [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options to work with the NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="18517-123">使用 Azure Blob 中的資料，然後在 Azure Machine Learning 中模型化</span><span class="sxs-lookup"><span data-stu-id="18517-123">Work with the data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="18517-124">將資料載入 SQL Server 資料庫，然後在 Azure Machine Learning 中模型化</span><span class="sxs-lookup"><span data-stu-id="18517-124">Load the data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="18517-125">在此教學課程中，我們會示範將資料平行大量匯入 SQL Server、資料探索、功能工程，以及使用 SQL Server Management Studio 及使用 IPython Notebook 進行向下取樣。</span><span class="sxs-lookup"><span data-stu-id="18517-125">In this tutorial we will demonstrate parallel bulk import of the data to a SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="18517-126">[指令碼範例](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)和 [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) 在 GitHub 中共用。</span><span class="sxs-lookup"><span data-stu-id="18517-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="18517-127">使用 Azure Blob 中資料的 IPython Notebook 範例也可以在相同位置中取得。</span><span class="sxs-lookup"><span data-stu-id="18517-127">A sample IPython notebook to work with the data in Azure blobs is also available in the same location.</span></span>

<span data-ttu-id="18517-128">設定您的 Azure 資料科學環境：</span><span class="sxs-lookup"><span data-stu-id="18517-128">To set up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="18517-129">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="18517-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="18517-130">建立 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="18517-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="18517-131">[佈建資料科學虛擬機器](machine-learning-data-science-setup-sql-server-virtual-machine.md)，這樣會提供 SQL Server 和 IPython Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="18517-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="18517-132">指令碼範例和 IPython Notebook 將在安裝過程中下載到您的資料科學虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="18517-132">The sample scripts and IPython notebooks will be downloaded to your Data Science virtual machine during the setup process.</span></span> <span data-ttu-id="18517-133">當 VM 後續安裝指令碼完成之後，範例將位於您的 VM 文件庫上。</span><span class="sxs-lookup"><span data-stu-id="18517-133">When the VM post-installation script completes, the samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="18517-134">指令碼範例：`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="18517-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="18517-135">IPython Notebook 範例：`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="18517-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="18517-136">where `<user_name>` 是 VM 的 Windows 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="18517-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="18517-137">我們會將範例資料夾稱為「指令碼範例」和「IPython Notebook 範例」。</span><span class="sxs-lookup"><span data-stu-id="18517-137">We will refer to the sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="18517-138">根據資料集大小、資料來源位置，以及選取的 Azure 目標環境，此案例的類似案例為[案例 \#5：本機檔案中的大型資料集、Azure VM 中的目標 SQL Server](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb)。</span><span class="sxs-lookup"><span data-stu-id="18517-138">Based on the dataset size, data source location, and the selected Azure target environment, this scenario is similar to [Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="18517-139"><a name="getdata"></a>從公用來源取得資料</span><span class="sxs-lookup"><span data-stu-id="18517-139"><a name="getdata"></a>Get the Data from Public Source</span></span>
<span data-ttu-id="18517-140">若要從 [NYC 計程車車程](http://www.andresmh.com/nyctaxitrips/)資料集的公用位置取得該資料集，您可以使用[從 Azure Blob 儲存體來回移動資料](machine-learning-data-science-move-azure-blob.md)中所述的任何一種方法，將資料複製到新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="18517-140">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your new virtual machine.</span></span>

<span data-ttu-id="18517-141">使用 AzCopy 複製資料：</span><span class="sxs-lookup"><span data-stu-id="18517-141">To copy the data using AzCopy:</span></span>

1. <span data-ttu-id="18517-142">登入您的虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="18517-142">Log in to your virtual machine (VM)</span></span>
2. <span data-ttu-id="18517-143">在 VM 的資料磁碟中建立新的目錄 (注意：請勿使用 VM 隨附的「暫存磁碟」做為資料磁碟)。</span><span class="sxs-lookup"><span data-stu-id="18517-143">Create a new directory in the VM's data disk (Note: Do not use the Temporary Disk which comes with the VM as a Data Disk).</span></span>
3. <span data-ttu-id="18517-144">在 [命令提示字元] 視窗中，執行下列 AzCopy 命令列，使用您在 (2) 中建立的 [資料] 資料夾來取代 <path_to_data_folder>：</span><span class="sxs-lookup"><span data-stu-id="18517-144">In a Command Prompt window, run the following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="18517-145">當 AzCopy 完成時，資料的資料夾中總共應該有 24 壓縮的 CSV 檔案 (12 個檔案是 trip\_data，12 個檔案是 trip\_fare)。</span><span class="sxs-lookup"><span data-stu-id="18517-145">When the AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in the data folder.</span></span>
4. <span data-ttu-id="18517-146">將下載的檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="18517-146">Unzip the downloaded files.</span></span> <span data-ttu-id="18517-147">請注意未壓縮檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="18517-147">Note the folder where the uncompressed files reside.</span></span> <span data-ttu-id="18517-148">此資料夾將稱為 <path\_to\_data\_files\>。</span><span class="sxs-lookup"><span data-stu-id="18517-148">This folder will be referred to as the <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="18517-149"><a name="dbload"></a>將資料大量匯入到 SQL Server 資料庫</span><span class="sxs-lookup"><span data-stu-id="18517-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="18517-150">使用「資料分割資料表和檢視」，就可以改善載入/傳輸大量資料至 SQL 資料庫和後續查詢的效能。</span><span class="sxs-lookup"><span data-stu-id="18517-150">The performance of loading/transferring large amounts of data to an SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="18517-151">在本節中，我們將遵循「 [使用 SQL 資料分割資料表平行大量資料匯入](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) 」中所述的指示建立新的資料庫，並將資料平行載入資料分割資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-151">In this section, we will follow the instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) to create a new database and load the data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="18517-152">登入 VM 之後，請啟動 **SQL Server Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="18517-152">While logged in to your VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="18517-153">使用 Windows 驗證進行連接。</span><span class="sxs-lookup"><span data-stu-id="18517-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS 連線][12]
3. <span data-ttu-id="18517-155">如果您尚未變更 SQL Server 驗證模式，且尚未建立新的 SQL 登入使用者，請開啟 [指令碼範例] 資料夾中名為 **change\_auth.sql** 的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="18517-155">If you have not yet changed the SQL Server authentication mode and created a new SQL login user, open the script file named **change\_auth.sql** in the **Sample Scripts** folder.</span></span> <span data-ttu-id="18517-156">變更預設的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="18517-156">Change the  default user name and password.</span></span> <span data-ttu-id="18517-157">按一下工具列中的 [ **!執行** ] 執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="18517-157">Click **!Execute** in the toolbar to run the script.</span></span>
   
    ![執行指令碼][13]
4. <span data-ttu-id="18517-159">驗證和 (或) 變更 SQL Server 預設資料庫和記錄檔資料夾，以確保新建立的資料庫會儲存於資料磁碟中。</span><span class="sxs-lookup"><span data-stu-id="18517-159">Verify and/or change the SQL Server default database and log folders to ensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="18517-160">系統會使用資料和記錄磁碟，預先設定已針對資料倉儲載入進行最佳化的 SQL Server VM 映像。</span><span class="sxs-lookup"><span data-stu-id="18517-160">The SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="18517-161">如果您的 VM 不含資料磁碟，而您在 VM 安裝過程中加入新的虛擬硬碟，則需變更預設資料夾，如下所示：</span><span class="sxs-lookup"><span data-stu-id="18517-161">If your VM did not include a Data Disk and you added new virtual hard disks during the VM setup process, change the default folders as follows:</span></span>
   
   * <span data-ttu-id="18517-162">以滑鼠右鍵按一下左面板中的 SQL Server 名稱，然後按一下 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="18517-162">Right-click the SQL Server name in the left panel and click **Properties**.</span></span>
     
       ![SQL Server 屬性][14]
   * <span data-ttu-id="18517-164">在左邊的 [選取頁面] 清單中，選取 [資料庫設定]。</span><span class="sxs-lookup"><span data-stu-id="18517-164">Select **Database Settings** from the **Select a page** list to the left.</span></span>
   * <span data-ttu-id="18517-165">確認**資料庫預設位置**，和 (或) 將其變更為您選擇的**資料磁碟**位置。</span><span class="sxs-lookup"><span data-stu-id="18517-165">Verify and/or change the **Database default locations** to the **Data Disk** locations of your choice.</span></span> <span data-ttu-id="18517-166">如果新資料庫是使用預設位置設定所建立，則此為新資料庫所在位置。</span><span class="sxs-lookup"><span data-stu-id="18517-166">This is where new databases reside if created with the default location settings.</span></span>
     
       ![SQL Database 的預設值][15]  
5. <span data-ttu-id="18517-168">若要建立新資料庫與一組檔案群組來保留資料分割資料表，請開啟指令碼範例 **create\_db\_default.sql**。</span><span class="sxs-lookup"><span data-stu-id="18517-168">To create a new database and a set of filegroups to hold the partitioned tables, open the sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="18517-169">指令碼將會在預設資料位置中建立名為 **TaxiNYC** 的新資料庫和 12 個檔案群組。</span><span class="sxs-lookup"><span data-stu-id="18517-169">The script will create a new database named **TaxiNYC** and 12 filegroups in the default data location.</span></span> <span data-ttu-id="18517-170">每個檔案群組都將保留一個月內的 trip\_data 和 trip\_fare 資料。</span><span class="sxs-lookup"><span data-stu-id="18517-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="18517-171">視需要修改資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="18517-171">Modify the database name, if desired.</span></span> <span data-ttu-id="18517-172">按一下 [ **!執行** ]，執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="18517-172">Click **!Execute** to run the script.</span></span>
6. <span data-ttu-id="18517-173">接下來，建立兩個資料分割資料表，一個用於 trip\_，另一個用於 trip\_fare。</span><span class="sxs-lookup"><span data-stu-id="18517-173">Next, create two partition tables, one for the trip\_data and another for the trip\_fare.</span></span> <span data-ttu-id="18517-174">開啟指令碼範例 **create\_partitioned\_table.sql**，其功用如下：</span><span class="sxs-lookup"><span data-stu-id="18517-174">Open the sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="18517-175">建立資料分割函式，以依月份分割資料。</span><span class="sxs-lookup"><span data-stu-id="18517-175">Create a partition function to split the data by month.</span></span>
   * <span data-ttu-id="18517-176">建立資料分割配置，將每個月的資料對應至不同的檔案群組。</span><span class="sxs-lookup"><span data-stu-id="18517-176">Create a partition scheme to map each month's data to a different filegroup.</span></span>
   * <span data-ttu-id="18517-177">建立兩個對應至資料分割配置的資料分割資料表：**nyctaxi\_trip** 會保留 trip\_data，**nyctaxi\_fare** 則會保留 trip\_fare 資料。</span><span class="sxs-lookup"><span data-stu-id="18517-177">Create two partitioned tables mapped to the partition scheme: **nyctaxi\_trip** will hold the trip\_data and **nyctaxi\_fare** will hold the trip\_fare data.</span></span>
     
     <span data-ttu-id="18517-178">按一下 [ **!執行** ] 執行指令碼，並建立資料分割資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-178">Click **!Execute** to run the script and create the partitioned tables.</span></span>
7. <span data-ttu-id="18517-179">[ **指令碼範例** ] 資料夾提供兩個 PowerShell 指令碼範例，可用來示範將資料平行大量匯入 SQL Server 資料表的方式。</span><span class="sxs-lookup"><span data-stu-id="18517-179">In the **Sample Scripts** folder, there are two sample PowerShell scripts provided to demonstrate parallel bulk imports of data to SQL Server tables.</span></span>
   
   * <span data-ttu-id="18517-180">**bcp\_parallel\_generic.ps1** 是將資料平行大量匯入資料表的泛型指令碼。</span><span class="sxs-lookup"><span data-stu-id="18517-180">**bcp\_parallel\_generic.ps1** is a generic script to parallel bulk import data into a table.</span></span> <span data-ttu-id="18517-181">修改此指令碼來設定輸入與目標變數，如指令碼的註解行中所示。</span><span class="sxs-lookup"><span data-stu-id="18517-181">Modify this script to set the input and target variables as indicated in the comment lines in the script.</span></span>
   * <span data-ttu-id="18517-182">**bcp\_parallel\_nyctaxi.ps1** 是預先設定的泛型指令碼版本，可用來同時載入適用於「NYC 計程車車程」資料的兩種資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of the generic script and can be used to to load both tables for the NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="18517-183">以滑鼠右鍵按一下 **bcp\_parallel\_nyctaxi.ps1** 指令碼名稱，然後按一下 [編輯] 利用 PowerShell 開啟。</span><span class="sxs-lookup"><span data-stu-id="18517-183">Right-click the **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** to open it in PowerShell.</span></span> <span data-ttu-id="18517-184">檢閱預設的變數，並根據您選取的資料庫名稱、輸入資料資料夾、目標記錄資料夾，以及格式檔案範例 **nyctaxi_trip.xml** 和 **nyctaxi\_fare.xml** (位於 [指令碼範例] 資料夾) 的路徑進行修改。</span><span class="sxs-lookup"><span data-stu-id="18517-184">Review the preset variables and modify according to your selected database name, input data folder, target log folder, and paths to the  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in the **Sample Scripts** folder).</span></span>
   
    ![大量匯入資料][16]
   
    <span data-ttu-id="18517-186">您也可以選取驗證模式，預設值是 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="18517-186">You may also select the authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="18517-187">按一下工具列中的綠色箭頭來執行。</span><span class="sxs-lookup"><span data-stu-id="18517-187">Click the green arrow in the toolbar to run.</span></span> <span data-ttu-id="18517-188">指令碼將平行啟動 24 個大量匯入作業，針對每個資料分割資料表啟動 12 個作業。</span><span class="sxs-lookup"><span data-stu-id="18517-188">The script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="18517-189">您可以藉由開啟 SQL Server 預設資料資料夾 (如上述所設定)，來監視資料匯入進度。</span><span class="sxs-lookup"><span data-stu-id="18517-189">You may monitor the data import progress by opening the SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="18517-190">PowerShell 指令碼會報告開始和結束時間。</span><span class="sxs-lookup"><span data-stu-id="18517-190">The PowerShell script reports the starting and ending times.</span></span> <span data-ttu-id="18517-191">完成所有大量匯入時，即會報告結束時間。</span><span class="sxs-lookup"><span data-stu-id="18517-191">When all bulk imports complete, the ending time is reported.</span></span> <span data-ttu-id="18517-192">檢查目標記錄資料夾，以確認大量匯入已成功，亦即，目標記錄資料夾中未報告任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="18517-192">Check the target log folder to verify that the bulk imports were successful, i.e., no errors reported in the target log folder.</span></span>
10. <span data-ttu-id="18517-193">您的資料庫已準備好進行探索、功能工程，以及所需的其他作業。</span><span class="sxs-lookup"><span data-stu-id="18517-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="18517-194">由於這些資料表是根據 **pickup\_datetime** 欄位來進行資料分割，因此資料分割配置將為在 **WHERE** 子句中加入 **pickup\_datetime** 條件的查詢帶來好處。</span><span class="sxs-lookup"><span data-stu-id="18517-194">Since the tables are partitioned according to the **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in the **WHERE** clause will benefit from the partition scheme.</span></span>
11. <span data-ttu-id="18517-195">在 **SQL Server Management Studio** 中，探索當中提供的指令碼範例 **sample\_queries.sql**。</span><span class="sxs-lookup"><span data-stu-id="18517-195">In **SQL Server Management Studio**, explore the provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="18517-196">若要執行查詢範例，請先將查詢行反白，然後按一下工具列中的 [ **!執行** ]。</span><span class="sxs-lookup"><span data-stu-id="18517-196">To run any of the sample queries, highlight the query lines then click **!Execute** in the toolbar.</span></span>
12. <span data-ttu-id="18517-197">「NYC 計程車車程」資料會載入兩個不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-197">The NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="18517-198">若要改善聯結作業，強烈建議您為資料表編製索引。</span><span class="sxs-lookup"><span data-stu-id="18517-198">To improve join operations, it is highly recommended to index the tables.</span></span> <span data-ttu-id="18517-199">指令碼範例 **create\_partitioned\_index.sql** 會在複合聯結索引鍵 **medallion、hack\_license 和 pickup\_datetime** 上建立資料分割索引。</span><span class="sxs-lookup"><span data-stu-id="18517-199">The sample script **create\_partitioned\_index.sql** creates partitioned indexes on the composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="18517-200"><a name="dbexplore"></a>SQL Server 中的資料探索和功能工程</span><span class="sxs-lookup"><span data-stu-id="18517-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="18517-201">在本節中，我們將使用先前建立的 SQL Server 資料庫，直接在 **SQL Server Management Studio** 中執行 SQL 查詢，藉此探索資料和產生功能。</span><span class="sxs-lookup"><span data-stu-id="18517-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in the **SQL Server Management Studio** using the SQL Server database created earlier.</span></span> <span data-ttu-id="18517-202">名為 **sample\_queries.sql** 的指令碼範例位於 [指令碼範例] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="18517-202">A sample script named **sample\_queries.sql** is provided in the **Sample Scripts** folder.</span></span> <span data-ttu-id="18517-203">若資料庫名稱與預設名稱： **TaxiNYC**不同，請修改指令碼變更該名稱。</span><span class="sxs-lookup"><span data-stu-id="18517-203">Modify the script to change the database name, if it is different from the default: **TaxiNYC**.</span></span>

<span data-ttu-id="18517-204">在這個練習中，我們將：</span><span class="sxs-lookup"><span data-stu-id="18517-204">In this exercise, we will:</span></span>

* <span data-ttu-id="18517-205">使用 Windows 驗證，或 SQL 驗證及 SQL 登入名稱和密碼，連接至 **SQL Server Management Studio** 。</span><span class="sxs-lookup"><span data-stu-id="18517-205">Connect to **SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and the SQL login name and password.</span></span>
* <span data-ttu-id="18517-206">在變動的時間範圍中探索數個欄位的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="18517-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="18517-207">調查經度和緯度欄位的資料品質。</span><span class="sxs-lookup"><span data-stu-id="18517-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="18517-208">根據 **tip\_amount** 產生二進位和多類別分類標籤。</span><span class="sxs-lookup"><span data-stu-id="18517-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="18517-209">產生功能，並計算或比較車程距離。</span><span class="sxs-lookup"><span data-stu-id="18517-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="18517-210">聯結這兩個資料表，並擷取將用來建置模型的隨機取樣。</span><span class="sxs-lookup"><span data-stu-id="18517-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

<span data-ttu-id="18517-211">當您準備好繼續進行 Azure Machine Learning，您可以：</span><span class="sxs-lookup"><span data-stu-id="18517-211">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="18517-212">儲存最後一個 SQL 查詢以對資料進行擷取和取樣，然後複製該查詢並直接貼到 Azure Machine Learning 中的[匯入資料][import-data]模組，或者</span><span class="sxs-lookup"><span data-stu-id="18517-212">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="18517-213">將您計畫用來建置模型的取樣和工程設計資料保存在新資料庫資料表中，然後在 Azure Machine Learning 的[匯入資料][import-data]模組中使用該新資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-213">Persist the sampled and engineered data you plan to use for model building in a new database table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="18517-214">在本節中，我們會儲存最後一個查詢，以擷取資料並對資料進行取樣。</span><span class="sxs-lookup"><span data-stu-id="18517-214">In this section we will save the final query to extract and sample the data.</span></span> <span data-ttu-id="18517-215">＜ [IPython Notebook 中的資料探索和功能工程](#ipnb) ＞一節中示範了第二個方法的執行方式。</span><span class="sxs-lookup"><span data-stu-id="18517-215">The second method is demonstrated in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="18517-216">若要在先前使用平行大量匯入所填入的資料表中，快速驗證資料列與資料行的數目，</span><span class="sxs-lookup"><span data-stu-id="18517-216">For a quick verification of the number of rows and columns in the tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="18517-217">探索：依據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="18517-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="18517-218">此範例會識別在特定期間內超過 100 趟車程的圓形徽章 (計程車數目)。</span><span class="sxs-lookup"><span data-stu-id="18517-218">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="18517-219">資料分割資料表存取的條件是以 **pickup\_datetime** 資料分割配置為依據，因為可為查詢帶來好處。</span><span class="sxs-lookup"><span data-stu-id="18517-219">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="18517-220">查詢完整資料集也會使用資料分割資料表及 (或) 索引掃描。</span><span class="sxs-lookup"><span data-stu-id="18517-220">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="18517-221">探索：依據 medallion 和 hack_license 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="18517-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="18517-222">資料品質評估：驗證含有不正確經度和/或緯度的記錄</span><span class="sxs-lookup"><span data-stu-id="18517-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="18517-223">此範例會檢查是否有任何經度和 (或) 緯度欄位包含無效值 (弧度角度應介於-90 和 90 之間)，或是具有 (0，0) 座標。</span><span class="sxs-lookup"><span data-stu-id="18517-223">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="18517-224">探索：已支付小費和未支付小費的車程分佈</span><span class="sxs-lookup"><span data-stu-id="18517-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="18517-225">此範例會尋找在指定期間內 (或者，如果涵蓋一整年，則是在整個資料庫中)，已收到小費及未收到小費的車程數目。</span><span class="sxs-lookup"><span data-stu-id="18517-225">This example finds the number of trips that were tipped vs. not tipped in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="18517-226">此分佈會反映二進位標籤分佈，以便稍後用來將二進位分類模型化。</span><span class="sxs-lookup"><span data-stu-id="18517-226">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="18517-227">探索：小費類別/範圍分佈</span><span class="sxs-lookup"><span data-stu-id="18517-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="18517-228">此範例會計算在指定期間內 (或者，如果涵蓋一整年，則是在整個資料庫中) 小費範圍的分佈。</span><span class="sxs-lookup"><span data-stu-id="18517-228">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="18517-229">這是標籤類別的分佈，會在稍後用來將多類別分類模型化。</span><span class="sxs-lookup"><span data-stu-id="18517-229">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

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

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="18517-230">探索：計算並比較車程距離</span><span class="sxs-lookup"><span data-stu-id="18517-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="18517-231">此範例會將上車和下車的經緯度轉換為 SQL 地理位置點、使用 SQL 地理位置點的差距來計算車程距離，然後傳回結果的隨機取樣以進行比較。</span><span class="sxs-lookup"><span data-stu-id="18517-231">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="18517-232">此範例只會使用稍早所提供的資料品質評估查詢，將結果限制為有效座標。</span><span class="sxs-lookup"><span data-stu-id="18517-232">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

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

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="18517-233">SQL 查詢中的功能工程</span><span class="sxs-lookup"><span data-stu-id="18517-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="18517-234">標籤產生和地理位置轉換探索查詢也可藉由移除計數組件，用來產生標籤或功能。</span><span class="sxs-lookup"><span data-stu-id="18517-234">The label generation and geography conversion exploration queries can also be used to generate labels/features by removing the counting part.</span></span> <span data-ttu-id="18517-235">＜ [IPython Notebook 中的資料探索和功能工程](#ipnb) ＞一節中提供了其他的功能工程 SQL 範例。</span><span class="sxs-lookup"><span data-stu-id="18517-235">Additional feature engineering SQL examples are provided in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="18517-236">使用可在 SQL Server 資料庫執行個體上直接執行的 SQL 查詢，以更有效率的方式在整個資料集或其上的大型子集上執行功能產生查詢。</span><span class="sxs-lookup"><span data-stu-id="18517-236">It is more efficient to run the feature generation queries on the full dataset or a large subset of it using SQL queries which run directly on the SQL Server database instance.</span></span> <span data-ttu-id="18517-237">查詢可能會在 **SQL Server Management Studio**、IPython Notebook 或任何可在本機或遠端存取資料庫的開發工具或環境中執行。</span><span class="sxs-lookup"><span data-stu-id="18517-237">The queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access the database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="18517-238">準備資料以進行模型建置</span><span class="sxs-lookup"><span data-stu-id="18517-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="18517-239">下列查詢可聯結 **nyctaxi\_trip** 和 **nyctaxi\_fare** 資料表、產生二進位分類標籤 **tipped**、多類別分類標籤 **tip\_class**，以及從完整聯結的資料集中擷取 1% 的隨機取樣。</span><span class="sxs-lookup"><span data-stu-id="18517-239">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from the full joined dataset.</span></span> <span data-ttu-id="18517-240">您可以複製此查詢並直接貼到 [Azure Machine Learning Studio](https://studio.azureml.net) 的[匯入資料][import-data]模組，以便從 Azure 中的 SQL Server 資料庫執行個體直接擷取資料。</span><span class="sxs-lookup"><span data-stu-id="18517-240">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL Server database instance in Azure.</span></span> <span data-ttu-id="18517-241">查詢會排除含有不正確 (0, 0) 座標的記錄。</span><span class="sxs-lookup"><span data-stu-id="18517-241">The query excludes records with incorrect (0, 0) coordinates.</span></span>

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


## <span data-ttu-id="18517-242"><a name="ipnb"></a>IPython Notebook 中的資料探索和功能工程</span><span class="sxs-lookup"><span data-stu-id="18517-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="18517-243">在本節中，我們將在先前建立的 SQL Server 資料庫中進行 Python 和 SQL 查詢，藉此探索資料和產生功能。</span><span class="sxs-lookup"><span data-stu-id="18517-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL Server database created earlier.</span></span> <span data-ttu-id="18517-244">名為 **machine-Learning-data-science-process-sql-story.ipynb** 的 IPython Notebook 範例位於 [Sample IPython Notebook 範例] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="18517-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in the **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="18517-245">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)也提供此 Notebook。</span><span class="sxs-lookup"><span data-stu-id="18517-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="18517-246">使用巨量資料時的建議順序如下：</span><span class="sxs-lookup"><span data-stu-id="18517-246">The recommended sequence when working with big data is the following:</span></span>

* <span data-ttu-id="18517-247">將小型資料取樣讀取至記憶體中的資料框架。</span><span class="sxs-lookup"><span data-stu-id="18517-247">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="18517-248">使用取樣的資料來執行一些視覺化操作和探索。</span><span class="sxs-lookup"><span data-stu-id="18517-248">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="18517-249">使用取樣的資料來試驗功能工程。</span><span class="sxs-lookup"><span data-stu-id="18517-249">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="18517-250">如為較大型的資料探索、資料操作及功能工程，請使用 Pythont，針對 Azure VM 中的 SQL Server 資料庫直接發出 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="18517-250">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL Server database in the Azure VM.</span></span>
* <span data-ttu-id="18517-251">決定用於 Azure Machine Learning 模型建置的取樣大小。</span><span class="sxs-lookup"><span data-stu-id="18517-251">Decide the sample size to use for Azure Machine Learning model building.</span></span>

<span data-ttu-id="18517-252">準備好繼續進行 Azure Machine Learning 時，您可以：</span><span class="sxs-lookup"><span data-stu-id="18517-252">When ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="18517-253">儲存最後一個 SQL 查詢以對資料進行擷取和取樣，然後複製該查詢並直接貼到 Azure Machine Learning 中的[匯入資料][import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="18517-253">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="18517-254">＜ [在 Azure Machine Learning 中建置模型](#mlmodel) ＞一節中示範了此方法的執行方式。</span><span class="sxs-lookup"><span data-stu-id="18517-254">This method is demonstrated in the [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="18517-255">將您計畫用來建置模型的取樣和工程設計資料保存在新資料庫資料表中，然後在[匯入資料][import-data]模組中使用該新資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-255">Persist the sampled and engineered data you plan to use for model building in a new database table, then use the new table in the [Import Data][import-data] module.</span></span>

<span data-ttu-id="18517-256">以下是數個資料探索、資料視覺化及功能工程範例。</span><span class="sxs-lookup"><span data-stu-id="18517-256">The following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="18517-257">如需其他範例，請參考 [ **IPython Notebooks 範例** ] 資料夾中的 SQL IPython Notebook 範例。</span><span class="sxs-lookup"><span data-stu-id="18517-257">For more examples, see the sample SQL IPython notebook in the **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="18517-258">初始化資料庫認證</span><span class="sxs-lookup"><span data-stu-id="18517-258">Initialize Database Credentials</span></span>
<span data-ttu-id="18517-259">使用下列變數來初始化資料庫連接設定：</span><span class="sxs-lookup"><span data-stu-id="18517-259">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="18517-260">建立資料庫連接</span><span class="sxs-lookup"><span data-stu-id="18517-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="18517-261">報告資料表 nyctaxi_trip 中資料列和資料行的數目</span><span class="sxs-lookup"><span data-stu-id="18517-261">Report number of rows and columns in table nyctaxi_trip</span></span>
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

* <span data-ttu-id="18517-262">資料列總數 = 173179759</span><span class="sxs-lookup"><span data-stu-id="18517-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="18517-263">資料行總數 = 14</span><span class="sxs-lookup"><span data-stu-id="18517-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a><span data-ttu-id="18517-264">從 SQL Server 資料庫讀入小型資料取樣</span><span class="sxs-lookup"><span data-stu-id="18517-264">Read-in a small data sample from the SQL Server Database</span></span>
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
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="18517-265">讀取取樣資料表的時間為 6.492000 秒</span><span class="sxs-lookup"><span data-stu-id="18517-265">Time to read the sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="18517-266">擷取的資料列和資料行數目 = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="18517-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="18517-267">描述性統計資料</span><span class="sxs-lookup"><span data-stu-id="18517-267">Descriptive Statistics</span></span>
<span data-ttu-id="18517-268">現在已經準備好來探索取樣的資料。</span><span class="sxs-lookup"><span data-stu-id="18517-268">Now are ready to explore the sampled data.</span></span> <span data-ttu-id="18517-269">一開始會先查看 **trip\_distance** 欄位或任何其他欄位的描述性統計資料：</span><span class="sxs-lookup"><span data-stu-id="18517-269">We start with looking at descriptive statistics for the **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="18517-270">視覺效果：盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="18517-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="18517-271">接下來將查看車程距離的盒狀圖，以視覺化方式檢視分位數</span><span class="sxs-lookup"><span data-stu-id="18517-271">Next we look at the box plot for the trip distance to visualize the quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![圖 #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="18517-273">視覺效果：分佈的盒狀圖範例</span><span class="sxs-lookup"><span data-stu-id="18517-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![圖 #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="18517-275">視覺效果：橫條和折線圖</span><span class="sxs-lookup"><span data-stu-id="18517-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="18517-276">在此範例中，我們可以將車程距離分類收納為五個分類收納組，並將分類收納結果視覺化。</span><span class="sxs-lookup"><span data-stu-id="18517-276">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="18517-277">我們可以在橫條圖或折線圖中繪製上述分類收納組的分佈，如下所示</span><span class="sxs-lookup"><span data-stu-id="18517-277">We can plot the above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![圖 #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![圖 #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="18517-280">視覺效果：散佈圖範例</span><span class="sxs-lookup"><span data-stu-id="18517-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="18517-281">這會顯示 **trip\_time\_in\_secs** 與 **trip\_distance** 之間的散佈圖，供您查看當中是否有任何關聯性</span><span class="sxs-lookup"><span data-stu-id="18517-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![圖 #6][6]

<span data-ttu-id="18517-283">也可以同樣的方式查看 **rate\_code** 與 **trip\_distance** 之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="18517-283">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![圖 #8][8]

### <a name="sub-sampling-the-data-in-sql"></a><span data-ttu-id="18517-285">針對 SQL 中的資料進行次取樣</span><span class="sxs-lookup"><span data-stu-id="18517-285">Sub-Sampling the Data in SQL</span></span>
<span data-ttu-id="18517-286">準備在 [Azure Machine Learning Studio](https://studio.azureml.net) 中建置模型所需的資料時，您可以決定**要直接在「匯入資料」模組中使用的 SQL 查詢**，或將工程設計和取樣資料保存在新的資料表中，您只要利用簡單的 **SELECT * FROM <your\_new\_table\_name>**，即可在[匯入資料][import-data]模組中使用此資料表。</span><span class="sxs-lookup"><span data-stu-id="18517-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on the **SQL query to use directly in the Import Data module** or persist the engineered and sampled data in a new table, which you could use in the [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="18517-287">在本節中，我們將建立新的資料表來保留取樣與工程資料。</span><span class="sxs-lookup"><span data-stu-id="18517-287">In this section we will create a new table to hold the sampled and engineered data.</span></span> <span data-ttu-id="18517-288">＜ [SQL Server 中的資料探索和功能工程](#dbexplore) ＞一節中提供了可用來建置模型的直接 SQL 查詢範例。</span><span class="sxs-lookup"><span data-stu-id="18517-288">An example of a direct SQL query for model building is provided in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="18517-289">建立取樣資料表並使用 1% 的聯結資料表來填入。</span><span class="sxs-lookup"><span data-stu-id="18517-289">Create a Sample Table and Populate with 1% of the Joined Tables.</span></span> <span data-ttu-id="18517-290">如果資料表存在，請先卸除它。</span><span class="sxs-lookup"><span data-stu-id="18517-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="18517-291">在本節中，我們會聯結資料表 **nyctaxi\_trip** 和 **nyctaxi\_fare**、擷取 1% 的隨機取樣，然後將取樣的資料保存在名為 **nyctaxi\_one\_percent** 的新資料表中：</span><span class="sxs-lookup"><span data-stu-id="18517-291">In this section, we join the tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist the sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="18517-292">在 IPython Notebook 中使用 SQL 查詢進行資料探索</span><span class="sxs-lookup"><span data-stu-id="18517-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="18517-293">在本節中，我們將使用前面所建立的新資料表中保存的 1% 取樣資料，來探索資料分佈。</span><span class="sxs-lookup"><span data-stu-id="18517-293">In this section, we explore data distributions using the 1% sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="18517-294">請注意，如 [SQL Server 中的資料探索和功能工程](#dbexplore)一節所述，您可以使用原始資料表，或是使用 **TABLESAMPLE** 執行類似的探索，以限制探索範例，或是透過使用 **pickup\_datetime** 資料分割，將結果限制為指定的期間。</span><span class="sxs-lookup"><span data-stu-id="18517-294">Note that similar explorations can be performed using the original tables, optionally using **TABLESAMPLE** to limit the exploration sample or by limiting the results to a given time period using the **pickup\_datetime** partitions, as illustrated in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="18517-295">探索：車程的每日分佈</span><span class="sxs-lookup"><span data-stu-id="18517-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="18517-296">探索：根據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="18517-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="18517-297">在 IPython Notebook 中使用 SQL 查詢進行的功能工程</span><span class="sxs-lookup"><span data-stu-id="18517-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="18517-298">本節將使用 SQL 查詢，直接產生新的標籤和功能，以便在我們於上一節中建立的 1% 取樣資料表上進行操作。</span><span class="sxs-lookup"><span data-stu-id="18517-298">In this section we will generate new labels and features directly using SQL queries, operating on the 1% sample table we created in the previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="18517-299">標籤產生：產生類別標籤</span><span class="sxs-lookup"><span data-stu-id="18517-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="18517-300">在下列範例中，我們會產生兩組標籤以用來進行模型化：</span><span class="sxs-lookup"><span data-stu-id="18517-300">In the following example, we generate two sets of labels to use for modeling:</span></span>

1. <span data-ttu-id="18517-301">二進位類別標籤 **tipped** (預測是否將給予小費)</span><span class="sxs-lookup"><span data-stu-id="18517-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="18517-302">多類別標籤 **tip\_class** (預測小費的收納組或範圍)</span><span class="sxs-lookup"><span data-stu-id="18517-302">Multiclass Labels **tip\_class** (predicting the tip bin or range)</span></span>
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="18517-303">功能工程：適用於類別資料行的計數功能</span><span class="sxs-lookup"><span data-stu-id="18517-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="18517-304">此範例會將類別欄位轉換為數值欄位，方法是使用它在資料中發生的計數來取代每個類別。</span><span class="sxs-lookup"><span data-stu-id="18517-304">This example transforms a categorical field into a numeric field by replacing each category with the count of its occurrences in the data.</span></span>

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="18517-305">功能工程：適用於數字資料行的收納組功能</span><span class="sxs-lookup"><span data-stu-id="18517-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="18517-306">此範例會將連續的數值欄位轉換成預設的類別範圍，亦即，將數值欄位轉換到類別欄位。</span><span class="sxs-lookup"><span data-stu-id="18517-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="18517-307">功能工程：從十進位經緯度擷取位置功能</span><span class="sxs-lookup"><span data-stu-id="18517-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="18517-308">此範例會將緯度和/或經度欄位的十進位表示法細分為資料粒度不同的多個區域欄位，例如國家/地區、城市、城鎮、街區等。請注意，新的地理位置欄位不會對應到實際的位置。</span><span class="sxs-lookup"><span data-stu-id="18517-308">This example breaks down the decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that the new geo-fields are not mapped to actual locations.</span></span> <span data-ttu-id="18517-309">如需對應地理編碼位置的資訊，請參閱 [Bing 地圖服務 REST 服務](https://msdn.microsoft.com/library/ff701710.aspx)。</span><span class="sxs-lookup"><span data-stu-id="18517-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

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

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="18517-310">驗證功能化表格的最後形式</span><span class="sxs-lookup"><span data-stu-id="18517-310">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="18517-311">我們現在已準備好在 [Azure Machine Learning](https://studio.azureml.net)中建置和部署模型。</span><span class="sxs-lookup"><span data-stu-id="18517-311">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="18517-312">資料已經準備好用於稍早所識別的任何預測問題，也就是：</span><span class="sxs-lookup"><span data-stu-id="18517-312">The data is ready for any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="18517-313">二進位分類：預測是否已支付某趟車程的小費。</span><span class="sxs-lookup"><span data-stu-id="18517-313">Binary classification: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="18517-314">多類別分類：根據先前定義的類別，預測所支付的小費範圍。</span><span class="sxs-lookup"><span data-stu-id="18517-314">Multiclass classification: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="18517-315">迴歸工作：預測已針對某趟車程支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="18517-315">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="18517-316"><a name="mlmodel"></a>在 Azure Machine Learning 中建置模型</span><span class="sxs-lookup"><span data-stu-id="18517-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="18517-317">若要開始進行模型化練習，請登入 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="18517-317">To begin the modeling exercise, log in to your Azure Machine Learning workspace.</span></span> <span data-ttu-id="18517-318">如果您尚未建立機器學習服務工作區，請參閱 [建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="18517-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="18517-319">若要開始使用 Azure Machine Learning，請參閱「 [什麼是 Azure Machine Learning Studio？](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="18517-319">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="18517-320">登入 [Azure Machine Learning Studio](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="18517-320">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="18517-321">Studio 首頁會提供豐富的資訊、影片、教學課程、與模組參考的連結，以及其他資源。</span><span class="sxs-lookup"><span data-stu-id="18517-321">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="18517-322">如需 Azure Machine Learning 的詳細資訊，請參閱「 [Azure Machine Learning 文件中心](https://azure.microsoft.com/documentation/services/machine-learning/)」。</span><span class="sxs-lookup"><span data-stu-id="18517-322">Fore more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="18517-323">典型的訓練體驗包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="18517-323">A typical training experiment consists of the following:</span></span>

1. <span data-ttu-id="18517-324">建立 **+NEW** 實驗。</span><span class="sxs-lookup"><span data-stu-id="18517-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="18517-325">將資料放到 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="18517-325">Get the data to Azure Machine Learning.</span></span>
3. <span data-ttu-id="18517-326">視需要前置處理、轉換和操作資料。</span><span class="sxs-lookup"><span data-stu-id="18517-326">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="18517-327">視需要產生功能。</span><span class="sxs-lookup"><span data-stu-id="18517-327">Generate features as needed.</span></span>
5. <span data-ttu-id="18517-328">將資料分割為訓練/驗證/測試資料集 (或讓每一個擁有個別的資料集)。</span><span class="sxs-lookup"><span data-stu-id="18517-328">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="18517-329">根據要解決的學習問題，選取一或多個機器學習服務演算法。</span><span class="sxs-lookup"><span data-stu-id="18517-329">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="18517-330">例如，二進位分類、多類別分類、迴歸。</span><span class="sxs-lookup"><span data-stu-id="18517-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="18517-331">使用訓練資料集來訓練一或多個模型。</span><span class="sxs-lookup"><span data-stu-id="18517-331">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="18517-332">使用訓練的模型，為驗證資料集計分。</span><span class="sxs-lookup"><span data-stu-id="18517-332">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="18517-333">評估模型來計算適用於學習問題的相關度量。</span><span class="sxs-lookup"><span data-stu-id="18517-333">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="18517-334">微調模型，並選取要部署的最佳模型。</span><span class="sxs-lookup"><span data-stu-id="18517-334">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="18517-335">在這個練習中，我們已經探索了 SQL Server 中的資料並進行工程 (步驟 1-4)，並且決定了要在 Azure Machine Learning 中內嵌的取樣大小。</span><span class="sxs-lookup"><span data-stu-id="18517-335">In this exercise, we have already explored and engineered the data in SQL Server, and decided on the sample size to ingest in Azure Machine Learning.</span></span> <span data-ttu-id="18517-336">建置一或多個我們所決定的預測模型：</span><span class="sxs-lookup"><span data-stu-id="18517-336">To build one or more of the prediction models we decided:</span></span>

1. <span data-ttu-id="18517-337">使用[匯入資料][import-data]模組 (可從**資料輸入和輸出**一節取得)，將資料匯入 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="18517-337">Get the data to Azure Machine Learning using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="18517-338">如需詳細資訊，請參閱[匯入資料][import-data]模組參考頁面。</span><span class="sxs-lookup"><span data-stu-id="18517-338">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Azure Machine Learning 匯入資料][17]
2. <span data-ttu-id="18517-340">在 [屬性] 面板中，選取 [Azure SQL Database] 做為 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="18517-340">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="18517-341">在 [ **資料庫伺服器名稱** ] 欄位中輸入資料庫的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="18517-341">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="18517-342">格式： `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="18517-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="18517-343">在對應欄位中輸入 **資料庫名稱** 。</span><span class="sxs-lookup"><span data-stu-id="18517-343">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="18517-344">在 **[伺服器使用者帳戶名稱] 中輸入 **SQL 使用者名稱**，並在 [伺服器使用者帳戶密碼] 中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="18517-344">Enter the **SQL user name** in the **Server user aqccount name, and the password in the **Server user account password**.</span></span>
6. <span data-ttu-id="18517-345">選取 [ **接受任何伺服器憑證** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="18517-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="18517-346">在 [ **資料庫查詢** ] 中編輯文字區域、貼上可擷取必要資料庫欄位的查詢 (包括任何經過計算的欄位，例如標籤)，以及向下取樣所需大小的資料。</span><span class="sxs-lookup"><span data-stu-id="18517-346">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="18517-347">下圖顯示從 SQL Server 資料庫中直接讀取資料的二進位分類實驗範例。</span><span class="sxs-lookup"><span data-stu-id="18517-347">An example of a binary classification experiment reading data directly from the SQL Server database is in the figure below.</span></span> <span data-ttu-id="18517-348">您可以針對多類別分類和迴歸問題建構類似的實驗。</span><span class="sxs-lookup"><span data-stu-id="18517-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning 訓練][10]

> [!IMPORTANT]
> <span data-ttu-id="18517-350">在前幾節中提供的模型化資料擷取和取樣查詢範例中， **這三個模型化練習的所有標籤都包含於此查詢中**。</span><span class="sxs-lookup"><span data-stu-id="18517-350">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="18517-351">每一個模型化練習的重要 (必要) 步驟都是針對其他兩個問題**排除**不需要的標籤，以及任何其他的**目標流失**。</span><span class="sxs-lookup"><span data-stu-id="18517-351">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="18517-352">例如，使用二進位分類時，請用 **tipped** 標籤，並排除 **tip\_class**、**tip\_amount** 和 **total\_amount** 欄位。</span><span class="sxs-lookup"><span data-stu-id="18517-352">For e.g., when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="18517-353">後者為目標流失，因為它們意指支付的小費。</span><span class="sxs-lookup"><span data-stu-id="18517-353">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="18517-354">若要排除不必要的資料行和 (或) 目標流失，您可以使用[選取資料集中的資料行][select-columns]模組或[編輯中繼資料][edit-metadata]。</span><span class="sxs-lookup"><span data-stu-id="18517-354">To exclude unnecessary columns and/or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="18517-355">如需詳細資訊，請參閱[選取資料集中的資料行][select-columns]和[編輯中繼資料][edit-metadata]參考頁面。</span><span class="sxs-lookup"><span data-stu-id="18517-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="18517-356"><a name="mldeploy"></a>在 Azure Machine Learning 中部署模型</span><span class="sxs-lookup"><span data-stu-id="18517-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="18517-357">當您備妥模型時，可以輕鬆地直接從實驗中將它部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="18517-357">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="18517-358">如需關於部署 Azure Machine Learning Web 服務的詳細資訊，請參閱 [部署 Azure 機器學習 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="18517-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="18517-359">若要部署新的 Web 服務，您需要：</span><span class="sxs-lookup"><span data-stu-id="18517-359">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="18517-360">建立計分實驗。</span><span class="sxs-lookup"><span data-stu-id="18517-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="18517-361">部署 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="18517-361">Deploy the web service.</span></span>

<span data-ttu-id="18517-362">若要從「已完成」的訓練實驗建立評分實驗，請按一下下方動作列中的 [建立評分實驗]。</span><span class="sxs-lookup"><span data-stu-id="18517-362">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Azure 評分][18]

<span data-ttu-id="18517-364">Azure Machine Learning 將根據訓練實驗的元件來建立計分實驗。</span><span class="sxs-lookup"><span data-stu-id="18517-364">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="18517-365">特別是，它將：</span><span class="sxs-lookup"><span data-stu-id="18517-365">In particular, it will:</span></span>

1. <span data-ttu-id="18517-366">儲存訓練的模型，並移除模型訓練模組。</span><span class="sxs-lookup"><span data-stu-id="18517-366">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="18517-367">識別邏輯 **輸入連接埠** ，表示預期的輸入資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="18517-367">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="18517-368">識別邏輯 **輸出連接埠** ，表示預期的 Web 服務輸出結構描述。</span><span class="sxs-lookup"><span data-stu-id="18517-368">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="18517-369">建立計分實驗時，請檢閱它，並視需要進行調整。</span><span class="sxs-lookup"><span data-stu-id="18517-369">When the scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="18517-370">典型的調整是使用某一個會排除標籤欄位的輸入資料集和 (或) 查詢來取代它們，因為在呼叫服務時將無法使用這些欄位。</span><span class="sxs-lookup"><span data-stu-id="18517-370">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="18517-371">若要將輸入資料集和 (或) 查詢的大小縮減為只有幾筆足以表示輸入結構描述的記錄，這也是個很好的練習。</span><span class="sxs-lookup"><span data-stu-id="18517-371">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="18517-372">針對輸出連接埠，通常會使用[選取資料集中的資料行][select-columns]模組在輸出中排除所有輸入欄位，只包含**計分標籤**和**計分機率**。</span><span class="sxs-lookup"><span data-stu-id="18517-372">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="18517-373">下圖為計分實驗範例。</span><span class="sxs-lookup"><span data-stu-id="18517-373">A sample scoring experiment is in the figure below.</span></span> <span data-ttu-id="18517-374">準備部署時，請按下方動作列中的 [發佈 Web 服務]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="18517-374">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Azure Machine Learning 發佈][11]

<span data-ttu-id="18517-376">總言之，在此逐步解說教學課程中，您已經建立 Azure 資料科學環境，從資料擷取到 Azure 機器學習 Web 服務的模型訓練和部署，這整個過程中都會使用大型公用資料集。</span><span class="sxs-lookup"><span data-stu-id="18517-376">To recap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all the way from data acquisition to model training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="18517-377">授權資訊</span><span class="sxs-lookup"><span data-stu-id="18517-377">License Information</span></span>
<span data-ttu-id="18517-378">此逐步解說範例及其隨附的指令碼和 IPython Notebook 是在 MIT 授權下由 Microsoft 所共用。</span><span class="sxs-lookup"><span data-stu-id="18517-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="18517-379">如需詳細資訊，請檢查 GitHub 上程式碼範例目錄中的 LICENSE.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="18517-379">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="18517-380">參考</span><span class="sxs-lookup"><span data-stu-id="18517-380">References</span></span>
<span data-ttu-id="18517-381">•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="18517-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="18517-382">•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="18517-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="18517-383">•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="18517-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
