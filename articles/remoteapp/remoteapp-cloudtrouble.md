---
title: "RemoteApp 雲端集合疑難排解 - 建立 | Microsoft Docs"
description: "了解如何疑難排解 RemoteApp 雲端集合建立失敗"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="ac927-103">建立 RemoteApp 雲端集合疑難排解</span><span class="sxs-lookup"><span data-stu-id="ac927-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac927-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ac927-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ac927-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="ac927-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ac927-106">如果建立雲端集合遇到問題，請查看下列資訊。</span><span class="sxs-lookup"><span data-stu-id="ac927-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="ac927-107">您的映像無效</span><span class="sxs-lookup"><span data-stu-id="ac927-107">Your image is invalid</span></span>
<span data-ttu-id="ac927-108">如果您在等候 Azure 佈建集合時，看到如「GoldImageInvalid」的訊息，表示範本映像不符合 [已定義的映像需求](remoteapp-imagereqs.md)。</span><span class="sxs-lookup"><span data-stu-id="ac927-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="ac927-109">因此，請閱讀 [需求](remoteapp-imagereqs.md)並修正映像，然後再嘗試重新建立集合。</span><span class="sxs-lookup"><span data-stu-id="ac927-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="ac927-110">Azure 管理入口網站中的常見錯誤</span><span class="sxs-lookup"><span data-stu-id="ac927-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="ac927-111">雲端集合通常會因為您在建立期間使用自訂映像而失敗。</span><span class="sxs-lookup"><span data-stu-id="ac927-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="ac927-112">如果您看到上述其中一個錯誤，而且您正在使用自訂映像來建立集合，請檢查下列事項：</span><span class="sxs-lookup"><span data-stu-id="ac927-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="ac927-113">確定上傳的自訂映像符合映像需求。</span><span class="sxs-lookup"><span data-stu-id="ac927-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="ac927-114">最常見的問題是映像的 Sysprep 處理不正確。</span><span class="sxs-lookup"><span data-stu-id="ac927-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="ac927-115">確認映像可以在 HYPER-V 內開機，或嘗試直接在 Azure 訂用帳戶中使用映像建立 IAAS VM。</span><span class="sxs-lookup"><span data-stu-id="ac927-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="ac927-116">如果 VM 無法開機且未啟動，則通常表示未正確準備自訂映像。</span><span class="sxs-lookup"><span data-stu-id="ac927-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="ac927-117">請遵循＜如何為 RemoteApp 建立自訂範本映像＞來確認已建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="ac927-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="ac927-118">如果您使用訂用帳戶隨附的其中一個 Microsoft 映像，請嘗試再次建立集合。</span><span class="sxs-lookup"><span data-stu-id="ac927-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="ac927-119">如果問題仍存在，請連絡 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="ac927-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="ac927-120">如果看到這個錯誤，通常表示您已經升級至付費帳戶，但您正在嘗試使用 Microsoft 提供的映像，而該映像只在服務的試用模式期間有效。</span><span class="sxs-lookup"><span data-stu-id="ac927-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="ac927-121">在此情況下，請嘗試再次建立您的雲端集合，但務必指定正確的映像。</span><span class="sxs-lookup"><span data-stu-id="ac927-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

