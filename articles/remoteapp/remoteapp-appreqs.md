---
title: "Azure RemoteApp 的應用程式需求 | Microsoft Docs"
description: "了解您想要用於 Azure RemoteApp 的應用程式需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="ce51f-103">應用程式需求</span><span class="sxs-lookup"><span data-stu-id="ce51f-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ce51f-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ce51f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ce51f-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="ce51f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ce51f-106">Azure RemoteApp 支援來自 Windows Server 2012 R2 映像的資料流 32 位元或 64 位元 Windows 架構應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce51f-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="ce51f-107">大部分現有 32 位元或 64 位元 Windows 架構應用程式都是「依現狀」在 Azure RemoteApp (遠端桌面服務或舊稱的「終端機服務」) 環境中執行。</span><span class="sxs-lookup"><span data-stu-id="ce51f-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="ce51f-108">不過，執行和良好執行是有差別的，有些應用程式運作正常且完善執行，有些則不是。</span><span class="sxs-lookup"><span data-stu-id="ce51f-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="ce51f-109">下列資訊提供在遠端桌面服務環境中開發應用程式，及測試以確保相容性的指引。</span><span class="sxs-lookup"><span data-stu-id="ce51f-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="ce51f-110">提示：我們正在為您建立一些實用的應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="ce51f-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="ce51f-111">您會看到討論如何在 RemoteApp 內使用 Microsoft Access、QuickBooks 和 APP-V 的新主題。</span><span class="sxs-lookup"><span data-stu-id="ce51f-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="ce51f-112">需求</span><span class="sxs-lookup"><span data-stu-id="ce51f-112">Requirements</span></span>
<span data-ttu-id="ce51f-113">如果遵循下列三個需求，可協助應用程式在 RemoteApp 中順暢執行：</span><span class="sxs-lookup"><span data-stu-id="ce51f-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="ce51f-114">符合所有 [Windows 傳統型應用程式認證需求](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx)，並遵循[遠端桌面服務程式設計指導方針](https://msdn.microsoft.com/library/aa383490.aspx)的應用程式，皆與 RemoteApp 完全相容。</span><span class="sxs-lookup"><span data-stu-id="ce51f-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="ce51f-115">應用程式應該永遠不要在可能遺失的映像或 RemoteApp 執行個體中本機儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ce51f-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="ce51f-116">建立 RemoteApp 集合之後，會複製執行個體，且不會呈現狀態並只包含應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce51f-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="ce51f-117">將資料儲存在外部來源，或使用者的設定檔內。</span><span class="sxs-lookup"><span data-stu-id="ce51f-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="ce51f-118">自訂映像不應該包含可能會遺失的資料。</span><span class="sxs-lookup"><span data-stu-id="ce51f-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="ce51f-119">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="ce51f-119">Testing your apps</span></span>
<span data-ttu-id="ce51f-120">使用下列步驟來測試應用程式：</span><span class="sxs-lookup"><span data-stu-id="ce51f-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="ce51f-121">安裝 Windows Server 2012 R2 和您的應用程式</span><span class="sxs-lookup"><span data-stu-id="ce51f-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="ce51f-122">啟用遠端桌面</span><span class="sxs-lookup"><span data-stu-id="ce51f-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="ce51f-123">建立兩個使用者帳戶 (UserA 和 UserB)，將這兩個使用者帳戶新增至遠端桌面的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="ce51f-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="ce51f-124">啟動應用程式時建立兩個同時 RDS 工作階段到電腦，藉此檢查多重工作階段相容性。</span><span class="sxs-lookup"><span data-stu-id="ce51f-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="ce51f-125">驗證應用程式行為</span><span class="sxs-lookup"><span data-stu-id="ce51f-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="ce51f-126">應用程式開發指導方針</span><span class="sxs-lookup"><span data-stu-id="ce51f-126">Application development guidelines</span></span>
<span data-ttu-id="ce51f-127">使用下列指導方針來開發 RemoteApp 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce51f-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="ce51f-128">多個使用者</span><span class="sxs-lookup"><span data-stu-id="ce51f-128">Multiple users</span></span>
* <span data-ttu-id="ce51f-129">安裝 [單一使用者的應用程式 ](https://msdn.microsoft.com/library/aa380661.aspx)可能在多使用者環境中造成問題。</span><span class="sxs-lookup"><span data-stu-id="ce51f-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="ce51f-130">應用程式應在使用者特定位置中 [儲存使用者專屬資訊](https://msdn.microsoft.com/library/aa383452.aspx) ，藉此與套用到所有使用者的全域資訊區隔。</span><span class="sxs-lookup"><span data-stu-id="ce51f-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="ce51f-131">RemoteApp 為 [核心物件使用多個命名空間](https://msdn.microsoft.com/library/aa382954.aspx)；主要是藉由用戶端/伺服器應用程式中的服務來使用全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="ce51f-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="ce51f-132">假設指派給電腦的電腦名稱或 [IP 位址](https://msdn.microsoft.com/library/aa382942.aspx) 與單一使用者相關聯並不安全，因為多個使用者可以同時登入遠端桌面工作階段主機 (RD 工作階段主機) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ce51f-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="ce51f-133">效能</span><span class="sxs-lookup"><span data-stu-id="ce51f-133">Performance</span></span>
* <span data-ttu-id="ce51f-134">先停用 [圖形效果](https://msdn.microsoft.com/library/aa380822.aspx) ，再將應用程式新增至 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="ce51f-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="ce51f-135">若要最大化所有使用者的 CPU 可用性，請停用 [背景工作 ](https://msdn.microsoft.com/library/aa380665.aspx) 或建立不需要大量資源的高效率背景工作。</span><span class="sxs-lookup"><span data-stu-id="ce51f-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="ce51f-136">您應該針對多使用者、多處理器環境微調和平衡應用程式 [執行緒使用量](https://msdn.microsoft.com/library/aa383520.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ce51f-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="ce51f-137">若要最佳化效能，讓應用程式 [偵測](https://msdn.microsoft.com/library/aa380798.aspx) 它們是否正在用戶端工作階段中執行是個好方法。</span><span class="sxs-lookup"><span data-stu-id="ce51f-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

