---
title: "aaaTroubleshoot 雲端服務部署問題 |Microsoft 文件"
description: "沒有部署雲端服務 tooAzure 時可能遇到的一些常見的問題。 本文章提供解決方案 toosome 它們。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="c2910-104">對雲端服務部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c2910-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="c2910-105">當您部署雲端服務應用程式封裝 tooAzure 時，您可以從 hello 取得 hello 部署資訊**屬性**hello Azure 入口網站中的窗格。</span><span class="sxs-lookup"><span data-stu-id="c2910-105">When you deploy a cloud service application package tooAzure, you can obtain information about hello deployment from hello **Properties** pane in hello Azure portal.</span></span> <span data-ttu-id="c2910-106">您可以使用 hello 詳細資料中此窗格 toohelp 問題進行疑難排解 hello 雲端服務，並開啟新的支援要求時，您可以提供此資訊 tooAzure 支援。</span><span class="sxs-lookup"><span data-stu-id="c2910-106">You can use hello details in this pane toohelp you troubleshoot problems with hello cloud service, and you can provide this information tooAzure Support when opening a new support request.</span></span>

<span data-ttu-id="c2910-107">您可以找到 hello**屬性**窗格中的，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c2910-107">You can find hello **Properties** pane as follows:</span></span>

* <span data-ttu-id="c2910-108">在 hello Azure 入口網站，按一下 hello 部署您的雲端服務中按一下**所有設定**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="c2910-108">In hello Azure portal, click hello deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="c2910-109">在 hello Azure 傳統入口網站，按一下您的雲端服務的 hello 部署，按一下**儀表板**、 hello 右下角的 hello 頁面 (在**快速概覽**)。</span><span class="sxs-lookup"><span data-stu-id="c2910-109">In hello Azure classic portal, click hello deployment of your cloud service, click **DASHBOARD**, located at hello lower-right corner of hello page (under **quick glance**).</span></span> <span data-ttu-id="c2910-110">請注意，此窗格中並沒有「屬性」標籤。</span><span class="sxs-lookup"><span data-stu-id="c2910-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="c2910-111">您可以複製 hello hello 內容**屬性**按一下 hello 圖示在 hello hello 窗格右上角的窗格 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c2910-111">You can copy hello contents of hello **Properties** pane toohello clipboard by clicking hello icon in hello upper-right corner of hello pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="c2910-112">問題：我無法存取我的網站，但是我已啟動部署且所有角色執行個體皆已就緒</span><span class="sxs-lookup"><span data-stu-id="c2910-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="c2910-113">hello hello 入口網站中顯示的網站 URL 連結不包含 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="c2910-113">hello website URL link shown in hello portal does not include hello port.</span></span> <span data-ttu-id="c2910-114">hello 網站的預設通訊埠為 80。</span><span class="sxs-lookup"><span data-stu-id="c2910-114">hello default port for websites is 80.</span></span> <span data-ttu-id="c2910-115">如果您的應用程式是在不同的通訊埠設定的 toorun，您必須新增 hello 正確的連接埠號碼 toohello URL 存取 hello 網站時。</span><span class="sxs-lookup"><span data-stu-id="c2910-115">If your application is configured toorun in a different port, you must add hello correct port number toohello URL when accessing hello website.</span></span>

1. <span data-ttu-id="c2910-116">在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c2910-116">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="c2910-117">在 hello**屬性**窗格中的 hello Azure 入口網站，檢查 hello hello 角色執行個體的連接埠 (在**輸入端點**)。</span><span class="sxs-lookup"><span data-stu-id="c2910-117">In hello **Properties** pane of hello Azure portal, check hello ports for hello role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="c2910-118">如果 hello 連接埠不是 80，新增 hello 正確的連接埠值 toohello URL，當您存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2910-118">If hello port is not 80, add hello correct port value toohello URL when you access hello application.</span></span> <span data-ttu-id="c2910-119">toospecify 非預設連接埠輸入 hello URL，後面接著冒號 （:），後面接著 hello 通訊埠編號，不含空格。</span><span class="sxs-lookup"><span data-stu-id="c2910-119">toospecify a non-default port, type hello URL, followed by a colon (:), followed by hello port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="c2910-120">問題：我的角色執行個體無故自行回收</span><span class="sxs-lookup"><span data-stu-id="c2910-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="c2910-121">當 Azure 偵測到問題的節點，並因此移動角色執行個體 toonew 節點，會自動發生服務修復。</span><span class="sxs-lookup"><span data-stu-id="c2910-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances toonew nodes.</span></span> <span data-ttu-id="c2910-122">發生此情況時，您可能會看見角色執行個體自動回收。</span><span class="sxs-lookup"><span data-stu-id="c2910-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="c2910-123">如果 toofind 服務修復發生：</span><span class="sxs-lookup"><span data-stu-id="c2910-123">toofind out if service healing occurred:</span></span>

1. <span data-ttu-id="c2910-124">在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c2910-124">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="c2910-125">在 hello**屬性**窗格中的 hello Azure 入口網站檢閱 hello 資訊並判斷發生服務修復期間 hello 觀察 hello 角色回收。</span><span class="sxs-lookup"><span data-stu-id="c2910-125">In hello **Properties** pane of hello Azure portal, review hello information and determine whether service healing occurred during hello time that you observed hello roles recycling.</span></span>

