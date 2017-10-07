---
title: "aaaProcess Azure blob 與進階分析的資料 |Microsoft 文件"
description: "處理 Azure Blob 儲存體中的資料。"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>處理使用進階分析的 Azure Blob 資料
本文件涵蓋探索資料以及從 Azure Blob 儲存體中儲存的資料產生功能的說明。 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Hello 資料載入熊資料框架
在訂單 tooexplore 和管理資料集，它必須從 hello blob 來源 tooa 本機檔案然後可以載入熊資料框架中下載。 以下是此程序的 hello 步驟 toofollow:

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

## <a name="blob-dataexploration"></a>資料探索
以下是幾個方法的範例使用熊 tooexplore 資料：

1. 檢查資料列和資料行的 hello 數目 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. 第一次檢查 hello 或最後幾個資料列中 hello 資料集，如下所示：
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. 檢查每個資料行匯入為使用下列範例程式碼的 hello hello 資料類型
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. 請檢查 hello hello hello 資料集中的資料行的基本統計資料，如下所示
   
        dataframe_blobdata.describe()
5. 尋找在 hello 的每個資料行值的項目，如下所示
   
        dataframe_blobdata['<column_name>'].value_counts()
6. 與 hello 實際數目，使用下列範例程式碼的 hello 每個資料行中的項目計數遺漏值
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. 如果您在 hello 資料有遺漏值的特定資料行，也可以加以卸除，如下所示：
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   另一個方式 tooreplace 遺漏的值是使用 hello 模式函式：
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. 建立使用變動數目的變數的分類收納 tooplot hello 分佈的長條圖圖    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. 查看使用 scatterplot 或 hello 內建的相互關聯的函式的變數之間的相互關聯
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>功能產生
我們可以使用 Python 來產生功能，如下所示：

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
3. 現在可以從 hello blob 使用讀取 hello 資料 hello Azure Machine Learning[匯入資料][ import-data]模組囉 」 畫面下方所示：

![讀取器 Blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

