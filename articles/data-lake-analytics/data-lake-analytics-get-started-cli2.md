---
title: "開始使用 Azure CLI 2.0 的 Azure Data Lake Analytics aaaGet |Microsoft 文件"
description: "了解如何 toouse hello Azure 命令列介面 2.0 toocreate Data Lake Analytics 帳戶中建立使用 U SQL Data Lake Analytics 工作並送出 hello 作業。 "
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
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>使用 Azure CLI 2.0 開始使用 Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

在本教學課程中，您會開發一個作業可讀取定位字元分隔值 (TSV) 檔案，並將該檔案轉換為逗點分隔值 (CSV) 檔案。 透過相同的教學課程使用其他支援的 hello toogo 工具，在這一節的 hello 最上層使用 hello 下拉式清單。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須具備下列項目 hello:

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure CLI 2.0**. 請參閱 [安裝和設定 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。

## <a name="log-in-tooazure"></a>登入 tooAzure

toolog tooyour Azure 訂用帳戶中：

```
azurecli
az login
```

您要求的 toobrowse tooa URL，而且輸入驗證碼。  然後依照 hello 指示 tooenter 您的認證。

一旦您登入，hello 登入的命令會列出訂用帳戶。

toouse 特定訂用帳戶：

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶
您需要 Data Lake Analytics 帳戶，才能執行作業。 toocreate Data Lake Analytics 帳戶，您必須指定下列項目 hello:

* **Azure 資源群組**。 Data Lake Analytics 帳戶必須建立在 Azure 資源群組內。 [Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可讓您與您的應用程式，為群組中的 hello 資源 toowork。 您可以部署、 更新或刪除 hello 資源的所有應用程式在單一、 協調作業。  

toolist hello 現有資源群組您的訂用帳戶底下：

```
az group list
```

toocreate 新的資源群組：

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Data Lake Analytics 帳戶名稱**。 每一個 Data Lake Analytics 帳戶都有名稱。
* **位置**。 使用其中一個支援 Data Lake Analytics 的 hello Azure 資料中心。
* **預設 Data Lake Store 帳戶**：每個 Data Lake Analytics 帳戶都有一個預設的 Data Lake Store 帳戶。

toolist hello 現有 Data Lake Store 帳戶：

```
az dls account list
```

toocreate 新的 Data Lake Store 帳戶：

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

使用下列語法 toocreate Data Lake Analytics 帳戶的 hello:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

建立帳戶後，您可以使用下列命令 toolist hello 帳戶 hello，並顯示 帳戶詳細資料：

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>上傳資料 tooData 湖存放區
在本教學課程中，您會處理一些搜尋記錄檔。  hello 搜尋記錄檔可以儲存在資料湖存放區或 Azure Blob 儲存體中。

hello Azure 入口網站提供使用者介面複製某些範例資料檔案 toohello 預設 Data Lake Store 帳戶，包括搜尋記錄檔。 請參閱[準備來源資料](data-lake-analytics-get-started-portal.md)tooupload hello 資料 toohello 預設 Data Lake Store 帳戶。

使用 CLI 2.0 tooupload 檔案中使用下列命令的 hello:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Data Lake Analytics 也可存取 Azure Blob 儲存體。  上傳資料 tooAzure Blob 儲存體，請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](../storage/common/storage-azure-cli.md)。

## <a name="submit-data-lake-analytics-jobs"></a>提交 Data Lake Analytics 工作
hello Data Lake Analytics 工作是以 hello U-SQL 語言撰寫。 toolearn 進一步了解 U-SQL，請參閱[開始使用 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)和[U-SQL 語言 eence](http://go.microsoft.com/fwlink/?LinkId=691348)。

**toocreate Data Lake Analytics 作業指令碼**

使用下列的 U-SQL 指令碼，建立文字檔案，並將儲存 hello 文字檔案 tooyour 工作站：

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

此 U-SQL 指令碼會讀取 hello 來源資料檔案使用**Extractors.Tsv()**，然後建立使用 csv 檔案**Outputters.Csv()**。

請勿修改 hello 兩個路徑，除非您將 hello 原始程式檔複製到不同的位置。  Data Lake Analytics 建立 hello 輸出資料夾，如果不存在。

它是簡單 toouse 預設 Data Lake Store 帳戶中儲存的檔案相對路徑。 您也可以使用絕對路徑。  例如：

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

您必須使用連結的儲存體帳戶中的絕對路徑 tooaccess 檔案。  檔案儲存在連結的 Azure 儲存體帳戶中的 hello 語法為：

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> 不支援使用公用 blob 的 Azure Blob 容器。      
> 不支援使用公用容器的 Azure Blob 容器。      
>

**toosubmit 工作**

使用下列語法 toosubmit 作業 hello。

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

例如：

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**toolist 作業與顯示工作詳細資料**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**toocancel 工作**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>擷取作業結果

作業完成之後，您可以使用下列命令 toolist hello 輸出檔案的 hello 和下載 hello 檔案：

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

使用 hello `az dla job pipeline` toosee hello 管線資訊先前已送出工作的命令。

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

使用 hello`az dla job recurrence`命令 toosee hello 循環資訊，如先前已提交的工作。

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>後續步驟

* toosee hello 資料湖分析 CLI 2.0 參考文件，請參閱[Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla)。
* toosee hello 資料湖存放區 CLI 2.0 參考文件，請參閱[Data Lake Store](https://docs.microsoft.com/cli/azure/dls)。
* toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。
