---
title: "aaaReplicate VMM tooa 次要站台中的 HYPER-V Vm，使用 PowerShell (Azure Resource Manager) |Microsoft 文件"
description: "描述如何 toodeploy Azure Site Recovery tooorchestrate 複寫、 容錯移轉和復原 VMM 中的 HYPER-V Vm 的雲端 tooa 次要部署 VMM 站台使用 PowerShell （資源管理員）"
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
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="f7635-103">複寫 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台使用 PowerShell （資源管理員）</span><span class="sxs-lookup"><span data-stu-id="f7635-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7635-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f7635-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="f7635-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f7635-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="f7635-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="f7635-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="f7635-107">歡迎使用 tooAzure Site Recovery ！</span><span class="sxs-lookup"><span data-stu-id="f7635-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="f7635-108">如果您想 tooreplicate 內部管理 System Center Virtual Machine Manager (VMM) 雲端 tooa 次要站台中的 HYPER-V 虛擬機器，請使用這份文件。</span><span class="sxs-lookup"><span data-stu-id="f7635-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="f7635-109">本文章將示範如何 toouse PowerShell tooautomate 一般工作時，您需要 tooperform 您在 System Center VMM 雲端 tooSystem Center 次要站台中的 VMM 雲端中設定 Azure Site Recovery tooreplicate HYPER-V 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f7635-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="f7635-110">hello 發行項包含 hello 案例的先決條件，並示範您</span><span class="sxs-lookup"><span data-stu-id="f7635-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="f7635-111">如何復原服務保存庫註冊 tooset</span><span class="sxs-lookup"><span data-stu-id="f7635-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="f7635-112">Hello 來源 VMM 伺服器與 hello 目標 VMM 伺服器上安裝 Azure Site Recovery Provider hello</span><span class="sxs-lookup"><span data-stu-id="f7635-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="f7635-113">Hello 保存庫中註冊 hello VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="f7635-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="f7635-114">設定 hello VMM 雲端的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="f7635-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="f7635-115">會套用的 tooall 受保護的虛擬機器 hello hello 原則中的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="f7635-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="f7635-116">啟用 hello 虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="f7635-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="f7635-117">Hello 的測試容錯移轉 Vm 個別或做為復原計劃 toomake 確定一切如預期般運作的一部分。</span><span class="sxs-lookup"><span data-stu-id="f7635-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="f7635-118">執行的已規劃或未規劃的容錯移轉的 Vm，個別或做為復原計劃 toomake 確定一切如預期般運作的一部分。</span><span class="sxs-lookup"><span data-stu-id="f7635-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="f7635-119">如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="f7635-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="f7635-120">Azure 建立和處理資源的 [部署模型](../azure-resource-manager/resource-manager-deployment-model.md) 有二種：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="f7635-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f7635-121">Azure 也有兩個入口網站 – hello Azure 傳統入口網站支援 hello 傳統部署模型，與 hello Azure 入口網站支援這兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="f7635-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="f7635-122">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="f7635-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="f7635-123">內部部署必要條件</span><span class="sxs-lookup"><span data-stu-id="f7635-123">On-premises prerequisites</span></span>
<span data-ttu-id="f7635-124">以下是您將需要在 hello 主要和次要內部部署站台 toodeploy 此案例中：</span><span class="sxs-lookup"><span data-stu-id="f7635-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="f7635-125">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="f7635-125">**Prerequisites**</span></span> | <span data-ttu-id="f7635-126">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="f7635-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="f7635-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="f7635-127">**VMM**</span></span> |<span data-ttu-id="f7635-128">我們建議您部署中的 VMM 伺服器 hello 主要站台和 hello 次要站台之 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7635-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="f7635-129">您也可以[在單一 VMM 伺服器上的雲端之間進行複寫](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)。</span><span class="sxs-lookup"><span data-stu-id="f7635-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="f7635-130">toodo 這將需要至少兩個雲端 hello VMM 伺服器上設定。</span><span class="sxs-lookup"><span data-stu-id="f7635-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="f7635-131">VMM 伺服器應至少執行 System Center 2012 SP1 含 hello 最新的更新。</span><span class="sxs-lookup"><span data-stu-id="f7635-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="f7635-132">每個 VMM 伺服器必須能夠在其中一個或更多雲端設定，而且所有雲端必須有 hello HYPER-V 容量設定檔集合。</span><span class="sxs-lookup"><span data-stu-id="f7635-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="f7635-133">雲端必須包含一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="f7635-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="f7635-134">深入了解設定 VMM 雲端中[設定 hello VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)，和[逐步解說： 使用 System Center 2012 SP1 VMM 建立私人雲端](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7635-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="f7635-135">VMM 伺服器必須能夠存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="f7635-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="f7635-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="f7635-136">**Hyper-V**</span></span> |<span data-ttu-id="f7635-137">HYPER-V 的伺服器必須至少執行 Windows Server 2012 與 hello HYPER-V 角色和擁有 hello 安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="f7635-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="f7635-138">Hyper-V 伺服器應該包含一或多部 VM。</span><span class="sxs-lookup"><span data-stu-id="f7635-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="f7635-139">HYPER-V 主機伺服器應該位於 hello 主要和次要 VMM 雲端中的主機群組。</span><span class="sxs-lookup"><span data-stu-id="f7635-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="f7635-140">如果您是在 Windows Server 2012 R2 上的叢集中執行 Hyper-V，則應該安裝[更新 2961977](https://support.microsoft.com/kb/2961977)。</span><span class="sxs-lookup"><span data-stu-id="f7635-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="f7635-141">如果您是在 Windows Server 2012 上的叢集中執行 Hyper-V，請注意，當您的叢集是靜態 IP 位址型叢集時，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="f7635-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="f7635-142">您以手動方式將需要 tooconfigure hello 叢集代理人。</span><span class="sxs-lookup"><span data-stu-id="f7635-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="f7635-143">[閱讀更多資訊](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f7635-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="f7635-144">**提供者**</span><span class="sxs-lookup"><span data-stu-id="f7635-144">**Provider**</span></span> |<span data-ttu-id="f7635-145">Site Recovery 部署期間，請在 VMM 伺服器上安裝 hello Azure Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="f7635-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="f7635-146">透過 HTTPS 443 tooorchestrate 複寫，hello 提供者進行通訊與站台復原。</span><span class="sxs-lookup"><span data-stu-id="f7635-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="f7635-147">透過 hello LAN hello 主要和次要 HYPER-V 伺服器或 VPN 連線之間，進行資料複寫。</span><span class="sxs-lookup"><span data-stu-id="f7635-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="f7635-148">hello hello VMM 伺服器上執行的提供者需要存取 toothese Url: *。.hypervrecoverymanager.windowsazure.com;*。 accesscontrol.windows.net;*。 backup.windowsazure.com;*。 account>.blob.core.windows.net;*。 store.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="f7635-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="f7635-149">此外，則允許從 hello VMM 伺服器 toohello 防火牆通訊[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)並允許 hello HTTPS (443) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f7635-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="f7635-150">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="f7635-150">Network mapping prerequisites</span></span>
<span data-ttu-id="f7635-151">Hello 主要和次要 VMM 伺服器上的 VMM VM 網路之間的網路對應會：</span><span class="sxs-lookup"><span data-stu-id="f7635-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="f7635-152">容錯移轉之後，選擇性地在次要 Hyper-V 主機上放置複本 VM。</span><span class="sxs-lookup"><span data-stu-id="f7635-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="f7635-153">複本 Vm tooappropriate VM 網路連線。</span><span class="sxs-lookup"><span data-stu-id="f7635-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="f7635-154">如果您未設定網路對應複本 Vm 不是連接的 tooany 網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="f7635-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="f7635-155">如果您想 tooset 網路站台復原期間將對應部署以下是您將需要：</span><span class="sxs-lookup"><span data-stu-id="f7635-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="f7635-156">請確定 hello 來源 HYPER-V 主機伺服器上的 Vm 的連線的 tooa VMM VM 網路。</span><span class="sxs-lookup"><span data-stu-id="f7635-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="f7635-157">該網路應連結的 tooa hello 雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="f7635-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="f7635-158">請確認 hello 您將用於復原的次要雲端已設定的對應 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="f7635-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="f7635-159">該 VM 網路應連結的 tooa hello 次要雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="f7635-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="f7635-160">深入了解在 hello 以下文章中設定 VMM 網路</span><span class="sxs-lookup"><span data-stu-id="f7635-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="f7635-161">如何在 VMM 中的 tooconfigure 邏輯網路</span><span class="sxs-lookup"><span data-stu-id="f7635-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="f7635-162">如何 tooconfigure VM 網路和閘道在 VMM 中</span><span class="sxs-lookup"><span data-stu-id="f7635-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="f7635-163">[深入了解](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) 網路對應的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f7635-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="f7635-164">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="f7635-164">PowerShell prerequisites</span></span>
<span data-ttu-id="f7635-165">請確定您具有 Azure PowerShell 準備 toogo。</span><span class="sxs-lookup"><span data-stu-id="f7635-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="f7635-166">如果您已經使用 PowerShell，您將需要 tooupgrade tooversion 0.8.10 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f7635-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="f7635-167">PowerShell 設定的詳細資訊，請參閱 hello[引導 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="f7635-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f7635-168">一旦您已安裝並設定 PowerShell，您可以檢視所有 hello 可用的 hello 服務 cmdlet[這裡](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f7635-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="f7635-169">toolearn 的相關技巧，可協助您使用 hello cmdlet，例如如何參數值、 輸入和輸出通常處理 Azure PowerShell，請參閱 hello[引導 tooget 開始使用 Azure Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="f7635-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="f7635-170">步驟 1： 設定 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f7635-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="f7635-171">從 Azure powershell、 Azure 帳戶的登入 tooyour： 使用下列 cmdlet 的 hello</span><span class="sxs-lookup"><span data-stu-id="f7635-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="f7635-172">取得您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="f7635-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="f7635-173">這也會列出 hello 訂用帳戶每一個 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7635-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="f7635-174">記下您想在其中 toocreate hello 復原服務保存庫的 hello 訂用帳戶的 hello subscriptionID</span><span class="sxs-lookup"><span data-stu-id="f7635-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="f7635-175">設定中的 hello 復原服務保存庫是由一提 hello 訂用帳戶 ID 的 toobe hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f7635-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="f7635-176">步驟 2：建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="f7635-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="f7635-177">如果您還沒有 Azure Resource Manager 資源群組，請建立一個</span><span class="sxs-lookup"><span data-stu-id="f7635-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="f7635-178">建立新的復原服務保存庫並儲存在變數 （會使用更新版本） 中建立 ASR 保存庫物件的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7635-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="f7635-179">您也可以擷取 hello ASR 保存庫後建立物件使用 hello Get AzureRMRecoveryServicesVault 指令程式:-</span><span class="sxs-lookup"><span data-stu-id="f7635-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="f7635-180">步驟 3： 設定 hello 復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="f7635-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="f7635-181">如果您已經建立的保存庫，執行下列命令 tooget hello 保存庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7635-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="f7635-182">藉由執行下列命令 hello 設定 hello 保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="f7635-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="f7635-183">步驟 4： 安裝 hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="f7635-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="f7635-184">Hello VMM 在電腦上，執行下列命令的 hello 建立目錄：</span><span class="sxs-lookup"><span data-stu-id="f7635-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="f7635-185">擷取使用 hello 下載提供者藉由執行下列命令的 hello hello 檔案</span><span class="sxs-lookup"><span data-stu-id="f7635-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="f7635-186">安裝 hello 提供者使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f7635-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="f7635-187">等候 hello 安裝 toofinish。</span><span class="sxs-lookup"><span data-stu-id="f7635-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="f7635-188">使用下列命令的 hello hello 保存庫中註冊伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="f7635-189">步驟 5︰建立複寫原則並建立關聯</span><span class="sxs-lookup"><span data-stu-id="f7635-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="f7635-190">建立 HYPER-V 2012 R2 複寫原則，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="f7635-191">hello VMM 雲端中可包含 HYPER-V 主機執行不同版本的 Windows Server （如 hello HYPER-V 必要條件中所述），但 hello 複寫原則是特定的作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="f7635-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="f7635-192">如果您有執行不同作業系統版本的主機，則請針對每一種作業系統版本建立不同的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="f7635-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="f7635-193">例如︰如果您有五部主機在 Windows Server 2012 上執行，有三部在 Windows Server 2012 R2 上執行，則請建立兩個複寫原則 – 每一種作業系統版本使用一個。</span><span class="sxs-lookup"><span data-stu-id="f7635-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="f7635-194">收到 hello 主要的保護容器 （主要 VMM 雲端） 和復原保護容器 （復原的 VMM 雲端），藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="f7635-195">擷取您在步驟 1 所使用的 hello 原則 hello hello 原則的好記的名稱</span><span class="sxs-lookup"><span data-stu-id="f7635-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="f7635-196">開始 hello 複寫原則中的 hello hello 保護容器 （VMM 雲端） 的關聯：</span><span class="sxs-lookup"><span data-stu-id="f7635-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="f7635-197">等候 hello 原則關聯工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="f7635-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="f7635-198">您可以檢查 hello 作業已使用下列 PowerShell 程式碼片段的 hello 來完成。</span><span class="sxs-lookup"><span data-stu-id="f7635-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="f7635-199">Hello 作業已完成處理之後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="f7635-200">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="f7635-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="f7635-201">步驟 6：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="f7635-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="f7635-202">hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7635-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="f7635-203">hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。</span><span class="sxs-lookup"><span data-stu-id="f7635-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="f7635-204">hello，下列命令會取得 hello 站台復原 hello 來源 VMM 伺服器和網路 hello 目標 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7635-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="f7635-205">第一個或 hello 第二個一個在 hello 伺服器陣列，可以 hello hello 來源 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7635-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="f7635-206">請檢查 hello hello VMM 伺服器名稱，並適當地取得 hello 網路</span><span class="sxs-lookup"><span data-stu-id="f7635-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="f7635-207">hello 最終 cmdlet 會建立 hello 主要網路與 hello 復原網路之間的對應。</span><span class="sxs-lookup"><span data-stu-id="f7635-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="f7635-208">hello 指令程式會指定 hello 主要網路作為 hello $PrimaryNetworks 和 hello $RecoveryNetworks hello 第一個項目與復原網路的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="f7635-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="f7635-209">步驟 7：設定儲存體對應</span><span class="sxs-lookup"><span data-stu-id="f7635-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="f7635-210">hello，下列命令會取得 hello 到 $storageclassifications 變數的儲存體分類清單。</span><span class="sxs-lookup"><span data-stu-id="f7635-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="f7635-211">hello，下列命令取得 hello 來源分類到 $SourceClassificaion 變數和目標分類到 $TargetClassification 變數。</span><span class="sxs-lookup"><span data-stu-id="f7635-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="f7635-212">hello 來源與目標分類可以 hello 陣列中的任何項目。</span><span class="sxs-lookup"><span data-stu-id="f7635-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="f7635-213">請參閱下面命令 toofigure hello 索引，來源與目標分類 $storageclassifications 陣列中的 hello toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="f7635-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="f7635-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="f7635-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="f7635-215">hello 以下指令程式會建立 hello 來源分類與 hello 目標分類之間的對應。</span><span class="sxs-lookup"><span data-stu-id="f7635-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="f7635-216">步驟 8：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="f7635-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="f7635-217">Hello 伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="f7635-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="f7635-218">tooenable 保護，執行下列命令 tooget hello 保護容器 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="f7635-219">取得 hello 保護實體 (VM) 執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f7635-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="f7635-220">執行下列命令的 hello 啟用 hello VM 的複寫：</span><span class="sxs-lookup"><span data-stu-id="f7635-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="f7635-221">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="f7635-221">Test your deployment</span></span>
<span data-ttu-id="f7635-222">tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器並執行測試容錯移轉的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7635-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="f7635-223">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="f7635-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="f7635-224">您可以在 Azure 入口網站中為應用程式建立復原方案。</span><span class="sxs-lookup"><span data-stu-id="f7635-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="f7635-225">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="f7635-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="f7635-226">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f7635-226">Run a test failover</span></span>
1. <span data-ttu-id="f7635-227">執行以下 cmdlet tooget hello VM 網路 toowhich hello 想 tootest 容錯移轉 Vm。</span><span class="sxs-lookup"><span data-stu-id="f7635-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="f7635-228">執行測試容錯移轉的 VM 執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7635-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="f7635-229">藉由 hello 下列執行復原計劃的測試容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="f7635-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="f7635-230">執行計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f7635-230">Run a planned failover</span></span>
1. <span data-ttu-id="f7635-231">執行規劃的容錯移轉的 VM 執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7635-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="f7635-232">執行規劃的容錯移轉復原方案執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f7635-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="f7635-233">執行非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f7635-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="f7635-234">執行規劃的容錯移轉的 VM 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f7635-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="f7635-235">2.執行規劃的容錯移轉復原方案執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f7635-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="f7635-236"><a name=monitor></a>監視活動</span><span class="sxs-lookup"><span data-stu-id="f7635-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="f7635-237">使用下列命令 toomonitor hello 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="f7635-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="f7635-238">請注意，您 toowait 之間 hello 處理 toofinish 的作業。</span><span class="sxs-lookup"><span data-stu-id="f7635-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="f7635-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7635-239">Next steps</span></span>
<span data-ttu-id="f7635-240">[閱讀更多](/powershell/module/azurerm.recoveryservices.backup/#recovery) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f7635-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
