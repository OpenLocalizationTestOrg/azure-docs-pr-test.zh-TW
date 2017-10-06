---
title: "開始使用 Azure PowerShell 的 Azure Data Lake Analytics aaaGet |Microsoft 文件"
description: "使用 Azure PowerShell toocreate Data Lake Analytics 帳戶、 建立使用 U SQL Data Lake Analytics 工作和送出 hello 作業。 "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>使用 Azure PowerShell 開始使用 Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

了解如何 toouse Azure PowerShell toocreate Azure Data Lake Analytics 帳戶，然後送出並執行 U SQL 作業。 如需有關 Data Lake Analytics 的詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。

## <a name="prerequisites"></a>必要條件

開始本教學課程之前，您必須擁有下列資訊的 hello:

* **Azure Data Lake Analytics 帳戶**。 請參閱[開始使用 Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)。
* **具有 Azure PowerShell 的工作站**。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="log-in-tooazure"></a>登入 tooAzure

本教學課程假設您已熟悉如何使用 Azure PowerShell。 特別是，您需要 tooknow 如何 toolog tooAzure 中的。 請參閱 hello[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps)如果您需要協助。

toolog 入訂用帳戶名稱：

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

而不是 hello 訂用帳戶名稱，您也可以使用訂用帳戶 id toolog 中：

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

如果成功，這個命令的 hello 輸出看起來 hello 下列文字：

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>準備 hello 教學課程

在此教學課程中的 hello PowerShell 程式碼片段會使用這些變數 toostore 這項資訊：

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>取得 Data Lake Analytics 帳戶的相關資訊

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>提交 U-SQL 作業

建立 PowerShell 變數 toohold hello U-SQL 指令碼。

```
$script = @"
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

"@
```

送出 hello 指令碼。

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

或者，您無法將 hello 指令碼儲存到檔案，並送出 hello 下列命令：

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


取得 hello 特定作業的狀態。 繼續使用這個指令程式，直到您看到 hello 工作完成為止。

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

而不是反覆呼叫 Get AdlAnalyticsJob，直到工作完成，您可以使用 hello 等候 AdlJob cmdlet。

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

下載 hello 輸出檔。

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>另請參閱
* toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。
* toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。
* 針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。
