---
title: "在傳統 Windows VM 上設定端點 | Microsoft Docs"
description: "了解如何在 Azure 傳統入口網站中設定 Windows VM 的端點，以允許與 Azure 中的 Windows 虛擬機器進行通訊。"
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
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="4e973-103">如何在 Azure 中的傳統 Windows 虛擬機器上設定端點</span><span class="sxs-lookup"><span data-stu-id="4e973-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="4e973-104">在 Azure 中使用傳統部署模型建立的所有 Windows 虛擬機器，都可以自動透過私人網路通道與同一雲端服務或虛擬網路中的其他虛擬機器通訊。</span><span class="sxs-lookup"><span data-stu-id="4e973-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="4e973-105">不過，網際網路或其他虛擬網路上的電腦需要端點，才能將傳入網路流量導向至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4e973-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="4e973-106">本文也適用於 [Linux 虛擬機器](../../linux/classic/setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="4e973-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e973-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="4e973-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4e973-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4e973-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4e973-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="4e973-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="4e973-110">在 **Resource Manager** 部署模型中，是使用**網路安全性群組 (NSG)** 來設定端點。</span><span class="sxs-lookup"><span data-stu-id="4e973-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="4e973-111">如需詳細資訊，請參閱 [允許使用 Azure 入口網站從外部存取您的 VM](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4e973-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4e973-112">當您在 Azure 入口網站建立 Windows 虛擬機器時，通常也會自動為您建立像是遠端桌面和 Windows PowerShell 遠端等的通用端點。</span><span class="sxs-lookup"><span data-stu-id="4e973-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="4e973-113">建立虛擬機器或日後有需要時，您可以設定其他端點。</span><span class="sxs-lookup"><span data-stu-id="4e973-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="4e973-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e973-114">Next steps</span></span>
* <span data-ttu-id="4e973-115">若要使用 Azure PowerShell Cmdlet 來設定 VM 端點，請參閱 [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e973-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="4e973-116">若要使用 Azure PowerShell Cmdlet 來管理端點上的 ACL，請參閱 [使用 PowerShell 管理端點的存取控制清單 (ACL)](../../../virtual-network/virtual-networks-acl-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="4e973-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="4e973-117">如果您已在 Resource Manager 部署模型中建立虛擬機器，則可以使用 Azure PowerShell 來 [建立網路安全性群組](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) 以控制對 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="4e973-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
