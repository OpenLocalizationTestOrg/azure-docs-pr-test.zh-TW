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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>使用 Pandas 瀏覽 Azure blob 儲存體中的資料
本文件涵蓋 tooexplore 資料儲存在 Azure blob 容器使用[熊](http://pandas.pydata.org/)Python 封裝。

hello 下列**功能表**連結 tootopics 描述 toouse 工具 tooexplore 資料，從不同的儲存體環境的方式。 這項工作是在 hello 步驟[資料科學程序]()。

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>必要條件
本文假設您已經：

* 建立 Azure 儲存體帳戶。 如需指示，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* 將您的資料儲存在 Azure blob 儲存體帳戶。 如果您需要的指示，請參閱[移動資料 tooand 從 Azure 儲存體](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Hello 資料載入熊資料框架
tooexplore 和管理資料集，它必須先從 hello blob 來源 tooa 本機檔案，然後可以載入熊資料框架中下載。 以下是此程序的 hello 步驟 toofollow:

1. 從 Azure 下載 hello 資料以下列 Python 程式碼範例使用 blob 服務的 hello 的 blob。 取代下列程式碼的特定值的 hello 中的 hello 變數： 
   
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
2. 在從 hello 熊資料範圍內的讀取 hello 資料下載檔案。
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

現在您已準備好 tooexplore hello 資料，並產生此資料集上的功能。

## <a name="blob-dataexploration"></a>使用 Pandas 的資料探索範例
以下是幾個方法的範例使用熊 tooexplore 資料：

1. 檢查 hello**數目的資料列和資料行** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **檢查**hello 第一個或最後幾個**列**中下列資料集的 hello:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. 檢查 hello**資料型別**每個資料行匯入為使用下列範例程式碼的 hello
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. 檢查 hello**基本統計資料**的 hello 中的資料行，如下所示 hello 資料集
   
        dataframe_blobdata.describe()
5. 尋找在 hello 的每個資料行值的項目，如下所示
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **計算遺漏值**與 hello 實際數目，使用下列範例程式碼的 hello 每個資料行中的項目
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. 如果您有**遺漏值**hello 資料中的特定資料行，也可以加以卸除，如下所示：
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   另一個方式 tooreplace 遺漏的值是使用 hello 模式函式：
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. 建立**長條圖**繪製使用變數的分類收納 tooplot hello 發佈數目可變的    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. 查看**相互關聯**之間使用 scatterplot 或 hello 內建的相互關聯的函式的變數
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

