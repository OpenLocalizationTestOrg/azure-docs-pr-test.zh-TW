---
title: "在 Azure 中的 aaaExplore 資料 blob 儲存體與熊 |Microsoft 文件"
description: "如何 tooexplore 資料儲存在 Azure blob 容器使用熊。"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="e4af1-103">使用 Pandas 瀏覽 Azure blob 儲存體中的資料</span><span class="sxs-lookup"><span data-stu-id="e4af1-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="e4af1-104">本文件涵蓋 tooexplore 資料儲存在 Azure blob 容器使用[熊](http://pandas.pydata.org/)Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="e4af1-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="e4af1-105">hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。</span><span class="sxs-lookup"><span data-stu-id="e4af1-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="e4af1-106">這項工作是在 hello 步驟[資料科學程序]()。</span><span class="sxs-lookup"><span data-stu-id="e4af1-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e4af1-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e4af1-107">Prerequisites</span></span>
<span data-ttu-id="e4af1-108">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="e4af1-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e4af1-109">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4af1-109">Created an Azure storage account.</span></span> <span data-ttu-id="e4af1-110">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e4af1-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="e4af1-111">將您的資料儲存在 Azure blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4af1-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="e4af1-112">如果您需要的指示，請參閱[移動資料 tooand 從 Azure 儲存體](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="e4af1-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="e4af1-113">Hello 資料載入熊資料框架</span><span class="sxs-lookup"><span data-stu-id="e4af1-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="e4af1-114">tooexplore 和管理資料集，它必須先從 hello blob 來源 tooa 本機檔案，然後可以載入熊資料框架中下載。</span><span class="sxs-lookup"><span data-stu-id="e4af1-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="e4af1-115">以下是此程序的 hello 步驟 toofollow:</span><span class="sxs-lookup"><span data-stu-id="e4af1-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="e4af1-116">從 Azure 下載 hello 資料以下列 Python 程式碼範例使用 blob 服務的 hello 的 blob。</span><span class="sxs-lookup"><span data-stu-id="e4af1-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="e4af1-117">取代下列程式碼的特定值的 hello 中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="e4af1-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="e4af1-118">在從 hello 熊資料範圍內的讀取 hello 資料下載檔案。</span><span class="sxs-lookup"><span data-stu-id="e4af1-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="e4af1-119">現在您已準備好 tooexplore hello 資料，並產生此資料集上的功能。</span><span class="sxs-lookup"><span data-stu-id="e4af1-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="e4af1-120"><a name="blob-dataexploration"></a>使用 Pandas 的資料探索範例</span><span class="sxs-lookup"><span data-stu-id="e4af1-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="e4af1-121">以下是幾個方法的範例使用熊 tooexplore 資料：</span><span class="sxs-lookup"><span data-stu-id="e4af1-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="e4af1-122">檢查 hello**數目的資料列和資料行**</span><span class="sxs-lookup"><span data-stu-id="e4af1-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="e4af1-123">**檢查**hello 第一個或最後幾個**列**中下列資料集的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4af1-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="e4af1-124">檢查 hello**資料型別**每個資料行匯入為使用下列範例程式碼的 hello</span><span class="sxs-lookup"><span data-stu-id="e4af1-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="e4af1-125">檢查 hello**基本統計資料**的 hello 中的資料行，如下所示 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="e4af1-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="e4af1-126">尋找在 hello 的每個資料行值的項目，如下所示</span><span class="sxs-lookup"><span data-stu-id="e4af1-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="e4af1-127">**計算遺漏值**與 hello 實際數目，使用下列範例程式碼的 hello 每個資料行中的項目</span><span class="sxs-lookup"><span data-stu-id="e4af1-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="e4af1-128">如果您有**遺漏值**hello 資料中的特定資料行，也可以加以卸除，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e4af1-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="e4af1-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="e4af1-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="e4af1-130">另一個方式 tooreplace 遺漏的值是使用 hello 模式函式：</span><span class="sxs-lookup"><span data-stu-id="e4af1-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="e4af1-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="e4af1-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="e4af1-132">建立**長條圖**繪製使用變數的分類收納 tooplot hello 發佈數目可變的</span><span class="sxs-lookup"><span data-stu-id="e4af1-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="e4af1-133">查看**相互關聯**之間使用 scatterplot 或 hello 內建的相互關聯的函式的變數</span><span class="sxs-lookup"><span data-stu-id="e4af1-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

