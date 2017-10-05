---
title: "針對雲端服務部署問題進行疑難排解 | Microsoft Docs"
description: "將雲端服務部署至 Azure 時，可能會發生幾個常見的問題。 本文章提供其中部分問題的解決方案。"
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
ms.openlocfilehash: 60e06ba292ff1e43d00cd69c1a422f9237d5e5a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="322cf-104">對雲端服務部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="322cf-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="322cf-105">當您將雲端服務應用程式封裝部署至 Azure 時，您可以從 Azure 入口網站中的 [屬性]  窗格取得部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="322cf-105">When you deploy a cloud service application package to Azure, you can obtain information about the deployment from the **Properties** pane in the Azure portal.</span></span> <span data-ttu-id="322cf-106">您可以利用此窗格中的詳細資料來排解雲端服務的問題，也可以在開啟新的支援要求時將這項資訊提供給 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="322cf-106">You can use the details in this pane to help you troubleshoot problems with the cloud service, and you can provide this information to Azure Support when opening a new support request.</span></span>

<span data-ttu-id="322cf-107">您可以依照下列方式找到 [屬性]  窗格：</span><span class="sxs-lookup"><span data-stu-id="322cf-107">You can find the **Properties** pane as follows:</span></span>

* <span data-ttu-id="322cf-108">在 Azure 入口網站中，依序按一下雲端服務的部署、[所有設定] 和 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="322cf-108">In the Azure portal, click the deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="322cf-109">在 Azure 傳統入口網站中，依序按一下雲端服務的部署、[儀表板]，位於頁面右下角 ([快速概覽] 下方)。</span><span class="sxs-lookup"><span data-stu-id="322cf-109">In the Azure classic portal, click the deployment of your cloud service, click **DASHBOARD**, located at the lower-right corner of the page (under **quick glance**).</span></span> <span data-ttu-id="322cf-110">請注意，此窗格中並沒有「屬性」標籤。</span><span class="sxs-lookup"><span data-stu-id="322cf-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="322cf-111">您可以按一下窗格右上角的圖示，將 [屬性] 窗格的內容複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="322cf-111">You can copy the contents of the **Properties** pane to the clipboard by clicking the icon in the upper-right corner of the pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="322cf-112">問題：我無法存取我的網站，但是我已啟動部署且所有角色執行個體皆已就緒</span><span class="sxs-lookup"><span data-stu-id="322cf-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="322cf-113">入口網站中顯示的網站 URL 連結未包含連接埠。</span><span class="sxs-lookup"><span data-stu-id="322cf-113">The website URL link shown in the portal does not include the port.</span></span> <span data-ttu-id="322cf-114">網站的預設連接埠為 80。</span><span class="sxs-lookup"><span data-stu-id="322cf-114">The default port for websites is 80.</span></span> <span data-ttu-id="322cf-115">如果您的應用程式設定為在不同的連接埠執行，您必須在存取網站時將正確的連接埠號碼新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="322cf-115">If your application is configured to run in a different port, you must add the correct port number to the URL when accessing the website.</span></span>

1. <span data-ttu-id="322cf-116">在 Azure 入口網站中，按一下您的雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="322cf-116">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="322cf-117">在 Azure 入口網站的 [屬性] 窗格中，查看角色執行個體的連接埠 (在 [輸入端點] 下方)。</span><span class="sxs-lookup"><span data-stu-id="322cf-117">In the **Properties** pane of the Azure portal, check the ports for the role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="322cf-118">如果連接埠不是 80，請在存取應用程式時將正確的連接埠值新增至 URL。</span><span class="sxs-lookup"><span data-stu-id="322cf-118">If the port is not 80, add the correct port value to the URL when you access the application.</span></span> <span data-ttu-id="322cf-119">若要指定非預設連接埠，請輸入 URL，後面依序加上冒號 (:) 和不含空格的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="322cf-119">To specify a non-default port, type the URL, followed by a colon (:), followed by the port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="322cf-120">問題：我的角色執行個體無故自行回收</span><span class="sxs-lookup"><span data-stu-id="322cf-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="322cf-121">當 Azure 偵測到有問題的節點，並將角色執行個體移至新節點時，會自動進行服務修復。</span><span class="sxs-lookup"><span data-stu-id="322cf-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances to new nodes.</span></span> <span data-ttu-id="322cf-122">發生此情況時，您可能會看見角色執行個體自動回收。</span><span class="sxs-lookup"><span data-stu-id="322cf-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="322cf-123">若要確認是否在執行服務修復：</span><span class="sxs-lookup"><span data-stu-id="322cf-123">To find out if service healing occurred:</span></span>

1. <span data-ttu-id="322cf-124">在 Azure 入口網站中，按一下您的雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="322cf-124">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="322cf-125">在 Azure 入口網站的 [屬性]  窗格中檢閱相關資訊，並判斷在您觀察角色回收的期間是否執行了服務修復。</span><span class="sxs-lookup"><span data-stu-id="322cf-125">In the **Properties** pane of the Azure portal, review the information and determine whether service healing occurred during the time that you observed the roles recycling.</span></span>

