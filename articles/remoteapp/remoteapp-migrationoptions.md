---
title: "移轉超出 Azure RemoteApp aaaOptions |Microsoft 文件"
description: "深入了解 Azure RemoteApp 超出移轉 hello 選項。"
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
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="e32e4-103">移出 Azure RemoteApp 的選項</span><span class="sxs-lookup"><span data-stu-id="e32e4-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e32e4-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="e32e4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e32e4-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e32e4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="e32e4-106">如果您已停止使用 Azure RemoteApp，因為 hello[淘汰公告](https://go.microsoft.com/fwlink/?linkid=821148)或因為您已完成評估版，您需要 toomigrate 移出 Azure RemoteApp tooanother 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="e32e4-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="e32e4-107">移轉有兩種不同的方法︰自我管理 (通常稱為基礎結構即服務 [IaaS]) 部署，或完全受管理 (通常稱為平台即服務或軟體即服務 [PaaS/SaaS]) 供應項目。</span><span class="sxs-lookup"><span data-stu-id="e32e4-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="e32e4-108">自助服務的 IaaS 是由您管理、操作及擁有的自己動手部署，可直接部署在虛擬機器 (VM) 或實體系統上。</span><span class="sxs-lookup"><span data-stu-id="e32e4-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="e32e4-109">在其他 hello 結束，完全受管理的 PaaS/SaaS 供應項目多個要 Azure RemoteApp-夥伴提供服務之上的層級處理操作在遠端處理解決方案以及服務時，hello 客戶執行一些映像和應用程式管理。</span><span class="sxs-lookup"><span data-stu-id="e32e4-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="e32e4-110">[移轉選項上檢視 hello Azure RemoteApp 網路研討會](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp)，或閱讀並了解詳細資訊 （包括 hello 不同裝載選項的範例）。</span><span class="sxs-lookup"><span data-stu-id="e32e4-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="e32e4-111">自我管理的 (IaaS) 解決方案</span><span class="sxs-lookup"><span data-stu-id="e32e4-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="e32e4-112">**IaaS 上的 RDS**</span><span class="sxs-lookup"><span data-stu-id="e32e4-112">**RDS on IaaS**</span></span>
<span data-ttu-id="e32e4-113">您可以使用 RemoteApp 或內部部署桌上型電腦或在託管環境 (如 Azure Vm 上) 中，部署以工作階段為基礎的原生遠端桌面服務 (在 Windows Server 中) 部署。</span><span class="sxs-lookup"><span data-stu-id="e32e4-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="e32e4-114">IaaS 部署上的 RDS 最適合於已經熟悉 RDS 部署且具備其現有技術專業知識的客戶。</span><span class="sxs-lookup"><span data-stu-id="e32e4-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="e32e4-115">您需要大量授權的軟體保證 (SA) 的 RDS 用戶端存取授權 toouse 此部署選項。</span><span class="sxs-lookup"><span data-stu-id="e32e4-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="e32e4-116">在 Azure VM 上部署 RDS 比以往您使用部署和修補範本時還要容易 (請讀取[概觀](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/)，然後 [加以取得](https://aka.ms/rdautomation))。</span><span class="sxs-lookup"><span data-stu-id="e32e4-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="e32e4-117">您可以取得 hello 相同彈性調整能力與 Azure RemoteApp 中的 Azure 傳統部署模型資源 （不是 Azure 資源模型資源） 使用 hello[自動調整指令碼](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76)，不過，當有多個自訂與設定。</span><span class="sxs-lookup"><span data-stu-id="e32e4-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="e32e4-118">當您部署 Azure Vm 上的 RDS 時，透過提供支援[Azure 支援](https://azure.microsoft.com/support/plans/)，hello 相同的技術支援工程師支援您的 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="e32e4-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="e32e4-119">您可以取得成本連絡來根據現有的使用量估算[Azure 支援](https://azure.microsoft.com/support/plans/)，您可以自行執行計算或使用 toobe 立即釋放成本計算機。</span><span class="sxs-lookup"><span data-stu-id="e32e4-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="e32e4-120">此外，N 系列 Vm （目前在私人預覽中） 您可以新增 vGPU-太多有關加入 vGPU 支援，以及有關如何聽到[駕馭 RDS 改善 Windows Server 2016 中的](https://myignite.microsoft.com/videos/2794)我們 Ignite 工作階段中。</span><span class="sxs-lookup"><span data-stu-id="e32e4-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="e32e4-121">我們有逐步部署指南[Windows Server 2012 R2](http://aka.ms/rdsonazure)和[Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist 與您的部署。</span><span class="sxs-lookup"><span data-stu-id="e32e4-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="e32e4-122">簽出 hello[遠端桌面部落格](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services)如 hello 最新消息。</span><span class="sxs-lookup"><span data-stu-id="e32e4-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="e32e4-123">**IaaS 上的 Citrix**</span><span class="sxs-lookup"><span data-stu-id="e32e4-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="e32e4-124">以工作階段為基礎之 XenApp 或 XenDesktop 的原生 Citrix 部署，可以部署於內部部署或託管環境中 (例如在 Azure VM 上)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="e32e4-125">簽出 hello 逐步部署指南 》，[在 Azure 上的 Citrix XA 7.6](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx)，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e32e4-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="e32e4-126">深入了解 [Azure 上的 Citrix](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx)，包括價格計算機。</span><span class="sxs-lookup"><span data-stu-id="e32e4-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="e32e4-127">您也可以尋找[Citrix 連絡人](http://citrix.com/English/contact/index.asp)toodiscuss 您使用的選項。</span><span class="sxs-lookup"><span data-stu-id="e32e4-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="e32e4-128">完全受管理的 (PaaS/SaaS) 供應項目</span><span class="sxs-lookup"><span data-stu-id="e32e4-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="e32e4-129">Citrix XenApp Essentials (2017 年 4 月發行)</span><span class="sxs-lookup"><span data-stu-id="e32e4-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="e32e4-130">現在可在 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials)、 Citrix XenApp Essentials 為新應用程式虛擬化服務 hello，結合 hello 電源和彈性的 hello 與 hello 簡單，不夠，Citrix 雲端平台和輕鬆使用 Microsoft Azure RemoteApp 願景。</span><span class="sxs-lookup"><span data-stu-id="e32e4-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="e32e4-131">現有 Azure RemoteApp 客戶可以 [註冊免費試用](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="e32e4-132">注意：只有 Citrix 使用者服務費免費，仍須收取 Azure 計算和儲存體費用</span><span class="sxs-lookup"><span data-stu-id="e32e4-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="e32e4-133">深入了解：</span><span class="sxs-lookup"><span data-stu-id="e32e4-133">Learn More:</span></span>
- [<span data-ttu-id="e32e4-134">從 Azure RemoteApp tooCitrix XenApp Essentials 移轉</span><span class="sxs-lookup"><span data-stu-id="e32e4-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- <span data-ttu-id="e32e4-135">[Citrix 和 Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="e32e4-135">[Citrix and Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)</span></span>
- <span data-ttu-id="e32e4-136">[Citrix XenApp Essentials 簡報](https://www.youtube.com/watch?v=91Z7CCfQ-9k) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="e32e4-137">Citrix Cloud XenApp 服務和 XenDesktop 服務</span><span class="sxs-lookup"><span data-stu-id="e32e4-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="e32e4-138">[Citrix 雲端 XenApp 服務和 XenDesktop 服務](https://www.citrix.com/products/citrix-cloud/services.html)是 hello hello 傳遞的同時應用程式和桌面，以及進階的管理和監視功能的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="e32e4-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="e32e4-139">Conexlink (平台名稱︰MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="e32e4-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="e32e4-140">[MyCloudIT](https://mycloudit.com)是和 IT 公司 toosimplify，一個自動化平台最佳化及調整 hello 移轉遠端桌面、 遠端的應用程式和基礎結構中的傳送 hello Microsoft Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="e32e4-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="e32e4-141">hello MyCloudIT 平台降低 95%，成本 30%的 Azure 部署時間，並將其用戶端的整個 IT 基礎結構移至 hello 雲端中的幾個按鍵。</span><span class="sxs-lookup"><span data-stu-id="e32e4-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="e32e4-142">夥伴可以立即管理客戶從一個通用的儀表板，hello 世界各地的服務使用者前所未有，成長而不會增加額外負荷或廣泛 Azure 訓練的營收。</span><span class="sxs-lookup"><span data-stu-id="e32e4-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="e32e4-143">主要地點︰美國德州達拉斯</span><span class="sxs-lookup"><span data-stu-id="e32e4-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="e32e4-144">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e32e4-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="e32e4-145">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="e32e4-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="e32e4-146">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-147">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-148">Azure RemoteApp 移轉解決方案︰是，[深入了解](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="e32e4-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="e32e4-149">Brian Garoutte, VP of Business Development</span><span class="sxs-lookup"><span data-stu-id="e32e4-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="e32e4-150">電話：972-218-0741</span><span class="sxs-lookup"><span data-stu-id="e32e4-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="e32e4-151">電子郵件：[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="e32e4-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="e32e4-152">Frame</span><span class="sxs-lookup"><span data-stu-id="e32e4-152">Frame</span></span>

<span data-ttu-id="e32e4-153">IT 組織中企業和政府、 受管理的服務提供者和前置的軟體廠商選擇框架 toocreate 及管理其安全的軟體定義的工作區 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="e32e4-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="e32e4-154">從小型 toolarge 組織畫面格，讓非常容易 toolet 使用者從任何裝置存取的任何瀏覽器上的 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e32e4-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="e32e4-155">hello 框架平台包括的所有項目從 hello 雲端包括 hello Azure 基礎結構和 RDS 授權系統管理需求 toodeploy 應用程式 （攜帶您自己的 Azure 帳戶和授權是選擇性的）。</span><span class="sxs-lookup"><span data-stu-id="e32e4-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="e32e4-156">深入了解 [Azure 上的 Frame](https://www.fra.me/ara)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="e32e4-157">主要位置︰美國加州的聖馬刁</span><span class="sxs-lookup"><span data-stu-id="e32e4-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="e32e4-158">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e32e4-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="e32e4-159">Microsoft 合作夥伴：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="e32e4-160">電話：1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="e32e4-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="e32e4-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="e32e4-161">Awingu</span></span>
<span data-ttu-id="e32e4-162">Awingu 提供執行傳統應用程式的簡易線上工作區解決方案、SaaS 和 html5 瀏覽器的文件。</span><span class="sxs-lookup"><span data-stu-id="e32e4-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="e32e4-163">這麼一來，即可在任何類型的裝置上安全地使用任何應用程式，</span><span class="sxs-lookup"><span data-stu-id="e32e4-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="e32e4-164">而 SaaS 服務也可使用多種單一登入選項。</span><span class="sxs-lookup"><span data-stu-id="e32e4-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="e32e4-165">此外，多樣化 (雲端) 檔案系統可深入整合至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="e32e4-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="e32e4-166">下一步 toofull 行動力，Awingu 的豐富線上工作區，將會獲得最佳的安全性與細微的控制 （例如下載/上傳）、 多重要素驗證 (例如 Azure MFA)、 工作階段錄製和多個稽核的完整使用量。</span><span class="sxs-lookup"><span data-stu-id="e32e4-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="e32e4-167">現成的 Awingu 可讓您分享文件和應用程式工作階段，以達到最佳化和安全的工作作業。</span><span class="sxs-lookup"><span data-stu-id="e32e4-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="e32e4-168">Awingu 的解決方案是多租用戶、多 AD 和開放式 API。</span><span class="sxs-lookup"><span data-stu-id="e32e4-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="e32e4-169">小型和大型企業、雲端服務提供者和 [Isv](http://www.isv2saas.com) 使用此解決方案。</span><span class="sxs-lookup"><span data-stu-id="e32e4-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="e32e4-170">這些客戶特別喜歡 hello 容易使用，方便安裝與低 TCO。</span><span class="sxs-lookup"><span data-stu-id="e32e4-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="e32e4-171">Awingu All-in-one 合一是[hello Azure Marketplace 中可用](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm)與 2 內建的並行使用者。</span><span class="sxs-lookup"><span data-stu-id="e32e4-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="e32e4-172">其他授權可透過 [廣大的經銷商和轉售商](http://www.awingu.com/reseller) 取得。</span><span class="sxs-lookup"><span data-stu-id="e32e4-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="e32e4-173">深入了解[Awingu 上的做為替代 tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="e32e4-174">主要地點︰比利時</span><span class="sxs-lookup"><span data-stu-id="e32e4-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="e32e4-175">作業區域：EMEA、北美洲和巴西</span><span class="sxs-lookup"><span data-stu-id="e32e4-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="e32e4-176">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="e32e4-177">全域：</span><span class="sxs-lookup"><span data-stu-id="e32e4-177">**Global**:</span></span>
> 
> <span data-ttu-id="e32e4-178">Arnaud Marlière，CMO</span><span class="sxs-lookup"><span data-stu-id="e32e4-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="e32e4-179">電子郵件：[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e32e4-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="e32e4-180">電話：+1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="e32e4-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="e32e4-181">**比利時總部**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="e32e4-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="e32e4-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="e32e4-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="e32e4-183">9000 Gent</span></span>
> 
> <span data-ttu-id="e32e4-184">電子郵件：[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e32e4-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="e32e4-185">電話：+32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="e32e4-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="e32e4-186">美國：</span><span class="sxs-lookup"><span data-stu-id="e32e4-186">**USA**:</span></span>
> 
> <span data-ttu-id="e32e4-187">第 7 floor、 1177 Ave 的 hello 美洲，</span><span class="sxs-lookup"><span data-stu-id="e32e4-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="e32e4-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="e32e4-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="e32e4-189">電子郵件：[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="e32e4-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="e32e4-190">Microsoft 託管服務提供者</span><span class="sxs-lookup"><span data-stu-id="e32e4-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="e32e4-191">主控夥伴通常會提供完整的管理裝載的 Windows 桌面和應用程式服務，其中可能包含管理 hello Azure 資源、 作業系統、 應用程式，使用 hello 夥伴的技術服務人員的授權合約與 Microsoft 和正在服務提供者授權合約 tooallow 充任訂戶存取授權 (SAL) 以及其他軟體提供者。</span><span class="sxs-lookup"><span data-stu-id="e32e4-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="e32e4-192">hello 下列資訊提供詳細資料和部分特製化協助客戶使用他們的 Azure RemoteApp 移轉中的 hello 主控者的連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="e32e4-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="e32e4-193">簽出[hello 目前裝載的服務提供者的清單](http://aka.ms/rdsonazurecertified)，已完成 hello RDS 學習路徑和評估 IaaS 上。</span><span class="sxs-lookup"><span data-stu-id="e32e4-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="e32e4-194">Citrix 服務提供者方案</span><span class="sxs-lookup"><span data-stu-id="e32e4-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="e32e4-195">hello Citrix 服務提供者程式輕鬆虛擬雲端運算 tooSMBs 中，提供他們希望方便且隨用隨付模型中的 hello 服務的服務提供者 toodeliver hello 簡易性。</span><span class="sxs-lookup"><span data-stu-id="e32e4-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="e32e4-196">Citrix 服務提供者增加其 Microsoft SPLA 企業和展開其 RDS 平台投資與任何裝置、 隨處存取、 hello 範圍最廣泛的應用程式支援、 豐富的體驗，提高的安全性和增強的延展性。</span><span class="sxs-lookup"><span data-stu-id="e32e4-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="e32e4-197">接著，Citrix 服務提供者可吸引更多訂閱者、提高客戶滿意度並降低其營運成本。</span><span class="sxs-lookup"><span data-stu-id="e32e4-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="e32e4-198">[深入了解](http://www.citrix.com/products/service-providers.html)或[尋找合作夥伴](https://www.citrix.com/buy/partnerlocator.html)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="e32e4-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="e32e4-199">Acuutech</span></span>
<span data-ttu-id="e32e4-200">[Acuutech](http://www.acuutech.com)專門用來提供託管桌面的解決方案，提供完整的桌面和 ISV 應用程式 Microsoft 技術 tooa 全域用戶端上建置基底他們自己的資料中心與 Azure 的體驗。</span><span class="sxs-lookup"><span data-stu-id="e32e4-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="e32e4-201">主要地點︰英國倫敦、新加坡、休士頓、德州</span><span class="sxs-lookup"><span data-stu-id="e32e4-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="e32e4-202">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e32e4-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="e32e4-203">合作夥伴狀態︰金級</span><span class="sxs-lookup"><span data-stu-id="e32e4-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="e32e4-204">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-205">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-206">Azure RemoteApp 移轉解決方案︰是，[深入了解](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="e32e4-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="e32e4-207">**英國**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="e32e4-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="e32e4-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="e32e4-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="e32e4-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="e32e4-210">電話：+44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="e32e4-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="e32e4-211">**新加坡**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="e32e4-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="e32e4-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="e32e4-213">hello 地球，新加坡 069532</span><span class="sxs-lookup"><span data-stu-id="e32e4-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="e32e4-214">電話：+65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="e32e4-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="e32e4-215">**北美洲**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-215">**North America**:</span></span>
>   
> <span data-ttu-id="e32e4-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="e32e4-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="e32e4-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="e32e4-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="e32e4-218">電話：+1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="e32e4-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="e32e4-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="e32e4-219">ASPEX</span></span>
<span data-ttu-id="e32e4-220">[ASPEX](http://www.aspex.be/en)專門用來轉換 toohello 雲端和 ISV Isv ' 尋找 toooptimize 其目前的雲端設定。</span><span class="sxs-lookup"><span data-stu-id="e32e4-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="e32e4-221">ASPEX 會提供廣泛的受管理服務、開發和諮詢服務。</span><span class="sxs-lookup"><span data-stu-id="e32e4-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="e32e4-222">主要地點︰比利時安特衛普</span><span class="sxs-lookup"><span data-stu-id="e32e4-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="e32e4-223">營運區域︰西歐</span><span class="sxs-lookup"><span data-stu-id="e32e4-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="e32e4-224">合作夥伴狀態︰[銀級](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="e32e4-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="e32e4-225">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-226">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-227">Azure RemoteApp 移轉解決方案︰是，[深入了解](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="e32e4-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="e32e4-228">電話︰+3232202198</span><span class="sxs-lookup"><span data-stu-id="e32e4-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="e32e4-229">電子郵件︰[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="e32e4-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="e32e4-230">Web：[http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="e32e4-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="e32e4-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="e32e4-231">Caase.com</span></span>
<span data-ttu-id="e32e4-232">[Caase.com](http://www.caase.com/)可協助企業、 本機政府、 非政府主體以及與 hello Microsoft 雲端中的工作更聰明的方式向其旅程醫療保健機構。</span><span class="sxs-lookup"><span data-stu-id="e32e4-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="e32e4-233">無論身在何處或使用何種裝置，您都能在安全的環境下發揮生產力，而不需要支付昂貴的 IT 成本。</span><span class="sxs-lookup"><span data-stu-id="e32e4-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="e32e4-234">Caase.com 是真正專精於 Microsoft Office 365、Azure、Enterprise Mobility + Security 及 Windows 的專家。</span><span class="sxs-lookup"><span data-stu-id="e32e4-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="e32e4-235">透過我們的諮詢、移轉服務、採用計畫、訓練、管理和支援，Caase.com 能夠為客戶的員工、合作夥伴和供應商建立最佳化且安全的共同作業平台。</span><span class="sxs-lookup"><span data-stu-id="e32e4-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="e32e4-236">Caase.com 是 hello mastermind hello Azure 遠端工作區 （行動場所中） 和 hello 數位工作場所 （社交內部網路）。</span><span class="sxs-lookup"><span data-stu-id="e32e4-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="e32e4-237">這兩種解決方案 – 完成與採用 – 是 hello foundation 可確保這些解決方案的 hello 使用者在其路由 toohello Microsoft 雲端具有 hello 最愉快、 成功且有效的經驗。</span><span class="sxs-lookup"><span data-stu-id="e32e4-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="e32e4-238">荷蘭文翻譯和支援影片的位址為：http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="e32e4-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="e32e4-239">營運區域：以荷蘭為基礎，觸角擴及全球</span><span class="sxs-lookup"><span data-stu-id="e32e4-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="e32e4-240">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="e32e4-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="e32e4-241">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-242">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-243">Azure RemoteApp 移轉解決方案︰是。[深入了解](http://caase.com/diensten/microsoft-azure/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="e32e4-244">荷蘭：</span><span class="sxs-lookup"><span data-stu-id="e32e4-244">Netherlands:</span></span>
> 
> <span data-ttu-id="e32e4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="e32e4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="e32e4-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="e32e4-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="e32e4-247">電話：+31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="e32e4-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="e32e4-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="e32e4-248">Nerdio</span></span>
<span data-ttu-id="e32e4-249">[Azure Nerdio](http://getnerdio.com/nfa/)是傳遞 hello Microsoft 雲端為非常簡單的佈建、 管理和最佳化的 IT 環境中完成的 IT 自動化平台。</span><span class="sxs-lookup"><span data-stu-id="e32e4-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="e32e4-250">只需要幾小時，您就能建立虛擬桌面、遠端應用程式和伺服器。</span><span class="sxs-lookup"><span data-stu-id="e32e4-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="e32e4-251">管理 hello 環境中按三下或更少與 Nerdio 系統管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="e32e4-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="e32e4-252">使用智慧型的自動調整並儲存在 Azure IaaS 資源 40 too60%。</span><span class="sxs-lookup"><span data-stu-id="e32e4-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="e32e4-253">主要位置：伊利諾伊州芝加哥，營運區域：全球，合作夥伴狀態：[金級](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1)，Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-254">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-255">Azure RemoteApp 移轉解決方案：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="e32e4-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="e32e4-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="e32e4-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="e32e4-257">Suite 212</span></span>
> 
> <span data-ttu-id="e32e4-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="e32e4-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="e32e4-259">USA</span><span class="sxs-lookup"><span data-stu-id="e32e4-259">USA</span></span>
> 
> <span data-ttu-id="e32e4-260">(844) 4NERDIO 分機6</span><span class="sxs-lookup"><span data-stu-id="e32e4-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="e32e4-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="e32e4-261">**SaaSplaza**</span></span>
<span data-ttu-id="e32e4-262">[SaaSplaza](http://www.saasplaza.com/) 提供完整的 Microsoft Dynamics 組合 (NAV、AX、GP、SL、CRM) 私人和公用雲端 (Azure)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="e32e4-263">主要位置︰荷蘭</span><span class="sxs-lookup"><span data-stu-id="e32e4-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="e32e4-264">營運區域︰全球</span><span class="sxs-lookup"><span data-stu-id="e32e4-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="e32e4-265">合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="e32e4-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="e32e4-266">Microsoft Cloud 服務提供者：是</span><span class="sxs-lookup"><span data-stu-id="e32e4-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="e32e4-267">提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者</span><span class="sxs-lookup"><span data-stu-id="e32e4-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="e32e4-268">**歐洲、中東與非洲**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="e32e4-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="e32e4-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="e32e4-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="e32e4-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="e32e4-271">hello 荷蘭</span><span class="sxs-lookup"><span data-stu-id="e32e4-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="e32e4-272">電話：+31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="e32e4-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="e32e4-273">**美洲**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-273">**Americas**:</span></span>
> 
> <span data-ttu-id="e32e4-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="e32e4-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="e32e4-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="e32e4-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="e32e4-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="e32e4-276">San Diego</span></span>
> 
> <span data-ttu-id="e32e4-277">美國</span><span class="sxs-lookup"><span data-stu-id="e32e4-277">United States</span></span>
> 
> <span data-ttu-id="e32e4-278">電話：+1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="e32e4-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="e32e4-279">**亞太地區**：</span><span class="sxs-lookup"><span data-stu-id="e32e4-279">**APAC**:</span></span>
> 
> <span data-ttu-id="e32e4-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="e32e4-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="e32e4-281">\#11-08 版 hello 八邊形</span><span class="sxs-lookup"><span data-stu-id="e32e4-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="e32e4-282">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="e32e4-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="e32e4-283">新加坡</span><span class="sxs-lookup"><span data-stu-id="e32e4-283">Singapore</span></span>
>   
> <span data-ttu-id="e32e4-284">電話 - 新加坡：+65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="e32e4-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="e32e4-285">電話 - 澳大利亞：+61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="e32e4-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="e32e4-286">電話 - 紐西蘭：+64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="e32e4-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="e32e4-287">需要其他協助？</span><span class="sxs-lookup"><span data-stu-id="e32e4-287">Need more help?</span></span>
<span data-ttu-id="e32e4-288">仍然需要協助進行選擇，或有進一步的問題？</span><span class="sxs-lookup"><span data-stu-id="e32e4-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="e32e4-289">使用下列方法 tooget 說明 hello 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="e32e4-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="e32e4-290">請透過下列電子郵件地址連絡我們：[arainfo@microsoft.com](mailto:arainfo@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="e32e4-291">連絡 [Azure 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="e32e4-292">從開啟 [Azure 支援案例](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)著手。</span><span class="sxs-lookup"><span data-stu-id="e32e4-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="e32e4-293">致電給我們。</span><span class="sxs-lookup"><span data-stu-id="e32e4-293">Call us.</span></span> <span data-ttu-id="e32e4-294">[尋找當地的銷售代表電話](https://azure.microsoft.com/overview/sales-number/)。</span><span class="sxs-lookup"><span data-stu-id="e32e4-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

