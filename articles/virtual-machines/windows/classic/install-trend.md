---
title: "在 VM 上 Trend Micro Deep Security aaaInstall |Microsoft 文件"
description: "本文說明如何 tooinstall 和設定 Trend 安全性與 hello 傳統部署模型，在 Azure 中建立的 VM 上。"
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
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="eeea9-103">如何 tooinstall 和設定 Trend Micro Deep Security 作為 Windows VM 上的服務</span><span class="sxs-lookup"><span data-stu-id="eeea9-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eeea9-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="eeea9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eeea9-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="eeea9-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="eeea9-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="eeea9-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="eeea9-107">本文章將示範如何 tooinstall 和設定 Trend Micro Deep Security 作為新的或現有虛擬機器 (VM) 執行 Windows Server 上的服務。</span><span class="sxs-lookup"><span data-stu-id="eeea9-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="eeea9-108">Deep Security as a Service 包括反惡意程式碼防護、防火牆、入侵防禦系統及完整監視。</span><span class="sxs-lookup"><span data-stu-id="eeea9-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="eeea9-109">hello 用戶端會安裝為透過 hello VM 代理程式的安全性延伸模組。</span><span class="sxs-lookup"><span data-stu-id="eeea9-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="eeea9-110">新的虛擬機器中，您可以安裝 hello Deep Security Agent，為 hello hello Azure 入口網站所自動建立 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eeea9-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="eeea9-111">現有的 VM 使用 hello 傳統入口網站、 hello Azure CLI 或 PowerShell 建立可能沒有 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eeea9-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="eeea9-112">現有的虛擬機器沒有 hello VM 代理程式，您需要 toodownload 與先安裝它。</span><span class="sxs-lookup"><span data-stu-id="eeea9-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="eeea9-113">本文將探討這兩種狀況。</span><span class="sxs-lookup"><span data-stu-id="eeea9-113">This article covers both situations.</span></span>

