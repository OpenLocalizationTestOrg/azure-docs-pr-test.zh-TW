---
title: "aaaAzure 虛擬機器代理程式概觀 |Microsoft 文件"
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
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="31064-103">Azure 虛擬機器代理程式概觀</span><span class="sxs-lookup"><span data-stu-id="31064-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="31064-104">hello Microsoft Azure 虛擬機器代理程式 （VM 代理程式） 是安全的輕量型程序管理 VM 與 hello Azure 網狀架構控制器之間的互動。</span><span class="sxs-lookup"><span data-stu-id="31064-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="31064-105">hello VM 代理程式已啟用和執行 Azure 虛擬機器擴充功能的主要角色。</span><span class="sxs-lookup"><span data-stu-id="31064-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="31064-106">VM 擴充功能可啟用虛擬機器的部署後組態，例如安裝和設定軟體。</span><span class="sxs-lookup"><span data-stu-id="31064-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="31064-107">虛擬機器擴充功能也會啟用復原功能，例如，重設虛擬機器的 hello 系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="31064-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="31064-108">沒有 hello Azure VM 代理程式，就無法執行虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="31064-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="31064-109">本文件詳述安裝、 偵測和移除 hello Azure 虛擬機器代理程式。</span><span class="sxs-lookup"><span data-stu-id="31064-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="31064-110">安裝 VM 代理程式 hello</span><span class="sxs-lookup"><span data-stu-id="31064-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="31064-111">Azure 資源庫映像</span><span class="sxs-lookup"><span data-stu-id="31064-111">Azure gallery image</span></span>

<span data-ttu-id="31064-112">從 Azure 資源庫映像部署任何 Windows 虛擬機器上的預設會安裝 hello Azure VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="31064-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="31064-113">部署 Azure 資源庫映像從 hello 入口網站、 PowerShell、 命令列介面或 Azure 資源管理員範本，當 hello Azure VM 代理程式也會安裝。</span><span class="sxs-lookup"><span data-stu-id="31064-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="31064-114">手動安裝</span><span class="sxs-lookup"><span data-stu-id="31064-114">Manual installation</span></span>

<span data-ttu-id="31064-115">hello Windows VM 代理程式可以使用 Windows installer 封裝來手動安裝。</span><span class="sxs-lookup"><span data-stu-id="31064-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="31064-116">建立會部署在 Azure 中的自訂虛擬機器映像時，可能需要手動安裝。</span><span class="sxs-lookup"><span data-stu-id="31064-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="31064-117">toomanually 安裝 hello Windows VM 代理程式，從這個位置下載 hello VM 代理程式安裝程式[Windows Azure VM 代理程式下載](http://go.microsoft.com/fwlink/?LinkID=394789)。</span><span class="sxs-lookup"><span data-stu-id="31064-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="31064-118">hello VM 代理程式可以按兩下 hello windows installer 檔案安裝。</span><span class="sxs-lookup"><span data-stu-id="31064-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="31064-119">自動或無人看管的 hello VM 代理程式安裝，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="31064-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="31064-120">偵測 hello VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="31064-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="31064-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31064-121">PowerShell</span></span>

<span data-ttu-id="31064-122">hello Azure 資源管理員 PowerShell 模組可以是使用的 tooretrieve 資訊有關 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="31064-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="31064-123">執行`Get-AzureRmVM`傳回相當多的資訊包括 hello 佈建 hello Azure VM 代理程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="31064-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="31064-124">hello 以下是剛 hello 子集`Get-AzureRmVM`輸出。</span><span class="sxs-lookup"><span data-stu-id="31064-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="31064-125">請注意 hello`ProvisionVMAgent`屬性在巢狀`OSProfile`，這個屬性可以是使用的 toodetermine 如果 hello VM 代理程式已部署的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="31064-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="31064-126">下列指令碼的 hello 可以是使用的 tooreturn hello hello VM 代理程式狀態的虛擬機器名稱簡明清單。</span><span class="sxs-lookup"><span data-stu-id="31064-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="31064-127">手動偵測</span><span class="sxs-lookup"><span data-stu-id="31064-127">Manual Detection</span></span>

<span data-ttu-id="31064-128">登入 Windows Azure VM tooa，工作管理員可以使用的 tooexamine 執行處理程序。</span><span class="sxs-lookup"><span data-stu-id="31064-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="31064-129">toocheck hello Azure VM 代理程式，開啟 [工作管理員 > 按一下 hello 詳細資料] 索引標籤，並尋找處理程序名稱`WindowsAzureGuestAgent.exe`。</span><span class="sxs-lookup"><span data-stu-id="31064-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="31064-130">此程序的 hello 存在表示該 hello VM 代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="31064-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="31064-131">升級 hello VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="31064-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="31064-132">hello Azure VM 代理程式的 Windows 會自動升級。</span><span class="sxs-lookup"><span data-stu-id="31064-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="31064-133">由於新的虛擬機器是部署的 tooAzure，他們會收到 hello 最新的 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="31064-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="31064-134">自訂 VM 映像應該手動更新的 tooinclude hello 新 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="31064-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
