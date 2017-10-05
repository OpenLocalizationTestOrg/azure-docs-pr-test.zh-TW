---
title: "準備環境以備份 Azure 虛擬機器 | Microsoft Docs"
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
ms.openlocfilehash: 072efdccaa8df5d430314d753a437b524986b53c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-your-environment-to-back-up-azure-virtual-machines"></a><span data-ttu-id="ad420-104">準備環境以備份 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ad420-104">Prepare your environment to back up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad420-105">Resource Manager 模型</span><span class="sxs-lookup"><span data-stu-id="ad420-105">Resource Manager model</span></span>](backup-azure-arm-vms-prepare.md)
> * [<span data-ttu-id="ad420-106">傳統模型</span><span class="sxs-lookup"><span data-stu-id="ad420-106">Classic model</span></span>](backup-azure-vms-prepare.md)
>
>

<span data-ttu-id="ad420-107">在您可以備份 Azure 虛擬機器 (VM) 之前，有三個條件必須存在。</span><span class="sxs-lookup"><span data-stu-id="ad420-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span></span>

* <span data-ttu-id="ad420-108">您需要在「與 VM 的相同區域中」 建立備份保存庫，或識別現有的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ad420-108">You need to create a backup vault or identify an existing backup vault *in the same region as your VM*.</span></span>
* <span data-ttu-id="ad420-109">在 Azure 公用網際網路位址和 Azure 儲存體端點之間建立網路連線。</span><span class="sxs-lookup"><span data-stu-id="ad420-109">Establish network connectivity between the Azure public Internet addresses and the Azure storage endpoints.</span></span>
* <span data-ttu-id="ad420-110">在 VM 上安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-110">Install the VM agent on the VM.</span></span>

