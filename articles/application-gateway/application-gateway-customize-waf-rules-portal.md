---
title: "aaaCustomize web 應用程式在 Azure 應用程式閘道 Azure 入口網站中的防火牆規則 |Microsoft 文件"
description: "這篇文章提供如何 toocustomize web 應用程式防火牆規則時，在應用程式閘道 hello Azure 入口網站的資訊。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="69edc-103">自訂 hello Azure 入口網站透過 web 應用程式防火牆規則</span><span class="sxs-lookup"><span data-stu-id="69edc-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69edc-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="69edc-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="69edc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69edc-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="69edc-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69edc-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="69edc-107">hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="69edc-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="69edc-108">這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。</span><span class="sxs-lookup"><span data-stu-id="69edc-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="69edc-109">某些規則可能會導致誤判，並封鎖真正的流量。</span><span class="sxs-lookup"><span data-stu-id="69edc-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="69edc-110">基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="69edc-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="69edc-111">如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="69edc-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="69edc-112">如果您的應用程式閘道器未使用 hello WAF 層，hello 選項 tooupgrade hello 應用程式閘道 toohello WAF 層會顯示 hello 右窗格中。</span><span class="sxs-lookup"><span data-stu-id="69edc-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![啟用 WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="69edc-114">檢視規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="69edc-114">View rule groups and rules</span></span>

<span data-ttu-id="69edc-115">**tooview 規則群組與規則**</span><span class="sxs-lookup"><span data-stu-id="69edc-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="69edc-116">瀏覽 toohello 應用程式閘道，然後再選取**Web 應用程式防火牆**。</span><span class="sxs-lookup"><span data-stu-id="69edc-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="69edc-117">選取 [進階規則設定]。</span><span class="sxs-lookup"><span data-stu-id="69edc-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="69edc-118">此檢視會顯示 hello hello 選擇規則集所提供的所有 hello 規則群組 頁面上的資料表。</span><span class="sxs-lookup"><span data-stu-id="69edc-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="69edc-119">選取所有 hello 規則的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="69edc-119">All of hello rule's check boxes are selected.</span></span>

![設定已停用的規則][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="69edc-121">規則 toodisable 搜尋</span><span class="sxs-lookup"><span data-stu-id="69edc-121">Search for rules toodisable</span></span>

<span data-ttu-id="69edc-122">hello **Web 應用程式的防火牆設定**刀鋒視窗中提供的功能，hello 文字搜尋透過 toofilter hello 規則。</span><span class="sxs-lookup"><span data-stu-id="69edc-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="69edc-123">hello 結果顯示只有 hello 規則群組，以及包含您在其中搜尋的 hello 文字的規則。</span><span class="sxs-lookup"><span data-stu-id="69edc-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![搜尋規則][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="69edc-125">停用規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="69edc-125">Disable rule groups and rules</span></span>

<span data-ttu-id="69edc-126">當您停用規則時，可以停用整個規則群組，或停用一或多個規則群組下的特定規則。</span><span class="sxs-lookup"><span data-stu-id="69edc-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="69edc-127">**toodisable 規則群組或特定的規則**</span><span class="sxs-lookup"><span data-stu-id="69edc-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="69edc-128">搜尋 hello 規則或規則群組，您會想 toodisable。</span><span class="sxs-lookup"><span data-stu-id="69edc-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="69edc-129">您想 toodisable 的 hello 規則，請清除 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="69edc-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="69edc-130">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="69edc-130">Select **Save**.</span></span> 

![儲存變更][3]

## <a name="next-steps"></a><span data-ttu-id="69edc-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69edc-132">Next steps</span></span>

<span data-ttu-id="69edc-133">您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。</span><span class="sxs-lookup"><span data-stu-id="69edc-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="69edc-134">如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。</span><span class="sxs-lookup"><span data-stu-id="69edc-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
