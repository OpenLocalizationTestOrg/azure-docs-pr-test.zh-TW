---
title: "發佈 Azure Stack (雲端操作員) 中的自訂 Marketplace 項目 | Microsoft Docs"
description: "您身為雲端操作員，應了解如何發佈 Azure Stack 中的自訂 Marketplace 項目。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: be61e746d97fbce166f44262fcc33e2f7118fd82
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="the-azure-stack-marketplace-overview"></a><span data-ttu-id="aac62-103">Azure Stack Marketplace 概觀</span><span class="sxs-lookup"><span data-stu-id="aac62-103">The Azure Stack Marketplace overview</span></span>
<span data-ttu-id="aac62-104">Marketplace 是一組針對 Azure Stack 自訂的服務、應用程式與資源集合，像是網路、虛擬機器、儲存體等等。</span><span class="sxs-lookup"><span data-stu-id="aac62-104">The Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="aac62-105">這是使用者用以建立新資源及部署新應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="aac62-105">Users come here to create new resources and deploy new applications.</span></span> <span data-ttu-id="aac62-106">不妨將其視為購物目錄，使用者可以在此瀏覽並選擇他們想要使用的項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-106">Think of it as a shopping catalog where users can browse and choose the items they want to use.</span></span> <span data-ttu-id="aac62-107">若要使用 Marketplace 項目，使用者必須訂閱會授與他們項目存取權的產品。</span><span class="sxs-lookup"><span data-stu-id="aac62-107">To use a Marketplace item, users must subscribe to an offer that grants them access to the item.</span></span>

<span data-ttu-id="aac62-108">您身為雲端操作員，可以決定要新增 (發佈) 到 Marketplace 中的項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-108">As a cloud operator, you decide which items to add (publish) to the Marketplace.</span></span> <span data-ttu-id="aac62-109">您可以發佈像資料庫、應用程式服務等等的項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="aac62-110">這會讓所有的使用者都可以看到它們。</span><span class="sxs-lookup"><span data-stu-id="aac62-110">This makes them visible to all your users.</span></span> <span data-ttu-id="aac62-111">您可以發佈您所建立的自訂項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-111">You can publish custom items that you create.</span></span> <span data-ttu-id="aac62-112">您也可以從成長中的 [Azure Marketplace 項目清單](azure-stack-marketplace-azure-items.md)內發佈項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="aac62-113">當您將項目發佈到 Marketplace 中，使用者在五分鐘內就可看到它。</span><span class="sxs-lookup"><span data-stu-id="aac62-113">When you publish an item to the Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="aac62-114">若要開啟 Marketplace，請按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="aac62-114">To open the Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="aac62-115">Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="aac62-115">Marketplace items</span></span>
<span data-ttu-id="aac62-116">Azure Stack Marketplace 項目是您的使用者可下載並使用的服務、應用程式與資源。</span><span class="sxs-lookup"><span data-stu-id="aac62-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="aac62-117">您所有的使用者都可以看到所有 Azure Stack Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="aac62-117">All Azure Stack Marketplace items are visible to all your users.</span></span>

<span data-ttu-id="aac62-118">每個 Marketplace 項目都有：</span><span class="sxs-lookup"><span data-stu-id="aac62-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="aac62-119">供資源佈建使用的 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="aac62-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="aac62-120">中繼資料，像是字串、圖示與其他行銷關聯資料</span><span class="sxs-lookup"><span data-stu-id="aac62-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="aac62-121">顯示入口網站中項目的格式化資訊</span><span class="sxs-lookup"><span data-stu-id="aac62-121">Formatting information to display the item in the portal</span></span>

<span data-ttu-id="aac62-122">發佈至 Marketplace 的每個項目，都會使用稱為 Azure 資源庫封裝 (azpkg) 的格式。</span><span class="sxs-lookup"><span data-stu-id="aac62-122">Every item published to the Marketplace uses a format called the Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="aac62-123">請分別將部署或執行階段資源 (如代碼、含軟體的 Zip 檔或虛擬機器映像) 新增到 Azure Stack 中，而不是當作 Marketplace 項目的一部分。</span><span class="sxs-lookup"><span data-stu-id="aac62-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) to Azure Stack separately, not as part of the Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aac62-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aac62-124">Next steps</span></span>
[<span data-ttu-id="aac62-125">建立及發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="aac62-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

