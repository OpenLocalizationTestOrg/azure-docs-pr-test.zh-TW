---
title: "移出 Azure RemoteApp 的選項 | Microsoft Docs"
description: "了解移出 Azure RemoteApp 的選項。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="e5bb8-103">移出 Azure RemoteApp 的選項</span><span class="sxs-lookup"><span data-stu-id="e5bb8-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e5bb8-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e5bb8-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="e5bb8-106">如果您因為[停用公告](https://go.microsoft.com/fwlink/?linkid=821148)或因為您已完成評估而停止使用 Azure RemoteApp，您需要從 Azure RemoteApp 移轉至另一個應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="e5bb8-107">移轉有兩種不同的方法︰自我管理 (通常稱為基礎結構即服務 [IaaS]) 部署，或完全受管理 (通常稱為平台即服務或軟體即服務 [PaaS/SaaS]) 供應項目。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="e5bb8-108">自助服務的 IaaS 是由您管理、操作及擁有的自己動手部署，可直接部署在虛擬機器 (VM) 或實體系統上。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="e5bb8-109">另一方面，完全受管理的 PaaS/SaaS 供應項目比較像 Azure RemoteApp - 合作夥伴會在遠端解決方案之上提供一個可處理操作和服務事宜的服務層，而身為客戶的您，只要進行一些映像和應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="e5bb8-110">[ Azure RemoteApp 網路研討會](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp)，或閱讀更多詳細資訊 (包括不同裝載選項的範例)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="e5bb8-111">自我管理的 (IaaS) 解決方案</span><span class="sxs-lookup"><span data-stu-id="e5bb8-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="e5bb8-112">**IaaS 上的 RDS**</span><span class="sxs-lookup"><span data-stu-id="e5bb8-112">**RDS on IaaS**</span></span>
<span data-ttu-id="e5bb8-113">您可以使用 RemoteApp 或內部部署桌上型電腦或在託管環境 (如 Azure Vm 上) 中，部署以工作階段為基礎的原生遠端桌面服務 (在 Windows Server 中) 部署。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="e5bb8-114">IaaS 部署上的 RDS 最適合於已經熟悉 RDS 部署且具備其現有技術專業知識的客戶。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="e5bb8-115">您需要 RDS 用戶端存取授權的大量授權與軟體保證 (SA)，才能使用此部署選項。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="e5bb8-116">在 Azure VM 上部署 RDS 比以往您使用部署和修補範本時還要容易 (請讀取[概觀](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/)，然後 [加以取得](https://aka.ms/rdautomation))。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="e5bb8-117">您可以使用[自動調整指令碼](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76)，在 Azure RemoteApp 內取得與 Azure 傳統部署模型資源 (而非 Azure 資源模型資源) 相同的彈性調整功能，不過有更多的自訂和設定功能。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="e5bb8-118">當您在 Azure VM 上部署 RDS 時，會透過 [Azure 支援](https://azure.microsoft.com/support/plans/) (為您提供 Azure RemoteApp 支援的相同支援專業人員) 提供支援。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="e5bb8-119">您可以連絡 [Azure 支援](https://azure.microsoft.com/support/plans/)，也可以使用即將發行的成本計算機自行執行計算，以取得以現有使用量為基礎的成本估計。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="e5bb8-120">此外，在 N 系列 VM (目前處於私人預覽狀態) 中，您可以新增 vGPU - 深入了解如何新增 vGPU，以及如何在我們的 Ignite 工作階段中[控管 Windows Server 2016 中的 RDS 改進](https://myignite.microsoft.com/videos/2794)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="e5bb8-121">我們提供 [Windows Server 2012 R2](http://aka.ms/rdsonazure) 和 [Windows Server 2016](http://aka.ms/rdsonazure2016) 的逐步部署指南，協助您進行部署。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="e5bb8-122">查看[遠端桌面部落格](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services)中的最新消息。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="e5bb8-123">**IaaS 上的 Citrix**</span><span class="sxs-lookup"><span data-stu-id="e5bb8-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="e5bb8-124">以工作階段為基礎之 XenApp 或 XenDesktop 的原生 Citrix 部署，可以部署於內部部署或託管環境中 (例如在 Azure VM 上)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="e5bb8-125">如需詳細資訊，請參閱逐步部署指南 ([Azure 上的 Citrix XA 7.6](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx))。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="e5bb8-126">深入了解 [Azure 上的 Citrix](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx)，包括價格計算機。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="e5bb8-127">您也可以找到 [Citrix 連絡人](http://citrix.com/English/contact/index.asp)一起討論您的選項。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="e5bb8-128">完全受管理的 (PaaS/SaaS) 供應項目</span><span class="sxs-lookup"><span data-stu-id="e5bb8-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="e5bb8-129">Citrix XenApp Essentials (2017 年 4 月發行)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="e5bb8-130">Citrix XenApp Essentials 現在已在 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials) 上推出，是新的應用程式虛擬化服務，將 Citrix Cloud 平台的優勢和彈性與 Microsoft Azure RemoteApp 簡單、規範性和便於取用的願景結合。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="e5bb8-131">現有 Azure RemoteApp 客戶可以 [註冊免費試用](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="e5bb8-132">注意：只有 Citrix 使用者服務費免費，仍須收取 Azure 計算和儲存體費用</span><span class="sxs-lookup"><span data-stu-id="e5bb8-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="e5bb8-133">深入了解：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-133">Learn More:</span></span>
- [<span data-ttu-id="e5bb8-134">從 Azure RemoteApp 移轉到 Citrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="e5bb8-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- <span data-ttu-id="e5bb8-135">[Citrix 和 Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-135">[Citrix and Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)</span></span>
- <span data-ttu-id="e5bb8-136">[Citrix XenApp Essentials 簡報](https://www.youtube.com/watch?v=91Z7CCfQ-9k) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="e5bb8-137">Citrix Cloud XenApp 服務和 XenDesktop 服務</span><span class="sxs-lookup"><span data-stu-id="e5bb8-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="e5bb8-138">[Citrix Cloud XenApp 服務和 XenDesktop 服務](https://www.citrix.com/products/citrix-cloud/services.html)是傳遞應用程式和桌面，以及進階管理和監視功能的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="e5bb8-139">Conexlink (平台名稱︰MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="e5bb8-140">[MyCloudIT](https://mycloudit.com) 是一個自動化平台，可供 IT 公司簡化、最佳化和調整移轉，以及在 Microsoft Azure 雲端中提供遠端桌面、遠端應用程式和基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="e5bb8-141">MyCloudIT 平台可減少 95% 的部署時間、30% 的 Azure 成本，而且只要按幾個按鍵，即可將其用戶端的整個 IT 基礎結構移到雲端。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="e5bb8-142">協力廠商現在可以從通用儀表板管理客戶、以前所未有的方式服務世界各地的使用者，並且讓營收成長，但不會增加額外的負荷或廣泛 Azure 訓練。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="e5bb8-143">主要地點︰美國德州達拉斯</span><span class="sxs-lookup"><span data-stu-id="e5bb8-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="e5bb8-144">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e5bb8-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="e5bb8-145">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="e5bb8-146">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-147">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-148">Azure RemoteApp 移轉解決方案︰是，[深入了解](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="e5bb8-149">Brian Garoutte, VP of Business Development</span><span class="sxs-lookup"><span data-stu-id="e5bb8-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="e5bb8-150">電話：972-218-0741</span><span class="sxs-lookup"><span data-stu-id="e5bb8-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="e5bb8-151">電子郵件：[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="e5bb8-152">Frame</span><span class="sxs-lookup"><span data-stu-id="e5bb8-152">Frame</span></span>

<span data-ttu-id="e5bb8-153">企業和政府中的 IT 組織、受管理的服務提供者和主要軟體供應商都選擇 Frame 來建立和管理其雲端中的安全、軟體定義程式的工作區。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="e5bb8-154">從小型到大型組織，Frame 讓使用者可以非常輕鬆地從任何裝置及任何瀏覽器上存取 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="e5bb8-155">Frame 平台包含系統管理員需要的所有項目以從雲端部署應用程式，包括 Azure 基礎結構和 RDS 授權 (可選擇性使用自己的 Azure 帳戶和授權)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="e5bb8-156">深入了解 [Azure 上的 Frame](https://www.fra.me/ara)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="e5bb8-157">主要位置︰美國加州的聖馬刁</span><span class="sxs-lookup"><span data-stu-id="e5bb8-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="e5bb8-158">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e5bb8-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="e5bb8-159">Microsoft 合作夥伴：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-160">電話：1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="e5bb8-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="e5bb8-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="e5bb8-161">Awingu</span></span>
<span data-ttu-id="e5bb8-162">Awingu 提供執行傳統應用程式的簡易線上工作區解決方案、SaaS 和 html5 瀏覽器的文件。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="e5bb8-163">這麼一來，即可在任何類型的裝置上安全地使用任何應用程式，</span><span class="sxs-lookup"><span data-stu-id="e5bb8-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="e5bb8-164">而 SaaS 服務也可使用多種單一登入選項。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="e5bb8-165">此外，多樣化 (雲端) 檔案系統可深入整合至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="e5bb8-166">除了完整的行動力之外，Awingu 豐富的線上工作區也會提供最佳的安全性及細微控制 (如下載/上傳)、完整的使用稽核、多重要素驗證 (如 Azure MFA)、工作階段記錄等等。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="e5bb8-167">現成的 Awingu 可讓您分享文件和應用程式工作階段，以達到最佳化和安全的工作作業。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="e5bb8-168">Awingu 的解決方案是多租用戶、多 AD 和開放式 API。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="e5bb8-169">小型和大型企業、雲端服務提供者和 [Isv](http://www.isv2saas.com) 使用此解決方案。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="e5bb8-170">這些客戶特別喜愛使用簡單、安裝簡單和低 TCO 等特點。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="e5bb8-171">Awingu All-in-One 於 [Azure Marketplace 上推出](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm)，具有 2 個內建的並行使用者。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="e5bb8-172">其他授權可透過 [廣大的經銷商和轉售商](http://www.awingu.com/reseller) 取得。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="e5bb8-173">深入了解 [做為 Azure RemoteApp 替代方案的 Awingu](http://alternative-for-azure-remoteapp.awingu.com/)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="e5bb8-174">主要地點︰比利時</span><span class="sxs-lookup"><span data-stu-id="e5bb8-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="e5bb8-175">作業區域：EMEA、北美洲和巴西</span><span class="sxs-lookup"><span data-stu-id="e5bb8-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="e5bb8-176">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="e5bb8-177">全域：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-177">**Global**:</span></span>
> 
> <span data-ttu-id="e5bb8-178">Arnaud Marlière，CMO</span><span class="sxs-lookup"><span data-stu-id="e5bb8-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="e5bb8-179">電子郵件：[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="e5bb8-180">電話：+1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="e5bb8-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="e5bb8-181">**比利時總部**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="e5bb8-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="e5bb8-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="e5bb8-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="e5bb8-183">9000 Gent</span></span>
> 
> <span data-ttu-id="e5bb8-184">電子郵件：[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="e5bb8-185">電話：+32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="e5bb8-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="e5bb8-186">美國：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-186">**USA**:</span></span>
> 
> <span data-ttu-id="e5bb8-187">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="e5bb8-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="e5bb8-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="e5bb8-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="e5bb8-189">電子郵件：[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="e5bb8-190">Microsoft 託管服務提供者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="e5bb8-191">託管協力廠商通常會依照協力廠商與 Microsoft 和其他軟體提供者簽訂的授權合約，以及允許轉售訂戶存取授權 (SAL) 的服務提供者授權合約，提供完全受管理的託管 Windows 桌面和應用程式服務，可能包括管理 Azure 資源、作業系統、應用程式和技術服務。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="e5bb8-192">下列資訊針對某些專門協助客戶處理其 Azure RemoteApp 移轉的主機服務提供者，提供詳細資料和連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="e5bb8-193">查看目前已完成 RDS on IaaS 學習路徑和評估的[託管服務提供者清單](http://aka.ms/rdsonazurecertified)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="e5bb8-194">Citrix 服務提供者方案</span><span class="sxs-lookup"><span data-stu-id="e5bb8-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="e5bb8-195">「Citrix 服務提供者方案」讓服務提供者能輕鬆提供簡單的虛擬雲端運算功能給中小企業，並以簡單、隨收隨付的模式提供他們想要的服務。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="e5bb8-196">Citrix 服務提供者可利用任何裝置、隨處存取、最廣泛的應用程式支援、豐富的經驗、提升的安全性和延展性，使其 Microsoft SPLA 業務成長茁壯，並擴充其 RDS 平台投資。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="e5bb8-197">接著，Citrix 服務提供者可吸引更多訂閱者、提高客戶滿意度並降低其營運成本。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="e5bb8-198">[深入了解](http://www.citrix.com/products/service-providers.html)或[尋找合作夥伴](https://www.citrix.com/buy/partnerlocator.html)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="e5bb8-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="e5bb8-199">Acuutech</span></span>
<span data-ttu-id="e5bb8-200">[Acuutech](http://www.acuutech.com) 專門提供託管桌面解決方案，並從 Azure 與其自己的資料中心將以 Microsoft 技術為基礎的完整桌面和 ISV 應用程式體驗提供給全球客戶群。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="e5bb8-201">主要地點︰英國倫敦、新加坡、休士頓、德州</span><span class="sxs-lookup"><span data-stu-id="e5bb8-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="e5bb8-202">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e5bb8-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="e5bb8-203">合作夥伴狀態︰金級</span><span class="sxs-lookup"><span data-stu-id="e5bb8-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="e5bb8-204">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-205">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-206">Azure RemoteApp 移轉解決方案︰是，[深入了解](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="e5bb8-207">**英國**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="e5bb8-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="e5bb8-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="e5bb8-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="e5bb8-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="e5bb8-210">電話：+44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="e5bb8-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="e5bb8-211">**新加坡**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="e5bb8-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="e5bb8-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="e5bb8-213">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="e5bb8-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="e5bb8-214">電話：+65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="e5bb8-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="e5bb8-215">**北美洲**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-215">**North America**:</span></span>
>   
> <span data-ttu-id="e5bb8-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="e5bb8-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="e5bb8-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="e5bb8-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="e5bb8-218">電話：+1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="e5bb8-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="e5bb8-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="e5bb8-219">ASPEX</span></span>
<span data-ttu-id="e5bb8-220">[ASPEX](http://www.aspex.be/en) 專精於從 ISV 轉換至雲端，而 ISV 想要將其目前的雲端設定最佳化。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="e5bb8-221">ASPEX 會提供廣泛的受管理服務、開發和諮詢服務。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="e5bb8-222">主要地點︰比利時安特衛普</span><span class="sxs-lookup"><span data-stu-id="e5bb8-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="e5bb8-223">營運區域︰西歐</span><span class="sxs-lookup"><span data-stu-id="e5bb8-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="e5bb8-224">合作夥伴狀態︰[銀級](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="e5bb8-225">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-226">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-227">Azure RemoteApp 移轉解決方案︰是，[深入了解](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="e5bb8-228">電話︰+3232202198</span><span class="sxs-lookup"><span data-stu-id="e5bb8-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="e5bb8-229">電子郵件︰[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="e5bb8-230">Web：[http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="e5bb8-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="e5bb8-231">Caase.com</span></span>
<span data-ttu-id="e5bb8-232">[Caase.com](http://www.caase.com/) \(英文\) 能協助企業、地方政府、非政府機構和醫療保健機構在 Microsoft Cloud 中開始以更聰明的方式工作。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="e5bb8-233">無論身在何處或使用何種裝置，您都能在安全的環境下發揮生產力，而不需要支付昂貴的 IT 成本。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="e5bb8-234">Caase.com 是真正專精於 Microsoft Office 365、Azure、Enterprise Mobility + Security 及 Windows 的專家。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="e5bb8-235">透過我們的諮詢、移轉服務、採用計畫、訓練、管理和支援，Caase.com 能夠為客戶的員工、合作夥伴和供應商建立最佳化且安全的共同作業平台。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="e5bb8-236">Caase.com 是 Azure 遠端工作區 (行動工作區) 和數位工作區 (社交內部網路) 的幕後功臣。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="e5bb8-237">這兩個已被廣為採納的解決方案，能確保解決方案使用者在開始使用 Microsoft Cloud 的過程中，能夠享有最愉快、成功和有效的體驗。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="e5bb8-238">荷蘭文翻譯和支援影片的位址為：http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="e5bb8-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="e5bb8-239">營運區域：以荷蘭為基礎，觸角擴及全球</span><span class="sxs-lookup"><span data-stu-id="e5bb8-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="e5bb8-240">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="e5bb8-241">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-242">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-243">Azure RemoteApp 移轉解決方案︰是。[深入了解](http://caase.com/diensten/microsoft-azure/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="e5bb8-244">荷蘭：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-244">Netherlands:</span></span>
> 
> <span data-ttu-id="e5bb8-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="e5bb8-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="e5bb8-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="e5bb8-247">電話：+31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="e5bb8-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="e5bb8-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="e5bb8-248">Nerdio</span></span>
<span data-ttu-id="e5bb8-249">[Nerdio for Azure](http://getnerdio.com/nfa/) \(英文\) 為 IT 自動化平台，可在 Microsoft Cloud 中提供完整 IT 環境的極簡化佈建、管理和最佳化。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="e5bb8-250">只需要幾小時，您就能建立虛擬桌面、遠端應用程式和伺服器。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="e5bb8-251">透過 Nerdio 管理入口網站，使用者最多只要按三下，便能開始管理環境。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="e5bb8-252">透過智慧型自動調整來節省 40% 至 60% 的 Azure IaaS 資源。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="e5bb8-253">主要位置：伊利諾伊州芝加哥，營運區域：全球，合作夥伴狀態：[金級](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1)，Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-254">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-255">Azure RemoteApp 移轉解決方案：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="e5bb8-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="e5bb8-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="e5bb8-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="e5bb8-257">Suite 212</span></span>
> 
> <span data-ttu-id="e5bb8-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="e5bb8-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="e5bb8-259">USA</span><span class="sxs-lookup"><span data-stu-id="e5bb8-259">USA</span></span>
> 
> <span data-ttu-id="e5bb8-260">(844) 4NERDIO 分機</span><span class="sxs-lookup"><span data-stu-id="e5bb8-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="e5bb8-261">6</span><span class="sxs-lookup"><span data-stu-id="e5bb8-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="e5bb8-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="e5bb8-262">**SaaSplaza**</span></span>
<span data-ttu-id="e5bb8-263">[SaaSplaza](http://www.saasplaza.com/) 提供完整的 Microsoft Dynamics 組合 (NAV、AX、GP、SL、CRM) 私人和公用雲端 (Azure)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="e5bb8-264">主要位置︰荷蘭</span><span class="sxs-lookup"><span data-stu-id="e5bb8-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="e5bb8-265">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e5bb8-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="e5bb8-266">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="e5bb8-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="e5bb8-267">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e5bb8-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e5bb8-268">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e5bb8-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e5bb8-269">**歐洲、中東與非洲**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="e5bb8-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="e5bb8-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="e5bb8-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="e5bb8-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="e5bb8-272">The Netherlands</span><span class="sxs-lookup"><span data-stu-id="e5bb8-272">The Netherlands</span></span>
> 
> <span data-ttu-id="e5bb8-273">電話：+31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="e5bb8-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="e5bb8-274">**美洲**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-274">**Americas**:</span></span>
> 
> <span data-ttu-id="e5bb8-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="e5bb8-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="e5bb8-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="e5bb8-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="e5bb8-277">San Diego</span><span class="sxs-lookup"><span data-stu-id="e5bb8-277">San Diego</span></span>
> 
> <span data-ttu-id="e5bb8-278">美國</span><span class="sxs-lookup"><span data-stu-id="e5bb8-278">United States</span></span>
> 
> <span data-ttu-id="e5bb8-279">電話：+1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="e5bb8-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="e5bb8-280">**亞太地區**：</span><span class="sxs-lookup"><span data-stu-id="e5bb8-280">**APAC**:</span></span>
> 
> <span data-ttu-id="e5bb8-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="e5bb8-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="e5bb8-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="e5bb8-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="e5bb8-283">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="e5bb8-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="e5bb8-284">新加坡</span><span class="sxs-lookup"><span data-stu-id="e5bb8-284">Singapore</span></span>
>   
> <span data-ttu-id="e5bb8-285">電話 - 新加坡：+65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="e5bb8-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="e5bb8-286">電話 - 澳大利亞：+61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="e5bb8-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="e5bb8-287">電話 - 紐西蘭：+64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="e5bb8-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="e5bb8-288">需要其他協助？</span><span class="sxs-lookup"><span data-stu-id="e5bb8-288">Need more help?</span></span>
<span data-ttu-id="e5bb8-289">仍然需要協助進行選擇，或有進一步的問題？</span><span class="sxs-lookup"><span data-stu-id="e5bb8-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="e5bb8-290">使用下列其中一種方法來取得協助。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="e5bb8-291">請透過下列電子郵件地址連絡我們：[arainfo@microsoft.com](mailto:arainfo@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="e5bb8-292">連絡 [Azure 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="e5bb8-293">從開啟 [Azure 支援案例](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)著手。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="e5bb8-294">致電給我們。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-294">Call us.</span></span> <span data-ttu-id="e5bb8-295">[尋找當地的銷售代表電話](https://azure.microsoft.com/overview/sales-number/)。</span><span class="sxs-lookup"><span data-stu-id="e5bb8-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

