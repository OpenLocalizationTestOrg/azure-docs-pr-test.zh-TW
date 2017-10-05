---
title: "Operations Management Suite (OMS) 架構 | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  本文會說明 OMS 中包含的各種服務，並提供其詳細內容的連結。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 76f69946724b5297b1f9a1f715819c69c4a4a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="oms-architecture"></a><span data-ttu-id="76aa3-104">OMS 架構</span><span class="sxs-lookup"><span data-stu-id="76aa3-104">OMS architecture</span></span>
<span data-ttu-id="76aa3-105">[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) 是管理內部部署和雲端環境的雲端型服務集合。</span><span class="sxs-lookup"><span data-stu-id="76aa3-105">[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) is a collection of cloud-based services for managing your on-premises and cloud environments.</span></span>  <span data-ttu-id="76aa3-106">本文描述 OMS 的不同內部部署和雲端元件以及其高階雲端運算架構。</span><span class="sxs-lookup"><span data-stu-id="76aa3-106">This article describes the different on-premises and cloud components of OMS and their high level cloud computing architecture.</span></span>  <span data-ttu-id="76aa3-107">您可以參考每個服務的文件，以取得進一步詳細資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-107">You can refer to the documentation for each service for further details.</span></span>

## <a name="log-analytics"></a><span data-ttu-id="76aa3-108">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="76aa3-108">Log Analytics</span></span>
<span data-ttu-id="76aa3-109">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) 收集的所有資料都會儲存到裝載於 Azure 的 OMS 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="76aa3-109">All data collected by [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) is stored in the OMS repository which is hosted in Azure.</span></span>  <span data-ttu-id="76aa3-110">已連接來源會產生收集到 OMS 儲存機制的資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-110">Connected Sources generate data collected into the OMS repository.</span></span>  <span data-ttu-id="76aa3-111">目前支援三種類型的已連接來源。</span><span class="sxs-lookup"><span data-stu-id="76aa3-111">There are currently three types of connected sources supported.</span></span>

* <span data-ttu-id="76aa3-112">[Windows](../log-analytics/log-analytics-windows-agents.md) 或 [Linux](../log-analytics/log-analytics-linux-agents.md) 電腦上所安裝的代理程式會直接連接到 OMS。</span><span class="sxs-lookup"><span data-stu-id="76aa3-112">An agent installed on a [Windows](../log-analytics/log-analytics-windows-agents.md) or [Linux](../log-analytics/log-analytics-linux-agents.md) computer connected directly to OMS.</span></span>
* <span data-ttu-id="76aa3-113">System Center Operations Manager (SCOM) 管理群組 [連接到 Log Analytics](../log-analytics/log-analytics-om-agents.md) 。</span><span class="sxs-lookup"><span data-stu-id="76aa3-113">A System Center Operations Manager (SCOM) management group [connected to Log Analytics](../log-analytics/log-analytics-om-agents.md) .</span></span>  <span data-ttu-id="76aa3-114">SCOM 代理程式會繼續與管理伺服器通訊，而管理伺服器會將資料和效能資料轉送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="76aa3-114">SCOM agents continue to communicate with management servers which forward events and performance data to Log Analytics.</span></span>
* <span data-ttu-id="76aa3-115">[Azure 儲存體帳戶](../log-analytics/log-analytics-azure-storage.md)，收集 Azure 背景工作角色、Web 角色或虛擬機器中的 [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) 資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-115">An [Azure storage account](../log-analytics/log-analytics-azure-storage.md) that collects [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) data from a worker role, web role, or virtual machine in Azure.</span></span>

