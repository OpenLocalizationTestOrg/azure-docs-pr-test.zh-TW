---
title: "處理使用進階分析的 Azure Blob 資料 | Microsoft Docs"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="1ae3b-103"><a name="heading"></a>處理使用進階分析的 Azure Blob 資料</span><span class="sxs-lookup"><span data-stu-id="1ae3b-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="1ae3b-104">本文件涵蓋探索資料以及從 Azure Blob 儲存體中儲存的資料產生功能的說明。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="1ae3b-105">將資料載入至 Pandas 資料框架</span><span class="sxs-lookup"><span data-stu-id="1ae3b-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="1ae3b-106">若要探索和操作資料集，必須從 Blob 來源將資料集下載至本機檔案，然後將其載入 Pandas 資料框架中。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="1ae3b-107">以下是此程序的遵循步驟：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="1ae3b-108">使用 Blob 服務，透過下列 Python 程式碼範例，從 Azure Blob 下載資料。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="1ae3b-109">使用您的特定值來取代下列程式碼中的變數：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="1ae3b-110">從下載的檔案中，將資料讀取至 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="1ae3b-111">現在您已經準備好探索資料並在此資料集上產生功能。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="1ae3b-112"><a name="blob-dataexploration"></a>資料探索</span><span class="sxs-lookup"><span data-stu-id="1ae3b-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="1ae3b-113">以下是數個可使用 Pandas 探索資料的範例方式：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="1ae3b-114">檢查資料列和資料行的數目</span><span class="sxs-lookup"><span data-stu-id="1ae3b-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="1ae3b-115">檢查資料集中的前幾個或最後幾個資料列，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="1ae3b-116">檢查使用下列程式碼範例匯入之每個資料行的資料類型</span><span class="sxs-lookup"><span data-stu-id="1ae3b-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="1ae3b-117">檢查資料集中資料行的基本統計資料，如下所示</span><span class="sxs-lookup"><span data-stu-id="1ae3b-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="1ae3b-118">查看每個資料行值的項目數，如下所示</span><span class="sxs-lookup"><span data-stu-id="1ae3b-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="1ae3b-119">使用下列程式碼範例，來計算每個資料行中的遺漏值與實際項目數</span><span class="sxs-lookup"><span data-stu-id="1ae3b-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="1ae3b-120">如果您在資料的特定資料行中有遺漏值，則可卸除它們，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="1ae3b-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="1ae3b-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="1ae3b-122">取代遺漏值的另一種方式是使用模式函式：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="1ae3b-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="1ae3b-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="1ae3b-124">使用變動數目的分類收納組來建立長條圖，以繪製變數的分佈</span><span class="sxs-lookup"><span data-stu-id="1ae3b-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="1ae3b-125">使用散佈圖或使用內建的相互關聯函式，來查看變數之間的相互關聯</span><span class="sxs-lookup"><span data-stu-id="1ae3b-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="1ae3b-126"><a name="blob-featuregen"></a>功能產生</span><span class="sxs-lookup"><span data-stu-id="1ae3b-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="1ae3b-127">我們可以使用 Python 來產生功能，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="1ae3b-128"><a name="blob-countfeature"></a>以指標值為基礎的功能產生</span><span class="sxs-lookup"><span data-stu-id="1ae3b-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="1ae3b-129">類別功能可使用如下的方式來建立：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="1ae3b-130">檢查類別資料行的分佈：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="1ae3b-131">產生每個資料行值的指標值</span><span class="sxs-lookup"><span data-stu-id="1ae3b-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="1ae3b-132">將指標資料行與原始資料框架聯結在一起</span><span class="sxs-lookup"><span data-stu-id="1ae3b-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="1ae3b-133">移除原始變數本身：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="1ae3b-134"><a name="blob-binningfeature"></a>分類收納功能產生</span><span class="sxs-lookup"><span data-stu-id="1ae3b-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="1ae3b-135">若要產生分類收納功能，我們可使用如下的方式繼續進行：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="1ae3b-136">新增一系列的資料行，以分類收納數值資料行</span><span class="sxs-lookup"><span data-stu-id="1ae3b-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="1ae3b-137">將分類收納轉換為一系列的布林值變數</span><span class="sxs-lookup"><span data-stu-id="1ae3b-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="1ae3b-138">最後，將虛擬變數新增回原始資料框架中</span><span class="sxs-lookup"><span data-stu-id="1ae3b-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="1ae3b-139"><a name="sql-featuregen"></a>將資料寫回 Azure Blob 並在 AzureMachine Learning 中取用</span><span class="sxs-lookup"><span data-stu-id="1ae3b-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="1ae3b-140">在您探索資料和建立必要功能後，可以上傳資料 (取樣性或功能性) 至 Azure Blob，並在 Azure Machine Learning 中透過下列步驟取用資料：請注意，您也可以在 Azure Machine Learning Studio 中建立其他功能。</span><span class="sxs-lookup"><span data-stu-id="1ae3b-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="1ae3b-141">將資料框架寫入本機檔案中</span><span class="sxs-lookup"><span data-stu-id="1ae3b-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="1ae3b-142">將資料上傳至 Azure Blob，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="1ae3b-143">現在您可以使用 Azure Machine Learning [匯入資料][import-data]模組從 Blob 讀取資料，如以下畫面所示：</span><span class="sxs-lookup"><span data-stu-id="1ae3b-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![讀取器 Blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

