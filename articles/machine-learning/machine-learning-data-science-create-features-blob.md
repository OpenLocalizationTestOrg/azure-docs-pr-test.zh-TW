---
title: "aaaCreate 功能的 Azure blob 儲存體資料使用貓熊 |Microsoft 文件"
description: "Toocreate 功能如何儲存在與 hello 貓熊 Python 封裝的 Azure blob 容器中的資料。"
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="70ba4-103">使用 Panda 建立 Azure blob 儲存體資料功能</span><span class="sxs-lookup"><span data-stu-id="70ba4-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="70ba4-104">本文件說明如何 toocreate 功能的資料儲存在 Azure blob 容器使用 hello[熊](http://pandas.pydata.org/)Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="70ba4-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="70ba4-105">之後大綱如何 tooload hello 資料至貓熊資料框架，它會顯示如何使用 Python 指令碼搭配指標值和分類收納功能 toogenerate 類別特徵。</span><span class="sxs-lookup"><span data-stu-id="70ba4-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="70ba4-106">這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。</span><span class="sxs-lookup"><span data-stu-id="70ba4-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="70ba4-107">這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="70ba4-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70ba4-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="70ba4-108">Prerequisites</span></span>
<span data-ttu-id="70ba4-109">本文假設您已建立 Azure Blob 儲存體帳戶，並將您的資料儲存在該處。</span><span class="sxs-lookup"><span data-stu-id="70ba4-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="70ba4-110">如果您需要指示 tooset 設定帳戶，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="70ba4-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="70ba4-111">Hello 資料載入熊資料框架</span><span class="sxs-lookup"><span data-stu-id="70ba4-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="70ba4-112">在順序 toodo 探索和管理資料集，它必須從 hello blob 來源 tooa 本機檔案然後可以載入熊資料框架中下載。</span><span class="sxs-lookup"><span data-stu-id="70ba4-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="70ba4-113">以下是此程序的 hello 步驟 toofollow:</span><span class="sxs-lookup"><span data-stu-id="70ba4-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="70ba4-114">從 Azure 下載 hello 資料以下列範例使用 blob 服務的 Python 程式碼的 hello 的 blob。</span><span class="sxs-lookup"><span data-stu-id="70ba4-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="70ba4-115">以您的特定值取代 hello 下列的程式碼中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="70ba4-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="70ba4-116">在從 hello 熊資料範圍內的讀取 hello 資料下載檔案。</span><span class="sxs-lookup"><span data-stu-id="70ba4-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="70ba4-117">現在您已準備好 tooexplore hello 資料，並產生此資料集上的功能。</span><span class="sxs-lookup"><span data-stu-id="70ba4-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="70ba4-118"><a name="blob-featuregen"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="70ba4-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="70ba4-119">hello 下兩節會顯示與指標值分類收納 toogenerate 類別特徵功能使用 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="70ba4-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="70ba4-120"><a name="blob-countfeature"></a>以指標值為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="70ba4-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="70ba4-121">類別功能可使用如下的方式來建立：</span><span class="sxs-lookup"><span data-stu-id="70ba4-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="70ba4-122">檢查 hello 分佈 hello 類別資料行：</span><span class="sxs-lookup"><span data-stu-id="70ba4-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="70ba4-123">產生每個 hello 資料行值的指標值</span><span class="sxs-lookup"><span data-stu-id="70ba4-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="70ba4-124">加入原始資料框架 hello 與 hello 指標資料行</span><span class="sxs-lookup"><span data-stu-id="70ba4-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="70ba4-125">移除 hello 原始變數本身：</span><span class="sxs-lookup"><span data-stu-id="70ba4-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="70ba4-126"><a name="blob-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="70ba4-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="70ba4-127">若要產生分類收納功能，我們可使用如下的方式繼續進行：</span><span class="sxs-lookup"><span data-stu-id="70ba4-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="70ba4-128">加入資料行 toobin 數值資料行序列</span><span class="sxs-lookup"><span data-stu-id="70ba4-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="70ba4-129">轉換布林值變數的分類收納 tooa 的序列</span><span class="sxs-lookup"><span data-stu-id="70ba4-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="70ba4-130">最後，聯結 hello dummy 變數回 toohello 原始資料框架</span><span class="sxs-lookup"><span data-stu-id="70ba4-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="70ba4-131"><a name="sql-featuregen"></a>將資料寫入回 tooAzure blob 和 Azure Machine Learning 中使用</span><span class="sxs-lookup"><span data-stu-id="70ba4-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="70ba4-132">您已經瀏覽 hello 資料及建立 hello 所需的功能之後，您可以上傳 hello 資料 (取樣或特徵化) tooan Azure blob，然後使用下列步驟的 hello Azure Machine Learning 中使用它： 請注意，可以在 hello 中建立額外的功能Azure Machine Learning Studio 以及。</span><span class="sxs-lookup"><span data-stu-id="70ba4-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="70ba4-133">寫入 hello 資料框架 toolocal 檔案</span><span class="sxs-lookup"><span data-stu-id="70ba4-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="70ba4-134">將 hello 資料 tooAzure blob 上傳，如下所示：</span><span class="sxs-lookup"><span data-stu-id="70ba4-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="70ba4-135">現在可以從 hello blob 使用讀取 hello 資料 hello Azure Machine Learning[匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)模組囉 」 畫面下方所示：</span><span class="sxs-lookup"><span data-stu-id="70ba4-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![讀取器 Blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

