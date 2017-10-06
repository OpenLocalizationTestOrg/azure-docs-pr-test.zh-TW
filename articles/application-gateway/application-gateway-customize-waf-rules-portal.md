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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>自訂 hello Azure 入口網站透過 web 應用程式防火牆規則

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。 這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。 某些規則可能會導致誤判，並封鎖真正的流量。 基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。 如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。

>[!NOTE]
> 如果您的應用程式閘道器未使用 hello WAF 層，hello 選項 tooupgrade hello 應用程式閘道 toohello WAF 層會顯示 hello 右窗格中。 

![啟用 WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>檢視規則群組與規則

**tooview 規則群組與規則**
   1. 瀏覽 toohello 應用程式閘道，然後再選取**Web 應用程式防火牆**。  
   2. 選取 [進階規則設定]。  
   此檢視會顯示 hello hello 選擇規則集所提供的所有 hello 規則群組 頁面上的資料表。 選取所有 hello 規則的核取方塊。

![設定已停用的規則][1]

## <a name="search-for-rules-toodisable"></a>規則 toodisable 搜尋

hello **Web 應用程式的防火牆設定**刀鋒視窗中提供的功能，hello 文字搜尋透過 toofilter hello 規則。 hello 結果顯示只有 hello 規則群組，以及包含您在其中搜尋的 hello 文字的規則。

![搜尋規則][2]

## <a name="disable-rule-groups-and-rules"></a>停用規則群組與規則

當您停用規則時，可以停用整個規則群組，或停用一或多個規則群組下的特定規則。 

**toodisable 規則群組或特定的規則**

   1. 搜尋 hello 規則或規則群組，您會想 toodisable。
   2. 您想 toodisable 的 hello 規則，請清除 hello 核取方塊。 
   2. 選取 [ **儲存**]。 

![儲存變更][3]

## <a name="next-steps"></a>後續步驟

您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。 如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
