---
title: "aaaPreparing 您註冊 Azure 虛擬機器的環境 tooback |Microsoft 文件"
description: "確認在 Azure 中備份虛擬機器的環境已準備就緒"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "備份；備份；"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a><span data-ttu-id="13e0b-104">準備您的環境 tooback Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="13e0b-104">Prepare your environment tooback up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13e0b-105">Resource Manager 模型</span><span class="sxs-lookup"><span data-stu-id="13e0b-105">Resource Manager model</span></span>](backup-azure-arm-vms-prepare.md)
> * [<span data-ttu-id="13e0b-106">傳統模型</span><span class="sxs-lookup"><span data-stu-id="13e0b-106">Classic model</span></span>](backup-azure-vms-prepare.md)
>
>

<span data-ttu-id="13e0b-107">在您可以備份 Azure 虛擬機器 (VM) 之前，有三個條件必須存在。</span><span class="sxs-lookup"><span data-stu-id="13e0b-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span></span>

* <span data-ttu-id="13e0b-108">您需要 toocreate 備份保存庫，或識別現有的備份保存庫*在 hello 與您的 VM 相同的區域*。</span><span class="sxs-lookup"><span data-stu-id="13e0b-108">You need toocreate a backup vault or identify an existing backup vault *in hello same region as your VM*.</span></span>
* <span data-ttu-id="13e0b-109">建立的 hello Azure 公用網際網路位址並 hello Azure 儲存體端點之間的網路連線。</span><span class="sxs-lookup"><span data-stu-id="13e0b-109">Establish network connectivity between hello Azure public Internet addresses and hello Azure storage endpoints.</span></span>
* <span data-ttu-id="13e0b-110">Hello VM 上安裝代理程式 hello VM。</span><span class="sxs-lookup"><span data-stu-id="13e0b-110">Install hello VM agent on hello VM.</span></span>

