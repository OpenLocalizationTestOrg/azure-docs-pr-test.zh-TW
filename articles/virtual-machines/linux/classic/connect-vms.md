---
title: "連線雲端服務中的 Linux VM | Microsoft Docs"
description: "將利用傳統部署模型所建立的 Linux 虛擬機器連線至 Azure 雲端服務或虛擬網路。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: e222645509640b104410f87e4bcd22834c8d9ec1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-linux-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="e1e25-103">透過虛擬網路或雲端服務來連線利用傳統部署模型所建立的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e1e25-103">Connect Linux virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1e25-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="e1e25-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e1e25-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="e1e25-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e1e25-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="e1e25-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e1e25-107">以傳統部署模型所建立的 Linux 虛擬機器一律會放置於雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="e1e25-107">Linux virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="e1e25-108">雲端服務能做為容器，並提供唯一的公用 DNS 名稱、公用 IP 位址，以及一組透過網際網路存取虛擬機器的端點。</span><span class="sxs-lookup"><span data-stu-id="e1e25-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="e1e25-109">雲端服務可以位於虛擬網路，但這不是必要條件。</span><span class="sxs-lookup"><span data-stu-id="e1e25-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="e1e25-110">您也可以[透過虛擬網路或雲端服務來連線 Windows 虛擬機器](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e1e25-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="e1e25-111">如果雲端服務不在虛擬網路中，就稱為 *獨立* 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e1e25-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="e1e25-112">獨立雲端服務中的虛擬機器可以使用其他虛擬機器的公用 DNS 名稱與其他虛擬機器通訊，且流量會透過網際網路傳送。</span><span class="sxs-lookup"><span data-stu-id="e1e25-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="e1e25-113">如果雲端服務是在虛擬網路中，該雲端服務中的虛擬機器可與虛擬網路中的所有其他虛擬機器通訊，而不需要透過網際網路傳送任何流量。</span><span class="sxs-lookup"><span data-stu-id="e1e25-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="e1e25-114">如果您將虛擬機器放在同一個獨立雲端服務中，您仍然可以使用負載平衡和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="e1e25-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="e1e25-115">如需詳細資訊，請參閱[虛擬機器負載平衡](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)和[管理虛擬機器的可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e1e25-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage the availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e1e25-116">不過，您無法組織子網路上的虛擬機器，或將獨立雲端服務連線到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="e1e25-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="e1e25-117">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="e1e25-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="e1e25-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1e25-118">Next steps</span></span>
<span data-ttu-id="e1e25-119">建立虛擬機器之後，最好 [新增資料磁碟](attach-disk.md) ，讓服務與工作負載有存放資料的地方。</span><span class="sxs-lookup"><span data-stu-id="e1e25-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
