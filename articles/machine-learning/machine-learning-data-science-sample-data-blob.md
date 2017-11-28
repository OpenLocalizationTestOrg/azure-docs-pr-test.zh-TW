---
title: "Azure Blob 儲存體中的取樣資料 | Microsoft Docs"
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="e6137-103"><a name="heading"></a>Azure blob 儲存體中的取樣資料</span><span class="sxs-lookup"><span data-stu-id="e6137-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="e6137-104">本文件說明為儲存於 Azure blob 儲存體中的資料進行取樣的方法，您可以利用程式設計方式加以下載，然後使用以 Python 撰寫的程序進行取樣。</span><span class="sxs-lookup"><span data-stu-id="e6137-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="e6137-105">以下**功能表**所連結的主題會說明如何從各種不同儲存體環境進行資料取樣。</span><span class="sxs-lookup"><span data-stu-id="e6137-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="e6137-106">**為何要對您的資料進行取樣？**</span><span class="sxs-lookup"><span data-stu-id="e6137-106">**Why sample your data?**</span></span>
<span data-ttu-id="e6137-107">如果您規劃分析的資料集很龐大，通常最好是對資料進行向下取樣，將資料縮減為更小但具代表性且更容易管理的大小。</span><span class="sxs-lookup"><span data-stu-id="e6137-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="e6137-108">這有助於資料了解、探索和功能工程。</span><span class="sxs-lookup"><span data-stu-id="e6137-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="e6137-109">它在 Cortana 分析程序中扮演的角色是能夠快速建立資料處理函式與機器學習服務模型的原型。</span><span class="sxs-lookup"><span data-stu-id="e6137-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="e6137-110">這個取樣工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="e6137-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="e6137-111">下載和降低取樣資料</span><span class="sxs-lookup"><span data-stu-id="e6137-111">Download and down-sample data</span></span>
1. <span data-ttu-id="e6137-112">從下列 Python 程式碼範例中，使用 Blob 服務，從 Azure Blob 儲存體下載資料。</span><span class="sxs-lookup"><span data-stu-id="e6137-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="e6137-113">從上述下載的檔案中將資料讀取至 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="e6137-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="e6137-114">使用 `numpy` 的 `random.choice` 以進行降低取樣資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e6137-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="e6137-115">現在您可以使用上述具有 1% 樣本的資料框架，進行進一步探索和功能產生。</span><span class="sxs-lookup"><span data-stu-id="e6137-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="e6137-116"><a name="heading"></a>將資料上傳並將其讀入 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e6137-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="e6137-117">您可以使用下列程式碼範例，對資料進行向下取樣，並直接在 Azure Machine Learning 中使用它：</span><span class="sxs-lookup"><span data-stu-id="e6137-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="e6137-118">將資料框架寫入本機檔案</span><span class="sxs-lookup"><span data-stu-id="e6137-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="e6137-119">使用下列程式碼範例，將本機檔案上傳至 Azure Blob：</span><span class="sxs-lookup"><span data-stu-id="e6137-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="e6137-120">使用 Azure Machine Learning [匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 從 Azure Blob 讀取資料，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e6137-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![讀取器 Blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

