---
title: "Azure Vm 的 aaaDisaster 復原案例 |Microsoft 文件"
description: "了解哪些 toodo hello Azure 服務中斷影響 Azure 虛擬機器的事件中。"
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a><span data-ttu-id="920bf-103">Azure 服務中斷影響 Azure Vm 的 hello 事件中的哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="920bf-103">What toodo in hello event that an Azure service disruption impacts Azure VMs</span></span>
<span data-ttu-id="920bf-104">Microsoft 在我們處理硬 toomake 確定我們的服務時，都是永遠可用 tooyou 需要它們。</span><span class="sxs-lookup"><span data-stu-id="920bf-104">At Microsoft, we work hard toomake sure that our services are always available tooyou when you need them.</span></span> <span data-ttu-id="920bf-105">有時候因為不可抗力之影響，造成服務意外中斷。</span><span class="sxs-lookup"><span data-stu-id="920bf-105">Forces beyond our control sometimes impact us in ways that cause unplanned service disruptions.</span></span>

<span data-ttu-id="920bf-106">Microsoft 為其服務提供服務等級協定 (SLA)，作為執行時間和連接承諾。</span><span class="sxs-lookup"><span data-stu-id="920bf-106">Microsoft provides a Service Level Agreement (SLA) for its services as a commitment for uptime and connectivity.</span></span> <span data-ttu-id="920bf-107">hello SLA 個別 Azure 服務，請參閱[Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="920bf-107">hello SLA for individual Azure services can be found at [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="920bf-108">Azure 已經有許多支援高可用性應用程式的內建平台功能。</span><span class="sxs-lookup"><span data-stu-id="920bf-108">Azure already has many built-in platform features that support highly available applications.</span></span> <span data-ttu-id="920bf-109">如需這些服務的詳細資訊，請參閱 [Azure 應用程式的災害復原與高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="920bf-109">For more about these services, read [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

<span data-ttu-id="920bf-110">本文涵蓋真正的災害復原案例中，當整個地區發生中斷，因為 toomajor 天然災害或廣泛的服務中斷時。</span><span class="sxs-lookup"><span data-stu-id="920bf-110">This article covers a true disaster recovery scenario, when a whole region experiences an outage due toomajor natural disaster or widespread service interruption.</span></span> <span data-ttu-id="920bf-111">這些都是極少數的相符項目，但是您必須準備 hello 是整個區域發生中斷的可能性。</span><span class="sxs-lookup"><span data-stu-id="920bf-111">These are rare occurrences, but you must prepare for hello possibility that there is an outage of an entire region.</span></span> <span data-ttu-id="920bf-112">如果整個區域發生服務中斷，hello 本機備援份資料會暫時無法使用。</span><span class="sxs-lookup"><span data-stu-id="920bf-112">If an entire region experiences a service disruption, hello locally redundant copies of your data would temporarily be unavailable.</span></span> <span data-ttu-id="920bf-113">如果已啟用異地複寫，會在不同的區域儲存額外三份 Azure 儲存體 Blob 和資料表。</span><span class="sxs-lookup"><span data-stu-id="920bf-113">If you have enabled geo-replication, three additional copies of your Azure Storage blobs and tables are stored in a different region.</span></span> <span data-ttu-id="920bf-114">萬一 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原，Azure 重新對應所有 hello DNS 項目 toohello 進行地理複寫的區域。</span><span class="sxs-lookup"><span data-stu-id="920bf-114">In hello event of a complete regional outage or a disaster in which hello primary region is not recoverable, Azure remaps all of hello DNS entries toohello geo-replicated region.</span></span>

<span data-ttu-id="920bf-115">toohelp 處理這些極少數的發生次數，我們提供下列指引 Azure 虛擬網路中的 hello Azure 虛擬機器應用程式部署所在的整個區域服務中斷的 hello 大小寫的 hello。</span><span class="sxs-lookup"><span data-stu-id="920bf-115">toohelp you handle these rare occurrences, we provide hello following guidance for Azure virtual machines in hello case of a service disruption of hello entire region where your Azure virtual machine application is deployed.</span></span>

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a><span data-ttu-id="920bf-116">選項 1︰使用 Azure Site Recovery 起始容錯移轉</span><span class="sxs-lookup"><span data-stu-id="920bf-116">Option 1: Initiate a failover by using Azure Site Recovery</span></span>
<span data-ttu-id="920bf-117">您可以為 VM 設定 Azure Site Recovery，如此一來，只要按一下花幾分鐘就能復原應用程式。</span><span class="sxs-lookup"><span data-stu-id="920bf-117">You can configure Azure Site Recovery for your VMs so that you can recover your application with a single click in matter of minutes.</span></span> <span data-ttu-id="920bf-118">您可以在您選擇的 tooAzure 區域和不受限制的 toopaired 區域複寫。</span><span class="sxs-lookup"><span data-stu-id="920bf-118">You can replicate tooAzure region of your choice and not restricted toopaired regions.</span></span> <span data-ttu-id="920bf-119">您可以[複寫虛擬機器](https://aka.ms/a2a-getting-started)來開始進行。</span><span class="sxs-lookup"><span data-stu-id="920bf-119">You can get started by [replicating your virtual machines](https://aka.ms/a2a-getting-started).</span></span> <span data-ttu-id="920bf-120">您可以[建立復原計劃](../site-recovery/site-recovery-create-recovery-plans.md)，讓您可以自動化 hello 整個容錯移轉程序，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="920bf-120">You can [create a recovery plan](../site-recovery/site-recovery-create-recovery-plans.md) so that you can automate hello entire failover process for your application.</span></span> <span data-ttu-id="920bf-121">您可以[測試您的容錯移轉](../site-recovery/site-recovery-test-failover-to-azure.md)可以事先做好而不會影響實際執行應用程式或 hello 進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="920bf-121">You can [test your failovers](../site-recovery/site-recovery-test-failover-to-azure.md) beforehand without impacting production application or hello ongoing replication.</span></span> <span data-ttu-id="920bf-122">在您剛在 hello 事件中的主要區域中斷，[起始容錯移轉](../site-recovery/site-recovery-failover.md)目標區域中，讓您的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="920bf-122">In hello event of a primary region disruption, you just [initiate a failover](../site-recovery/site-recovery-failover.md) and bring your application in target region.</span></span>


## <a name="option-2-wait-for-recovery"></a><span data-ttu-id="920bf-123">選項 2︰等待復原</span><span class="sxs-lookup"><span data-stu-id="920bf-123">Option 2: Wait for recovery</span></span>
<span data-ttu-id="920bf-124">在此情況下，您不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="920bf-124">In this case, no action on your part is required.</span></span> <span data-ttu-id="920bf-125">知道，我們正努力 toorestore 服務可用性。</span><span class="sxs-lookup"><span data-stu-id="920bf-125">Know that we are working diligently toorestore service availability.</span></span> <span data-ttu-id="920bf-126">您可以看到 hello 目前服務的狀態上我們[Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。</span><span class="sxs-lookup"><span data-stu-id="920bf-126">You can see hello current service status on our [Azure Service Health Dashboard](https://azure.microsoft.com/status/).</span></span>

<span data-ttu-id="920bf-127">如果未設定 Azure 站台復原 」、 「 讀取權限地理備援儲存體或 「 地理備援儲存體先前 toohello 中斷，這會是 hello 最佳選項。</span><span class="sxs-lookup"><span data-stu-id="920bf-127">This is hello best option if you have not set up Azure Site Recovery, read-access geo-redundant storage, or geo-redundant storage prior toohello disruption.</span></span> <span data-ttu-id="920bf-128">如果您有設定地理備援儲存體或 hello 儲存體帳戶的讀取權限地理備援儲存體儲存 VM 虛擬硬碟 (Vhd)，您可以尋找 toorecover hello 基底映像 VHD，然後再次嘗試 tooprovision 中它的新 VM。</span><span class="sxs-lookup"><span data-stu-id="920bf-128">If you have set up geo-redundant storage or read-access geo-redundant storage for hello storage account where your VM virtual hard drives (VHDs) are stored, you can look toorecover hello base image VHD and try tooprovision a new VM from it.</span></span> <span data-ttu-id="920bf-129">因為不保證能夠同步處理資料，所以這不是慣用的選項。</span><span class="sxs-lookup"><span data-stu-id="920bf-129">This is not a preferred option because there are no guarantees of synchronization of data.</span></span> <span data-ttu-id="920bf-130">因此，此選項不保證 toowork。</span><span class="sxs-lookup"><span data-stu-id="920bf-130">Consequently, this option is not guaranteed toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="920bf-131">請注意，您完全無法控制這個程序，而且它只有在全區域服務中斷時才會發生。</span><span class="sxs-lookup"><span data-stu-id="920bf-131">Be aware that you do not have any control over this process, and it will only occur for region-wide service disruptions.</span></span> <span data-ttu-id="920bf-132">因為這個緣故，您必須也依賴其他應用程式特定的備份策略 tooachieve hello 最高層級的可用性。</span><span class="sxs-lookup"><span data-stu-id="920bf-132">Because of this, you must also rely on other application-specific backup strategies tooachieve hello highest level of availability.</span></span> <span data-ttu-id="920bf-133">如需詳細資訊，請參閱 hello 一節[災害復原的資料策略](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery)。</span><span class="sxs-lookup"><span data-stu-id="920bf-133">For more information, see hello section on [Data strategies for disaster recovery](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="920bf-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="920bf-134">Next steps</span></span>

- <span data-ttu-id="920bf-135">使用 Azure Site Recovery 開始[保護在 Azure 虛擬機器上執行的應用程式](https://aka.ms/a2a-getting-started)</span><span class="sxs-lookup"><span data-stu-id="920bf-135">Start [protecting your applications running on Azure virtual machines](https://aka.ms/a2a-getting-started) using Azure Site Recovery</span></span>

- <span data-ttu-id="920bf-136">深入了解如何 tooimplement 災害復原和高可用性策略，請參閱 toolearn[災害復原與高可用性 Azure 應用程式](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="920bf-136">toolearn more about how tooimplement a disaster recovery and high availability strategy, see [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).</span></span>

- <span data-ttu-id="920bf-137">toodevelop 詳細了解技術的雲端平台的功能，請參閱[Azure 復原技術的指引](../resiliency/resiliency-technical-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="920bf-137">toodevelop a detailed technical understanding of a cloud platform’s capabilities, see [Azure resiliency technical guidance](../resiliency/resiliency-technical-guidance.md).</span></span>


- <span data-ttu-id="920bf-138">如果 hello 指示不清除，或如果您想要代表您的 Microsoft toodo hello 作業，請連絡[客戶支援](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。</span><span class="sxs-lookup"><span data-stu-id="920bf-138">If hello instructions are not clear, or if you would like Microsoft toodo hello operations on your behalf, contact [Customer Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
