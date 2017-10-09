---
title: "aaaReplicate hello 傳統入口網站中使用 PowerShell 的 HYPER-V Vm tooAzure |Microsoft 文件"
description: "自動化 hello hello 傳統入口網站中使用站台復原和 PowerShell 的 VMM 雲端中 HYPER-V 虛擬機器的複寫"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="6937b-103">使用 PowerShell 的 HYPER-V Vm tooAzure hello 傳統入口網站中的複寫</span><span class="sxs-lookup"><span data-stu-id="6937b-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6937b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6937b-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="6937b-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="6937b-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="6937b-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="6937b-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="6937b-107">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="6937b-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="6937b-108">概觀</span><span class="sxs-lookup"><span data-stu-id="6937b-108">Overview</span></span>
<span data-ttu-id="6937b-109">Azure Site Recovery 提供 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調複寫、 容錯移轉和復原的虛擬機器中部署案例的數目。</span><span class="sxs-lookup"><span data-stu-id="6937b-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="6937b-110">如需完整的部署案例請參閱 hello [Azure 站台復原概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6937b-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="6937b-111">本文章將示範如何 toouse PowerShell tooautomate 一般工作時，您需要 tooperform 您設定 Azure Site Recovery tooreplicate HYPER-V 虛擬機器在 System Center VMM 雲端 tooAzure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="6937b-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="6937b-112">hello 文章包含 hello 案例中，並顯示您如何註冊 Site Recovery 保存庫 tooset 安裝 hello hello 來源 VMM 伺服器上的 Azure Site Recovery Provider 的必要條件、 hello 保存庫中註冊伺服器 hello、 新增 Azure 儲存體帳戶、 安裝 hello Azure復原服務代理程式在 HYPER-V 主機伺服器，設定會套用的 tooall 受保護的虛擬機器，並再啟用保護這些虛擬機器的 VMM 雲端的保護設定。</span><span class="sxs-lookup"><span data-stu-id="6937b-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="6937b-113">完成的測試 hello 容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="6937b-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="6937b-114">如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="6937b-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="6937b-115">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6937b-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6937b-116">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6937b-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="6937b-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="6937b-117">Before you start</span></span>
<span data-ttu-id="6937b-118">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="6937b-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="6937b-119">Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="6937b-119">Azure prerequisites</span></span>
* <span data-ttu-id="6937b-120">您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937b-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="6937b-121">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="6937b-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6937b-122">您將需要 Azure 儲存體帳戶 toostore 複寫資料。</span><span class="sxs-lookup"><span data-stu-id="6937b-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="6937b-123">hello 帳戶必須啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="6937b-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="6937b-124">它應該會在 hello 與 hello Azure Site Recovery 保存庫相同的區域，並且與相關聯 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937b-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="6937b-125">[深入了解 Azure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6937b-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="6937b-126">您必須確定您想 tooprotect 虛擬機器符合 toomake [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="6937b-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="6937b-127">VMM 必要條件</span><span class="sxs-lookup"><span data-stu-id="6937b-127">VMM prerequisites</span></span>
* <span data-ttu-id="6937b-128">您將需要在 System Center 2012 R2 上執行的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6937b-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="6937b-129">您必須在 hello 想 tooprotect VMM 伺服器上的至少一個雲端。</span><span class="sxs-lookup"><span data-stu-id="6937b-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="6937b-130">hello 雲端應包含：</span><span class="sxs-lookup"><span data-stu-id="6937b-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="6937b-131">一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="6937b-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="6937b-132">每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。</span><span class="sxs-lookup"><span data-stu-id="6937b-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="6937b-133">一或多個虛擬機器 hello 來源 HYPER-V 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="6937b-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="6937b-134">Hyper-V 的必要條件</span><span class="sxs-lookup"><span data-stu-id="6937b-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="6937b-135">hello HYPER-V 主機伺服器必須執行至少**Windows Server 2012**與 HYPER-V 角色或**Microsoft HYPER-V Server 2012**和擁有 hello 安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="6937b-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="6937b-136">如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="6937b-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="6937b-137">您以手動方式將需要 tooconfigure hello 叢集代理人。</span><span class="sxs-lookup"><span data-stu-id="6937b-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="6937b-138">toodo 這在 伺服器管理員 > 連接 toohello 叢集容錯移轉叢集管理員 中，按一下**設定角色**選取**HYPER-V 複本代理人**在 hello**選取角色**hello 高可用性精靈 的螢幕。</span><span class="sxs-lookup"><span data-stu-id="6937b-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="6937b-139">必須包含任何 HYPER-V 主機伺服器或叢集，您會想 toomanage 保護 VMM 雲端中。</span><span class="sxs-lookup"><span data-stu-id="6937b-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="6937b-140">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="6937b-140">Network mapping prerequisites</span></span>
<span data-ttu-id="6937b-141">當您保護 Azure 網路對應中的虛擬機器 hello 來源 VMM 伺服器上的 VM 網路和目標 Azure 網路 tooenable hello 下列之間進行對應：</span><span class="sxs-lookup"><span data-stu-id="6937b-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="6937b-142">容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，無論它們是在復原計劃。</span><span class="sxs-lookup"><span data-stu-id="6937b-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="6937b-143">如果網路閘道 hello 目標 Azure 網路上的安裝程式，虛擬機器可以連接 tooother 在內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6937b-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="6937b-144">如果您未設定網路對應，只有容錯移轉 hello 中相同的虛擬機器容錯移轉 tooAzure 後，即可能 tooconnect tooeach 其他復原方案。</span><span class="sxs-lookup"><span data-stu-id="6937b-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="6937b-145">如果您想 toodeploy 網路對應，您將需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="6937b-146">hello 想 tooprotect hello 來源 VMM 伺服器上的虛擬機器應連接的 tooa VM 網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="6937b-147">該網路應連結的 tooa hello 雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="6937b-148">Azure 網路 toowhich 複寫虛擬機器可以容錯移轉之後連接。</span><span class="sxs-lookup"><span data-stu-id="6937b-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="6937b-149">在 hello 容錯移轉期間，會選取此網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="6937b-150">hello 網路應位於 hello 與 Azure Site Recovery 訂用帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="6937b-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="6937b-151">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="6937b-151">PowerShell prerequisites</span></span>
<span data-ttu-id="6937b-152">請確定您具有 Azure PowerShell 準備 toogo。</span><span class="sxs-lookup"><span data-stu-id="6937b-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="6937b-153">如果您已經使用 PowerShell，您將需要 tooupgrade tooversion 0.8.10 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6937b-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="6937b-154">PowerShell 設定的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="6937b-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="6937b-155">一旦您已安裝並設定 PowerShell，您可以檢視所有 hello 可用的 hello 服務 cmdlet[這裡](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6937b-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="6937b-156">toolearn 的相關技巧，可協助您使用 hello cmdlet，例如如何參數值、 輸入和輸出通常處理 Azure PowerShell，請參閱[開始使用 Azure Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="6937b-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="6937b-157">步驟 1： 設定 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6937b-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="6937b-158">在 PowerShell 中，執行這些 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="6937b-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="6937b-159">Hello hello"< > 」 中的項目取代為您的專屬資訊。</span><span class="sxs-lookup"><span data-stu-id="6937b-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="6937b-160">步驟 2：建立 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="6937b-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="6937b-161">在 PowerShell 中，您的專屬資訊，以取代 hello hello"< > 」 中的項目，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6937b-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="6937b-162">步驟 3：產生保存庫註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="6937b-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="6937b-163">Hello 保存庫中產生註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="6937b-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="6937b-164">您下載 hello Azure Site Recovery Provider，並將它安裝在 hello VMM 伺服器之後，您將使用此索引鍵 tooregister hello VMM 伺服器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="6937b-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="6937b-165">取得 hello 保存庫設定檔，並設定 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="6937b-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="6937b-166">執行下列命令的 hello 設定 hello 保存庫的內容：</span><span class="sxs-lookup"><span data-stu-id="6937b-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="6937b-167">步驟 4： 安裝 hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="6937b-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="6937b-168">Hello VMM 在電腦上，執行下列命令的 hello 建立目錄：</span><span class="sxs-lookup"><span data-stu-id="6937b-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="6937b-169">擷取使用 hello 下載提供者藉由執行下列命令的 hello hello 檔案</span><span class="sxs-lookup"><span data-stu-id="6937b-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="6937b-170">安裝 hello 提供者使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6937b-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="6937b-171">等候 hello 安裝 toofinish。</span><span class="sxs-lookup"><span data-stu-id="6937b-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="6937b-172">使用下列命令的 hello hello 保存庫中註冊伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="6937b-173">步驟 5：建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6937b-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="6937b-174">如果您沒有 Azure 儲存體帳戶，請執行下列命令的 hello 建立啟用地理複寫帳戶：</span><span class="sxs-lookup"><span data-stu-id="6937b-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="6937b-175">請注意，hello 儲存體帳戶必須在 hello 與 hello Azure Site Recovery 服務相同的區域和與其相關聯 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6937b-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="6937b-176">步驟 6： 安裝 Azure Recovery Services Agent hello</span><span class="sxs-lookup"><span data-stu-id="6937b-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="6937b-177">Hello Azure 入口網站位於 hello VMM 雲端中每部 HYPER-V 主機伺服器上安裝 hello Azure 復原服務代理程式從您想 tooprotect。</span><span class="sxs-lookup"><span data-stu-id="6937b-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="6937b-178">執行下列命令，在所有 VMM 主機上的 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="6937b-179">步驟 7：設定雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="6937b-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="6937b-180">建立雲端保護設定檔 tooAzure 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="6937b-181">藉由執行下列命令的 hello 取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="6937b-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="6937b-182">開始 hello 雲端中的 hello hello 保護容器的關聯：</span><span class="sxs-lookup"><span data-stu-id="6937b-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="6937b-183">Hello 工作已完成之後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="6937b-184">Hello 作業已完成處理之後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-184">After hello job has finished processing, run hello following command:</span></span>

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



<span data-ttu-id="6937b-185">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="6937b-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="6937b-186">步驟 8：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="6937b-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="6937b-187">開始之前請確認網路對應 hello 來源 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="6937b-188">此外，請建立一或多個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="6937b-189">請注意，多個 VM 網路可以是對應的 tooa 單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="6937b-190">附註是否 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 是相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="6937b-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="6937b-191">如果沒有具有相符名稱的目標子網路，hello 虛擬機器將會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="6937b-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="6937b-192">hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6937b-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="6937b-193">hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。</span><span class="sxs-lookup"><span data-stu-id="6937b-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="6937b-194">hello 第二個命令會取得 hello hello 第一部伺服器的站台復原網路 hello $Servers 陣列中。</span><span class="sxs-lookup"><span data-stu-id="6937b-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="6937b-195">hello 命令儲存 hello 網路 hello $Networks 變數中。</span><span class="sxs-lookup"><span data-stu-id="6937b-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="6937b-196">hello 第三個命令會取得您的 Azure 訂用帳戶使用 hello Get-azuresubscription cmdlet，然後將該值儲存 hello $Subscriptions 變數。</span><span class="sxs-lookup"><span data-stu-id="6937b-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="6937b-197">hello 第四個命令會取得 Azure 虛擬網路使用 hello Get AzureVNetSite cmdlet，然後該值 hello $AzureVmNetworks 變數中。</span><span class="sxs-lookup"><span data-stu-id="6937b-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="6937b-198">hello 最終 cmdlet 會建立 hello 主要網路與 hello Azure 虛擬機器網路之間的對應。</span><span class="sxs-lookup"><span data-stu-id="6937b-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="6937b-199">hello 指令程式會指定 hello 主要網路作為 $Networks hello 第一個項目。</span><span class="sxs-lookup"><span data-stu-id="6937b-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="6937b-200">hello cmdlet 指定 $AzureVmNetworks hello 第一個項目為虛擬機器網路，使用其識別碼。</span><span class="sxs-lookup"><span data-stu-id="6937b-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="6937b-201">hello 命令包含您的 Azure 訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="6937b-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="6937b-202">步驟 9：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="6937b-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="6937b-203">伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="6937b-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="6937b-204">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6937b-204">Note hello following:</span></span>

<span data-ttu-id="6937b-205">虛擬機器必須符合 [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="6937b-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="6937b-206">tooenable 保護 hello 作業系統和作業系統磁碟屬性必須設定為 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6937b-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="6937b-207">當您在 VMM 使用虛擬機器範本中建立虛擬機器時，您可以設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6937b-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="6937b-208">您也可以設定這些屬性的現有虛擬機器上 hello**一般**和**硬體組態**hello 虛擬機器內容 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6937b-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="6937b-209">如果您不需要在 VMM 中設定這些屬性，您將必須能夠 tooconfigure hello Azure Site Recovery 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6937b-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="6937b-210">tooenable 保護，執行下列命令 tooget hello 保護容器 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="6937b-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="6937b-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="6937b-212">取得 hello 保護實體 (VM) 執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6937b-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="6937b-213">執行下列命令的 hello 啟用 hello DR hello VM:</span><span class="sxs-lookup"><span data-stu-id="6937b-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="6937b-214">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="6937b-214">Test your deployment</span></span>
<span data-ttu-id="6937b-215">tootest 規劃您的部署，您可以執行測試容錯移轉的單一虛擬機器，或建立復原方案包含多個虛擬機器並執行測試容錯移轉的 hello。</span><span class="sxs-lookup"><span data-stu-id="6937b-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="6937b-216">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="6937b-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="6937b-217">請注意：</span><span class="sxs-lookup"><span data-stu-id="6937b-217">Note that:</span></span>

* <span data-ttu-id="6937b-218">如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。</span><span class="sxs-lookup"><span data-stu-id="6937b-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="6937b-219">容錯移轉之後，您將使用遠端桌面在 Azure 中使用公用 IP 位址 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6937b-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="6937b-220">如果您希望 toodo 如此，請確定您沒有任何網域原則，讓您無法使用的公用位址的連接 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6937b-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="6937b-221">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="6937b-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="6937b-222">建立復原計畫</span><span class="sxs-lookup"><span data-stu-id="6937b-222">Create a recovery plan</span></span>
1. <span data-ttu-id="6937b-223">做為範本使用 hello 資料，復原方案中建立的.xml 檔，然後將它儲存為"C:\RPTemplatePath.xml"。</span><span class="sxs-lookup"><span data-stu-id="6937b-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="6937b-224">Hello RecoveryPlan 節點識別碼、 名稱、 PrimaryServerId 和 SecondaryServerId 變更。</span><span class="sxs-lookup"><span data-stu-id="6937b-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="6937b-225">Hello ProtectionEntity 節點 PrimaryProtectionEntityId （vmid，可從 VMM） 的變更。</span><span class="sxs-lookup"><span data-stu-id="6937b-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="6937b-226">您可以新增更多 ProtectionEntity 節點來新增更多 VM。</span><span class="sxs-lookup"><span data-stu-id="6937b-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="6937b-227">填入 hello hello 範本中的資料：</span><span class="sxs-lookup"><span data-stu-id="6937b-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="6937b-228">建立 hello RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="6937b-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="6937b-229">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="6937b-229">Run a test failover</span></span>
1. <span data-ttu-id="6937b-230">藉由執行下列命令的 hello 收到 hello RecoveryPlan 物件：</span><span class="sxs-lookup"><span data-stu-id="6937b-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="6937b-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="6937b-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="6937b-232">執行下列命令的 hello 啟動 hello 測試容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="6937b-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="6937b-233"><a name=monitor></a>監視活動</span><span class="sxs-lookup"><span data-stu-id="6937b-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="6937b-234">使用下列命令 toomonitor hello 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="6937b-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="6937b-235">請注意，您 toowait 之間 hello 處理 toofinish 的作業。</span><span class="sxs-lookup"><span data-stu-id="6937b-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="6937b-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6937b-236">Next steps</span></span>
<span data-ttu-id="6937b-237">[閱讀更多](/powershell/azure/overview) Azure Site Recovery PowerShell Cmdlet 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6937b-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="6937b-238"></a>。</span><span class="sxs-lookup"><span data-stu-id="6937b-238"></a>.</span></span>
