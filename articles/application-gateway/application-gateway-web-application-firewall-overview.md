---
title: "aaaIntroduction tooweb 應用程式防火牆 Azure 應用程式閘道 (WAF) |Microsoft 文件"
description: "本頁面提供適用於應用程式閘道的 Web 應用程式防火牆 (WAF) 的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Web 應用程式防火牆 (WAF)

Web 應用程式防火牆 (WAF) 是一項應用程式閘道功能，可提供 Web 應用程式的集中式保護，免於遭遇常見的攻擊和弱點。 

Web 應用程式防火牆會根據規則從 hello [OWASP 核心規則集](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)3.0 或 2.2.9。 Web 應用程式已逐漸成為利用常見已知弱點的惡意攻擊目標。 通用的這些攻擊 SQL 插入式攻擊，跨網站指令碼處理攻擊 tooname 幾個。 防止這類攻擊中應用程式程式碼極具挑戰，可能需要嚴格的維護、 修補和監視 hello 應用程式拓撲的多個層級。 集中式的 web 應用程式防火牆有助於讓安全性管理簡單許多，並提供更好的保證 tooapplication 系統管理員針對威脅或入侵。 WAF 方案也可以回應 tooa 更快的安全性威脅的修補與保護每個個別的 web 應用程式的中央位置的已知的弱點。 現有的應用程式閘道可以輕鬆地是轉換的 tooa web 應用程式啟用防火牆應用程式閘道。

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

應用程式閘道會作為應用程式傳遞控制站和優惠 SSL 終止、 cookie 架構工作階段親和性、 循環配置資源負載分佈，內容為基礎的路由、 能力 toohost 運作多個網站和安全性增強功能。 應用程式閘道所提供的安全性增強功能包括 SSL 原則管理，結束 tooend SSL 支援。 應用程式的安全性是現在再加上由 WAF （web 應用程式防火牆） 已直接整合到 hello ADC 供應項目。 這可提供簡單 tooconfigure 中央位置 toomanage 並保護您的 web 應用程式對一般 web 弱點。

## <a name="benefits"></a>優點

hello 下面是應用程式閘道和 web 應用程式防火牆提供 hello 核心優勢：

### <a name="protection"></a>保護

* 保護您的 web 應用程式 web 的弱點可能會與沒有修改 toobackend 程式碼的攻擊。

* 保護多個 web 應用程式閘道後方相同時間 hello 應用程式。 應用程式閘道支援無法所有受保護以免 web 攻擊，而且 WAF，單一閘道後方 too20 網站上裝載。

### <a name="monitoring"></a>監視

* 使用即時 WAF 記錄來監視 Web 應用程式對抗攻擊。 此記錄檔與整合[Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)tootrack WAF 警示和記錄檔，並輕鬆地監視趨勢。

* WAF 即將與 Azure 資訊安全中心整合。 Azure 資訊安全中心可讓中央檢視的所有 Azure 資源的 hello 安全性狀態。

### <a name="customization"></a>自訂

* hello 能力 toocustomize WAF 規則和規則分組 toosuit 應用程式的需求，並消除誤判。

## <a name="features"></a>特性

Web 應用程式防火牆會預先 CRS 3.0 預設設定，或者您可以選擇 toouse 2.2.9。 CRS 3.0 的誤判情形低於 2.2.9。 太 hello 能力[自訂您的需求規則 toosuit](application-gateway-customize-waf-rules-portal.md)提供。 Hello 的 web 應用程式防火牆防止常見 web 弱點部分包括：

* SQL 插入式攻擊保護
* 跨網站指令碼保護
* 常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊
* 防範 HTTP 通訊協定違規
* 防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭
* 防範 Bot、編目程式和掃描器
* 偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)

