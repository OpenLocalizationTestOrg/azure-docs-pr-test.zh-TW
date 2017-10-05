---
title: "使用 PowerShell 與 Azure Resource Manager 來複寫 Hyper-V VM | Microsoft Docs"
description: "使用 PowerShell 和 Azure Resource Manager，透過 Azure Site Recovery 將 Hyper-V VM 至 Azure 的複寫自動化。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="aac3e-103">使用 PowerShell 和 Azure Resource Manager 在內部部署 Hyper-V 虛擬機器與 Azure 之間複寫</span><span class="sxs-lookup"><span data-stu-id="aac3e-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aac3e-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aac3e-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="aac3e-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="aac3e-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="aac3e-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="aac3e-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="aac3e-107">Overview</span><span class="sxs-lookup"><span data-stu-id="aac3e-107">Overview</span></span>
<span data-ttu-id="aac3e-108">Azure Site Recovery 可在一些部署案例中協調虛擬機器的複寫、容錯移轉及復原，為您的商務持續性與災害復原做出貢獻。</span><span class="sxs-lookup"><span data-stu-id="aac3e-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="aac3e-109">如需完整的部署案例清單，請參閱 [Azure Site Recovery 概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="aac3e-110">Azure PowerShell 是個模組，其提供了各種 Cmdlet 來透過 Windows PowerShell 管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="aac3e-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="aac3e-111">它可以搭配兩種模組類型使用：Azure 設定檔模組或 Azure Resource Manager 模組。</span><span class="sxs-lookup"><span data-stu-id="aac3e-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="aac3e-112">Azure PowerShell for Azure Resource Manager 提供的 Site Recovery PowerShell Cmdlet 可讓您在 Azure 中保護與復原伺服器。</span><span class="sxs-lookup"><span data-stu-id="aac3e-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="aac3e-113">本文說明如何搭配 Azure Resource Manager 使用 Windows PowerShell 來部署 Site Recovery，以設定及協調 Azure 的伺服器保護。</span><span class="sxs-lookup"><span data-stu-id="aac3e-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="aac3e-114">本文中所用的範例會說明如何使用 Azure PowerShell 和 Azure Resource Manager 保護、容錯移轉及復原 Hyper-V 主機上的虛擬機器至 Azure。</span><span class="sxs-lookup"><span data-stu-id="aac3e-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="aac3e-115">Site Recovery PowerShell Cmdlet 目前可讓您設定下列各項︰從一個 Virtual Machine Manager 網站到另一個、Virtual Machine Manager 到 Azure 及 Hyper-V 網站至 Azure。</span><span class="sxs-lookup"><span data-stu-id="aac3e-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="aac3e-116">您不需要是 PowerShell 專家也能使用本文，但您必須了解模組、Cmdlet 和工作階段等基本概念。</span><span class="sxs-lookup"><span data-stu-id="aac3e-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="aac3e-117">如需 Windows PowerShell 的詳細資訊，請參閱 [開始使用 Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="aac3e-118">您也可以參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aac3e-119">屬於雲端方案提供者 (CSP) 計畫的 Microsoft 合作夥伴，可以在其客戶各自的 CSP 訂用帳戶 (租用戶訂用帳戶) 設定和管理客戶的伺服器保護。</span><span class="sxs-lookup"><span data-stu-id="aac3e-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="aac3e-120">開始之前</span><span class="sxs-lookup"><span data-stu-id="aac3e-120">Before you start</span></span>
<span data-ttu-id="aac3e-121">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="aac3e-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="aac3e-122">[Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aac3e-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="aac3e-123">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="aac3e-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="aac3e-124">此外，您可以參閱 [Azure Site Recovery 管理員價格](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="aac3e-125">Azure PowerShell 1.0。</span><span class="sxs-lookup"><span data-stu-id="aac3e-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="aac3e-126">如需有關此版本以及如何安裝的資訊，請參閱 [Azure PowerShell 1.0。](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="aac3e-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="aac3e-127">[AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) 和 [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) 模組。</span><span class="sxs-lookup"><span data-stu-id="aac3e-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="aac3e-128">您可以從 [PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="aac3e-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="aac3e-129">本文會說明如何使用 Azure Powershell 與 Azure Resource Manager 來設定及管理伺服器保護。</span><span class="sxs-lookup"><span data-stu-id="aac3e-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="aac3e-130">本文中所用的範例會示範如何在 Hyper-V 主機執行保護 Azure 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aac3e-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="aac3e-131">下列必要條件為本範例專用。</span><span class="sxs-lookup"><span data-stu-id="aac3e-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="aac3e-132">如需一組更完整的各種 Site Recovery 案例需求，請參閱各案例文件。</span><span class="sxs-lookup"><span data-stu-id="aac3e-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="aac3e-133">執行 Windows Server 2012 R2 或 Microsoft Hyper-V Server 2012 R2 且包含一或多部虛擬機器的 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="aac3e-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="aac3e-134">直接或透過 Proxy 連接到網際網路的 Hyper-V 伺服器。</span><span class="sxs-lookup"><span data-stu-id="aac3e-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="aac3e-135">您想要保護的虛擬機器應符合 [虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="aac3e-136">步驟 1：登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="aac3e-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="aac3e-137">開啟 PowerShell 主控台並執行這個命令，登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="aac3e-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="aac3e-138">此 cmdlet 會開啟網頁，提示您輸入您的帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="aac3e-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="aac3e-139">或者，您也可以使用 `-Credential` 參數，以參數形式將您的帳戶認證加入 `Login-AzureRmAccount` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="aac3e-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="aac3e-140">如果您是代表租用戶工作的 CSP 合作夥伴，請使用客戶的 tenantID 或租用戶主要網域名稱將客戶指定為租用戶。</span><span class="sxs-lookup"><span data-stu-id="aac3e-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="aac3e-141">一個帳戶可以有多個訂用帳戶，因此您應該建立要使用的訂用帳戶和帳戶的關聯性。</span><span class="sxs-lookup"><span data-stu-id="aac3e-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="aac3e-142">使用下列命令確認您的訂用帳戶已註冊使用 Azure 復原服務提供者和 Site Recovery：</span><span class="sxs-lookup"><span data-stu-id="aac3e-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="aac3e-143">如果 **RegistrationState** 在上述這些命令的輸出中設為 [已註冊]，您可以繼續執行步驟 2。</span><span class="sxs-lookup"><span data-stu-id="aac3e-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="aac3e-144">如果未設定，訂用帳戶中應該註冊遺漏的提供者。</span><span class="sxs-lookup"><span data-stu-id="aac3e-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="aac3e-145">若要註冊 Site Recovery 和復原服務的 Azure 提供者，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="aac3e-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="aac3e-146">確認提供者成功使用 `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` 和 `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery` 命令註冊。</span><span class="sxs-lookup"><span data-stu-id="aac3e-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="aac3e-147">步驟 2：設定復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="aac3e-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="aac3e-148">建立您將在其中建立保存庫的 Azure Resource Manager 資源群組，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="aac3e-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="aac3e-149">您可以使用下列命令建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="aac3e-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="aac3e-150">$ResourceGroupName 變數包含您想要建立的資源群組名稱，而 $Geo 變數包含要在其中建立資源群組的 Azure 區域 (例如：巴西南部)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="aac3e-151">您可以使用 `Get-AzureRmResourceGroup` Cmdlet 在訂用帳戶中取得資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="aac3e-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="aac3e-152">建立新的 Azure 復原服務保存庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="aac3e-153">您可以使用 `Get-AzureRmRecoveryServicesVault` Cmdlet 擷取現有保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="aac3e-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="aac3e-154">如果您想要使用傳統入口網站或 Azure 服務管理 PowerShell 模組在建立的 Site Recovery 保存庫上執行作業，您可以使用 `Get-AzureRmSiteRecoveryVault` Cmdlet 擷取這些保存庫的清單。</span><span class="sxs-lookup"><span data-stu-id="aac3e-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="aac3e-155">您應該為所有的新作業建立新的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="aac3e-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="aac3e-156">您稍早建立的 Site Recovery 保存庫仍會受到支援，但不會有最新的功能。</span><span class="sxs-lookup"><span data-stu-id="aac3e-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="aac3e-157">步驟 3：設定復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="aac3e-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="aac3e-158">執行下列命令來設定保存庫內容：</span><span class="sxs-lookup"><span data-stu-id="aac3e-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="aac3e-159">步驟 4：建立 Hyper-V 網站，並產生網站的新保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="aac3e-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="aac3e-160">建立新的 Hyper-V 站台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="aac3e-161">這個 Cmdlet 會啟動 Site Recovery 作業來建立網站，並傳回 Site Recovery 作業物件。</span><span class="sxs-lookup"><span data-stu-id="aac3e-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="aac3e-162">等待作業完成，並確認作業已成功完成。</span><span class="sxs-lookup"><span data-stu-id="aac3e-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="aac3e-163">您可以擷取作業物件，並使用 Get-AzureRmSiteRecoveryJob Cmdlet 檢查目前的作業狀態。</span><span class="sxs-lookup"><span data-stu-id="aac3e-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="aac3e-164">產生並下載網站的註冊金鑰，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="aac3e-165">將下載的金鑰複製到 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="aac3e-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="aac3e-166">您需要金鑰向網站註冊 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="aac3e-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="aac3e-167">步驟 5：在 Hyper-V 主機上安裝 Azure Site Recovery 提供者和 Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="aac3e-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="aac3e-168">從 [Microsoft](https://aka.ms/downloaddra)下載最新版提供者的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="aac3e-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="aac3e-169">在 Hyper-V 主機上執行安裝程式，然後在安裝結尾繼續註冊步驟。</span><span class="sxs-lookup"><span data-stu-id="aac3e-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="aac3e-170">當系統提示時提供下載的網站註冊金鑰，並完成網站的 Hyper-V 主機註冊。</span><span class="sxs-lookup"><span data-stu-id="aac3e-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="aac3e-171">確認 Hyper-V 主機使用下列命令向網站註冊：</span><span class="sxs-lookup"><span data-stu-id="aac3e-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="aac3e-172">步驟 6：建立複寫原則，並建立其與保護容器的關聯</span><span class="sxs-lookup"><span data-stu-id="aac3e-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="aac3e-173">建立複寫原則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="aac3e-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="aac3e-174">請檢查傳回的作業，以確保複寫原則建立成功。</span><span class="sxs-lookup"><span data-stu-id="aac3e-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="aac3e-175">指定的儲存體帳戶應與您的復原服務保存庫位於相同的 Azure 區域中，而且應該啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="aac3e-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="aac3e-176">如果指定的復原儲存體帳戶屬於 Azure Storage (Classic) 類型，受保護機器的容錯移轉會將機器復原到 Azure IaaS (Classic)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="aac3e-177">如果指定的復原儲存體帳戶屬於 Azure Storage (Azure Resource Manager) 類型，受保護機器的容錯移轉會將機器復原到 Azure IaaS (Azure Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="aac3e-178">取得對應至網站的保護容器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="aac3e-179">啟動保護容器與複寫原則的關聯，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="aac3e-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="aac3e-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="aac3e-181">等待關聯作業完成，並確保成功完成。</span><span class="sxs-lookup"><span data-stu-id="aac3e-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="aac3e-182">步驟 7：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="aac3e-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="aac3e-183">取得對應至您想要保護之 VM 的保護實體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="aac3e-184">停止保護虛擬機器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="aac3e-185">指定的儲存體帳戶應與您的復原服務保存庫位於相同的 Azure 區域中，而且應該啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="aac3e-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="aac3e-186">如果指定的復原儲存體帳戶屬於 Azure Storage (Classic) 類型，受保護機器的容錯移轉會將機器復原到 Azure IaaS (Classic)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="aac3e-187">如果指定的復原儲存體帳戶屬於 Azure Storage (Azure Resource Manager) 類型，受保護機器的容錯移轉會將機器復原到 Azure IaaS (Azure Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="aac3e-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="aac3e-188">如果您要保護的 VM 有多個連接到它的磁碟，請使用 OSDiskName  參數指定作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="aac3e-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="aac3e-189">在初始複寫後，等待虛擬機器達到受保護的狀態。</span><span class="sxs-lookup"><span data-stu-id="aac3e-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="aac3e-190">所需時間長短，受到要複寫的資料量和可用的 Azure 上游頻寬等因素影響。</span><span class="sxs-lookup"><span data-stu-id="aac3e-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="aac3e-191">當 VM 達到受保護的狀態時，作業的 State 和 StateDescription 就會更新，如下所示。</span><span class="sxs-lookup"><span data-stu-id="aac3e-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="aac3e-192">更新 VM 角色大小等復原屬性，以及在容錯移轉時要附加虛擬機器網路介面卡的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="aac3e-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update the virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="aac3e-193">步驟 8：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="aac3e-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="aac3e-194">執行測試容錯移轉作業，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="aac3e-195">確認已在 Azure 中建立測試 VM。</span><span class="sxs-lookup"><span data-stu-id="aac3e-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="aac3e-196">(在 Azure 中建立測試 VM 之後，測試容錯移轉作業已經暫停。</span><span class="sxs-lookup"><span data-stu-id="aac3e-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="aac3e-197">作業會藉由清除繼續進行作業時建立的成品來完成，如下一個步驟所示。)</span><span class="sxs-lookup"><span data-stu-id="aac3e-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="aac3e-198">完成測試容錯移轉，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aac3e-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="aac3e-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aac3e-199">Next Steps</span></span>
<span data-ttu-id="aac3e-200">[閱讀更多](https://msdn.microsoft.com/library/azure/mt637930.aspx) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aac3e-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
