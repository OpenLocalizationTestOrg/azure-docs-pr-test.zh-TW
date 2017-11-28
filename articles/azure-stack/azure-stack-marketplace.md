---
title: "aaaPublish 自訂的服務商場中的項目 Azure 堆疊 （雲端操作員） |Microsoft 文件"
description: "雲端操作員，了解 toopublish 自訂 marketplace Azure 堆疊中的項目。"
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
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a><span data-ttu-id="bbe70-103">hello Azure 堆疊 Marketplace 概觀</span><span class="sxs-lookup"><span data-stu-id="bbe70-103">hello Azure Stack Marketplace overview</span></span>
<span data-ttu-id="bbe70-104">hello Marketplace 是服務、 應用程式和自訂 Azure 堆疊，例如網路、 虛擬機器、 儲存和等等的資源集合。</span><span class="sxs-lookup"><span data-stu-id="bbe70-104">hello Marketplace is a collection of services, applications, and resources customized for Azure Stack, like networks, virtual machines, storage, and so on.</span></span> <span data-ttu-id="bbe70-105">使用者過來 toocreate 新的資源，並部署新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bbe70-105">Users come here toocreate new resources and deploy new applications.</span></span> <span data-ttu-id="bbe70-106">將它視為購物目錄使用者可以瀏覽並選擇 hello 項目他們想 toouse。</span><span class="sxs-lookup"><span data-stu-id="bbe70-106">Think of it as a shopping catalog where users can browse and choose hello items they want toouse.</span></span> <span data-ttu-id="bbe70-107">toouse Marketplace 項目，使用者必須訂閱 tooan 供應項目會授與他們存取 toohello 項目。</span><span class="sxs-lookup"><span data-stu-id="bbe70-107">toouse a Marketplace item, users must subscribe tooan offer that grants them access toohello item.</span></span>

<span data-ttu-id="bbe70-108">雲端操作員，您可以決定哪些項目 tooadd （發行） toohello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="bbe70-108">As a cloud operator, you decide which items tooadd (publish) toohello Marketplace.</span></span> <span data-ttu-id="bbe70-109">您可以發佈像資料庫、應用程式服務等等的項目。</span><span class="sxs-lookup"><span data-stu-id="bbe70-109">You can publish things like databases, App Services, and so on.</span></span> <span data-ttu-id="bbe70-110">這讓它們看 tooall 您的使用者。</span><span class="sxs-lookup"><span data-stu-id="bbe70-110">This makes them visible tooall your users.</span></span> <span data-ttu-id="bbe70-111">您可以發佈您所建立的自訂項目。</span><span class="sxs-lookup"><span data-stu-id="bbe70-111">You can publish custom items that you create.</span></span> <span data-ttu-id="bbe70-112">您也可以從成長中的 [Azure Marketplace 項目清單](azure-stack-marketplace-azure-items.md)內發佈項目。</span><span class="sxs-lookup"><span data-stu-id="bbe70-112">You can also publish items from a growing [list of Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="bbe70-113">當您發行的項目 toohello Marketplace 時，使用者可以看到它五分鐘內。</span><span class="sxs-lookup"><span data-stu-id="bbe70-113">When you publish an item toohello Marketplace, users can see it within five minutes.</span></span>

<span data-ttu-id="bbe70-114">按一下 tooopen hello Marketplace，**新增**。</span><span class="sxs-lookup"><span data-stu-id="bbe70-114">tooopen hello Marketplace, click **New**.</span></span>

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a><span data-ttu-id="bbe70-115">Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="bbe70-115">Marketplace items</span></span>
<span data-ttu-id="bbe70-116">Azure Stack Marketplace 項目是您的使用者可下載並使用的服務、應用程式與資源。</span><span class="sxs-lookup"><span data-stu-id="bbe70-116">An Azure Stack Marketplace item is a service, application, or resource that your users can download and use.</span></span> <span data-ttu-id="bbe70-117">所有 Azure 堆疊 Marketplace 項目是可見的 tooall 您的使用者。</span><span class="sxs-lookup"><span data-stu-id="bbe70-117">All Azure Stack Marketplace items are visible tooall your users.</span></span>

<span data-ttu-id="bbe70-118">每個 Marketplace 項目都有：</span><span class="sxs-lookup"><span data-stu-id="bbe70-118">Every Marketplace item has:</span></span>

* <span data-ttu-id="bbe70-119">供資源佈建使用的 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="bbe70-119">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="bbe70-120">中繼資料，像是字串、圖示與其他行銷關聯資料</span><span class="sxs-lookup"><span data-stu-id="bbe70-120">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="bbe70-121">格式化 hello 入口網站中的資訊 toodisplay hello 項目</span><span class="sxs-lookup"><span data-stu-id="bbe70-121">Formatting information toodisplay hello item in hello portal</span></span>

<span data-ttu-id="bbe70-122">每個項目已發佈的 toohello Marketplace 使用格式稱為的 hello Azure 圖庫套件 (azpkg)。</span><span class="sxs-lookup"><span data-stu-id="bbe70-122">Every item published toohello Marketplace uses a format called hello Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="bbe70-123">將部署或執行階段的資源 （例如程式碼軟體或虛擬機器映像的 zip 檔案） 新增 tooAzure 分別堆疊不是一部分的 hello Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="bbe70-123">Add deployment or runtime resources (like code, zip files with software, or virtual machine images) tooAzure Stack separately, not as part of hello Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bbe70-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bbe70-124">Next steps</span></span>
[<span data-ttu-id="bbe70-125">建立及發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="bbe70-125">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)

