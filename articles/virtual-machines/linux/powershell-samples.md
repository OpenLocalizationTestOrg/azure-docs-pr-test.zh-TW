---
title: "虛擬機器的 PowerShell 範例 aaaAzure |Microsoft 文件"
description: "Azure 虛擬機器 PowerShell 範例"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: 089d85dfb1ac0995bcb45ac9e927db727b5ed09d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a><span data-ttu-id="7b074-103">Azure 虛擬機器 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="7b074-103">Azure Virtual Machine PowerShell samples</span></span>

<span data-ttu-id="7b074-104">hello 下表包含可建立及管理的 Linux 虛擬機器連結 tooPowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="7b074-104">hello following table includes links tooPowerShell scripts samples that create and manage Linux virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="7b074-105">**建立虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="7b074-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="7b074-106">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7b074-106">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-linux-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="7b074-107">建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="7b074-107">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="7b074-108">建立已啟用 Docker 功能的 VM</span><span class="sxs-lookup"><span data-stu-id="7b074-108">Create a VM with Docker enabled</span></span>](./../scripts/virtual-machines-linux-powershell-sample-create-docker-host.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="7b074-109">建立虛擬機器、設定此 VM 作為 Docker 主機，然後執行 NGINX 容器。</span><span class="sxs-lookup"><span data-stu-id="7b074-109">Creates a virtual machine, configures this VM as a Docker host, and runs an NGINX container.</span></span> |
| [<span data-ttu-id="7b074-110">建立 VM 並執行組態指令碼</span><span class="sxs-lookup"><span data-stu-id="7b074-110">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-linux-powershell-sample-create-vm-nginx.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="7b074-111">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall NGINX。</span><span class="sxs-lookup"><span data-stu-id="7b074-111">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall NGINX.</span></span> |
| [<span data-ttu-id="7b074-112">建立已安裝 WordPress 的 VM</span><span class="sxs-lookup"><span data-stu-id="7b074-112">Create a VM with WordPress installed</span></span>](./../scripts/virtual-machines-linux-powershell-sample-create-vm-wordpress.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="7b074-113">建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall WordPress。</span><span class="sxs-lookup"><span data-stu-id="7b074-113">Creates a virtual machine and uses hello Azure Custom Script extension tooinstall WordPress.</span></span> |
|<span data-ttu-id="7b074-114">**監視虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="7b074-114">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="7b074-115">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="7b074-115">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-linux-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="7b074-116">建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="7b074-116">Creates a virtual machine, installs hello Operations Management Suite agent, and enrolls hello VM in an OMS Workspace.</span></span>  |
| | |
