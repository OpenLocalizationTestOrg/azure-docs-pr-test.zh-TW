---
title: "使用 PowerShell 和 Azure 資源管理員的 HYPER-V Vm aaaReplicate |Microsoft 文件"
description: "使用 PowerShell 和 Azure 資源管理員的 Azure Site recovery 自動化 HYPER-V Vm tooAzure hello 的複寫。"
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
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="33098-103">使用 PowerShell 和 Azure Resource Manager 在內部部署 Hyper-V 虛擬機器與 Azure 之間複寫</span><span class="sxs-lookup"><span data-stu-id="33098-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33098-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="33098-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="33098-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="33098-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="33098-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="33098-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="33098-107">概觀</span><span class="sxs-lookup"><span data-stu-id="33098-107">Overview</span></span>
<span data-ttu-id="33098-108">Azure Site Recovery 提供 tooyour 業務續航力和災害復原策略可藉由協調複寫、 容錯移轉，以及一些部署案例中的虛擬機器的復原。</span><span class="sxs-lookup"><span data-stu-id="33098-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="33098-109">如需部署案例的完整清單，請參閱 hello [Azure 站台復原概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="33098-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="33098-110">Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="33098-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="33098-111">它可以使用兩種類型的模組： hello Azure 設定檔模組或 hello Azure 資源管理員模組。</span><span class="sxs-lookup"><span data-stu-id="33098-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="33098-112">Azure PowerShell for Azure Resource Manager 提供的 Site Recovery PowerShell Cmdlet 可讓您在 Azure 中保護與復原伺服器。</span><span class="sxs-lookup"><span data-stu-id="33098-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="33098-113">本文說明如何 toouse Windows PowerShell，以及 Azure 資源管理員，toodeploy Site Recovery tooconfigure 以及協調伺服器保護 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="33098-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="33098-114">在本文中使用的 hello 範例將示範如何 tooprotect，容錯移轉和復原虛擬機器上的 HYPER-V 主機 tooAzure，使用 Azure PowerShell 的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="33098-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="33098-115">hello 站台復原 PowerShell cmdlet 目前可讓您遵循 tooconfigure hello： 一個 Virtual Machine Manager 的站台 tooanother、 Virtual Machine Manager 網站 tooAzure 及 HYPER-V 站台 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="33098-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="33098-116">您不需要 toobe PowerShell 專家 toouse 本文中，但您需要 toounderstand hello 基本概念，例如模組、 cmdlet 和工作階段。</span><span class="sxs-lookup"><span data-stu-id="33098-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="33098-117">如需 Windows PowerShell 的詳細資訊，請參閱 [開始使用 Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="33098-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="33098-118">您也可以參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="33098-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33098-119">屬於 hello 雲端方案提供者 (CSP) 程式的 Microsoft 合作夥伴可以設定及管理其客戶的伺服器的保護個別 CSP 訂閱 tootheir 客戶 （租用戶訂閱）。</span><span class="sxs-lookup"><span data-stu-id="33098-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="33098-120">開始之前</span><span class="sxs-lookup"><span data-stu-id="33098-120">Before you start</span></span>
<span data-ttu-id="33098-121">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="33098-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="33098-122">[Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="33098-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="33098-123">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="33098-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="33098-124">此外，您可以參閱 [Azure Site Recovery 管理員價格](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="33098-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="33098-125">Azure PowerShell 1.0。</span><span class="sxs-lookup"><span data-stu-id="33098-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="33098-126">如需有關此版本資訊和如何 tooinstall，請參閱[Azure PowerShell 1.0。](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="33098-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="33098-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/)和[AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/)模組。</span><span class="sxs-lookup"><span data-stu-id="33098-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="33098-128">您可以從 hello 取得 hello 最新版本，這些模組[PowerShell 資源庫](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="33098-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="33098-129">本文將說明如何使用 Azure Resource Manager tooconfigure toouse Azure Powershell 及管理您伺服器的保護。</span><span class="sxs-lookup"><span data-stu-id="33098-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="33098-130">在本文中使用的 hello 範例將示範如何為虛擬機器，主機上執行 HYPER-V，tooAzure tooprotect。</span><span class="sxs-lookup"><span data-stu-id="33098-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="33098-131">hello 下列必要條件是特定 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="33098-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="33098-132">一組更完整的需求的 hello 各種站台復原案例，請參閱相關 toothat 案例 toohello 文件。</span><span class="sxs-lookup"><span data-stu-id="33098-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="33098-133">執行 Windows Server 2012 R2 或 Microsoft Hyper-V Server 2012 R2 且包含一或多部虛擬機器的 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="33098-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="33098-134">HYPER-V 伺服器連接網際網路，toohello 直接或透過 proxy。</span><span class="sxs-lookup"><span data-stu-id="33098-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="33098-135">hello 想 tooprotect 的虛擬機器都應該符合[虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="33098-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="33098-136">步驟 1： 登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="33098-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="33098-137">開啟 PowerShell 主控台並執行此命令 toosign tooyour Azure 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="33098-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="33098-138">hello cmdlet 就會開啟一個網頁，會提示您輸入您的帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="33098-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="33098-139">或者，加入您的帳戶認證為參數 toohello `Login-AzureRmAccount` cmdlet，利用 hello`-Credential`參數。</span><span class="sxs-lookup"><span data-stu-id="33098-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="33098-140">如果您是使用代表租用戶的 CSP 夥伴時，指定為租用戶，hello 客戶使用其 tenantID 或租用戶的主要網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33098-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="33098-141">帳戶可以有數個訂閱，所以您應該將您想要與 hello 帳戶 toouse hello 訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="33098-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="33098-142">請確認您的訂用帳戶註冊的 toouse 復原服務與站台復原 hello Azure 提供者，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="33098-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="33098-143">Hello 輸出中的這些命令，如果 hello **RegistrationState**設定得**註冊**，您可以繼續 tooStep 2。</span><span class="sxs-lookup"><span data-stu-id="33098-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="33098-144">如果沒有，您應該註冊您的訂用帳戶中的 hello 遺漏提供者。</span><span class="sxs-lookup"><span data-stu-id="33098-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="33098-145">tooregister hello Azure 提供者站台復原和復原服務，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="33098-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="33098-146">請確認 hello 提供者已成功註冊使用下列命令的 hello:`Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`和`Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`。</span><span class="sxs-lookup"><span data-stu-id="33098-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="33098-147">步驟 2： 設定復原服務保存庫的 hello</span><span class="sxs-lookup"><span data-stu-id="33098-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="33098-148">建立 Azure 資源管理員資源群組中，您將建立 hello 保存庫，或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="33098-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="33098-149">您可以使用下列命令的 hello，以建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="33098-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="33098-150">hello $ResourceGroupName 變數包含 hello hello 資源群組名稱在您想 toocreate，而且 hello $Geo 變數包含 hello Azure 區域中哪一個 toocreate hello 資源群組 （例如，"巴西南部 」）。</span><span class="sxs-lookup"><span data-stu-id="33098-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="33098-151">您也可以使用 hello 您訂用帳戶中取得一份資源群組`Get-AzureRmResourceGroup`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="33098-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="33098-152">建立新的 Azure 復原服務保存庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="33098-153">您可以擷取一份現有保存庫使用 hello `Get-AzureRmRecoveryServicesVault` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="33098-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="33098-154">如果您想使用 hello 傳統入口網站或 hello Azure Service Management PowerShell 模組所建立的站台復原保存庫 tooperform 作業時，您可以擷取一份這類保存庫使用 hello `Get-AzureRmSiteRecoveryVault` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="33098-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="33098-155">您應該為所有的新作業建立新的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33098-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="33098-156">您稍早建立的 hello Site Recovery 保存庫支援，但是沒有 hello 最新的功能。</span><span class="sxs-lookup"><span data-stu-id="33098-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="33098-157">步驟 3： 設定 hello 復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="33098-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="33098-158">執行下列命令的 hello 設定 hello 保存庫的內容：</span><span class="sxs-lookup"><span data-stu-id="33098-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="33098-159">步驟 4： 建立 HYPER-V 站台，並產生新的保存庫註冊金鑰 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="33098-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="33098-160">建立新的 Hyper-V 站台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="33098-161">此 cmdlet 會啟動站台復原作業 toocreate hello 站台，並傳回站台復原工作物件。</span><span class="sxs-lookup"><span data-stu-id="33098-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="33098-162">等候 hello 作業 toocomplete，並確認該 hello 工作順利完成。</span><span class="sxs-lookup"><span data-stu-id="33098-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="33098-163">您可以擷取 hello 工作物件，並藉此使用 hello Get AzureRmSiteRecoveryJob cmdlet 檢查 hello hello 作業目前狀態。</span><span class="sxs-lookup"><span data-stu-id="33098-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="33098-164">產生並下載註冊金鑰 hello 網站，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="33098-165">複製 hello 下載金鑰 toohello HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="33098-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="33098-166">您需要 hello 金鑰 tooregister hello HYPER-V 主機 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="33098-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="33098-167">步驟 5: Hello Azure Site Recovery provider 和 Azure Recovery Services Agent 安裝在 HYPER-V 主機上</span><span class="sxs-lookup"><span data-stu-id="33098-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="33098-168">下載 hello hello hello 提供者，從最新版本的安裝程式[Microsoft](https://aka.ms/downloaddra)。</span><span class="sxs-lookup"><span data-stu-id="33098-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="33098-169">Hello 執行安裝程式在 HYPER-V 主機上，並在 hello hello 安裝結尾繼續 toohello 註冊的步驟。</span><span class="sxs-lookup"><span data-stu-id="33098-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="33098-170">出現提示時，提供 hello 下載站台的註冊金鑰，並完成註冊的 hello HYPER-V 主機 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="33098-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="33098-171">確認該 hello HYPER-V 主機已註冊的 toohello 站台使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="33098-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="33098-172">步驟 6： 建立複寫原則，並將它與 hello 保護容器關聯</span><span class="sxs-lookup"><span data-stu-id="33098-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="33098-173">建立複寫原則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="33098-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="33098-174">傳回 hello 複寫原則建立成功的作業 tooensure 核取 hello。</span><span class="sxs-lookup"><span data-stu-id="33098-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="33098-175">hello 指定儲存體帳戶應在 hello 與您的復原服務保存庫相同的 Azure 區域，而且應啟用地理複寫。</span><span class="sxs-lookup"><span data-stu-id="33098-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="33098-176">如果 hello 指定儲存體帳戶屬於型別 Azure 儲存體 （傳統） 的復原，容錯移轉的 hello 受保護機器復原 hello 機器 tooAzure IaaS （傳統）。</span><span class="sxs-lookup"><span data-stu-id="33098-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="33098-177">如果 hello 指定復原儲存體帳戶屬於 Azure 儲存體 (Azure Resource Manager) 的型別，hello 的容錯移轉受保護機器復原 hello 機器 tooAzure IaaS (Azure Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="33098-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="33098-178">取得 hello 保護容器對應 toohello 站台，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="33098-179">開始 hello 關聯 hello 保護容器 hello 複寫原則，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="33098-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="33098-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="33098-181">等候 hello 關聯作業 toocomplete，並請確定已成功完成。</span><span class="sxs-lookup"><span data-stu-id="33098-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="33098-182">步驟 7：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="33098-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="33098-183">收到 hello 保護實體對應 toohello VM 想 tooprotect，，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="33098-184">開始保護 hello 虛擬機器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="33098-185">hello 指定儲存體帳戶應在 hello 與您的復原服務保存庫相同的 Azure 區域，而且應啟用地理複寫。</span><span class="sxs-lookup"><span data-stu-id="33098-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="33098-186">如果 hello 指定儲存體帳戶屬於型別 Azure 儲存體 （傳統） 的復原，容錯移轉的 hello 受保護機器復原 hello 機器 tooAzure IaaS （傳統）。</span><span class="sxs-lookup"><span data-stu-id="33098-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="33098-187">如果 hello 指定復原儲存體帳戶屬於 Azure 儲存體 (Azure Resource Manager) 的型別，hello 的容錯移轉受保護機器復原 hello 機器 tooAzure IaaS (Azure Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="33098-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="33098-188">如果您要保護的 VM hello 有多個磁碟附加的 tooit，使用 hello 指定 hello 作業系統磁碟*OSDiskName*參數。</span><span class="sxs-lookup"><span data-stu-id="33098-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="33098-189">等候 hello 虛擬機器 tooreach 受保護的狀態 hello 初始複寫之後。</span><span class="sxs-lookup"><span data-stu-id="33098-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="33098-190">這可以使用一段時間，取決於複寫資料 toobe hello 量等因素，並 hello tooAzure 上游的可用頻寬。</span><span class="sxs-lookup"><span data-stu-id="33098-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="33098-191">hello 工作狀態和 StateDescription，則會在 hello VM 達到受保護的狀態時，如下所示，更新。</span><span class="sxs-lookup"><span data-stu-id="33098-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="33098-192">更新修復屬性，例如 hello VM 角色大小和 hello Azure 網路 tooattach hello 虛擬機器的網路介面卡 tooupon 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="33098-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

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
        DisplayName      : Update hello virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="33098-193">步驟 8：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="33098-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="33098-194">執行測試容錯移轉作業，如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="33098-195">請確認 VM 在 Azure 中建立該 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="33098-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="33098-196">（hello 測試容錯移轉作業已暫停之後在 Azure 中建立 hello 測試 VM。</span><span class="sxs-lookup"><span data-stu-id="33098-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="33098-197">hello 作業的完成作業清除已完成時繼續 hello 工作建立 hello artefacts hello 下一個步驟中所示。）</span><span class="sxs-lookup"><span data-stu-id="33098-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="33098-198">完成 hello 測試容錯移轉的如下所示：</span><span class="sxs-lookup"><span data-stu-id="33098-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="33098-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33098-199">Next Steps</span></span>
<span data-ttu-id="33098-200">[閱讀更多](https://msdn.microsoft.com/library/azure/mt637930.aspx) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="33098-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
