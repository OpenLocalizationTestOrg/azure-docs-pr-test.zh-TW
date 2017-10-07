---
title: "aaaConnect Linux Vm 的雲端服務 |Microsoft 文件"
description: "連接使用 hello 傳統部署模型 tooan Azure 雲端服務或虛擬網路建立的 Linux 虛擬機器。"
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
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="4c002-103">使用與虛擬網路或雲端服務的 hello 傳統部署模型建立的 Linux 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="4c002-103">Connect Linux virtual machines created with hello classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4c002-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="4c002-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c002-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4c002-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4c002-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="4c002-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="4c002-107">一定會與 hello 傳統部署模型所建立的 Linux 虛擬機器放置在雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4c002-107">Linux virtual machines created with hello classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="4c002-108">hello 雲端服務做為容器，並透過 hello 網際網路提供唯一的公開 DNS 名稱、 公用 IP 位址，以及一組端點 tooaccess hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4c002-108">hello cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints tooaccess hello virtual machine over hello Internet.</span></span> <span data-ttu-id="4c002-109">hello 雲端服務是在虛擬網路中，但並非必要條件。</span><span class="sxs-lookup"><span data-stu-id="4c002-109">hello cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="4c002-110">您也可以[透過虛擬網路或雲端服務來連線 Windows 虛擬機器](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4c002-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="4c002-111">如果雲端服務不在虛擬網路中，就稱為 *獨立* 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4c002-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="4c002-112">hello 獨立雲端服務中的虛擬機器與其他虛擬機器使用通訊 hello 其他虛擬機器的公用 DNS 名稱，和 hello 流量，透過網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="4c002-112">hello virtual machines in a standalone cloud service communicate with other virtual machines by using hello other virtual machines’ public DNS names, and hello traffic travels over hello Internet.</span></span> <span data-ttu-id="4c002-113">如果雲端服務是虛擬網路，hello 虛擬機器，雲端服務可以與 hello 虛擬網路中的所有其他虛擬機器沒有任何流量傳送 hello 網際網路上通訊。</span><span class="sxs-lookup"><span data-stu-id="4c002-113">If a cloud service is in a virtual network, hello virtual machines in that cloud service can communicate with all other virtual machines in hello virtual network without sending any traffic over hello Internet.</span></span>

<span data-ttu-id="4c002-114">如果您將您的虛擬機器中的 hello 相同獨立雲端服務，您仍然可以使用負載平衡和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="4c002-114">If you place your virtual machines in hello same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="4c002-115">如需詳細資訊，請參閱[負載平衡虛擬機器](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)和[管理虛擬機器可用性 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4c002-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage hello availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4c002-116">不過，您無法組織 hello 子網路上的虛擬機器，或將獨立雲端服務 tooyour 在內部部署網路連線。</span><span class="sxs-lookup"><span data-stu-id="4c002-116">However, you can't organize hello virtual machines on subnets or connect a standalone cloud service tooyour on-premises network.</span></span> <span data-ttu-id="4c002-117">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="4c002-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="4c002-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c002-118">Next steps</span></span>
<span data-ttu-id="4c002-119">建立虛擬機器之後，就是個好主意太[新增資料磁碟](attach-disk.md)讓您的服務和工作負載有位置 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="4c002-119">After you create a virtual machine, it's a good idea too[add a data disk](attach-disk.md) so your services and workloads have a location toostore data.</span></span>
