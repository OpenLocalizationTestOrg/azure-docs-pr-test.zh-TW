---
title: "Azure 受管理應用程式 marketplace 中 aaaConsume |Microsoft 文件"
description: "Describeshow toocreate Azure 受管理應用程式，可透過 hello Marketplace。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="66c7d-103">使用 Azure 受管理 hello Marketplace 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="66c7d-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="66c7d-104">Hello 中所述[受管理的應用程式概觀](managed-application-overview.md)文章、 hello 端點 tooend 體驗中有兩種案例。</span><span class="sxs-lookup"><span data-stu-id="66c7d-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="66c7d-105">其中一個是 hello 發行者或想 toocreate 供客戶使用的 managed 應用程式廠商。</span><span class="sxs-lookup"><span data-stu-id="66c7d-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="66c7d-106">hello 第二個是 hello 一般客戶或 hello 取用者 hello 受管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="66c7d-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="66c7d-107">本文涵蓋 hello 第二個案例。</span><span class="sxs-lookup"><span data-stu-id="66c7d-107">This article covers hello second scenario.</span></span> <span data-ttu-id="66c7d-108">它會描述如何部署來自 hello Microsoft Azure Marketplace 的受管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="66c7d-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="66c7d-109">建立從 hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="66c7d-109">Create from hello Marketplace</span></span>

<span data-ttu-id="66c7d-110">部署受管理的應用程式從 hello Marketplace 是類似 toodeploying 任何類型的 hello Marketplace 的資源。</span><span class="sxs-lookup"><span data-stu-id="66c7d-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="66c7d-111">在 hello 入口網站中，選取  **+ 新增**，並搜尋解決方案 toodeploy hello 型別。</span><span class="sxs-lookup"><span data-stu-id="66c7d-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="66c7d-112">從 hello 可用的選項，選取您需要一個 hello。</span><span class="sxs-lookup"><span data-stu-id="66c7d-112">From hello available options, select hello one you need.</span></span>

![搜尋解決方案](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="66c7d-114">檢閱 hello 摘要 hello 應用程式，並選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="66c7d-114">Review hello summary of hello application, and select **Create**.</span></span>

![建立受管理的應用程式](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="66c7d-116">如同任何其他解決方案，您會看到欄位 tooprovide 值。</span><span class="sxs-lookup"><span data-stu-id="66c7d-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="66c7d-117">這些欄位會因您所建立的受管理應用程式的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="66c7d-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="66c7d-118">檢視支援資訊</span><span class="sxs-lookup"><span data-stu-id="66c7d-118">View support information</span></span>

<span data-ttu-id="66c7d-119">Managed 應用程式已經部署之後，檢視 hello hello 應用程式的支援資訊。</span><span class="sxs-lookup"><span data-stu-id="66c7d-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="66c7d-120">在 hello 受管理的應用程式 刀鋒視窗會列出 hello 支援資訊。</span><span class="sxs-lookup"><span data-stu-id="66c7d-120">In hello managed application blade, hello support information is listed.</span></span>

![支援](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="66c7d-122">檢視發行者權限</span><span class="sxs-lookup"><span data-stu-id="66c7d-122">View publisher permissions</span></span>

<span data-ttu-id="66c7d-123">管理您的應用程式的 hello 廠商會授與存取 tooyour 資源。</span><span class="sxs-lookup"><span data-stu-id="66c7d-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="66c7d-124">這些權限，選取 toosee**授權**。</span><span class="sxs-lookup"><span data-stu-id="66c7d-124">toosee those permissions, select **Authorizations**.</span></span>

![授權](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="66c7d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66c7d-126">Next steps</span></span>

* <span data-ttu-id="66c7d-127">如需在 hello Marketplace 中發佈受管理的應用程式資訊，請參閱[Azure 受管理應用程式 Marketplace 中](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="66c7d-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="66c7d-128">toopublish 管理只使用 toousers 組織中的應用程式請參閱[建立服務類別目錄管理應用程式並發行](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="66c7d-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="66c7d-129">tooconsume 管理只使用 toousers 組織中的應用程式請參閱[取用服務類別目錄管理應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="66c7d-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
