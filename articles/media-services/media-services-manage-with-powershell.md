---
title: "aaaManage 使用 PowerShell 的 Azure 媒體服務帳戶"
description: "了解如何 toomanage Azure Media Services 帳戶的 PowerShell cmdlet。"
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>利用 PowerShell 管理 Azure Media Services 帳戶
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe 無法 toocreate Azure Media Services 帳戶，您必須有 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 免費試用</a>。
> 
> 

## <a name="overview"></a>概觀
本文列出 hello Azure PowerShell cmdlet 的 Azure 媒體服務 (AMS) hello Azure Resource Manager 架構中。 hello cmdlet 存在於 hello **Microsoft.Azure.Commands.Media**命名空間。

## <a name="versions"></a>版本
**ApiVersion**："2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
建立媒體服務。

### <a name="syntax"></a>語法
參數集︰StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

參數集︰StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | Name |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

**-Location &lt;String&gt;**

指定 hello 媒體服務的 hello 資源的位置。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |2 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-StorageAccountId &lt;String&gt;**

指定與 hello 媒體服務相關聯的主要儲存體帳戶。

* 新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。
* hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |3 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 參數集名稱 |StorageAccountIdParamSet |
| 接受萬用字元？ |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

指定與 hello 媒體服務相關聯的儲存體帳戶。

* 新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。
* hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。
* 只可以指定一個主要儲存體帳戶。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |3 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 參數集名稱 |StorageAccountsParamSet |
| 接受萬用字元？ |false |

**-Tags &lt;Hashtable&gt;**

指定雜湊表的 hello 與 hello 媒體服務相關聯的標記。

* 範例: @{"標籤 1"="value1";"標籤 2 」 =: value2"}

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置？ |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
更新媒體服務。

### <a name="syntax"></a>語法
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | Name |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

指定與 hello 媒體服務相關聯的儲存體帳戶。

* 新建立儲存體帳戶 （以 hello 資源管理員 API） 才支援。
* hello 儲存體帳戶必須存在，且具有 hello 與 hello 媒體服務的相同位置。
* 只可以指定一個主要儲存體帳戶。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置？ |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 參數集名稱 |StorageAccountsParamSet |
| 接受萬用字元？ |false |

**-Tags &lt;Hashtable&gt;**

指定雜湊表的 hello 與此媒體服務相關聯的標記。

* hello 媒體服務相關聯的 hello 標記會取代 hello 客戶所指定的值。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置？ |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
移除媒體服務。

### <a name="syntax"></a>語法
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |2 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |False |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
取得資源群組中的所有媒體服務或取得指定名稱的媒體服務。

### <a name="syntax"></a>語法
參數集：ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

參數集：AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 參數集名稱 |ResourceGroupParameterSet、AccountNameParameterSet |

接受萬用字元？   false

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 參數集名稱 |AccountNameParameterSet |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
取得媒體服務的金鑰。

### <a name="syntax"></a>語法
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
重新產生媒體服務的主要或次要金鑰。

### <a name="syntax"></a>語法
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-KeyType &lt;KeyType&gt;**

指定 hello hello 媒體服務金鑰類型。

* 主要或次要

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |2 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toothe cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
同步處理與 hello 媒體服務相關聯的儲存體帳戶的儲存體帳戶金鑰。

### <a name="syntax"></a>語法
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>參數
**-ResourceGroupName &lt;String&gt;**

指定此媒體服務所屬的 hello 資源群組 toowhich hello 名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |0 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-AccountName &lt;String&gt;**

指定 hello hello 媒體服務名稱。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置？ |1 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**-StorageAccountId &lt;String&gt;**

指定 hello 與 hello 媒體服務相關聯的儲存體帳戶。

| 別名 | 識別碼 |
| --- | --- |
| 必要？ |true |
| 位置？ |2 |
| 預設值 |無 |
| 接受管線輸入？ |true(ByPropertyName) |
| 接受萬用字元？ |false |

**&lt;CommandParameters&gt;**

這個 cmdlet 支援 hello 一般參數:-偵錯、-ErrorAction、-ErrorVariable、-InformationAction、-InformationVariable、-OutVariable、-OutBuffer、-PipelineVariable、-Verbose、-WarningAction 以及-WarningVariable。

### <a name="inputs"></a>輸入
hello 輸入型別是 hello hello 型別物件，您可以使用管線傳送 toohello cmdlet。

### <a name="outputs"></a>輸出
hello 輸出類型是 hello hello cmdlet 的 hello 物件型別會發出。

## <a name="next-step"></a>後續步驟
查看媒體服務學習途徑。

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

