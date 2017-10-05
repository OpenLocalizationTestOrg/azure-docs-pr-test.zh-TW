---
title: "準備機器，在使用 Site Recovery 移轉至 Azure 後，設定 Azure 之間的災害復原 | Microsoft Docs"
description: "本文說明如何準備機器，以在使用 Azure Site Recovery 移轉至 Azure 後，設定 Azure 區域之間的災害復原。"
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="8debe-103">使用 Azure Site Recovery 移轉至 Azure 後，將 Azure VM 複寫至另一個區域</span><span class="sxs-lookup"><span data-stu-id="8debe-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="8debe-104">Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="8debe-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="8debe-105">概觀</span><span class="sxs-lookup"><span data-stu-id="8debe-105">Overview</span></span>

<span data-ttu-id="8debe-106">本文可協助您準備 Azure 虛擬機器，在利用 Azure Site Recovery 從內部部署環境將這些機器移轉到 Azure 後，進行兩個 Azure 區域之間的複寫。</span><span class="sxs-lookup"><span data-stu-id="8debe-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="8debe-107">災害復原和合規性</span><span class="sxs-lookup"><span data-stu-id="8debe-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="8debe-108">現在，越來越多企業將其工作負載移轉到 Azure。</span><span class="sxs-lookup"><span data-stu-id="8debe-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="8debe-109">隨著企業將任務關鍵性內部部署生產工作負載移轉到 Azure，必須對於這些工作負載設定災害復原，才能達到合規性並防範 Azure 區域的任何干擾。</span><span class="sxs-lookup"><span data-stu-id="8debe-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="8debe-110">準備移轉後的機器以進行複寫的步驟</span><span class="sxs-lookup"><span data-stu-id="8debe-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="8debe-111">若要準備移轉後的機器以設定複寫到另一個 Azure 區域：</span><span class="sxs-lookup"><span data-stu-id="8debe-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="8debe-112">完成移轉。</span><span class="sxs-lookup"><span data-stu-id="8debe-112">Complete migration.</span></span>
2. <span data-ttu-id="8debe-113">視需要安裝 Azure 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8debe-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="8debe-114">移除行動服務。</span><span class="sxs-lookup"><span data-stu-id="8debe-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="8debe-115">重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="8debe-115">Restart the VM.</span></span>