<span data-ttu-id="ad420-111">如果您知道環境滿足這些條件，請繼續依 [備份 VM 文章](backup-azure-vms.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="ad420-111">If you know these conditions already exist in your environment then proceed to the [Back up your VMs article](backup-azure-vms.md).</span></span> <span data-ttu-id="ad420-112">否則，請繼續閱讀，這篇文章會引導您逐步完成備妥環境來備份 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ad420-112">Otherwise, read on, this article will lead you through the steps to prepare your environment to back up an Azure VM.</span></span>

##<a name="supported-operating-system-for-backup"></a><span data-ttu-id="ad420-113">支援的備份作業系統</span><span class="sxs-lookup"><span data-stu-id="ad420-113">Supported operating system for backup</span></span>
 * <span data-ttu-id="ad420-114">**Linux**：Azure 備份支援 [Azure 所背書的散發套件清單](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ，但核心作業系統 Linux 除外。</span><span class="sxs-lookup"><span data-stu-id="ad420-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span></span> <span data-ttu-id="ad420-115">_只要虛擬機器上有 VM 代理程式並且可支援 Python，其他「攜帶您自己的 Linux」散發套件可能也可以運作。不過，我們並不為這些備份散發套件背書。_</span><span class="sxs-lookup"><span data-stu-id="ad420-115">_Other Bring-Your-Own-Linux distributions also might work as long as the VM agent is available on the virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span></span>
 * <span data-ttu-id="ad420-116">**Windows Server**：不支援比 Windows Server 2008 R2 更舊的版本。</span><span class="sxs-lookup"><span data-stu-id="ad420-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span></span>


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a><span data-ttu-id="ad420-117">備份和還原 VM 時的限制</span><span class="sxs-lookup"><span data-stu-id="ad420-117">Limitations when backing up and restoring a VM</span></span>
> [!NOTE]
> <span data-ttu-id="ad420-118">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ad420-118">Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ad420-119">下列清單提供在傳統的模型中部署時的限制。</span><span class="sxs-lookup"><span data-stu-id="ad420-119">The following list provides the limitations when deploying in the classic model.</span></span>
>
>

* <span data-ttu-id="ad420-120">不支援備份具有 16 個以上資料磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ad420-120">Backing up virtual machines with more than 16 data disks is not supported.</span></span>
* <span data-ttu-id="ad420-121">不支援備份具有保留的 IP 且沒有已定義之端點的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ad420-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span></span>
* <span data-ttu-id="ad420-122">備份資料不包含連接至 VM 的網路掛接磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ad420-122">Backup data doesn't include network mounted drives attached to VM.</span></span>
* <span data-ttu-id="ad420-123">不支援在還原期間取代現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ad420-123">Replacing an existing virtual machine during restore is not supported.</span></span> <span data-ttu-id="ad420-124">先刪除現有的虛擬機器及任何相關聯的磁碟，然後從備份還原資料。</span><span class="sxs-lookup"><span data-stu-id="ad420-124">First delete the existing virtual machine and any associated disks, and then restore the data from backup.</span></span>
* <span data-ttu-id="ad420-125">不支援跨區域備份和還原。</span><span class="sxs-lookup"><span data-stu-id="ad420-125">Cross-region backup and restore is not supported.</span></span>
* <span data-ttu-id="ad420-126">Azure 的所有公用區域皆支援使用「Azure 備份」服務來備份虛擬機器 (請參閱支援的區域 [檢查清單](https://azure.microsoft.com/regions/#services) )。</span><span class="sxs-lookup"><span data-stu-id="ad420-126">Backing up virtual machines by using the Azure Backup service is supported in all public regions of Azure (see the [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span></span> <span data-ttu-id="ad420-127">如果您尋找的區域目前不受支援，在建立保存庫期間，該區域就不會顯示在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="ad420-127">If the region that you are looking for is unsupported today, it will not appear in the dropdown list during vault creation.</span></span>
* <span data-ttu-id="ad420-128">只有特定的作業系統版本才支援使用「Azure 備份」服務來備份虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="ad420-128">Backing up virtual machines by using the Azure Backup service is supported only for select operating system versions:</span></span>
* <span data-ttu-id="ad420-129">只有透過 PowerShell 才支援還原屬於多網域控制站 (DC) 組態的 DC VM。</span><span class="sxs-lookup"><span data-stu-id="ad420-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span></span> <span data-ttu-id="ad420-130">進一步了解 [還原多 DC 網域控制站](backup-azure-restore-vms.md#restoring-domain-controller-vms)。</span><span class="sxs-lookup"><span data-stu-id="ad420-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span></span>
* <span data-ttu-id="ad420-131">僅支援透過 PowerShell 還原具有以下特殊網路組態的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ad420-131">Restoring virtual machines that have the following special network configurations is supported only through PowerShell.</span></span> <span data-ttu-id="ad420-132">藉由使用 UI 中的還原工作流程來建立的 VM 在還原作業完成之後，將不會具有這些網路組態。</span><span class="sxs-lookup"><span data-stu-id="ad420-132">VMs that you create by using the restore workflow in the UI will not have these network configurations after the restore operation is complete.</span></span> <span data-ttu-id="ad420-133">若要深入了解，請參閱 [還原具有特殊網路組態的 VM](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)。</span><span class="sxs-lookup"><span data-stu-id="ad420-133">To learn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span></span>
  * <span data-ttu-id="ad420-134">負載平衡器組態下的虛擬機器 (內部與外部)</span><span class="sxs-lookup"><span data-stu-id="ad420-134">Virtual machines under load balancer configuration (internal and external)</span></span>
  * <span data-ttu-id="ad420-135">具有多個保留的 IP 位址的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ad420-135">Virtual machines with multiple reserved IP addresses</span></span>
  * <span data-ttu-id="ad420-136">具有多個網路介面卡的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ad420-136">Virtual machines with multiple network adapters</span></span>

## <a name="create-a-backup-vault-for-a-vm"></a><span data-ttu-id="ad420-137">為 VM 建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="ad420-137">Create a backup vault for a VM</span></span>
<span data-ttu-id="ad420-138">備份保存庫是一個實體，儲存隨著時間建立的所有備份和復原點。</span><span class="sxs-lookup"><span data-stu-id="ad420-138">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="ad420-139">備份保存庫也包含備份虛擬機器時將套用的備份原則。</span><span class="sxs-lookup"><span data-stu-id="ad420-139">The backup vault also contains the backup policies that will be applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad420-140">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ad420-140">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span> <span data-ttu-id="ad420-141">我們仍然支援現有的備份保存庫，您也可以[使用 Azure PowerShell 來建立備份保存庫](./backup-client-automation-classic.md#create-a-backup-vault)。</span><span class="sxs-lookup"><span data-stu-id="ad420-141">Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault).</span></span> <span data-ttu-id="ad420-142">不過，Microsoft 建議您建立所有部署的復原服務保存庫，因為未來的增強功能僅適用於復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ad420-142">However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.</span></span>


<span data-ttu-id="ad420-143">此影像顯示各種 Azure 備份實體之間的關係：![Azure 備份實體和關聯性](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span><span class="sxs-lookup"><span data-stu-id="ad420-143">This image shows the relationships between the various Azure Backup entities: ![Azure Backup entities and relationships](./media/backup-azure-vms-prepare/vault-policy-vm.png)</span></span>



## <a name="network-connectivity"></a><span data-ttu-id="ad420-144">網路連線</span><span class="sxs-lookup"><span data-stu-id="ad420-144">Network connectivity</span></span>
<span data-ttu-id="ad420-145">為了管理 VM 快照，備份擴充功能需要連接 Azure 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ad420-145">In order to manage the VM snapshots, the backup extension needs connectivity to the Azure public IP addresses.</span></span> <span data-ttu-id="ad420-146">若無適當的網際網路連線，虛擬機器的 HTTP 要求將會逾時，而備份作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="ad420-146">Without the right Internet connectivity, the virtual machine's HTTP requests time out and the backup operation fails.</span></span> <span data-ttu-id="ad420-147">如果您的部署有存取限制 (如透過網路安全性群組 (NSG))，請選擇其中一個選項來為備份流量提供明確的路徑︰</span><span class="sxs-lookup"><span data-stu-id="ad420-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span></span>

* <span data-ttu-id="ad420-148">[將 Azure 資料中心 IP 範圍列入允許清單](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - 請參閱文章以取得將 IP 位址列入白名單的指示。</span><span class="sxs-lookup"><span data-stu-id="ad420-148">[Whitelist the Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see the article for instructions on how to whitelist the IP addresses.</span></span>
* <span data-ttu-id="ad420-149">部署 HTTP Proxy 伺服器來路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="ad420-149">Deploy an HTTP proxy server for routing traffic.</span></span>

<span data-ttu-id="ad420-150">在決定該使用哪個選項時，要取捨的不外乎是可管理性、精確控制及成本等要素。</span><span class="sxs-lookup"><span data-stu-id="ad420-150">When deciding which option to use, the trade-offs are between manageability, granular control, and cost.</span></span>

| <span data-ttu-id="ad420-151">選項</span><span class="sxs-lookup"><span data-stu-id="ad420-151">Option</span></span> | <span data-ttu-id="ad420-152">優點</span><span class="sxs-lookup"><span data-stu-id="ad420-152">Advantages</span></span> | <span data-ttu-id="ad420-153">缺點</span><span class="sxs-lookup"><span data-stu-id="ad420-153">Disadvantages</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad420-154">將 IP 範圍列入允許清單</span><span class="sxs-lookup"><span data-stu-id="ad420-154">Whitelist IP ranges</span></span> |<span data-ttu-id="ad420-155">沒有額外的成本。</span><span class="sxs-lookup"><span data-stu-id="ad420-155">No additional costs.</span></span><br><br><span data-ttu-id="ad420-156">如需在某個 NSG 中開啟存取權，請使用 <i>Set-AzureNetworkSecurityRule</i> Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ad420-156">For opening access in an NSG, use the <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span></span> |<span data-ttu-id="ad420-157">由於受影響的 IP 範圍會隨著時間改變，因此難以管理。</span><span class="sxs-lookup"><span data-stu-id="ad420-157">Complex to manage as the impacted IP ranges change over time.</span></span><br><br><span data-ttu-id="ad420-158">提供整個 Azure 的存取權，而不只是「儲存體」的存取權。</span><span class="sxs-lookup"><span data-stu-id="ad420-158">Provides access to the whole of Azure, and not just Storage.</span></span> |
| <span data-ttu-id="ad420-159">HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="ad420-159">HTTP proxy</span></span> |<span data-ttu-id="ad420-160">在 proxy 中精確控制允許的儲存體 URL。</span><span class="sxs-lookup"><span data-stu-id="ad420-160">Granular control in the proxy over the storage URLs allowed.</span></span> <span data-ttu-id="ad420-161">若要在 Proxy 中設定細微控制，必須將 https://\*.blob.core.windows.net/\* URL 模式設為允許清單。</span><span class="sxs-lookup"><span data-stu-id="ad420-161">To setup granular control in the proxy, https://\*.blob.core.windows.net/\* URL Pattern needs to be whitelisted.</span></span> <span data-ttu-id="ad420-162">若只要將 VM 所使用的儲存體帳戶白名單設為允許清單，必須將 https://\<storageAccount\>.blob.core.windows.net/\* URL 模式設為允許清單。</span><span class="sxs-lookup"><span data-stu-id="ad420-162">To whitelist only the storage account used by the VM, https://\<storageAccount\>.blob.core.windows.net/\* URL pattern needs to be whitelisted.</span></span> <br><span data-ttu-id="ad420-163">VM 的單一網際網路存取點。</span><span class="sxs-lookup"><span data-stu-id="ad420-163">Single point of Internet access to VMs.</span></span><br><span data-ttu-id="ad420-164">不會隨著 Azure IP 位址變更。</span><span class="sxs-lookup"><span data-stu-id="ad420-164">Not subject to Azure IP address changes.</span></span> |<span data-ttu-id="ad420-165">使用 Proxy 軟體執行 VM 時的額外成本。</span><span class="sxs-lookup"><span data-stu-id="ad420-165">Additional costs for running a VM with the proxy software.</span></span> |

### <a name="whitelist-the-azure-datacenter-ip-ranges"></a><span data-ttu-id="ad420-166">將 Azure 資料中心 IP 範圍列入允許清單</span><span class="sxs-lookup"><span data-stu-id="ad420-166">Whitelist the Azure datacenter IP ranges</span></span>
<span data-ttu-id="ad420-167">若要將 Azure 資料中心 IP 範圍列入允許清單，請參閱 [Azure 網站](http://www.microsoft.com/en-us/download/details.aspx?id=41653) 以取得 IP 範圍的詳細資料和指示。</span><span class="sxs-lookup"><span data-stu-id="ad420-167">To whitelist the Azure datacenter IP ranges, please see the [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on the IP ranges, and instructions.</span></span>

### <a name="using-an-http-proxy-for-vm-backups"></a><span data-ttu-id="ad420-168">使用 HTTP Proxy 進行 VM 備份</span><span class="sxs-lookup"><span data-stu-id="ad420-168">Using an HTTP proxy for VM backups</span></span>
<span data-ttu-id="ad420-169">備份 VM 時，VM 上的備份擴充功能會使用 HTTPS API 將快照管理命令傳送到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ad420-169">When backing up a VM, the backup extension on the VM sends the snapshot management commands to Azure Storage using an HTTPS API.</span></span> <span data-ttu-id="ad420-170">透過 HTTP Proxy 路由傳送擴充功能流量，因為它是唯一為了要存取公用網際網路而設定的元件。</span><span class="sxs-lookup"><span data-stu-id="ad420-170">Route the backup extension traffic through the HTTP proxy since it is the only component configured for access to the public Internet.</span></span>

> [!NOTE]
> <span data-ttu-id="ad420-171">對於應該使用什麼 Proxy 軟體，並無任何建議。</span><span class="sxs-lookup"><span data-stu-id="ad420-171">There is no recommendation for the proxy software that should be used.</span></span> <span data-ttu-id="ad420-172">請務必挑選具備輸出綁定 (outbound stickiness) 功能，且與下方設定步驟相容的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="ad420-172">Ensure that you pick a proxy that has outbound stickiness and which is compatible with the configuration steps below.</span></span> <span data-ttu-id="ad420-173">確定第三方軟體沒有修改 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="ad420-173">Make sure third party softwares do not modify the proxy settings</span></span>
>
>

<span data-ttu-id="ad420-174">以下範例影像示範使用 HTTP Proxy 所需的三個組態步驟︰</span><span class="sxs-lookup"><span data-stu-id="ad420-174">The example image below shows the three configuration steps necessary to use an HTTP proxy:</span></span>

* <span data-ttu-id="ad420-175">應用程式 VM 會透過 Proxy VM 路由傳送所有連往公用網際網路的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="ad420-175">App VM routes all HTTP traffic bound for the public Internet through Proxy VM.</span></span>
* <span data-ttu-id="ad420-176">Proxy VM 允許從虛擬網路之 VM 傳輸的傳入流量。</span><span class="sxs-lookup"><span data-stu-id="ad420-176">Proxy VM allows incoming traffic from VMs in the virtual network.</span></span>
* <span data-ttu-id="ad420-177">名為 NSF-lockdown 的網路安全性群組 (NSG) 需要允許從 Proxy VM 傳輸之輸出網際網路流量的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="ad420-177">The Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span></span>

![包含 HTTP Proxy 部署圖表的 NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

<span data-ttu-id="ad420-179">若要使用 HTTP Proxy 來與公用網際網路通訊，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="ad420-179">To use an HTTP proxy to communicating to the public Internet, follow these steps:</span></span>

#### <a name="step-1-configure-outgoing-network-connections"></a><span data-ttu-id="ad420-180">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="ad420-180">Step 1.</span></span> <span data-ttu-id="ad420-181">設定連出網路連線</span><span class="sxs-lookup"><span data-stu-id="ad420-181">Configure outgoing network connections</span></span>
###### <a name="for-windows-machines"></a><span data-ttu-id="ad420-182">Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="ad420-182">For Windows machines</span></span>
<span data-ttu-id="ad420-183">這會設定本機系統帳戶的 Proxy 伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="ad420-183">This will setup proxy server configuration for Local System Account.</span></span>

1. <span data-ttu-id="ad420-184">下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span><span class="sxs-lookup"><span data-stu-id="ad420-184">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span></span>
2. <span data-ttu-id="ad420-185">從提升權限的提示字元執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="ad420-185">Run following command from elevated prompt,</span></span>

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     <span data-ttu-id="ad420-186">它會開啟 Internet Explorer 視窗。</span><span class="sxs-lookup"><span data-stu-id="ad420-186">It will open internet explorer window.</span></span>
3. <span data-ttu-id="ad420-187">移至 [工具]-> [網際網路選項]-> [連線]-> [區域網路設定]。</span><span class="sxs-lookup"><span data-stu-id="ad420-187">Go to Tools -> Internet Options -> Connections -> LAN settings.</span></span>
4. <span data-ttu-id="ad420-188">確認系統帳戶的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="ad420-188">Verify proxy settings for System account.</span></span> <span data-ttu-id="ad420-189">設定 Proxy IP 和連接埠。</span><span class="sxs-lookup"><span data-stu-id="ad420-189">Set Proxy IP and port.</span></span>
5. <span data-ttu-id="ad420-190">關閉 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="ad420-190">Close Internet Explorer.</span></span>

<span data-ttu-id="ad420-191">這會設定一個整部機器的 Proxy 設定，並用於任何連出 HTTP/HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="ad420-191">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span></span>

<span data-ttu-id="ad420-192">如果您已在目前的使用者帳戶 (非本機系統帳戶) 上設定 Proxy 伺服器，請使用下列指令碼將它們套用至 SYSTEMACCOUNT︰</span><span class="sxs-lookup"><span data-stu-id="ad420-192">If you have setup a proxy server on a current user account(not a Local System Account), use the following script to apply them to SYSTEMACCOUNT:</span></span>

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> <span data-ttu-id="ad420-193">如果您在 Proxy 伺服器記錄檔中發現「(407) 需要 Proxy 驗證」，請檢查驗證設定是否正確。</span><span class="sxs-lookup"><span data-stu-id="ad420-193">If you observe "(407)Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.</span></span>
>
>

###### <a name="for-linux-machines"></a><span data-ttu-id="ad420-194">Linux 電腦</span><span class="sxs-lookup"><span data-stu-id="ad420-194">For Linux machines</span></span>
<span data-ttu-id="ad420-195">在 ```/etc/environment``` 檔案中新增以下文字行：</span><span class="sxs-lookup"><span data-stu-id="ad420-195">Add the following line to the ```/etc/environment``` file:</span></span>

```
http_proxy=http://<proxy IP>:<proxy port>
```

<span data-ttu-id="ad420-196">將下列幾行新增至 ```/etc/waagent.conf``` 檔案：</span><span class="sxs-lookup"><span data-stu-id="ad420-196">Add the following lines to the ```/etc/waagent.conf``` file:</span></span>

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-the-proxy-server"></a><span data-ttu-id="ad420-197">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="ad420-197">Step 2.</span></span> <span data-ttu-id="ad420-198">在 Proxy 伺服器上允許連入連線：</span><span class="sxs-lookup"><span data-stu-id="ad420-198">Allow incoming connections on the proxy server:</span></span>
1. <span data-ttu-id="ad420-199">在 Proxy 伺服器上，開啟 [Windows 防火牆]。</span><span class="sxs-lookup"><span data-stu-id="ad420-199">On the proxy server, open Windows Firewall.</span></span> <span data-ttu-id="ad420-200">存取防火牆最簡單的方式搜尋「具有進階安全性的 Windows 防火牆」。</span><span class="sxs-lookup"><span data-stu-id="ad420-200">The easiest way to access the firewall is to search for Windows Firewall with Advanced Security.</span></span>

    ![開啟防火牆](./media/backup-azure-vms-prepare/firewall-01.png)
2. <span data-ttu-id="ad420-202">在 [Windows 防火牆] 對話方塊中，以滑鼠右鍵按一下 [輸入規則] 並按一下 [新增規則...]。</span><span class="sxs-lookup"><span data-stu-id="ad420-202">In the Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span></span>

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-02.png)
3. <span data-ttu-id="ad420-204">在 [新增輸入規則精靈] 中，針對 [規則類型] 選擇 [自訂] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ad420-204">In the **New Inbound Rule Wizard**, choose the **Custom** option for the **Rule Type** and click **Next**.</span></span>
4. <span data-ttu-id="ad420-205">在選取 [程式] 的頁面上，選擇 [所有程式]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ad420-205">On the page to select the **Program**, choose **All Programs** and click **Next**.</span></span>
5. <span data-ttu-id="ad420-206">在 [通訊協定和連接埠] 頁面上，輸入下列資訊，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="ad420-206">On the **Protocol and Ports** page, enter the following information and click **Next**:</span></span>

    ![建立新的規則](./media/backup-azure-vms-prepare/firewall-03.png)

   * <span data-ttu-id="ad420-208">針對 [通訊協定類型]，請選擇 [TCP]</span><span class="sxs-lookup"><span data-stu-id="ad420-208">for *Protocol type* choose *TCP*</span></span>
   * <span data-ttu-id="ad420-209">針對 [本機連接埠]，請選擇 [特定連接埠]，在下方欄位中指定已經設定的 ```<Proxy Port>```。</span><span class="sxs-lookup"><span data-stu-id="ad420-209">for *Local port* choose *Specific Ports*, in the field below specify the ```<Proxy Port>``` that has been configured.</span></span>
   * <span data-ttu-id="ad420-210">針對 [遠端連接埠]，請選取 [所有連接埠]</span><span class="sxs-lookup"><span data-stu-id="ad420-210">for *Remote port* select *All Ports*</span></span>

     <span data-ttu-id="ad420-211">在精靈的其餘部分，按一下直到結束為止並指定此規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="ad420-211">For the rest of the wizard, click all the way to the end and give this rule a name.</span></span>

#### <a name="step-3-add-an-exception-rule-to-the-nsg"></a><span data-ttu-id="ad420-212">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="ad420-212">Step 3.</span></span> <span data-ttu-id="ad420-213">新增 NSG 例外規則：</span><span class="sxs-lookup"><span data-stu-id="ad420-213">Add an exception rule to the NSG:</span></span>
<span data-ttu-id="ad420-214">在 Azure PowerShell 命令提示字元中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ad420-214">In an Azure PowerShell command prompt, enter the following command:</span></span>

<span data-ttu-id="ad420-215">下列命令會新增 NSG 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ad420-215">The following command adds an exception to the NSG.</span></span> <span data-ttu-id="ad420-216">此例外狀況允許從 10.0.0.5 上任何連接埠傳輸至 80 (HTTP) 或 443 (HTTPS) 連接埠上任何網際網路位址的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="ad420-216">This exception allows TCP traffic from any port on 10.0.0.5 to any Internet address on port 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="ad420-217">如果您需要公用網際網路中的特定連接埠，請務必將該連接埠一併新增至 ```-DestinationPortRange``` 。</span><span class="sxs-lookup"><span data-stu-id="ad420-217">If you require a specific port in the public Internet, be sure to add that port to the ```-DestinationPortRange``` as well.</span></span>

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

<span data-ttu-id="ad420-218">*務必以適合您的部署的詳細資料取代範例中的名稱。*</span><span class="sxs-lookup"><span data-stu-id="ad420-218">*Ensure that you replace the names in the example with the details appropriate to your deployment.*</span></span>

## <a name="vm-agent"></a><span data-ttu-id="ad420-219">VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad420-219">VM agent</span></span>
<span data-ttu-id="ad420-220">備份 Azure 虛擬機器之前，您應該先確定虛擬機器上已正確安裝 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-220">Before you can back up the Azure virtual machine, you should ensure that the Azure VM agent is correctly installed on the virtual machine.</span></span> <span data-ttu-id="ad420-221">由於 VM 代理程式在虛擬機器建立時為選擇性元件，因此佈建虛擬機器之前，請先確定已選取 VM 代理程式的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ad420-221">Since the VM agent is an optional component at the time that the virtual machine is created, ensure that the check box for the VM agent is selected before the virtual machine is provisioned.</span></span>

### <a name="manual-installation-and-update"></a><span data-ttu-id="ad420-222">手動安裝和更新</span><span class="sxs-lookup"><span data-stu-id="ad420-222">Manual installation and update</span></span>
<span data-ttu-id="ad420-223">從 Azure 資源庫建立的 VM 中已經有 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-223">The VM agent is already present in VMs that are created from the Azure gallery.</span></span> <span data-ttu-id="ad420-224">不過，從內部部署資料中心移轉的虛擬機器不會安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-224">However, virtual machines that are migrated from on-premises datacenters would not have the VM agent installed.</span></span> <span data-ttu-id="ad420-225">對於這類 VM，必須明確安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-225">For such VMs, the VM agent needs to be installed explicitly.</span></span> <span data-ttu-id="ad420-226">深入了解 [在現有 VM 上安裝 VM 代理程式](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad420-226">Read more about [installing the VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span></span>

| <span data-ttu-id="ad420-227">**作業**</span><span class="sxs-lookup"><span data-stu-id="ad420-227">**Operation**</span></span> | <span data-ttu-id="ad420-228">**Windows**</span><span class="sxs-lookup"><span data-stu-id="ad420-228">**Windows**</span></span> | <span data-ttu-id="ad420-229">**Linux**</span><span class="sxs-lookup"><span data-stu-id="ad420-229">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad420-230">安裝 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad420-230">Installing the VM agent</span></span> |<li><span data-ttu-id="ad420-231">下載並安裝 [代理程式 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="ad420-231">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="ad420-232">您需要有系統管理員權限，才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="ad420-232">You will need Administrator privileges to complete the installation.</span></span> <li><span data-ttu-id="ad420-233">[更新 VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 以表示已安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-233">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |<li> <span data-ttu-id="ad420-234">從 GitHub 安裝最新的 [Linux 代理程式](https://github.com/Azure/WALinuxAgent) 。</span><span class="sxs-lookup"><span data-stu-id="ad420-234">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="ad420-235">您需要有系統管理員權限，才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="ad420-235">You will need Administrator privileges to complete the installation.</span></span> <li> <span data-ttu-id="ad420-236">[更新 VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 以表示已安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="ad420-236">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |
| <span data-ttu-id="ad420-237">更新 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad420-237">Updating the VM agent</span></span> |<span data-ttu-id="ad420-238">更新 VM 代理程式與重新安裝 [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="ad420-238">Updating the VM agent is as simple as reinstalling the [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><br><span data-ttu-id="ad420-239">確定在更新 VM 代理程式時，沒有任何執行中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="ad420-239">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |<span data-ttu-id="ad420-240">請遵循[更新 Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)上的指示。</span><span class="sxs-lookup"><span data-stu-id="ad420-240">Follow the instructions on [updating the Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><br><span data-ttu-id="ad420-241">確定在更新 VM 代理程式時，沒有任何執行中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="ad420-241">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |
| <span data-ttu-id="ad420-242">驗證 VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="ad420-242">Validating the VM agent installation</span></span> |<li><span data-ttu-id="ad420-243">瀏覽至 Azure VM 中的 C:\WindowsAzure\Packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ad420-243">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span></span> <li><span data-ttu-id="ad420-244">您應該會發現 WaAppAgent.exe 檔案已存在。</span><span class="sxs-lookup"><span data-stu-id="ad420-244">You should find the WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="ad420-245">在該檔案上按一下滑鼠右鍵，前往 [屬性]，然後選取 [詳細資料] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ad420-245">Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="ad420-246">[產品版本] 欄位應為 2.6.1198.718 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ad420-246">The Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="ad420-247">N/A</span><span class="sxs-lookup"><span data-stu-id="ad420-247">N/A</span></span> |

<span data-ttu-id="ad420-248">深入了解 [VM 代理程式](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409)和[如何安裝](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)。</span><span class="sxs-lookup"><span data-stu-id="ad420-248">Learn about the [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span></span>

### <a name="backup-extension"></a><span data-ttu-id="ad420-249">備份擴充功能</span><span class="sxs-lookup"><span data-stu-id="ad420-249">Backup extension</span></span>
<span data-ttu-id="ad420-250">為了備份虛擬機器，「Azure 備份」服務會安裝 VM 代理程式的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ad420-250">To back up the virtual machine, the Azure Backup service installs an extension to the VM agent.</span></span> <span data-ttu-id="ad420-251">Azure 備份服務無需使用者介入，即可順暢地升級和修補備份擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ad420-251">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span></span>

<span data-ttu-id="ad420-252">如果 VM 正在執行，表示已安裝備份擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ad420-252">The backup extension is installed if the VM is running.</span></span> <span data-ttu-id="ad420-253">執行中的 VM 也提供了取得應用程式一致復原點的絕佳機會。</span><span class="sxs-lookup"><span data-stu-id="ad420-253">A running VM also provides the greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="ad420-254">不過，即使 VM 已關閉而無法安裝擴充功能 (亦稱為離線 VM)，「Azure 備份」服務仍會繼續備份 VM。</span><span class="sxs-lookup"><span data-stu-id="ad420-254">However, the Azure Backup service will continue to back up the VM--even if it is turned off, and the extension could not be installed (aka Offline VM).</span></span> <span data-ttu-id="ad420-255">在此情況下，復原點將如前面所述為「當機時保持一致」  。</span><span class="sxs-lookup"><span data-stu-id="ad420-255">In this case, the recovery point will be *crash consistent* as discussed above.</span></span>

## <a name="questions"></a><span data-ttu-id="ad420-256">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="ad420-256">Questions?</span></span>
<span data-ttu-id="ad420-257">如果您有問題，或希望我們加入任何功能，請 [傳送意見反應給我們](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="ad420-257">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad420-258">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad420-258">Next steps</span></span>
<span data-ttu-id="ad420-259">您現在已經備妥環境來備份您的 VM，您的下一個邏輯步驟是建立備份。</span><span class="sxs-lookup"><span data-stu-id="ad420-259">Now that you have prepared your environment for backing up your VM, your next logical step is to create a backup.</span></span> <span data-ttu-id="ad420-260">規劃文章會提供備份 VM 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ad420-260">The planning article provides more detailed information about backing up VMs.</span></span>

* [<span data-ttu-id="ad420-261">備份虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ad420-261">Back up virtual machines</span></span>](backup-azure-vms.md)
* [<span data-ttu-id="ad420-262">規劃 VM 備份基礎結構</span><span class="sxs-lookup"><span data-stu-id="ad420-262">Plan your VM backup infrastructure</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="ad420-263">管理虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="ad420-263">Manage virtual machine backups</span></span>](backup-azure-manage-vms.md)
