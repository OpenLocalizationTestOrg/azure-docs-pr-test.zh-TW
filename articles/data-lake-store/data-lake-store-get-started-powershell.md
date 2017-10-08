---
title: "開始使用 Azure Data Lake Store 的 aaaUse PowerShell tooget |Microsoft 文件"
description: "使用 Azure PowerShell toocreate Data Lake Store 帳戶以及執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>使用 Azure PowerShell 開始使用 Azure 資料湖分析存放區
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

了解如何 toouse Azure PowerShell toocreate Azure 資料湖存放區帳戶和執行基本作業，例如建立資料夾、 上傳和下載資料檔，刪除您的帳戶，依此類推。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更新版本**。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="authentication"></a>驗證
本文使用更簡單的驗證方法提示的 tooenter 所在的資料湖存放區與您的 Azure 帳戶的認證。 hello 存取層級 tooData Lake Store 帳戶和檔案系統，然後係由 hello hello 登入的使用者存取層級。 不過，有一些其他方法為以及 tooauthenticate 與資料湖存放區，也就是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)或[服務對服務驗證](data-lake-store-authenticate-using-active-directory.md)。

## <a name="create-an-azure-data-lake-store-account"></a>建立 Azure 資料湖存放區帳戶
1. 從您的桌面上，開啟新的 Windows PowerShell 視窗中，輸入下列程式碼片段 toolog tooyour Azure 帳戶中的 hello、 設定 hello 訂用帳戶，並註冊 hello 資料湖存放區提供者。 當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶 admininistrators/擁有者：

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Azure Data Lake Store 帳戶與 Azure 資源群組相關聯。 從建立 Azure 資源群組開始。

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![建立 Azure 資源群組](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "建立 Azure 資源群組")
3. 建立 Azure Data Lake Store 帳戶。 您指定的 hello 名稱只能包含小寫字母和數字。

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![建立 Azure Data Lake Store 帳戶](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "建立 Azure Data Lake Store 帳戶")
4. 確認已成功建立 hello 帳戶。

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    這應該是輸出的 hello **True**。

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>在您的 Azure 資料湖存放區中建立目錄結構
您可以在您的 Azure Data Lake Store 帳戶 toomanage 下建立目錄，並儲存資料。

1. 指定根目錄。

        $myrootdir = "/"
2. 建立新的目錄稱為**mynewdirectory** hello 指定根目錄下。

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. 請確認已成功建立該 hello 新目錄。

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    它應該會顯示類似 hello 下列輸出：

    ![確認目錄](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "確認目錄")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>上傳資料 tooyour Azure Data Lake Store
您可以上傳資料 tooData 湖存放區直接在 hello 根層級或 tooa 目錄 hello 帳戶中建立。 下列的 hello 片段會示範如何 tooupload 某些範例資料 toohello 目錄 (**mynewdirectory**) 您建立 hello 前一節中。

如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。 下載 hello 檔案，並將它儲存在您的電腦，例如 C:\sampledata\ 上的本機目錄。

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>重新命名、下載與刪除資料湖存放區中的資料
toorename 檔案，使用下列命令的 hello:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload 檔案，使用下列命令的 hello:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete 檔案，使用下列命令的 hello:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

出現提示時，輸入**Y** toodelete hello 項目。 如果您有多個檔案 toodelete，您可以提供以逗號分隔的所有 hello 路徑。

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>刪除 Azure 資料湖存放區帳戶
使用下列命令 toodelete hello Data Lake Store 帳戶。

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

出現提示時，輸入**Y** toodelete hello 帳戶。

## <a name="performance-guidance-while-using-powershell"></a>使用 PowerShell 時的效能指引

以下是最重要的設定，可以是微調的 tooget hello 最佳效能，同時使用 Data Lake Store 的 PowerShell toowork hello:

| 屬性            | 預設值 | 說明 |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | 這個參數可讓您上傳或下載每個檔案的平行執行緒 toochoose hello 數目。 這個數字代表 hello 執行緒數目上限可配置每個檔案，但您可能會收到較少的執行緒，根據您的案例 (例如： 如果您要上傳的 1 KB 的檔案，就會收到一個執行緒，即使您尋求 20 個執行緒)。  |
| ConcurrentFileCount | 10      | 這個參數特別用於上傳或下載資料夾。 這個參數會決定 hello 並行上傳或下載的檔案數目。 這個數字代表 hello 並行的檔案可上傳或下載一次的數目上限，但您可能會收到較少的並行存取，根據您的案例 (例如： 如果您要上傳兩個檔案，您就會取得兩個並行的檔案上傳，即使您要求15)。 |

