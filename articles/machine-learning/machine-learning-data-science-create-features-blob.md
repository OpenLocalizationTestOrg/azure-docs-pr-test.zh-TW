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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>使用 Panda 建立 Azure blob 儲存體資料功能
本文件說明如何 toocreate 功能的資料儲存在 Azure blob 容器使用 hello[熊](http://pandas.pydata.org/)Python 封裝。 之後大綱如何 tooload hello 資料至貓熊資料框架，它會顯示如何使用 Python 指令碼搭配指標值和分類收納功能 toogenerate 類別特徵。

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。 這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

## <a name="prerequisites"></a>必要條件
本文假設您已建立 Azure Blob 儲存體帳戶，並將您的資料儲存在該處。 如果您需要指示 tooset 設定帳戶，請參閱[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Hello 資料載入熊資料框架
在順序 toodo 探索和管理資料集，它必須從 hello blob 來源 tooa 本機檔案然後可以載入熊資料框架中下載。 以下是此程序的 hello 步驟 toofollow:

1. 從 Azure 下載 hello 資料以下列範例使用 blob 服務的 Python 程式碼的 hello 的 blob。 以您的特定值取代 hello 下列的程式碼中的 hello 變數：
   
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

## <a name="blob-featuregen"></a>功能產生
hello 下兩節會顯示與指標值分類收納 toogenerate 類別特徵功能使用 Python 指令碼。

### <a name="blob-countfeature"></a>以指標值為基礎的功能產生
類別功能可使用如下的方式來建立：

1. 檢查 hello 分佈 hello 類別資料行：
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. 產生每個 hello 資料行值的指標值
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. 加入原始資料框架 hello 與 hello 指標資料行
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. 移除 hello 原始變數本身：
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>分類收納功能產生
若要產生分類收納功能，我們可使用如下的方式繼續進行：

1. 加入資料行 toobin 數值資料行序列
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. 轉換布林值變數的分類收納 tooa 的序列
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. 最後，聯結 hello dummy 變數回 toohello 原始資料框架
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>將資料寫入回 tooAzure blob 和 Azure Machine Learning 中使用
您已經瀏覽 hello 資料及建立 hello 所需的功能之後，您可以上傳 hello 資料 (取樣或特徵化) tooan Azure blob，然後使用下列步驟的 hello Azure Machine Learning 中使用它： 請注意，可以在 hello 中建立額外的功能Azure Machine Learning Studio 以及。

1. 寫入 hello 資料框架 toolocal 檔案
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. 將 hello 資料 tooAzure blob 上傳，如下所示：
   
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
3. 現在可以從 hello blob 使用讀取 hello 資料 hello Azure Machine Learning[匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)模組囉 」 畫面下方所示：

![讀取器 Blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

