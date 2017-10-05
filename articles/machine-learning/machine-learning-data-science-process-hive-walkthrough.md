---
title: "瀏覽 Hadoop 叢集中的資料，並在 Azure Machine Learning 中建立模型 | Microsoft Docs"
description: "對採用 HDInsight Hadoop 叢集來建置和部署使用公開可用資料集模型的端對端案例使用 Team Data Science Process。"
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
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="a68a4-103">Team Data Science Process 實務：使用 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="a68a4-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="a68a4-104">在這個逐步解說中，我們會在採用 [Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)的端對端案例中使用 [Team Data Science Process (TDSP)](data-science-process-overview.md)，以對 [NYC Taxi Trips (NYC 計程車車程)](http://www.andresmh.com/nyctaxitrips/) 資料集內可公開使用的資料進行儲存、探索和特徵工程設計，並縮減取樣資料。</span><span class="sxs-lookup"><span data-stu-id="a68a4-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="a68a4-105">資料的模型是使用 Azure Machine Learning 建置，以處理二元和多元分類和迴歸預測工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="a68a4-106">如需示範如何使用 HDInsight Hadoop 叢集，針對類似的案例處理更大 (1 TB) 資料集資料的逐步解說，請參閱 [Team Data Science Process - 在 1 TB 資料集上使用 Azure HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-criteo-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="a68a4-107">此外，也可以使用 1 TB 資料集，使用 IPython Notebook 來完成本逐步解說中說明的工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="a68a4-108">想要嘗試這種方法的使用者，應該查閱 [使用 Hive ODBC 連線的 Criteo 逐步解說](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 主題。</span><span class="sxs-lookup"><span data-stu-id="a68a4-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="a68a4-109"><a name="dataset"></a>NYC 計程車車程資料集說明</span><span class="sxs-lookup"><span data-stu-id="a68a4-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="a68a4-110">「NYC 計程車車程」資料大約是 20GB 以逗號分隔值 (CSV) 的壓縮檔 (未壓縮時可達 48GB)，其中包含超過 1 億 7300 萬筆個別車程及針對每趟車程支付的費用。</span><span class="sxs-lookup"><span data-stu-id="a68a4-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="a68a4-111">每趟車程記錄包括上車和下車的位置與時間、匿名的計程車司機駕照號碼，以及圓形徽章 (計程車的唯一識別碼) 號碼。</span><span class="sxs-lookup"><span data-stu-id="a68a4-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="a68a4-112">資料涵蓋 2013 年的所有車程，並且每月會在下列兩個資料集中加以提供：</span><span class="sxs-lookup"><span data-stu-id="a68a4-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="a68a4-113">'trip_data' CSV 檔案包含車程詳細資訊，例如乘客數、上車和下車地點、車程持續時間，以及車程長度。</span><span class="sxs-lookup"><span data-stu-id="a68a4-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="a68a4-114">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="a68a4-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="a68a4-115">'trip_data' CSV 檔案包含針對每趟車程所支付的費用詳細資料，例如付款類型、費用金額、附加費和稅金、小費和通行費，以及支付的總金額。</span><span class="sxs-lookup"><span data-stu-id="a68a4-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="a68a4-116">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="a68a4-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="a68a4-117">聯結 trip\_data 和 trip\_fare 的唯一索引鍵是由下列欄位組成：medallion、hack\_licence、pickup\_datetime。</span><span class="sxs-lookup"><span data-stu-id="a68a4-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="a68a4-118">若要取得特定車程的所有詳細資訊，加入下列三個索引鍵便已足夠："medallion"、"hack\_license"、"pickup\_datetime"。</span><span class="sxs-lookup"><span data-stu-id="a68a4-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="a68a4-119">稍後將這些資料儲存至 Hive 資料表時，我們將更詳細地加以說明。</span><span class="sxs-lookup"><span data-stu-id="a68a4-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="a68a4-120"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="a68a4-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="a68a4-121">處理資料時，根據分析來決定您想要進行的預測種類，有助於釐清您必須在程序中包含的工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="a68a4-122">以下是三個預測問題的範例，我們將在本逐步解說中說明哪一個構想是以 tip\_amount 為基礎：</span><span class="sxs-lookup"><span data-stu-id="a68a4-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="a68a4-123">**二元分類**：預測是否已支付某趟車程的小費，例如大於美金 $0 元的 tip\_amount 為正面範例，而等於美金 $0 元的 tip\_amount 為負面範例。</span><span class="sxs-lookup"><span data-stu-id="a68a4-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="a68a4-124">**多元分類**：預測針對該趟車程支付的小費金額範圍。</span><span class="sxs-lookup"><span data-stu-id="a68a4-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="a68a4-125">我們將 tip\_amount 分成五個分類收納組或類別：</span><span class="sxs-lookup"><span data-stu-id="a68a4-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="a68a4-126">**迴歸工作**：預測已針對某趟車程支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="a68a4-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="a68a4-127"><a name="setup"></a>設定進階分析的 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="a68a4-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-128">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-129">您可以採取三個步驟，為利用 HDInsight 叢集的進階分析設定 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="a68a4-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="a68a4-130">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)：這個儲存體帳戶是用來將資料儲存在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a68a4-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="a68a4-131">HDInsight 叢集中使用的資料也位於此處。</span><span class="sxs-lookup"><span data-stu-id="a68a4-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="a68a4-132">[針對進階分析程序和技術自訂 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="a68a4-133">這個步驟會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="a68a4-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="a68a4-134">自訂 HDInsight 叢集時應注意兩個重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="a68a4-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="a68a4-135">建立 HDInsight 叢集時，請務必將步驟 1 中建立的儲存體帳戶與您的 HDInsight 叢集連結。</span><span class="sxs-lookup"><span data-stu-id="a68a4-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="a68a4-136">這個儲存體帳戶是用來存取在叢集內處理的資料。</span><span class="sxs-lookup"><span data-stu-id="a68a4-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="a68a4-137">建立叢集之後，請對叢集的前端節點啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="a68a4-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="a68a4-138">巡覽至 [組態] 索引標籤，然後按一下 [啟用遠端]。</span><span class="sxs-lookup"><span data-stu-id="a68a4-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="a68a4-139">這個步驟可指定使用於遠端登入的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="a68a4-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="a68a4-140">[建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)：這個 Azure Machine Learning 工作區可用來建置機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="a68a4-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="a68a4-141">使用 HDInsight 叢集完成初始資料探索和縮小取樣之後，會處理這項工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="a68a4-142"><a name="getdata"></a>從公用來源取得資料</span><span class="sxs-lookup"><span data-stu-id="a68a4-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-143">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-144">若要從 [NYC 計程車車程](http://www.andresmh.com/nyctaxitrips/)資料集的公用位置取得該資料集，您可以使用[將資料移進和移出 Azure Blob 儲存體](machine-learning-data-science-move-azure-blob.md)中所述的任何一種方法，將資料複製到您的電腦。</span><span class="sxs-lookup"><span data-stu-id="a68a4-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="a68a4-145">我們在這裡說明如何使用 AzCopy 來傳輸含有資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="a68a4-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="a68a4-146">若要下載並安裝 AzCopy，請遵循 [開始使用 AzCopy 命令列公用程式](../storage/common/storage-use-azcopy.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="a68a4-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="a68a4-147">從命令提示字元視窗中發出下列 AzCopy 命令，以所需的目的地取代<path_to_data_folder>：</span><span class="sxs-lookup"><span data-stu-id="a68a4-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="a68a4-148">複製完成時，總共 24 個壓縮檔會位於選擇的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="a68a4-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="a68a4-149">將下載的檔案解壓縮到您本機電腦上的相同目錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="a68a4-150">記下未壓縮檔案所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a68a4-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="a68a4-151">接下來會將這個資料夾稱為 <path\_to\_unzipped_data\_files\>。</span><span class="sxs-lookup"><span data-stu-id="a68a4-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="a68a4-152"><a name="upload"></a>將資料上傳至 Azure HDInsight Hadoop 叢集的預設容器</span><span class="sxs-lookup"><span data-stu-id="a68a4-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-153">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-154">在下列 AzCopy 命令中，以建立 Hadoop 叢集和解壓縮資料檔案時指定的實際值取代下列參數。</span><span class="sxs-lookup"><span data-stu-id="a68a4-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="a68a4-155">&#60;path_to_data_folder>：在包含未解壓縮資料檔案之電腦上的目錄 (以及路徑)</span><span class="sxs-lookup"><span data-stu-id="a68a4-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="a68a4-156">&#60;storage account name of Hadoop cluster>：與您的 HDInsight 叢集關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a68a4-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="a68a4-157">&#60;default container of Hadoop cluster>：您的叢集所使用的預設容器。</span><span class="sxs-lookup"><span data-stu-id="a68a4-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="a68a4-158">請注意，預設容器的名稱通常與叢集本身的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="a68a4-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="a68a4-159">例如，如果叢集稱為 "abc123.azurehdinsight.net"，預設容器即為 abc123。</span><span class="sxs-lookup"><span data-stu-id="a68a4-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="a68a4-160">&#60;storage account key>：您的叢集所使用的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="a68a4-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="a68a4-161">從電腦的命令提示字元或 Windows PowerShell 視窗，執行下列兩個 AzCopy 命令。</span><span class="sxs-lookup"><span data-stu-id="a68a4-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="a68a4-162">這個命令會將車程資料，上傳至 Hadoop 叢集之預設容器中的 nyctaxitripraw 目錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="a68a4-163">這個命令會將費用資料，上傳至 Hadoop 叢集之預設容器中的 nyctaxifareraw 目錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="a68a4-164">資料現在應該位於 Azure Blob 儲存體，而且準備好在 HDInsight 叢集內使用。</span><span class="sxs-lookup"><span data-stu-id="a68a4-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="a68a4-165"><a name="#download-hql-files"></a>登入 Hadoop 叢集的前端節點，並準備進行探索資料分析</span><span class="sxs-lookup"><span data-stu-id="a68a4-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-166">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-167">若要存取叢集的前端節點以進行資料的探索資料分析和縮小取樣，請遵循 [存取 Hadoop 叢集的前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)中所述的程序進行。</span><span class="sxs-lookup"><span data-stu-id="a68a4-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="a68a4-168">在本逐步解說中，我們主要是使用 [Hive](https://hive.apache.org/)中撰寫的查詢 (類似 SQL 的查詢語言) 來執行初步資料探索。</span><span class="sxs-lookup"><span data-stu-id="a68a4-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="a68a4-169">Hive 查詢會儲存在 .hql 檔案。</span><span class="sxs-lookup"><span data-stu-id="a68a4-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="a68a4-170">我們接著會縮小取樣這份資料，以便在 Azure Machine Learning 中用來建置模型。</span><span class="sxs-lookup"><span data-stu-id="a68a4-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="a68a4-171">為了準備探索資料分析的叢集，我們從 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) 將包含相關 Hive 指令碼的 .hql 檔案下載至前端節點上的本機目錄 (C:\temp)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="a68a4-172">若要這樣做，請從叢集的前端節點內開啟 **命令提示字元** ，並發出下列兩個命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="a68a4-173">這兩個命令會將本逐步解說中所需的所有 .hql 檔案，下載到前端節點的本機目錄 C:\temp&#92;。</span><span class="sxs-lookup"><span data-stu-id="a68a4-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="a68a4-174"><a name="#hive-db-tables"></a>建立依月份分割的 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="a68a4-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-175">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-176">我們現在已準備好為我們的 NYC 計程車資料集建立 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="a68a4-177">在 Hadoop 叢集的前端節點中，於前端節點的桌面上開啟 ***Hadoop 命令列*** ，然後輸入命令以進入 Hive 目錄</span><span class="sxs-lookup"><span data-stu-id="a68a4-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="a68a4-178">**請從上述的 Hive bin/ 目錄提示字元執行本逐步解說中的所有 Hive 命令。如此可自動處理路徑相關問題。我們將在本逐步解說中交替使用「Hive 目錄提示字元」、「Hive bin/ 目錄提示字元」、「Hadoop 命令列」等詞語。**</span><span class="sxs-lookup"><span data-stu-id="a68a4-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="a68a4-179">從 Hive 目錄提示字元，於前端節點的 Hadoop 命令列中輸入下列命令，以提交 Hive 查詢來建立 Hive 資料庫和資料表：</span><span class="sxs-lookup"><span data-stu-id="a68a4-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="a68a4-180">以下是 C:\temp\sample\_hive\_create\_db\_and\_tables.hql 檔案的內容，其會建立 Hive 資料庫 nyctaxidb 及 trip 和 fare 資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="a68a4-181">這個 Hive 指令碼會建立兩個資料表：</span><span class="sxs-lookup"><span data-stu-id="a68a4-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="a68a4-182">"trip" 資料表包含每趟車程的詳細資料 (駕駛詳細資料、上車時間、車程距離和時間)</span><span class="sxs-lookup"><span data-stu-id="a68a4-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="a68a4-183">"fare" 資料表包含費用詳細資料 (費用金額、小費金額、通行費及附加費)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="a68a4-184">如果您需要這些程序的任何額外協助，或想要調查替代程序，請參閱[從 Hadoop 命令列直接提交 Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)一節。</span><span class="sxs-lookup"><span data-stu-id="a68a4-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="a68a4-185"><a name="#load-data"></a>依資料分割將資料載入 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="a68a4-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-186">這通常是 **管理** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-187">NYC 計程車資料集會依月份自然分割資料，可讓我們更快速處理和查詢時間。</span><span class="sxs-lookup"><span data-stu-id="a68a4-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="a68a4-188">下列 PowerShell 命令 (使用 **Hadoop 命令列**從 Hive 目錄發出) 會將資料載入至依月份分割的 "trip" 和 "fare" Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="a68a4-189">sample\_hive\_load\_data\_by\_partitions.hql 檔案包含下列 **LOAD** 命令。</span><span class="sxs-lookup"><span data-stu-id="a68a4-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="a68a4-190">請注意，我們在這裡使用於探索程序中的許多 Hive 查詢，只會查看單一資料分割或幾個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a68a4-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="a68a4-191">但這些查詢可跨整個資料執行。</span><span class="sxs-lookup"><span data-stu-id="a68a4-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="a68a4-192"><a name="#show-db"></a>顯示 HDInsight Hadoop 叢集中的資料庫</span><span class="sxs-lookup"><span data-stu-id="a68a4-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="a68a4-193">若要在 Hadoop 命令列視窗內顯示在 HDInsight Hadoop 叢集中建立的資料庫，可在 Hadoop 命令列中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="a68a4-194"><a name="#show-tables"></a>顯示 nyctaxidb 資料庫中的 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="a68a4-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="a68a4-195">若要顯示 nyctaxidb 資料庫中的資料表，可在 Hadoop 命令列中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="a68a4-196">我們可發出下列命令來確認資料表已分割：</span><span class="sxs-lookup"><span data-stu-id="a68a4-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="a68a4-197">預期的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="a68a4-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="a68a4-198">同樣地，我們可以發出下列命令來確保 fare 資料表已分割：</span><span class="sxs-lookup"><span data-stu-id="a68a4-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="a68a4-199">預期的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="a68a4-199">The expected output is shown below:</span></span>

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

## <span data-ttu-id="a68a4-200"><a name="#explore-hive"></a>Hive 中的資料探索和特徵工程</span><span class="sxs-lookup"><span data-stu-id="a68a4-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-201">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-202">適用於已載入 Hive 資料表之資料的資料探索和功能工程工作可以使用 Hive 查詢來完成。</span><span class="sxs-lookup"><span data-stu-id="a68a4-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="a68a4-203">以下是我們將在本節中逐步引導您執行的這類工作範例：</span><span class="sxs-lookup"><span data-stu-id="a68a4-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="a68a4-204">檢視這兩個資料表中的前 10 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="a68a4-205">在變動的時間範圍中探索數個欄位的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="a68a4-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="a68a4-206">調查經度和緯度欄位的資料品質。</span><span class="sxs-lookup"><span data-stu-id="a68a4-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="a68a4-207">根據 **tip\_amount** 產生二進位和多類別分類標籤。</span><span class="sxs-lookup"><span data-stu-id="a68a4-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="a68a4-208">藉由計算車程的直線距離來產生功能。</span><span class="sxs-lookup"><span data-stu-id="a68a4-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="a68a4-209">探索：檢視 trip 資料表中的前 10 筆記錄</span><span class="sxs-lookup"><span data-stu-id="a68a4-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-210">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-211">為了查看資料的外觀，我們檢查每個資料表的 10 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="a68a4-212">從 Hadoop 命令列主控台的 Hive 目錄提示字元，個別執行下列兩個查詢來檢查記錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="a68a4-213">若要從 "trip" 資料表取得第一個月的前 10 筆記錄：</span><span class="sxs-lookup"><span data-stu-id="a68a4-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="a68a4-214">若要從 "fare" 資料表取得第一個月的前 10 筆記錄：</span><span class="sxs-lookup"><span data-stu-id="a68a4-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="a68a4-215">通常是用於儲存記錄到檔案，以方便檢視。</span><span class="sxs-lookup"><span data-stu-id="a68a4-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="a68a4-216">對上述查詢進行微幅變更以完成這項作業：</span><span class="sxs-lookup"><span data-stu-id="a68a4-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="a68a4-217">探索：檢視 12 個資料分割中每一個資料分割的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="a68a4-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-218">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-219">令人感興趣的是車程數目在日曆年度的變化。</span><span class="sxs-lookup"><span data-stu-id="a68a4-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="a68a4-220">依月份分組可讓我們查看這個車程的大約分佈情況。</span><span class="sxs-lookup"><span data-stu-id="a68a4-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="a68a4-221">這會提供輸出：</span><span class="sxs-lookup"><span data-stu-id="a68a4-221">This gives us the output :</span></span>

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

<span data-ttu-id="a68a4-222">這裡的第一個資料行是月份，而第二個資料行是該月份的車程數目。</span><span class="sxs-lookup"><span data-stu-id="a68a4-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="a68a4-223">我們也可以在 Hive 目錄提示字元中發出下列命令，計算車程資料集的記錄總數。</span><span class="sxs-lookup"><span data-stu-id="a68a4-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="a68a4-224">這會產生：</span><span class="sxs-lookup"><span data-stu-id="a68a4-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="a68a4-225">我們可以使用針對車程資料集所顯示的類似命令，從 Hive 目錄提示字元發出費用資料集的 Hive 查詢，以驗證記錄數目。</span><span class="sxs-lookup"><span data-stu-id="a68a4-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="a68a4-226">這會提供輸出：</span><span class="sxs-lookup"><span data-stu-id="a68a4-226">This gives us the output:</span></span>

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

<span data-ttu-id="a68a4-227">請注意，兩個資料集會傳回完全相同的每月車程數。</span><span class="sxs-lookup"><span data-stu-id="a68a4-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="a68a4-228">這會提供已正確載入資料的第一次驗證。</span><span class="sxs-lookup"><span data-stu-id="a68a4-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="a68a4-229">您可以從 Hive 目錄提示字元使用下列命令，來計算費用資料集中的記錄總數：</span><span class="sxs-lookup"><span data-stu-id="a68a4-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="a68a4-230">這會產生：</span><span class="sxs-lookup"><span data-stu-id="a68a4-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="a68a4-231">兩個資料表中的記錄總數也會相同。</span><span class="sxs-lookup"><span data-stu-id="a68a4-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="a68a4-232">這會提供資料已正確載入的第二次驗證。</span><span class="sxs-lookup"><span data-stu-id="a68a4-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="a68a4-233">探索：依據 medallion 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="a68a4-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-234">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-235">此範例會識別在特定期間內超過 100 趟車程的圓形徽章 (計程車數目)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="a68a4-236">由於這個查詢受到資料分割變數 **month**的條件約束，因此使用資料分割資料表會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="a68a4-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="a68a4-237">查詢結果會寫入前端節點上 `C:\temp` 中的本機檔案 queryoutput.tsv。</span><span class="sxs-lookup"><span data-stu-id="a68a4-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="a68a4-238">以下是要檢查之 sample\_hive\_trip\_count\_by\_medallion.hql 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="a68a4-239">NYC 計程車資料集中的 medallion 會識別唯一的計程車。</span><span class="sxs-lookup"><span data-stu-id="a68a4-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="a68a4-240">我們可以詢問哪些計程車在特定時段超過特定的車程數目，以識別哪些計程車「忙碌中」。</span><span class="sxs-lookup"><span data-stu-id="a68a4-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="a68a4-241">下列範例會識別在前三個月中超過幾百趟車程的計程車，並將查詢結果儲存至本機檔案 C:\temp\queryoutput.tsv。</span><span class="sxs-lookup"><span data-stu-id="a68a4-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="a68a4-242">以下是要檢查之 sample\_hive\_trip\_count\_by\_medallion.hql 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="a68a4-243">從 Hive 目錄提示字元發出下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="a68a4-244">探索：依據 medallion 和 hack_license 的車程分佈</span><span class="sxs-lookup"><span data-stu-id="a68a4-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-245">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-246">當探索資料集時，我們通常會想要檢查共同出現的值群組數目。</span><span class="sxs-lookup"><span data-stu-id="a68a4-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="a68a4-247">本節提供如何為計程車和駕駛執行這項作業的範例。</span><span class="sxs-lookup"><span data-stu-id="a68a4-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="a68a4-248">sample\_hive\_trip\_count\_by\_medallion\_license.hql 檔案會將費用資料集分組成 "medallion" 和 "hack_license"，並傳回每個組合的計數。</span><span class="sxs-lookup"><span data-stu-id="a68a4-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="a68a4-249">以下是其內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="a68a4-250">這個查詢會依車程數目的遞減順序，傳回計程車和特定駕駛的組合。</span><span class="sxs-lookup"><span data-stu-id="a68a4-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="a68a4-251">從 Hive 目錄提示字元執行：</span><span class="sxs-lookup"><span data-stu-id="a68a4-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="a68a4-252">查詢結果會寫入本機檔案 C:\temp\queryoutput.tsv。</span><span class="sxs-lookup"><span data-stu-id="a68a4-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="a68a4-253">探索：藉由檢查無效的經度/緯度記錄來評估資料品質</span><span class="sxs-lookup"><span data-stu-id="a68a4-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-254">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-255">常見的探索資料分析目標是去掉無效或不正確的記錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="a68a4-256">本節的範例會判斷經度或緯度欄位是否包含遠離 NYC 區域的值。</span><span class="sxs-lookup"><span data-stu-id="a68a4-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="a68a4-257">由於這類記錄可能具有錯誤的經度-緯度值，因此我們想要從用來建立模型的任何資料中排除這些錯誤值。</span><span class="sxs-lookup"><span data-stu-id="a68a4-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="a68a4-258">以下是要檢查之 sample\_hive\_quality\_assessment.hql 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="a68a4-259">從 Hive 目錄提示字元執行：</span><span class="sxs-lookup"><span data-stu-id="a68a4-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="a68a4-260">這個命令中包含的 *-S* 引數會隱藏 Hive Map/Reduce 工作的狀態畫面顯示。</span><span class="sxs-lookup"><span data-stu-id="a68a4-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="a68a4-261">這非常有用，因為它讓 Hive 查詢輸出的螢幕顯示更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="a68a4-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="a68a4-262">探索：車程小費的二元類別分佈</span><span class="sxs-lookup"><span data-stu-id="a68a4-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-263">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-264">對於 [預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 一節中所述的二元分類問題而言，了解是否已指定小費會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="a68a4-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="a68a4-265">小費是二元分佈：</span><span class="sxs-lookup"><span data-stu-id="a68a4-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="a68a4-266">tip given(Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="a68a4-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="a68a4-267">no tip (Class 0, tip\_amount = $0)</span><span class="sxs-lookup"><span data-stu-id="a68a4-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="a68a4-268">以下顯示的 sample\_hive\_tipped\_frequencies.hql 檔案會執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="a68a4-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="a68a4-269">從 Hive 目錄提示字元執行：</span><span class="sxs-lookup"><span data-stu-id="a68a4-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="a68a4-270">探索：多元設定中的類別分佈</span><span class="sxs-lookup"><span data-stu-id="a68a4-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-271">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-272">對於 [預測工作的範例](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 一節中所述的多元分類問題，這個資料集也可用於自然分類，在這種情況下我們可能會想要預測指定的小費金額。</span><span class="sxs-lookup"><span data-stu-id="a68a4-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="a68a4-273">我們可以使用二元分類來定義查詢中的小費範圍。</span><span class="sxs-lookup"><span data-stu-id="a68a4-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="a68a4-274">為了取得各種小費範圍的類別分佈，我們使用 sample\_hive\_tip\_range\_frequencies.hql 檔案。</span><span class="sxs-lookup"><span data-stu-id="a68a4-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="a68a4-275">以下是其內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-275">Below are its contents.</span></span>

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

<span data-ttu-id="a68a4-276">從 Hadoop 命令列主控台執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="a68a4-277">探索：計算兩個經度-緯度位置之間的直線距離</span><span class="sxs-lookup"><span data-stu-id="a68a4-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-278">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-279">直線距離的量值可協助我們了解與實際車程距離之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a68a4-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="a68a4-280">這項特徵是用來指出當乘客認為駕駛刻意繞遠路時，他們可能比較不會給小費。</span><span class="sxs-lookup"><span data-stu-id="a68a4-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="a68a4-281">為了查看兩個經度-緯度點 (「大圓」距離) 之間的實際車程距離與 [Haversine 距離](http://en.wikipedia.org/wiki/Haversine_formula) 的比較，我們使用 Hive 中的可用三角函數 (如下所示)：</span><span class="sxs-lookup"><span data-stu-id="a68a4-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="a68a4-282">在上述查詢中，R 是地球的半徑 (英里)，而 pi 會轉換成弧度。</span><span class="sxs-lookup"><span data-stu-id="a68a4-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="a68a4-283">請注意，經度-緯度點會經過「篩選」，以移除遠離 NYC 區域的值。</span><span class="sxs-lookup"><span data-stu-id="a68a4-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="a68a4-284">在本例中，我們將結果寫入 "queryoutputdir" 目錄。</span><span class="sxs-lookup"><span data-stu-id="a68a4-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="a68a4-285">以下所示的一連串命令會先建立這個輸出目錄，然後再執行 Hive 命令。</span><span class="sxs-lookup"><span data-stu-id="a68a4-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="a68a4-286">從 Hive 目錄提示字元執行：</span><span class="sxs-lookup"><span data-stu-id="a68a4-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="a68a4-287">查詢結果會寫入 Hadoop 叢集的預設容器下的 9 個 Azure Blob，即 queryoutputdir/000000\_0 至 queryoutputdir/000008\_0。</span><span class="sxs-lookup"><span data-stu-id="a68a4-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="a68a4-288">為了查看個別 Blob 的大小，我們從 Hive 目錄提示字元執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="a68a4-289">為了查看指定檔案的內容 (假設是 000000\_0)，我們使用 Hadoop 的 `copyToLocal` 命令 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="a68a4-290">遇到大型檔案，`copyToLocal` 可能會很慢，因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="a68a4-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="a68a4-291">將此資料放在 Azure Blob 中的主要優點在於，我們可以使用[匯入資料][import-data]模組在 Azure Machine Learning 內探索資料。</span><span class="sxs-lookup"><span data-stu-id="a68a4-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="a68a4-292"><a name="#downsample"></a>在 Azure Machine Learning 中縮小取樣和建置模型</span><span class="sxs-lookup"><span data-stu-id="a68a4-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="a68a4-293">這通常是 **資料科學家** 工作。</span><span class="sxs-lookup"><span data-stu-id="a68a4-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="a68a4-294">在探索資料分析階段之後，我們現在已準備好縮小取樣資料，以便在 Azure Machine Learning 中建置模型。</span><span class="sxs-lookup"><span data-stu-id="a68a4-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="a68a4-295">在本節中，我們將示範如何使用 Hive 查詢來縮小取樣資料，然後從 Azure Machine Learning 中的[匯入資料][import-data]模組存取此資料。</span><span class="sxs-lookup"><span data-stu-id="a68a4-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="a68a4-296">縮小取樣資料</span><span class="sxs-lookup"><span data-stu-id="a68a4-296">Down sampling the data</span></span>
<span data-ttu-id="a68a4-297">這個程序包含兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="a68a4-297">There are two steps in this procedure.</span></span> <span data-ttu-id="a68a4-298">首先我們在所有記錄都會出現的三個索引鍵("medallion"、"hack\_license"、"pickup\_datetime") 上加入 **nyctaxidb.trip** 和 **nyctaxidb.fare** 資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="a68a4-299">接著產生二元分類標籤 **tipped** 和多元分類標籤 **tip\_class**。</span><span class="sxs-lookup"><span data-stu-id="a68a4-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="a68a4-300">為了能夠直接從 Azure Machine Learning 中的[匯入資料][import-data]模組使用縮小取樣的資料，必須將上述查詢的結果儲存至內部 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="a68a4-301">接下來我們將建立內部 Hive 資料表，並以加入和縮小取樣的資料來填入其內容。</span><span class="sxs-lookup"><span data-stu-id="a68a4-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="a68a4-302">查詢會直接套用標準 Hive 函式，以從 "pickup\_datetime" 欄位產生時間、週數和工作日 (1 代表星期一，7 代表星期日)，以及上車和下車位置之間的直線距離。</span><span class="sxs-lookup"><span data-stu-id="a68a4-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="a68a4-303">使用者可以參考 [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) 以取得這類函數的完整清單。</span><span class="sxs-lookup"><span data-stu-id="a68a4-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="a68a4-304">查詢會接著縮小取樣資料，以將查詢結果填入 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="a68a4-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="a68a4-305">只有約 1% 的原始資料集會匯入 Studio。</span><span class="sxs-lookup"><span data-stu-id="a68a4-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="a68a4-306">以下是 sample\_hive\_prepare\_for\_aml\_full.hql 檔案的內容，該檔案會準備在 Azure Machine Learning 中建置模型所要使用的資料。</span><span class="sxs-lookup"><span data-stu-id="a68a4-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

        --- now insert contents of the join into the above internal table

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

<span data-ttu-id="a68a4-307">若要從 Hive 目錄提示字元執行這個查詢：</span><span class="sxs-lookup"><span data-stu-id="a68a4-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="a68a4-308">我們現在有內部資料表 "nyctaxidb.nyctaxi_downsampled_dataset"，使用 Azure Machine Learning 中的[匯入資料][import-data]模組即可存取此資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="a68a4-309">此外，我們可能使用這個資料集來建置機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="a68a4-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="a68a4-310">使用 Azure Machine Learning 中的「匯入資料」模組來存取縮小取樣的資料</span><span class="sxs-lookup"><span data-stu-id="a68a4-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="a68a4-311">若要在 Azure Machine Learning 的[匯入資料][import-data]模組中發出 Hive 查詢，先決條件是要能夠存取 Azure Machine Learning 工作區，以及要能夠存取叢集及其相關儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="a68a4-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="a68a4-312">以下是[匯入資料][import-data]模組及輸入參數的一些詳細資料：</span><span class="sxs-lookup"><span data-stu-id="a68a4-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="a68a4-313">**HCatalog 伺服器 URI**：如果叢集名稱是 abc123，則為：https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="a68a4-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="a68a4-314">**Hadoop 使用者帳戶名稱**：為叢集選擇的使用者名稱 (**非**遠端存取使用者名稱)</span><span class="sxs-lookup"><span data-stu-id="a68a4-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="a68a4-315">**Hadoop 使用者帳戶密碼**：為叢集選擇的密碼 (**非**遠端存取密碼)</span><span class="sxs-lookup"><span data-stu-id="a68a4-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="a68a4-316">**輸出資料的位置** ：選擇為 Azure。</span><span class="sxs-lookup"><span data-stu-id="a68a4-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="a68a4-317">**Azure 儲存體帳戶名稱** ：與叢集相關聯的預設儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a68a4-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="a68a4-318">**Azure 容器名稱** ：這是叢集的預設容器名稱，且通常與叢集名稱相同。</span><span class="sxs-lookup"><span data-stu-id="a68a4-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="a68a4-319">如果叢集為 "abc123"，即為 abc123。</span><span class="sxs-lookup"><span data-stu-id="a68a4-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a68a4-320">**任何我們想要使用 Azure Machine Learning 中的[匯入資料][import-data]模組來查詢的資料表都必須是內部資料表。**</span><span class="sxs-lookup"><span data-stu-id="a68a4-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="a68a4-321">以下是判斷資料庫 D.db 中的資料表 T 是否為內部資料表的秘訣。</span><span class="sxs-lookup"><span data-stu-id="a68a4-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="a68a4-322">從 Hive 目錄提示字元發出下列命令：</span><span class="sxs-lookup"><span data-stu-id="a68a4-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="a68a4-323">如果資料表是內部資料表並已填妥，其內容必須顯示在這裡。</span><span class="sxs-lookup"><span data-stu-id="a68a4-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="a68a4-324">判斷資料表是否為內部資料表的另一種方式是使用 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="a68a4-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="a68a4-325">您可以使用它巡覽至叢集的預設容器名稱，然後依資料表名稱篩選。</span><span class="sxs-lookup"><span data-stu-id="a68a4-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="a68a4-326">如果有顯示資料表及其內容，則可確認它是內部資料表。</span><span class="sxs-lookup"><span data-stu-id="a68a4-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="a68a4-327">以下是 Hive 查詢和[匯入資料][import-data]模組的快照：</span><span class="sxs-lookup"><span data-stu-id="a68a4-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![匯入資料模組的 Hive 查詢](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="a68a4-329">請注意，由於縮小取樣的資料位於預設容器中，因此從 Azure Machine Learning 產生的 Hive 查詢會很簡單，只會是 "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data"。</span><span class="sxs-lookup"><span data-stu-id="a68a4-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="a68a4-330">資料集現在可做為建置機器學習服務模型的起點。</span><span class="sxs-lookup"><span data-stu-id="a68a4-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="a68a4-331"><a name="mlmodel"></a>在 Azure Machine Learning 中建置模型</span><span class="sxs-lookup"><span data-stu-id="a68a4-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="a68a4-332">我們現在可在 [Azure Machine Learning](https://studio.azureml.net)中繼續建置和部署模型。</span><span class="sxs-lookup"><span data-stu-id="a68a4-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="a68a4-333">資料已就緒，可用來解決以上指出的預測問題：</span><span class="sxs-lookup"><span data-stu-id="a68a4-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="a68a4-334">**1.二元分類**：預測是否已支付某趟車程的小費。</span><span class="sxs-lookup"><span data-stu-id="a68a4-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="a68a4-335">**已使用學習者：** 二元羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="a68a4-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="a68a4-336">a.</span><span class="sxs-lookup"><span data-stu-id="a68a4-336">a.</span></span> <span data-ttu-id="a68a4-337">對於這個問題，我們的目標 (或類別) 標籤是 "tipped"。</span><span class="sxs-lookup"><span data-stu-id="a68a4-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="a68a4-338">縮小取樣的原始資料集有幾個資料行會顯示這個分類實驗目標。</span><span class="sxs-lookup"><span data-stu-id="a68a4-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="a68a4-339">特別是 tip\_class、tip\_amount 和 total\_amount，可揭示測試時不會提供之目標標籤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a68a4-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="a68a4-340">我們使用[選取資料集中的資料行][select-columns]模組，從考量範圍中移除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="a68a4-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="a68a4-341">以下快照顯示我們的實驗，目的是預測是否會支付指定車程的小費。</span><span class="sxs-lookup"><span data-stu-id="a68a4-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="a68a4-343">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68a4-343">b.</span></span> <span data-ttu-id="a68a4-344">對於這項實驗，我們的目標標籤分佈大約是 1:1。</span><span class="sxs-lookup"><span data-stu-id="a68a4-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="a68a4-345">以下快照顯示二元分類問題之 tip 類別標籤的分佈。</span><span class="sxs-lookup"><span data-stu-id="a68a4-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![類別標籤的分佈](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="a68a4-347">因此，我們將取得 0.987 的 AUC，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="a68a4-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![AUC 值](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="a68a4-349">**2.多元分類**：若要預測針對該趟車程支付的小費金額範圍，請使用先前定義的類別。</span><span class="sxs-lookup"><span data-stu-id="a68a4-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="a68a4-350">**已使用學習者：** 多元羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="a68a4-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="a68a4-351">a.</span><span class="sxs-lookup"><span data-stu-id="a68a4-351">a.</span></span> <span data-ttu-id="a68a4-352">對於這個問題，我們的目標 (或類別) 標籤是 "tip\_class"，可能採用五個值 (0、1、2、3、4) 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="a68a4-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="a68a4-353">如二元分類案例所示，我們有幾個資料行會顯示這個實驗的目標。</span><span class="sxs-lookup"><span data-stu-id="a68a4-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="a68a4-354">特別是 tipped、tip\_amount 和 total\_amount，可揭示測試時不會提供之目標標籤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a68a4-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="a68a4-355">我們使用[選取資料集中的資料行][select-columns]模組來移除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="a68a4-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="a68a4-356">以下快照顯示我們的實驗預測小費可能落在哪個分類收納組中 (類別 0：小費 = 美金 $0 元，類別 1：小費 > 美金 $0 元且 <= 美金 $5 元，類別 2：小費 > 美金 $5 元且 <= 美金 $10 元，類別 3：小費 > 美金 $10 元且 <= 美金 $20 元，類別 4：小費 > 美金 $20 元)</span><span class="sxs-lookup"><span data-stu-id="a68a4-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="a68a4-358">現在會顯示實際的測試類別分佈。</span><span class="sxs-lookup"><span data-stu-id="a68a4-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="a68a4-359">我們看到類別 0 和類別 1 很普遍，其他類別則很罕見。</span><span class="sxs-lookup"><span data-stu-id="a68a4-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![測試類別分佈](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="a68a4-361">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68a4-361">b.</span></span> <span data-ttu-id="a68a4-362">對於這項實驗，我們使用混淆矩陣來查看預測精確度。</span><span class="sxs-lookup"><span data-stu-id="a68a4-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="a68a4-363">如下所示。</span><span class="sxs-lookup"><span data-stu-id="a68a4-363">This is shown below.</span></span>

![混淆矩陣](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="a68a4-365">請注意，雖然常見類別上的類別精確度很高，但模型對較罕見類別沒有很好的「學習」效果。</span><span class="sxs-lookup"><span data-stu-id="a68a4-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="a68a4-366">**3.迴歸工作**：預測針對某趟車程支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="a68a4-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="a68a4-367">**已使用學習者：** 推進式決策樹</span><span class="sxs-lookup"><span data-stu-id="a68a4-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="a68a4-368">a.</span><span class="sxs-lookup"><span data-stu-id="a68a4-368">a.</span></span> <span data-ttu-id="a68a4-369">對於這個問題，我們的目標 (或類別) 標籤是 "tip\_amount"。</span><span class="sxs-lookup"><span data-stu-id="a68a4-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="a68a4-370">在本例中，我們的顯示目標是：tipped、tip\_class、total\_amount；所有變數都會揭示測試時通常不會提供之小費金額的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a68a4-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="a68a4-371">我們使用[選取資料集中的資料行][select-columns]模組來移除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="a68a4-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="a68a4-372">以下快照顯示我們用來預測指定小費金額的實驗。</span><span class="sxs-lookup"><span data-stu-id="a68a4-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![實驗快照](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="a68a4-374">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68a4-374">b.</span></span> <span data-ttu-id="a68a4-375">對於迴歸問題，我們會藉由查看預測中的平方誤差、決定係數等，來測量預測的精確度。</span><span class="sxs-lookup"><span data-stu-id="a68a4-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="a68a4-376">以下將進行示範。</span><span class="sxs-lookup"><span data-stu-id="a68a4-376">We show these below.</span></span>

![預測統計資料](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="a68a4-378">我們看到決定係數是 0.709，其中隱含的變異大約有 71% 是由我們的模型係數所造成。</span><span class="sxs-lookup"><span data-stu-id="a68a4-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a68a4-379">若要深入了解 Azure Machine Learning，及如何存取並使用它，請參閱[什麼是機器學習服務?](machine-learning-what-is-machine-learning.md)。</span><span class="sxs-lookup"><span data-stu-id="a68a4-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="a68a4-380">若要在 Azure Machine Learning 上進行眾多機器學習服務實驗， [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com/)是非常實用的資源。</span><span class="sxs-lookup"><span data-stu-id="a68a4-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="a68a4-381">該資源庫涵蓋了所有實驗，並且完整介紹了 Azure 機器學習的功能範圍。</span><span class="sxs-lookup"><span data-stu-id="a68a4-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="a68a4-382">授權資訊</span><span class="sxs-lookup"><span data-stu-id="a68a4-382">License Information</span></span>
<span data-ttu-id="a68a4-383">此範例逐步解說及其隨附的指令碼是在 MIT 授權下由 Microsoft 所共用。</span><span class="sxs-lookup"><span data-stu-id="a68a4-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="a68a4-384">如需詳細資訊，請檢查 GitHub 上程式碼範例目錄中的 LICENSE.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="a68a4-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="a68a4-385">參考</span><span class="sxs-lookup"><span data-stu-id="a68a4-385">References</span></span>
<span data-ttu-id="a68a4-386">•    [Andrés Monroy NYC 計程車車程下載頁面](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="a68a4-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="a68a4-387">•    [FOILing NYC 的計程車車程資料 (作者為 Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="a68a4-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="a68a4-388">•    [NYC 計程車和禮車委託研究和統計資料](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="a68a4-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
