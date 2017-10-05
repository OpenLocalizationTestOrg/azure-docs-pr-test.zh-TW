---
title: "在 VM 上安裝 Trend Micro Deep Security | Microsoft Docs"
description: "本文說明如何在 Azure 中，在以傳統部署模型建立的 VM 上安裝和設定 Trend Micro 安全性。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="821e4-103">如何在 Windows VM 上安裝和設定 Trend Micro Deep Security as a Service</span><span class="sxs-lookup"><span data-stu-id="821e4-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="821e4-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="821e4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="821e4-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="821e4-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="821e4-106">Microsoft 建議讓大部分的新部署使用 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="821e4-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="821e4-107">本文說明如何在執行 Windows Server 的新或現有虛擬機器 (VM) 上，安裝和設定 Trend Micro Deep Security as a Service。</span><span class="sxs-lookup"><span data-stu-id="821e4-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="821e4-108">Deep Security as a Service 包括反惡意程式碼防護、防火牆、入侵防禦系統及完整監視。</span><span class="sxs-lookup"><span data-stu-id="821e4-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="821e4-109">透過 VM 代理程式，用戶端會安裝為安全性延伸模組。</span><span class="sxs-lookup"><span data-stu-id="821e4-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="821e4-110">在新的虛擬機器上，您將安裝 Deep Security Agent，因為 Azure 入口網站會自動建立 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="821e4-111">使用傳統入口網站、Azure CLI 或 PowerShell 建立的現有 VM 可能沒有 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="821e4-112">對於沒有 VM 代理程式的現有虛擬機器，您必須先下載與安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="821e4-113">本文將探討這兩種狀況。</span><span class="sxs-lookup"><span data-stu-id="821e4-113">This article covers both situations.</span></span>

