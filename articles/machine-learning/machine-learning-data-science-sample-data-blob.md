---
title: "aaaSample 資料在 Azure blob 儲存體 |Microsoft 文件"
description: "Azure blob 儲存體中的取樣資料"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="ee586-103"><a name="heading"></a>Azure blob 儲存體中的取樣資料</span><span class="sxs-lookup"><span data-stu-id="ee586-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="ee586-104">本文件說明為儲存於 Azure blob 儲存體中的資料進行取樣的方法，您可以利用程式設計方式加以下載，然後使用以 Python 撰寫的程序進行取樣。</span><span class="sxs-lookup"><span data-stu-id="ee586-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="ee586-105">hello 下列**功能表**連結 tootopics 描述如何從各種不同的儲存體環境 toosample 資料。</span><span class="sxs-lookup"><span data-stu-id="ee586-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="ee586-106">**為何要對您的資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="ee586-106">**Why sample your data?**</span></span>
<span data-ttu-id="ee586-107">如果您計劃 tooanalyze hello 資料集很大，它通常是個不錯的主意 toodown 範例 hello 資料 tooreduce 它 tooa 小型但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="ee586-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="ee586-108">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="ee586-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="ee586-109">Hello Cortana 分析程序在其角色將是 tooenable 快速原型化的 hello 資料處理函式和機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="ee586-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="ee586-110">此取樣工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。</span><span class="sxs-lookup"><span data-stu-id="ee586-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="ee586-111">下載和降低取樣資料</span><span class="sxs-lookup"><span data-stu-id="ee586-111">Download and down-sample data</span></span>
1. <span data-ttu-id="ee586-112">使用從下列 hello hello blob 服務的 Azure blob 儲存體下載 hello 資料的範例 Python 程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee586-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="ee586-113">在上方所下載的 hello 檔案從熊資料範圍內讀取資料。</span><span class="sxs-lookup"><span data-stu-id="ee586-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="ee586-114">向下範例 hello 資料使用 hello`numpy`的`random.choice`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee586-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="ee586-115">現在您可以使用與 hello 百分之 1 範例進行進一步探索和功能產生的資料框架上方的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee586-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="ee586-116"><a name="heading"></a>將資料上傳並將其讀入 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ee586-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="ee586-117">您可以使用下列範例程式碼 toodown 範例 hello 資料 hello，並直接在 Azure Machine Learning 中使用它：</span><span class="sxs-lookup"><span data-stu-id="ee586-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="ee586-118">寫入 hello 資料框架 tooa 本機檔案</span><span class="sxs-lookup"><span data-stu-id="ee586-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="ee586-119">上傳 hello 本機檔案 tooan Azure blob，使用下列範例程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee586-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="ee586-120">讀取 hello Azure blob，使用 Azure Machine Learning 中的 hello 資料[匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)hello 圖所示：</span><span class="sxs-lookup"><span data-stu-id="ee586-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![讀取器 Blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

