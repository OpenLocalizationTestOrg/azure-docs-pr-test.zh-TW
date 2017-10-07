---
title: "aaaAzure RemoteApp 授權 |Microsoft 文件"
description: "了解 Azure RemoteApp 中的授權如何運作。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a><span data-ttu-id="0843b-103">Azure RemoteApp 中的授權如何運作？</span><span class="sxs-lookup"><span data-stu-id="0843b-103">How does licensing work in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0843b-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="0843b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0843b-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0843b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0843b-106">因此您設定您的 Azure RemoteApp 服務，建立您的範本，並準備好 toopublish 應用程式 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="0843b-106">So you've set up your Azure RemoteApp service, created your templates, and are ready toopublish apps tooyour users.</span></span> <span data-ttu-id="0843b-107">但仍有一個出的最後一件事 toofigure： 授權。</span><span class="sxs-lookup"><span data-stu-id="0843b-107">But there's still one last thing toofigure out: licensing.</span></span> <span data-ttu-id="0843b-108">只要如何運作授權 RemoteApp 和您共用透過 RemoteApp hello 應用程式？</span><span class="sxs-lookup"><span data-stu-id="0843b-108">Just how does licensing work for RemoteApp and for hello apps you share through RemoteApp?</span></span>

<span data-ttu-id="0843b-109">RemoteApp 不需要任何 Windows 授權或遠端桌面 CAL。</span><span class="sxs-lookup"><span data-stu-id="0843b-109">RemoteApp does not require any Windows licenses or Remote Desktop CALs.</span></span> <span data-ttu-id="0843b-110">Hello 本身 RemoteApp 端會負責您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0843b-110">Your subscription takes care of hello RemoteApp side itself.</span></span> <span data-ttu-id="0843b-111">(簽出 hello 詳細資料的 hello[定價方案](https://azure.microsoft.com/pricing/details/remoteapp)。)</span><span class="sxs-lookup"><span data-stu-id="0843b-111">(Check out hello details of hello [pricing plans](https://azure.microsoft.com/pricing/details/remoteapp).)</span></span>

<span data-ttu-id="0843b-112">如果您使用其中一個包含您的訂用帳戶中的 hello 映像，您可以將該映像上安裝而不需要個別授權的 hello 應用任何的程式共用。</span><span class="sxs-lookup"><span data-stu-id="0843b-112">If you use one of hello images that is included in your subscription, you can share any of hello apps installed on that image without needing a separate license.</span></span> <span data-ttu-id="0843b-113">例如，如果您使用 hello Windows Server 2012 R2 範本映像 toobuild 您的集合，您就可以與您的使用者共用 System Center Endpoint Protection。</span><span class="sxs-lookup"><span data-stu-id="0843b-113">For example, if you use hello Windows Server 2012 R2 template image toobuild your collection, you can share System Center Endpoint Protection with your users.</span></span> <span data-ttu-id="0843b-114">hello 例外狀況 toothis 規則是 Office 365 ProPlus，這需要不同的訂用帳戶，以及 Office 2013，不能共用生產階段前集合中。</span><span class="sxs-lookup"><span data-stu-id="0843b-114">hello only exceptions toothis rule are Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be shared in a production collection.</span></span>

<span data-ttu-id="0843b-115">如果您想 toouse hello Office 365 範本映像隨附 RemoteApp，您必須擁有*現有*Office 365 ProPlus 計劃。</span><span class="sxs-lookup"><span data-stu-id="0843b-115">If you want toouse hello Office 365 template image that comes with RemoteApp, you must have an *existing* Office 365 ProPlus plan.</span></span> <span data-ttu-id="0843b-116">hello 也適用於您發佈的資料使用的自訂範本的任何 Office 365 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0843b-116">hello same is true for any Office 365 app that you publish using a custom template.</span></span> <span data-ttu-id="0843b-117">您需要 tooactivate hello 應用程式與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0843b-117">You need tooactivate hello apps with your own subscription.</span></span> <span data-ttu-id="0843b-118">無論試用版或付費訂用帳戶都是如此。</span><span class="sxs-lookup"><span data-stu-id="0843b-118">This is true for both trial and paid subscriptions.</span></span> <span data-ttu-id="0843b-119">如果您想 toouse hello Office 365 範本映像 hello 試用期間*您還沒有訂用帳戶和*，移至 Office 365 toohello 頁面太[註冊](https://go.microsoft.com/fwlink/p/?LinkID=403802)試用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0843b-119">If you want toouse hello Office 365 template image during hello trial, *and you don't already have a subscription*, go toohello Office 365 page too[sign up](https://go.microsoft.com/fwlink/p/?LinkID=403802) for a trial subscription.</span></span> <span data-ttu-id="0843b-120">如需詳細資訊，請參閱 [RemoteApp 與 Office 如何共同運作？](remoteapp-o365.md) 。</span><span class="sxs-lookup"><span data-stu-id="0843b-120">See [How do RemoteApp and Office work together?](remoteapp-o365.md) for more information.</span></span>

<span data-ttu-id="0843b-121">如果在 hello 試用期間，您不想 tooget Office 365 試用訂閱，使用 hello Office 2013 Professional Plus 的範本映像隨附 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="0843b-121">If, during hello trial period, you don't want tooget an Office 365 trial subscription, use hello Office 2013 Professional Plus template image that comes with RemoteApp.</span></span> <span data-ttu-id="0843b-122">此範本映像只能使用 30 天，而且無法轉換成付費收藏。</span><span class="sxs-lookup"><span data-stu-id="0843b-122">This template image can only be used for 30 days and cannot be converted into a paid collection.</span></span>

<span data-ttu-id="0843b-123">對於其他應用程式，您需要 toomake 確定您已擁有 hello 授權 tooshare hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0843b-123">For other apps, you need toomake sure that you have hello license tooshare hello app.</span></span>

<span data-ttu-id="0843b-124">這很合理，對吧？</span><span class="sxs-lookup"><span data-stu-id="0843b-124">That makes sense, right?</span></span> <span data-ttu-id="0843b-125">您可以發佈任何應用程式，您有遵循和法令資格 tooshare。</span><span class="sxs-lookup"><span data-stu-id="0843b-125">You can publish any app that you are legally entitled tooshare.</span></span> <span data-ttu-id="0843b-126">而且您需要確定您真的是 toomake 標題 tooshare 為您的程式。</span><span class="sxs-lookup"><span data-stu-id="0843b-126">And you need toomake sure you really are entitled tooshare your programs.</span></span>

<span data-ttu-id="0843b-127">請注意，您不能在雲端收藏中使用 CAL 或大量授權合約。</span><span class="sxs-lookup"><span data-stu-id="0843b-127">Please note that you cannot use a CAL or Volume License agreement in a cloud collection.</span></span> <span data-ttu-id="0843b-128">您*可以*混合式集合 （除了 Office) 中使用大量授權合約 tooactivate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0843b-128">You *can* use a Volume License agreement tooactivate applications in your hybrid collection (except for Office).</span></span> <span data-ttu-id="0843b-129">您只需要的 tooinstall 它們在您的範本映像從 hello 大量授權的媒體。</span><span class="sxs-lookup"><span data-stu-id="0843b-129">You just need tooinstall them on your template image from hello Volume License media.</span></span> <span data-ttu-id="0843b-130">請依照 hello 資訊 hello 應用程式廠商 tooinstall 授權遠端桌面環境中執行。</span><span class="sxs-lookup"><span data-stu-id="0843b-130">Follow hello information from hello application vendor tooinstall licenses in a Remote Desktop environment.</span></span>

