---
title: "Azure CLI 範例 | Microsoft Docs"
description: "Azure CLI 範例"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 43fe6d30bb08c6f79151705437cb184cbf154898
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a><span data-ttu-id="82b03-103">適用於 Linux 虛擬機器的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="82b03-103">Azure CLI Samples for Linux virtual machines</span></span>

<span data-ttu-id="82b03-104">下表包含使用 Azure CLI 所建置之 Bash 指令碼的連結。</span><span class="sxs-lookup"><span data-stu-id="82b03-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="82b03-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="82b03-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="82b03-106">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="82b03-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-107">以最低限度的組態建立 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="82b03-107">Creates a Linux virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="82b03-108">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="82b03-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-109">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="82b03-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="82b03-110">建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="82b03-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-111">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="82b03-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="82b03-112">建立已啟用 Docker 功能的 VM</span><span class="sxs-lookup"><span data-stu-id="82b03-112">Create a VM with Docker enabled</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-113">建立虛擬機器、設定此 VM 作為 Docker 主機，然後執行 NGINX 容器。</span><span class="sxs-lookup"><span data-stu-id="82b03-113">Creates a virtual machine, configures this VM as a Docker host, and runs an NGINX container.</span></span> |
| [<span data-ttu-id="82b03-114">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="82b03-114">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-115">建立虛擬機器，並使用「Azure 自訂指令碼」擴充功能來安裝 NGINX。</span><span class="sxs-lookup"><span data-stu-id="82b03-115">Creates a virtual machine and uses the Azure Custom Script extension to install NGINX.</span></span> |
| [<span data-ttu-id="82b03-116">建立已安裝 WordPress 的 VM</span><span class="sxs-lookup"><span data-stu-id="82b03-116">Create a VM with WordPress installed</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-117">建立虛擬機器，並使用「Azure 自訂指令碼」擴充功能來安裝 WordPress。</span><span class="sxs-lookup"><span data-stu-id="82b03-117">Creates a virtual machine and uses the Azure Custom Script extension to install WordPress.</span></span> |
| [<span data-ttu-id="82b03-118">從受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="82b03-118">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-119">連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="82b03-119">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="82b03-120">從快照集建立 VM</span><span class="sxs-lookup"><span data-stu-id="82b03-120">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-121">先從快照集建立受控磁碟，然後連結新的受控磁碟作為 OS 磁碟，以從快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="82b03-121">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching the new managed disk as OS disk.</span></span> |
|<span data-ttu-id="82b03-122">**管理儲存體**</span><span class="sxs-lookup"><span data-stu-id="82b03-122">**Manage storage**</span></span>||
| [<span data-ttu-id="82b03-123">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="82b03-123">Create managed disk from a VHD</span></span>](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-124">從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="82b03-124">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk.</span></span>  |
| [<span data-ttu-id="82b03-125">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="82b03-125">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-126">從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="82b03-126">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="82b03-127">將受控磁碟複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82b03-127">Copy managed disk to same or different subscription</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-128">將受控磁碟複製到與父受控磁碟相同區域中相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="82b03-128">Copies managed disk to same or different subscription but in the same region as the parent managed disk.</span></span> 
| [<span data-ttu-id="82b03-129">將快照集以 VHD 格式匯出至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="82b03-129">Export a snapshot as VHD to a storage account</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-130">將受管理快照集以 VDH 格式匯出至不同區域中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="82b03-130">Exports a managed snapshot as VHD to a storage account in different region.</span></span> |
| [<span data-ttu-id="82b03-131">將快照集複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82b03-131">Copy snapshot to same or different subscription</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="82b03-132">將快照集複製到與父快照集相同區域中相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="82b03-132">Copies snapshot to same or different subscription but in the same region as the parent snapshot.</span></span> |
|<span data-ttu-id="82b03-133">**網路虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="82b03-133">**Network virtual machines**</span></span>||
| [<span data-ttu-id="82b03-134">保護虛擬機器之間的網路流量</span><span class="sxs-lookup"><span data-stu-id="82b03-134">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-135">建立兩部虛擬機器、所有相關資源以及內部和外部網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="82b03-135">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="82b03-136">**保護虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="82b03-136">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="82b03-137">加密 VM 和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="82b03-137">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-138">建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。</span><span class="sxs-lookup"><span data-stu-id="82b03-138">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="82b03-139">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="82b03-139">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="82b03-140">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="82b03-140">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-141">建立虛擬機器、安裝 Operations Management Suite 代理程式，並在 OMS 工作區中註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="82b03-141">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
|<span data-ttu-id="82b03-142">**針對虛擬機器進行疑難排解**</span><span class="sxs-lookup"><span data-stu-id="82b03-142">**Troubleshoot virtual machines**</span></span>||
| [<span data-ttu-id="82b03-143">針對 VM 作業系統磁碟進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="82b03-143">Troubleshoot a VMs operating system disk</span></span>](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="82b03-144">掛接一個 VM 的作業系統磁碟作為第二個 VM 上的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="82b03-144">Mounts the operating system disk from one VM as a data disk on a second VM.</span></span> |
| | |