<span data-ttu-id="76aa3-116">資料來源可定義 Log Analytics 從已連接來源 (包括事件記錄檔和效能計數器) 收集的資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-116">Data sources define the data that Log Analytics collects from connected sources including event logs and performance counters.</span></span>  <span data-ttu-id="76aa3-117">解決方案可新增 OMS 的功能，而且可以輕鬆地從 [OMS 解決方案庫](../log-analytics/log-analytics-add-solutions.md)新增到您的工作區。</span><span class="sxs-lookup"><span data-stu-id="76aa3-117">Solutions add functionality to OMS and can easily be added to your workspace from the [OMS Solutions Gallery](../log-analytics/log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="76aa3-118">有些解決方案可能需要從 SCOM 代理程式直接連接到 Log Analytics，有些則可能需要安裝其他代理程式。</span><span class="sxs-lookup"><span data-stu-id="76aa3-118">Some solutions may require a direct connection to Log Analytics from SCOM agents while others may require an additional agent to be installed.</span></span>

<span data-ttu-id="76aa3-119">Log Analytics 的 Web 型入口網站可用來管理 OMS 資源、新增和設定 OMS 解決方案，以及檢視和分析 OMS 儲存機制中的資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-119">Log Analytics has a web-based portal that you can use to manage OMS resources, add and configure OMS solutions, and view and analyze data in the OMS repository.</span></span>

