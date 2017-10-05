---
title: "在 Azure 應用程式閘道中自訂 Web 應用程式防火牆規則 - Azure 入口網站 | Microsoft Docs"
description: "本文提供如何透過 Azure 入口網站，在應用程式閘道中自訂 Web 應用程式防火牆規則的相關資訊。"
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="b9a65-103">透過 Azure 入口網站自訂 Web 應用程式防火牆規則</span><span class="sxs-lookup"><span data-stu-id="b9a65-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9a65-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b9a65-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="b9a65-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a65-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="b9a65-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b9a65-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="b9a65-107">Azure 應用程式閘道 Web 應用程式防火牆 (WAF) 提供 Web 應用程式的保護。</span><span class="sxs-lookup"><span data-stu-id="b9a65-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="b9a65-108">這些保護是由開放 Web 應用程式安全性專案 (OWASP) 的核心規則集 (CRS) 所提供。</span><span class="sxs-lookup"><span data-stu-id="b9a65-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="b9a65-109">某些規則可能會導致誤判，並封鎖真正的流量。</span><span class="sxs-lookup"><span data-stu-id="b9a65-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="b9a65-110">因此，應用程式閘道會提供功能以自訂規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="b9a65-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="b9a65-111">如需特定規則群組與規則的詳細資訊，請參閱 [Web 應用程式防火牆 CRS 規則群組與規則的清單](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="b9a65-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="b9a65-112">如果您的應用程式閘道並未使用 WAF 層，右窗格中會出現將應用程式閘道升級至 WAF 層的選項。</span><span class="sxs-lookup"><span data-stu-id="b9a65-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![啟用 WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="b9a65-114">檢視規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="b9a65-114">View rule groups and rules</span></span>

<span data-ttu-id="b9a65-115">**檢視規則群組與規則**</span><span class="sxs-lookup"><span data-stu-id="b9a65-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="b9a65-116">瀏覽至應用程式閘道，然後選取 [Web 應用程式防火牆]。</span><span class="sxs-lookup"><span data-stu-id="b9a65-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="b9a65-117">選取 [進階規則設定]。</span><span class="sxs-lookup"><span data-stu-id="b9a65-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="b9a65-118">這個檢視會在透過所選擇規則集提供之所有規則群組的頁面上顯示一個表格，</span><span class="sxs-lookup"><span data-stu-id="b9a65-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="b9a65-119">並選取所有的規則核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b9a65-119">All of the rule's check boxes are selected.</span></span>

![設定已停用的規則][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="b9a65-121">搜尋要停用的規則</span><span class="sxs-lookup"><span data-stu-id="b9a65-121">Search for rules to disable</span></span>

<span data-ttu-id="b9a65-122">[Web 應用程式防火牆設定] 刀鋒視窗提供透過文字搜尋篩選規則的功能。</span><span class="sxs-lookup"><span data-stu-id="b9a65-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="b9a65-123">結果只會顯示包含您搜尋之文字的規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="b9a65-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![搜尋規則][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="b9a65-125">停用規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="b9a65-125">Disable rule groups and rules</span></span>

<span data-ttu-id="b9a65-126">當您停用規則時，可以停用整個規則群組，或停用一或多個規則群組下的特定規則。</span><span class="sxs-lookup"><span data-stu-id="b9a65-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="b9a65-127">**停用規則群組或特定規則**</span><span class="sxs-lookup"><span data-stu-id="b9a65-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="b9a65-128">搜尋您要停用的規則或規則群組。</span><span class="sxs-lookup"><span data-stu-id="b9a65-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="b9a65-129">清除您要停用之規則的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b9a65-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="b9a65-130">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="b9a65-130">Select **Save**.</span></span> 

![儲存變更][3]

## <a name="next-steps"></a><span data-ttu-id="b9a65-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9a65-132">Next steps</span></span>

<span data-ttu-id="b9a65-133">設定已停用的規則之後，您可以了解如何檢視 WAF 記錄。</span><span class="sxs-lookup"><span data-stu-id="b9a65-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="b9a65-134">如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。</span><span class="sxs-lookup"><span data-stu-id="b9a65-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
