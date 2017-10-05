---
title: "使用 PowerShell (Azure Resource Manager) 將 VMM 中的 Hyper-V VM 複寫到次要站台 | Microsoft Docs"
description: "描述如何使用 PowerShell (Resource Manager) 部署 Azure Site Recovery，以協調將 VMM 雲端中的 Hyper-V VM 複寫、容錯移轉和復原至次要 VMM 站台"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="675bb-103">使用 PowerShell 將位於 VMM 雲端中的 Hyper-V 虛擬機器複寫至次要 VMM 站台 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="675bb-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="675bb-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="675bb-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="675bb-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="675bb-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="675bb-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="675bb-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="675bb-107">歡迎使用 Azure Site Recovery！</span><span class="sxs-lookup"><span data-stu-id="675bb-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="675bb-108">如果您想要將 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V 虛擬機器複寫至次要站台，請使用本文。</span><span class="sxs-lookup"><span data-stu-id="675bb-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="675bb-109">本文說明如何使用 PowerShell 自動化您在設定 Azure Site Recovery 將 System Center VMM 雲端中的 Hyper-V 虛擬機器，複寫到次要站台中的 System Center VMM 時常需要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="675bb-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="675bb-110">本文包含案例的必要條件，並對您示範</span><span class="sxs-lookup"><span data-stu-id="675bb-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="675bb-111">如何設定復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="675bb-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="675bb-112">在來源 VMM 伺服器與目標 VMM 伺服器上安裝 Azure Site Recovery 提供者</span><span class="sxs-lookup"><span data-stu-id="675bb-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="675bb-113">在保存庫中註冊 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="675bb-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="675bb-114">設定 VMM 雲端的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="675bb-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="675bb-115">原則中的複寫設定將套用到所有受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="675bb-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="675bb-116">為虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="675bb-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="675bb-117">個別或在復原計劃中測試 VM 的容錯移轉，確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="675bb-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="675bb-118">個別或在復原計劃中執行 VM 計劃性或非計劃性的容錯移轉，確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="675bb-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="675bb-119">您在設定此案例如有任何問題，可將問題張貼到 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="675bb-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="675bb-120">Azure 建立和處理資源的 [部署模型](../azure-resource-manager/resource-manager-deployment-model.md) 有二種：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="675bb-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="675bb-121">Azure 也有兩個入口網站 – 支援傳統部署模型的 Azure 傳統入口網站，以及支援兩種部署模型的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="675bb-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="675bb-122">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="675bb-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="675bb-123">內部部署必要條件</span><span class="sxs-lookup"><span data-stu-id="675bb-123">On-premises prerequisites</span></span>
<span data-ttu-id="675bb-124">以下是您需要在主要和次要內部部署站台中部署此案例的情況：</span><span class="sxs-lookup"><span data-stu-id="675bb-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="675bb-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="675bb-125">**Prerequisites**</span></span> | <span data-ttu-id="675bb-126">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="675bb-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="675bb-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="675bb-127">**VMM**</span></span> |<span data-ttu-id="675bb-128">建議您在主要站台與次要站台各部署一部 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="675bb-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="675bb-129">您也可以[在單一 VMM 伺服器上的雲端之間進行複寫](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)。</span><span class="sxs-lookup"><span data-stu-id="675bb-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="675bb-130">若要這樣做，您至少需要在 VMM 伺服器上設定兩個雲端。</span><span class="sxs-lookup"><span data-stu-id="675bb-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="675bb-131">VMM 伺服器至少應執行含有最新更新的 System Center 2012 SP1。</span><span class="sxs-lookup"><span data-stu-id="675bb-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="675bb-132">每部 VMM 伺服器都必須設定一或多個雲端，而所有雲端都必須設定 Hyper-V 容量設定檔。</span><span class="sxs-lookup"><span data-stu-id="675bb-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="675bb-133">雲端必須包含一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="675bb-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="675bb-134">若要深入了解如何設定 VMM 雲端，請參閱[設定 VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)和[Walkthrough: Creating private clouds with System Center 2012 SP1 VMM (逐步解說：使用 System Center 2012 SP1 VMM 建立私人雲端)](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)。</span><span class="sxs-lookup"><span data-stu-id="675bb-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="675bb-135">VMM 伺服器必須能夠存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="675bb-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="675bb-136">**Hyper-V**</span></span> |<span data-ttu-id="675bb-137">Hyper-V 伺服器必須至少執行具備 Hyper-V 角色並已安裝最新更新的 Windows Server 2012。</span><span class="sxs-lookup"><span data-stu-id="675bb-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="675bb-138">Hyper-V 伺服器應該包含一或多部 VM。</span><span class="sxs-lookup"><span data-stu-id="675bb-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="675bb-139">Hyper-V 主機伺服器應該位於主要和次要 VMM 雲端的主機群組中。</span><span class="sxs-lookup"><span data-stu-id="675bb-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="675bb-140">如果您是在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，則應該安裝[更新 2961977](https://support.microsoft.com/kb/2961977)。</span><span class="sxs-lookup"><span data-stu-id="675bb-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="675bb-141">如果您是在 Windows Server 2012 上的叢集中執行 Hyper-V，請注意，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="675bb-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="675bb-142">您必須手動設定叢集代理。</span><span class="sxs-lookup"><span data-stu-id="675bb-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="675bb-143">[閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。</span><span class="sxs-lookup"><span data-stu-id="675bb-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="675bb-144">**提供者**</span><span class="sxs-lookup"><span data-stu-id="675bb-144">**Provider**</span></span> |<span data-ttu-id="675bb-145">在 Site Recovery 部署期間，您會在 VMM 伺服器上安裝 Azure Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="675bb-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="675bb-146">Provider 會透過 HTTPS 443 與 Site Recovery 通訊來協調複寫。</span><span class="sxs-lookup"><span data-stu-id="675bb-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="675bb-147">資料複寫是透過 LAN 或 VPN 連線在主要和次要 Hyper-V 伺服器之間進行。</span><span class="sxs-lookup"><span data-stu-id="675bb-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="675bb-148">在 VMM 伺服器上執行的提供者需要能夠存取下列 URL：*.hypervrecoverymanager.windowsazure.com、*.accesscontrol.windows.net、*.backup.windowsazure.com、*.blob.core.windows.net、*.store.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="675bb-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="675bb-149">此外，還要允許從 VMM 伺服器到 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)的防火牆通訊，並允許 HTTPS (443) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="675bb-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="675bb-150">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="675bb-150">Network mapping prerequisites</span></span>
<span data-ttu-id="675bb-151">網路對應會在主要和次要 VMM伺服器上的 VMM VM 網路之間進行對應：</span><span class="sxs-lookup"><span data-stu-id="675bb-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="675bb-152">容錯移轉之後，選擇性地在次要 Hyper-V 主機上放置複本 VM。</span><span class="sxs-lookup"><span data-stu-id="675bb-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="675bb-153">將複本 VM 連接到適當的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="675bb-154">如果您沒有設定網路對應，複本 VM 將不會在容錯移轉之後連接到任何網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="675bb-155">如果您想要在 Site Recovery 部署期間設定網路對應，就需要執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="675bb-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="675bb-156">確認來源 Hyper-V 主機伺服器上的 VM 已連接到 VMM VM 網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="675bb-157">該網路應該連結到與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="675bb-158">確認您將用於復原的次要雲端已設定相對應的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="675bb-159">該 VM 網路應該連結到與次要雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="675bb-160">從以下文章深入了解設定 VMM 網路</span><span class="sxs-lookup"><span data-stu-id="675bb-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="675bb-161">如何在 VMM 中設定邏輯網路</span><span class="sxs-lookup"><span data-stu-id="675bb-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="675bb-162">如何在 VMM 中設定 VM 網路和閘道</span><span class="sxs-lookup"><span data-stu-id="675bb-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="675bb-163">[深入了解](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) 網路對應的運作方式。</span><span class="sxs-lookup"><span data-stu-id="675bb-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="675bb-164">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="675bb-164">PowerShell prerequisites</span></span>
<span data-ttu-id="675bb-165">確定 Azure PowerShell 已經準備就緒。</span><span class="sxs-lookup"><span data-stu-id="675bb-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="675bb-166">如果您已經使用 PowerShell，您必須升級至 0.8.10 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="675bb-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="675bb-167">如需設定 PowerShell 的資訊，請參閱 [安裝和設定 Azure PowerShell 指南](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="675bb-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="675bb-168">一旦已安裝並設定 PowerShell，您可以檢視 [這裡](/powershell/azure/overview)之服務的所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="675bb-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="675bb-169">如需了解可協助您使用這些 Cmdlet 的提示 (例如參數值、輸入及輸出在 Azure PowerShell 中的處理方式)，請參閱 [Azure Cmdlet 使用者入門](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="675bb-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="675bb-170">步驟 1：設定訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="675bb-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="675bb-171">從 Azure powershell，登入您的 Azure 帳戶︰使用下列 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="675bb-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="675bb-172">取得您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="675bb-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="675bb-173">這樣也會列出每個訂用帳戶的 subscriptionID。</span><span class="sxs-lookup"><span data-stu-id="675bb-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="675bb-174">記下您要建立復原服務保存庫之訂用帳戶的 subscriptionID</span><span class="sxs-lookup"><span data-stu-id="675bb-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="675bb-175">設定藉由提及訂用帳戶識別碼在其中建立復原服務保存庫的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="675bb-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="675bb-176">步驟 2：建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="675bb-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="675bb-177">如果您還沒有 Azure Resource Manager 資源群組，請建立一個</span><span class="sxs-lookup"><span data-stu-id="675bb-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="675bb-178">建立新的復原服務保存庫，並儲存在變數 (稍後使用) 中建立的 ASR 保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="675bb-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="675bb-179">您也可以使用 Get-AzureRMRecoveryServicesVault Cmdlet 擷取建立後的 ASR 保存庫物件：-</span><span class="sxs-lookup"><span data-stu-id="675bb-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="675bb-180">步驟 3：設定復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="675bb-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="675bb-181">如果您已建立保存庫，請執行下列命令來取得保存庫。</span><span class="sxs-lookup"><span data-stu-id="675bb-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="675bb-182">執行下面的命令來設定保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="675bb-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="675bb-183">步驟 4：安裝 Azure Site Recovery 提供者</span><span class="sxs-lookup"><span data-stu-id="675bb-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="675bb-184">在 VMM 機器上，執行下列命令來建立目錄：</span><span class="sxs-lookup"><span data-stu-id="675bb-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="675bb-185">執行下列命令，使用已下載的提供者將檔案解壓縮</span><span class="sxs-lookup"><span data-stu-id="675bb-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="675bb-186">使用下列命令安裝提供者：</span><span class="sxs-lookup"><span data-stu-id="675bb-186">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="675bb-187">等待安裝完成。</span><span class="sxs-lookup"><span data-stu-id="675bb-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="675bb-188">使用下列命令在保存庫中註冊伺服器：</span><span class="sxs-lookup"><span data-stu-id="675bb-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="675bb-189">步驟 5︰建立複寫原則並建立關聯</span><span class="sxs-lookup"><span data-stu-id="675bb-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="675bb-190">執行下列命令來建立 Hyper-V 2012 R2 複寫原則：</span><span class="sxs-lookup"><span data-stu-id="675bb-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="675bb-191">VMM 雲端可以包含執行不同 Windows Server 版本 (如 Hyper-V 先決條件所述) 的 Hyper-V 主機，但複寫原則會依據特定的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="675bb-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="675bb-192">如果您有執行不同作業系統版本的主機，則請針對每一種作業系統版本建立不同的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="675bb-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="675bb-193">例如︰如果您有五部主機在 Windows Server 2012 上執行，有三部在 Windows Server 2012 R2 上執行，則請建立兩個複寫原則 – 每一種作業系統版本使用一個。</span><span class="sxs-lookup"><span data-stu-id="675bb-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="675bb-194">執行下列命令，取得主要保護容器 (主要 VMM 雲端) 和復原保護容器 (復原 VMM 雲端)︰</span><span class="sxs-lookup"><span data-stu-id="675bb-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="675bb-195">擷取您在步驟 1 使用好記的原則名稱所建立的原則</span><span class="sxs-lookup"><span data-stu-id="675bb-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="675bb-196">開始建立保護容器 (VMM 雲端) 與複寫原則的關聯：</span><span class="sxs-lookup"><span data-stu-id="675bb-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="675bb-197">等候原則關聯工作完成。</span><span class="sxs-lookup"><span data-stu-id="675bb-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="675bb-198">您可以使用下列 PowerShell 程式碼片段檢查工作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="675bb-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="675bb-199">完成工作處理之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="675bb-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="675bb-200">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="675bb-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="675bb-201">步驟 6：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="675bb-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="675bb-202">第一個命令會取得目前的 Azure Site Recovery 保存庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="675bb-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="675bb-203">命令會將 Microsoft Azure Site Recovery 伺服器儲存在 $Servers 陣列變數。</span><span class="sxs-lookup"><span data-stu-id="675bb-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="675bb-204">下列命令取得來源 VMM 伺服器和目標 VMM 伺服器的站台復原網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="675bb-205">來源 VMM 伺服器在伺服器陣列中可以是第一部或第二部伺服器。</span><span class="sxs-lookup"><span data-stu-id="675bb-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="675bb-206">檢查 VMM 伺服器的名稱，並適當地取得網路</span><span class="sxs-lookup"><span data-stu-id="675bb-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="675bb-207">最終的 Cmdlet 會在主要網路與復原網路之間建立對應。</span><span class="sxs-lookup"><span data-stu-id="675bb-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="675bb-208">Cmdlet 將主要網路指定為 $PrimaryNetworks 的第一個元素，將復原網路指定為 $RecoveryNetworks 的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="675bb-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="675bb-209">步驟 7：設定儲存體對應</span><span class="sxs-lookup"><span data-stu-id="675bb-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="675bb-210">下列命令將能把儲存體分類清單置入 $storageclassifications 變數中。</span><span class="sxs-lookup"><span data-stu-id="675bb-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="675bb-211">下列命令將能把來源分類置入 $SourceClassificaion 變數中，並把目標分類置入 $TargetClassification 變數中。</span><span class="sxs-lookup"><span data-stu-id="675bb-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="675bb-212">來源和目標分類可以是陣列中的任何元素。</span><span class="sxs-lookup"><span data-stu-id="675bb-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="675bb-213">請參考下列命令的輸出，以了解 $storageclassifications 陣列中來源和目標分類的目錄。</span><span class="sxs-lookup"><span data-stu-id="675bb-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="675bb-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="675bb-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="675bb-215">下列 Cmdlet 能在來源分類和目標分類之間建立對應。</span><span class="sxs-lookup"><span data-stu-id="675bb-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="675bb-216">步驟 8：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="675bb-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="675bb-217">正確設定伺服器、雲端和網路後，您就可以對雲端中的虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="675bb-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="675bb-218">若要啟用保護，請執行下列命令以取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="675bb-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="675bb-219">執行下列命令以取得保護實體 (VM)：</span><span class="sxs-lookup"><span data-stu-id="675bb-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="675bb-220">執行下列命令以啟用 VM 的複寫：</span><span class="sxs-lookup"><span data-stu-id="675bb-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="675bb-221">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="675bb-221">Test your deployment</span></span>
<span data-ttu-id="675bb-222">若要測試部署，您可以對單一虛擬機器執行測試容錯移轉，或者建立包含多部虛擬機器的復原方案，再對這個方案執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="675bb-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="675bb-223">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="675bb-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="675bb-224">您可以在 Azure 入口網站中為應用程式建立復原方案。</span><span class="sxs-lookup"><span data-stu-id="675bb-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="675bb-225">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="675bb-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="675bb-226">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="675bb-226">Run a test failover</span></span>
1. <span data-ttu-id="675bb-227">執行下列 Cmdlet 以取得您要測試 VM 容錯移轉的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="675bb-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="675bb-228">執行下列內容執行 VM 的測試容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="675bb-229">執行下列內容執行復原方案的測試容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="675bb-230">執行計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="675bb-230">Run a planned failover</span></span>
1. <span data-ttu-id="675bb-231">執行下列內容執行 VM 的計劃性容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="675bb-232">執行下列內容執行復原方案的計劃性容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="675bb-233">執行非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="675bb-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="675bb-234">執行下列內容執行 VM 的非計劃性容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="675bb-235">2. 執行下列內容執行復原方案的非計劃性容錯移轉︰</span><span class="sxs-lookup"><span data-stu-id="675bb-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="675bb-236"><a name=monitor></a>監視活動</span><span class="sxs-lookup"><span data-stu-id="675bb-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="675bb-237">使用下列命令來監視活動。</span><span class="sxs-lookup"><span data-stu-id="675bb-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="675bb-238">請注意，您必須在工作之間等候處理程序完成。</span><span class="sxs-lookup"><span data-stu-id="675bb-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="675bb-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="675bb-239">Next steps</span></span>
<span data-ttu-id="675bb-240">[閱讀更多](/powershell/module/azurerm.recoveryservices.backup/#recovery) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="675bb-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