**範例**

此命令會從 Azure Data Lake Store toohello 使用者的本機磁碟機使用 20 個執行緒，每個檔案和 100 個並行的檔案下載檔案。

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>我要如何判斷 hello 值 tooset 這些參數的？

以下是一些您可以使用的指引。

* **步驟 1： 決定 hello 總執行緒計數**-一開始應該計算 hello 總執行緒計數 toouse。 一般來說，您應該針對每個實體核心使用 6 個執行緒。

        Total thread count = total physical cores * 6

    **範例**

    假設您正在執行 hello PowerShell 命令從 D14 VM，在具有 16 個核心

        Total thread count = 16 cores * 6 = 96 threads


* **步驟 2： 計算 PerFileThreadCount** -我們 PerFileThreadCount 根據 hello hello 檔案大小來計算。 小於 2.5 GB 的檔案，沒有任何需要 toochange 此參數因為 hello 預設值是 10 已足夠。 大於 2.5 GB 的檔案，您應該使用 10 個執行緒的 hello 基底 hello 第一個有 2.5 GB，並加入 1 個執行緒的每個額外的 256 MB 增加檔案大小。 如果您要複製包含各種檔案大小的資料夾，請考慮將其分組為相似的檔案大小。 檔案大小不相近可能會導致非最佳的效能。 如果不可能 toogroup 類似檔案大小，您應該設定 PerFileThreadCount hello 最大檔案大小為基礎。

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **範例**

    我們假設您有 100 個檔案，範圍介於 1 GB too10GB，使用的 hello hello 最大為 10 GB 檔案大小的方程式，它會讀取 hello 如下。

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **步驟 3： 計算 ConcurrentFilecount** -使用 hello 總執行緒計數和 PerFileThreadCount toocalculate ConcurrentFileCount 取決於下列方程式 hello。

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **範例**

    根據我們使用 hello 範例值

        96 = 40 * ConcurrentFileCount

    因此， **ConcurrentFileCount**是**2.4**，我們可以藉由四捨五入太其中**2**。

### <a name="further-tuning"></a>進一步微調

您可能需要進一步調整因為沒有與檔案大小 toowork 的範圍。 上述計算 hello 運作 hello 檔案的全部或大部分是較大且更接近 toohello 10 GB 範圍的情況。 相反地，如果有許多不同的檔案大小且很多檔案比較小，您可以減少 PerFileThreadCount。 藉由減少 hello PerFileThreadCount，我們可以增加 ConcurrentFileCount。 因此，如果我們假設，我們檔案的最小 hello 5 GB 範圍中，我們可以重新執行我們的計算：

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

因此， **ConcurrentFileCount**會立即 96/20，也就是 4.8 四捨五入太**4**。

您可以繼續 tootune 這些設定變更 hello **PerFileThreadCount**向上和向下的檔案大小的 hello 分佈而定。

### <a name="limitation"></a>限制

* **檔案數目小於 ConcurrentFileCount**： 如果您要上傳的檔案的 hello 數目小於 hello **ConcurrentFileCount**您計算，然後您應該降低**ConcurrentFileCount**檔案 toobe 等於 toohello 數目。 您可以使用任何剩餘的執行緒 tooincrease **PerFileThreadCount**。

* **太多執行緒**： 如果您增加執行緒計數太多而不會增加您的叢集大小、 hello 造成效能降低的問題。 內容切換 hello CPU 上時，可以是競爭問題。

* **不足的並行**： 如果 hello 並行處理並不敷使用，則您的叢集可能會太小。 這樣會提供您多個並行叢集中，您可以增加 hello 節點數目。

* **節流錯誤**︰如果並行處理量太高，您可能會看到節流錯誤。 如果您看見期間發生節流錯誤，您應該降低 hello 並行或與我們連絡。

## <a name="next-steps"></a>後續步驟
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)

