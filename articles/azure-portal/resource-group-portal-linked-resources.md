---
title: "aaaRelated 和連結的資源，在 hello 並排組件庫"
description: "深入了解相關和連結會顯示在 hello hello Azure 預覽入口網站的 並排顯示組件庫中的資源。"
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
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="07839-103">Hello 並排組件庫中的連結與相關資源</span><span class="sxs-lookup"><span data-stu-id="07839-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="07839-104">hello 磚圖庫可讓您的特定資源的 toofind 磚，並將其拖曳至您目前的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07839-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="07839-105">使用 hello 磚資源庫，您可以建立跨越資源的管理檢視。</span><span class="sxs-lookup"><span data-stu-id="07839-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="07839-106">對於任何指定的資源，hello 與相關資源在其資源群組和任何連結 tooor 從 hello 資源的資源包括 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="07839-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="07839-107">Resource Manager 中連結的資源</span><span class="sxs-lookup"><span data-stu-id="07839-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="07839-108">連結是 hello 資源管理員的功能。</span><span class="sxs-lookup"><span data-stu-id="07839-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="07839-109">它可讓您 toodeclare 資源之間的關聯性即使它們不在 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="07839-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="07839-110">連結您的資源不會影響帳單及不影響的角色型存取的 hello 執行階段任何影響。</span><span class="sxs-lookup"><span data-stu-id="07839-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="07839-111">它是只是您可以使用 toorepresent 關聯性，讓工具 hello 磚圖庫可以提供豐富的管理體驗的機制。</span><span class="sxs-lookup"><span data-stu-id="07839-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="07839-112">您的工具可以檢查 hello 連結使用 hello 連結應用程式開發介面，並提供自訂的關聯性的管理也體驗。</span><span class="sxs-lookup"><span data-stu-id="07839-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="07839-113">如何連結我的資源？</span><span class="sxs-lookup"><span data-stu-id="07839-113">How do I link my resources?</span></span>
<span data-ttu-id="07839-114">當您建立資源，透過 hello 入口網站，或藉由部署範本，以透過 Azure PowerShell 或 Azure CLI 時，某些相依的資源時，會自動建立連結。</span><span class="sxs-lookup"><span data-stu-id="07839-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="07839-115">您也以程式設計方式可以將資源連結使用 hello[連結資源的 REST API](/rest/api/resources/resourcelinks)。</span><span class="sxs-lookup"><span data-stu-id="07839-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07839-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07839-116">Next steps</span></span>
* <span data-ttu-id="07839-117">如果您需要簡介 toowriting 資源管理員範本，請參閱[撰寫樣板](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="07839-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="07839-118">toounderstand 進一步了解使用資源群組，透過 hello 入口網站，請參閱[使用 hello Azure 入口網站 toomanage 您的 Azure 資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="07839-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

