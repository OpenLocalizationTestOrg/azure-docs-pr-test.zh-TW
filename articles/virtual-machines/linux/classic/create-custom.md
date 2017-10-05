---
title: "使用 Azure CLI 1.0 建立傳統 Linux VM | Microsoft Docs"
description: "了解如何使用傳統部署模型搭配 Azure CLI 1.0 建立 Linux 虛擬機器"
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
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="0d428-103">如何使用 Azure CLI 1.0 建立傳統 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0d428-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0d428-104">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0d428-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0d428-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0d428-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0d428-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="0d428-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0d428-107">如需 Resource Manager 版本，請參閱[這裡](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0d428-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0d428-108">本主題說明如何使用傳統部署模型，以 Azure CLI 1.0 建立 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="0d428-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="0d428-109">我們將使用 Azure 上可用「映像」  中的 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="0d428-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="0d428-110">Azure CLI 1.0 命令提供下列組態選項：</span><span class="sxs-lookup"><span data-stu-id="0d428-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="0d428-111">將 VM 連線到虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0d428-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="0d428-112">將 VM 加入現有的雲端服務</span><span class="sxs-lookup"><span data-stu-id="0d428-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="0d428-113">將 VM 加入現有的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0d428-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="0d428-114">將 VM 加入可用性集合或位置</span><span class="sxs-lookup"><span data-stu-id="0d428-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d428-115">如果要讓 VM 器使用虛擬網路，以便依主機名稱來連接虛擬機器，或設定跨單位連線，則必須在建立 VM 時指定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0d428-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="0d428-116">只有在建立 VM 時，才能將 VM 設定為加入虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0d428-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="0d428-117">如需虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](http://go.microsoft.com/fwlink/p/?LinkID=294063)。</span><span class="sxs-lookup"><span data-stu-id="0d428-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="0d428-118">如何使用傳統的部署模型建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0d428-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

