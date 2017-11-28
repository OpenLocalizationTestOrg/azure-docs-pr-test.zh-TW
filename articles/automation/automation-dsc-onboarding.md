---
title: "管理 Azure 自動化 DSC aaaOnboarding 機器 |Microsoft 文件"
description: "Toosetup 以使用 Azure 自動化 DSC 進行管理的電腦"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="002b2-103">上架由 Azure 自動化 DSC 管理的機器</span><span class="sxs-lookup"><span data-stu-id="002b2-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="002b2-104">為什麼要使用 Azure 自動化 DSC 管理機器？</span><span class="sxs-lookup"><span data-stu-id="002b2-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="002b2-105">如同 [PowerShell 期望的狀態設定](https://technet.microsoft.com/library/dn249912.aspx)，Azure 自動化期望的狀態設定在任何雲端或內部部署資料中心中是 DSC 節點 (實體和虛擬機器) 的一個簡單但強大的組態管理服務。</span><span class="sxs-lookup"><span data-stu-id="002b2-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="002b2-106">它可讓您從中央、安全的位置快速且輕鬆地延展性到數千部電腦。</span><span class="sxs-lookup"><span data-stu-id="002b2-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="002b2-107">您可以輕鬆地登入機器，它們的宣告式組態，並檢視報表，顯示每個電腦的指派的相容性 toohello 預期的狀態，您所指定。</span><span class="sxs-lookup"><span data-stu-id="002b2-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance toohello desired state you specified.</span></span> <span data-ttu-id="002b2-108">hello Azure Automation DSC 管理層是 tooDSC hello Azure 自動化的管理圖層 tooPowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="002b2-108">hello Azure Automation DSC management layer is tooDSC what hello Azure Automation management layer is tooPowerShell scripting.</span></span> <span data-ttu-id="002b2-109">換句話說，在 hello Azure 自動化可協助您的相同方式來管理 PowerShell 指令碼，也可協助您管理 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="002b2-109">In other words, in hello same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="002b2-110">請參閱深入了解使用 Azure 自動化 DSC，hello 優勢 toolearn [Azure Automation DSC 概觀](automation-dsc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="002b2-110">toolearn more about hello benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="002b2-111">Azure 自動化 DSC 可以用的 toomanage 各種不同的機器：</span><span class="sxs-lookup"><span data-stu-id="002b2-111">Azure Automation DSC can be used toomanage a variety of machines:</span></span>

* <span data-ttu-id="002b2-112">Azure 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="002b2-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="002b2-113">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="002b2-113">Azure virtual machines</span></span>
* <span data-ttu-id="002b2-114">Amazon Web Services (AWS) 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="002b2-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="002b2-115">位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="002b2-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="002b2-116">位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器</span><span class="sxs-lookup"><span data-stu-id="002b2-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="002b2-117">此外，如果您不是從 hello 雲端準備 toomanage 機器組態，Azure 自動化 DSC 也可用做為報表專用端點。</span><span class="sxs-lookup"><span data-stu-id="002b2-117">In addition, if you are not ready toomanage machine configuration from hello cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="002b2-118">這可讓您透過 DSC 內部 tooset (push) 所需的設定，而檢視豐富報表的詳細資料節點的相容性以 hello Azure 自動化中的狀態。</span><span class="sxs-lookup"><span data-stu-id="002b2-118">This allows you tooset (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with hello desired state in Azure Automation.</span></span>

<span data-ttu-id="002b2-119">hello 下列各節簡述如何將產品上架機器 tooAzure Automation DSC 的每個型別。</span><span class="sxs-lookup"><span data-stu-id="002b2-119">hello following sections outline how you can onboard each type of machine tooAzure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="002b2-120">Azure 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="002b2-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="002b2-121">向 Azure 自動化 DSC，您可以輕鬆地登入 Azure 虛擬機器 （傳統） 組態管理使用 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="002b2-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either hello Azure portal, or PowerShell.</span></span> <span data-ttu-id="002b2-122">Hello 幕後並沒有需要 tooremote hello VM 到系統管理員，hello Azure VM Desired State Configuration 延伸模組會使用 Azure 自動化 DSC 註冊 hello VM。</span><span class="sxs-lookup"><span data-stu-id="002b2-122">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="002b2-123">Hello Azure VM Desired State Configuration 延伸模組以非同步方式執行步驟 tootrack 其進度，或疑難排解因為它提供在 hello [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-123">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="002b2-124">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="002b2-124">Azure portal</span></span>

<span data-ttu-id="002b2-125">在 hello [Azure 入口網站](http://portal.azure.com/)，按一下 **瀏覽** -> **虛擬機器 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="002b2-125">In hello [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="002b2-126">選取您想要 tooonboard Windows VM hello。</span><span class="sxs-lookup"><span data-stu-id="002b2-126">Select hello Windows VM you want tooonboard.</span></span> <span data-ttu-id="002b2-127">Hello 虛擬機器的儀表板] 刀鋒視窗中，按一下 [**所有設定** -> **延伸** -> **新增** ->  **Azure 自動化 DSC** -> **建立**。</span><span class="sxs-lookup"><span data-stu-id="002b2-127">On hello virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="002b2-128">輸入 hello [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)使用案例，您的自動化帳戶登錄機碼和登錄的 URL，並選擇性節點組態 tooassign toohello VM 所需。</span><span class="sxs-lookup"><span data-stu-id="002b2-128">Enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="002b2-129">toofind hello 註冊 URL 和 hello 自動化帳戶 tooonboard hello 機器金鑰，請參閱 hello [**安全註冊**](#secure-registration)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-129">toofind hello registration URL and key for hello Automation account tooonboard hello machine to, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="002b2-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="002b2-130">PowerShell</span></span>

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="002b2-131">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="002b2-131">Azure virtual machines</span></span>

<span data-ttu-id="002b2-132">Azure 自動化 DSC 可讓您輕鬆地登入 Azure 虛擬機器組態管理使用 hello Azure 入口網站、 Azure Resource Manager 範本或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="002b2-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either hello Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="002b2-133">Hello 幕後並沒有需要 tooremote hello VM 到系統管理員，hello Azure VM Desired State Configuration 延伸模組會使用 Azure 自動化 DSC 註冊 hello VM。</span><span class="sxs-lookup"><span data-stu-id="002b2-133">Under hello hood, and without an administrator having tooremote into hello VM, hello Azure VM Desired State Configuration extension registers hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="002b2-134">Hello Azure VM Desired State Configuration 延伸模組以非同步方式執行步驟 tootrack 其進度，或疑難排解因為它提供在 hello [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-134">Since hello Azure VM Desired State Configuration extension runs asynchronously, steps tootrack its progress or troubleshoot it are provided in hello [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="002b2-135">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="002b2-135">Azure portal</span></span>

<span data-ttu-id="002b2-136">在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello 想 tooonboard 虛擬機器的 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="002b2-136">In hello [Azure portal](https://portal.azure.com/), navigate toohello Azure Automation account where you want tooonboard virtual machines.</span></span> <span data-ttu-id="002b2-137">在 hello 自動化帳戶儀表板，按一下  **DSC 節點** -> **新增 Azure VM**。</span><span class="sxs-lookup"><span data-stu-id="002b2-137">On hello Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="002b2-138">在下**選取虛擬機器 tooonboard**、 選取一或多個 Azure 虛擬機器 tooonboard。</span><span class="sxs-lookup"><span data-stu-id="002b2-138">Under **Select virtual machines tooonboard**, select one or more Azure virtual machines tooonboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="002b2-139">在下**設定註冊資料**，輸入 hello [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)所需的使用案例中，並選擇性節點組態 tooassign toohello VM。</span><span class="sxs-lookup"><span data-stu-id="002b2-139">Under **Configure registration data**, enter hello [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration tooassign toohello VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="002b2-140">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="002b2-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="002b2-141">您可以部署 azure 虛擬機器和 onboarded tooAzure Automation DSC 透過 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="002b2-141">Azure virtual machines can be deployed and onboarded tooAzure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="002b2-142">請參閱[設定透過 DSC 延伸模組的 VM 和 Azure 自動化 DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/)範例範本該 onboards 現有的 VM tooAzure Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="002b2-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM tooAzure Automation DSC.</span></span> <span data-ttu-id="002b2-143">toofind hello 登錄機碼及註冊 URL 採取做為此範本中的輸入，請參閱 hello [**安全註冊**](#secure-registration)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-143">toofind hello registration key and registration URL taken as input in this template, see hello [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="002b2-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="002b2-144">PowerShell</span></span>

<span data-ttu-id="002b2-145">hello[暫存器 AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode)指令程式可以使用的 tooonboard hello 透過 PowerShell 的 Azure 入口網站中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="002b2-145">hello [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used tooonboard virtual machines in hello Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="002b2-146">Amazon Web Services (AWS) 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="002b2-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="002b2-147">您可以輕鬆加入 Amazon Web Services 虛擬機器組態管理 Azure 自動化 dsc 使用 hello AWS DSC 工具組。</span><span class="sxs-lookup"><span data-stu-id="002b2-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using hello AWS DSC Toolkit.</span></span> <span data-ttu-id="002b2-148">您可以進一步了解 hello toolkit[這裡](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/)。</span><span class="sxs-lookup"><span data-stu-id="002b2-148">You can learn more about hello toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="002b2-149">位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="002b2-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="002b2-150">在內部部署的 Windows 電腦以及 Windows （例如 Amazon Web Services) 的非 Azure 雲端中也可以是 onboarded tooAzure 自動化 DSC，只要有 toohello 對外存取網際網路，透過一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="002b2-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="002b2-151">請確定 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝想 tooonboard tooAzure Automation DSC 在 hello 機器上。</span><span class="sxs-lookup"><span data-stu-id="002b2-151">Make sure hello latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="002b2-152">一節中的 hello 遵循[**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations)下方 toogenerate 需要一個資料夾包含 hello DSC 中繼設定。</span><span class="sxs-lookup"><span data-stu-id="002b2-152">Follow hello directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="002b2-153">從遠端適用於您想 tooonboard hello PowerShell DSC 中繼設定 toohello 機器。</span><span class="sxs-lookup"><span data-stu-id="002b2-153">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard.</span></span> <span data-ttu-id="002b2-154">**此命令會從執行的 hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝**:</span><span class="sxs-lookup"><span data-stu-id="002b2-154">**hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="002b2-155">如果您無法從遠端套用 hello PowerShell DSC 中繼設定，請將 hello 中繼設定資料夾複製到每個機器 tooonboard 步驟 2 中。</span><span class="sxs-lookup"><span data-stu-id="002b2-155">If you cannot apply hello PowerShell DSC metaconfigurations remotely, copy hello metaconfigurations folder from step 2 onto each machine tooonboard.</span></span> <span data-ttu-id="002b2-156">然後呼叫**Set-dsclocalconfigurationmanager**在本機上每個機器 tooonboard。</span><span class="sxs-lookup"><span data-stu-id="002b2-156">Then call **Set-DscLocalConfigurationManager** locally on each machine tooonboard.</span></span>
5. <span data-ttu-id="002b2-157">使用 hello Azure 入口網站或 cmdlet，您的 Azure 自動化帳戶中註冊的 hello 機器 tooonboard 現在顯示為 DSC 節點的核取。</span><span class="sxs-lookup"><span data-stu-id="002b2-157">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="002b2-158">位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器</span><span class="sxs-lookup"><span data-stu-id="002b2-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="002b2-159">在內部部署 Linux 機器，Linux 機器，在 Azure 中，而且非 Azure 雲端中的 Linux 機器也可能 onboarded tooAzure 自動化 DSC，只要有 toohello 對外存取網際網路，透過一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="002b2-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded tooAzure Automation DSC, as long as they have outbound access toohello internet, via a few simple steps:</span></span>

1. <span data-ttu-id="002b2-160">請確定 hello 最新版本的[Linux 的 PowerShell 預期狀態設定](https://github.com/Microsoft/PowerShell-DSC-for-Linux)安裝想 tooonboard tooAzure Automation DSC 在 hello 機器上。</span><span class="sxs-lookup"><span data-stu-id="002b2-160">Make sure hello latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on hello machines you want tooonboard tooAzure Automation DSC.</span></span>
2. <span data-ttu-id="002b2-161">如果 hello [PowerShell DSC 本機設定管理員的預設值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)符合您的使用案例，而且您想 tooonboard 機器例如它們**兩者**從提取和報告 tooAzure 自動化 DSC:</span><span class="sxs-lookup"><span data-stu-id="002b2-161">If hello [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want tooonboard machines such that they **both** pull from and report tooAzure Automation DSC:</span></span>

   + <span data-ttu-id="002b2-162">在每個 Linux 機器 tooonboard tooAzure 自動化 DSC，使用 Register.py tooonboard 使用的 hello PowerShell DSC 本機設定管理員的預設值：</span><span class="sxs-lookup"><span data-stu-id="002b2-162">On each Linux machine tooonboard tooAzure Automation DSC, use Register.py tooonboard using hello PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="002b2-163">toofind hello 登錄機碼及註冊 URL 為您的自動化帳戶，請參閱 hello [**安全註冊**](#secure-registration)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-163">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="002b2-164">如果 hello PowerShell DSC 本機設定管理員預設**不要****不**符合您的使用案例，或者您想 tooonboard 機器，它們只會報告 tooAzure 自動化 DSC，但不要提取設定或 PowerShell 模組，請遵循步驟 3 到 6。</span><span class="sxs-lookup"><span data-stu-id="002b2-164">If hello PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want tooonboard machines such that they only report tooAzure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="002b2-165">否則，請繼續直接 toostep 6。</span><span class="sxs-lookup"><span data-stu-id="002b2-165">Otherwise, proceed directly toostep 6.</span></span>

3. <span data-ttu-id="002b2-166">依照指示進行 hello hello [**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations) toogenerate 下方區段包含所需的 hello DSC 中繼設定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="002b2-166">Follow hello directions in hello [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below toogenerate a folder containing hello needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="002b2-167">從遠端適用於您想 tooonboard hello PowerShell DSC 中繼設定 toohello 機器：</span><span class="sxs-lookup"><span data-stu-id="002b2-167">Remotely apply hello PowerShell DSC metaconfiguration toohello machines you want tooonboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="002b2-168">此命令會從執行的 hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝。</span><span class="sxs-lookup"><span data-stu-id="002b2-168">hello machine this command is run from must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="002b2-169">如果您無法將 hello PowerShell DSC 中繼設定套用的每個 Linux 機器 tooonboard 的遠端電腦上，複製到 hello Linux 機器上的步驟 5 中的 hello 資料夾 hello 中繼設定對應 toothat 機器。</span><span class="sxs-lookup"><span data-stu-id="002b2-169">If you cannot apply hello PowerShell DSC metaconfigurations remotely, for each Linux machine tooonboard, copy hello metaconfiguration corresponding toothat machine from hello folder in step 5 onto hello Linux machine.</span></span> <span data-ttu-id="002b2-170">然後呼叫`SetDscLocalConfigurationManager.py`本機每部 Linux 機器上您想 tooonboard tooAzure 自動化 DSC:</span><span class="sxs-lookup"><span data-stu-id="002b2-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want tooonboard tooAzure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. <span data-ttu-id="002b2-171">使用 hello Azure 入口網站或 cmdlet，您的 Azure 自動化帳戶中註冊的 hello 機器 tooonboard 現在顯示為 DSC 節點的核取。</span><span class="sxs-lookup"><span data-stu-id="002b2-171">Using hello Azure portal or cmdlets, check that hello machines tooonboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="002b2-172">產生 DSC 中繼設定</span><span class="sxs-lookup"><span data-stu-id="002b2-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="002b2-173">toogenerically 任何機器 tooAzure Automation DSC 的上架[DSC 中繼設定](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig)可以產生的當套用，告知 hello DSC 代理程式上從 hello 機器 toopull 及/或報告 tooAzure Automation DSC。</span><span class="sxs-lookup"><span data-stu-id="002b2-173">toogenerically onboard any machine tooAzure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells hello DSC agent on hello machine toopull from and/or report tooAzure Automation DSC.</span></span> <span data-ttu-id="002b2-174">可以使用 PowerShell DSC 設定或 hello Azure 自動化的 PowerShell 指令程式會產生 Azure 自動化 DSC 的 DSC 中繼設定。</span><span class="sxs-lookup"><span data-stu-id="002b2-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or hello Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="002b2-175">DSC 中繼設定會包含 hello 所需的秘密 tooonboard 機器 tooan 管理的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="002b2-175">DSC metaconfigurations contain hello secrets needed tooonboard a machine tooan Automation account for management.</span></span> <span data-ttu-id="002b2-176">請確定 tooproperly 保護您建立時，任何 DSC 中繼設定，或在使用後刪除它們。</span><span class="sxs-lookup"><span data-stu-id="002b2-176">Make sure tooproperly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="002b2-177">使用 DSC 設定</span><span class="sxs-lookup"><span data-stu-id="002b2-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="002b2-178">開啟 hello 身為系統管理員的 PowerShell ISE 中的本機環境中的機器。</span><span class="sxs-lookup"><span data-stu-id="002b2-178">Open hello PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="002b2-179">hello 機器必須 hello 最新版本的[WMF 5](http://aka.ms/wmf5latest)安裝。</span><span class="sxs-lookup"><span data-stu-id="002b2-179">hello machine must have hello latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="002b2-180">複製下列指令碼在本機的 hello。</span><span class="sxs-lookup"><span data-stu-id="002b2-180">Copy hello following script locally.</span></span> <span data-ttu-id="002b2-181">此指令碼包含 PowerShell DSC 設定用於建立中繼設定和命令 tookick hello 中繼設定建立功能。</span><span class="sxs-lookup"><span data-stu-id="002b2-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command tookick off hello metaconfiguration creation.</span></span>

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="002b2-182">為您的自動化帳戶，以及 hello 機器 tooonboard hello 名稱填入 hello 註冊金鑰和 URL。</span><span class="sxs-lookup"><span data-stu-id="002b2-182">Fill in hello registration key and URL for your Automation account, as well as hello names of hello machines tooonboard.</span></span> <span data-ttu-id="002b2-183">所有其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="002b2-183">All other parameters are optional.</span></span> <span data-ttu-id="002b2-184">toofind hello 登錄機碼及註冊 URL 為您的自動化帳戶，請參閱 hello [**安全註冊**](#secure-registration)下一節。</span><span class="sxs-lookup"><span data-stu-id="002b2-184">toofind hello registration key and registration URL for your Automation account, see hello [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="002b2-185">如果您想 hello 機器 tooreport DSC 狀態資訊 tooAzure 自動化 DSC，但不是會提取組態或 PowerShell 模組，設定 hello **ReportOnly**參數 tootrue。</span><span class="sxs-lookup"><span data-stu-id="002b2-185">If you want hello machines tooreport DSC status information tooAzure Automation DSC, but not pull configuration or PowerShell modules, set hello **ReportOnly** parameter tootrue.</span></span>
5. <span data-ttu-id="002b2-186">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="002b2-186">Run hello script.</span></span> <span data-ttu-id="002b2-187">您現在應該會有一個名為資料夾**DscMetaConfigs**在您的工作目錄中包含的 hello 機器 tooonboard （以系統管理員身分） hello PowerShell DSC 中繼設定：</span><span class="sxs-lookup"><span data-stu-id="002b2-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a><span data-ttu-id="002b2-188">使用 hello Azure 自動化 cmdlet</span><span class="sxs-lookup"><span data-stu-id="002b2-188">Using hello Azure Automation cmdlets</span></span>

<span data-ttu-id="002b2-189">如果 hello PowerShell DSC 本機設定管理員的預設值符合您的使用案例，而且希望 tooonboard 機器同時從提取，並且報告 tooAzure 自動化 DSC，hello Azure 自動化 cmdlet 提供簡化的方法，來產生 hello DSC所需的中繼設定：</span><span class="sxs-lookup"><span data-stu-id="002b2-189">If hello PowerShell DSC Local Configuration Manager defaults match your use case, and you want tooonboard machines such that they both pull from and report tooAzure Automation DSC, hello Azure Automation cmdlets provide a simplified method of generating hello DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="002b2-190">Hello PowerShell 主控台或 PowerShell ISE 中系統管理員身分在中開啟您的本機環境中的機器。</span><span class="sxs-lookup"><span data-stu-id="002b2-190">Open hello PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="002b2-191">TooAzure 資源管理員使用連接**新增 AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="002b2-191">Connect tooAzure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="002b2-192">您想要從 hello 自動化 tooonboard hello 機器帳戶 toowhich 想 tooonboard 節點，請下載 hello PowerShell DSC 中繼設定：</span><span class="sxs-lookup"><span data-stu-id="002b2-192">Download hello PowerShell DSC metaconfigurations for hello machines you want tooonboard from hello Automation account toowhich you want tooonboard nodes:</span></span>

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="002b2-193">您現在應該會有一個名為資料夾***DscMetaConfigs***，包含 hello PowerShell DSC 中繼設定，如 hello 機器 tooonboard （以系統管理員身分）：</span><span class="sxs-lookup"><span data-stu-id="002b2-193">You should now have a folder called ***DscMetaConfigs***, containing hello PowerShell DSC metaconfigurations for hello machines tooonboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="002b2-194">安全註冊</span><span class="sxs-lookup"><span data-stu-id="002b2-194">Secure registration</span></span>

<span data-ttu-id="002b2-195">電腦可以安全地登入 tooan 透過 hello WMF 5 DSC 註冊通訊協定，可讓 DSC 節點 tooauthenticate tooa PowerShell DSC V2 提取或報表伺服器 （包括 Azure Automation DSC） 的 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="002b2-195">Machines can securely onboard tooan Azure Automation account through hello WMF 5 DSC registration protocol, which allows a DSC node tooauthenticate tooa PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="002b2-196">hello 節點註冊 toohello 伺服器**登錄 URL**、 驗證使用**登錄機碼**。</span><span class="sxs-lookup"><span data-stu-id="002b2-196">hello node registers toohello server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="002b2-197">在註冊期間，hello DSC 節點和 DSC 提取/報表伺服器會交涉驗證 toohello 伺服器後註冊此節點 toouse 的唯一憑證。</span><span class="sxs-lookup"><span data-stu-id="002b2-197">During registration, hello DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node toouse for authentication toohello server post-registration.</span></span> <span data-ttu-id="002b2-198">此程序可避免上架的節點彼此模擬，例如當節點遭到入侵並且具有惡意行為。</span><span class="sxs-lookup"><span data-stu-id="002b2-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="002b2-199">註冊後，hello 登錄機碼不會用於驗證一次，並會刪除從 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="002b2-199">After registration, hello Registration key is not used for authentication again, and is deleted from hello node.</span></span>

<span data-ttu-id="002b2-200">您可以取得 hello 資訊所需的 hello DSC 註冊通訊協定從 hello**管理金鑰**hello Azure preview 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="002b2-200">You can get hello information required for hello DSC registration protocol from hello **Manage Keys** blade in hello Azure preview portal.</span></span> <span data-ttu-id="002b2-201">Hello hello 上的索引鍵圖示，即可開啟此刀鋒視窗**Essentials** hello 自動化帳戶的面板。</span><span class="sxs-lookup"><span data-stu-id="002b2-201">Open this blade by clicking hello key icon on hello **Essentials** panel for hello Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="002b2-202">註冊 URL 是 hello 管理金鑰 刀鋒視窗中的 hello URL 欄位。</span><span class="sxs-lookup"><span data-stu-id="002b2-202">Registration URL is hello URL field in hello Manage Keys blade.</span></span>
* <span data-ttu-id="002b2-203">登錄機碼是在 hello 管理金鑰 刀鋒視窗的 hello 主要存取金鑰或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="002b2-203">Registration key is hello Primary Access Key or Secondary Access Key in hello Manage Keys blade.</span></span> <span data-ttu-id="002b2-204">可以使用這兩個金鑰。</span><span class="sxs-lookup"><span data-stu-id="002b2-204">Either key can be used.</span></span>

<span data-ttu-id="002b2-205">為了提高安全性，hello 的自動化帳戶的主要和次要存取金鑰會重新產生在任何時間 (上 hello**管理金鑰**刀鋒視窗) tooprevent 未來的節點註冊使用前一個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="002b2-205">For added security, hello primary and secondary access keys of an Automation account can be regenerated at any time (on hello **Manage Keys** blade) tooprevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="002b2-206">疑難排解 Azure 虛擬機器上架</span><span class="sxs-lookup"><span data-stu-id="002b2-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="002b2-207">Azure Automation DSC 可讓您輕鬆地將 Azure Windows VM 上架以進行組態管理。</span><span class="sxs-lookup"><span data-stu-id="002b2-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="002b2-208">Hello 幕後 hello Azure VM Desired State Configuration 延伸模組會為使用的 tooregister hello 向 Azure 自動化 DSC VM。</span><span class="sxs-lookup"><span data-stu-id="002b2-208">Under hello hood, hello Azure VM Desired State Configuration extension is used tooregister hello VM with Azure Automation DSC.</span></span> <span data-ttu-id="002b2-209">Hello Azure VM Desired State Configuration 延伸模組會以非同步方式執行，因為追蹤進度及疑難排解其執行可能很重要。</span><span class="sxs-lookup"><span data-stu-id="002b2-209">Since hello Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="002b2-210">上架 Azure Windows VM tooAzure Automation DSC 使用 hello Azure VM Desired State Configuration 延伸模組可能需要向上 hello 節點 tooshow tooan 小時註冊 Azure 自動化中的任何方法。</span><span class="sxs-lookup"><span data-stu-id="002b2-210">Any method of onboarding an Azure Windows VM tooAzure Automation DSC that uses hello Azure VM Desired State Configuration extension could take up tooan hour for hello node tooshow up as registered in Azure Automation.</span></span> <span data-ttu-id="002b2-211">這是因為 Windows Management Framework 5.0 上 hello VM hello Azure VM DSC 延伸模組，這是必要的 tooonboard hello VM tooAzure Automation DSC toohello 安裝。</span><span class="sxs-lookup"><span data-stu-id="002b2-211">This is due toohello installation of Windows Management Framework 5.0 on hello VM by hello Azure VM DSC extension, which is required tooonboard hello VM tooAzure Automation DSC.</span></span>

<span data-ttu-id="002b2-212">hello hello Azure 入口網站中的 Azure VM Desired State Configuration 延伸模組或檢視表 tootroubleshoot hello 狀態瀏覽 toohello 進行入門訓練的 VM，然後按一下-> **所有設定** -> **擴充功能**  ->  **DSC**。</span><span class="sxs-lookup"><span data-stu-id="002b2-212">tootroubleshoot or view hello status of hello Azure VM Desired State Configuration extension, in hello Azure portal navigate toohello VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="002b2-213">如需詳細資訊，您可以按一下 [檢視詳細狀態] 。</span><span class="sxs-lookup"><span data-stu-id="002b2-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="002b2-214">憑證到期日和重新註冊</span><span class="sxs-lookup"><span data-stu-id="002b2-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="002b2-215">註冊 Azure Automation DSC 的 DSC 節點的電腦之後, 有一些情況下您可能必須 tooreregister hello 中的該節點未來：</span><span class="sxs-lookup"><span data-stu-id="002b2-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need tooreregister that node in hello future:</span></span>

* <span data-ttu-id="002b2-216">在註冊之後，每個節點會自動交涉唯一的驗證憑證，該憑證於一年之後到期。</span><span class="sxs-lookup"><span data-stu-id="002b2-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="002b2-217">目前，當它們即將到期，所以您一年的時間之後需要 tooreregister hello 節點 hello PowerShell DSC 註冊通訊協定無法自動更新憑證。</span><span class="sxs-lookup"><span data-stu-id="002b2-217">Currently, hello PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need tooreregister hello nodes after a year's time.</span></span> <span data-ttu-id="002b2-218">在重新登錄之前，請確定每個節點都正在執行 Windows Management Framework 5.0 RTM。</span><span class="sxs-lookup"><span data-stu-id="002b2-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="002b2-219">如果節點的驗證憑證過期，而且 hello 節點未重新註冊，hello 節點將無法與 Azure 自動化 toocommunicate，且將標示為 '無回應。'</span><span class="sxs-lookup"><span data-stu-id="002b2-219">If a node's authentication certificate expires, and hello node is not reregistered, hello node will be unable toocommunicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="002b2-220">更新間隔執行 90 天，或小於 hello 憑證到期時間，或在任何時間點 hello 憑證到期時間之後, 將會導致正在產生和使用新的憑證。</span><span class="sxs-lookup"><span data-stu-id="002b2-220">Reregistration performed 90 days or less from hello certificate expiration time, or at any point after hello certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="002b2-221">toochange 任何[PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)hello 節點，例如 ConfigurationMode 初始註冊期間設定的。</span><span class="sxs-lookup"><span data-stu-id="002b2-221">toochange any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of hello node, such as ConfigurationMode.</span></span> <span data-ttu-id="002b2-222">目前，這些 DSC 代理程式值只可以透過重新註冊變更。</span><span class="sxs-lookup"><span data-stu-id="002b2-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="002b2-223">hello 有一個例外狀況為 hello 分派 toohello 節點的節點組態--這可以在 Azure Automation DSC 直接變更。</span><span class="sxs-lookup"><span data-stu-id="002b2-223">hello one exception is hello Node Configuration assigned toohello node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="002b2-224">可以在 hello 本文描述您註冊 hello 節點一開始，使用任何 hello 入門訓練方法的相同方式執行登錄。</span><span class="sxs-lookup"><span data-stu-id="002b2-224">Reregistration can be performed in hello same way you registered hello node initially, using any of hello onboarding methods described in this document.</span></span> <span data-ttu-id="002b2-225">您不需要 toounregister 從 Azure Automation DSC 的節點然後再重新登錄它。</span><span class="sxs-lookup"><span data-stu-id="002b2-225">You do not need toounregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="002b2-226">相關文章</span><span class="sxs-lookup"><span data-stu-id="002b2-226">Related Articles</span></span>

* [<span data-ttu-id="002b2-227">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="002b2-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="002b2-228">Azure 自動化 DSC Cmdlet</span><span class="sxs-lookup"><span data-stu-id="002b2-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="002b2-229">Azure 自動化 DSC 價格</span><span class="sxs-lookup"><span data-stu-id="002b2-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