<span data-ttu-id="13e0b-111">如果您知道這些條件已存在於您的環境，然後繼續 toohello[備份您的 Vm 文章](backup-azure-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-111">If you know these conditions already exist in your environment then proceed toohello [Back up your VMs article](backup-azure-vms.md).</span></span> <span data-ttu-id="13e0b-112">否則，請閱讀，本文將引導您完成 hello 步驟 tooprepare 您的環境 tooback Azure vm。</span><span class="sxs-lookup"><span data-stu-id="13e0b-112">Otherwise, read on, this article will lead you through hello steps tooprepare your environment tooback up an Azure VM.</span></span>

##<a name="supported-operating-system-for-backup"></a><span data-ttu-id="13e0b-113">支援的備份作業系統</span><span class="sxs-lookup"><span data-stu-id="13e0b-113">Supported operating system for backup</span></span>
 * <span data-ttu-id="13e0b-114">**Linux**：Azure 備份支援 [Azure 所背書的散發套件清單](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ，但核心作業系統 Linux 除外。</span><span class="sxs-lookup"><span data-stu-id="13e0b-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span></span> <span data-ttu-id="13e0b-115">_其他提到-您-擁有-Linux 散發套件也可能會運作，只要 hello VM 代理程式位於 hello 虛擬機器和 Python 存在的支援。不過，我們並不為這些備份散發套件背書。_</span><span class="sxs-lookup"><span data-stu-id="13e0b-115">_Other Bring-Your-Own-Linux distributions also might work as long as hello VM agent is available on hello virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span></span>
 * <span data-ttu-id="13e0b-116">**Windows Server**：不支援比 Windows Server 2008 R2 更舊的版本。</span><span class="sxs-lookup"><span data-stu-id="13e0b-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span></span>


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a><span data-ttu-id="13e0b-117">備份和還原 VM 時的限制</span><span class="sxs-lookup"><span data-stu-id="13e0b-117">Limitations when backing up and restoring a VM</span></span>
> [!NOTE]
> <span data-ttu-id="13e0b-118">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-118">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="13e0b-119">hello 下列清單提供 hello 限制 hello 傳統模式中部署時。</span><span class="sxs-lookup"><span data-stu-id="13e0b-119">hello following list provides hello limitations when deploying in hello classic model.</span></span>
>
>

* <span data-ttu-id="13e0b-120">不支援備份具有 16 個以上資料磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="13e0b-120">Backing up virtual machines with more than 16 data disks is not supported.</span></span>
* <span data-ttu-id="13e0b-121">不支援備份具有保留的 IP 且沒有已定義之端點的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="13e0b-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span></span>
* <span data-ttu-id="13e0b-122">備份資料不包含掛接的網路磁碟機附加 tooVM。</span><span class="sxs-lookup"><span data-stu-id="13e0b-122">Backup data doesn't include network mounted drives attached tooVM.</span></span>
* <span data-ttu-id="13e0b-123">不支援在還原期間取代現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="13e0b-123">Replacing an existing virtual machine during restore is not supported.</span></span> <span data-ttu-id="13e0b-124">第一次刪除 hello 現有的虛擬機器和任何相關聯的磁碟，然後再從備份還原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="13e0b-124">First delete hello existing virtual machine and any associated disks, and then restore hello data from backup.</span></span>
* <span data-ttu-id="13e0b-125">不支援跨區域備份和還原。</span><span class="sxs-lookup"><span data-stu-id="13e0b-125">Cross-region backup and restore is not supported.</span></span>
* <span data-ttu-id="13e0b-126">在 Azure 的所有公用區域使用 hello Azure 備份服務來備份虛擬機器支援 (請參閱 hello[檢查清單](https://azure.microsoft.com/regions/#services)支援的地區)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-126">Backing up virtual machines by using hello Azure Backup service is supported in all public regions of Azure (see hello [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span></span> <span data-ttu-id="13e0b-127">如果您要尋找的 hello 地區不支援目前，它不會出現在 hello 下拉式清單中保存庫建立期間。</span><span class="sxs-lookup"><span data-stu-id="13e0b-127">If hello region that you are looking for is unsupported today, it will not appear in hello dropdown list during vault creation.</span></span>
* <span data-ttu-id="13e0b-128">使用 hello Azure 備份服務來備份虛擬機器僅支援選取的作業系統版本：</span><span class="sxs-lookup"><span data-stu-id="13e0b-128">Backing up virtual machines by using hello Azure Backup service is supported only for select operating system versions:</span></span>
* <span data-ttu-id="13e0b-129">只有透過 PowerShell 才支援還原屬於多網域控制站 (DC) 組態的 DC VM。</span><span class="sxs-lookup"><span data-stu-id="13e0b-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span></span> <span data-ttu-id="13e0b-130">進一步了解 [還原多 DC 網域控制站](backup-azure-restore-vms.md#restoring-domain-controller-vms)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span></span>
* <span data-ttu-id="13e0b-131">還原虛擬機器具有特殊的網路設定的 hello 只可透過 PowerShell 支援。</span><span class="sxs-lookup"><span data-stu-id="13e0b-131">Restoring virtual machines that have hello following special network configurations is supported only through PowerShell.</span></span> <span data-ttu-id="13e0b-132">您使用在 hello hello 還原工作流程建立的 Vm UI 不會有這些網路組態 hello 還原操作完成後。</span><span class="sxs-lookup"><span data-stu-id="13e0b-132">VMs that you create by using hello restore workflow in hello UI will not have these network configurations after hello restore operation is complete.</span></span> <span data-ttu-id="13e0b-133">詳細資訊，請參閱 toolearn[還原特殊的網路組態的 Vm](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-133">toolearn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span></span>
  * <span data-ttu-id="13e0b-134">負載平衡器組態下的虛擬機器 (內部與外部)</span><span class="sxs-lookup"><span data-stu-id="13e0b-134">Virtual machines under load balancer configuration (internal and external)</span></span>
  * <span data-ttu-id="13e0b-135">具有多個保留的 IP 位址的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="13e0b-135">Virtual machines with multiple reserved IP addresses</span></span>
  * <span data-ttu-id="13e0b-136">具有多個網路介面卡的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="13e0b-136">Virtual machines with multiple network adapters</span></span>

## <a name="create-a-backup-vault-for-a-vm"></a><span data-ttu-id="13e0b-137">為 VM 建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="13e0b-137">Create a backup vault for a VM</span></span>
<span data-ttu-id="13e0b-138">備份保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。</span><span class="sxs-lookup"><span data-stu-id="13e0b-138">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="13e0b-139">hello 備份保存庫也包含 hello 將會套用的 toohello 虛擬機器進行備份的備份原則。</span><span class="sxs-lookup"><span data-stu-id="13e0b-139">hello backup vault also contains hello backup policies that will be applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13e0b-140">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="13e0b-140">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span> <span data-ttu-id="13e0b-141">仍然支援現有的備份保存庫，且可能會太[使用 Azure PowerShell toocreate 備份保存庫](./backup-client-automation-classic.md#create-a-backup-vault)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-141">Existing Backup vaults are still supported, and it is possible too[use Azure PowerShell toocreate Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault).</span></span> <span data-ttu-id="13e0b-142">不過，Microsoft 建議您建立的所有部署的復原服務保存庫，因為未來的增強功能套用 tooRecovery 服務保存庫，僅。</span><span class="sxs-lookup"><span data-stu-id="13e0b-142">However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply tooRecovery Services vaults, only.</span></span>


<span data-ttu-id="13e0b-143">下圖顯示 hello hello 之間的關聯性各種 Azure 備份實體： ![Azure 備份實體和關聯性](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span><span class="sxs-lookup"><span data-stu-id="13e0b-143">This image shows hello relationships between hello various Azure Backup entities: ![Azure Backup entities and relationships](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span></span>



## <a name="network-connectivity"></a><span data-ttu-id="13e0b-144">網路連線</span><span class="sxs-lookup"><span data-stu-id="13e0b-144">Network connectivity</span></span>
<span data-ttu-id="13e0b-145">在訂單 toomanage hello VM 快照，hello 備用分機號碼需要連線 toohello Azure 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="13e0b-145">In order toomanage hello VM snapshots, hello backup extension needs connectivity toohello Azure public IP addresses.</span></span> <span data-ttu-id="13e0b-146">未 hello 正確連線到網際網路，hello 虛擬機器的 HTTP 要求逾時以及 hello 備份作業失敗。</span><span class="sxs-lookup"><span data-stu-id="13e0b-146">Without hello right Internet connectivity, hello virtual machine's HTTP requests time out and hello backup operation fails.</span></span> <span data-ttu-id="13e0b-147">如果您的部署有存取限制 (如透過網路安全性群組 (NSG))，請選擇其中一個選項來為備份流量提供明確的路徑︰</span><span class="sxs-lookup"><span data-stu-id="13e0b-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span></span>

* <span data-ttu-id="13e0b-148">[白名單 hello Azure 資料中心 IP 範圍](http://www.microsoft.com/en-us/download/details.aspx?id=41653)-請參閱 hello 文件，指示如何 toowhitelist hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="13e0b-148">[Whitelist hello Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see hello article for instructions on how toowhitelist hello IP addresses.</span></span>
* <span data-ttu-id="13e0b-149">部署 HTTP Proxy 伺服器來路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="13e0b-149">Deploy an HTTP proxy server for routing traffic.</span></span>

<span data-ttu-id="13e0b-150">當決定哪些選項 toouse，hello 取捨是管理能力、 細微的控制與成本之間。</span><span class="sxs-lookup"><span data-stu-id="13e0b-150">When deciding which option toouse, hello trade-offs are between manageability, granular control, and cost.</span></span>

| <span data-ttu-id="13e0b-151">選項</span><span class="sxs-lookup"><span data-stu-id="13e0b-151">Option</span></span> | <span data-ttu-id="13e0b-152">優點</span><span class="sxs-lookup"><span data-stu-id="13e0b-152">Advantages</span></span> | <span data-ttu-id="13e0b-153">缺點</span><span class="sxs-lookup"><span data-stu-id="13e0b-153">Disadvantages</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13e0b-154">將 IP 範圍列入允許清單</span><span class="sxs-lookup"><span data-stu-id="13e0b-154">Whitelist IP ranges</span></span> |<span data-ttu-id="13e0b-155">沒有額外的成本。</span><span class="sxs-lookup"><span data-stu-id="13e0b-155">No additional costs.</span></span><br><br><span data-ttu-id="13e0b-156">存取在中開啟的 NSG，使用 hello<i>組 AzureNetworkSecurityRule</i> cmdlet。</span><span class="sxs-lookup"><span data-stu-id="13e0b-156">For opening access in an NSG, use hello <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span></span> |<span data-ttu-id="13e0b-157">經過一段時間的影響 hello IP 範圍變更成的複雜 toomanage。</span><span class="sxs-lookup"><span data-stu-id="13e0b-157">Complex toomanage as hello impacted IP ranges change over time.</span></span><br><br><span data-ttu-id="13e0b-158">提供存取 toohello 整個 Azure 中，並不只是儲存體。</span><span class="sxs-lookup"><span data-stu-id="13e0b-158">Provides access toohello whole of Azure, and not just Storage.</span></span> |
| <span data-ttu-id="13e0b-159">HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="13e0b-159">HTTP proxy</span></span> |<span data-ttu-id="13e0b-160">允許更精確地控制在 hello proxy hello 儲存體 Url。</span><span class="sxs-lookup"><span data-stu-id="13e0b-160">Granular control in hello proxy over hello storage URLs allowed.</span></span> <span data-ttu-id="13e0b-161">toosetup hello proxy 中的細微控制 https://\*.blob.core.windows.net/\* URL 模式需要 toobe 白名單。</span><span class="sxs-lookup"><span data-stu-id="13e0b-161">toosetup granular control in hello proxy, https://\*.blob.core.windows.net/\* URL Pattern needs toobe whitelisted.</span></span> <span data-ttu-id="13e0b-162">toowhitelist 只 hello hello VM 所使用的儲存體帳戶 https://\<storageAccount\>.blob.core.windows.net/\* URL 模式需要 toobe 白名單。</span><span class="sxs-lookup"><span data-stu-id="13e0b-162">toowhitelist only hello storage account used by hello VM, https://\<storageAccount\>.blob.core.windows.net/\* URL pattern needs toobe whitelisted.</span></span> <br><span data-ttu-id="13e0b-163">單一點的網際網路存取 tooVMs。</span><span class="sxs-lookup"><span data-stu-id="13e0b-163">Single point of Internet access tooVMs.</span></span><br><span data-ttu-id="13e0b-164">不遵守 tooAzure IP 位址變更。</span><span class="sxs-lookup"><span data-stu-id="13e0b-164">Not subject tooAzure IP address changes.</span></span> |<span data-ttu-id="13e0b-165">Hello proxy 軟體中執行 VM 的額外成本。</span><span class="sxs-lookup"><span data-stu-id="13e0b-165">Additional costs for running a VM with hello proxy software.</span></span> |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a><span data-ttu-id="13e0b-166">白名單 hello Azure 資料中心 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="13e0b-166">Whitelist hello Azure datacenter IP ranges</span></span>
<span data-ttu-id="13e0b-167">toowhitelist hello Azure 資料中心 IP 範圍，請參閱 hello [Azure 網站](http://www.microsoft.com/en-us/download/details.aspx?id=41653)如 hello IP 範圍和指示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="13e0b-167">toowhitelist hello Azure datacenter IP ranges, please see hello [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on hello IP ranges, and instructions.</span></span>

### <a name="using-an-http-proxy-for-vm-backups"></a><span data-ttu-id="13e0b-168">使用 HTTP Proxy 進行 VM 備份</span><span class="sxs-lookup"><span data-stu-id="13e0b-168">Using an HTTP proxy for VM backups</span></span>
<span data-ttu-id="13e0b-169">當備份 VM，hello hello VM 上的備份延伸模組會傳送 hello 快照集管理命令 tooAzure 使用 HTTPS API 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="13e0b-169">When backing up a VM, hello backup extension on hello VM sends hello snapshot management commands tooAzure Storage using an HTTPS API.</span></span> <span data-ttu-id="13e0b-170">這些 hello 備用分機號碼流量透過 hello HTTP proxy 路由傳送，因為它是設定為存取 toohello hello 唯一元件公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="13e0b-170">Route hello backup extension traffic through hello HTTP proxy since it is hello only component configured for access toohello public Internet.</span></span>

> [!NOTE]
> <span data-ttu-id="13e0b-171">沒有建議應該使用的 hello proxy 軟體。</span><span class="sxs-lookup"><span data-stu-id="13e0b-171">There is no recommendation for hello proxy software that should be used.</span></span> <span data-ttu-id="13e0b-172">請確認您挑選具有輸出神奇結果的 proxy，而是與 hello 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="13e0b-172">Ensure that you pick a proxy that has outbound stickiness and which is compatible with hello configuration steps below.</span></span> <span data-ttu-id="13e0b-173">請確定第三方廠商軟體不會修改 hello proxy 設定</span><span class="sxs-lookup"><span data-stu-id="13e0b-173">Make sure third party softwares do not modify hello proxy settings</span></span>
>
>

<span data-ttu-id="13e0b-174">下面的 hello 範例影像會顯示 hello 三個設定步驟必要 toouse HTTP proxy:</span><span class="sxs-lookup"><span data-stu-id="13e0b-174">hello example image below shows hello three configuration steps necessary toouse an HTTP proxy:</span></span>

* <span data-ttu-id="13e0b-175">針對繫結的所有 HTTP 流量的應用程式 VM 路由 hello Proxy VM 透過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="13e0b-175">App VM routes all HTTP traffic bound for hello public Internet through Proxy VM.</span></span>
* <span data-ttu-id="13e0b-176">Proxy VM 會允許 hello 虛擬網路中的 Vm 所傳來的連入流量。</span><span class="sxs-lookup"><span data-stu-id="13e0b-176">Proxy VM allows incoming traffic from VMs in hello virtual network.</span></span>
* <span data-ttu-id="13e0b-177">網路安全性群組 (NSG) 名為 NSF 鎖定 hello 需要安全性規則允許連出網際網路流量從 Proxy VM。</span><span class="sxs-lookup"><span data-stu-id="13e0b-177">hello Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span></span>

![包含 HTTP Proxy 部署圖表的 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

<span data-ttu-id="13e0b-179">toouse HTTP proxy toocommunicating toohello 公用網際網路，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="13e0b-179">toouse an HTTP proxy toocommunicating toohello public Internet, follow these steps:</span></span>

#### <a name="step-1-configure-outgoing-network-connections"></a><span data-ttu-id="13e0b-180">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="13e0b-180">Step 1.</span></span> <span data-ttu-id="13e0b-181">設定連出網路連線</span><span class="sxs-lookup"><span data-stu-id="13e0b-181">Configure outgoing network connections</span></span>
###### <a name="for-windows-machines"></a><span data-ttu-id="13e0b-182">Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="13e0b-182">For Windows machines</span></span>
<span data-ttu-id="13e0b-183">這會設定本機系統帳戶的 Proxy 伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="13e0b-183">This will setup proxy server configuration for Local System Account.</span></span>

1. <span data-ttu-id="13e0b-184">下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span><span class="sxs-lookup"><span data-stu-id="13e0b-184">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span></span>
2. <span data-ttu-id="13e0b-185">從提升權限的提示字元執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="13e0b-185">Run following command from elevated prompt,</span></span>

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     <span data-ttu-id="13e0b-186">它會開啟 Internet Explorer 視窗。</span><span class="sxs-lookup"><span data-stu-id="13e0b-186">It will open internet explorer window.</span></span>
3. <span data-ttu-id="13e0b-187">移 tooTools]-> [網際網路選項]-> [連接]-> [LAN 設定。</span><span class="sxs-lookup"><span data-stu-id="13e0b-187">Go tooTools -> Internet Options -> Connections -> LAN settings.</span></span>
4. <span data-ttu-id="13e0b-188">確認系統帳戶的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="13e0b-188">Verify proxy settings for System account.</span></span> <span data-ttu-id="13e0b-189">設定 Proxy IP 和連接埠。</span><span class="sxs-lookup"><span data-stu-id="13e0b-189">Set Proxy IP and port.</span></span>
5. <span data-ttu-id="13e0b-190">關閉 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="13e0b-190">Close Internet Explorer.</span></span>

<span data-ttu-id="13e0b-191">這會設定一個整部機器的 Proxy 設定，並用於任何連出 HTTP/HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="13e0b-191">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span></span>

<span data-ttu-id="13e0b-192">如果您設定 proxy 伺服器上目前的使用者帳戶 （不是本機系統帳戶），請使用 hello 下列指令碼 tooapply 它們 tooSYSTEMACCOUNT:</span><span class="sxs-lookup"><span data-stu-id="13e0b-192">If you have setup a proxy server on a current user account(not a Local System Account), use hello following script tooapply them tooSYSTEMACCOUNT:</span></span>

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> <span data-ttu-id="13e0b-193">如果您在 Proxy 伺服器記錄檔中發現「(407) 需要 Proxy 驗證」，請檢查驗證設定是否正確。</span><span class="sxs-lookup"><span data-stu-id="13e0b-193">If you observe "(407)Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.</span></span>
>
>

###### <a name="for-linux-machines"></a><span data-ttu-id="13e0b-194">Linux 電腦</span><span class="sxs-lookup"><span data-stu-id="13e0b-194">For Linux machines</span></span>
<span data-ttu-id="13e0b-195">加入下列行 toohello hello```/etc/environment```檔案：</span><span class="sxs-lookup"><span data-stu-id="13e0b-195">Add hello following line toohello ```/etc/environment``` file:</span></span>

```
http_proxy=http://<proxy IP>:<proxy port>
```

<span data-ttu-id="13e0b-196">新增下列幾行 toohello hello```/etc/waagent.conf```檔案：</span><span class="sxs-lookup"><span data-stu-id="13e0b-196">Add hello following lines toohello ```/etc/waagent.conf``` file:</span></span>

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a><span data-ttu-id="13e0b-197">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="13e0b-197">Step 2.</span></span> <span data-ttu-id="13e0b-198">Hello proxy 伺服器上允許連入連線：</span><span class="sxs-lookup"><span data-stu-id="13e0b-198">Allow incoming connections on hello proxy server:</span></span>
1. <span data-ttu-id="13e0b-199">Hello proxy 伺服器上，開啟 Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="13e0b-199">On hello proxy server, open Windows Firewall.</span></span> <span data-ttu-id="13e0b-200">hello 最簡單方式 tooaccess hello 防火牆是 toosearch 具有進階安全性的 Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="13e0b-200">hello easiest way tooaccess hello firewall is toosearch for Windows Firewall with Advanced Security.</span></span>

    ![開啟防火牆 hello](./media/backup-azure-vms-prepare/firewall-01.png)
2. <span data-ttu-id="13e0b-202">在 hello Windows 防火牆對話方塊中，以滑鼠右鍵按一下**輸入規則**按一下**新增規則...**.</span><span class="sxs-lookup"><span data-stu-id="13e0b-202">In hello Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span></span>

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-02.png)
3. <span data-ttu-id="13e0b-204">在 [hello**新增輸入規則精靈**，選擇 hello**自訂**hello 選項**規則類型**按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="13e0b-204">In hello **New Inbound Rule Wizard**, choose hello **Custom** option for hello **Rule Type** and click **Next**.</span></span>
4. <span data-ttu-id="13e0b-205">在 [hello 頁面 tooselect hello**程式**，選擇**所有程式**按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="13e0b-205">On hello page tooselect hello **Program**, choose **All Programs** and click **Next**.</span></span>
5. <span data-ttu-id="13e0b-206">在 hello**通訊協定和連接埠**頁面上，輸入下列資訊的 hello，按一下 **下一步**:</span><span class="sxs-lookup"><span data-stu-id="13e0b-206">On hello **Protocol and Ports** page, enter hello following information and click **Next**:</span></span>

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-03.png)

   * <span data-ttu-id="13e0b-208">針對 [通訊協定類型]，請選擇 [TCP]</span><span class="sxs-lookup"><span data-stu-id="13e0b-208">for *Protocol type* choose *TCP*</span></span>
   * <span data-ttu-id="13e0b-209">如*本機連接埠*選擇*特定連接埠*，底下的 hello 欄位中指定 hello```<Proxy Port>```已經設定。</span><span class="sxs-lookup"><span data-stu-id="13e0b-209">for *Local port* choose *Specific Ports*, in hello field below specify hello ```<Proxy Port>``` that has been configured.</span></span>
   * <span data-ttu-id="13e0b-210">針對 [遠端連接埠]，請選取 [所有連接埠]</span><span class="sxs-lookup"><span data-stu-id="13e0b-210">for *Remote port* select *All Ports*</span></span>

     <span data-ttu-id="13e0b-211">Hello 精靈 hello 其餘部分，按一下 所有 hello 方式 toohello 結束，並指定此規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="13e0b-211">For hello rest of hello wizard, click all hello way toohello end and give this rule a name.</span></span>

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a><span data-ttu-id="13e0b-212">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="13e0b-212">Step 3.</span></span> <span data-ttu-id="13e0b-213">新增例外狀況規則 toohello NSG:</span><span class="sxs-lookup"><span data-stu-id="13e0b-213">Add an exception rule toohello NSG:</span></span>
<span data-ttu-id="13e0b-214">在使用 Azure PowerShell 命令提示字元中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13e0b-214">In an Azure PowerShell command prompt, enter hello following command:</span></span>

<span data-ttu-id="13e0b-215">hello，下列命令會將例外狀況 toohello NSG。</span><span class="sxs-lookup"><span data-stu-id="13e0b-215">hello following command adds an exception toohello NSG.</span></span> <span data-ttu-id="13e0b-216">這個例外狀況允許從 10.0.0.5 上任何連接埠 TCP 流量 tooany 通訊埠 80 (HTTP) 或 443 (HTTPS) 的網際網路位址。</span><span class="sxs-lookup"><span data-stu-id="13e0b-216">This exception allows TCP traffic from any port on 10.0.0.5 tooany Internet address on port 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="13e0b-217">如果您需要在特定的連接埠 hello 公用網際網路，可確定 tooadd 該通訊埠 toohello```-DestinationPortRange```以及。</span><span class="sxs-lookup"><span data-stu-id="13e0b-217">If you require a specific port in hello public Internet, be sure tooadd that port toohello ```-DestinationPortRange``` as well.</span></span>

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

<span data-ttu-id="13e0b-218">*請確定 hello 範例中的 hello 名稱取代 hello 詳細資料的適當 tooyour 部署。*</span><span class="sxs-lookup"><span data-stu-id="13e0b-218">*Ensure that you replace hello names in hello example with hello details appropriate tooyour deployment.*</span></span>

## <a name="vm-agent"></a><span data-ttu-id="13e0b-219">VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="13e0b-219">VM agent</span></span>
<span data-ttu-id="13e0b-220">您可以備份 hello Azure 虛擬機器之前，您應該確定該 hello Azure VM 代理程式已正確安裝 hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="13e0b-220">Before you can back up hello Azure virtual machine, you should ensure that hello Azure VM agent is correctly installed on hello virtual machine.</span></span> <span data-ttu-id="13e0b-221">由於 hello VM 代理程式是選用的元件在 hello 建立 hello 虛擬機器的時間，確定 hello VM 代理程式會選取前 hello 虛擬機器已佈建該 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="13e0b-221">Since hello VM agent is an optional component at hello time that hello virtual machine is created, ensure that hello check box for hello VM agent is selected before hello virtual machine is provisioned.</span></span>

### <a name="manual-installation-and-update"></a><span data-ttu-id="13e0b-222">手動安裝和更新</span><span class="sxs-lookup"><span data-stu-id="13e0b-222">Manual installation and update</span></span>
<span data-ttu-id="13e0b-223">hello VM 代理程式已經在 Vm 中建立的 hello Azure 圖庫中。</span><span class="sxs-lookup"><span data-stu-id="13e0b-223">hello VM agent is already present in VMs that are created from hello Azure gallery.</span></span> <span data-ttu-id="13e0b-224">不過，從內部部署資料中心移轉的虛擬機器沒有 hello 安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="13e0b-224">However, virtual machines that are migrated from on-premises datacenters would not have hello VM agent installed.</span></span> <span data-ttu-id="13e0b-225">對於這類的 Vm，必須明確安裝 toobe hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="13e0b-225">For such VMs, hello VM agent needs toobe installed explicitly.</span></span> <span data-ttu-id="13e0b-226">深入了解[現有的 VM 上安裝 hello VM 代理程式](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-226">Read more about [installing hello VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span></span>

| <span data-ttu-id="13e0b-227">**作業**</span><span class="sxs-lookup"><span data-stu-id="13e0b-227">**Operation**</span></span> | <span data-ttu-id="13e0b-228">**Windows**</span><span class="sxs-lookup"><span data-stu-id="13e0b-228">**Windows**</span></span> | <span data-ttu-id="13e0b-229">**Linux**</span><span class="sxs-lookup"><span data-stu-id="13e0b-229">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13e0b-230">Hello VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="13e0b-230">Installing hello VM agent</span></span> |<li><span data-ttu-id="13e0b-231">下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-231">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="13e0b-232">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="13e0b-232">You will need Administrator privileges toocomplete hello installation.</span></span> <li><span data-ttu-id="13e0b-233">[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="13e0b-233">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |<li> <span data-ttu-id="13e0b-234">安裝最新的 hello [Linux 代理程式](https://github.com/Azure/WALinuxAgent)從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="13e0b-234">Install hello latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="13e0b-235">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="13e0b-235">You will need Administrator privileges toocomplete hello installation.</span></span> <li> <span data-ttu-id="13e0b-236">[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。</span><span class="sxs-lookup"><span data-stu-id="13e0b-236">[Update hello VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate that hello agent is installed.</span></span> |
| <span data-ttu-id="13e0b-237">更新 hello VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="13e0b-237">Updating hello VM agent</span></span> |<span data-ttu-id="13e0b-238">更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-238">Updating hello VM agent is as simple as reinstalling hello [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><br><span data-ttu-id="13e0b-239">請確認在 hello VM 代理程式在更新時，執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="13e0b-239">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |<span data-ttu-id="13e0b-240">依 hello 指示[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-240">Follow hello instructions on [updating hello Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><br><span data-ttu-id="13e0b-241">請確認在 hello VM 代理程式在更新時，執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="13e0b-241">Ensure that no backup operation is running while hello VM agent is being updated.</span></span> |
| <span data-ttu-id="13e0b-242">正在驗證 hello VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="13e0b-242">Validating hello VM agent installation</span></span> |<li><span data-ttu-id="13e0b-243">瀏覽 toohello *C:\WindowsAzure\Packages* hello Azure VM 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="13e0b-243">Navigate toohello *C:\WindowsAzure\Packages* folder in hello Azure VM.</span></span> <li><span data-ttu-id="13e0b-244">您應該尋找 hello WaAppAgent.exe 檔案存在。</span><span class="sxs-lookup"><span data-stu-id="13e0b-244">You should find hello WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="13e0b-245">以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="13e0b-245">Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="13e0b-246">N/A</span><span class="sxs-lookup"><span data-stu-id="13e0b-246">N/A</span></span> |

<span data-ttu-id="13e0b-247">深入了解 hello [VM 代理程式](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409)和[如何 tooinstall 它](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-247">Learn about hello [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how tooinstall it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span></span>

### <a name="backup-extension"></a><span data-ttu-id="13e0b-248">備份擴充功能</span><span class="sxs-lookup"><span data-stu-id="13e0b-248">Backup extension</span></span>
<span data-ttu-id="13e0b-249">tooback hello 虛擬機器，hello Azure 備份服務會安裝延伸 toohello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="13e0b-249">tooback up hello virtual machine, hello Azure Backup service installs an extension toohello VM agent.</span></span> <span data-ttu-id="13e0b-250">hello Azure 備份服務順暢地升級和修補程式不需要額外的使用者介入的 hello 備用分機號碼。</span><span class="sxs-lookup"><span data-stu-id="13e0b-250">hello Azure Backup service seamlessly upgrades and patches hello backup extension without additional user intervention.</span></span>

<span data-ttu-id="13e0b-251">如果 hello VM 正在執行，就會安裝 hello 備用分機號碼。</span><span class="sxs-lookup"><span data-stu-id="13e0b-251">hello backup extension is installed if hello VM is running.</span></span> <span data-ttu-id="13e0b-252">執行中的 VM 也提供 hello 取得應用程式一致復原點的最大的機會。</span><span class="sxs-lookup"><span data-stu-id="13e0b-252">A running VM also provides hello greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="13e0b-253">不過，hello Azure 備份服務將會繼續向上 hello VM-tooback，即使它已關閉，而且找不到 hello 擴充功能安裝 (也稱為離線 VM)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-253">However, hello Azure Backup service will continue tooback up hello VM--even if it is turned off, and hello extension could not be installed (aka Offline VM).</span></span> <span data-ttu-id="13e0b-254">Hello 復原點將會在此情況下，*絕對一致*如同上面所討論。</span><span class="sxs-lookup"><span data-stu-id="13e0b-254">In this case, hello recovery point will be *crash consistent* as discussed above.</span></span>

## <a name="questions"></a><span data-ttu-id="13e0b-255">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="13e0b-255">Questions?</span></span>
<span data-ttu-id="13e0b-256">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="13e0b-256">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e0b-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13e0b-257">Next steps</span></span>
<span data-ttu-id="13e0b-258">既然您已經備妥您的環境來備份您的 VM，您下一步是 toocreate 備份。</span><span class="sxs-lookup"><span data-stu-id="13e0b-258">Now that you have prepared your environment for backing up your VM, your next logical step is toocreate a backup.</span></span> <span data-ttu-id="13e0b-259">規劃發行項的 hello 提供備份 Vm 的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="13e0b-259">hello planning article provides more detailed information about backing up VMs.</span></span>

* [<span data-ttu-id="13e0b-260">備份虛擬機器</span><span class="sxs-lookup"><span data-stu-id="13e0b-260">Back up virtual machines</span></span>](backup-azure-vms.md)
* [<span data-ttu-id="13e0b-261">規劃 VM 備份基礎結構</span><span class="sxs-lookup"><span data-stu-id="13e0b-261">Plan your VM backup infrastructure</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="13e0b-262">管理虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="13e0b-262">Manage virtual machine backups</span></span>](backup-azure-manage-vms.md)
