---
title: "aaaCreate hello Azure 入口網站中的 VM |Microsoft 文件"
description: "在 hello Azure 入口網站中建立 Windows 虛擬機器。"
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
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="721c9-103">建立執行 Windows hello Azure 入口網站中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="721c9-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="721c9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="721c9-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="721c9-105">PowerShell：傳統部署</span><span class="sxs-lookup"><span data-stu-id="721c9-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="721c9-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="721c9-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="721c9-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="721c9-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="721c9-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="721c9-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="721c9-109">了解如何太[使用 hello Resource Manager 部署的模型執行這些步驟](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)使用 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="721c9-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="721c9-110">本教學課程示範如何 toocreate Azure hello Azure 入口網站中執行 Windows 的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="721c9-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="721c9-111">我們將使用 Windows Server 映像，例如，但是，這是只有一個許多映像的 hello Azure 優惠。</span><span class="sxs-lookup"><span data-stu-id="721c9-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="721c9-112">請注意，您可以選擇何種映像取決於您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="721c9-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="721c9-113">例如，Windows 桌面映像可能是可用 tooMSDN 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="721c9-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="721c9-114">這個區段會顯示如何 toouse hello**儀表板**在 hello Azure 入口網站 tooselect，然後再建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="721c9-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="721c9-115">您也可以使用 [您自己的映像](createupload-vhd.md)來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="721c9-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="721c9-116">toolearn 有關這個主題以及其他方法，請參閱[不同的方式 toocreate Windows 虛擬機器](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="721c9-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="721c9-117"><a id="createvirtualmachine"></a>建立 hello 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="721c9-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="721c9-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="721c9-118">Next steps</span></span>
* <span data-ttu-id="721c9-119">了解如何太[使用 hello Resource Manager 部署模型建立 VM](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="721c9-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="721c9-120">登入 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="721c9-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="721c9-121">如需指示，請參閱[登入執行 Windows Server 的虛擬機器 tooa](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="721c9-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="721c9-122">附加磁碟 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="721c9-122">Attach a disk toostore data.</span></span> <span data-ttu-id="721c9-123">您可以附加空的磁碟和含有資料的磁碟。</span><span class="sxs-lookup"><span data-stu-id="721c9-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="721c9-124">如需指示，請參閱 hello[附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型](attach-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="721c9-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
