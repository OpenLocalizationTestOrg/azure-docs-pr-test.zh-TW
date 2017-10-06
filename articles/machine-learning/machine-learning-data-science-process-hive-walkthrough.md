---
title: "aaaExplore 資料在 Hadoop 叢集，並在 Azure Machine Learning 中建立模型 |Microsoft 文件"
description: "使用 hello 小組資料科學程序的端對端案例，採用 HDInsight Hadoop 叢集 toobuild，並部署模型，使用公開可用的資料集。"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="c9d91-103">在動作中的 hello 小組資料科學程序： 使用 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="c9d91-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="c9d91-104">在本逐步解說中，我們使用 hello[小組資料科學程序 (TDSP)](data-science-process-overview.md)端對端實例使用[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，探索和公開功能從 hello 的工程資料可用[NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集和 toodown 範例 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="c9d91-105">使用 Azure Machine Learning toohandle 二進位和多級分類和迴歸的預測工作所建置的 hello 資料模型。</span><span class="sxs-lookup"><span data-stu-id="c9d91-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="c9d91-106">如需示範如何 toohandle 較大的 (1 tb) 資料集的類似的狀況使用 HDInsight Hadoop 叢集以提供資料處理的逐步解說，請參閱[小組資料科學流程1TB資料集上使用AzureHDInsightHadoop叢集](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c9d91-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="c9d91-107">它也是可能 toouse IPython 筆記型電腦 tooaccomplish hello 工作呈現的 hello 逐步解說使用 hello 1 TB 的資料集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="c9d91-108">使用者會像這種方法，應洽詢的 tootry hello [Criteo 逐步解說使用 hive 控制檔的 ODBC 連接](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb)主題。</span><span class="sxs-lookup"><span data-stu-id="c9d91-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="c9d91-109"><a name="dataset"></a>NYC 計程車車程資料集說明</span><span class="sxs-lookup"><span data-stu-id="c9d91-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="c9d91-110">hello NYC 計程車路線資料約 20 GB 的壓縮以逗號分隔值 (CSV) 檔案 (~ 48 GB 未壓縮)，可包含多個 173 百萬個個別的往返和 hello fares 支付每往返作業。</span><span class="sxs-lookup"><span data-stu-id="c9d91-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="c9d91-111">每個往返記錄包括 hello 收取和下車位置和時間、 匿名的 hack (driver) 授權編號和 medallion (計程車的唯一 id) 數目。</span><span class="sxs-lookup"><span data-stu-id="c9d91-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="c9d91-112">hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9d91-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="c9d91-113">hello 'trip_data' CSV 檔案包含路線詳細資料，例如乘客、 收取和 dropoff 點數目、 路線持續時間，以及路線長度。</span><span class="sxs-lookup"><span data-stu-id="c9d91-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="c9d91-114">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="c9d91-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="c9d91-115">hello 'trip_fare' CSV 檔案包含 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="c9d91-116">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="c9d91-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="c9d91-117">hello 唯一索引鍵 toojoin 路線\_資料和路線\_價位組成 hello 欄位： medallion 具 「 可回復\_授權與收取\_日期時間。</span><span class="sxs-lookup"><span data-stu-id="c9d91-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="c9d91-118">tooget 所有 hello 詳細資料相關的 tooa 特定路線，它是具有三個索引鍵的足夠 toojoin: hello"medallion"，"hack\_授權 」 和 「 收取\_datetime"。</span><span class="sxs-lookup"><span data-stu-id="c9d91-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="c9d91-119">當我們將它們儲存成 Hive 資料表稍後我們將描述 hello 資料的其他一些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="c9d91-120"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="c9d91-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="c9d91-121">當處理資料時，判斷 hello 種類的預測，您想要根據其分析的 toomake 有助於釐清您的程序中，您將需要 tooinclude hello 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="c9d91-122">以下是三個預測的問題，我們解決其編寫根據 hello 這個逐步解說中的範例*提示\_量*:</span><span class="sxs-lookup"><span data-stu-id="c9d91-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="c9d91-123">**二元分類**：預測是否已支付某趟車程的小費，例如大於美金 $0 元的 tip\_amount 為正面範例，而等於美金 $0 元的 tip\_amount 為負面範例。</span><span class="sxs-lookup"><span data-stu-id="c9d91-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="c9d91-124">**多級分類**: hello 路線支付 toopredict hello 範圍的提示數量。</span><span class="sxs-lookup"><span data-stu-id="c9d91-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="c9d91-125">我們將 hello*提示\_量*到五個紙匣或類別：</span><span class="sxs-lookup"><span data-stu-id="c9d91-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="c9d91-126">**迴歸工作**: hello 提示 toopredict hello 數量支付路線。</span><span class="sxs-lookup"><span data-stu-id="c9d91-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="c9d91-127"><a name="setup"></a>設定進階分析的 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="c9d91-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-128">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-129">您可以採取三個步驟，為利用 HDInsight 叢集的進階分析設定 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="c9d91-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="c9d91-130">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)：這個儲存體帳戶是用來將資料儲存在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="c9d91-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="c9d91-131">用於 HDInsight 叢集的 hello 資料也位於此處。</span><span class="sxs-lookup"><span data-stu-id="c9d91-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="c9d91-132">[自訂 Azure HDInsight Hadoop 叢集以提供 hello 進階分析程序和技術](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="c9d91-133">這個步驟會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="c9d91-134">有兩個重要步驟 tooremember 時自訂您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="c9d91-135">請記住 toolink hello 儲存體帳戶建立它時，與您的 HDInsight 叢集的步驟 1 中建立。</span><span class="sxs-lookup"><span data-stu-id="c9d91-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="c9d91-136">這個儲存體帳戶是使用的 tooaccess 處理 hello 叢集內的資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="c9d91-137">建立 hello 叢集之後，啟用 遠端存取 toohello 叢集前端節點 hello。</span><span class="sxs-lookup"><span data-stu-id="c9d91-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="c9d91-138">瀏覽 toohello**組態**索引標籤上，按一下 **啟用遠端**。</span><span class="sxs-lookup"><span data-stu-id="c9d91-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="c9d91-139">此步驟中指定遠端登入所用的 hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="c9d91-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="c9d91-140">[建立 Azure 機器學習工作區](machine-learning-create-workspace.md)： 此 Azure 機器學習工作區是使用的 toobuild 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="c9d91-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="c9d91-141">這項工作已獲得解決，完成初始資料探索之後，並向使用 hello HDInsight 叢集的取樣。</span><span class="sxs-lookup"><span data-stu-id="c9d91-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="c9d91-142"><a name="getdata"></a>從公用的來源取得 hello 資料</span><span class="sxs-lookup"><span data-stu-id="c9d91-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-143">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-144">tooget hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)從公用位置的資料集，您可以使用任何 hello 方法中所述[從 Azure Blob 儲存體移動資料 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 資料 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="c9d91-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="c9d91-145">這裡我們將描述如何使用 AzCopy tootransfer hello 檔案包含的資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="c9d91-146">toodownload 並安裝 AzCopy 遵循 hello 指示[開始使用 AzCopy 命令列公用程式的 hello](../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="c9d91-147">命令提示字元 視窗中，發出下列的 AzCopy 命令、 取代 hello *< path_to_data_folder >*與 hello 所需的目的地：</span><span class="sxs-lookup"><span data-stu-id="c9d91-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="c9d91-148">Hello 複製完成時，總共 24 zip 檔案會位於 hello 資料資料夾中選擇。</span><span class="sxs-lookup"><span data-stu-id="c9d91-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="c9d91-149">解壓縮下載的 hello 檔案 toohello 本機電腦上相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="c9d91-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="c9d91-150">記下 hello hello 未壓縮檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c9d91-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="c9d91-151">這個資料夾將會參考的 tooas hello *< 路徑\_至\_unzipped_data\_檔案\>*是後面。</span><span class="sxs-lookup"><span data-stu-id="c9d91-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="c9d91-152"><a name="upload"></a>上傳 Azure HDInsight Hadoop 叢集中的 hello 資料 toohello 預設容器</span><span class="sxs-lookup"><span data-stu-id="c9d91-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-153">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-154">在 hello 下列的 AzCopy 命令，會取代 hello 遵循 hello 實際值來建立 hello Hadoop 叢集時，您所指定的參數，並解壓縮 hello 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="c9d91-155">***&#60; path_to_data_folder >*** hello 目錄 （以及路徑） 包含 hello 解壓縮資料檔案在電腦上</span><span class="sxs-lookup"><span data-stu-id="c9d91-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="c9d91-156">***&#60; Hadoop 叢集的儲存體帳戶名稱 >*** hello 與您的 HDInsight 叢集相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c9d91-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="c9d91-157">***&#60; Hadoop 叢集的預設容器 >*** hello 叢集所使用的預設容器。</span><span class="sxs-lookup"><span data-stu-id="c9d91-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="c9d91-158">請注意該 hello 名稱的 hello 預設容器通常是相同的名稱，為 hello 叢集本身的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9d91-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="c9d91-159">例如，如果 hello 叢集中稱為 「 abc123.azurehdinsight.net"，hello 預設容器。 abc123</span><span class="sxs-lookup"><span data-stu-id="c9d91-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="c9d91-160">***&#60; 儲存體帳戶金鑰 >*** hello 叢集所使用的 hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d91-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="c9d91-161">從命令提示字元或在您的電腦中的 Windows PowerShell 視窗中，執行下列兩個的 AzCopy 命令 hello。</span><span class="sxs-lookup"><span data-stu-id="c9d91-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="c9d91-162">此命令會將上傳 hello 路線資料太***nyctaxitripraw***目錄中的 hello Hadoop 叢集的 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="c9d91-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="c9d91-163">此命令會將上傳 hello 價位資料太***nyctaxifareraw***目錄中的 hello Hadoop 叢集的 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="c9d91-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="c9d91-164">hello 資料現在應該在 Azure Blob 儲存體和準備 toobe 耗用 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="c9d91-165"><a name="#download-hql-files"></a>登入 hello Hadoop 叢集前端節點，並準備資料探勘分析</span><span class="sxs-lookup"><span data-stu-id="c9d91-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-166">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-167">tooaccess hello 叢集前端節點 hello 探勘測試的資料分析的時間和停機的 hello 資料取樣，請遵循 「 hello 程序中所述[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="c9d91-168">在本逐步解說中，我們主要是使用撰寫的查詢[Hive](https://hive.apache.org/)，類似 SQL 的查詢語言、 tooperform 初步資料瀏覽。</span><span class="sxs-lookup"><span data-stu-id="c9d91-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="c9d91-169">hello Hive 查詢會儲存在.hql 檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="c9d91-170">我們再向下範例此 Azure Machine Learning 中用來建立模型的資料 toobe。</span><span class="sxs-lookup"><span data-stu-id="c9d91-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="c9d91-171">資料探勘分析 tooprepare hello 叢集，我們下載 hello.hql 檔案，其中包含 hello 相關的 Hive 指令碼從[github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa 本機目錄 (C:\temp)，hello 前端節點上的。</span><span class="sxs-lookup"><span data-stu-id="c9d91-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="c9d91-172">toodo，開啟 hello**命令提示字元**從 hello 前端節點的 hello 叢集和問題 hello 下列兩個命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="c9d91-173">這兩個命令會下載需要此逐步解說 toohello 本機目錄中的所有.hql 檔案***C:\temp &#92;*** hello 前端節點中。</span><span class="sxs-lookup"><span data-stu-id="c9d91-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="c9d91-174"><a name="#hive-db-tables"></a>建立依月份分割的 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="c9d91-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-175">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-176">我們已經準備好 toocreate Hive 資料表我們 NYC 計程車資料集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="c9d91-177">在 hello hello Hadoop 叢集的前端節點，開啟 hello ***Hadoop 命令列***hello 桌面的 hello 前端節點，且輸入 hello 命令輸入 hello Hive 目錄</span><span class="sxs-lookup"><span data-stu-id="c9d91-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="c9d91-178">**在此逐步解說中執行所有的登錄區命令，從上述 Hive bin hello / 目錄提示字元。如此可自動處理路徑相關問題。我們使用 hello 詞彙"Hive 目錄 prompt"，"Hive bin / 目錄提示字元 」，和交換在本逐步解說中的 「 Hadoop 命令列 」。**</span><span class="sxs-lookup"><span data-stu-id="c9d91-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="c9d91-179">Hello Hive 目錄提示字元中，輸入下列命令在 hello 前端節點 toosubmit hello Hive 查詢 toocreate Hive 資料庫和資料表的 Hadoop 命令列的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9d91-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="c9d91-180">以下是 hello hello 內容***C:\temp\sample\_hive\_建立\_db\_和\_tables.hql***檔案會建立登錄區資料庫***nyctaxidb***和資料表***路線***和***價位***。</span><span class="sxs-lookup"><span data-stu-id="c9d91-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="c9d91-181">這個 Hive 指令碼會建立兩個資料表：</span><span class="sxs-lookup"><span data-stu-id="c9d91-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="c9d91-182">hello 「 往返 」 資料表包含 （驅動程式詳細資料、 收取的時間、 旅行距離和時間） 的每個賽車路線詳細資料</span><span class="sxs-lookup"><span data-stu-id="c9d91-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="c9d91-183">hello"價位 」 資料表包含價位詳細資料 （價位量、 提示量、 tolls 和 surcharges）。</span><span class="sxs-lookup"><span data-stu-id="c9d91-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="c9d91-184">如果您需要這些程序的任何其他協助，或想 tooinvestigate 替代項目，請參閱 hello 節[提交 Hive 查詢直接從 hello Hadoop 命令列](machine-learning-data-science-move-hive-tables.md#submit)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="c9d91-185"><a name="#load-data"></a>載入資料 tooHive 資料表資料分割</span><span class="sxs-lookup"><span data-stu-id="c9d91-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-186">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-187">hello NYC 計程車資料集有自然的資料分割以月，我們使用 tooenable 處理和查詢的速度。</span><span class="sxs-lookup"><span data-stu-id="c9d91-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="c9d91-188">hello 下列 PowerShell 命令 (從 hello Hive 目錄使用 hello 發出**Hadoop 命令列**) 載入 toohello"路線 」 及 「 價位"Hive 資料表，根據月份分割。</span><span class="sxs-lookup"><span data-stu-id="c9d91-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="c9d91-189">hello*範例\_hive\_載入\_資料\_由\_partitions.hql*檔案包含下列 hello**載入**命令。</span><span class="sxs-lookup"><span data-stu-id="c9d91-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="c9d91-190">請注意一些我們在此使用 hello 瀏覽處理序中的 Hive 查詢包含查詢只是單一分割，或者只使用幾個資料分割。</span><span class="sxs-lookup"><span data-stu-id="c9d91-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="c9d91-191">但是，這些查詢可以執行跨 hello 整個資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="c9d91-192"><a name="#show-db"></a>顯示資料庫中 hello HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="c9d91-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="c9d91-193">所建立的 HDInsight Hadoop 叢集內 hello Hadoop 命令列視窗中，執行下列命令 Hadoop 命令列中的 hello tooshow hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="c9d91-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="c9d91-194"><a name="#show-tables"></a>顯示 hello nyctaxidb 資料庫中的 hello Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="c9d91-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="c9d91-195">在 hello nyctaxidb 資料庫，請執行下列命令 Hadoop 命令列中的 hello tooshow hello 資料表：</span><span class="sxs-lookup"><span data-stu-id="c9d91-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="c9d91-196">我們可以確認 hello 資料表已分割藉由發出下列 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="c9d91-197">hello 預期輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9d91-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="c9d91-198">同樣地，我們可以確定該 hello 價位表分割藉由發出下列 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="c9d91-199">hello 預期輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="c9d91-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="c9d91-200"><a name="#explore-hive"></a>Hive 中的資料探索和特徵工程</span><span class="sxs-lookup"><span data-stu-id="c9d91-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-201">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-202">hello 資料瀏覽和功能的資料載入至 hello Hive 資料表可以使用 Hive 查詢來達成的 hello 工程工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="c9d91-203">以下是我們將在本節中逐步引導您執行的這類工作範例：</span><span class="sxs-lookup"><span data-stu-id="c9d91-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="c9d91-204">檢視兩個資料表中的 hello 前 10 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="c9d91-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="c9d91-205">在變動的時間範圍中探索數個欄位的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="c9d91-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="c9d91-206">調查 hello 經度和緯度欄位的資料品質。</span><span class="sxs-lookup"><span data-stu-id="c9d91-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="c9d91-207">產生二進位和多級分類標籤根據 hello**提示\_量**。</span><span class="sxs-lookup"><span data-stu-id="c9d91-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="c9d91-208">產生功能，藉由計算 hello 直接的旅行距離。</span><span class="sxs-lookup"><span data-stu-id="c9d91-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="c9d91-209">瀏覽： 檢視資料表旅程中的 hello 前 10 筆記錄</span><span class="sxs-lookup"><span data-stu-id="c9d91-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-210">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-211">hello 資料看起來像 toosee，我們會檢查每個資料表中的 10 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="c9d91-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="c9d91-212">執行 hello hello Hadoop 命令列主控台 tooinspect hello 記錄中的 hello Hive 目錄提示字元中的個別下列兩個查詢。</span><span class="sxs-lookup"><span data-stu-id="c9d91-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="c9d91-213">tooget hello 前 10 筆記錄 hello 資料表 」 行程"hello 第一個月中：</span><span class="sxs-lookup"><span data-stu-id="c9d91-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="c9d91-214">tooget hello 前 10 個資料表中的記錄 hello"再見"hello 從第一個月：</span><span class="sxs-lookup"><span data-stu-id="c9d91-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="c9d91-215">它通常是很有用的 toosave hello 記錄 tooa 檔方便檢視。</span><span class="sxs-lookup"><span data-stu-id="c9d91-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="c9d91-216">上述查詢小幅變更 toohello 完成這項操作：</span><span class="sxs-lookup"><span data-stu-id="c9d91-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="c9d91-217">瀏覽： 檢視每個 hello 12 個資料分割中的 hello 記錄數目</span><span class="sxs-lookup"><span data-stu-id="c9d91-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-218">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-219">感興趣的是如何 hello 的往返次數變化期間 hello 日曆年度的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9d91-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="c9d91-220">依月份群組可讓我們 toosee 的行程此分佈是什麼樣子。</span><span class="sxs-lookup"><span data-stu-id="c9d91-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="c9d91-221">這會提供 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="c9d91-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="c9d91-222">在這裡，hello 第一個資料行是 hello 的月份，而 hello 該月份的第二種是 hello 的往返次數。</span><span class="sxs-lookup"><span data-stu-id="c9d91-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="c9d91-223">我們也可以藉由發出下列命令，在提示字元中 Hive 目錄 hello hello 我們路線資料集中計數 hello 的總記錄數。</span><span class="sxs-lookup"><span data-stu-id="c9d91-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="c9d91-224">這會產生：</span><span class="sxs-lookup"><span data-stu-id="c9d91-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="c9d91-225">使用命令類似 toothose 所示為 hello 路線的資料集，我們可以發出 Hive 查詢從 hello 價位資料集 toovalidate hello 的記錄數目的 hello Hive 目錄提示字元。</span><span class="sxs-lookup"><span data-stu-id="c9d91-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="c9d91-226">這會提供 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="c9d91-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="c9d91-227">請注意，hello 完全相同的往返次數每個月就會傳回兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="c9d91-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="c9d91-228">這會提供 hello 第一個驗證該 hello 正確地載入資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="c9d91-229">計算 hello 的總記錄數 hello 價位資料集中，才可以使用下面的 hello Hive 目錄提示字元中的 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="c9d91-230">這會產生：</span><span class="sxs-lookup"><span data-stu-id="c9d91-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="c9d91-231">也 hello hello 的總記錄數兩個資料表中相同。</span><span class="sxs-lookup"><span data-stu-id="c9d91-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="c9d91-232">這會提供第二個驗證該 hello 正確地載入資料。</span><span class="sxs-lookup"><span data-stu-id="c9d91-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="c9d91-233">探索：依據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="c9d91-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-234">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-235">這個範例會在給定的時間間隔內識別超過 100 個往返 hello medallion （計程車數字）。</span><span class="sxs-lookup"><span data-stu-id="c9d91-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="c9d91-236">從 hello hello 查詢優點分割資料表存取，因為它由 hello 分割變數所**月份**。</span><span class="sxs-lookup"><span data-stu-id="c9d91-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="c9d91-237">hello 查詢結果會以撰寫 tooa 本機檔案 queryoutput.tsv `C:\temp` hello 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="c9d91-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="c9d91-238">以下是 hello 內容*範例\_hive\_路線\_計數\_由\_medallion.hql*進行檢查的檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="c9d91-239">hello medallion hello NYC 計程車資料集內識別的唯一封包。</span><span class="sxs-lookup"><span data-stu-id="c9d91-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="c9d91-240">我們可以詢問哪些計程車在特定時段超過特定的車程數目，以識別哪些計程車「忙碌中」。</span><span class="sxs-lookup"><span data-stu-id="c9d91-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="c9d91-241">hello 下列範例會識別在 hello 中前三個月，進行超過一百往返的封包，並儲存 hello 查詢結果 tooa 本機檔案，C:\temp\queryoutput.tsv。</span><span class="sxs-lookup"><span data-stu-id="c9d91-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="c9d91-242">以下是 hello 內容*範例\_hive\_路線\_計數\_由\_medallion.hql*進行檢查的檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="c9d91-243">從 hello hive 控制檔目錄提示字元中，下列的問題 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="c9d91-244">探索：依據 medallion 和 hack_license 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="c9d91-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-245">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-246">當瀏覽資料集，我們經常想 tooexamine hello 次數 co-群組的值。</span><span class="sxs-lookup"><span data-stu-id="c9d91-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="c9d91-247">本章節將提供範例，此作業對於擷取 toodo 如何與驅動程式。</span><span class="sxs-lookup"><span data-stu-id="c9d91-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="c9d91-248">hello*範例\_hive\_路線\_計數\_由\_medallion\_license.hql* "medallion"和"hack_license"上設定的 hello 價位資料的檔案群組與每個組合的傳回計數。</span><span class="sxs-lookup"><span data-stu-id="c9d91-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="c9d91-249">以下是其內容。</span><span class="sxs-lookup"><span data-stu-id="c9d91-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="c9d91-250">這個查詢會依車程數目的遞減順序，傳回計程車和特定駕駛的組合。</span><span class="sxs-lookup"><span data-stu-id="c9d91-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="c9d91-251">從 hello hive 控制檔目錄提示字元，請執行：</span><span class="sxs-lookup"><span data-stu-id="c9d91-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="c9d91-252">hello 查詢結果會寫入 C:\temp\queryoutput.tsv tooa 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="c9d91-253">探索：藉由檢查無效的經度/緯度記錄來評估資料品質</span><span class="sxs-lookup"><span data-stu-id="c9d91-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-254">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-255">資料探勘分析的常見目標是 tooweed 出無效或不正確的記錄。</span><span class="sxs-lookup"><span data-stu-id="c9d91-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="c9d91-256">hello 本節中的範例會決定是否可以是 hello 經度或緯度的欄位包含遠超出 hello NYC 區域的值。</span><span class="sxs-lookup"><span data-stu-id="c9d91-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="c9d91-257">因為這是可能這類記錄都有錯誤的經度-緯度值，我們想要從 toobe 任何資料模型所用的 tooeliminate。</span><span class="sxs-lookup"><span data-stu-id="c9d91-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="c9d91-258">以下是 hello 內容*範例\_hive\_品質\_assessment.hql*進行檢查的檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="c9d91-259">從 hello hive 控制檔目錄提示字元，請執行：</span><span class="sxs-lookup"><span data-stu-id="c9d91-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="c9d91-260">hello *-S*包含在此命令的引數會抑制 hello 狀態螢幕列印成品的 hello Hive Map/Reduce 作業。</span><span class="sxs-lookup"><span data-stu-id="c9d91-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="c9d91-261">這非常有用，因為它會讓 hello 螢幕列印 hello 的 Hive 查詢的輸出更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="c9d91-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="c9d91-262">探索：車程小費的二元類別分佈</span><span class="sxs-lookup"><span data-stu-id="c9d91-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-263">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-264">Hello 中所述的 hello 二元分類問題[預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 區段中，很有用的 tooknow 是否或不指定提示。</span><span class="sxs-lookup"><span data-stu-id="c9d91-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="c9d91-265">小費是二元分佈：</span><span class="sxs-lookup"><span data-stu-id="c9d91-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="c9d91-266">tip given(Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="c9d91-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="c9d91-267">no tip (Class 0, tip\_amount = $0)</span><span class="sxs-lookup"><span data-stu-id="c9d91-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="c9d91-268">hello*範例\_hive\_傾斜\_frequencies.hql*檔案如下所示的做法。</span><span class="sxs-lookup"><span data-stu-id="c9d91-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="c9d91-269">從 hello hive 控制檔目錄提示字元，請執行：</span><span class="sxs-lookup"><span data-stu-id="c9d91-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="c9d91-270">瀏覽： Hello 多級設定中的類別分佈</span><span class="sxs-lookup"><span data-stu-id="c9d91-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-271">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-272">Hello 中所述的 hello 多級分類問題[預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks)此資料集也借用本身 tooa 自然的分類，其中，我們都希望 toopredict hello 數量指定 hello 提示 > 一節。</span><span class="sxs-lookup"><span data-stu-id="c9d91-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="c9d91-273">我們可以使用分類收納 toodefine 提示範圍 hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="c9d91-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="c9d91-274">tooget hello hello 類別分配不同提示的範圍，我們使用 hello*範例\_hive\_提示\_範圍\_frequencies.hql*檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="c9d91-275">以下是其內容。</span><span class="sxs-lookup"><span data-stu-id="c9d91-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="c9d91-276">執行下列命令從 Hadoop 命令列主控台 hello:</span><span class="sxs-lookup"><span data-stu-id="c9d91-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="c9d91-277">探索：計算兩個經度-緯度位置之間的直線距離</span><span class="sxs-lookup"><span data-stu-id="c9d91-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-278">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-279">擁有 hello 直接距離的量值可讓我們 toofind hello 不一致，它與 hello 之間出實際成為距離。</span><span class="sxs-lookup"><span data-stu-id="c9d91-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="c9d91-280">我們藉由指出，旅客可能會小於激勵這項功能可能工具提示 」 如果它們找出該 hello 驅動程式具有刻意它們所採取的較長的路由。</span><span class="sxs-lookup"><span data-stu-id="c9d91-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="c9d91-281">實際的旅行距離與 hello toosee hello 比較[Haversine 距離](http://en.wikipedia.org/wiki/Haversine_formula)經度-緯度兩點之間 （hello"優越 circle"距離），我們使用可用的 hello 三角函式內登錄區，因此：</span><span class="sxs-lookup"><span data-stu-id="c9d91-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="c9d91-282">在上述查詢 hello，R 是 hello 半徑 hello 地球英里，而 pi 是轉換的 tooradians。</span><span class="sxs-lookup"><span data-stu-id="c9d91-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="c9d91-283">請注意，hello 經度-緯度點為遠離 hello NYC 區域的 篩選 」 tooremove 值。</span><span class="sxs-lookup"><span data-stu-id="c9d91-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="c9d91-284">在此情況下，我們會撰寫我們稱為 「 queryoutputdir"的結果 tooa 目錄。</span><span class="sxs-lookup"><span data-stu-id="c9d91-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="c9d91-285">hello 順序如下所示的命令的輸出目錄中，會先建立，並執行 hello Hive 命令。</span><span class="sxs-lookup"><span data-stu-id="c9d91-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="c9d91-286">從 hello hive 控制檔目錄提示字元，請執行：</span><span class="sxs-lookup"><span data-stu-id="c9d91-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="c9d91-287">hello 查詢結果會寫入 too9 Azure blob ***queryoutputdir/000000\_0***太***queryoutputdir/000008\_0*** hello hello Hadoop 叢集的預設容器下。</span><span class="sxs-lookup"><span data-stu-id="c9d91-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="c9d91-288">toosee hello 的 hello 個別 blob 的大小，我們要執行 hello hello Hive 目錄提示字元中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="c9d91-289">指定的檔案，toosee hello 內容說 000000\_0，我們使用 Hadoop 的`copyToLocal`命令，因此。</span><span class="sxs-lookup"><span data-stu-id="c9d91-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="c9d91-290">遇到大型檔案，`copyToLocal` 可能會很慢，因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="c9d91-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="c9d91-291">包含此資料位於 Azure blob 的主要優點是，我們可能會瀏覽使用 hello Azure Machine Learning 中的 hello 資料[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="c9d91-292"><a name="#downsample"></a>在 Azure Machine Learning 中縮小取樣和建置模型</span><span class="sxs-lookup"><span data-stu-id="c9d91-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="c9d91-293">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="c9d91-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c9d91-294">Hello 探勘測試的資料分析階段之後，我們現在是準備 toodown 範例 hello 資料來建立 Azure Machine Learning 中的模型。</span><span class="sxs-lookup"><span data-stu-id="c9d91-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="c9d91-295">在本節中，我們會示範如何 toouse Hive 查詢 toodown 範例 hello 資料，然後從 hello 存取[匯入資料][ import-data] Azure Machine Learning 中的模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="c9d91-296">向下取樣 hello 資料</span><span class="sxs-lookup"><span data-stu-id="c9d91-296">Down sampling hello data</span></span>
<span data-ttu-id="c9d91-297">這個程序包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="c9d91-297">There are two steps in this procedure.</span></span> <span data-ttu-id="c9d91-298">我們第一次加入 hello **nyctaxidb.trip**和**nyctaxidb.fare**上會出現在所有記錄中的三個索引鍵的資料表:"medallion"，"hack\_授權 」，和 「 收取\_datetime"。</span><span class="sxs-lookup"><span data-stu-id="c9d91-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="c9d91-299">接著產生二元分類標籤 **tipped** 和多元分類標籤 **tip\_class**。</span><span class="sxs-lookup"><span data-stu-id="c9d91-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="c9d91-300">取樣的資料，直接從 hello 向 toobe 無法 toouse hello[匯入資料][ import-data]模組在 Azure Machine Learning 中，就需要 toostore hello 結果的查詢 tooan 內部的 Hive 資料表上方的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9d91-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="c9d91-301">在以下，我們會建立內部的 Hive 資料表，並聯結 hello 上下取樣的資料填入它的內容。</span><span class="sxs-lookup"><span data-stu-id="c9d91-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="c9d91-302">hello 查詢適用於標準 Hive 函式直接 toogenerate hello 當日小時、 一週的年、 週間日 （1 代表星期一和 7 代表星期日） 從 hello"收取\_日期時間 」 欄位，以及 hello 直接 hello 收取和距離 dropoff位置。</span><span class="sxs-lookup"><span data-stu-id="c9d91-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="c9d91-303">使用者可以參考太[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF)的這類函式的完整清單。</span><span class="sxs-lookup"><span data-stu-id="c9d91-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="c9d91-304">hello 查詢，然後向下範例 hello 資料，以便 hello 查詢結果可以納入 hello Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="c9d91-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="c9d91-305">只有約 1%的 hello 原始資料集匯入 hello Studio。</span><span class="sxs-lookup"><span data-stu-id="c9d91-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="c9d91-306">下面是 hello 內容*範例\_hive\_準備\_如\_aml\_full.hql*建置 Azure Machine Learning 中的模型來準備資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="c9d91-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="c9d91-307">此查詢中的，從 hello Hive 目錄提示 toorun:</span><span class="sxs-lookup"><span data-stu-id="c9d91-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="c9d91-308">我們現在有內部的資料表使用 hello 可存取的 「 nyctaxidb.nyctaxi_downsampled_dataset"[匯入資料][ import-data]從 Azure 機器學習模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="c9d91-309">此外，我們可能使用這個資料集來建置機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="c9d91-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="c9d91-310">Azure Machine Learning tooaccess hello 向取樣資料中使用 hello 資料匯入模組</span><span class="sxs-lookup"><span data-stu-id="c9d91-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="c9d91-311">為發行在 hello 的 Hive 查詢的必要條件[匯入資料][ import-data] Azure 機器學習模組中的，我們需要存取 tooan Azure Machine Learning 工作區，並存取 hello toohello 認證叢集和與其相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9d91-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="c9d91-312">部分詳細資料上 hello[匯入資料][ import-data]模組和 hello 參數 tooinput:</span><span class="sxs-lookup"><span data-stu-id="c9d91-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="c9d91-313">**HCatalog 伺服器 URI**： 如果 hello 叢集名稱 abc123，則這只是： https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="c9d91-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="c9d91-314">**Hadoop 使用者帳戶名稱**: hello hello 叢集針對所選的使用者名稱 (**不**hello 遠端存取使用者名稱)</span><span class="sxs-lookup"><span data-stu-id="c9d91-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="c9d91-315">**Hadoop ser 帳戶密碼**: hello 叢集所選擇的 hello 密碼 (**不**hello 遠端存取密碼)</span><span class="sxs-lookup"><span data-stu-id="c9d91-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="c9d91-316">**輸出資料的位置**： 這選擇 toobe Azure。</span><span class="sxs-lookup"><span data-stu-id="c9d91-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="c9d91-317">**Azure 儲存體帳戶名稱**: hello 與 hello 叢集相關聯的預設儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c9d91-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="c9d91-318">**Azure 容器名稱**： 這是 hello hello 叢集的預設容器名稱，通常是相同 hello 與 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="c9d91-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="c9d91-319">如果叢集為 "abc123"，即為 abc123。</span><span class="sxs-lookup"><span data-stu-id="c9d91-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9d91-320">**我們希望使用 hello tooquery 任何資料表[匯入資料][ import-data] Azure Machine Learning 中的模組必須是內部的資料表。**</span><span class="sxs-lookup"><span data-stu-id="c9d91-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="c9d91-321">以下是判斷資料庫 D.db 中的資料表 T 是否為內部資料表的秘訣。</span><span class="sxs-lookup"><span data-stu-id="c9d91-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="c9d91-322">從 hello hive 控制檔目錄提示字元中，問題 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="c9d91-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="c9d91-323">如果 hello 資料表為內部的資料表，且它會擴展，其內容必須顯示在這裡。</span><span class="sxs-lookup"><span data-stu-id="c9d91-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="c9d91-324">另一個方式 toodetermine 資料表是否為內部的資料表為 toouse hello Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="c9d91-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="c9d91-325">使用它的 hello 叢集 toonavigate toohello 預設容器名稱，然後篩選 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="c9d91-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="c9d91-326">如果 hello 資料表和其內容顯示，這可確認它是內部的資料表。</span><span class="sxs-lookup"><span data-stu-id="c9d91-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="c9d91-327">以下是建立的快照 hello Hive 查詢並 hello[匯入資料][ import-data]模組：</span><span class="sxs-lookup"><span data-stu-id="c9d91-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![匯入資料模組的 Hive 查詢](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="c9d91-329">請注意，因為我們 hello 預設容器中的取樣的資料所在的清單中，從 Azure Machine Learning hello 產生 Hive 查詢非常簡單只是 「 選取 * 從 nyctaxidb.nyctaxi\_downsampled\_資料 」。</span><span class="sxs-lookup"><span data-stu-id="c9d91-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="c9d91-330">hello 資料集現在做 hello 起點來建立機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="c9d91-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="c9d91-331"><a name="mlmodel"></a>在 Azure Machine Learning 中建置模型</span><span class="sxs-lookup"><span data-stu-id="c9d91-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="c9d91-332">我們現在是無法 tooproceed toomodel 建置和中的模型部署[Azure Machine Learning](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="c9d91-333">hello 資料已準備好我們 toouse 解決上述 hello 預測問題：</span><span class="sxs-lookup"><span data-stu-id="c9d91-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="c9d91-334">**1.二元分類**: toopredict 提示是否支付路線。</span><span class="sxs-lookup"><span data-stu-id="c9d91-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="c9d91-335">**已使用學習者：** 二元羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="c9d91-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="c9d91-336">a.</span><span class="sxs-lookup"><span data-stu-id="c9d91-336">a.</span></span> <span data-ttu-id="c9d91-337">對於這個問題，我們的目標 (或類別) 標籤是 "tipped"。</span><span class="sxs-lookup"><span data-stu-id="c9d91-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="c9d91-338">縮小取樣的原始資料集有幾個資料行會顯示這個分類實驗目標。</span><span class="sxs-lookup"><span data-stu-id="c9d91-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="c9d91-339">特別是： 提示\_類別中，提示\_數量，與總\_金額不是可在測試時間的 hello 目標標籤的顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="c9d91-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="c9d91-340">我們將不考慮使用 hello 移除這些資料行[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c9d91-341">hello 快照下方會顯示我們實驗 toopredict 提示支付給定的路線。</span><span class="sxs-lookup"><span data-stu-id="c9d91-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="c9d91-343">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9d91-343">b.</span></span> <span data-ttu-id="c9d91-344">對於這項實驗，我們的目標標籤分佈大約是 1:1。</span><span class="sxs-lookup"><span data-stu-id="c9d91-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="c9d91-345">hello 快照下方顯示 hello 分佈 hello 二元分類問題的秘訣類別標籤。</span><span class="sxs-lookup"><span data-stu-id="c9d91-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![類別標籤的分佈](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="c9d91-347">如此一來，我們取得 0.987 的 AUC hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="c9d91-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![AUC 值](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="c9d91-349">**2.多級分類**: hello 來回傳送時，先前使用 hello 付費的提示數量 toopredict hello 範圍定義的類別。</span><span class="sxs-lookup"><span data-stu-id="c9d91-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="c9d91-350">**已使用學習者：** 多元羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="c9d91-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="c9d91-351">a.</span><span class="sxs-lookup"><span data-stu-id="c9d91-351">a.</span></span> <span data-ttu-id="c9d91-352">對於這個問題，我們的目標 (或類別) 標籤是 "tip\_class"，可能採用五個值 (0、1、2、3、4) 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="c9d91-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="c9d91-353">如同 hello 二元分類的情況，我們有此實驗目標流失的幾個資料行。</span><span class="sxs-lookup"><span data-stu-id="c9d91-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="c9d91-354">特別是： 傾斜，提示\_總數量\_金額不是可在測試時間的 hello 目標標籤的顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="c9d91-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="c9d91-355">我們會移除這些資料行使用 hello[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c9d91-356">hello 的快照集所示的紙匣中的秘訣是可能 toofall 我們實驗 toopredict (類別 0： 提示 = $0，1 類別： 提示 > $0 和秘訣 < = $5，類別 2： 提示 > $5 和秘訣 < = $10、 等級 3： 提示 > $10 到提示 < = $20類別 4： 提示 > $20)</span><span class="sxs-lookup"><span data-stu-id="c9d91-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="c9d91-358">現在會顯示實際的測試類別分佈。</span><span class="sxs-lookup"><span data-stu-id="c9d91-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="c9d91-359">我們看到普遍類別 0 和 1 類別時，hello 其他類別少。</span><span class="sxs-lookup"><span data-stu-id="c9d91-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![測試類別分佈](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="c9d91-361">b.</span><span class="sxs-lookup"><span data-stu-id="c9d91-361">b.</span></span> <span data-ttu-id="c9d91-362">此實驗中，我們會使用混淆矩陣 toolook 在我們的預測精確度。</span><span class="sxs-lookup"><span data-stu-id="c9d91-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="c9d91-363">如下所示。</span><span class="sxs-lookup"><span data-stu-id="c9d91-363">This is shown below.</span></span>

![混淆矩陣](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="c9d91-365">請注意，雖然 hello 普遍類別上我們類別精確度是很好，hello 模型並不會很好的 「 學習 」 hello 少數類別上。</span><span class="sxs-lookup"><span data-stu-id="c9d91-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="c9d91-366">**3.迴歸工作**: toopredict hello 數量提示支付路線。</span><span class="sxs-lookup"><span data-stu-id="c9d91-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="c9d91-367">**已使用學習者：** 推進式決策樹</span><span class="sxs-lookup"><span data-stu-id="c9d91-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="c9d91-368">a.</span><span class="sxs-lookup"><span data-stu-id="c9d91-368">a.</span></span> <span data-ttu-id="c9d91-369">對於這個問題，我們的目標 (或類別) 標籤是 "tip\_amount"。</span><span class="sxs-lookup"><span data-stu-id="c9d91-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="c9d91-370">我們的目標流失在此情況下，： 傾斜，提示\_類別細明體，總\_量; 所有這些變數會顯示 hello 通常無法使用，在測試時間的提示數量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c9d91-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="c9d91-371">我們會移除這些資料行使用 hello[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="c9d91-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c9d91-372">hello 快照 belows 顯示我們實驗 toopredict hello 的數量 hello 提供提示。</span><span class="sxs-lookup"><span data-stu-id="c9d91-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="c9d91-374">b.</span><span class="sxs-lookup"><span data-stu-id="c9d91-374">b.</span></span> <span data-ttu-id="c9d91-375">針對迴歸問題，我們可以藉由查看 hello 預測中的 hello 平方錯誤測量 hello 我們預測的精確度，當做、 hello 判斷的係數和 hello 類似。</span><span class="sxs-lookup"><span data-stu-id="c9d91-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="c9d91-376">以下將進行示範。</span><span class="sxs-lookup"><span data-stu-id="c9d91-376">We show these below.</span></span>

![預測統計資料](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="c9d91-378">我們會看到有關 hello 判斷的係數是 0.709，意味著大約 71 %hello 差異的說明由我們模型的係數。</span><span class="sxs-lookup"><span data-stu-id="c9d91-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9d91-379">深入了解 Azure Machine Learning toolearn 以及 tooaccess 並使用它，請參閱太[什麼是機器學習？](machine-learning-what-is-machine-learning.md)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="c9d91-380">與 Azure Machine Learning 中的機器學習實驗的一大堆矔菛非常實用的資源為 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/)。</span><span class="sxs-lookup"><span data-stu-id="c9d91-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="c9d91-381">hello 圖庫涵蓋實驗的一系列，並且提供 Azure Machine Learning 的 hello 各種功能的完整介紹。</span><span class="sxs-lookup"><span data-stu-id="c9d91-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="c9d91-382">授權資訊</span><span class="sxs-lookup"><span data-stu-id="c9d91-382">License Information</span></span>
<span data-ttu-id="c9d91-383">此範例逐步解說和其隨附的指令碼由共用 Microsoft hello MIT 授權。</span><span class="sxs-lookup"><span data-stu-id="c9d91-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="c9d91-384">請 hello 目錄中的 hello 範例程式碼在 GitHub 上如需詳細資訊，在檢查 hello LICENSE.txt 檔。</span><span class="sxs-lookup"><span data-stu-id="c9d91-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="c9d91-385">參考</span><span class="sxs-lookup"><span data-stu-id="c9d91-385">References</span></span>
<span data-ttu-id="c9d91-386">•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="c9d91-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="c9d91-387">•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="c9d91-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="c9d91-388">•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="c9d91-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
