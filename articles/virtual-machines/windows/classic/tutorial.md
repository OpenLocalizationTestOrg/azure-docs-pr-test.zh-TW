---
title: "在 Azure 入口網站中建立 VM | Microsoft Docs"
description: "在 Azure 入口網站中建立 Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="cf30c-103">在 Azure 入口網站中建立執行 Windows 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cf30c-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf30c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cf30c-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="cf30c-105">PowerShell：傳統部署</span><span class="sxs-lookup"><span data-stu-id="cf30c-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="cf30c-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cf30c-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="cf30c-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="cf30c-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="cf30c-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="cf30c-109">了解如何透過 **Azure 入口網站**，[使用 Resource Manager 部署模型執行這些步驟](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="cf30c-110">本教學課程示範如何在 Azure 入口網站中建立執行 Windows 的 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="cf30c-111">我們將使用 Windows Server 映像做為範例，這只是 Azure 提供眾多映像中的一種。</span><span class="sxs-lookup"><span data-stu-id="cf30c-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="cf30c-112">請注意，您可以選擇何種映像取決於您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf30c-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="cf30c-113">例如，Windows 桌面映像可能可供 MSDN 訂閱者使用。</span><span class="sxs-lookup"><span data-stu-id="cf30c-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="cf30c-114">本節說明如何使用 Azure 入口網站中的**儀表板**以選擇並建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cf30c-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="cf30c-115">您也可以使用 [您自己的映像](createupload-vhd.md)來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="cf30c-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="cf30c-116">若要了解上述方法與其他方法，請參閱 [建立 Windows 虛擬機器的其他方式](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="cf30c-117"><a id="createvirtualmachine"> </a>建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cf30c-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="cf30c-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf30c-118">Next steps</span></span>
* <span data-ttu-id="cf30c-119">深入了解如何在 Azure 入口網站，[使用 Resource Manager 部署模型建立 VM](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="cf30c-120">登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cf30c-120">Log on to the virtual machine.</span></span> <span data-ttu-id="cf30c-121">如需相關指示，請參閱 [登入執行 Windows Server 的虛擬機器](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="cf30c-122">附加磁碟來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="cf30c-122">Attach a disk to store data.</span></span> <span data-ttu-id="cf30c-123">您可以附加空的磁碟和含有資料的磁碟。</span><span class="sxs-lookup"><span data-stu-id="cf30c-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="cf30c-124">如需相關指示，請參閱 [將資料磁碟連接至以傳統部署模型建立的 Windows 虛擬機器](attach-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="cf30c-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
