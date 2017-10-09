---
title: "個傳統的 Linux VM 上端點的 aaaSet |Microsoft 文件"
description: "針對 Linux VM 在 Azure 傳統入口網站 tooallow 通訊 hello 與 Azure 中 Linux 虛擬機器學習 tooset 個端點"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="2929a-103">如何 tooset 向上 Linux 傳統 Azure 中虛擬機器上的端點</span><span class="sxs-lookup"><span data-stu-id="2929a-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="2929a-104">您在 Azure 中使用 hello 傳統部署模型中建立的所有 Linux 虛擬機器可以自動透過都通訊與 hello 中其他虛擬機器的私人網路通道相同雲端服務或虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2929a-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="2929a-105">不過，在 hello 網際網路或其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2929a-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="2929a-106">本文也適用於 [Windows 虛擬機器](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2929a-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2929a-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="2929a-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2929a-108">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="2929a-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2929a-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="2929a-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="2929a-110">在 hello**資源管理員**部署模型，使用已設定端點**網路安全性群組 (Nsg)**。</span><span class="sxs-lookup"><span data-stu-id="2929a-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="2929a-111">如需詳細資訊，請參閱[開啟連接埠和端點](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2929a-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2929a-112">當您建立 Linux 虛擬機器在 hello Azure 入口網站中時，端點的安全殼層 (SSH) 是通常為您自動建立。</span><span class="sxs-lookup"><span data-stu-id="2929a-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="2929a-113">視需要建立 hello 虛擬機器時或之後，您可以設定其他端點。</span><span class="sxs-lookup"><span data-stu-id="2929a-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="2929a-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2929a-114">Next steps</span></span>
* <span data-ttu-id="2929a-115">您也可以建立的 VM 端點使用 hello [Azure 命令列介面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="2929a-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="2929a-116">執行 hello **azure vm 端點，請建立**命令。</span><span class="sxs-lookup"><span data-stu-id="2929a-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="2929a-117">如果在 hello Resource Manager 部署模型中建立虛擬機器，您也可以使用資源管理員模式中的 hello Azure CLI[建立網路安全性群組](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md)toocontrol 流量 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="2929a-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
