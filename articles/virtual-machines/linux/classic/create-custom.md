---
title: "傳統 Linux VM，使用 aaaCreate hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何 toocreate Linux 虛擬機器使用 Azure CLI 1.0 hello hello 傳統部署模型"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="947c0-103">與傳統 Linux VM 的 tooCreate hello Azure CLI 1.0 的方式</span><span class="sxs-lookup"><span data-stu-id="947c0-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="947c0-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="947c0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="947c0-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="947c0-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="947c0-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="947c0-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="947c0-107">Hello 資源管理員版本，請參閱[這裡](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="947c0-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="947c0-108">本主題描述如何 toocreate Linux 虛擬機器 (VM) 與使用 Azure CLI 1.0 hello hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="947c0-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="947c0-109">我們使用 Linux 映像，從可用的 hello**映像**在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="947c0-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="947c0-110">hello Azure CLI 1.0，提供下列設定選項，和其他項目 hello:</span><span class="sxs-lookup"><span data-stu-id="947c0-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="947c0-111">Hello VM tooa 虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="947c0-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="947c0-112">加入 hello VM tooan 現有雲端服務</span><span class="sxs-lookup"><span data-stu-id="947c0-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="947c0-113">新增 hello VM tooan 現有儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="947c0-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="947c0-114">新增 hello VM tooan 可用性設定組或位置</span><span class="sxs-lookup"><span data-stu-id="947c0-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="947c0-115">如果您希望您 VM toouse 虛擬網路，讓您能連接 tooit 直接以主機名稱或設定跨單位連線，請確定您在建立 hello VM 時指定 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="947c0-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="947c0-116">只有在您建立 hello VM 時，VM 可能會設定的 toojoin 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="947c0-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="947c0-117">如需虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](http://go.microsoft.com/fwlink/p/?LinkID=294063)。</span><span class="sxs-lookup"><span data-stu-id="947c0-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="947c0-118">如何使用 Linux VM 的 toocreate hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="947c0-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

