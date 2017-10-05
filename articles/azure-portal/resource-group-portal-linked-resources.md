---
title: "磚庫中相關的資源與連結的資源"
description: "了解 Azure Preview 入口網站磚庫中的相關資源和連結資源。"
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="2c508-103">磚庫中相關的資源與連結的資源</span><span class="sxs-lookup"><span data-stu-id="2c508-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="2c508-104">磚庫可讓您尋找磚的特定資源，並將其拖曳到您目前的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c508-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="2c508-105">您可以使用磚庫建立跨越資源的管理檢視。</span><span class="sxs-lookup"><span data-stu-id="2c508-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="2c508-106">對於任何指定的資源，相關的資源會在它的資源群組中包含所有資源，以及連結到資源或從資源連結而來的任何資源。</span><span class="sxs-lookup"><span data-stu-id="2c508-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="2c508-107">Resource Manager 中連結的資源</span><span class="sxs-lookup"><span data-stu-id="2c508-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="2c508-108">連結是 Resource Manager 的一項功能。</span><span class="sxs-lookup"><span data-stu-id="2c508-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="2c508-109">它可讓您宣告資源之間的關聯性，即使它們不是存放在相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2c508-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="2c508-110">連結不會影響資源的執行階段、計費，以及以角色為基礎的存取。</span><span class="sxs-lookup"><span data-stu-id="2c508-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="2c508-111">它只是一個可以用來表示關聯性的機制，以便如磚庫等工具可以提供豐富的管理體驗。</span><span class="sxs-lookup"><span data-stu-id="2c508-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="2c508-112">您的工具可以使用連結 API 檢查連結，同時提供自訂的關聯性管理體驗。</span><span class="sxs-lookup"><span data-stu-id="2c508-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="2c508-113">如何連結我的資源？</span><span class="sxs-lookup"><span data-stu-id="2c508-113">How do I link my resources?</span></span>
<span data-ttu-id="2c508-114">當您透過入口網站或透過 Azure PowerShell 或 Azure CLI 部署範本建立資源時，就會自動為某些相依的資源建立連結。</span><span class="sxs-lookup"><span data-stu-id="2c508-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="2c508-115">您也可以使用[連結的資源 REST API](/rest/api/resources/resourcelinks)，以程式設計方式連結資源。</span><span class="sxs-lookup"><span data-stu-id="2c508-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c508-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c508-116">Next steps</span></span>
* <span data-ttu-id="2c508-117">如果您需要撰寫 Resource Manager 範本的簡介，請參閱[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2c508-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2c508-118">若要深入了解如何透過入口網站使用資源群組，請參閱[使用 Azure 入口網站管理 Azure 資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2c508-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

