---
title: "Azure 虛擬機器代理程式概觀 | Microsoft Docs"
description: "Azure 虛擬機器代理程式概觀"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="3bffc-103">Azure 虛擬機器代理程式概觀</span><span class="sxs-lookup"><span data-stu-id="3bffc-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="3bffc-104">「Microsoft Azure 虛擬機器代理程式」(VM 代理程式) 是安全的輕量型處理程序，可管理 VM 與「Azure 網狀架構控制器」的互動。</span><span class="sxs-lookup"><span data-stu-id="3bffc-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="3bffc-105">VM 代理程式已啟用主要角色並執行 Azure 虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="3bffc-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="3bffc-106">VM 擴充功能可啟用虛擬機器的部署後組態，例如安裝和設定軟體。</span><span class="sxs-lookup"><span data-stu-id="3bffc-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="3bffc-107">虛擬機器擴充功能也會啟用復原功能，例如重設虛擬機器的系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="3bffc-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="3bffc-108">若沒有 Azure VM 代理程式，便無法執行虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="3bffc-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="3bffc-109">本文件詳述 Azure 虛擬機器代理程式的安裝、偵測及移除。</span><span class="sxs-lookup"><span data-stu-id="3bffc-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="3bffc-110">安裝 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="3bffc-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="3bffc-111">Azure 資源庫映像</span><span class="sxs-lookup"><span data-stu-id="3bffc-111">Azure gallery image</span></span>

<span data-ttu-id="3bffc-112">根據預設，Azure VM 代理程式會安裝於任何從 Azure 資源庫映像部署的 Windows 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="3bffc-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="3bffc-113">經由入口網站、PowerShell、命令列介面或 Azure Resource Manager 範本部署 Azure 資源庫映像時，也會安裝 Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="3bffc-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="3bffc-114">手動安裝</span><span class="sxs-lookup"><span data-stu-id="3bffc-114">Manual installation</span></span>

<span data-ttu-id="3bffc-115">Windows VM 代理程式可以使用 Windows Installer 套件來手動安裝。</span><span class="sxs-lookup"><span data-stu-id="3bffc-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="3bffc-116">建立會部署在 Azure 中的自訂虛擬機器映像時，可能需要手動安裝。</span><span class="sxs-lookup"><span data-stu-id="3bffc-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="3bffc-117">若要手動安裝 Windows VM 代理程式，請從這個位置下載 VM 代理程式安裝程式：[Windows Azure VM 代理程式下載](http://go.microsoft.com/fwlink/?LinkID=394789)。</span><span class="sxs-lookup"><span data-stu-id="3bffc-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="3bffc-118">按兩下 Windows Installer 檔案即可安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="3bffc-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="3bffc-119">如需自動安裝 VM 代理程式，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="3bffc-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="3bffc-120">偵測 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="3bffc-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="3bffc-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bffc-121">PowerShell</span></span>

<span data-ttu-id="3bffc-122">Azure Resource Manager PowerShell 模組可以用來擷取 Azure 虛擬機器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3bffc-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="3bffc-123">執行 `Get-AzureRmVM` 可傳回相當多的資訊，包括 Azure VM 代理程式的佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="3bffc-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="3bffc-124">以下只是 `Get-AzureRmVM` 輸出的子集。</span><span class="sxs-lookup"><span data-stu-id="3bffc-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="3bffc-125">請注意，`ProvisionVMAgent` 屬性會以巢狀方式置於 `OSProfile` 內，這個屬性可用來判斷 VM 代理程式是否已部署至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3bffc-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="3bffc-126">下列指令碼可以用來傳回簡明的虛擬機器名稱清單和 VM 代理程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="3bffc-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="3bffc-127">手動偵測</span><span class="sxs-lookup"><span data-stu-id="3bffc-127">Manual Detection</span></span>

<span data-ttu-id="3bffc-128">記錄到 Windows Azure VM 時，工作管理員可用來檢查執行中的程序。</span><span class="sxs-lookup"><span data-stu-id="3bffc-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="3bffc-129">若要檢查 Azure VM 代理程式，請開啟 [工作管理員] > 按一下 [詳細資料] 索引標籤，然後尋找程序名稱 `WindowsAzureGuestAgent.exe`。</span><span class="sxs-lookup"><span data-stu-id="3bffc-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="3bffc-130">此程序的目前狀態表示已安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="3bffc-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="3bffc-131">升級 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="3bffc-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="3bffc-132">適用於 Windows 的 Azure VM 代理程式會自動升級。</span><span class="sxs-lookup"><span data-stu-id="3bffc-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="3bffc-133">當新的虛擬機器部署至 Azure 時，這些機器會收到最新的 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="3bffc-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="3bffc-134">自訂 VM 映像應進行手動更新，以包含新的 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="3bffc-134">Custom VM images should be manually updated to include the new VM agent.</span></span>