![Log Analytics 高階架構](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a><span data-ttu-id="76aa3-121">Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="76aa3-121">Azure Automation</span></span>
<span data-ttu-id="76aa3-122">[Azure 自動化 Runbook](http://azure.microsoft.com/documentation/services/automation) 是在 Azure 雲端中執行，而且可以存取 Azure 或其他雲端服務中的資源，或可從公用網際網路存取的資源。</span><span class="sxs-lookup"><span data-stu-id="76aa3-122">[Azure Automation runbooks](http://azure.microsoft.com/documentation/services/automation) are executed in the Azure cloud and can access resources that are in Azure, in other cloud services, or accessible from the public Internet.</span></span>  <span data-ttu-id="76aa3-123">您也可以使用[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) 指定本機資料中心的內部部署電腦，讓 Runbook 可以存取本機資源。</span><span class="sxs-lookup"><span data-stu-id="76aa3-123">You can also designate on-premises machines in your local data center using [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md) so that runbooks can access local resources.</span></span>

<span data-ttu-id="76aa3-124">[DSC 組態](../automation/automation-dsc-overview.md) 可以直接套用到 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="76aa3-124">[DSC configurations](../automation/automation-dsc-overview.md) stored in Azure Automation can be directly applied to Azure virtual machines.</span></span>  <span data-ttu-id="76aa3-125">其他實體和虛擬機器可以從 Azure 自動化 DSC 提取伺服器中要求組態。</span><span class="sxs-lookup"><span data-stu-id="76aa3-125">Other physical and virtual machines can request configurations from the Azure Automation DSC pull server.</span></span>

<span data-ttu-id="76aa3-126">Azure 自動化的 OMS 解決方案會顯示統計資料，以及啟動 Azure 入口網站進行任何作業的連結。</span><span class="sxs-lookup"><span data-stu-id="76aa3-126">Azure Automation has an OMS solution that displays statistics and links to launch the Azure portal for any operations.</span></span>

![Azure 自動化高階架構](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a><span data-ttu-id="76aa3-128">Azure 備份</span><span class="sxs-lookup"><span data-stu-id="76aa3-128">Azure Backup</span></span>
<span data-ttu-id="76aa3-129">[Azure 備份](http://azure.microsoft.com/documentation/services/backup) 中的受保護資料儲存在位於特定地理區域的備份保存庫中。</span><span class="sxs-lookup"><span data-stu-id="76aa3-129">Protected data in [Azure Backup](http://azure.microsoft.com/documentation/services/backup) is stored in a backup vault located in a particular geographic region.</span></span>  <span data-ttu-id="76aa3-130">資料是在相同的區域內進行複寫，而且根據保存庫類型，也可能會複寫到另一個區域，以進行進一步備援。</span><span class="sxs-lookup"><span data-stu-id="76aa3-130">The data is replicated within the same region and, depending on the type of vault, may also be replicated to another region for further redundancy.</span></span>

<span data-ttu-id="76aa3-131">Azure 備份有三種基本案例。</span><span class="sxs-lookup"><span data-stu-id="76aa3-131">Azure Backup has three fundamental scenarios.</span></span>

* <span data-ttu-id="76aa3-132">具有 Azure 備份代理程式的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="76aa3-132">Windows machine with Azure Backup agent.</span></span>  <span data-ttu-id="76aa3-133">這可讓您將任何 Windows 伺服器或用戶端中的檔案和資料夾直接備份到 Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="76aa3-133">This allows you to backup files and folders from any Windows server or client directly to your Azure backup vault.</span></span>  
* <span data-ttu-id="76aa3-134">System Center Data Protection Manager (DPM) 或 Microsoft Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="76aa3-134">System Center Data Protection Manager (DPM) or Microsoft Azure Backup Server.</span></span> <span data-ttu-id="76aa3-135">這可讓您運用 DPM 或 Microsoft Azure 備份伺服器，將檔案和資料夾以及 SQL 和 SharePoint 這類應用程式工作負載備份到本機儲存體，然後再複寫到 Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="76aa3-135">This allows you to leverage DPM or Microsoft Azure Backup Server to backup files and folders in addition to application workloads such as SQL and SharePoint to local storage and then replicate to your Azure backup vault.</span></span>
* <span data-ttu-id="76aa3-136">Azure 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="76aa3-136">Azure Virtual Machine Extensions.</span></span>  <span data-ttu-id="76aa3-137">這可讓您將 Azure 虛擬機器備份到 Azure 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="76aa3-137">This allows you to backup Azure virtual machines to your Azure backup vault.</span></span>

<span data-ttu-id="76aa3-138">Azure 備份的 OMS 解決方案會顯示統計資料，以及啟動 Azure 入口網站進行任何作業的連結。</span><span class="sxs-lookup"><span data-stu-id="76aa3-138">Azure Backup has an OMS solution that displays statistics and links to launch the Azure portal for any operations.</span></span>

![Azure 備份高階架構](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a><span data-ttu-id="76aa3-140">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="76aa3-140">Azure Site Recovery</span></span>
<span data-ttu-id="76aa3-141">[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) 可協調虛擬機器和實體伺服器的複寫、容錯移轉和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="76aa3-141">[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) orchestrates replication, failover, and failback of virtual machines and physical servers.</span></span> <span data-ttu-id="76aa3-142">複寫資料會在 Hyper-V 主機、VMware Hypervisor 與主要和次要資料中心內的實體伺服器之間進行交換，或是在資料中心與 Azure 儲存體之間進行交換。</span><span class="sxs-lookup"><span data-stu-id="76aa3-142">Replication data is exchanged between Hyper-V hosts, VMware hypervisors, and physical servers in primary and secondary datacenters, or between the datacenter and Azure storage.</span></span>  <span data-ttu-id="76aa3-143">Site Recovery 會將元資料儲存到位於特定地理 Azure 區域的保存庫中。</span><span class="sxs-lookup"><span data-stu-id="76aa3-143">Site Recovery stores metadata in vaults located in a particular geographic Azure region.</span></span> <span data-ttu-id="76aa3-144">Site Recovery 服務不會儲存任何複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="76aa3-144">No replicated data is stored by the Site Recovery service.</span></span>

<span data-ttu-id="76aa3-145">Azure Site Recovery 有三種基本複寫案例。</span><span class="sxs-lookup"><span data-stu-id="76aa3-145">Azure Site Recovery has three fundamental replication scenarios.</span></span>

<span data-ttu-id="76aa3-146">**Hyper-V 虛擬機器的複寫**</span><span class="sxs-lookup"><span data-stu-id="76aa3-146">**Replication of Hyper-V virtual machines**</span></span>

* <span data-ttu-id="76aa3-147">如果 Hyper-V 虛擬機器是在 VMM 雲端中進行管理，則您可以複寫到次要資料來源或 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="76aa3-147">If Hyper-V virtual machines are managed in VMM clouds, you can replicate to a secondary data center or to Azure storage.</span></span>  <span data-ttu-id="76aa3-148">複寫到 Azure 是透過安全的網際網路連線進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-148">Replication to Azure is over a secure internet connection.</span></span>  <span data-ttu-id="76aa3-149">複寫到次要資料中心是透過 LAN 來進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-149">Replication to a secondary datacenter is over the LAN.</span></span>
* <span data-ttu-id="76aa3-150">如果 VMM 未管理 Hyper-V 虛擬機器，則您只能複寫到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="76aa3-150">If Hyper-V virtual machines aren’t managed by VMM, you can replicate to Azure storage only.</span></span>  <span data-ttu-id="76aa3-151">複寫到 Azure 是透過安全的網際網路連線進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-151">Replication to Azure is over a secure internet connection.</span></span>

<span data-ttu-id="76aa3-152">**VMWare 虛擬機器的複寫**</span><span class="sxs-lookup"><span data-stu-id="76aa3-152">**Replication of VMWare virtual machines**</span></span>

* <span data-ttu-id="76aa3-153">您可以將 VMware 虛擬機器複寫到執行 VMware 的次要資料中心或是 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="76aa3-153">You can replicate VMware virtual machines to a secondary datacenter running VMware or to Azure storage.</span></span>  <span data-ttu-id="76aa3-154">複寫到 Azure 可以透過站對站 VPN、Azure ExpressRoute 或安全的網際網路連線進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-154">Replication to Azure can occur over a site-to-site VPN or Azure ExpressRoute or over a secure Internet connection.</span></span> <span data-ttu-id="76aa3-155">複寫到次要資料中心是透過 InMage Scout 資料通道進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-155">Replication to a secondary datacenter occurs over the InMage Scout data channel.</span></span>

<span data-ttu-id="76aa3-156">**實體 Windows 和 Linux 伺服器的複寫**</span><span class="sxs-lookup"><span data-stu-id="76aa3-156">**Replication of physical Windows and Linux servers**</span></span> 

* <span data-ttu-id="76aa3-157">您可以將實體伺服器複寫到次要資料中心或 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="76aa3-157">You can replicate physical servers to a secondary datacenter or to Azure storage.</span></span> <span data-ttu-id="76aa3-158">複寫到 Azure 可以透過站對站 VPN、Azure ExpressRoute 或安全的網際網路連線進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-158">Replication to Azure can occur over a site-to-site VPN or Azure ExpressRoute or over a secure Internet connection.</span></span> <span data-ttu-id="76aa3-159">複寫到次要資料中心是透過 InMage Scout 資料通道進行。</span><span class="sxs-lookup"><span data-stu-id="76aa3-159">Replication to a secondary datacenter occurs over the InMage Scout data channel.</span></span>  <span data-ttu-id="76aa3-160">Azure Site Recovery 的 OMS 解決方案會顯示一些統計資料，但必須使用 Azure 入口網站進行所有作業。</span><span class="sxs-lookup"><span data-stu-id="76aa3-160">Azure Site Recovery has an OMS solution that displays some statistics, but you must use the Azure portal for any operations.</span></span>

![Azure Site Recovery 高階架構](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a><span data-ttu-id="76aa3-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76aa3-162">Next steps</span></span>
* <span data-ttu-id="76aa3-163">了解 [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)。</span><span class="sxs-lookup"><span data-stu-id="76aa3-163">Learn about [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).</span></span>
* <span data-ttu-id="76aa3-164">了解 [Azure 自動化](https://azure.microsoft.com/documentation/services/automation)。</span><span class="sxs-lookup"><span data-stu-id="76aa3-164">Learn about [Azure Automation](https://azure.microsoft.com/documentation/services/automation).</span></span>
* <span data-ttu-id="76aa3-165">了解 [Azure 備份](http://azure.microsoft.com/documentation/services/backup)。</span><span class="sxs-lookup"><span data-stu-id="76aa3-165">Learn about [Azure Backup](http://azure.microsoft.com/documentation/services/backup).</span></span>
* <span data-ttu-id="76aa3-166">了解 [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)。</span><span class="sxs-lookup"><span data-stu-id="76aa3-166">Learn about [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).</span></span>

