---
title: "使用 Azure RemoteApp aaaValidate hello Azure VNET toouse |Microsoft 文件"
description: "了解如何 toomake 確定 Azure VNET 準備使用 Azure RemoteApp toouse"
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
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="6df1d-103">驗證與 Azure RemoteApp 一起 hello Azure VNET toouse</span><span class="sxs-lookup"><span data-stu-id="6df1d-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6df1d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="6df1d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6df1d-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6df1d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6df1d-106">您可以使用 Azure VNET 與 Azure RemoteApp 之前，您可能想 toovalidate hello VNET。</span><span class="sxs-lookup"><span data-stu-id="6df1d-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="6df1d-107">這有助於避免發生連線問題。</span><span class="sxs-lookup"><span data-stu-id="6df1d-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="6df1d-108">toovalidate Azure VNET 中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="6df1d-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="6df1d-109">建立 Azure 虛擬機器內的 hello Azure VNET，您想要使用 Azure RemoteApp toouse hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="6df1d-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="6df1d-110">使用 hello 連線 toothat VM**連接**hello 管理入口網站中的選項。</span><span class="sxs-lookup"><span data-stu-id="6df1d-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="6df1d-111">加入 hello 虛擬機器 toohello 您想使用 Azure RemoteApp toouse 相同的網域。</span><span class="sxs-lookup"><span data-stu-id="6df1d-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="6df1d-112">如果您要建立混合式集合 tooyour 在內部部署網路連線，再加入 hello 虛擬機器 tooyour 本機網域。</span><span class="sxs-lookup"><span data-stu-id="6df1d-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="6df1d-113">如果成功，hello Azure VNET 是準備 toouse RemoteApp 使用。</span><span class="sxs-lookup"><span data-stu-id="6df1d-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="6df1d-114">如需 hello 端對端混合式集合工作流程的詳細資訊，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="6df1d-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="6df1d-115">如何 tooplan 的 Azure RemoteApp 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6df1d-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="6df1d-116">建立混合式收藏</span><span class="sxs-lookup"><span data-stu-id="6df1d-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="6df1d-117">部署 Azure RemoteApp 集合 tooyour Azure 虛擬網路 （透過 ExpressRoute 支援）</span><span class="sxs-lookup"><span data-stu-id="6df1d-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

