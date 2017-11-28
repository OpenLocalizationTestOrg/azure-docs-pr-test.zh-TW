---
title: "在 Azure 中建立 Windows VM 的不同方式 | Microsoft Docs"
description: "列出使用資源管理員建立 Windows 虛擬機器的不同方式。"
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a><span data-ttu-id="9dce1-103">建立 Windows 虛擬機器的不同方式</span><span class="sxs-lookup"><span data-stu-id="9dce1-103">Different ways to create a Windows virtual machine</span></span>

<span data-ttu-id="9dce1-104">Azure 提供建立虛擬機器的不同方式，因為虛擬機器適用於不同的使用者和用途。</span><span class="sxs-lookup"><span data-stu-id="9dce1-104">Azure offers different ways to create a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="9dce1-105">這表示您需要針對虛擬機器以及建立方式進行一些選擇。</span><span class="sxs-lookup"><span data-stu-id="9dce1-105">This means that you need to make some choices about the virtual machine and how to create it.</span></span> <span data-ttu-id="9dce1-106">本文提供這些選項及指示連結的摘要說明。</span><span class="sxs-lookup"><span data-stu-id="9dce1-106">This article gives you a summary of these choices and links to instructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="9dce1-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9dce1-107">Azure portal</span></span>
<span data-ttu-id="9dce1-108">使用 Azure 入口網站是嘗試設定虛擬機器的簡單方法，特別是在您剛開始使用 Azure 時。</span><span class="sxs-lookup"><span data-stu-id="9dce1-108">Using the Azure portal is a simple way to try out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="9dce1-109">使用入口網站建立執行 Windows 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9dce1-109">Create a virtual machine running Windows using the portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="9dce1-110">範本</span><span class="sxs-lookup"><span data-stu-id="9dce1-110">Template</span></span>
<span data-ttu-id="9dce1-111">虛擬機器需要各種資源 (例如可用性設定組和儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="9dce1-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="9dce1-112">您不是分開部署與管理每個資源，而是建立一個 Azure Resource Manager 範本，藉此經由協調的單一作業來部署與佈建所有資源。</span><span class="sxs-lookup"><span data-stu-id="9dce1-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of the resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="9dce1-113">利用 Resource Manager 範本建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9dce1-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="9dce1-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dce1-114">Azure PowerShell</span></span>
<span data-ttu-id="9dce1-115">如果您偏好使用命令殼層，可以使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9dce1-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="9dce1-116">使用 PowerShell 建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="9dce1-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="9dce1-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9dce1-117">Visual Studio</span></span>
<span data-ttu-id="9dce1-118">使用 Visual Studio 搭配 Azure Tools for Visual Studio 和 Azure SDK 來建置、管理與部署 VM。</span><span class="sxs-lookup"><span data-stu-id="9dce1-118">Use Visual Studio to build, manage, and deploy VMs with the Azure Tools for Visual Studio and the Azure SDK.</span></span>

[<span data-ttu-id="9dce1-119">Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9dce1-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

