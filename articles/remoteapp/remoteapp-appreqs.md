---
title: "Azure RemoteApp aaaApp 需求 |Microsoft 文件"
description: "深入了解應用程式的 toouse Azure RemoteApp 中的 hello 需求"
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
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="319e6-103">應用程式需求</span><span class="sxs-lookup"><span data-stu-id="319e6-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="319e6-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="319e6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="319e6-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="319e6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="319e6-106">Azure RemoteApp 支援來自 Windows Server 2012 R2 映像的資料流 32 位元或 64 位元 Windows 架構應用程式。</span><span class="sxs-lookup"><span data-stu-id="319e6-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="319e6-107">大部分現有 32 位元或 64 位元 Windows 架構應用程式都是「依現狀」在 Azure RemoteApp (遠端桌面服務或舊稱的「終端機服務」) 環境中執行。</span><span class="sxs-lookup"><span data-stu-id="319e6-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="319e6-108">不過，執行和良好執行是有差別的，有些應用程式運作正常且完善執行，有些則不是。</span><span class="sxs-lookup"><span data-stu-id="319e6-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="319e6-109">下列資訊的 hello 提供遠端桌面服務環境中的應用程式的開發和測試 tooensure 相容性的指引。</span><span class="sxs-lookup"><span data-stu-id="319e6-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="319e6-110">提示：我們正在為您建立一些實用的應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="319e6-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="319e6-111">您會看到討論如何在 RemoteApp 內使用 Microsoft Access、QuickBooks 和 APP-V 的新主題。</span><span class="sxs-lookup"><span data-stu-id="319e6-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="319e6-112">需求</span><span class="sxs-lookup"><span data-stu-id="319e6-112">Requirements</span></span>
<span data-ttu-id="319e6-113">如果遵循下列三個需求，可協助應用程式在 RemoteApp 中順暢執行：</span><span class="sxs-lookup"><span data-stu-id="319e6-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="319e6-114">符合所有的應用程式[Windows 桌面應用程式的憑證需求](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx)和遵守太[程式設計指導方針的遠端桌面服務](https://msdn.microsoft.com/library/aa383490.aspx)必須完成與 RemoteApp 的相容性。</span><span class="sxs-lookup"><span data-stu-id="319e6-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="319e6-115">應用程式應該永遠不會將資料儲存在本機 hello 映像或可能會遺失的 RemoteApp 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="319e6-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="319e6-116">建立一個 RemoteApp 集合之後，hello 執行個體就會遭到複製，並是無狀態而應該只包含應用程式。</span><span class="sxs-lookup"><span data-stu-id="319e6-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="319e6-117">將外部來源中或 hello 使用者設定檔中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="319e6-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="319e6-118">自訂映像不應該包含可能會遺失的資料。</span><span class="sxs-lookup"><span data-stu-id="319e6-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="319e6-119">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="319e6-119">Testing your apps</span></span>
<span data-ttu-id="319e6-120">使用這些步驟 tootesting 應用程式：</span><span class="sxs-lookup"><span data-stu-id="319e6-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="319e6-121">安裝 Windows Server 2012 R2 和您的應用程式</span><span class="sxs-lookup"><span data-stu-id="319e6-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="319e6-122">啟用遠端桌面</span><span class="sxs-lookup"><span data-stu-id="319e6-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="319e6-123">建立兩個使用者帳戶，使用者 a 和使用者 b，加入這兩個使用者帳戶 toohello 遠端桌面安全性群組。</span><span class="sxs-lookup"><span data-stu-id="319e6-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="319e6-124">藉由建立兩個同時 RDS 工作階段 toohello 電腦在啟動 hello 應用程式時檢查多重工作階段相容性。</span><span class="sxs-lookup"><span data-stu-id="319e6-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="319e6-125">驗證應用程式行為</span><span class="sxs-lookup"><span data-stu-id="319e6-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="319e6-126">應用程式開發指導方針</span><span class="sxs-lookup"><span data-stu-id="319e6-126">Application development guidelines</span></span>
<span data-ttu-id="319e6-127">使用下列指導方針來開發應用程式，remoteapp hello。</span><span class="sxs-lookup"><span data-stu-id="319e6-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="319e6-128">多個使用者</span><span class="sxs-lookup"><span data-stu-id="319e6-128">Multiple users</span></span>
* <span data-ttu-id="319e6-129">安裝 [單一使用者的應用程式 ](https://msdn.microsoft.com/library/aa380661.aspx)可能在多使用者環境中造成問題。</span><span class="sxs-lookup"><span data-stu-id="319e6-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="319e6-130">應用程式應該[儲存使用者特定資訊](https://msdn.microsoft.com/library/aa383452.aspx)使用者特定位置中分別從全域資訊套用 tooall 使用者。</span><span class="sxs-lookup"><span data-stu-id="319e6-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="319e6-131">RemoteApp 為 [核心物件使用多個命名空間](https://msdn.microsoft.com/library/aa382954.aspx)；主要是藉由用戶端/伺服器應用程式中的服務來使用全域命名空間。</span><span class="sxs-lookup"><span data-stu-id="319e6-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="319e6-132">它不是電腦名稱或 hello hello 的安全 tooassume [IP 位址](https://msdn.microsoft.com/library/aa382942.aspx)指派的 toohello 電腦與使用者相關聯單一因為多個使用者可以登入同時 tooa 遠端桌面工作階段主機 （RD 工作階段主機） 伺服器。</span><span class="sxs-lookup"><span data-stu-id="319e6-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="319e6-133">效能</span><span class="sxs-lookup"><span data-stu-id="319e6-133">Performance</span></span>
* <span data-ttu-id="319e6-134">停用[圖形效果](https://msdn.microsoft.com/library/aa380822.aspx)新增應用程式 tooRemoteApp 之前。</span><span class="sxs-lookup"><span data-stu-id="319e6-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="319e6-135">將停用所有使用者，toomaximize CPU 可用性[背景工作](https://msdn.microsoft.com/library/aa380665.aspx)或建立有效率的背景工作不需要大量資源。</span><span class="sxs-lookup"><span data-stu-id="319e6-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="319e6-136">您應該針對多使用者、多處理器環境微調和平衡應用程式 [執行緒使用量](https://msdn.microsoft.com/library/aa383520.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="319e6-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="319e6-137">toooptimize 效能，應用程式的最佳作法是太[偵測](https://msdn.microsoft.com/library/aa380798.aspx)中用戶端工作階段是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="319e6-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

