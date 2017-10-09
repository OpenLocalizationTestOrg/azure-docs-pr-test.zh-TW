---
title: "aaaProtect Active Directory 和 DNS 與 Azure Site Recovery |Microsoft 文件"
description: "本文章說明如何使用 Azure Site Recovery 的 Active Directory 的嚴重損壞修復解決方案 tooimplement。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a><span data-ttu-id="c7770-103">以 Azure Site Recovery 保護 Active Directory 和 DNS</span><span class="sxs-lookup"><span data-stu-id="c7770-103">Protect Active Directory and DNS with Azure Site Recovery</span></span>
<span data-ttu-id="c7770-104">企業應用程式，例如 SharePoint、 Dynamics AX 和 SAP 取決於 Active Directory 和 DNS 基礎結構 toofunction 正確。</span><span class="sxs-lookup"><span data-stu-id="c7770-104">Enterprise applications such as SharePoint, Dynamics AX, and SAP depend on Active Directory and a DNS infrastructure toofunction correctly.</span></span> <span data-ttu-id="c7770-105">當您建立應用程式的災害復原解決方案時，它是您需要 tooprotect，並復原之前 hello 的 Active Directory 和 DNS 的重要 tooremember 其他應用程式元件、 tooensure 當災害發生時，項目正常運作。</span><span class="sxs-lookup"><span data-stu-id="c7770-105">When you create a disaster recovery solution for applications, it's important tooremember that you need tooprotect and recover Active Directory and DNS before hello other application components, tooensure that things function correctly when disaster occurs.</span></span>

<span data-ttu-id="c7770-106">Site Recovery 是一項 Azure 服務，可藉由協調虛擬機器的複寫、容錯移轉及復原，提供災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="c7770-106">Site Recovery is an Azure service that provides disaster recovery by orchestrating replication, failover, and recovery of virtual machines.</span></span> <span data-ttu-id="c7770-107">站台復原支援複寫案例 tooconsistently 保護，且順暢地容錯移轉虛擬機器和應用程式 tooprivate、 public 或主機服務提供者雲端的數的字。</span><span class="sxs-lookup"><span data-stu-id="c7770-107">Site Recovery supports a number of replication scenarios tooconsistently protect, and seamlessly failover virtual machines and applications tooprivate, public, or hoster clouds.</span></span>

<span data-ttu-id="c7770-108">使用 Site Recovery，您可以針對 Active Directory 建立一個完整的自動化災害復原計畫。</span><span class="sxs-lookup"><span data-stu-id="c7770-108">Using Site Recovery, you can create a complete automated disaster recovery plan for Active Directory.</span></span> <span data-ttu-id="c7770-109">當發生中斷情況時，您可以在幾秒鐘內從任何地方起始容錯移轉，並在數分鐘內啟動並執行 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c7770-109">When disruptions occur, you can initiate a failover within seconds from anywhere and get Active Directory up and running in a few minutes.</span></span> <span data-ttu-id="c7770-110">如果您已部署 Active Directory 的多個應用程式，例如 SharePoint 和 SAP 中您的主要站台，而且您想 toofail 在 hello 完成站台上，您可以容錯移轉第一個使用 Active Directory 站台復原，然後容錯移轉 hello 其他應用程式使用應用程式專屬復原計劃。</span><span class="sxs-lookup"><span data-stu-id="c7770-110">If you've deployed Active Directory for multiple applications such as SharePoint and SAP in your primary site, and you want toofail over hello complete site, you can fail over Active Directory first using Site Recovery, and then fail over hello other applications using application-specific recovery plans.</span></span>

<span data-ttu-id="c7770-111">本文說明如何 toocreate Active Directory 的災害復原方案、 如何 tooperform 規劃、 未規劃，並使用一種單鍵復原計劃的測試容錯移轉 hello 支援的組態和必要條件。</span><span class="sxs-lookup"><span data-stu-id="c7770-111">This article explains how toocreate a disaster recovery solution for Active Directory, how tooperform planned, unplanned, and test failovers using a one-click recovery plan, hello supported configurations, and prerequisites.</span></span>  <span data-ttu-id="c7770-112">開始之前，您應該先熟悉 Active Directory 與 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="c7770-112">You should be familiar with Active Directory and Azure Site Recovery before you start.</span></span>

## <a name="replicating-domain-controller"></a><span data-ttu-id="c7770-113">複寫網域控制站</span><span class="sxs-lookup"><span data-stu-id="c7770-113">Replicating Domain Controller</span></span>

