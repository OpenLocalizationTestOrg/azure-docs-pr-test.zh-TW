---
title: "aaaTroubleshoot RemoteApp 雲端集合建立 |Microsoft 文件"
description: "了解如何 tootroubleshoot RemoteApp 雲端集合建立失敗"
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="b09bd-103">建立 RemoteApp 雲端集合疑難排解</span><span class="sxs-lookup"><span data-stu-id="b09bd-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b09bd-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="b09bd-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b09bd-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b09bd-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b09bd-106">若您有建立雲端集合的問題，請查看下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="b09bd-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="b09bd-107">您的映像無效</span><span class="sxs-lookup"><span data-stu-id="b09bd-107">Your image is invalid</span></span>
<span data-ttu-id="b09bd-108">如果您正在等候 Azure tooprovision 您的集合時，您會看到類似 「 GoldImageInvalid 」 的訊息，表示您的範本映像不符合 hello[定義映像需求](remoteapp-imagereqs.md)。</span><span class="sxs-lookup"><span data-stu-id="b09bd-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="b09bd-109">因此，請移讀取這些[需求](remoteapp-imagereqs.md)，修正您的映像，然後再試 toocreate 集合一次。</span><span class="sxs-lookup"><span data-stu-id="b09bd-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="b09bd-110">在 hello Azure 管理入口網站中看到的常見錯誤</span><span class="sxs-lookup"><span data-stu-id="b09bd-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="b09bd-111">雲端集合通常會因為您在建立期間使用自訂映像而失敗。</span><span class="sxs-lookup"><span data-stu-id="b09bd-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="b09bd-112">如果您看到上述錯誤 hello 的而且您使用自訂映像 toocreate hello 集合，請參閱 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="b09bd-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="b09bd-113">確定您已上傳該 hello 自訂映像符合映像需求。</span><span class="sxs-lookup"><span data-stu-id="b09bd-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="b09bd-114">最常 hello 常見的問題是該 hello 映像未正確 syspreped。</span><span class="sxs-lookup"><span data-stu-id="b09bd-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="b09bd-115">確認 hello 映像可以開機 HYPER-V 中，或嘗試直接在您使用 hello 映像的 Azure 訂用帳戶中建立的 IAAS VM。</span><span class="sxs-lookup"><span data-stu-id="b09bd-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="b09bd-116">如果 hello VM 失敗 tooboot 並不會啟動，則這通常表示該 hello 自訂映像未準備正確。</span><span class="sxs-lookup"><span data-stu-id="b09bd-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="b09bd-117">確認 hello 自訂映像已建立下列 hello 如何 toocreate 自訂的範本映像的 RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b09bd-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="b09bd-118">如果您使用其中一個 hello Microsoft 映像包含您訂用帳戶，請嘗試再次 toocreate hello 集合。</span><span class="sxs-lookup"><span data-stu-id="b09bd-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="b09bd-119">如果 hello 問題持續發生請連絡 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="b09bd-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="b09bd-120">如果您看到此錯誤通常表示尚未升級的 tooa 付費帳戶，但您嘗試 toouse 在 hello hello 服務試用模式期間才是有效的 Microsoft 提供的映像。</span><span class="sxs-lookup"><span data-stu-id="b09bd-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="b09bd-121">在此情況下，嘗試 toocreate 您雲端的集合，但會確定 toospecify hello 正確的映像。</span><span class="sxs-lookup"><span data-stu-id="b09bd-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

