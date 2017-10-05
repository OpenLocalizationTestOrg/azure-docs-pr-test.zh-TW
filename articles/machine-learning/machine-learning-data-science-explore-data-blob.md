---
title: "使用 Pandas 瀏覽 Azure blob 儲存體中的資料 | Microsoft Docs"
description: "如何使用 Pandas 瀏覽儲存在 Azure blob 容器的資料。"
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="2ed70-103">使用 Pandas 瀏覽 Azure blob 儲存體中的資料</span><span class="sxs-lookup"><span data-stu-id="2ed70-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="2ed70-104">本文件涵蓋如何使用 [Pandas](http://pandas.pydata.org/) Python 封裝瀏覽儲存在 Azure blob 容器的資料。</span><span class="sxs-lookup"><span data-stu-id="2ed70-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="2ed70-105">下列 **功能表** 所連結的主題會說明如何從各種不同的儲存體環境使用工具來瀏覽資料。</span><span class="sxs-lookup"><span data-stu-id="2ed70-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="2ed70-106">此工作是 [資料科學程序]()中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="2ed70-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="2ed70-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="2ed70-107">Prerequisites</span></span>
<span data-ttu-id="2ed70-108">本文假設您已經：</span><span class="sxs-lookup"><span data-stu-id="2ed70-108">This article assumes that you have:</span></span>

* <span data-ttu-id="2ed70-109">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ed70-109">Created an Azure storage account.</span></span> <span data-ttu-id="2ed70-110">如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="2ed70-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="2ed70-111">將您的資料儲存在 Azure blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ed70-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="2ed70-112">如需指示，請參閱 [從 Azure 儲存體來回移動資料](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="2ed70-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="2ed70-113">將資料載入 Pandas 資料框架</span><span class="sxs-lookup"><span data-stu-id="2ed70-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="2ed70-114">若要探索和操作資料集，必須先從 Blob 來源將資料集下載至本機檔案，然後將其載入 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="2ed70-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="2ed70-115">以下是此程序的遵循步驟：</span><span class="sxs-lookup"><span data-stu-id="2ed70-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="2ed70-116">使用 blob 服務，透過下列 Python 程式碼範例，從 Azure blob 下載資料。</span><span class="sxs-lookup"><span data-stu-id="2ed70-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="2ed70-117">使用您的特定值來取代下列程式碼中的變數：</span><span class="sxs-lookup"><span data-stu-id="2ed70-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="2ed70-118">從下載的檔案中，將資料讀取至 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="2ed70-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="2ed70-119">現在您已經準備好探索資料並在此資料集上產生功能。</span><span class="sxs-lookup"><span data-stu-id="2ed70-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="2ed70-120"><a name="blob-dataexploration"></a>使用 Pandas 的資料探索範例</span><span class="sxs-lookup"><span data-stu-id="2ed70-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="2ed70-121">以下是數個可使用 Pandas 探索資料的範例方式：</span><span class="sxs-lookup"><span data-stu-id="2ed70-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="2ed70-122">檢查 **資料列和資料行的數目**</span><span class="sxs-lookup"><span data-stu-id="2ed70-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="2ed70-123">**檢查**資料集中的前幾個或最後幾個**資料列**：</span><span class="sxs-lookup"><span data-stu-id="2ed70-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="2ed70-124">檢查使用下列程式碼範例匯入之每個資料行的 **資料類型**</span><span class="sxs-lookup"><span data-stu-id="2ed70-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="2ed70-125">檢查資料集中資料行的 **基本統計資料** ，如下所示</span><span class="sxs-lookup"><span data-stu-id="2ed70-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="2ed70-126">查看每個資料行值的項目數，如下所示</span><span class="sxs-lookup"><span data-stu-id="2ed70-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="2ed70-127">**計算遺漏值** 與實際項目數</span><span class="sxs-lookup"><span data-stu-id="2ed70-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="2ed70-128">如果您在資料的特定資料行中有 **遺漏值** ，則可卸除它們，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ed70-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="2ed70-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="2ed70-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="2ed70-130">取代遺漏值的另一種方式是使用模式函式：</span><span class="sxs-lookup"><span data-stu-id="2ed70-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="2ed70-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="2ed70-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="2ed70-132">使用變動數目的分類收納組來建立 **長條圖** ，以繪製變數的分佈</span><span class="sxs-lookup"><span data-stu-id="2ed70-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="2ed70-133">使用散佈圖或使用內建的相互關聯函式，來查看變數之間的 **相互關聯**</span><span class="sxs-lookup"><span data-stu-id="2ed70-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