<span data-ttu-id="c7770-114">您需要 toosetup[站台復原複寫](#enable-protection-using-site-recovery)至少一個裝載網域控制站和 DNS 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="c7770-114">You need toosetup [Site Recovery replication](#enable-protection-using-site-recovery) on at least one virtual machine hosting Domain Controller and DNS.</span></span> <span data-ttu-id="c7770-115">如果您有[多個網域控制站](#environment-with-multiple-domain-controllers)在環境中，此外 tooreplicating hello 網域控制站虛擬機器使用站台復原也將最多有 tooset[其他網域控制站](#protect-active-directory-with-active-directory-replication) hello 目標站台 （Azure 或內部次要資料中心） 上。</span><span class="sxs-lookup"><span data-stu-id="c7770-115">If you have [multiple domain controllers](#environment-with-multiple-domain-controllers) in your environment, in addition tooreplicating hello domain controller virtual machine with Site Recovery you would also have tooset up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on hello target site (Azure or a secondary on-premises datacenter).</span></span> 

### <a name="single-domain-controller-environment"></a><span data-ttu-id="c7770-116">單一網域控制站環境</span><span class="sxs-lookup"><span data-stu-id="c7770-116">Single domain controller environment</span></span>
<span data-ttu-id="c7770-117">如果您有少數應用程式和只有單一網域控制站，和您想 toofail 在 hello 整個站台上，則建議使用 Site Recovery tooreplicate hello 網域控制站 toohello 次要站台 (您是否無法透過 tooAzure 或tooa 次要站台）。</span><span class="sxs-lookup"><span data-stu-id="c7770-117">If you have a few applications and only a single domain controller, and you want toofail over hello entire site together, then we recommend using Site Recovery tooreplicate hello domain controller toohello secondary site (whether you're failing over tooAzure or tooa secondary site).</span></span> <span data-ttu-id="c7770-118">hello 相同複寫的網域控制站/DNS 虛擬機器可用於[測試容錯移轉](#test-failover-considerations)以及。</span><span class="sxs-lookup"><span data-stu-id="c7770-118">hello same replicated domain controller/DNS virtual machine can be used for [test failover](#test-failover-considerations) as well.</span></span>

### <a name="environment-with-multiple-domain-controllers"></a><span data-ttu-id="c7770-119">含有多個網域控制站的環境</span><span class="sxs-lookup"><span data-stu-id="c7770-119">Environment with multiple domain controllers</span></span>
<span data-ttu-id="c7770-120">如果您有許多應用程式和多個網域控制站在 hello 環境中，或是如果您打算 toofail 一些應用程式上一次，我們建議，此外 tooreplicating hello 網域控制站虛擬機器的 Site Recovery 您也設定[其他網域控制站](#protect-active-directory-with-active-directory-replication)hello 目標站台 （Azure 或內部次要資料中心） 上。</span><span class="sxs-lookup"><span data-stu-id="c7770-120">If you have many applications and there's more than one domain controller in hello environment, or if you plan toofail over a few applications at a time, we recommend that in addition tooreplicating hello domain controller virtual machine with Site Recovery you also set up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on hello target site (Azure or a secondary on-premises datacenter).</span></span> <span data-ttu-id="c7770-121">如[測試容錯移轉](#test-failover-considerations)，您可以使用複寫的站台復原和容錯移轉，hello hello 目標站台上的其他網域控制站的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c7770-121">For [test failover](#test-failover-considerations), you use domain controller replicated by Site Recovery and for failover, hello additional domain controller on hello target site.</span></span> 


<span data-ttu-id="c7770-122">hello 下列各節說明如何 tooenable 保護 Site Recovery 中的網域控制站以及如何在 Azure 中的網域控制站 tooset。</span><span class="sxs-lookup"><span data-stu-id="c7770-122">hello following sections explain how tooenable protection for a domain controller in Site Recovery, and how tooset up a domain controller in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7770-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="c7770-123">Prerequisites</span></span>
* <span data-ttu-id="c7770-124">內部部署 Active Directory 和 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7770-124">An on-premises deployment of Active Directory and DNS server.</span></span>
* <span data-ttu-id="c7770-125">在 Microsoft Azure 訂用帳戶中有 Azure Site Recovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="c7770-125">An Azure Site Recovery Services vault in a Microsoft Azure subscription.</span></span>
* <span data-ttu-id="c7770-126">如果您要複寫 tooAzure，Vm tooensure 上執行 hello Azure 虛擬機器整備評估工具，變更就 Azure Vm 與 Azure Site Recovery Services 相容。</span><span class="sxs-lookup"><span data-stu-id="c7770-126">If you're replicating tooAzure, run hello Azure Virtual Machine Readiness Assessment tool on VMs tooensure they're compatible with Azure VMs and Azure Site Recovery Services.</span></span>

## <a name="enable-protection-using-site-recovery"></a><span data-ttu-id="c7770-127">使用 Site Recovery 啟用保護</span><span class="sxs-lookup"><span data-stu-id="c7770-127">Enable protection using Site Recovery</span></span>
### <a name="protect-hello-virtual-machine"></a><span data-ttu-id="c7770-128">保護 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c7770-128">Protect hello virtual machine</span></span>
<span data-ttu-id="c7770-129">啟用 hello 網域控制站 /DNS Site Recovery 中的虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="c7770-129">Enable protection of hello domain controller/DNS virtual machine in Site Recovery.</span></span> <span data-ttu-id="c7770-130">設定 hello 虛擬機器類型 （HYPER-V 或 VMware） 為基礎的站台復原設定。</span><span class="sxs-lookup"><span data-stu-id="c7770-130">Configure Site Recovery settings based on hello virtual machine type (Hyper-V or VMware).</span></span> <span data-ttu-id="c7770-131">複寫使用站台復原的 hello 網域控制站用於[測試容錯移轉](#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="c7770-131">hello domain controller replicated using Site Recovery is used for [test failover](#test-failover-considerations).</span></span> <span data-ttu-id="c7770-132">請確定它符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7770-132">Make sure it meets hello following requirements:</span></span>

1. <span data-ttu-id="c7770-133">hello 網域控制站是通用類別目錄伺服器</span><span class="sxs-lookup"><span data-stu-id="c7770-133">hello domain controller is a global catalog server</span></span>
2. <span data-ttu-id="c7770-134">hello 網域控制站應該 hello FSMO 角色的擁有者將需要在測試容錯移轉期間的角色 (這些角色還需要 toobe[抓住](http://aka.ms/ad_seize_fsmo)hello 容錯移轉之後)</span><span class="sxs-lookup"><span data-stu-id="c7770-134">hello domain controller should be hello FSMO role owner for roles that will be needed during a test failover (else these roles will need toobe [seized](http://aka.ms/ad_seize_fsmo) after hello failover)</span></span>

### <a name="configure-virtual-machine-network-settings"></a><span data-ttu-id="c7770-135">設定虛擬機器的網路設定</span><span class="sxs-lookup"><span data-stu-id="c7770-135">Configure virtual machine network settings</span></span>
<span data-ttu-id="c7770-136">Hello 網域控制站/DNS 虛擬機器，如此 hello 虛擬機器將附加的 toohello 正確網路容錯移轉之後，在站台復原中設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="c7770-136">For hello domain controller/DNS virtual machine, configure network settings in Site Recovery so that hello virtual machine will be attached toohello right network after failover.</span></span> 

![VM 網路設定](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a><span data-ttu-id="c7770-138">以 Active Directory 複寫保護 Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7770-138">Protect Active Directory with Active Directory replication</span></span>
### <a name="site-to-site-protection"></a><span data-ttu-id="c7770-139">站對站保護</span><span class="sxs-lookup"><span data-stu-id="c7770-139">Site-to-site protection</span></span>
<span data-ttu-id="c7770-140">Hello 次要站台上建立網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c7770-140">Create a domain controller on hello secondary site.</span></span> <span data-ttu-id="c7770-141">當您升級 hello 伺服器 tooa 網域控制站角色時，指定 hello hello 名稱正在使用 hello 主要站台的相同網域。</span><span class="sxs-lookup"><span data-stu-id="c7770-141">When you promote hello server tooa domain controller role, specify hello name of hello same domain that is being used on hello primary site.</span></span> <span data-ttu-id="c7770-142">您可以使用 hello **Active Directory 站台及服務**嵌入式管理單元 tooconfigure hello 站台連結上的設定物件會加入 toowhich hello 站台。</span><span class="sxs-lookup"><span data-stu-id="c7770-142">You can use hello **Active Directory Sites and Services** snap-in tooconfigure settings on hello site link object toowhich hello sites are added.</span></span> <span data-ttu-id="c7770-143">藉由設定網站連結，您可以控制兩個以上的網站之間的複寫發生的時間和頻率。</span><span class="sxs-lookup"><span data-stu-id="c7770-143">By configuring settings on a site link, you can control when replication occurs between two or more sites, and how often.</span></span> <span data-ttu-id="c7770-144">如需詳細資訊，請參閱[排程網站之間的複寫](https://technet.microsoft.com/library/cc731862.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c7770-144">For more information, see [Scheduling Replication Between Sites](https://technet.microsoft.com/library/cc731862.aspx).</span></span>

### <a name="site-to-azure-protection"></a><span data-ttu-id="c7770-145">站對 Azure 保護</span><span class="sxs-lookup"><span data-stu-id="c7770-145">Site-to-Azure protection</span></span>
<span data-ttu-id="c7770-146">請依照下列指示 hello 太[在 Azure 虛擬網路中建立的網域控制站](../active-directory/active-directory-install-replica-active-directory-domain-controller.md)。</span><span class="sxs-lookup"><span data-stu-id="c7770-146">Follow hello instructions too[create a domain controller in an Azure virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md).</span></span> <span data-ttu-id="c7770-147">當您升級 hello 伺服器 tooa 網域控制站角色時，指定 hello hello 主要站台上使用相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="c7770-147">When you promote hello server tooa domain controller role, specify hello same domain name that's used on hello primary site.</span></span>

<span data-ttu-id="c7770-148">然後[hello hello 虛擬網路的 DNS 伺服器重新設定](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network)，在 Azure 中的 toouse hello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7770-148">Then [reconfigure hello DNS server for hello virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), toouse hello DNS server in Azure.</span></span>

![Azure 網路](./media/site-recovery-active-directory/azure-network.png)

<span data-ttu-id="c7770-150">**Azure 實際執行網路中的 DNS**</span><span class="sxs-lookup"><span data-stu-id="c7770-150">**DNS in Azure Production Network**</span></span>

## <a name="test-failover-considerations"></a><span data-ttu-id="c7770-151">測試容錯移轉考量</span><span class="sxs-lookup"><span data-stu-id="c7770-151">Test failover considerations</span></span>
<span data-ttu-id="c7770-152">測試容錯移轉是在與生產網路隔離的網路中發生，因此不會影響生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="c7770-152">Test failover occurs in a network that's isolated from production network so that there's no impact on production workloads.</span></span>

<span data-ttu-id="c7770-153">大部分的應用程式也需要網域控制站和 DNS 伺服器 toofunction hello 存在。</span><span class="sxs-lookup"><span data-stu-id="c7770-153">Most applications also require hello presence of a domain controller and a DNS server toofunction.</span></span> <span data-ttu-id="c7770-154">因此，hello 應用程式容錯移轉之前，網域控制站需要 toobe hello 隔離網路 toobe 用於測試容錯移轉中建立。</span><span class="sxs-lookup"><span data-stu-id="c7770-154">Therefore, before hello application is failed over, a domain controller needs toobe created in hello isolated network toobe used for test failover.</span></span> <span data-ttu-id="c7770-155">hello 最簡單的方式 toodo 這是 tooreplicate 與 Site Recovery 的網域控制站/DNS 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7770-155">hello easiest way toodo this is tooreplicate a domain controller/DNS virtual machine with Site Recovery.</span></span> <span data-ttu-id="c7770-156">然後執行測試容錯移轉的 hello 網域控制站虛擬機器，才能執行 hello hello 應用程式的復原計劃的測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c7770-156">Then run a test failover of hello domain controller virtual machine before running a test failover of hello recovery plan for hello application.</span></span> <span data-ttu-id="c7770-157">以下是做法：</span><span class="sxs-lookup"><span data-stu-id="c7770-157">Here's how you do that:</span></span>

1. <span data-ttu-id="c7770-158">[複寫](site-recovery-replicate-vmware-to-azure.md)hello 網域控制站/DNS 虛擬機器使用站台復原。</span><span class="sxs-lookup"><span data-stu-id="c7770-158">[Replicate](site-recovery-replicate-vmware-to-azure.md) hello domain controller/DNS virtual machine using Site Recovery.</span></span>
1. <span data-ttu-id="c7770-159">建立隔離的網路。</span><span class="sxs-lookup"><span data-stu-id="c7770-159">Create an isolated network.</span></span> <span data-ttu-id="c7770-160">在 Azure 中建立的任何虛擬網路預設是與其他網路隔離。</span><span class="sxs-lookup"><span data-stu-id="c7770-160">Any virtual network created in Azure by default is isolated from other networks.</span></span> <span data-ttu-id="c7770-161">我們建議 hello 這個網路的 IP 位址範圍與您的生產網路相同。</span><span class="sxs-lookup"><span data-stu-id="c7770-161">We recommend that hello IP address range for this network is same as that of your production network.</span></span> <span data-ttu-id="c7770-162">請勿在此網路上啟用網站對網站連線能力。</span><span class="sxs-lookup"><span data-stu-id="c7770-162">Don't enable site-to-site connectivity on this network.</span></span>
1. <span data-ttu-id="c7770-163">提供建立，做為您預期 hello DNS 虛擬機器 tooget hello IP 位址的 hello 網路中的 DNS IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c7770-163">Provide a DNS IP address in hello network created, as hello IP address that you expect hello DNS virtual machine tooget.</span></span> <span data-ttu-id="c7770-164">如果您要複寫 tooAzure，然後提供 hello IP 位址使用中的容錯移轉的 VM hello**目標 IP**中設定**計算與網路**設定。</span><span class="sxs-lookup"><span data-stu-id="c7770-164">If you're replicating tooAzure, then provide hello IP address for hello VM that is used on failover in **Target IP** setting in **Compute and Network** settings.</span></span> 

    <span data-ttu-id="c7770-165">![目標 IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **目標 IP**</span><span class="sxs-lookup"><span data-stu-id="c7770-165">![Target IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **Target IP**</span></span>

    ![Azure 測試網路](./media/site-recovery-active-directory/azure-test-network.png)

    <span data-ttu-id="c7770-167">**Azure 測試網路中的 DNS**</span><span class="sxs-lookup"><span data-stu-id="c7770-167">**DNS in Azure Test Network**</span></span>

> [!TIP]
> <span data-ttu-id="c7770-168">站台復原嘗試 toocreate 測試虛擬機器中相同名稱的子網路，以及使用 hello 與中提供的相同 IP**計算與網路**hello 虛擬機器的設定。</span><span class="sxs-lookup"><span data-stu-id="c7770-168">Site Recovery attempts toocreate test virtual machines in a subnet of same name and using hello same IP as that provided in **Compute and Network** settings of hello virtual machine.</span></span> <span data-ttu-id="c7770-169">如果相同名稱的子網路不是 hello 為測試容錯移轉時，所提供的 Azure 虛擬網路中可用的則依字母順序建立 hello 第一個子網路中測試虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7770-169">If subnet of same name is not available in hello Azure virtual network provided for test failover, then test virtual machine is created in hello first subnet alphabetically.</span></span> <span data-ttu-id="c7770-170">Hello 目標 IP 是 hello 選擇子網路的一部分，如果站台復原會嘗試 toocreate hello 測試容錯移轉虛擬機器使用 hello 目標 IP。</span><span class="sxs-lookup"><span data-stu-id="c7770-170">If hello target IP is part of hello chosen subnet, then Site Recovery tries toocreate hello test failover virtual machine using hello target IP.</span></span> <span data-ttu-id="c7770-171">如果 hello 目標 IP 不屬於 hello 選擇子網路，然後取得建立測試容錯移轉虛擬機器，在 hello 選擇子網路中使用任何可用的 IP。</span><span class="sxs-lookup"><span data-stu-id="c7770-171">If hello target IP is not part of hello chosen subnet, then test failover virtual machine gets created using any available IP in hello chosen subnet.</span></span> 
>
>


1. <span data-ttu-id="c7770-172">如果您要複寫 tooanother 在內部部署站台，而且您使用 DHCP，請依照下列指示 hello 太[針對測試容錯移轉設定 DNS 和 DHCP](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)</span><span class="sxs-lookup"><span data-stu-id="c7770-172">If you're replicating tooanother on-premises site and you're using DHCP, follow hello instructions too[setup DNS and DHCP for test failover](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)</span></span>
1. <span data-ttu-id="c7770-173">執行 hello 網域控制站虛擬機器在 hello 隔離網路中執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c7770-173">Do a test failover of hello domain controller virtual machine run in hello isolated network.</span></span> <span data-ttu-id="c7770-174">使用的最新可用的**應用程式一致**hello 網域控制站虛擬機器 toodo hello 測試容錯移轉的復原點。</span><span class="sxs-lookup"><span data-stu-id="c7770-174">Use latest available **application consistent** recovery point of hello domain controller virtual machine toodo hello test failover.</span></span> 
1. <span data-ttu-id="c7770-175">執行包含 hello 應用程式的虛擬機器的 hello 復原計劃的測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c7770-175">Run a test failover for hello recovery plan that contains virtual machines of hello application.</span></span> 
1. <span data-ttu-id="c7770-176">測試完成之後，**清除測試容錯移轉**hello 網域控制站虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="c7770-176">After testing is complete, **Cleanup test failover** on hello domain controller virtual machine.</span></span> <span data-ttu-id="c7770-177">此步驟會刪除針對測試容錯移轉建立 hello 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c7770-177">This step deletes hello domain controller that was created for test failover.</span></span>


### <a name="removing-reference-tooother-domain-controllers"></a><span data-ttu-id="c7770-178">移除參考 tooother 網域控制站</span><span class="sxs-lookup"><span data-stu-id="c7770-178">Removing reference tooother domain controllers</span></span>
<span data-ttu-id="c7770-179">當您在進行測試容錯移轉時，您不將所有 hello 網域控制站在 hello 測試網路。</span><span class="sxs-lookup"><span data-stu-id="c7770-179">When you are doing a test failover, you don't bring all hello domain controllers in hello test network.</span></span> <span data-ttu-id="c7770-180">tooremove hello 參考存在於實際執行環境中其他網域控制站，您可能需要過[拿取 FSMO Active Directory 角色](http://aka.ms/ad_seize_fsmo)執行[中繼資料清除](https://technet.microsoft.com/library/cc816907.aspx)遺漏網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c7770-180">tooremove hello reference of other domain controllers that exist in your production environment, you might need too[seize FSMO Active Directory roles](http://aka.ms/ad_seize_fsmo) and do [metadata cleanup](https://technet.microsoft.com/library/cc816907.aspx) for missing domain controllers.</span></span> 



> [!IMPORTANT]
> <span data-ttu-id="c7770-181">某些 hello 之後 > 一節中所述的 hello 組態不 hello 標準/預設網域控制站組態。</span><span class="sxs-lookup"><span data-stu-id="c7770-181">Some of hello configurations described in hello following section are not hello standard/default domain controller configurations.</span></span> <span data-ttu-id="c7770-182">如果您不想 toomake 這些變更 tooa 實際執行網域控制站，則您可以建立用於 Site Recovery 測試容錯移轉網域控制站專用 toobe 及進行這些變更 toothat。</span><span class="sxs-lookup"><span data-stu-id="c7770-182">If you don't want toomake these changes tooa production domain controller, then you can create a domain controller dedicated toobe used for Site Recovery test failover and make these changes toothat.</span></span>  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a><span data-ttu-id="c7770-183">由於虛擬化保護措施所產生的問題</span><span class="sxs-lookup"><span data-stu-id="c7770-183">Issues because of virtualization safeguards</span></span> 

<span data-ttu-id="c7770-184">從 Windows Server 2012 開始，[Active Directory Domain Services 已內建額外保護措施](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100)。</span><span class="sxs-lookup"><span data-stu-id="c7770-184">Beginning with Windows Server 2012, [additional safeguards have been built into Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).</span></span> <span data-ttu-id="c7770-185">這些保護，可協助保護對 USN 回復的虛擬的網域控制站，只要基礎 hypervisor 平台 hello 支援-VM 世代識別碼。</span><span class="sxs-lookup"><span data-stu-id="c7770-185">These safeguards help protect virtualized domain controllers against USN Rollbacks, as long as hello underlying hypervisor platform supports VM-GenerationID.</span></span> <span data-ttu-id="c7770-186">Azure 支援 Vm-generationid，這表示執行 Windows Server 2012 或更新版本的 Azure 虛擬機器的網域控制站具有 hello 額外的保護措施。</span><span class="sxs-lookup"><span data-stu-id="c7770-186">Azure supports VM-GenerationID, which means that domain controllers that run Windows Server 2012 or later on Azure virtual machines have hello additional safeguards.</span></span> 


<span data-ttu-id="c7770-187">重設 hello-VM 世代識別碼，則當 hello hello AD DS 資料庫的 invocationID 也會重設、，捨棄 RID 集區 hello 和 SYSVOL 會標示為非系統授權。</span><span class="sxs-lookup"><span data-stu-id="c7770-187">When hello VM-GenerationID is reset, hello invocationID of hello AD DS database is also reset, hello RID pool is discarded, and SYSVOL is marked as non-authoritative.</span></span> <span data-ttu-id="c7770-188">如需詳細資訊，請參閱[簡介 tooActive Directory 網域服務虛擬化](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100)和[安全地虛擬化 DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)</span><span class="sxs-lookup"><span data-stu-id="c7770-188">For more information, see [Introduction tooActive Directory Domain Services Virtualization](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) and [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)</span></span>

<span data-ttu-id="c7770-189">容錯移轉 tooAzure 可能會導致重設 Vm-generationid 的介入 hello 額外的保護措施在 Azure 中的 hello 網域控制站虛擬機器啟動時。</span><span class="sxs-lookup"><span data-stu-id="c7770-189">Failing over tooAzure may cause resetting of VM-GenerationID and that kicks in hello additional safeguards when hello domain controller virtual machine starts in Azure.</span></span> <span data-ttu-id="c7770-190">這可能會導致**明顯的延遲**使用者不能 toologin toohello 網域控制站虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="c7770-190">This may result in a **significant delay** in user being able toologin toohello domain controller virtual machine.</span></span> <span data-ttu-id="c7770-191">此網域控制站只會用於測試容錯移轉，因此不需要虛擬化保護措施。</span><span class="sxs-lookup"><span data-stu-id="c7770-191">Since this domain controller would be used only in a test failover, virtualization safeguards are not necessary.</span></span> <span data-ttu-id="c7770-192">-VM 世代識別碼 hello 網域控制站虛擬機器不會變更，則您可以變更下列 DWORD too4 hello 在內部部署網域控制站中的 hello 值的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="c7770-192">tooensure that VM-GenerationID for hello domain controller virtual machine doesn't change, then you can change hello value of following DWORD too4 in hello on-premises domain controller.</span></span>

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a><span data-ttu-id="c7770-193">虛擬化保護措施的徵兆</span><span class="sxs-lookup"><span data-stu-id="c7770-193">Symptoms of virtualization safeguards</span></span>
 
<span data-ttu-id="c7770-194">如果在測試容錯移轉之後執行了虛擬化保護措施，您可能會看到下列一或多個徵兆︰</span><span class="sxs-lookup"><span data-stu-id="c7770-194">If virtualization safeguards have kicked in after a test failover, you may see one or more of following symptoms:</span></span>  

<span data-ttu-id="c7770-195">世代識別碼變更</span><span class="sxs-lookup"><span data-stu-id="c7770-195">Generation ID change</span></span>

![世代識別碼變更](./media/site-recovery-active-directory/Event2170.png)

<span data-ttu-id="c7770-197">叫用識別碼變更</span><span class="sxs-lookup"><span data-stu-id="c7770-197">Invocation ID change</span></span>

![叫用識別碼變更](./media/site-recovery-active-directory/Event1109.png)

<span data-ttu-id="c7770-199">無法使用 Sysvol 與 Netlogon 共用</span><span class="sxs-lookup"><span data-stu-id="c7770-199">Sysvol and Netlogon shares are not available</span></span>

![Sysvol 共用](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

<span data-ttu-id="c7770-202">任何 DFSR 資料庫都會遭到刪除</span><span class="sxs-lookup"><span data-stu-id="c7770-202">Any DFSR databases are deleted</span></span>

![DFSR DB 刪除](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> <span data-ttu-id="c7770-204">某些 hello 之後 > 一節中所述的 hello 組態不 hello 標準/預設網域控制站組態。</span><span class="sxs-lookup"><span data-stu-id="c7770-204">Some of hello configurations described in hello following section are not hello standard/default domain controller configurations.</span></span> <span data-ttu-id="c7770-205">如果您不想 toomake 這些變更 tooa 實際執行網域控制站，則您可以建立用於 Site Recovery 測試容錯移轉網域控制站專用 toobe 及進行這些變更 toothat。</span><span class="sxs-lookup"><span data-stu-id="c7770-205">If you don't want toomake these changes tooa production domain controller, then you can create a domain controller dedicated toobe used for Site Recovery test failover and make these changes toothat.</span></span>  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a><span data-ttu-id="c7770-206">在測試容錯移轉期間，對網域控制站問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c7770-206">Troubleshooting domain controller issues during test failover</span></span>


<span data-ttu-id="c7770-207">在命令提示字元中，執行下列命令 toocheck 是否共用 SYSVOL 與 NETLOGON 資料夾的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7770-207">On a command prompt, run hello following command toocheck whether SYSVOL and NETLOGON folders are shared:</span></span>

    NET SHARE

<span data-ttu-id="c7770-208">Hello 命令提示字元處執行下列命令 hello 網域控制站的 tooensure 運作正常的 hello。</span><span class="sxs-lookup"><span data-stu-id="c7770-208">On hello command prompt, run hello following command tooensure that hello domain controller is functioning properly.</span></span>

    dcdiag /v > dcdiag.txt

<span data-ttu-id="c7770-209">Hello 輸出記錄檔中尋找 hello 網域控制站的下列文字 tooconfirm 正常運作。</span><span class="sxs-lookup"><span data-stu-id="c7770-209">In hello output log, look for following text tooconfirm that hello domain controller is functioning well.</span></span> 

* <span data-ttu-id="c7770-210">"passed test Connectivity"</span><span class="sxs-lookup"><span data-stu-id="c7770-210">"passed test Connectivity"</span></span>
* <span data-ttu-id="c7770-211">"passed test Advertising"</span><span class="sxs-lookup"><span data-stu-id="c7770-211">"passed test Advertising"</span></span>
* <span data-ttu-id="c7770-212">"passed test MachineAccount"</span><span class="sxs-lookup"><span data-stu-id="c7770-212">"passed test MachineAccount"</span></span>

<span data-ttu-id="c7770-213">如果 hello 上述條件符合，它可能是該 hello 網域控制站正常運作。</span><span class="sxs-lookup"><span data-stu-id="c7770-213">If hello preceding conditions are satisfied, it is likely that hello domain controller is functioning well.</span></span> <span data-ttu-id="c7770-214">如果沒有，請嘗試下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c7770-214">If not, try following steps.</span></span>


* <span data-ttu-id="c7770-215">請勿 hello 網域控制站的系統授權還原。</span><span class="sxs-lookup"><span data-stu-id="c7770-215">Do an authoritative restore of hello domain controller.</span></span>
    * <span data-ttu-id="c7770-216">雖然[不建議使用 toouse FRS 複寫](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/)，但是，如果您仍在使用它，然後遵循所提供的 hello 步驟[這裡](https://support.microsoft.com/kb/290762)toodo 系統授權還原。</span><span class="sxs-lookup"><span data-stu-id="c7770-216">Although it is [not recommended toouse FRS replication](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), but if you are still using it then follow hello steps provided [here](https://support.microsoft.com/kb/290762) toodo an authoritative restore.</span></span> <span data-ttu-id="c7770-217">您可以閱讀更多有關 Burflags hello 先前連結中討論[這裡](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/)。</span><span class="sxs-lookup"><span data-stu-id="c7770-217">You can read more about Burflags talked about in hello previous link [here](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).</span></span>
    * <span data-ttu-id="c7770-218">如果您使用 DFSR 複寫，請依照 hello 步驟可用[這裡](https://support.microsoft.com/kb/2218556)toodo 系統授權還原。</span><span class="sxs-lookup"><span data-stu-id="c7770-218">If you are using DFSR replication, then follow hello steps available [here](https://support.microsoft.com/kb/2218556) toodo an authoritative restore.</span></span> <span data-ttu-id="c7770-219">您也可以使用這個[連結](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/)中的 Powershell 函式執行權威復原。</span><span class="sxs-lookup"><span data-stu-id="c7770-219">You can also use Powershell functions available on this [link](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) for this purpose.</span></span> 
    
* <span data-ttu-id="c7770-220">藉由設定下列登錄金鑰 too0 hello 在內部部署網域控制站中的，略過初始同步處理需求。</span><span class="sxs-lookup"><span data-stu-id="c7770-220">Bypass initial synchronization requirement by setting following registry key too0 in hello on-premises domain controller.</span></span> <span data-ttu-id="c7770-221">如果此 DWORD 不存在，您可以在節點 'Parameters' 下建立。</span><span class="sxs-lookup"><span data-stu-id="c7770-221">If this DWORD doesn't exist, then you can create it under node 'Parameters'.</span></span> <span data-ttu-id="c7770-222">您可以在[此處](https://support.microsoft.com/kb/2001093)閱讀相關資訊</span><span class="sxs-lookup"><span data-stu-id="c7770-222">You can read more about it [here](https://support.microsoft.com/kb/2001093)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* <span data-ttu-id="c7770-223">停用的通用類別目錄伺服器是可用 toovalidate 使用者登入，藉由設定下列登錄金鑰 too1 hello 在內部部署網域控制站中的 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="c7770-223">Disable hello requirement that a global catalog server is available toovalidate user logon by setting following registry key too1 in hello on-premises domain controller.</span></span> <span data-ttu-id="c7770-224">如果此 DWORD 不存在，您可以在節點 'Lsa' 下建立。</span><span class="sxs-lookup"><span data-stu-id="c7770-224">If this DWORD doesn't exist, then you can create it under node 'Lsa'.</span></span> <span data-ttu-id="c7770-225">您可以在[此處](http://support.microsoft.com/kb/241789)閱讀相關資訊</span><span class="sxs-lookup"><span data-stu-id="c7770-225">You can read more about it [here](http://support.microsoft.com/kb/241789)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a><span data-ttu-id="c7770-226">不同電腦上的 DNS 和網域控制站</span><span class="sxs-lookup"><span data-stu-id="c7770-226">DNS and domain controller on different machines</span></span>
<span data-ttu-id="c7770-227">如果在 hello 的 DNS 不相同的虛擬機器為 hello 網域控制站，您需要 toocreate DNS VM hello 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c7770-227">If DNS isn't on hello same virtual machine as hello domain controller, you need toocreate a DNS VM for hello test failover.</span></span> <span data-ttu-id="c7770-228">如果它們位於 hello 相同的 VM，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="c7770-228">If they're on hello same VM, you can skip this section.</span></span>

<span data-ttu-id="c7770-229">您可以使用全新的 DNS 伺服器，並建立 hello 所需的所有區域。</span><span class="sxs-lookup"><span data-stu-id="c7770-229">You can use a fresh DNS server and create all hello required zones.</span></span> <span data-ttu-id="c7770-230">例如，如果您的 Active Directory 網域為 contoso.com，您可以建立 DNS 區域與 hello 名稱 contoso.com。hello 項目對應 tooActive 目錄必須更新在 DNS 中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7770-230">For example, if your Active Directory domain is contoso.com, you can create a DNS zone with hello name contoso.com. hello entries corresponding tooActive Directory must be updated in DNS, as follows:</span></span>

1. <span data-ttu-id="c7770-231">請確定這些設定已就緒 hello 復原計劃中的任何其他虛擬機器出現之前：</span><span class="sxs-lookup"><span data-stu-id="c7770-231">Ensure these settings are in place before any other virtual machine in hello recovery plan comes up:</span></span>
   
   * <span data-ttu-id="c7770-232">hello 區域必須為名 hello 樹系根名稱。</span><span class="sxs-lookup"><span data-stu-id="c7770-232">hello zone must be named after hello forest root name.</span></span>
   * <span data-ttu-id="c7770-233">hello 區域必須是檔案備份。</span><span class="sxs-lookup"><span data-stu-id="c7770-233">hello zone must be file-backed.</span></span>
   * <span data-ttu-id="c7770-234">hello 區域必須啟用安全和非安全更新。</span><span class="sxs-lookup"><span data-stu-id="c7770-234">hello zone must be enabled for secure and non-secure updates.</span></span>
   * <span data-ttu-id="c7770-235">hello 的 hello 網域控制站虛擬機器的解析程式應該指向 toohello hello DNS 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c7770-235">hello resolver of hello domain controller virtual machine should point toohello IP address of hello DNS virtual machine.</span></span>
2. <span data-ttu-id="c7770-236">執行下列命令，在網域控制站虛擬機器上的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7770-236">Run hello following command on domain controller virtual machine:</span></span>
   
    `nltest /dsregdns`
3. <span data-ttu-id="c7770-237">Hello DNS 伺服器上加入區域、 允許不安全的更新，並加入項目，tooDNS:</span><span class="sxs-lookup"><span data-stu-id="c7770-237">Add a zone on hello DNS server, allow non-secure updates, and add an entry for it tooDNS:</span></span>
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a><span data-ttu-id="c7770-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7770-238">Next steps</span></span>
<span data-ttu-id="c7770-239">讀取[可以保護哪些工作負載？](site-recovery-workload.md) toolearn 深入了解保護與 Azure Site Recovery 的企業工作負載。</span><span class="sxs-lookup"><span data-stu-id="c7770-239">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>

