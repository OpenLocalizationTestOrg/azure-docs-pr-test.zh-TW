---
title: "使用 PowerShell 在傳統入口網站中將 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "在傳統入口網站中使用 Site Recovery 及 PowerShell，將 VMM 雲端中 Hyper-V 虛擬機器的複寫自動化"
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="1fd86-103">在傳統入口網站中使用 PowerShell 將 Hyper-V VM 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="1fd86-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fd86-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1fd86-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="1fd86-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="1fd86-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="1fd86-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="1fd86-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="1fd86-107">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="1fd86-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="1fd86-108">Overview</span><span class="sxs-lookup"><span data-stu-id="1fd86-108">Overview</span></span>
<span data-ttu-id="1fd86-109">Azure Site Recovery 可在一些部署案例中協調虛擬機器的複寫、容錯移轉及復原，為您的商務持續性與災害復原 (BCDR) 做出貢獻。</span><span class="sxs-lookup"><span data-stu-id="1fd86-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="1fd86-110">如需完整的部署案例清單，請參閱 [Azure Site Recovery 概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="1fd86-111">本文說明如何使用 PowerShell 自動化您在設定 Azure Site Recovery 將 System Center VMM 雲端中的 HYPER-V 虛擬機器，複寫到 Azure 儲存體時常需要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="1fd86-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="1fd86-112">本文包含案例的必要條件，並示範如何設定 Site Recovery 保存庫、在來源 VMM 伺服器上安裝 Azure Site Recovery 提供者、在保存庫註冊伺服器、加入 Azure 儲存體帳戶、在 Hyper-V 主機伺服器上安裝 Azure Site Recovery 代理程式、設定將套用到所有受保護虛擬機器之 VMM 雲端的保護設定、然後啟用那些虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="1fd86-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="1fd86-113">測試容錯移轉，確認一切如預期般運作以完成動作。</span><span class="sxs-lookup"><span data-stu-id="1fd86-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="1fd86-114">您在設定此案例如有任何問題，可將問題張貼到 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="1fd86-115">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1fd86-116">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1fd86-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="1fd86-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="1fd86-117">Before you start</span></span>
<span data-ttu-id="1fd86-118">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="1fd86-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="1fd86-119">Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="1fd86-119">Azure prerequisites</span></span>
* <span data-ttu-id="1fd86-120">您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1fd86-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="1fd86-121">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="1fd86-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1fd86-122">您需要 Azure 儲存體帳戶來儲存複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="1fd86-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="1fd86-123">此帳戶必須啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="1fd86-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="1fd86-124">它應該與 Azure Site Recovery 保存庫位於相同的區域，且和同一個訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1fd86-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="1fd86-125">[深入了解 Azure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="1fd86-126">您必須確定您要保護的虛擬機器符合 [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="1fd86-127">VMM 必要條件</span><span class="sxs-lookup"><span data-stu-id="1fd86-127">VMM prerequisites</span></span>
* <span data-ttu-id="1fd86-128">您將需要在 System Center 2012 R2 上執行的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="1fd86-129">在您想要保護的 VMM 伺服器上，您至少需要一個雲端。</span><span class="sxs-lookup"><span data-stu-id="1fd86-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="1fd86-130">這個雲端應該包含：</span><span class="sxs-lookup"><span data-stu-id="1fd86-130">The cloud should contain:</span></span>
  * <span data-ttu-id="1fd86-131">一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="1fd86-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="1fd86-132">每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。</span><span class="sxs-lookup"><span data-stu-id="1fd86-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="1fd86-133">來源 Hyper-V 伺服器上的一或多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="1fd86-134">Hyper-V 的必要條件</span><span class="sxs-lookup"><span data-stu-id="1fd86-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="1fd86-135">Hyper-V 主機伺服器必須至少執行具備 Hyper-V 角色的 **Windows Server 2012** 或 **Microsoft Hyper-V Server 2012** 並已安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="1fd86-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="1fd86-136">如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="1fd86-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="1fd86-137">您必須手動設定叢集代理。</span><span class="sxs-lookup"><span data-stu-id="1fd86-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="1fd86-138">若要執行此作業，請在 [伺服器管理員] > [容錯移轉叢集管理員] 中連接到叢集，按一下 [設定角色]，然後在 [高可用性精靈] 之 [選取角色] 畫面中選取 [Hyper-V 複本代理人]。</span><span class="sxs-lookup"><span data-stu-id="1fd86-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="1fd86-139">您想要管理保護的任何 Hyper-V 主機伺服計或叢集都必須包含在 VMM 雲端中。</span><span class="sxs-lookup"><span data-stu-id="1fd86-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="1fd86-140">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="1fd86-140">Network mapping prerequisites</span></span>
<span data-ttu-id="1fd86-141">當您在 Azure 網路對應中保護虛擬機器，請對應來源 VMM 伺服器上的 VM 網路和目標 Azure 網路，以啟用下列項目：</span><span class="sxs-lookup"><span data-stu-id="1fd86-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="1fd86-142">在相同網路上容錯移轉的所有機器都可以彼此連接，無論它們隸屬於哪個復原計畫都一樣。</span><span class="sxs-lookup"><span data-stu-id="1fd86-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="1fd86-143">如果目標 Azure 網路上已設定網路閘道，則虛擬機器可以連接到其他內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="1fd86-144">如果您未設定網路對應，則只有在相同復原計畫中容錯移轉的虛擬機器才能在容錯移轉到 Azure 之後彼此連接。</span><span class="sxs-lookup"><span data-stu-id="1fd86-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="1fd86-145">如果您想要部署網路對應，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1fd86-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="1fd86-146">您想要在來源 VMM 伺服器上保護的虛擬機器應該連線到 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="1fd86-147">該網路應該連結到與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="1fd86-148">複寫的虛擬機器可在容錯移轉之後連線的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="1fd86-149">您將在容錯移轉時選取此網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="1fd86-150">此網路應該和您的 Azure Site Recovery 訂用帳戶在相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="1fd86-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="1fd86-151">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="1fd86-151">PowerShell prerequisites</span></span>
<span data-ttu-id="1fd86-152">確定 Azure PowerShell 已經準備就緒。</span><span class="sxs-lookup"><span data-stu-id="1fd86-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="1fd86-153">如果您已經使用 PowerShell，您必須升級至 0.8.10 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1fd86-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="1fd86-154">如需設定 PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="1fd86-155">一旦已安裝並設定 PowerShell，您可以檢視 [這裡](/powershell/azure/overview)之服務的所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1fd86-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="1fd86-156">如需深入了解可協助您使用這些 Cmdlet 的提示 (例如參數值、輸入及輸出在 Azure PowerShell 中的處理方式)，請參閱 [Azure Cmdlet 使用者入門](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="1fd86-157">步驟 1：設定訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1fd86-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="1fd86-158">在 PowerShell 中，執行這些 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="1fd86-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="1fd86-159">以您的特定資訊取代 "< >" 中的元素。</span><span class="sxs-lookup"><span data-stu-id="1fd86-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="1fd86-160">步驟 2：建立 Site Recovery 保存庫</span><span class="sxs-lookup"><span data-stu-id="1fd86-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="1fd86-161">在 PowerShell 中，將 "< >" 裡面的元素取代成您的特定資訊，然後執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="1fd86-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="1fd86-162">步驟 3：產生保存庫註冊金鑰</span><span class="sxs-lookup"><span data-stu-id="1fd86-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="1fd86-163">在保存庫中產生註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="1fd86-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="1fd86-164">下載 Azure Site Recovery 提供者並將其安裝在 VMM 伺服器之後，您將使用此金鑰在保存庫中註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="1fd86-165">取得保存庫設定檔並設定內容：</span><span class="sxs-lookup"><span data-stu-id="1fd86-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="1fd86-166">執行下列命令來設定保存庫內容：</span><span class="sxs-lookup"><span data-stu-id="1fd86-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="1fd86-167">步驟 4：安裝 Azure Site Recovery 提供者</span><span class="sxs-lookup"><span data-stu-id="1fd86-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="1fd86-168">在 VMM 機器上，執行下列命令來建立目錄：</span><span class="sxs-lookup"><span data-stu-id="1fd86-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="1fd86-169">執行下列命令，使用已下載的提供者將檔案解壓縮</span><span class="sxs-lookup"><span data-stu-id="1fd86-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="1fd86-170">使用下列命令安裝提供者：</span><span class="sxs-lookup"><span data-stu-id="1fd86-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="1fd86-171">等待安裝完成。</span><span class="sxs-lookup"><span data-stu-id="1fd86-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="1fd86-172">使用下列命令在保存庫中註冊伺服器：</span><span class="sxs-lookup"><span data-stu-id="1fd86-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="1fd86-173">步驟 5：建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1fd86-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="1fd86-174">如果您沒有 Azure 儲存體帳戶，請執行下列命令來建立啟用帳戶的異地複寫：</span><span class="sxs-lookup"><span data-stu-id="1fd86-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="1fd86-175">請注意，儲存體帳戶必須與 Azure Site Recovery 服務位於相同的區或，且與相同的訂用帳戶關聯。</span><span class="sxs-lookup"><span data-stu-id="1fd86-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="1fd86-176">步驟 6：安裝 Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="1fd86-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="1fd86-177">從 Azure 入口網站，在 VMM 雲端中您要保護的每一個 Hyper-V 主機伺服器上，安裝 Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="1fd86-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="1fd86-178">在所有 VMM 主機上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="1fd86-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="1fd86-179">步驟 7：設定雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="1fd86-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="1fd86-180">執行下列命令來建立 Azure 的雲端保護設定檔：</span><span class="sxs-lookup"><span data-stu-id="1fd86-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="1fd86-181">執行下列命令以取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="1fd86-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="1fd86-182">啟動與雲端的保護容器關聯：</span><span class="sxs-lookup"><span data-stu-id="1fd86-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="1fd86-183">完成工作之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="1fd86-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="1fd86-184">完成工作處理之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="1fd86-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="1fd86-185">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="1fd86-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="1fd86-186">步驟 8：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="1fd86-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="1fd86-187">開始網路對應之前，請確認來源 VMM 伺服器上的虛擬機器已連線到 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="1fd86-188">此外，請建立一或多個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="1fd86-189">請注意，多個 VM 網路可對應至單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="1fd86-190">請注意，如果目標網路具有多個子網路，且其中一個子網路的名稱和來源虛擬機器所在之子網路名稱相同，複本虛擬機器將會在容錯移轉之後連線到該目標子網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="1fd86-191">如果沒有目標子網路具有相符的名稱，虛擬機器將會連線到網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="1fd86-192">第一個命令會取得目前的 Azure Site Recovery 保存庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="1fd86-193">命令會將 Microsoft Azure Site Recovery 伺服器儲存在 $Servers 陣列變數。</span><span class="sxs-lookup"><span data-stu-id="1fd86-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="1fd86-194">第二個命令會取得 $Servers 陣列中第一部伺服器的站台復原網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="1fd86-195">此命令會在 $Networks 變數中儲存網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="1fd86-196">第三個命令使用 Get-AzuresubScription Cmdlet 取得 Azure 訂用帳戶，然後再將該值儲存在 $Subscriptions 變數中。</span><span class="sxs-lookup"><span data-stu-id="1fd86-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="1fd86-197">第四個命令會使用 Get-AzureVNetSite Cmdlet，然後是 $AzureVmNetworks 變數中的該值來取得 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1fd86-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="1fd86-198">最終的 Cmdlet 會在主要網路與 Azure 虛擬機器網路之間建立對應。</span><span class="sxs-lookup"><span data-stu-id="1fd86-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="1fd86-199">Cmdlet 會將主要網路指定為 $Networks 的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="1fd86-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="1fd86-200">Cmdlet 為使用其識別碼，將虛擬機器網路指定為 $AzureVmNetworks 的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="1fd86-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="1fd86-201">此命令包含您的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1fd86-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="1fd86-202">步驟 9：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="1fd86-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="1fd86-203">正確設定伺服器、雲端和網路後，您就可以對雲端中的虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="1fd86-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="1fd86-204">請注意：</span><span class="sxs-lookup"><span data-stu-id="1fd86-204">Note the following:</span></span>

<span data-ttu-id="1fd86-205">虛擬機器必須符合 [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="1fd86-206">若要啟用保護功能，您必須為虛擬機器設定作業系統和作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="1fd86-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="1fd86-207">當您使用虛擬機器範本在 VMM 中建立虛擬機器時，您可以設定屬性。</span><span class="sxs-lookup"><span data-stu-id="1fd86-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="1fd86-208">您也可以在虛擬機器屬性的 [一般] 及 [硬體設定] 索引標籤上，為現有的虛擬機器設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="1fd86-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="1fd86-209">若未在 VMM 中設定這些屬性，您將可在 Azure 站台復原入口網站中加以設定。</span><span class="sxs-lookup"><span data-stu-id="1fd86-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="1fd86-210">若要啟用保護，請執行下列命令以取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="1fd86-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="1fd86-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="1fd86-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="1fd86-212">執行下列命令以取得保護實體 (VM)：</span><span class="sxs-lookup"><span data-stu-id="1fd86-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="1fd86-213">執行下列命令以啟用 VM 的 DR：</span><span class="sxs-lookup"><span data-stu-id="1fd86-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="1fd86-214">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="1fd86-214">Test your deployment</span></span>
<span data-ttu-id="1fd86-215">若要測試部署，您可以對單一虛擬機器執行測試容錯移轉，或者建立包含多部虛擬機器的復原方案，再對這個方案執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1fd86-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="1fd86-216">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="1fd86-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="1fd86-217">請注意：</span><span class="sxs-lookup"><span data-stu-id="1fd86-217">Note that:</span></span>

* <span data-ttu-id="1fd86-218">如果您在容錯移轉之後要使用遠端桌面連接到 Azure 中的虛擬機器，請先在虛擬機器上啟用遠端桌面連線，再執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="1fd86-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="1fd86-219">容錯移轉之後，您將透過遠端桌面使用公用 IP 位址連接到 Azure 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="1fd86-220">如果想要這樣做，請確定沒有任何網域原則禁止您使用公用位址連接到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1fd86-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="1fd86-221">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="1fd86-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="1fd86-222">建立復原計畫</span><span class="sxs-lookup"><span data-stu-id="1fd86-222">Create a recovery plan</span></span>
1. <span data-ttu-id="1fd86-223">使用下列資料，建立 .xml 檔案做為復原計劃範本，然後將它儲存為 "C:\RPTemplatePath.xml"。</span><span class="sxs-lookup"><span data-stu-id="1fd86-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="1fd86-224">變更 RecoveryPlan 節點識別碼、Name、PrimaryServerId 和 SecondaryServerId。</span><span class="sxs-lookup"><span data-stu-id="1fd86-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="1fd86-225">變更 ProtectionEntity 節點 PrimaryProtectionEntityId (來自 VMM 的 vmid)。</span><span class="sxs-lookup"><span data-stu-id="1fd86-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="1fd86-226">您可以新增更多 ProtectionEntity 節點來新增更多 VM。</span><span class="sxs-lookup"><span data-stu-id="1fd86-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="1fd86-227">在範本中填入資料：</span><span class="sxs-lookup"><span data-stu-id="1fd86-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="1fd86-228">建立 RecoveryPlan：</span><span class="sxs-lookup"><span data-stu-id="1fd86-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="1fd86-229">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="1fd86-229">Run a test failover</span></span>
1. <span data-ttu-id="1fd86-230">執行下列命令以取得 RecoveryPlan 物件：</span><span class="sxs-lookup"><span data-stu-id="1fd86-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="1fd86-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="1fd86-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="1fd86-232">執行下列命令來啟動測試容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="1fd86-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="1fd86-233"><a name=monitor></a> 監視活動</span><span class="sxs-lookup"><span data-stu-id="1fd86-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="1fd86-234">使用下列命令來監視活動。</span><span class="sxs-lookup"><span data-stu-id="1fd86-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="1fd86-235">請注意，您必須在工作之間等候處理程序完成。</span><span class="sxs-lookup"><span data-stu-id="1fd86-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="1fd86-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fd86-236">Next steps</span></span>
<span data-ttu-id="1fd86-237">[閱讀更多](/powershell/azure/overview) Azure Site Recovery PowerShell Cmdlet 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1fd86-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="1fd86-238"></a>。</span><span class="sxs-lookup"><span data-stu-id="1fd86-238"></a>.</span></span>
