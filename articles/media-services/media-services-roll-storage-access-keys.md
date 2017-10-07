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
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="2c795-103">更換儲存體存取金鑰之後更新媒體服務</span><span class="sxs-lookup"><span data-stu-id="2c795-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="2c795-104">當您建立新的 Azure 媒體服務 (AMS) 帳戶時，您也必須的 tooselect Azure 儲存體帳戶也就是使用 toostore 媒體內容。</span><span class="sxs-lookup"><span data-stu-id="2c795-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="2c795-105">您可以加入一個以上的儲存體帳戶 tooyour Media Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="2c795-106">本主題說明如何 toorotate 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="2c795-107">它也會示範如何 tooadd 儲存體帳戶 tooa media 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="2c795-108">本主題中所述的 tooperform hello 動作，您應該使用[ARM Api](https://docs.microsoft.com/rest/api/media/mediaservice)和[Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media)。</span><span class="sxs-lookup"><span data-stu-id="2c795-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="2c795-109">如需詳細資訊，請參閱[如何 toomanage Azure PowerShell 與資源管理員資源](../azure-resource-manager/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="2c795-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="2c795-110">概觀</span><span class="sxs-lookup"><span data-stu-id="2c795-110">Overview</span></span>

<span data-ttu-id="2c795-111">建立新的儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，也就是使用的 tooauthenticate 存取 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="2c795-112">tookeep 您的儲存體連接更安全，建議 tooperiodically 重新產生並旋轉您的儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="2c795-113">兩個存取金鑰 （主要和次要） 會提供在順序 tooenable toomaintain 連線 toohello 儲存體帳戶使用其中一個索引鍵時存取您重新產生 hello 其他存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="2c795-114">此程序也稱為 「 更換存取金鑰 」。</span><span class="sxs-lookup"><span data-stu-id="2c795-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="2c795-115">Media Services 提供 tooit 儲存體金鑰而定。</span><span class="sxs-lookup"><span data-stu-id="2c795-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="2c795-116">具體而言，所使用的 toostream 或下載您的資產 hello 定位器 hello 指定儲存體存取金鑰而定。</span><span class="sxs-lookup"><span data-stu-id="2c795-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="2c795-117">AMS 帳戶建立時所花費的相依性 hello 主要儲存體存取金鑰上依預設，但以使用者中，您可以更新 AMS 具有 hello 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="2c795-118">您必須確定 toolet 媒體服務知道哪些金鑰 toouse 依照本主題中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="2c795-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="2c795-119">如果您有多個儲存體帳戶，請針對每一個儲存體帳戶執行此程序。</span><span class="sxs-lookup"><span data-stu-id="2c795-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="2c795-120">hello 順序，您將旋轉儲存體金鑰不被固定的。</span><span class="sxs-lookup"><span data-stu-id="2c795-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="2c795-121">您可以先旋轉 hello 次要金鑰，並再 hello 主要索引鍵，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="2c795-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="2c795-122">先執行步驟，本主題說明在實際執行帳戶，請確定 tootest 它們進入生產階段前帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="2c795-123">步驟 toorotate 儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="2c795-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="2c795-124">變更 hello 儲存體帳戶主要金鑰透過 hello powershell cmdlet 或[Azure](https://portal.azure.com/)入口網站。</span><span class="sxs-lookup"><span data-stu-id="2c795-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="2c795-125">呼叫同步 AzureRmMediaServiceStorageKeys cmdlet 搭配適當的 params tooforce 媒體帳戶 toopick 總儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="2c795-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="2c795-126">hello 下列範例顯示如何 toosync 金鑰 toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="2c795-127">請等候約一小時。</span><span class="sxs-lookup"><span data-stu-id="2c795-127">Wait an hour or so.</span></span> <span data-ttu-id="2c795-128">檢查 hello 資料流案例正常運作。</span><span class="sxs-lookup"><span data-stu-id="2c795-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="2c795-129">變更 hello powershell cmdlet 或 Azure 入口網站透過儲存體帳戶次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="2c795-130">呼叫同步 AzureRmMediaServiceStorageKeys powershell 適當 params tooforce 媒體帳戶 toopick 註冊新的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c795-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="2c795-131">請等候約一小時。</span><span class="sxs-lookup"><span data-stu-id="2c795-131">Wait an hour or so.</span></span> <span data-ttu-id="2c795-132">檢查 hello 資料流案例正常運作。</span><span class="sxs-lookup"><span data-stu-id="2c795-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="2c795-133">PowerShell Cmdlet 範例</span><span class="sxs-lookup"><span data-stu-id="2c795-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="2c795-134">hello 下列範例示範如何 tooget hello 儲存體帳戶和同步與 hello AMS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c795-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="2c795-135">步驟 tooadd 儲存體帳戶 tooyour AMS 帳戶</span><span class="sxs-lookup"><span data-stu-id="2c795-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="2c795-136">hello 下列主題說明如何 tooadd 儲存體帳戶 tooyour AMS 帳戶：[附加多個儲存體帳戶 tooa Media Services 帳戶](meda-services-managing-multiple-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="2c795-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2c795-137">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="2c795-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2c795-138">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="2c795-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="2c795-139">通知</span><span class="sxs-lookup"><span data-stu-id="2c795-139">Acknowledgments</span></span>
<span data-ttu-id="2c795-140">我們想要遵循造成建立這份文件的人 tooacknowledge hello: Cenk Dingiloglu、 Milan Gada Seva Titov。</span><span class="sxs-lookup"><span data-stu-id="2c795-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