如需更詳細的規則清單和其保護，請參閱 hello 下列[核心規則集](#core-rule-sets)。

### <a name="core-rule-sets"></a>核心規則集

應用程式閘道支援兩個規則集：CRS 3.0 和 CRS 2.2.9。 這些核心規則集是可保護 Web 應用程式免於遭遇惡意活動的規則集合。

#### <a name="owasp30"></a>OWASP_3.0

提供 hello 3.0 核心規則集有 13 規則群組中 hello 下表所示。 每個規則群組包含多個規則 (可加以停用)。

|RuleGroup|說明|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|包含規則 tooprotect 針對已知垃圾郵件傳送者或惡意活動。|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|包含規則 toolock 向下方法 (PUT、 PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| 包含規則 tooprotect 阻絕服務 (DoS) 攻擊。|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| 包含規則 tooprotect 針對連接埠和環境的掃描器。|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|包含規則 tooprotect 針對通訊協定與編碼的問題。|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|包含規則 tooprotect 針對標頭資料隱碼、 smuggling，要求和回應分割|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|包含規則 tooprotect 攻擊，檔案和路徑。|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|包含規則 tooprotect 針對遠端檔案包含 (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|包含規則 tooprotect 再次遠端執行程式碼。|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|包含規則 tooprotect PHP 資料隱碼攻擊。|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|包含規則，可防範跨網站指令碼。|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|包含規則，可防禦 SQL 插入式攻擊。|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|包含規則 tooprotect 針對工作階段 Fixation 攻擊。|

#### <a name="owasp229"></a>OWASP_2.2.9

提供 hello 2.2.9 核心規則集有 10 個規則群組中 hello 下表所示。 每個規則群組包含多個規則 (可加以停用)。

|RuleGroup|說明|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|包含規則 tooprotect 針對通訊協定違規 （無效的字元，取得與要求本文等。）|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|包含規則 tooprotect 針對不正確的標頭資訊。|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|包含規則 tooprotect 針對引數或超過限制的檔案。|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|包含規則 tooprotect 針對受限制的方法、 標頭，以及檔案類型。 |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|包含規則 tooprotect 針對網頁自動尋檢和掃描器。|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|包含規則 tooprotect 攻擊泛型 （工作階段 fixation、 遠端檔案包含、 PHP 資料隱碼等等）|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|包含規則 tooprotect SQL 資料隱碼攻擊|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|包含針對跨網站指令碼的規則 tooprotect。|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|包含規則 tooprotect 路徑周遊攻擊|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|包含規則 tooprotect 針對後門特洛伊程式。|

### <a name="waf-modes"></a>WAF 模式

應用程式閘道 WAF 可以設定的 toorun hello 下列兩種模式中：

* **偵測模式**– 在偵測模式中，應用程式閘道 WAF 設定的 toorun 監視，和 tooa 記錄檔中記錄所有潛在威脅的警示時。 應用程式閘道的記錄診斷應該開啟使用 hello**診斷**> 一節。 您也需要 hello WAF 的 tooensure 選取並開啟記錄檔。 在偵測模式執行的 Web 應用程式防火牆不會封鎖連入要求。
* **防止模式**– 當在防止模式中，應用程式閘道設定的 toorun 主動封鎖入侵和其規則所偵測到的攻擊。 hello 攻擊者會收到 403 的未經授權的存取例外狀況，並終止 hello 連線。 防止模式會繼續 toolog 這類攻擊 hello WAF 記錄檔中。

### <a name="application-gateway-waf-reports"></a>WAF 監視

監視的應用程式閘道的 hello 健全狀況很重要的。 監視 web 應用程式的應用程式防火牆與 hello 它所保護的 hello 健全狀況是透過記錄和監視 Azure、 Azure 資訊安全中心 （即將推出），且記錄分析的整合來提供。

![診斷](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure 監視器

每個應用程式閘道記錄都會與 [Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)整合。  這可讓您 tootrack 包括 WAF 警示和記錄檔的診斷資訊。  這項功能提供 hello 下 hello hello 入口網站中的應用程式閘道資源內**診斷**索引標籤上，或直接透過 hello Azure 監視服務。 有關啟用應用程式閘道的診斷記錄檔，請瀏覽的 toolearn[應用程式閘道診斷](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure 資訊安全中心

[Azure 資訊安全中心](../security-center/security-center-intro.md)幫助您防止、 偵測，並以進一步掌握回應 toothreats 及控制 hello 您的 Azure 資源的安全性。 應用程式閘道現在會[整合到 Azure 資訊安全中心](application-gateway-integration-security-center.md)。 Azure 資訊安全中心會掃描您環境 toodetect 受保護的 web 應用程式。 它現在可以建議應用程式閘道 WAF tooprotect 這些易受攻擊的資源。 您可以從直接建立應用程式閘道 WAF hello Azure 資訊安全中心。  這些 WAF 執行個體與 Azure 資訊安全中心整合，而會傳送警示和健全狀況資訊回 tooAzure 資訊安全中心進行報告。

![圖 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>記錄

應用程式閘道 WAF 提供其偵測到之每個威脅的詳細報告。 記錄會與 Azure 診斷記錄整合，而且警示會以 JSON 格式來記錄。 這些記錄可以與 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) 整合。

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>應用程式閘道 WAF SKU 價格

只有在新的 WAF SKU 之下才能使用 Web 應用程式防火牆。 只在 Azure 資源管理員佈建模型和 hello 傳統部署模式下不使用這個 SKU。 此外 WAF SKU 僅以中型和大型應用程式閘道執行個體大小提供。 所有應用程式閘道的 hello 限制也適用於 toohello WAF SKU。 價格是以每小時的閘道器執行個體費用和資料處理費用為基礎。 WAF SKU 的每小時閘道價格不同於標準 SKU 費用，您可在[應用程式閘道價格詳細資料](https://azure.microsoft.com/pricing/details/application-gateway/)找到。 資料處理費用保持 hello 相同。 不會依照每個規則或規則群組計算費用。 您可以保護多個 web 應用程式背後 hello 相同 web 應用程式防火牆並沒有任何額外的費用，以支援多個應用程式。 

如 WAF 會開始計費有效 5/5/2017，直到然後 hello WAF SKU 閘道會繼續 toobe 標準費率計費。

## <a name="next-steps"></a>後續步驟

之後學習 WAF hello 功能有關的詳細資訊，請瀏覽[tooconfigure web 應用程式閘道上的應用程式防火牆](application-gateway-web-application-firewall-portal.md)。

