---
title: "aaaAzure CLI 範例 Windows |Microsoft 文件"
description: "Azure CLI 範例 Windows"
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
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="fe598-103">適用於 Windows 虛擬機器的 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="fe598-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="fe598-104">hello 下表包含連結 toobash 指令碼使用 Azure CLI hello 建置部署 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fe598-104">hello following table includes links toobash scripts built using hello Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="fe598-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="fe598-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="fe598-106">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe598-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-107">以最低限度的組態建立 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fe598-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="fe598-108">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe598-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-109">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fe598-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="fe598-110">建立高可用性的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe598-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-111">依據高可用性和負載平衡組態建立數個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fe598-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="fe598-112">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="fe598-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-113">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="fe598-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall IIS.</span></span> |
| [<span data-ttu-id="fe598-114">建立 VM 並執行 DSC 組態</span><span class="sxs-lookup"><span data-stu-id="fe598-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-115">建立虛擬機器，並使用 hello Azure 預期狀態設定 (DSC) 延伸模組 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="fe598-115">Creates a virtual machine and uses hello Azure Desired State Configuration (DSC) extension tooinstall IIS.</span></span> |
|<span data-ttu-id="fe598-116">**網路虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="fe598-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="fe598-117">保護虛擬機器之間的網路流量</span><span class="sxs-lookup"><span data-stu-id="fe598-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-118">建立兩部虛擬機器、所有相關資源以及內部和外部網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="fe598-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="fe598-119">**保護虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="fe598-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="fe598-120">加密 VM 和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="fe598-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-121">建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。</span><span class="sxs-lookup"><span data-stu-id="fe598-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="fe598-122">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="fe598-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="fe598-123">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="fe598-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="fe598-124">建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="fe598-124">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
