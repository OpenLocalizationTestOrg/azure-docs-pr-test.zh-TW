---
title: "更換儲存體存取金鑰之後更新媒體服務 | Microsoft Docs"
description: "本文章會教您如何在更換儲存體存取金鑰之後更新媒體服務。"
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
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="b48da-103">更換儲存體存取金鑰之後更新媒體服務</span><span class="sxs-lookup"><span data-stu-id="b48da-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="b48da-104">在建立新的 Azure 媒體服務 (AMS) 帳戶時，您需要選取用來儲存媒體內容的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b48da-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="b48da-105">您可以在媒體服務帳戶新增一個以上的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b48da-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="b48da-106">本主題說明如何更換儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="b48da-107">其中也示範如何在媒體帳戶新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b48da-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="b48da-108">若要執行本主題中描述的動作，您應該使用 [ARM API](https://docs.microsoft.com/rest/api/media/mediaservice) 和 [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media)。</span><span class="sxs-lookup"><span data-stu-id="b48da-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="b48da-109">如需詳細資訊，請參閱[如何使用 PowerShell 和資源管理員來管理 Azure 資源](../azure-resource-manager/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="b48da-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="b48da-110">概觀</span><span class="sxs-lookup"><span data-stu-id="b48da-110">Overview</span></span>

<span data-ttu-id="b48da-111">建立新的儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，用來驗證儲存體帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="b48da-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="b48da-112">為了讓儲存體連線更加安全，建議您定期重新產生並更換儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="b48da-113">您會收到兩個存取金鑰(主要和次要)，這樣當您重新產生其他存取金鑰時，您就可以使用其中一個存取金鑰保持儲存體連線不中斷。</span><span class="sxs-lookup"><span data-stu-id="b48da-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="b48da-114">此程序也稱為 「 更換存取金鑰 」。</span><span class="sxs-lookup"><span data-stu-id="b48da-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="b48da-115">媒體服務取決於所提供的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="b48da-116">具體而言，定位器是要串流傳送或下載您的資產，這會根據指定的儲存體存取金鑰而定。</span><span class="sxs-lookup"><span data-stu-id="b48da-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="b48da-117">建立 AMS 帳戶時，它預設會相依於主要儲存體存取金鑰，但身為使用者，您可以更新 AMS 所擁有的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="b48da-118">您必須確定會讓媒體服務知道本主題中所述之下列步驟所使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="b48da-119">如果您有多個儲存體帳戶，請針對每一個儲存體帳戶執行此程序。</span><span class="sxs-lookup"><span data-stu-id="b48da-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="b48da-120">更換儲存體金鑰無固定順序。</span><span class="sxs-lookup"><span data-stu-id="b48da-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="b48da-121">您可以先更換次要金鑰再更換主要金鑰，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="b48da-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="b48da-122">在實際商用的帳戶上執行本文章描述的步驟之前，請事先在測試用帳戶上進行測試。</span><span class="sxs-lookup"><span data-stu-id="b48da-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="b48da-123">更換儲存體金鑰的步驟</span><span class="sxs-lookup"><span data-stu-id="b48da-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="b48da-124">透過 PowerShell Cmdlet 或 [Azure](https://portal.azure.com/) 入口網站來變更儲存體帳戶主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="b48da-125">搭配適當的參數呼叫 Sync-AzureRmMediaServiceStorageKeys Cmdlet，以強制媒體帳戶接收儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="b48da-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="b48da-126">以下範例示範如何將金鑰同步到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b48da-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="b48da-127">請等候約一小時。</span><span class="sxs-lookup"><span data-stu-id="b48da-127">Wait an hour or so.</span></span> <span data-ttu-id="b48da-128">確認資料流案例運作無誤。</span><span class="sxs-lookup"><span data-stu-id="b48da-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="b48da-129">透過 PowerShell Cmdlet 或 Azure 入口網站變更儲存體帳戶次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="b48da-130">搭配適當的參數呼叫 Sync-AzureRmMediaServiceStorageKeys PowerShell，以強制媒體帳戶接收儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b48da-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="b48da-131">請等候約一小時。</span><span class="sxs-lookup"><span data-stu-id="b48da-131">Wait an hour or so.</span></span> <span data-ttu-id="b48da-132">確認資料流案例運作無誤。</span><span class="sxs-lookup"><span data-stu-id="b48da-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="b48da-133">PowerShell Cmdlet 範例</span><span class="sxs-lookup"><span data-stu-id="b48da-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="b48da-134">以下範例示範如何取得儲存體帳戶並與 AMS 帳戶同步。</span><span class="sxs-lookup"><span data-stu-id="b48da-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="b48da-135">將儲存體帳戶新增到 AMS 帳戶的步驟</span><span class="sxs-lookup"><span data-stu-id="b48da-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="b48da-136">以下主題說明如何將儲存體帳戶新增到 AMS 帳戶：[將多個儲存體帳戶附加到媒體服務帳戶](meda-services-managing-multiple-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="b48da-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b48da-137">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="b48da-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b48da-138">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="b48da-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="b48da-139">通知</span><span class="sxs-lookup"><span data-stu-id="b48da-139">Acknowledgments</span></span>
<span data-ttu-id="b48da-140">我們想要向下列為建立此文件貢獻心力的人員致謝：Cenk Dingiloglu、Milan Gada、Seva Titov。</span><span class="sxs-lookup"><span data-stu-id="b48da-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