<span data-ttu-id="322cf-126">在主機 OS 和客體 OS 升級期間，角色大約每個月會回收一次。</span><span class="sxs-lookup"><span data-stu-id="322cf-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="322cf-127">如需詳細資訊，請參閱部落格文章 [角色執行個體由於作業系統升級而重新啟動](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="322cf-127">For more information, see the blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="322cf-128">問題：我無法進行 VIP 交換並收到錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="322cf-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="322cf-129">在部署更新進行期間不允許 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="322cf-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="322cf-130">部署更新可能在下列時間點自動執行：</span><span class="sxs-lookup"><span data-stu-id="322cf-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="322cf-131">新的客體作業系統可供使用時，和您設定要自動更新時。</span><span class="sxs-lookup"><span data-stu-id="322cf-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="322cf-132">服務修復執行時。</span><span class="sxs-lookup"><span data-stu-id="322cf-132">Service healing occurs.</span></span>

<span data-ttu-id="322cf-133">若要確認自動更新是否使您無法進行 VIP 交換：</span><span class="sxs-lookup"><span data-stu-id="322cf-133">To find out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="322cf-134">在 Azure 入口網站中，按一下您的雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="322cf-134">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="322cf-135">在 Azure 入口網站的 [屬性] 窗格中，查看 [狀態] 的值。</span><span class="sxs-lookup"><span data-stu-id="322cf-135">In the **Properties** pane of the Azure portal, look at the value of **Status**.</span></span> <span data-ttu-id="322cf-136">如果是 [就緒]，則查看 [前一個作業]，以確認最近執行的作業是否可能阻止 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="322cf-136">If it is **Ready**, then check **Last operation** to see if one recently happened that might prevent the VIP swap.</span></span>
3. <span data-ttu-id="322cf-137">為生產部署重複步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="322cf-137">Repeat steps 1 and 2 for the production deployment.</span></span>
4. <span data-ttu-id="322cf-138">如果自動更新正在進行中，請等候它完成再嘗試進行 VIP 交換。</span><span class="sxs-lookup"><span data-stu-id="322cf-138">If an automatic update is in process, wait for it to finish before trying to do the VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="322cf-139">問題：角色執行個體在 [已啟動]、[初始化中]、[忙碌] 和 [已停止] 之間循環</span><span class="sxs-lookup"><span data-stu-id="322cf-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="322cf-140">這種情況可能表示應用程式的程式碼、封裝或組態檔發生問題。</span><span class="sxs-lookup"><span data-stu-id="322cf-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="322cf-141">在此情況下，您應該能夠看見狀態每隔幾分鐘就會變更，且 Azure 入口網站可能顯示 [回收中]、[忙碌] 或 [正在初始化] 之類的訊息。</span><span class="sxs-lookup"><span data-stu-id="322cf-141">In that case, you should be able to see the status changing every few minutes and the Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="322cf-142">這表示應用程式發生了某些錯誤，導致角色執行個體無法執行。</span><span class="sxs-lookup"><span data-stu-id="322cf-142">This indicates that there is something wrong with the application that is keeping the role instance from running.</span></span>

<span data-ttu-id="322cf-143">如需如何對此問題進行疑難排解的詳細資訊，請參閱部落格文章 [Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)和[導致角色回收的常見問題](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)。</span><span class="sxs-lookup"><span data-stu-id="322cf-143">For more information on how to troubleshoot for this problem, see the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles to recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="322cf-144">問題：我的應用程式停止運作</span><span class="sxs-lookup"><span data-stu-id="322cf-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="322cf-145">在 Azure 入口網站中，按一下 [角色執行個體]。</span><span class="sxs-lookup"><span data-stu-id="322cf-145">In the Azure portal, click the role instance.</span></span>
2. <span data-ttu-id="322cf-146">在 Azure 入口網站的 [屬性]  窗格中，考量下列狀況以解決您的問題：</span><span class="sxs-lookup"><span data-stu-id="322cf-146">In the **Properties** pane of the Azure portal, consider the following conditions to resolve your problem:</span></span>
   * <span data-ttu-id="322cf-147">如果角色執行個體在最近停止 (您可以檢查 [中止計數] 的值)，部署可能正在更新。</span><span class="sxs-lookup"><span data-stu-id="322cf-147">If the role instance has recently stopped (you can check the value of **Abort count**), the deployment could be updating.</span></span> <span data-ttu-id="322cf-148">請等候並觀察角色執行個體是否會自行恢復運作。</span><span class="sxs-lookup"><span data-stu-id="322cf-148">Wait to see if the role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="322cf-149">如果角色執行個體處於 [忙碌] 狀態，請檢查應用程式的程式碼，查看 [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) 事件是否已處理。</span><span class="sxs-lookup"><span data-stu-id="322cf-149">If the role instance is **Busy**, check your application code to see if the [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="322cf-150">您可能需要新增或修正處理此事件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="322cf-150">You might need to add or fix some code that handles this event.</span></span>
   * <span data-ttu-id="322cf-151">請瀏覽部落格文章 [Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)中的診斷資料及疑難排解案例。</span><span class="sxs-lookup"><span data-stu-id="322cf-151">Go through the diagnostic data and troubleshooting scenarios in the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="322cf-152">如果您回收雲端服務，您會重設部署的屬性，而有效清除原始問題的資訊。</span><span class="sxs-lookup"><span data-stu-id="322cf-152">If you recycle your cloud service, you reset the properties for the deployment, effectively erasing the information for the original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="322cf-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="322cf-153">Next steps</span></span>
<span data-ttu-id="322cf-154">檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。</span><span class="sxs-lookup"><span data-stu-id="322cf-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="322cf-155">若要了解如何利用 Azure PaaS 電腦診斷資料對雲端服務角色問題進行疑難排解，請參閱 [Kevin Williamson 的部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。</span><span class="sxs-lookup"><span data-stu-id="322cf-155">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