<span data-ttu-id="821e4-114">如果您已有 Trend Micro 的內部部署解決方案的目前訂用帳戶，您可以用它來協助保護 Azure 虛擬機器的安全。</span><span class="sxs-lookup"><span data-stu-id="821e4-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="821e4-115">如果您還不是 Symantec 客戶，您可以註冊試用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="821e4-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="821e4-116">如需有關此解決方案的詳細資訊，請參閱 Trend Micro 部落格文章 [適用於 Deep Security 的 Microsoft Azure VM 代理程式延伸模組](http://go.microsoft.com/fwlink/p/?LinkId=403945)。</span><span class="sxs-lookup"><span data-stu-id="821e4-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="821e4-117">在新的 VM 上安裝 Deep Security 代理程式</span><span class="sxs-lookup"><span data-stu-id="821e4-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="821e4-118">當您使用來自 **Marketplace** 的映像建立虛擬機器時，[Azure 入口網站](http://portal.azure.com)可讓您安裝 Trend Micro 安全性擴充功能。</span><span class="sxs-lookup"><span data-stu-id="821e4-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="821e4-119">如果您打算建立單一虛擬機器，使用此入口網站可輕易地新增 Trend Micro 的防護。</span><span class="sxs-lookup"><span data-stu-id="821e4-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="821e4-120">使用來自 **Marketplace** 的項目會開啟能協助您設定虛擬機器的精靈。</span><span class="sxs-lookup"><span data-stu-id="821e4-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="821e4-121">您會使用精靈中的第三個面板 [設定] 刀鋒視窗，來安裝 Trend Micro 安全性擴充功能。</span><span class="sxs-lookup"><span data-stu-id="821e4-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="821e4-122">如需一般指示，請參閱[在 Azure 入口網站中建立執行 Windows 的虛擬機器](tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="821e4-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="821e4-123">當您進入精靈的**設定**刀鋒視窗時，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="821e4-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="821e4-124">按一下 [擴充功能]，然後在下一個窗格中按一下 [新增擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="821e4-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![開始新增擴充功能][1]

2. <span data-ttu-id="821e4-126">在 [新增資源] 窗格中選取 [Deep Security 代理程式]。</span><span class="sxs-lookup"><span data-stu-id="821e4-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="821e4-127">在 [Deep Security 代理程式] 窗格中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="821e4-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![識別 Deep Security Agent][2]

3. <span data-ttu-id="821e4-129">輸入擴充功能的**租用戶識別碼**和**租用戶啟用密碼**。</span><span class="sxs-lookup"><span data-stu-id="821e4-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="821e4-130">您可以選擇性地輸入**安全性原則識別碼**。</span><span class="sxs-lookup"><span data-stu-id="821e4-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="821e4-131">然後按一下 [確定] 來新增用戶端。</span><span class="sxs-lookup"><span data-stu-id="821e4-131">Then, click **OK** to add the client.</span></span>

   ![提供擴充功能詳細資料][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="821e4-133">在現有 VM 上安裝 Deep Security 代理程式</span><span class="sxs-lookup"><span data-stu-id="821e4-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="821e4-134">若要在現有的 VM 上安裝代理程式，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="821e4-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="821e4-135">在本機電腦上安裝 Azure PowerShell 模組 0.8.2 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="821e4-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="821e4-136">您可以使用 **Get-Module azure | format-table version** 命令來檢查已安裝的 Azure PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="821e4-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="821e4-137">如需最新版本的指示與連結，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="821e4-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="821e4-138">使用 `Add-AzureAccount`登入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="821e4-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="821e4-139">在目標虛擬機器上安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="821e4-140">首先，確認已安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="821e4-141">填寫雲端服務名稱和虛擬機器名稱，然後在系統管理員層級 Azure PowerShell 命令提示字元上執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="821e4-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="821e4-142">取代括弧內 (包括 < 和 > 字元) 的所有項目。</span><span class="sxs-lookup"><span data-stu-id="821e4-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="821e4-143">如果您不知道雲端服務和虛擬機器名稱，請執行 **Get-AzureVM** ，來顯示目前訂用帳戶中所有虛擬機器的該項資訊。</span><span class="sxs-lookup"><span data-stu-id="821e4-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="821e4-144">如果 **write-host** 命令傳回 **True**，則會安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="821e4-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="821e4-145">如果傳回 **False**,，請參閱 Azure 部落格文章 [VM 代理程式與延伸模組 - 第 2 部分](http://go.microsoft.com/fwlink/p/?LinkId=403947)中的指示和下載連結。</span><span class="sxs-lookup"><span data-stu-id="821e4-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="821e4-146">如果已安裝 VM 代理程式，請執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="821e4-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="821e4-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="821e4-147">Next steps</span></span>
<span data-ttu-id="821e4-148">讓代理程式安裝並開始執行需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="821e4-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="821e4-149">之後，您必須在虛擬機器上啟用 Deep Security，才能由 Deep Security Manager 進行管理。</span><span class="sxs-lookup"><span data-stu-id="821e4-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="821e4-150">如需其他指示，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="821e4-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="821e4-151">與此解決方案相關的 Trend 文章： [Microsoft Azure 的即時雲端安全性](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="821e4-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="821e4-152">設定虛擬機器的 [Windows PowerShell 指令碼範例](http://go.microsoft.com/fwlink/?LinkId=404100)</span><span class="sxs-lookup"><span data-stu-id="821e4-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="821e4-153">[指示](http://go.microsoft.com/fwlink/?LinkId=404099) </span><span class="sxs-lookup"><span data-stu-id="821e4-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="821e4-154">其他資源</span><span class="sxs-lookup"><span data-stu-id="821e4-154">Additional resources</span></span>
<span data-ttu-id="821e4-155">[如何登入執行 Windows Server 的虛擬機器]</span><span class="sxs-lookup"><span data-stu-id="821e4-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="821e4-156">[Azure VM 延伸模組與功能]</span><span class="sxs-lookup"><span data-stu-id="821e4-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="821e4-157">[如何登入執行 Windows Server 的虛擬機器]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="821e4-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="821e4-158">[Azure VM 延伸模組與功能]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="821e4-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>
