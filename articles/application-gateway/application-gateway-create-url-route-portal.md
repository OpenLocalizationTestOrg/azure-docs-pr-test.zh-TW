---
title: "建立路徑型規則 - Azure 應用程式閘道 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用入口網站為應用程式閘道建立路徑型規則"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="69682-103">使用入口網站為應用程式閘道建立路徑型規則</span><span class="sxs-lookup"><span data-stu-id="69682-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69682-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="69682-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="69682-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="69682-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="69682-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69682-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="69682-107">URL 路徑型路由可讓您根據 Http 要求的 URL 路徑來關聯路由。</span><span class="sxs-lookup"><span data-stu-id="69682-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="69682-108">它會檢查是否有路由連至針對「應用程式閘道」中的 URL 清單設定的後端集區，並將網路流量傳送至定義的後端集區。</span><span class="sxs-lookup"><span data-stu-id="69682-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="69682-109">URL 型路由的常見用法是將不同內容類型的要求負載平衡至不同的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="69682-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="69682-110">URL 型路由會將新的規則類型引進應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="69682-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="69682-111">應用程式閘道具有兩種規則類型：基本和路徑型規則。</span><span class="sxs-lookup"><span data-stu-id="69682-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="69682-112">基本規則類型會針對後端集區提供循環配置資源服務，而路徑型規則除了循環配置資源發佈之外，也會在選擇適當的後端集區時將要求 URL 的路徑模式納入考慮。</span><span class="sxs-lookup"><span data-stu-id="69682-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="69682-113">案例</span><span class="sxs-lookup"><span data-stu-id="69682-113">Scenario</span></span>

<span data-ttu-id="69682-114">下列案例會完成在現有應用程式閘道中建立路徑型規則的程序。</span><span class="sxs-lookup"><span data-stu-id="69682-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="69682-115">此案例假設您已經依照步驟 [建立應用程式閘道](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="69682-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![URL 路由][scenario]

## <span data-ttu-id="69682-117"><a name="createrule"></a>建立路徑型規則</span><span class="sxs-lookup"><span data-stu-id="69682-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="69682-118">路徑型規則需要自己的接聽程式，在建立此規則之前，請務必確認您有接聽程式可供使用。</span><span class="sxs-lookup"><span data-stu-id="69682-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="69682-119">步驟 1</span><span class="sxs-lookup"><span data-stu-id="69682-119">Step 1</span></span>

<span data-ttu-id="69682-120">瀏覽到 [Azure 入口網站](http://portal.azure.com)，然後選取現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="69682-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="69682-121">按一下 [規則] </span><span class="sxs-lookup"><span data-stu-id="69682-121">Click **Rules**</span></span>

![應用程式閘道概觀][1]

### <a name="step-2"></a><span data-ttu-id="69682-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="69682-123">Step 2</span></span>

<span data-ttu-id="69682-124">按一下 [路徑型]  按鈕來新增路徑型規則。</span><span class="sxs-lookup"><span data-stu-id="69682-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="69682-125">步驟 3</span><span class="sxs-lookup"><span data-stu-id="69682-125">Step 3</span></span>

<span data-ttu-id="69682-126">[新增路徑型規則]  刀鋒視窗有兩個區段。</span><span class="sxs-lookup"><span data-stu-id="69682-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="69682-127">您會在第一個區段中，定義接聽程式、規則的名稱和預設路徑設定。</span><span class="sxs-lookup"><span data-stu-id="69682-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="69682-128">預設路徑設定適用於未落在自訂路徑型路由之下的路由。</span><span class="sxs-lookup"><span data-stu-id="69682-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="69682-129">您會在 [新增路徑型規則]  刀鋒視窗的第二個區段中，定義路徑型規則本身。</span><span class="sxs-lookup"><span data-stu-id="69682-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="69682-130">**基本設定**</span><span class="sxs-lookup"><span data-stu-id="69682-130">**Basic Settings**</span></span>

* <span data-ttu-id="69682-131">**名稱** - 此值是可在入口網站中存取的易記規則名稱。</span><span class="sxs-lookup"><span data-stu-id="69682-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="69682-132">**接聽程式** - 此值是用於規則的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="69682-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="69682-133">**預設後端集區** - 此設定可定義要用於預設規則的後端</span><span class="sxs-lookup"><span data-stu-id="69682-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="69682-134">**預設 HTTP 設定** - 此設定可定義要用於預設規則的 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="69682-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="69682-135">**路徑型規則**</span><span class="sxs-lookup"><span data-stu-id="69682-135">**Path-based rules**</span></span>

* <span data-ttu-id="69682-136">**名稱** - 此值是路徑型規則的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="69682-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="69682-137">**路徑** - 此設定可定義規則在轉送流量時尋找的路徑</span><span class="sxs-lookup"><span data-stu-id="69682-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="69682-138">**後端集區** - 此設定可定義要用於規則的後端</span><span class="sxs-lookup"><span data-stu-id="69682-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="69682-139">**HTTP 設定** - 此設定可定義要用於規則的 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="69682-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69682-140">路徑︰要比對的路徑模式清單。</span><span class="sxs-lookup"><span data-stu-id="69682-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="69682-141">每個路徑都必須以 / 開頭，而且只有結尾允許使用 "\*"。</span><span class="sxs-lookup"><span data-stu-id="69682-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="69682-142">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="69682-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![已填入資訊的新增路徑型規則刀鋒視窗][2]

<span data-ttu-id="69682-144">將路徑型規則新增至現有應用程式閘道是在入口網站中進行的簡單程序。</span><span class="sxs-lookup"><span data-stu-id="69682-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="69682-145">建立路徑型規則後，即可加以編輯以便新增其他規則。</span><span class="sxs-lookup"><span data-stu-id="69682-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![新增其他路徑型規則][3]

<span data-ttu-id="69682-147">此步驟會設定路徑型路由。</span><span class="sxs-lookup"><span data-stu-id="69682-147">This step configures a path-based route.</span></span> <span data-ttu-id="69682-148">請務必了解系統不會重寫要求，應用程式閘道會在收到要求時檢查要求，並根據 URL 模式將要求傳送到適當的後端。</span><span class="sxs-lookup"><span data-stu-id="69682-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69682-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69682-149">Next steps</span></span>

<span data-ttu-id="69682-150">若要了解如何設定與「Azure 應用程式閘道」搭配運作的「SSL 卸載」，請參閱 [設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="69682-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
