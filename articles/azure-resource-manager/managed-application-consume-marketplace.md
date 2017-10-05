---
title: "在 Marketplace 中使用 Azure 受管理的應用程式 | Microsoft Docs"
description: "描述如何建立可透過 Marketplace 取得的 Azure 受管理的應用程式。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="96290-103">使用 Marketplace 中 Azure 受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="96290-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="96290-104">如[受管理的應用程式概觀](managed-application-overview.md)一文中所討論，端對端體驗中有兩種案例。</span><span class="sxs-lookup"><span data-stu-id="96290-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="96290-105">其中一個是發行者或廠商，是要建立受管理的應用程式供客戶使用。</span><span class="sxs-lookup"><span data-stu-id="96290-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="96290-106">第二個是受管理應用程式的客戶或取用者。</span><span class="sxs-lookup"><span data-stu-id="96290-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="96290-107">本文涵蓋第二個案例。</span><span class="sxs-lookup"><span data-stu-id="96290-107">This article covers the second scenario.</span></span> <span data-ttu-id="96290-108">它會描述您可以如何從 Microsoft Azure Marketplace 部署受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96290-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="96290-109">從 Marketplace 建立</span><span class="sxs-lookup"><span data-stu-id="96290-109">Create from the Marketplace</span></span>

<span data-ttu-id="96290-110">從 Marketplace 部署受管理的應用程式類似於從 Marketplace 部署任何類型的資源。</span><span class="sxs-lookup"><span data-stu-id="96290-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="96290-111">在入口網站中，選取 [+ 新增]，並搜尋要部署的解決方案類型。</span><span class="sxs-lookup"><span data-stu-id="96290-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="96290-112">從可用的選項，選取您需要的選項。</span><span class="sxs-lookup"><span data-stu-id="96290-112">From the available options, select the one you need.</span></span>

![搜尋解決方案](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="96290-114">檢閱應用程式的摘要，並選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="96290-114">Review the summary of the application, and select **Create**.</span></span>

![建立受管理的應用程式](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="96290-116">如同任何其他解決方案，您會看到要提供值的欄位。</span><span class="sxs-lookup"><span data-stu-id="96290-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="96290-117">這些欄位會因您建立的受管理應用程式類型而變。</span><span class="sxs-lookup"><span data-stu-id="96290-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="96290-118">檢視支援資訊</span><span class="sxs-lookup"><span data-stu-id="96290-118">View support information</span></span>

<span data-ttu-id="96290-119">部署受管理的應用程式之後，檢視應用程式的支援資訊。</span><span class="sxs-lookup"><span data-stu-id="96290-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="96290-120">在 [受管理的應用程式] 刀鋒視窗中，會列出支援資訊。</span><span class="sxs-lookup"><span data-stu-id="96290-120">In the managed application blade, the support information is listed.</span></span>

![支援](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="96290-122">檢視發行者權限</span><span class="sxs-lookup"><span data-stu-id="96290-122">View publisher permissions</span></span>

<span data-ttu-id="96290-123">管理您應用程式的廠商會被授與資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="96290-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="96290-124">若要查看這些權限，請選取 [授權]。</span><span class="sxs-lookup"><span data-stu-id="96290-124">To see those permissions, select **Authorizations**.</span></span>

![授權](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="96290-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96290-126">Next steps</span></span>

* <span data-ttu-id="96290-127">如需在 Marketplace 中發行受管理應用程式的詳細資訊，請參閱 [Marketplace 中 Azure 受管理的應用程式](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="96290-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="96290-128">若要發行只供您組織中使用者使用之受管理的應用程式，請參閱[建立和發行 Service Catalog 受管理的應用程式](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="96290-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="96290-129">若要使用只供您組織中使用者使用之受管理的應用程式，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="96290-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>