---
title: "aaaPrepare 機器 tooset 之間移轉 tooAzure 使用站台復原後的 Azure 地區的災害復原 |Microsoft 文件"
description: "本文說明如何 tooprepare 機器 tooset 之間之後移轉 tooAzure 使用 Azure Site Recovery 的 Azure 地區的災害復原。"
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
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="cbe0a-103">使用 Azure Site Recovery 將 Azure Vm tooanother 區域複寫之後移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="cbe0a-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="cbe0a-104">Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="cbe0a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="cbe0a-105">Overview</span></span>

<span data-ttu-id="cbe0a-106">這篇文章可協助您準備這些機器已從內部部署環境 tooAzure 移轉使用 Azure 站台復原後的兩個 Azure 區域間複寫的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="cbe0a-107">災害復原和合規性</span><span class="sxs-lookup"><span data-stu-id="cbe0a-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="cbe0a-108">現在，越來越多企業要移動其工作負載 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="cbe0a-109">移動內部任務關鍵性生產環境的企業工作負載 tooAzure，設定這些工作負載的災害復原是必要的符合性與 toosafeguard 對 Azure 的區域中的任何干擾。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="cbe0a-110">準備移轉後的機器以進行複寫的步驟</span><span class="sxs-lookup"><span data-stu-id="cbe0a-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="cbe0a-111">tooprepare 移轉機器的複寫 tooanother Azure 地區設定：</span><span class="sxs-lookup"><span data-stu-id="cbe0a-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="cbe0a-112">完成移轉。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-112">Complete migration.</span></span>
2. <span data-ttu-id="cbe0a-113">安裝 Azure 代理程式視 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="cbe0a-114">移除 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="cbe0a-115">重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-115">Restart hello VM.</span></span>

<span data-ttu-id="cbe0a-116">在 hello 下列各節中詳細說明這些步驟。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="cbe0a-117">步驟 1： 移轉 HYPER-V Vm、 VMware Vm 和 Azure Vm 上的實體伺服器 toorun 上執行的工作負載</span><span class="sxs-lookup"><span data-stu-id="cbe0a-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="cbe0a-118">tooset 複寫並移轉您在內部部署 HYPER-V 和 VMware 及實體工作負載 tooAzure 後續 hello 中的步驟 hello[移轉 Azure IaaS 虛擬機器與 Azure Site Recovery 的 Azure 區域之間](site-recovery-migrate-to-azure.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="cbe0a-119">移轉之後，您不需要 toocommit 或刪除容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="cbe0a-120">相反地，選取 hello**完成移轉**選項要為每一部機器 toomigrate:</span><span class="sxs-lookup"><span data-stu-id="cbe0a-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="cbe0a-121">在**複寫的項目**，以滑鼠右鍵按一下 hello VM，然後按一下**完成移轉**。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="cbe0a-122">按一下**確定**toocomplete hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="cbe0a-123">您可以藉由監視 hello 完成移轉作業中的追蹤 hello VM 屬性中的進度**站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="cbe0a-124">hello**完成移轉**動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止 hello 機器的 Site Recovery 計費。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="cbe0a-126">步驟 2: Hello 虛擬機器上安裝 hello Azure VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="cbe0a-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="cbe0a-127">hello Azure [VM 代理程式](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux)必須 hello 虛擬機器上安裝的 hello Site Recovery 延伸 toowork 和 toohelp 保護 hello VM。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cbe0a-128">開頭為 Windows 虛擬機器上的版本 9.7.0.0，hello 行動服務安裝程式也會安裝 hello 最新可用 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="cbe0a-129">在移轉，hello 虛擬機器符合必要條件使用任何 VM 擴充功能，包括 hello Site Recovery 擴充功能的代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="cbe0a-130">hello Azure VM 代理程式需求 toobe 手動安裝 hello hello 上安裝行動服務移轉的機器時，才是 9.6 或更早版本。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="cbe0a-131">hello 下表提供有關安裝 hello VM 代理程式和驗證已安裝的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="cbe0a-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="cbe0a-132">**作業**</span><span class="sxs-lookup"><span data-stu-id="cbe0a-132">**Operation**</span></span> | <span data-ttu-id="cbe0a-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="cbe0a-133">**Windows**</span></span> | <span data-ttu-id="cbe0a-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="cbe0a-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbe0a-135">Hello VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="cbe0a-135">Installing hello VM agent</span></span> |<span data-ttu-id="cbe0a-136">下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="cbe0a-137">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="cbe0a-138">安裝最新的 hello [Linux 代理程式](../virtual-machines/linux/agent-user-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="cbe0a-139">您需要系統管理員權限 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="cbe0a-140">我們建議您發佈的儲存機制從安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="cbe0a-141">我們*不建議*直接從 GitHub 安裝 hello Linux VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="cbe0a-142">正在驗證 hello VM 代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="cbe0a-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="cbe0a-143">1.瀏覽 toohello C:\WindowsAzure\Packages 資料夾 hello Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="cbe0a-144">您應該會看見 hello WaAppAgent.exe 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="cbe0a-145">2.以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，，然後選取 [hello**詳細資料**] 索引標籤 hello**產品版本**欄位應該是 2.6.1198.718 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="cbe0a-146">N/A</span><span class="sxs-lookup"><span data-stu-id="cbe0a-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="cbe0a-147">步驟 3： 移除 hello hello 從行動服務移轉的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cbe0a-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="cbe0a-148">如果您已移轉您的內部部署 VMware 機器或實體 Windows/Linux 上的伺服器，您需要從 hello 已移轉的虛擬機器 toomanually 移除/解除安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cbe0a-149">這個步驟不需要 HYPER-V Vm 移轉 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="cbe0a-150">解除安裝 Windows Server VM 上的 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="cbe0a-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="cbe0a-151">使用其中一個 Windows Server 電腦上遵循方法 toouninstall hello 行動服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="cbe0a-152">使用 hello Windows UI 解除安裝</span><span class="sxs-lookup"><span data-stu-id="cbe0a-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="cbe0a-153">在 hello 控制台中，選取 **程式**。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="cbe0a-154">選取 [Microsoft Azure Site Recovery Mobility Service/主要目標伺服器]，然後選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="cbe0a-155">在命令提示字元中解除安裝</span><span class="sxs-lookup"><span data-stu-id="cbe0a-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="cbe0a-156">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="cbe0a-157">toouninstall hello 行動服務，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe0a-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="cbe0a-158">解除安裝 hello Linux 電腦上的行動服務</span><span class="sxs-lookup"><span data-stu-id="cbe0a-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="cbe0a-159">在 Linux 伺服器上，以 **root** 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="cbe0a-160">在終端機中，移太/使用者/本機/ASR。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="cbe0a-161">toouninstall hello 行動服務，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe0a-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="cbe0a-162">步驟 4： 重新啟動 VM hello</span><span class="sxs-lookup"><span data-stu-id="cbe0a-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="cbe0a-163">您解除安裝 hello 行動服務後，才能重新啟動 hello VM 設定複寫 tooanother Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cbe0a-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbe0a-164">Next steps</span></span>
- <span data-ttu-id="cbe0a-165">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="cbe0a-166">深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe0a-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