<span data-ttu-id="8debe-116">這些步驟將於下列各節中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="8debe-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="8debe-117">步驟 1：將在 Hyper-V VM、VMware VM 和實體伺服器上執行的工作負載，移轉到 Azure VM 上來執行</span><span class="sxs-lookup"><span data-stu-id="8debe-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="8debe-118">若要設定複寫，並將內部部署 Hyper-V、 VMware 和實體工作負載移轉至 Azure，請依照[使用 Azure Site Recovery 在 Azure 區域之間移轉 Azure IaaS 虛擬機器](site-recovery-migrate-to-azure.md)文章中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="8debe-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="8debe-119">移轉後，您不需要認可或刪除容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8debe-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="8debe-120">相反地，請為您要移轉的每一部機器選取 [完成移轉] 選項：</span><span class="sxs-lookup"><span data-stu-id="8debe-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="8debe-121">在 [複寫的項目] 中，以滑鼠右鍵按一下 VM，然後按一下 [完成移轉]。</span><span class="sxs-lookup"><span data-stu-id="8debe-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="8debe-122">按一下 [確定] 完成步驟。</span><span class="sxs-lookup"><span data-stu-id="8debe-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="8debe-123">您可以在 [Site Recovery 作業] 中監視 [完成移轉] 作業，以在 VM 屬性中追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="8debe-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="8debe-124">**完成移轉**動作會完成移轉程序、移除機器的複寫，並停止該機器的 Site Recovery 計費。</span><span class="sxs-lookup"><span data-stu-id="8debe-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="8debe-126">步驟 2：在虛擬機器中安裝 Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="8debe-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="8debe-127">Azure [VM 代理程式](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)必須安裝在虛擬機器上，站台復原擴充功能才能運作，並協助保護 VM。</span><span class="sxs-lookup"><span data-stu-id="8debe-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8debe-128">從版本 9.7.0.0 開始，在 Windows 虛擬機器上，行動服務安裝程式也會安裝最新可用的 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8debe-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="8debe-129">在移轉時，虛擬機器符合使用任何 VM 擴充功能的代理程式安裝必要條件，包括 Site Recovery 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8debe-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="8debe-130">移轉後的機器上安裝的行動服務是 9.6 或更早版本時，才需要手動安裝 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8debe-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="8debe-131">下表提供安裝 VM 代理程式和驗證已安裝所需的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="8debe-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="8debe-132">**作業**</span><span class="sxs-lookup"><span data-stu-id="8debe-132">**Operation**</span></span> | <span data-ttu-id="8debe-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="8debe-133">**Windows**</span></span> | <span data-ttu-id="8debe-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="8debe-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8debe-135">安裝 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="8debe-135">Installing the VM agent</span></span> |<span data-ttu-id="8debe-136">下載並安裝 [代理程式 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="8debe-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="8debe-137">您需要有系統管理員權限，才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="8debe-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="8debe-138">安裝最新的 [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="8debe-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="8debe-139">您需要有系統管理員權限，才能完成安裝。</span><span class="sxs-lookup"><span data-stu-id="8debe-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="8debe-140">我們建議您從散發儲存機制安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="8debe-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="8debe-141">我們「不建議」您直接從 Github 安裝 Linux VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8debe-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="8debe-142">驗證 VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="8debe-142">Validating the VM agent installation</span></span> |<span data-ttu-id="8debe-143">1.瀏覽至 Azure VM 中的 C:\WindowsAzure\Packages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8debe-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="8debe-144">您應該會看見 WaAppAgent.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="8debe-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="8debe-145">2.在該檔案上按一下滑鼠右鍵，前往 [屬性]，然後選取 [詳細資料] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8debe-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="8debe-146">[產品版本] 欄位應為 2.6.1198.718 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="8debe-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="8debe-147">N/A</span><span class="sxs-lookup"><span data-stu-id="8debe-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="8debe-148">步驟 3：從移轉後的虛擬機器解除行動服務</span><span class="sxs-lookup"><span data-stu-id="8debe-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="8debe-149">如果您已移轉 Windows/Linux 上的內部部署 VMware 機器或實體伺服器，則需要從移轉後的虛擬機器手動移除/解除安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="8debe-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8debe-150">移轉至 Azure 的 Hyper-V VM 不需要進行此步驟。</span><span class="sxs-lookup"><span data-stu-id="8debe-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="8debe-151">將 Windows Server VM 上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="8debe-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="8debe-152">您可以使用下列其中一種方法將 Windows Server 電腦上的行動服務解除安裝。</span><span class="sxs-lookup"><span data-stu-id="8debe-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="8debe-153">使用 Windows UI 來解除安裝</span><span class="sxs-lookup"><span data-stu-id="8debe-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="8debe-154">在 [控制台] 中，選取 [程式]。</span><span class="sxs-lookup"><span data-stu-id="8debe-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="8debe-155">選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="8debe-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="8debe-156">在命令提示字元中解除安裝</span><span class="sxs-lookup"><span data-stu-id="8debe-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="8debe-157">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8debe-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="8debe-158">執行下列命令以將行動服務解除安裝：</span><span class="sxs-lookup"><span data-stu-id="8debe-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="8debe-159">將 Linux 電腦上的行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="8debe-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="8debe-160">在 Linux 伺服器上，以 **root** 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="8debe-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="8debe-161">在終端機中，移至 /user/local/ASR。</span><span class="sxs-lookup"><span data-stu-id="8debe-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="8debe-162">執行下列命令以將行動服務解除安裝：</span><span class="sxs-lookup"><span data-stu-id="8debe-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="8debe-163">步驟 4：重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="8debe-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="8debe-164">解除安裝行動服務之後，先重新啟動 VM，再設定複寫到另一個 Azure 區域的作業。</span><span class="sxs-lookup"><span data-stu-id="8debe-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8debe-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8debe-165">Next steps</span></span>
- <span data-ttu-id="8debe-166">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="8debe-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="8debe-167">深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="8debe-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
