---
title: "將由 Azure 自動化 DSC 管理的機器上架 | Microsoft Docs"
description: "如何設定機器以使用 Azure 自動化 DSC 管理"
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
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="6ab4a-103">上架由 Azure 自動化 DSC 管理的機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="6ab4a-104">為什麼要使用 Azure 自動化 DSC 管理機器？</span><span class="sxs-lookup"><span data-stu-id="6ab4a-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="6ab4a-105">如同 [PowerShell 期望的狀態設定](https://technet.microsoft.com/library/dn249912.aspx)，Azure 自動化期望的狀態設定在任何雲端或內部部署資料中心中是 DSC 節點 (實體和虛擬機器) 的一個簡單但強大的組態管理服務。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="6ab4a-106">它可讓您從中央、安全的位置快速且輕鬆地延展性到數千部電腦。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="6ab4a-107">您可以輕鬆地上架機器、指派它們宣告式組態和檢視顯示每個電腦的符合性報告 (達您指定的所需狀態)。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="6ab4a-108">Azure 自動化 DSC 管理層之於 DSC 如同 Azure 自動化管理層之於 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="6ab4a-109">換句話說，「Azure 自動化」會以協助您管理 Powershell 指令碼的相同方式，同樣協助您管理 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="6ab4a-110">若要深入了解使用 Azure Automation DSC 的優點，請參閱 [Azure Automation DSC 概觀](automation-dsc-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="6ab4a-111">Azure 自動化 DSC 可以用來管理各種不同的機器：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="6ab4a-112">Azure 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="6ab4a-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="6ab4a-113">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-113">Azure virtual machines</span></span>
* <span data-ttu-id="6ab4a-114">Amazon Web Services (AWS) 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="6ab4a-115">位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="6ab4a-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="6ab4a-116">位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="6ab4a-117">此外，如果您不準備從雲端管理機器組態，Azure Automation DSC 也可用來當做報告專用端點。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="6ab4a-118">這可讓您透過 DSC 內部部署設定 (推送) 所需的組態，以及檢視與 Azure 自動化中的期望狀態相符節點的豐富報告詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="6ab4a-119">下列各節概述如何將每個類型的機器上架到 Azure 自動化 DSC。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="6ab4a-120">Azure 虛擬機器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="6ab4a-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="6ab4a-121">利用 Azure 自動化 DSC，您可以輕鬆上架 Azure 虛擬機器 (傳統)，以使用 Azure 入口網站或 PowerShell 進行組態管理。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="6ab4a-122">在幕後並且不需要系統管理員遠端連至 VM 的情況下，Azure VM 期望的狀態組態延伸模組會向 Azure 自動化 DSC 註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="6ab4a-123">因為 Azure VM 預期狀態設定延伸模組是以非同步方式執行，以下的 [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6ab4a-124">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6ab4a-124">Azure portal</span></span>

<span data-ttu-id="6ab4a-125">在 [Azure 入口網站](http://portal.azure.com/)中，按一下 [瀏覽] -> [虛擬機器 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="6ab4a-126">選取您要上架的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="6ab4a-127">在虛擬機器的儀表板刀鋒視窗上，按一下 [所有設定] -> [擴充功能] -> [新增] -> [Azure Automation DSC] -> [建立]。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="6ab4a-128">輸入您的使用情況所需的 [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4)、自動化帳戶的註冊金鑰和註冊 URL，並選擇性地輸入要指派給 VM 的節點組態。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="6ab4a-129">若要找出自動化帳戶所要上架機器的註冊 URL 與金鑰，請查看以下的 [**安全註冊**](#secure-registration) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="6ab4a-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ab4a-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
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

## <a name="azure-virtual-machines"></a><span data-ttu-id="6ab4a-131">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-131">Azure virtual machines</span></span>

<span data-ttu-id="6ab4a-132">Azure 自動化 DSC 可讓您輕鬆上架 Azure 虛擬機器以進行組態管理，請使用 Azure 入口網站、Azure 資源管理員範本或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="6ab4a-133">在幕後並且不需要系統管理員遠端連至 VM 的情況下，Azure VM 期望的狀態組態延伸模組會向 Azure 自動化 DSC 註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="6ab4a-134">因為 Azure VM 預期狀態設定延伸模組是以非同步方式執行，以下的 [**疑難排解 Azure 虛擬機器上架**](#troubleshooting-azure-virtual-machine-onboarding) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6ab4a-135">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6ab4a-135">Azure portal</span></span>

<span data-ttu-id="6ab4a-136">在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您想要佈建虛擬機器的「Azure 自動化」帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="6ab4a-137">在 [自動化帳戶] 儀表板上，按一下 [DSC 節點] -> [新增 Azure VM]。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="6ab4a-138">在 [選取要上架的虛擬機器] 下，選取一或多個要上架的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="6ab4a-139">在 [設定註冊資料] 下，輸入您的使用情況所需的 [PowerShell DSC 本機設定管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4) ，並選擇性地輸入要指派給 VM 的節點組態。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="6ab4a-140">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="6ab4a-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="6ab4a-141">您可以透過 Azure 資源管理員範本部署 Azure 虛擬機器和上架到 Azure 自動化 DSC。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="6ab4a-142">如需將現有的 VM 上架到 Azure Automation DSC 的範例範本，請參閱 [透過 DSC 延伸模組和 Azure Automation DSC 設定 VM](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="6ab4a-143">若要尋找註冊金鑰和註冊 URL 做為此範本中的輸入，請參閱以下的 [**安全註冊**](#secure-registration) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="6ab4a-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ab4a-144">PowerShell</span></span>

<span data-ttu-id="6ab4a-145">您可以透過 PowerShell 使用 [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) Cmdlet 在 Azure 入口網站中佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="6ab4a-146">Amazon Web Services (AWS) 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="6ab4a-147">您可以使用 AWS DSC Toolkit 輕鬆加入 Amazon Web Services 虛擬機器，讓 Azure 自動化 DSC 管理組態。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="6ab4a-148">您可以在 [這裡](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/)深入了解工具組。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="6ab4a-149">位於內部部署或 Azure/AWS 以外之雲端中的實體/虛擬 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="6ab4a-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="6ab4a-150">內部部署 Windows 電腦和非 Azure 雲端中的 Windows 電腦 (例如 Amazon Web Services) 也可以上架到 Azure 自動化 DSC，只要它們對外可存取網際網路，透過一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="6ab4a-151">確定在您想要上架到 Azure Automation DSC 的電腦上已安裝最新版的 [WMF 5](http://aka.ms/wmf5latest) 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="6ab4a-152">請依照下列 [**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations) 一節中的指示，來產生包含所需 DSC 中繼設定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="6ab4a-153">從遠端將 PowerShell DSC 中繼設定套用至您想要上架的電腦。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="6ab4a-154">**執行此命令的電腦必須安裝最新版的 [WMF 5](http://aka.ms/wmf5latest)** ：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="6ab4a-155">如果您無法從遠端套用 PowerShell DSC 中繼設定，請將步驟 2 中繼設定的資料夾複製到每一部要上架的電腦。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="6ab4a-156">然後在要上架的每台電腦本機上呼叫 **Set-DscLocalConfigurationManager** 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="6ab4a-157">使用 Azure 入口網站或 Cmdlet，檢查要上架的電腦現在在您的 Azure 自動化帳戶中顯示為已註冊的 DSC 節點。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="6ab4a-158">位於內部部署、Azure 或 Azure 以外之雲端中的實體/虛擬 Linux 機器</span><span class="sxs-lookup"><span data-stu-id="6ab4a-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="6ab4a-159">內部部署 Linux 電腦、Azure 中的 Linux 電腦和非 Azure 雲端中的 Linux 電腦也可以上架到 Azure Automation DSC，只要它們對外可存取網際網路，透過一些簡單的步驟：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="6ab4a-160">確定在您想要在 Azure 自動化 DSC 上線的電腦上已安裝最新版的 [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux)。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="6ab4a-161">如果 [PowerShell DSC 本機設定管理員的預設值](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 符合您的使用案例，且您想要將電腦上架 **同時** 從 Azure 自動化 DSC 提取並報告：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="6ab4a-162">在要上架到 Azure 自動化 DSC 的每部 Linux 電腦上，使用 Register.py 來使用 PowerShell DSC 本機組態管理員預設值上架：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="6ab4a-163">若要尋找您的自動化帳戶的註冊金鑰和註冊 URL，請參閱以下的 [**安全註冊**](#secure-registration) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="6ab4a-164">如果 PowerShell DSC 本機設定管理員的預設值**不**符合您的使用案例，或者您希望將電腦上架，使其只向 Azure Automation DSC 報告，但不從中提取設定或 PowerShell 模組，請依照步驟 3 - 6 執行。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="6ab4a-165">否則，請直接跳到步驟 6。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="6ab4a-166">請依照下列 [**產生 DSC 中繼設定**](#generating-dsc-metaconfigurations) 一節中的指示，來產生包含所需 DSC 中繼設定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="6ab4a-167">從遠端將 PowerShell DSC metaconfiguration 套用至您想要上架的電腦：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="6ab4a-168">執行此命令的電腦必須安裝最新版的 [WMF 5](http://aka.ms/wmf5latest) 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="6ab4a-169">如果您無法從遠端套用 PowerShell DSC 中繼設定，針對要上架的每部 Linux 電腦，請從步驟 5 的資料夾複製對應於該電腦的中繼組態到 Linux 電腦。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="6ab4a-170">然後在您要上架到 Azure Automation DSC 的每個 Linux 電腦本機上呼叫 `SetDscLocalConfigurationManager.py` ：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="6ab4a-171">使用 Azure 入口網站或 Cmdlet，檢查要上架的電腦現在在您的 Azure 自動化帳戶中顯示為已註冊的 DSC 節點。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="6ab4a-172">產生 DSC 中繼設定</span><span class="sxs-lookup"><span data-stu-id="6ab4a-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="6ab4a-173">若要以一般方式將任何電腦上架至 Azure Automation DSC，可產生套用時會告知電腦上的 DSC 代理程式從 Azure Automation DSC 提取且/或報告的 [DSC 中繼設定](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig)。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="6ab4a-174">Azure 自動化 DSC 的 DSC 中繼設定可以使用 PowerShell DSC 設定或 Azure 自動化 PowerShell Cmdlet 產生。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab4a-175">DSC 中繼設定包含將電腦上架至進行管理之自動化帳戶的機密資料。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="6ab4a-176">請務必適當地保護您所建立的任何 DSC 中繼設定，或在使用後將它們刪除。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="6ab4a-177">使用 DSC 設定</span><span class="sxs-lookup"><span data-stu-id="6ab4a-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="6ab4a-178">在您的本機環境中，以電腦的系統管理員身分開啟 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="6ab4a-179">電腦必須安裝最新版本的 [WMF 5](http://aka.ms/wmf5latest) 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="6ab4a-180">在本機複製下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-180">Copy the following script locally.</span></span> <span data-ttu-id="6ab4a-181">此指令碼包含用來建立中繼設定的 PowerShell DSC 設定，以及開始執行中繼設定建立作業的命令。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
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

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="6ab4a-182">填寫您自動化帳戶的註冊金鑰和 URL，以及要上架的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="6ab4a-183">所有其他參數都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-183">All other parameters are optional.</span></span> <span data-ttu-id="6ab4a-184">若要尋找您的自動化帳戶的註冊金鑰和註冊 URL，請參閱以下的 [**安全註冊**](#secure-registration) 一節會提供追蹤其進度或疑難排解的步驟。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="6ab4a-185">如果您希望電腦向 Azure 自動化 DSC 報告 DSC 狀態資訊，但不提取設定或 PowerShell 模組，請將 **ReportOnly** 參數設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="6ab4a-186">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-186">Run the script.</span></span> <span data-ttu-id="6ab4a-187">您現在工作目錄中應該有一個名為 **DscMetaConfigs** 的資料夾，其中包含要上架之電腦的 PowerShell DSC 中繼設定 (以系統管理員身分)：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="6ab4a-188">使用 Azure 自動化 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6ab4a-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="6ab4a-189">如果 PowerShell DSC 本機設定管理員的預設值符合您的使用案例，且您想要將電腦上架同時從 Azure 自動化 DSC 提取並報告，Azure 自動化 Cmdlet 會提供簡單的方法，來產生所需的 DSC 中繼設定：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="6ab4a-190">在您的本機環境的機器中，以系統管理員身分開啟 PowerShell 主控台或 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="6ab4a-191">使用 **Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="6ab4a-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="6ab4a-192">從您要上架節點的目標自動化帳戶下載您想要上架之電腦的 PowerShell DSC 中繼設定：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="6ab4a-193">您現在應該有一個名為 ***DscMetaConfigs*** 的資料夾，其中包含要上架之電腦的 PowerShell DSC 中繼設定 (以系統管理員身分)：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="6ab4a-194">安全註冊</span><span class="sxs-lookup"><span data-stu-id="6ab4a-194">Secure registration</span></span>

<span data-ttu-id="6ab4a-195">機器可以透過 WMF 5 DSC 註冊通訊協定安全地上架到 Azure 自動化帳戶，如此可讓 DSC 節點向 PowerShell DSC V2 提取或報表伺服器 (包括 Azure 自動化 DSC) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="6ab4a-196">節點會在**註冊 URL** 時向伺服器註冊，並使用**註冊金鑰**進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="6ab4a-197">在註冊期間，DSC 節點和 DSC 提取/報告伺服器會交涉獨特的憑證，讓此節點在註冊伺服器用於進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="6ab4a-198">此程序可避免上架的節點彼此模擬，例如當節點遭到入侵並且具有惡意行為。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="6ab4a-199">註冊之後，註冊金鑰不會再次用於驗證，並且會從節點中刪除。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="6ab4a-200">您可以從 Azure Preview 入口網站的 [管理金鑰]  刀鋒視窗取得 DSC 註冊通訊協定所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="6ab4a-201">在自動化帳戶的 [基本功能]  面板按一下金鑰圖示，可開啟此刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="6ab4a-202">「註冊 URL」是 [管理金鑰] 刀鋒視窗中的 [URL] 欄位。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="6ab4a-203">「註冊金鑰」是 [管理金鑰] 刀鋒視窗中的主要存取金鑰或次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="6ab4a-204">可以使用這兩個金鑰。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-204">Either key can be used.</span></span>

<span data-ttu-id="6ab4a-205">為了提高安全性，自動化帳戶的主要和次要存取金鑰可以隨時重新產生 (在 [管理金鑰]  刀鋒視窗上)，以避免未來的節點使用先前的金鑰註冊。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="6ab4a-206">疑難排解 Azure 虛擬機器上架</span><span class="sxs-lookup"><span data-stu-id="6ab4a-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="6ab4a-207">Azure Automation DSC 可讓您輕鬆地將 Azure Windows VM 上架以進行組態管理。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="6ab4a-208">在幕後，Azure VM 期望的狀態組態延伸模組是用來向 Azure 自動化 DSC 註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="6ab4a-209">因為 Azure VM 期望的狀態組態延伸模組是以非同步方式執行，追蹤其進度和疑難排解其執行可能很重要。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab4a-210">將 Azure Windows VM 上架到使用 Azure VM 期望的狀態組態延伸模組的 Azure 自動化 DSC 的任何方法，最多可能需要一小時的時間，節點才會顯示為已在 Azure 自動化中註冊。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="6ab4a-211">這是因為 VM 上憑藉著 Azure VM DSC 延伸模組的 Windows Management Framework 5.0 安裝，需要它才能將 VM 上架到 Azure 自動化 DSC。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="6ab4a-212">若要對「Azure VM 預期狀態設定」擴充功能的狀態進行疑難排解或檢視，請在 Azure 入口網站中，瀏覽至要上架的 VM，然後按一下 -> [所有設定] -> [擴充功能] -> [DSC]。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="6ab4a-213">如需詳細資訊，您可以按一下 [檢視詳細狀態] 。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="6ab4a-214">憑證到期日和重新註冊</span><span class="sxs-lookup"><span data-stu-id="6ab4a-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="6ab4a-215">在將機器註冊為 Azure Automation DSC 中的 DSC 節點之後，有數種原因讓您可能需要在未來重新註冊該節點：</span><span class="sxs-lookup"><span data-stu-id="6ab4a-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="6ab4a-216">在註冊之後，每個節點會自動交涉唯一的驗證憑證，該憑證於一年之後到期。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="6ab4a-217">目前，當憑證即將過期時，PowerShell DSC 註冊通訊協定便無法自動更新憑證，因此您必須在一年之後重新註冊這些節點。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="6ab4a-218">在重新登錄之前，請確定每個節點都正在執行 Windows Management Framework 5.0 RTM。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="6ab4a-219">如果節點的驗證憑證過期，而且該節點尚未註冊，則該節點將無法與 Azure 自動化通訊，並將標示為「未回應」。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="6ab4a-220">與憑證到期時間相距 90 天或更短時間內執行的註冊，或是憑證到期時間之後任何時間點執行的註冊，將會產生新的憑證並予以使用。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="6ab4a-221">變更在節點初始註冊期間設定的任何 [PowerShell DSC 本機組態管理員值](https://msdn.microsoft.com/powershell/dsc/metaconfig4) ，例如 ConfigurationMode。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="6ab4a-222">目前，這些 DSC 代理程式值只可以透過重新註冊變更。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="6ab4a-223">其中一個例外是指派給節點的節點組態 - 它可以在 Azure Automation DSC 中直接變更。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="6ab4a-224">重新註冊可以用您初始註冊節點的相同方法執行，使用這份文件中所述的任何上架方法。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="6ab4a-225">重新註冊節點之前，您不需要從 Azure Automation DSC 取消註冊節點。</span><span class="sxs-lookup"><span data-stu-id="6ab4a-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6ab4a-226">相關文章</span><span class="sxs-lookup"><span data-stu-id="6ab4a-226">Related Articles</span></span>

* [<span data-ttu-id="6ab4a-227">Azure 自動化 DSC 概觀</span><span class="sxs-lookup"><span data-stu-id="6ab4a-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="6ab4a-228">Azure 自動化 DSC Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6ab4a-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="6ab4a-229">Azure 自動化 DSC 價格</span><span class="sxs-lookup"><span data-stu-id="6ab4a-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
