---
title: "使用 Panda 建立 Azure blob 儲存體資料功能 | Microsoft Docs"
description: "如何使用 Panda Python 封裝對儲存在 Azure blob 容器的資料建立功能。"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="a57a8-103">使用 Panda 建立 Azure blob 儲存體資料功能</span><span class="sxs-lookup"><span data-stu-id="a57a8-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="a57a8-104">本文件說明如何使用 [Pandas](http://pandas.pydata.org/) Python 封裝，對儲存在 Azure blob 容器的資料建立特徵。</span><span class="sxs-lookup"><span data-stu-id="a57a8-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="a57a8-105">概述如何將資料載入 Panda 資料框架後，接著會示範如何使用 Python 指令碼，搭配指標值和分類收納特徵，以產生分類特徵。</span><span class="sxs-lookup"><span data-stu-id="a57a8-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="a57a8-106">這個 **功能表** 所連結的主題會說明如何在各種環境中建立資料的特徵。</span><span class="sxs-lookup"><span data-stu-id="a57a8-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="a57a8-107">此工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a57a8-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a57a8-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a57a8-108">Prerequisites</span></span>
<span data-ttu-id="a57a8-109">本文假設您已建立 Azure Blob 儲存體帳戶，並將您的資料儲存在該處。</span><span class="sxs-lookup"><span data-stu-id="a57a8-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="a57a8-110">如需設定帳戶的指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a57a8-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="a57a8-111">將資料載入至 Pandas 資料框架</span><span class="sxs-lookup"><span data-stu-id="a57a8-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="a57a8-112">若要進行探索和操作資料集，必須從 Blob 來源將資料集下載至本機檔案，然後將其載入 Pandas 資料框架中。</span><span class="sxs-lookup"><span data-stu-id="a57a8-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="a57a8-113">以下是此程序的遵循步驟：</span><span class="sxs-lookup"><span data-stu-id="a57a8-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="a57a8-114">使用 Blob 服務，透過下列 Python 程式碼範例，從 Azure Blob 下載資料。</span><span class="sxs-lookup"><span data-stu-id="a57a8-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="a57a8-115">使用您的特定值來取代下列程式碼中的變數：</span><span class="sxs-lookup"><span data-stu-id="a57a8-115">Replace the variable in the code below with your specific values:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="a57a8-116">從下載的檔案中，將資料讀取至 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="a57a8-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="a57a8-117">現在您已經準備好探索資料並在此資料集上產生功能。</span><span class="sxs-lookup"><span data-stu-id="a57a8-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="a57a8-118"><a name="blob-featuregen"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="a57a8-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="a57a8-119">接下兩節會說明如何使用 Python 指令碼，產生帶有指標值和分類收納功能的分類功能。</span><span class="sxs-lookup"><span data-stu-id="a57a8-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="a57a8-120"><a name="blob-countfeature"></a>以指標值為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="a57a8-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="a57a8-121">類別功能可使用如下的方式來建立：</span><span class="sxs-lookup"><span data-stu-id="a57a8-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="a57a8-122">檢查類別資料行的分佈：</span><span class="sxs-lookup"><span data-stu-id="a57a8-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="a57a8-123">產生每個資料行值的指標值</span><span class="sxs-lookup"><span data-stu-id="a57a8-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="a57a8-124">將指標資料行與原始資料框架聯結在一起</span><span class="sxs-lookup"><span data-stu-id="a57a8-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="a57a8-125">移除原始變數本身：</span><span class="sxs-lookup"><span data-stu-id="a57a8-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="a57a8-126"><a name="blob-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="a57a8-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="a57a8-127">若要產生分類收納功能，我們可使用如下的方式繼續進行：</span><span class="sxs-lookup"><span data-stu-id="a57a8-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="a57a8-128">新增一系列的資料行，以分類收納數值資料行</span><span class="sxs-lookup"><span data-stu-id="a57a8-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="a57a8-129">將分類收納轉換為一系列的布林值變數</span><span class="sxs-lookup"><span data-stu-id="a57a8-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="a57a8-130">最後，將虛擬變數新增回原始資料框架中</span><span class="sxs-lookup"><span data-stu-id="a57a8-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="a57a8-131"><a name="sql-featuregen"></a>將資料寫回 Azure Blob 並在 AzureMachine Learning 中取用</span><span class="sxs-lookup"><span data-stu-id="a57a8-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="a57a8-132">在您探索資料和建立必要功能後，可以上傳資料 (取樣性或功能性) 至 Azure Blob，並在 Azure Machine Learning 中透過下列步驟取用資料：請注意，您也可以在 Azure Machine Learning Studio 中建立其他功能。</span><span class="sxs-lookup"><span data-stu-id="a57a8-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="a57a8-133">將資料框架寫入本機檔案中</span><span class="sxs-lookup"><span data-stu-id="a57a8-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="a57a8-134">將資料上傳至 Azure Blob，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a57a8-134">Upload the data to Azure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="a57a8-135">現在您可以使用 Azure Machine Learning [匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 模組從 Blob 讀取資料，如以下畫面所示：</span><span class="sxs-lookup"><span data-stu-id="a57a8-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![讀取器 Blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

