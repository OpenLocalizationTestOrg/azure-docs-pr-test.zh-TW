---
title: "aaaUpdate Media Services 之後輪流儲存體存取金鑰 |Microsoft 文件"
description: "此文章提供如何 tooupdate Media Services 之後輪流儲存體存取金鑰的指引。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>更換儲存體存取金鑰之後更新媒體服務

當您建立新的 Azure 媒體服務 (AMS) 帳戶時，您也必須的 tooselect Azure 儲存體帳戶也就是使用 toostore 媒體內容。 您可以加入一個以上的儲存體帳戶 tooyour Media Services 帳戶。 本主題說明如何 toorotate 儲存體金鑰。 它也會示範如何 tooadd 儲存體帳戶 tooa media 帳戶。 

本主題中所述的 tooperform hello 動作，您應該使用[ARM Api](https://docs.microsoft.com/rest/api/media/mediaservice)和[Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media)。  如需詳細資訊，請參閱[如何 toomanage Azure PowerShell 與資源管理員資源](../azure-resource-manager/powershell-azure-resource-manager.md)。

## <a name="overview"></a>概觀

建立新的儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，也就是使用的 tooauthenticate 存取 tooyour 儲存體帳戶。 tookeep 您的儲存體連接更安全，建議 tooperiodically 重新產生並旋轉您的儲存體存取金鑰。 兩個存取金鑰 （主要和次要） 會提供在順序 tooenable toomaintain 連線 toohello 儲存體帳戶使用其中一個索引鍵時存取您重新產生 hello 其他存取金鑰。 此程序也稱為 「 更換存取金鑰 」。

Media Services 提供 tooit 儲存體金鑰而定。 具體而言，所使用的 toostream 或下載您的資產 hello 定位器 hello 指定儲存體存取金鑰而定。 AMS 帳戶建立時所花費的相依性 hello 主要儲存體存取金鑰上依預設，但以使用者中，您可以更新 AMS 具有 hello 儲存體金鑰。 您必須確定 toolet 媒體服務知道哪些金鑰 toouse 依照本主題中所述的步驟。  

>[!NOTE]
> 如果您有多個儲存體帳戶，請針對每一個儲存體帳戶執行此程序。 hello 順序，您將旋轉儲存體金鑰不被固定的。 您可以先旋轉 hello 次要金鑰，並再 hello 主要索引鍵，反之亦然。
>
> 先執行步驟，本主題說明在實際執行帳戶，請確定 tootest 它們進入生產階段前帳戶。
>

## <a name="steps-toorotate-storage-keys"></a>步驟 toorotate 儲存體金鑰 
 
 1. 變更 hello 儲存體帳戶主要金鑰透過 hello powershell cmdlet 或[Azure](https://portal.azure.com/)入口網站。
 2. 呼叫同步 AzureRmMediaServiceStorageKeys cmdlet 搭配適當的 params tooforce 媒體帳戶 toopick 總儲存體帳戶金鑰
 
    hello 下列範例顯示如何 toosync 金鑰 toostorage 帳戶。
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. 請等候約一小時。 檢查 hello 資料流案例正常運作。
 4. 變更 hello powershell cmdlet 或 Azure 入口網站透過儲存體帳戶次要金鑰。
 5. 呼叫同步 AzureRmMediaServiceStorageKeys powershell 適當 params tooforce 媒體帳戶 toopick 註冊新的儲存體帳戶金鑰。 
 6. 請等候約一小時。 檢查 hello 資料流案例正常運作。
 
### <a name="a-powershell-cmdlet-example"></a>PowerShell Cmdlet 範例 

hello 下列範例示範如何 tooget hello 儲存體帳戶和同步與 hello AMS 帳戶。

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>步驟 tooadd 儲存體帳戶 tooyour AMS 帳戶

hello 下列主題說明如何 tooadd 儲存體帳戶 tooyour AMS 帳戶：[附加多個儲存體帳戶 tooa Media Services 帳戶](meda-services-managing-multiple-storage-accounts.md)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>通知
我們想要遵循造成建立這份文件的人 tooacknowledge hello: Cenk Dingiloglu、 Milan Gada Seva Titov。
