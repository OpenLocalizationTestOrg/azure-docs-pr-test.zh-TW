---
title: "Azure 虛擬機器 PowerShell 範例 | Microsoft Docs"
description: "Azure 虛擬機器 PowerShell 範例"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ff8b741b04ff37fa1a5fbaddabdd588ab43f19c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a><span data-ttu-id="27a65-103">Azure 虛擬機器 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="27a65-103">Azure Virtual Machine PowerShell samples</span></span>

<span data-ttu-id="27a65-104">下表包含可供建立和管理 Windows 虛擬機器之 PowerShell 指令碼範例的連結。</span><span class="sxs-lookup"><span data-stu-id="27a65-104">The following table includes links to PowerShell scripts samples that create and manage Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="27a65-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="27a65-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="27a65-106">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="27a65-106">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-107">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="27a65-107">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="27a65-108">建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="27a65-108">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-109">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="27a65-109">Creates several virtual machines in a highly available and load balanced configuration.</span></span>|
| [<span data-ttu-id="27a65-110">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="27a65-110">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-111">建立虛擬機器，並使用 Azure 自訂指令碼擴充功能來安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="27a65-111">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="27a65-112">建立 VM 並執行 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="27a65-112">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-113">建立虛擬機器，並使用 Azure 預期狀態設定 (DSC) 擴充功能來安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="27a65-113">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
| [<span data-ttu-id="27a65-114">上傳 VHD 並建立 VM</span><span class="sxs-lookup"><span data-stu-id="27a65-114">Upload a VHD and create VMs</span></span>](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | <span data-ttu-id="27a65-115">將本機 VHD 檔案上傳至 Azure、從 VHD 建立映像，然後從該映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="27a65-115">Uplaods a local VHD file to Azure, creates and image from the VHD and then creates a VM from that image.</span></span> |
| [<span data-ttu-id="27a65-116">從受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="27a65-116">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-117">連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="27a65-117">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="27a65-118">從快照集建立 VM</span><span class="sxs-lookup"><span data-stu-id="27a65-118">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-119">先從快照集建立受控磁碟，然後連結新的受控磁碟作為 OS 磁碟，以從快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="27a65-119">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching the new managed disk as OS disk.</span></span> |
|<span data-ttu-id="27a65-120">**管理儲存體**</span><span class="sxs-lookup"><span data-stu-id="27a65-120">**Manage storage**</span></span>||
| [<span data-ttu-id="27a65-121">在相同或不同的訂用帳戶中從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="27a65-121">Create managed disk from a VHD in same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-122">在相同或不同的訂用帳戶中，從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="27a65-122">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk in same or different subscription.</span></span>  |
| [<span data-ttu-id="27a65-123">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="27a65-123">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-124">從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="27a65-124">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="27a65-125">將受控磁碟複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27a65-125">Copy managed disk to same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-126">將受控磁碟複製到與父受控磁碟相同區域中相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="27a65-126">Copies managed disk to same or different subscription but in the same region as the parent managed disk.</span></span> 
| [<span data-ttu-id="27a65-127">將快照集以 VHD 格式匯出至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="27a65-127">Export a snapshot as VHD to a storage account</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-128">將受管理快照集以 VDH 格式匯出至不同區域中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="27a65-128">Exports a managed snapshot as VHD to a storage account in different region.</span></span> |
| [<span data-ttu-id="27a65-129">從 VDH 建立快照集</span><span class="sxs-lookup"><span data-stu-id="27a65-129">Create a snapshot from a VHD</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-130">從 VHD 建立快照集以在短時間內從快照集建立多個相同的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="27a65-130">Creates snapshot from a VHD to create multiple identical managed disks from snapshot in short amount of time.</span></span>  |
| [<span data-ttu-id="27a65-131">將快照集複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27a65-131">Copy snapshot to same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-132">將快照集複製到與父快照集相同區域中相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="27a65-132">Copies snapshot to same or different subscription but in the same region as the parent snapshot.</span></span> |
|<span data-ttu-id="27a65-133">**保護虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="27a65-133">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="27a65-134">加密 VM 和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="27a65-134">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | <span data-ttu-id="27a65-135">建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。</span><span class="sxs-lookup"><span data-stu-id="27a65-135">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="27a65-136">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="27a65-136">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="27a65-137">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="27a65-137">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="27a65-138">建立虛擬機器、安裝 Operations Management Suite 代理程式，並在 OMS 工作區中註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="27a65-138">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |

