---
title: "設定端點傳統 Windows VM 上 aaaSet |Microsoft 文件"
description: "針對 Windows VM 在 Azure 傳統入口網站 tooallow 通訊 hello 與 Windows Azure 中虛擬機器學習 tooset 個端點。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="d3f8a-103">如何 tooset 個在 Azure 中的傳統 Windows 虛擬機器上的端點</span><span class="sxs-lookup"><span data-stu-id="d3f8a-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="d3f8a-104">您在 Azure 中使用 hello 傳統部署模型中建立的虛擬機器可以透過與在其他虛擬機器的私人網路通道自動進行通訊的所有 Windows 都 hello 相同雲端服務或虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="d3f8a-105">不過，在 hello 網際網路或其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="d3f8a-106">本文也適用於 [Linux 虛擬機器](../../linux/classic/setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3f8a-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d3f8a-108">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d3f8a-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="d3f8a-110">在 hello**資源管理員**部署模型，使用已設定端點**網路安全性群組 (Nsg)**。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="d3f8a-111">如需詳細資訊，請參閱[允許外部存取 tooyour VM 使用 hello Azure 入口網站](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d3f8a-112">當您建立 Windows 虛擬機器在 hello Azure 入口網站中時，遠端桌面和 Windows PowerShell 遠端執行功能一樣的一般端點會通常為您自動建立。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="d3f8a-113">視需要建立 hello 虛擬機器時或之後，您可以設定其他端點。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="d3f8a-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3f8a-114">Next steps</span></span>
* <span data-ttu-id="d3f8a-115">toouse Azure PowerShell cmdlet tooset，VM 端點，請參閱[Add-azureendpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="d3f8a-116">toouse Azure PowerShell cmdlet toomanage ACL 的端點，請參閱[管理存取控制清單 (Acl) 端點使用 PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="d3f8a-117">如果在 hello Resource Manager 部署模型中建立虛擬機器，您也可以使用 Azure PowerShell[建立網路安全性群組](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md)toocontrol 流量 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="d3f8a-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