<span data-ttu-id="c2910-126">在主機 OS 和客體 OS 升級期間，角色大約每個月會回收一次。</span><span class="sxs-lookup"><span data-stu-id="c2910-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="c2910-127">如需詳細資訊，請參閱 hello 部落格文章[角色執行個體因而重新啟動 tooOS 升級](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="c2910-127">For more information, see hello blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="c2910-128">問題：我無法進行 VIP 交換並收到錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="c2910-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="c2910-129">在部署更新進行期間不允許 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="c2910-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="c2910-130">部署更新可能在下列時間點自動執行：</span><span class="sxs-lookup"><span data-stu-id="c2910-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="c2910-131">新的客體作業系統可供使用時，和您設定要自動更新時。</span><span class="sxs-lookup"><span data-stu-id="c2910-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="c2910-132">服務修復執行時。</span><span class="sxs-lookup"><span data-stu-id="c2910-132">Service healing occurs.</span></span>

<span data-ttu-id="c2910-133">toofind out 如果自動更新，所以您無法進行 VIP 交換：</span><span class="sxs-lookup"><span data-stu-id="c2910-133">toofind out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="c2910-134">在 hello Azure 入口網站，按一下 hello 部署您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c2910-134">In hello Azure portal, click hello deployment of your cloud service.</span></span>
2. <span data-ttu-id="c2910-135">在 hello**屬性**窗格中的 hello Azure 入口網站，看看 hello 值**狀態**。</span><span class="sxs-lookup"><span data-stu-id="c2910-135">In hello **Properties** pane of hello Azure portal, look at hello value of **Status**.</span></span> <span data-ttu-id="c2910-136">如果是**準備**，然後檢查**上次作業**toosee 如果其中一個是最近發生的阻礙 hello VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="c2910-136">If it is **Ready**, then check **Last operation** toosee if one recently happened that might prevent hello VIP swap.</span></span>
3. <span data-ttu-id="c2910-137">重複步驟 1 和 2 hello 生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="c2910-137">Repeat steps 1 and 2 for hello production deployment.</span></span>
4. <span data-ttu-id="c2910-138">如果自動更新正在進行時，等候它 toofinish 之前嘗試 toodo hello VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="c2910-138">If an automatic update is in process, wait for it toofinish before trying toodo hello VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="c2910-139">問題：角色執行個體在 [已啟動]、[初始化中]、[忙碌] 和 [已停止] 之間循環</span><span class="sxs-lookup"><span data-stu-id="c2910-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="c2910-140">這種情況可能表示應用程式的程式碼、封裝或組態檔發生問題。</span><span class="sxs-lookup"><span data-stu-id="c2910-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="c2910-141">在此情況下，您應能 toosee hello 狀態變更每隔幾分鐘，而且 hello Azure 入口網站可能看起來像**回收**，**忙碌**，或**Initializing**。</span><span class="sxs-lookup"><span data-stu-id="c2910-141">In that case, you should be able toosee hello status changing every few minutes and hello Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="c2910-142">這表示已發生某些錯誤會導致無法執行 hello 角色執行個體的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2910-142">This indicates that there is something wrong with hello application that is keeping hello role instance from running.</span></span>

<span data-ttu-id="c2910-143">如需有關如何 tootroubleshoot 這個問題，請參閱 hello 部落格文章[Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)和[常見問題該原因角色 toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。</span><span class="sxs-lookup"><span data-stu-id="c2910-143">For more information on how tootroubleshoot for this problem, see hello blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="c2910-144">問題：我的應用程式停止運作</span><span class="sxs-lookup"><span data-stu-id="c2910-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="c2910-145">在 hello Azure 入口網站，按一下 hello 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="c2910-145">In hello Azure portal, click hello role instance.</span></span>
2. <span data-ttu-id="c2910-146">在 hello**屬性**窗格中的 hello Azure 入口網站，請考慮下列條件 tooresolve hello 您的問題：</span><span class="sxs-lookup"><span data-stu-id="c2910-146">In hello **Properties** pane of hello Azure portal, consider hello following conditions tooresolve your problem:</span></span>
   * <span data-ttu-id="c2910-147">如果 hello 角色執行個體最近停止 (您可以檢查的 hello 值**中止計數**)，無法更新 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="c2910-147">If hello role instance has recently stopped (you can check hello value of **Abort count**), hello deployment could be updating.</span></span> <span data-ttu-id="c2910-148">如果 hello 角色執行個體繼續其本身上運作，請等候 toosee。</span><span class="sxs-lookup"><span data-stu-id="c2910-148">Wait toosee if hello role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="c2910-149">如果 hello 角色執行個體是**忙碌**，檢查您的應用程式程式碼 toosee hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck)處理事件。</span><span class="sxs-lookup"><span data-stu-id="c2910-149">If hello role instance is **Busy**, check your application code toosee if hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="c2910-150">您可能需要 tooadd 或修正某個處理此事件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2910-150">You might need tooadd or fix some code that handles this event.</span></span>
   * <span data-ttu-id="c2910-151">瀏覽 hello 診斷資料及疑難排解案例 hello 部落格文章[Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c2910-151">Go through hello diagnostic data and troubleshooting scenarios in hello blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="c2910-152">如果回收您的雲端服務時，您重設 hello 部署的 hello 屬性有效地清除 hello hello 原始問題的資訊。</span><span class="sxs-lookup"><span data-stu-id="c2910-152">If you recycle your cloud service, you reset hello properties for hello deployment, effectively erasing hello information for hello original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c2910-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2910-153">Next steps</span></span>
<span data-ttu-id="c2910-154">檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="c2910-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="c2910-155">toolearn tootroubleshoot 雲端服務角色如何發出使用 Azure PaaS 電腦診斷資料，請參閱[Kevin Williamson 部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c2910-155">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