<span data-ttu-id="eeea9-114">如果您有目前訂用帳戶趨勢科技從內部部署解決方案，您可以使用 toohelp 保護您的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eeea9-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="eeea9-115">如果您還不是 Symantec 客戶，您可以註冊試用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eeea9-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="eeea9-116">如需此解決方案的詳細資訊，請參閱 hello 趨勢科技部落格文章[Microsoft Azure VM 代理程式延伸模組的 Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945)。</span><span class="sxs-lookup"><span data-stu-id="eeea9-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="eeea9-117">在新的 VM 上安裝 hello Deep Security Agent</span><span class="sxs-lookup"><span data-stu-id="eeea9-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="eeea9-118">hello [Azure 入口網站](http://portal.azure.com)可讓您安裝 hello 趨勢科技安全性延伸模組，當您使用映像從 hello **Marketplace** toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eeea9-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="eeea9-119">如果您要建立單一的虛擬機器，使用 hello 入口網站是從趨勢科技輕鬆 tooadd 保護。</span><span class="sxs-lookup"><span data-stu-id="eeea9-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="eeea9-120">使用的項目從 hello **Marketplace**開啟精靈，可協助您設定 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eeea9-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="eeea9-121">使用 hello**設定**刀鋒視窗，hello hello 精靈 tooinstall hello 趨勢科技安全性延伸模組的第三個的面板。</span><span class="sxs-lookup"><span data-stu-id="eeea9-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="eeea9-122">一般指示，請參閱[建立執行 Windows hello Azure 入口網站中的虛擬機器](tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="eeea9-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="eeea9-123">當您取得 toohello**設定**刀鋒視窗中的 hello 精靈 中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="eeea9-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="eeea9-124">按一下**延伸**，然後按一下 **將延伸加入**hello 下一個窗格中。</span><span class="sxs-lookup"><span data-stu-id="eeea9-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![開始加入 hello 延伸模組][1]

2. <span data-ttu-id="eeea9-126">選取**Deep Security Agent**在 hello**新資源**窗格。</span><span class="sxs-lookup"><span data-stu-id="eeea9-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="eeea9-127">在 hello Deep Security Agent 窗格中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="eeea9-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![識別 Deep Security Agent][2]

3. <span data-ttu-id="eeea9-129">輸入 hello**租用戶識別碼**和**租用戶啟用密碼**hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="eeea9-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="eeea9-130">您可以選擇性地輸入**安全性原則識別碼**。</span><span class="sxs-lookup"><span data-stu-id="eeea9-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="eeea9-131">然後，按一下 **確定**tooadd hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="eeea9-131">Then, click **OK** tooadd hello client.</span></span>

   ![提供擴充功能詳細資料][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="eeea9-133">在現有的 VM 上安裝 hello Deep Security Agent</span><span class="sxs-lookup"><span data-stu-id="eeea9-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="eeea9-134">現有的 VM 上 tooinstall hello 代理程式，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="eeea9-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="eeea9-135">hello Azure PowerShell 模組、 0.8.2 版或更新版本，已安裝在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="eeea9-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="eeea9-136">您可以檢查 hello 版本的 Azure PowerShell，您已安裝使用 hello **Get-module azure | 格式資料表版本**命令。</span><span class="sxs-lookup"><span data-stu-id="eeea9-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="eeea9-137">如需指示和連結 toohello 最新版本，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="eeea9-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="eeea9-138">登入 tooyour Azure 訂用帳戶使用`Add-AzureAccount`。</span><span class="sxs-lookup"><span data-stu-id="eeea9-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="eeea9-139">hello hello 目標虛擬機器上安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eeea9-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="eeea9-140">首先，確認已安裝 VM 代理程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="eeea9-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="eeea9-141">填寫 hello 雲端服務名稱和虛擬機器名稱，然後執行下列命令，以系統管理員層級 Azure PowerShell 命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="eeea9-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="eeea9-142">取代 hello 引號，包括 hello < 和 > 字元內的所有內容。</span><span class="sxs-lookup"><span data-stu-id="eeea9-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="eeea9-143">如果您不知道 hello 雲端服務和虛擬機器名稱，執行**Get-azurevm** toodisplay 所有資訊都 hello 您目前的訂用帳戶中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eeea9-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="eeea9-144">如果 hello**寫入主機**命令會傳回**True**，hello 安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eeea9-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="eeea9-145">如果它傳回**False**，請參閱 hello 指示與下載 hello Azure 部落格文章中的連結 toohello [VM 代理程式和擴充功能-第 2 部分](http://go.microsoft.com/fwlink/p/?LinkId=403947)。</span><span class="sxs-lookup"><span data-stu-id="eeea9-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="eeea9-146">如果已安裝 VM 代理程式 hello，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="eeea9-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="eeea9-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eeea9-147">Next steps</span></span>
<span data-ttu-id="eeea9-148">花幾分鐘，讓 hello 代理程式 toostart 安裝時執行。</span><span class="sxs-lookup"><span data-stu-id="eeea9-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="eeea9-149">在這之後，您會需要 tooactivate Deep Security hello 虛擬機器上的，它可以管理由深層安全性管理員。</span><span class="sxs-lookup"><span data-stu-id="eeea9-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="eeea9-150">請參閱下列文章以取得其他指示的 hello:</span><span class="sxs-lookup"><span data-stu-id="eeea9-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="eeea9-151">與此解決方案相關的 Trend 文章： [Microsoft Azure 的即時雲端安全性](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="eeea9-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="eeea9-152">A[範例 Windows PowerShell 指令碼](http://go.microsoft.com/fwlink/?LinkId=404100)tooconfigure hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="eeea9-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="eeea9-153">[指示](http://go.microsoft.com/fwlink/?LinkId=404099)hello 範例</span><span class="sxs-lookup"><span data-stu-id="eeea9-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeea9-154">其他資源</span><span class="sxs-lookup"><span data-stu-id="eeea9-154">Additional resources</span></span>
<span data-ttu-id="eeea9-155">[如何 toolog tooa 虛擬機器執行 Windows Server 上]</span><span class="sxs-lookup"><span data-stu-id="eeea9-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="eeea9-156">[Azure VM 延伸模組與功能]</span><span class="sxs-lookup"><span data-stu-id="eeea9-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[如何 toolog tooa 虛擬機器執行 Windows Server 上]:connect-logon.md
[Azure VM 延伸模組與功能]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
