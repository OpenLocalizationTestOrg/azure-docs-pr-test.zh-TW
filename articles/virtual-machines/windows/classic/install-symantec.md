---
title: "在 Azure 中的 Windows VM 上的 Symantec Endpoint Protection aaaInstall |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定新的 hello Symantec Endpoint Protection 安全性延伸模組，或現有的 Azure VM 建立與 hello 傳統部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="f038e-103">如何 tooinstall 及 Windows VM 上設定 Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f038e-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f038e-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f038e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f038e-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f038e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f038e-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="f038e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f038e-107">本文章將示範如何 tooinstall 和設定現有的虛擬機器 (VM) 執行 Windows Server 上 hello Symantec Endpoint Protection 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f038e-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="f038e-108">此完整用戶端包括服務 (例如病毒和間諜軟體防護、防火牆及入侵防禦)。</span><span class="sxs-lookup"><span data-stu-id="f038e-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="f038e-109">hello 會安裝用戶端的安全性延伸模組為使用 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f038e-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="f038e-110">如果您有內部部署解決方案 symantec 提供的現有訂閱，您可以使用它 tooprotect Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f038e-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="f038e-111">如果您還不是 Symantec 客戶，您可以註冊試用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f038e-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="f038e-112">如需此解決方案的詳細資訊，請參閱 [Microsoft Azure 平台上的 Symantec Endpoint Protection][Symantec]。</span><span class="sxs-lookup"><span data-stu-id="f038e-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="f038e-113">這個網頁也有連結 toolicensing 資訊和指示安裝 hello 用戶端，如果您已經 Symantec 客戶。</span><span class="sxs-lookup"><span data-stu-id="f038e-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="f038e-114">在現有 VM 上安裝 Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f038e-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="f038e-115">在開始之前，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f038e-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="f038e-116">hello Azure PowerShell 模組、 0.8.2 版或更新版本，在您的工作電腦。</span><span class="sxs-lookup"><span data-stu-id="f038e-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="f038e-117">您可以檢查 hello 版本的 Azure PowerShell 安裝與 hello **Get-module azure | 格式資料表版本**命令。</span><span class="sxs-lookup"><span data-stu-id="f038e-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="f038e-118">如需指示和連結 toohello 最新版本，請參閱[如何 tooInstall 和設定 Azure PowerShell][PS]。</span><span class="sxs-lookup"><span data-stu-id="f038e-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="f038e-119">登入 tooyour Azure 訂用帳戶使用`Add-AzureAccount`。</span><span class="sxs-lookup"><span data-stu-id="f038e-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="f038e-120">hello VM 代理程式上執行 hello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f038e-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="f038e-121">首先，確認該 hello hello 虛擬機器已安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f038e-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="f038e-122">填寫 hello 雲端服務名稱和虛擬機器名稱，然後執行下列命令，以系統管理員層級 Azure PowerShell 命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="f038e-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="f038e-123">取代 hello 引號，包括 hello < 和 > 字元內的所有內容。</span><span class="sxs-lookup"><span data-stu-id="f038e-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="f038e-124">如果您不知道 hello 雲端服務和虛擬機器名稱，執行**Get-azurevm** toolist hello 您目前的訂用帳戶中的所有虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="f038e-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="f038e-125">如果 hello**寫入主機**命令便會顯示**True**，hello 安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f038e-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="f038e-126">如果它顯示**False**，請參閱 hello 指示與下載 hello Azure 部落格文章中的連結 toohello [VM 代理程式和擴充功能-第 2 部分][Agent]。</span><span class="sxs-lookup"><span data-stu-id="f038e-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="f038e-127">如果已安裝 VM 代理程式 hello，執行這些命令 tooinstall hello Symantec Endpoint Protection 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f038e-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="f038e-128">hello Symantec 安全性延伸模組的 tooverify 已安裝且是最新的：</span><span class="sxs-lookup"><span data-stu-id="f038e-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="f038e-129">登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f038e-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="f038e-130">如需指示，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog][Logon]。</span><span class="sxs-lookup"><span data-stu-id="f038e-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="f038e-131">在 Windows Server 2008 R2 中，按一下 [開始] > [Symantec Endpoint Protection]。</span><span class="sxs-lookup"><span data-stu-id="f038e-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="f038e-132">如需 Windows Server 2012 或 Windows Server 2012 R2，從 hello [開始] 畫面，輸入**Symantec**，然後按一下 **Symantec Endpoint Protection**。</span><span class="sxs-lookup"><span data-stu-id="f038e-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="f038e-133">從 hello**狀態** 索引標籤的 hello**狀態 Symantec Endpoint Protection**視窗中，套用更新，或視需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="f038e-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f038e-134">其他資源</span><span class="sxs-lookup"><span data-stu-id="f038e-134">Additional resources</span></span>
<span data-ttu-id="f038e-135">[如何 tooLog tooa 執行 Windows Server 的虛擬機器上][Logon]</span><span class="sxs-lookup"><span data-stu-id="f038e-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="f038e-136">[Azure VM 擴充功能與功能][Ext]</span><span class="sxs-lookup"><span data-stu-id="f038e-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
