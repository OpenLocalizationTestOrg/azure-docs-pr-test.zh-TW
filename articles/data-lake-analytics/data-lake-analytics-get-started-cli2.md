---
title: "使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何透過 Azure 命令列介面 2.0 建立 Data Lake Analytics 帳戶、使用 U-SQL 建立 Data Lake Analytics 作業，以及提交作業。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: fe2b84aac718ff5eddd4d73b5dc2120362952c1e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

在本教學課程中，您會開發一個作業可讀取定位字元分隔值 (TSV) 檔案，並將該檔案轉換為逗點分隔值 (CSV) 檔案。 若要使用其他支援的工具進行同一個教學課程，請使用此區段最上方的下拉式清單。

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備下列項目：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure CLI 2.0**. 請參閱 [安裝和設定 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。

## <a name="log-in-to-azure"></a>登入 Azure

若要登入您的 Azure 訂用帳戶：

```
azurecli
az login
```

系統會要求您瀏覽至 URL，然後輸入驗證碼。  然後遵循指示輸入您的認證。

一旦您已登入後，登入命令會列出您的訂用帳戶。

若要使用特定的訂用帳戶︰

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶
您需要 Data Lake Analytics 帳戶，才能執行作業。 若要建立 Data Lake Analytics 帳戶，您必須指定下列項目：

* **Azure 資源群組**。 Data Lake Analytics 帳戶必須建立在 Azure 資源群組內。 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 可讓您將應用程式中的資源做為群組使用。 您可以透過單一、協調的作業，將應用程式的所有資源進行部署、更新或刪除。  

若要列出訂用帳戶下的現有資源群組：

```
az group list
```

若要建立新的資源群組：

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Data Lake Analytics 帳戶名稱**。 每一個 Data Lake Analytics 帳戶都有名稱。
* **位置**。 使用其中一個支援 Data Lake Analytics 的 Azure 資料中心。
* **預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。

若要列出現有的 Data Lake Store 帳戶：

```
az dls account list
```

建立新的 Data Lake Store 帳戶：

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

使用下列語法建立 Data Lake Analytics 帳戶：

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

建立帳戶後，您可以使用下列命令列出帳戶，並顯示帳戶詳細資料︰

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a>將資料上傳至 Data Lake Store
在本教學課程中，您會處理一些搜尋記錄檔。  搜尋記錄檔可以儲存在 Data Lake Store 或 Azure Blob 儲存體中。

Azure 入口網站會提供使用者介面，可將範例資料檔案複製到預設的 Data Lake Store 存放區帳戶，其中包括搜尋記錄檔案。 若要將資料上傳至預設 Data Lake Store 帳戶，請參閱 [準備來源資料](data-lake-analytics-get-started-portal.md) 。

若要使用 CLI 2.0 上傳檔案，請使用下列命令：

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Data Lake Analytics 也可存取 Azure Blob 儲存體。  若要將資料上傳至 Azure Blob 儲存體，請參閱 [使用 Azure CLI 搭配 Azure 儲存體](../storage/common/storage-azure-cli.md)。

## <a name="submit-data-lake-analytics-jobs"></a>提交 Data Lake Analytics 工作
Data Lake Analytics 工作是以 U-SQL 語言撰寫。 若要深入了解 U-SQL，請參閱[開始使用 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)和 [U-SQL 語言參考](http://go.microsoft.com/fwlink/?LinkId=691348)。

**建立 Data Lake Analytics 工作指令碼**

使用下列 U-SQL 指令碼建立文字檔，並將該檔案儲存到您的工作站：

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

此 U-SQL 指令碼會使用 **Extractors.Tsv()** 讀取來源資料檔案，然後使用 **Outputters.Csv()** 建立 csv 檔案。

除非您將來源檔案複製到其他位置，否則請勿修改這兩個路徑。  Data Lake Analytics 會建立輸出資料夾 (若尚未建立)。

使用儲存在預設 Data Lake Store 帳戶中檔案的相對路徑，是比較容易的方法。 您也可以使用絕對路徑。  例如：

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

您必須使用絕對路徑存取連結儲存體帳戶中的檔案。  儲存在連結 Azure 儲存體帳戶中之檔案的語法是：

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> 不支援使用公用 blob 的 Azure Blob 容器。      
> 不支援使用公用容器的 Azure Blob 容器。      
>

**提交作業**

使用以下語法提交作業。

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

例如：

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**若要列出作業並顯示作業詳細資料**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**取消作業**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>擷取作業結果

作業完成之後，您可以使用下列命令列出該輸出檔案，並下載檔案：

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

例如：

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>管線和週期

**取得管線和週期的相關資訊**

使用 `az dla job pipeline` 命令來查看先前提交作業的管線資訊。

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

使用 `az dla job recurrence` 命令來查看先前提交作業的週期資訊。

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>後續步驟

* 若要查看 Data Lake Analytics CLI 2.0 參考文件，請參閱 [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla)。
* 若要查看 Data Lake Store CLI 2.0 參考文件，請參閱 [Data Lake Store](https://docs.microsoft.com/cli/azure/dls)。
* 若要了解更複雜的查詢，請參閱 [使用 Azure Data Lake Analytics 來分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。
