---
title: "虛擬機器的 PowerShell 範例 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a><span data-ttu-id="2ef36-103">Azure 虛擬機器 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="2ef36-103">Azure Virtual Machine PowerShell samples</span></span>

<span data-ttu-id="2ef36-104">hello 下表包含可建立及管理 Windows 虛擬機器連結 tooPowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="2ef36-104">hello following table includes links tooPowerShell scripts samples that create and manage Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="2ef36-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="2ef36-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="2ef36-106">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2ef36-106">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-107">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="2ef36-107">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="2ef36-108">建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2ef36-108">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-109">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ef36-109">Creates several virtual machines in a highly available and load balanced configuration.</span></span>|
| [<span data-ttu-id="2ef36-110">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="2ef36-110">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-111">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="2ef36-111">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="2ef36-112">建立 VM 並執行 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="2ef36-112">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-113">建立虛擬機器，並使用 hello Azure 預期狀態設定 (DSC) 延伸模組 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="2ef36-113">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="2ef36-114">上傳 VHD 並建立 VM</span><span class="sxs-lookup"><span data-stu-id="2ef36-114">Upload a VHD and create VMs</span></span>](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | <span data-ttu-id="2ef36-115">Uplaods 將本機 VHD 檔案 tooAzure 建立和從 hello VHD 映像，然後從該映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="2ef36-115">Uplaods a local VHD file tooAzure, creates and image from hello VHD and then creates a VM from that image.</span></span> |
| [<span data-ttu-id="2ef36-116">從受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="2ef36-116">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-117">連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ef36-117">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="2ef36-118">從快照集建立 VM</span><span class="sxs-lookup"><span data-stu-id="2ef36-118">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-119">從快照集建立虛擬機器，請先建立從快照集的 受管理的磁碟，然後附加 hello 新受管理的磁碟與作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ef36-119">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching hello new managed disk as OS disk.</span></span> |
|<span data-ttu-id="2ef36-120">**管理儲存體**</span><span class="sxs-lookup"><span data-stu-id="2ef36-120">**Manage storage**</span></span>||
| [<span data-ttu-id="2ef36-121">在相同或不同的訂用帳戶中從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="2ef36-121">Create managed disk from a VHD in same or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-122">在相同或不同的訂用帳戶中，從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ef36-122">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk in same or different subscription.</span></span>  |
| [<span data-ttu-id="2ef36-123">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="2ef36-123">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-124">從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ef36-124">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="2ef36-125">複製受管理的磁碟 toosame 或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2ef36-125">Copy managed disk toosame or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-126">受管理的複本磁碟 toosame 或不同的訂用帳戶，但在 hello 相同與 hello 父區域管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="2ef36-126">Copies managed disk toosame or different subscription but in hello same region as hello parent managed disk.</span></span> 
| [<span data-ttu-id="2ef36-127">將快照集匯出為 VHD tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2ef36-127">Export a snapshot as VHD tooa storage account</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-128">將受管理的快照集匯出為不同的區域中的 VHD tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ef36-128">Exports a managed snapshot as VHD tooa storage account in different region.</span></span> |
| [<span data-ttu-id="2ef36-129">從 VDH 建立快照集</span><span class="sxs-lookup"><span data-stu-id="2ef36-129">Create a snapshot from a VHD</span></span>](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-130">建立快照集 VHD toocreate 從多個相同的受管理的磁碟從快照集在短時間內。</span><span class="sxs-lookup"><span data-stu-id="2ef36-130">Creates snapshot from a VHD toocreate multiple identical managed disks from snapshot in short amount of time.</span></span>  |
| [<span data-ttu-id="2ef36-131">複製快照集 toosame 或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2ef36-131">Copy snapshot toosame or different subscription</span></span>](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-132">複製快照集 toosame 或 hello 相同但在不同的訂閱與 hello 父快照集的區域。</span><span class="sxs-lookup"><span data-stu-id="2ef36-132">Copies snapshot toosame or different subscription but in hello same region as hello parent snapshot.</span></span> |
|<span data-ttu-id="2ef36-133">**保護虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="2ef36-133">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="2ef36-134">加密 VM 和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="2ef36-134">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | <span data-ttu-id="2ef36-135">建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。</span><span class="sxs-lookup"><span data-stu-id="2ef36-135">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="2ef36-136">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="2ef36-136">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="2ef36-137">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="2ef36-137">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2ef36-138">建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="2ef36-138">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |

