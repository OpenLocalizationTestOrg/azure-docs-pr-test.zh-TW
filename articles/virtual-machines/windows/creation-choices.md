---
title: "aaaDifferent 方式 toocreate Azure 中的 Windows VM |Microsoft 文件"
description: "列出 hello 不同的方式 toocreate Windows 虛擬機器與資源管理員。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="a6214-103">不同的方式 toocreate Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6214-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="a6214-104">因為虛擬機器適用於不同的使用者和用途，azure 將提供不同的方式 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a6214-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="a6214-105">這表示您需要 toomake hello 虛擬機器相關的一些選項以及如何 toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="a6214-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="a6214-106">這篇文章會提供這些選項的摘要，並連結 tooinstructions。</span><span class="sxs-lookup"><span data-stu-id="a6214-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="a6214-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a6214-107">Azure portal</span></span>
<span data-ttu-id="a6214-108">使用 hello Azure 入口網站是出虛擬機器時，簡單的方式 tootry，特別是如果您剛開始使用 Azure。</span><span class="sxs-lookup"><span data-stu-id="a6214-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="a6214-109">建立執行 Windows 的 hello 入口網站的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6214-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="a6214-110">範本</span><span class="sxs-lookup"><span data-stu-id="a6214-110">Template</span></span>
<span data-ttu-id="a6214-111">虛擬機器需要各種資源 (例如可用性設定組和儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="a6214-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="a6214-112">而不是部署與個別管理每個資源，您可以建立的 Azure Resource Manager 範本部署和佈建的所有單一、 協調作業中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a6214-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="a6214-113">利用 Resource Manager 範本建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6214-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="a6214-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6214-114">Azure PowerShell</span></span>
<span data-ttu-id="a6214-115">如果您偏好使用命令殼層，可以使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a6214-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="a6214-116">使用 PowerShell 建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="a6214-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="a6214-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6214-117">Visual Studio</span></span>
<span data-ttu-id="a6214-118">使用 Visual Studio toobuild、 管理和部署 Vm 使用 hello Azure Tools for Visual Studio 和 hello Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="a6214-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="a6214-119">Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6214-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

