---
title: "將路徑架構的 aaaCreate 規則-Azure 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate 應用程式閘道使用的路徑規則 hello 入口網站"
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="6824f-103">透過 hello 入口網站建立應用程式閘道的路徑規則</span><span class="sxs-lookup"><span data-stu-id="6824f-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6824f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6824f-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="6824f-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="6824f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="6824f-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6824f-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="6824f-107">路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="6824f-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="6824f-108">它會檢查是否為 hello 應用程式閘道中所列的 hello URL 設定路由 tooa 後端集區，並將傳送 hello 網路流量 toohello 定義後端集區。</span><span class="sxs-lookup"><span data-stu-id="6824f-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="6824f-109">URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="6824f-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="6824f-110">URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。</span><span class="sxs-lookup"><span data-stu-id="6824f-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="6824f-111">應用程式閘道具有兩種規則類型：基本和路徑型規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="6824f-112">hello 基本規則類型，並提供循環配置資源服務的 hello 後端集區的路徑為基礎的規則時此外 tooround 環散佈，也會考量 hello 要求 URL 的路徑模式並選擇 hello 適當的後端集區。</span><span class="sxs-lookup"><span data-stu-id="6824f-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="6824f-113">案例</span><span class="sxs-lookup"><span data-stu-id="6824f-113">Scenario</span></span>

<span data-ttu-id="6824f-114">hello 下列案例會經歷在現有的應用程式閘道中建立路徑為基礎的規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="6824f-115">hello 案例假設您已經有太遵循 hello 步驟[建立應用程式閘道](application-gateway-create-gateway-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6824f-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![URL 路由][scenario]

## <span data-ttu-id="6824f-117"><a name="createrule"></a>建立 hello 路徑型規則</span><span class="sxs-lookup"><span data-stu-id="6824f-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="6824f-118">路徑為基礎的規則建立 hello 規則確定您有可用的接聽程式 toouse 的 tooverify 之前需要它自己的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="6824f-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="6824f-119">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6824f-119">Step 1</span></span>

<span data-ttu-id="6824f-120">瀏覽 toohello [Azure 入口網站](http://portal.azure.com)選取現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="6824f-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="6824f-121">按一下 [規則] </span><span class="sxs-lookup"><span data-stu-id="6824f-121">Click **Rules**</span></span>

![應用程式閘道概觀][1]

### <a name="step-2"></a><span data-ttu-id="6824f-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6824f-123">Step 2</span></span>

<span data-ttu-id="6824f-124">按一下**路徑基礎**按鈕 tooadd 新路徑為基礎的規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="6824f-125">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6824f-125">Step 3</span></span>

<span data-ttu-id="6824f-126">hello**加入路徑為基礎的規則**分頁有兩個區段。</span><span class="sxs-lookup"><span data-stu-id="6824f-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="6824f-127">hello 第一個區段是定義 hello 接聽程式、 hello 名稱 hello 規則以及 hello 預設路徑設定位置。</span><span class="sxs-lookup"><span data-stu-id="6824f-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="6824f-128">hello 預設路徑設定為未落在 hello 自訂路徑型路由的路由。</span><span class="sxs-lookup"><span data-stu-id="6824f-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="6824f-129">hello 第二個區段的 hello**加入路徑為基礎的規則**刀鋒視窗是您在其中定義 hello 路徑為基礎的規則本身。</span><span class="sxs-lookup"><span data-stu-id="6824f-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="6824f-130">**基本設定**</span><span class="sxs-lookup"><span data-stu-id="6824f-130">**Basic Settings**</span></span>

* <span data-ttu-id="6824f-131">**名稱**-此值為 hello 入口網站中存取的易記名稱 toohello 規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="6824f-132">**接聽程式**-這個值是用於 hello 規則 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="6824f-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="6824f-133">**預設 後端集區**-此設定是定義 hello 用於 hello 預設規則的後端 toobe hello 設定</span><span class="sxs-lookup"><span data-stu-id="6824f-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="6824f-134">**預設的 HTTP 設定**-此設定是定義 hello hello 預設規則使用的 HTTP 設定 toobe hello 設定。</span><span class="sxs-lookup"><span data-stu-id="6824f-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="6824f-135">**路徑型規則**</span><span class="sxs-lookup"><span data-stu-id="6824f-135">**Path-based rules**</span></span>

* <span data-ttu-id="6824f-136">**名稱**-這個值是易記的名稱 toopath 型規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="6824f-137">**路徑**-此設定可定義 hello 路徑 hello 規則會搜尋時將流量轉送</span><span class="sxs-lookup"><span data-stu-id="6824f-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="6824f-138">**後端集區**-此設定是定義 hello 後端 toobe hello 規則使用的 hello 設定</span><span class="sxs-lookup"><span data-stu-id="6824f-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="6824f-139">**HTTP 設定**-此設定是定義 hello hello 規則使用的 HTTP 設定 toobe hello 設定。</span><span class="sxs-lookup"><span data-stu-id="6824f-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6824f-140">路徑模式 toomatch 路徑： hello 清單。</span><span class="sxs-lookup"><span data-stu-id="6824f-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="6824f-141">每個開頭必須是 / 和 hello 唯一地方"\*」 允許 hello 結尾會。</span><span class="sxs-lookup"><span data-stu-id="6824f-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="6824f-142">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="6824f-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![已填入資訊的新增路徑型規則刀鋒視窗][2]

<span data-ttu-id="6824f-144">新增路徑為基礎的規則 tooan 現有應用程式閘道會是簡單的程序，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6824f-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="6824f-145">建立路徑規則之後，它可以編輯的 tooadd 其他規則。</span><span class="sxs-lookup"><span data-stu-id="6824f-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![新增其他路徑型規則][3]

<span data-ttu-id="6824f-147">此步驟會設定路徑型路由。</span><span class="sxs-lookup"><span data-stu-id="6824f-147">This step configures a path-based route.</span></span> <span data-ttu-id="6824f-148">要求不會重寫的重要 toounderstand，因為要求來自於應用程式閘道會檢查 hello 要求和 basic hello url 模式傳送嗨要求 toohello 適當後端上。</span><span class="sxs-lookup"><span data-stu-id="6824f-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6824f-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6824f-149">Next steps</span></span>

<span data-ttu-id="6824f-150">如何 tooconfigure SSL 卸載，以及 Azure 應用程式閘道，請參閱的 toolearn[設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6824f-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
