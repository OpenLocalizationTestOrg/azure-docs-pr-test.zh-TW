---
title: "aaaAzure CLI 範例 |Microsoft 文件"
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
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a><span data-ttu-id="829f8-103">適用於 Linux 虛擬機器的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="829f8-103">Azure CLI Samples for Linux virtual machines</span></span>

<span data-ttu-id="829f8-104">hello 下表包含使用 Azure CLI hello 建置連結 toobash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="829f8-104">hello following table includes links toobash scripts built using hello Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="829f8-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="829f8-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="829f8-106">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="829f8-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-107">以最低限度的組態建立 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="829f8-107">Creates a Linux virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="829f8-108">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="829f8-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-109">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="829f8-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="829f8-110">建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="829f8-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-111">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="829f8-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="829f8-112">建立已啟用 Docker 功能的 VM</span><span class="sxs-lookup"><span data-stu-id="829f8-112">Create a VM with Docker enabled</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-113">建立虛擬機器、設定此 VM 作為 Docker 主機，然後執行 NGINX 容器。</span><span class="sxs-lookup"><span data-stu-id="829f8-113">Creates a virtual machine, configures this VM as a Docker host, and runs an NGINX container.</span></span> |
| [<span data-ttu-id="829f8-114">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="829f8-114">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-115">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall NGINX。</span><span class="sxs-lookup"><span data-stu-id="829f8-115">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall NGINX.</span></span> |
| [<span data-ttu-id="829f8-116">建立已安裝 WordPress 的 VM</span><span class="sxs-lookup"><span data-stu-id="829f8-116">Create a VM with WordPress installed</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-117">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall WordPress。</span><span class="sxs-lookup"><span data-stu-id="829f8-117">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall WordPress.</span></span> |
| [<span data-ttu-id="829f8-118">從受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="829f8-118">Create a VM from a managed OS disk</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-119">連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="829f8-119">Creates a virtual machine by attaching an existing Managed Disk as OS disk.</span></span> |
| [<span data-ttu-id="829f8-120">從快照集建立 VM</span><span class="sxs-lookup"><span data-stu-id="829f8-120">Create a VM from a snapshot</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-121">從快照集建立虛擬機器，請先建立從快照集的 受管理的磁碟，然後附加 hello 新受管理的磁碟與作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="829f8-121">Creates a virtual machine from a snapshot by first creating a managed disk from snapshot and then attaching hello new managed disk as OS disk.</span></span> |
|<span data-ttu-id="829f8-122">**管理儲存體**</span><span class="sxs-lookup"><span data-stu-id="829f8-122">**Manage storage**</span></span>||
| [<span data-ttu-id="829f8-123">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="829f8-123">Create managed disk from a VHD</span></span>](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-124">從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="829f8-124">Creates a managed disk from a specialized VHD as a OS disk or from a data VHD as data disk.</span></span>  |
| [<span data-ttu-id="829f8-125">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="829f8-125">Create a managed disk from a snapshot</span></span>](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-126">從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="829f8-126">Creates a managed disk from a snapshot.</span></span> |
| [<span data-ttu-id="829f8-127">複製受管理的磁碟 toosame 或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="829f8-127">Copy managed disk toosame or different subscription</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-128">受管理的複本磁碟 toosame 或不同的訂用帳戶，但在 hello 相同與 hello 父區域管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="829f8-128">Copies managed disk toosame or different subscription but in hello same region as hello parent managed disk.</span></span> 
| [<span data-ttu-id="829f8-129">將快照集匯出為 VHD tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="829f8-129">Export a snapshot as VHD tooa storage account</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-130">將受管理的快照集匯出為不同的區域中的 VHD tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="829f8-130">Exports a managed snapshot as VHD tooa storage account in different region.</span></span> |
| [<span data-ttu-id="829f8-131">複製快照集 toosame 或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="829f8-131">Copy snapshot toosame or different subscription</span></span>](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | <span data-ttu-id="829f8-132">複製快照集 toosame 或 hello 相同但在不同的訂閱與 hello 父快照集的區域。</span><span class="sxs-lookup"><span data-stu-id="829f8-132">Copies snapshot toosame or different subscription but in hello same region as hello parent snapshot.</span></span> |
|<span data-ttu-id="829f8-133">**網路虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="829f8-133">**Network virtual machines**</span></span>||
| [<span data-ttu-id="829f8-134">保護虛擬機器之間的網路流量</span><span class="sxs-lookup"><span data-stu-id="829f8-134">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-135">建立兩部虛擬機器、所有相關資源以及內部和外部網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="829f8-135">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="829f8-136">**保護虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="829f8-136">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="829f8-137">加密 VM 和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="829f8-137">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-138">建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。</span><span class="sxs-lookup"><span data-stu-id="829f8-138">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="829f8-139">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="829f8-139">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="829f8-140">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="829f8-140">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-141">建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="829f8-141">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
|<span data-ttu-id="829f8-142">**針對虛擬機器進行疑難排解**</span><span class="sxs-lookup"><span data-stu-id="829f8-142">**Troubleshoot virtual machines**</span></span>||
| [<span data-ttu-id="829f8-143">針對 VM 作業系統磁碟進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="829f8-143">Troubleshoot a VMs operating system disk</span></span>](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="829f8-144">Hello 作業系統磁碟從掛接一個 VM 當做資料磁碟上的第二個 VM。</span><span class="sxs-lookup"><span data-stu-id="829f8-144">Mounts hello operating system disk from one VM as a data disk on a second VM.</span></span> |
| | |
