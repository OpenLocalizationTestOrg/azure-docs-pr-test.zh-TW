---
title: "驗證要搭配 Azure RemoteApp 使用的 Azure VNET | Microsoft Docs"
description: "了解如何確定 Azure VNET 已準備好搭配 Azure RemoteApp 使用"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="fd7bc-103">驗證要搭配 Azure RemoteApp 使用的 Azure VNET</span><span class="sxs-lookup"><span data-stu-id="fd7bc-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fd7bc-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fd7bc-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fd7bc-106">在搭配 Azure RemoteApp 使用 Azure VNET 之前，您可能想要驗證 VNET。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="fd7bc-107">這有助於避免發生連線問題。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="fd7bc-108">若要驗證 Azure VNET，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fd7bc-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="fd7bc-109">在您想要搭配 Azure RemoteApp 使用之 Azure VNET 的子網路內建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="fd7bc-110">使用管理入口網站中的 [ **連接** ] 選項連接到該 VM 。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="fd7bc-111">將您想要搭配 Azure RemoteApp 使用的虛擬機器加入至相同網域。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="fd7bc-112">如果您要建立連線到內部部署網路的混合式集合，請將此虛擬機器加入您的本機網域。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="fd7bc-113">如果成功，Azure VNET 已準備好搭配 RemoteApp 使用。</span><span class="sxs-lookup"><span data-stu-id="fd7bc-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="fd7bc-114">如需端對端混合式收藏工作流程的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="fd7bc-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="fd7bc-115">如何針對 Azure RemoteApp 規劃您的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="fd7bc-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="fd7bc-116">建立混合式收藏</span><span class="sxs-lookup"><span data-stu-id="fd7bc-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="fd7bc-117">將 Azure RemoteApp 收藏部署到 Azure 虛擬網路 (支援 ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="fd7bc-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

