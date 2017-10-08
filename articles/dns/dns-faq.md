---
title: "aaaAzure DNS 常見問題集 |Microsoft 文件"
description: "關於 Azure DNS 的常見問題集"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Azure DNS 常見問題集

## <a name="about-azure-dns"></a>關於 Azure DNS

### <a name="what-is-azure-dns"></a>什麼是 Azure DNS？

hello 網域名稱系統或 DNS，負責將轉譯 （或解決） 的網站或服務名稱 tooits IP 位址。 Azure DNS 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。 裝載您在 Azure 中的網域，您可以管理您的 DNS 記錄使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。

Azure DNS 中的 DNS 網域裝載於 Azure 的 DNS 名稱伺服器全球網路。 我們使用任一傳播網路，讓每個 DNS 查詢由 hello 最接近可用 DNS 伺服器回應。 這為您的網域提供快速的效能與高可用性。

hello Azure DNS 服務會採用 Azure 資源管理員。 因此可得益於 Resource Manager 的功能，如角色型存取控制、稽核記錄檔、資源鎖定。 您的網域和記錄可以透過 hello Azure 入口網站，Azure PowerShell cmdlet，管理和 hello 跨平台 Azure CLI。 需要 DNS 的自動管理的應用程式可以整合透過 hello hello 服務 REST API 和 Sdk。

### <a name="how-much-does-azure-dns-cost"></a>Azure DNS 的費用是多少？

hello Azure DNS 計費模型根據 Azure DNS 和 DNS 查詢他們收到的 hello 數量裝載的 DNS 區域的 hello 數目。 根據使用量會提供折扣。

如需詳細資訊，請參閱 hello [Azure DNS 定價頁面](https://azure.microsoft.com/pricing/details/dns/)。

### <a name="what-is-hello-sla-for-azure-dns"></a>Azure DNS 的 hello SLA 是什麼？

我們保證，有效的 DNS 要求會從接收回應至少一個 Azure DNS 名稱伺服器至少 99.99%的 hello 時間。

如需詳細資訊，請參閱 hello [Azure DNS SLA 頁面](https://azure.microsoft.com/support/legal/sla/dns)。

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>什麼是「DNS 區域」？ 是它做為 DNS 網域 hello 相同？ 

網域在 hello 網域名稱系統中，例如 'contoso.com' 是唯一的名稱。

DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。 例如，hello 網域 'contoso.com' 可能包含數個 DNS 記錄，例如 'mail.contoso.com' （適用於郵件伺服器） 和 'www.contoso.com' （適用於該網站）。 這些會裝載於 hello DNS 區域 'contoso.com'。

網域名稱是*只有名稱*，而 DNS 區域是包含網域名稱的 hello DNS 記錄的資料資源。 Azure DNS 可讓您 toohost DNS 區域，並管理網域，以在 Azure 中的 hello DNS 記錄。 它也提供 DNS 名稱伺服器 tooanswer hello 網際網路 DNS 查詢。

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>是否需要 DNS 網域名稱 toouse Azure DNS toopurchase？ 

不一定。

您不需要 toopurchase 網域 toohost Azure DNS 中的 DNS 區域。 您可以隨時建立 DNS 區域，但不擁有 hello 網域名稱。 此區域的 DNS 查詢只會解決是否它們會被導向 toohello Azure DNS 名稱伺服器指派 toohello 區域。

如果您想 toolink DNS 區域寫入 hello 通用 DNS 的階層 – 這個控制項可讓 DNS 查詢從任何地方 hello world toofind 中 DNS 區域，並回答您的 DNS 記錄，就會需要 toopurchase hello 網域名稱。

## <a name="azure-dns-features"></a>Azure DNS 功能

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Azure DNS 是否支援 DNS 型流量路由或端點容錯移轉？

DNS 型流量路由和端點容錯移轉是由「Azure 流量管理員」所提供。 這是一項可以與 Azure DNS 一起使用的個別 Azure 服務。 如需詳細資訊，請參閱 hello [Traffic Manager 概述](../traffic-manager/traffic-manager-overview.md)。

Azure DNS 僅支援裝載 'static' 的 DNS 網域，每個指定的 DNS 記錄的 DNS 查詢永遠接收 hello 相同的 DNS 回應。

### <a name="does-azure-dns-support-domain-name-registration"></a>Azure DNS 是否支援網域名稱註冊？

否。 Azure DNS 目前不支援購買網域名稱。 如果您想 toopurchase 網域時，您會需要 toouse 第三方網域名稱註冊機構。 hello 註冊機構通常費用小年費。 hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。 請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。

這是我們的待處理項目上所追蹤的一項功能。 您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar)。

### <a name="does-azure-dns-support-private-domains"></a>Azure DNS 是否支援「私人」網域？

否。 Azure DNS 目前只支援網際網路對向網域。

這是我們的待處理項目上所追蹤的一項功能。 您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int)。

如需有關 Azure 中內部 DNS 選項的資訊，請參閱 [VM 與角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

### <a name="does-azure-dns-support-dnssec"></a>Azure DNS 是否支援 DNSSEC？

否。 Azure DNS 目前不支援 DNSSEC。

這是我們的待處理項目上所追蹤的一項功能。 您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support)。

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Azure DNS 是否支援區域傳輸 (AXFR/IXFR)？

否。 Azure DNS 目前不支援區域傳輸。 DNS 區域可以是[匯入至 Azure DNS 使用 hello Azure CLI](dns-import-export.md)。 DNS 記錄管理透過 hello [Azure DNS 管理入口網站](dns-operations-recordsets-portal.md)，我們[REST API](https://docs.microsoft.com/powershell/module/azurerm.dns)， [SDK](dns-sdk.md)， [PowerShell cmdlet](dns-operations-recordsets.md)，或[CLI 工具](dns-operations-recordsets-cli.md)。

這是我們的待處理項目上所追蹤的一項功能。 您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c)。

### <a name="does-azure-dns-support-url-redirects"></a>Azure DNS 是否支援 URL 重新導向？

否。 URL 重新導向服務不是實際的 DNS 服務-hello HTTP 層級，而非 hello DNS 層級運作。 某些 DNS 提供者 toobundle URL 重新導向服務做為其整體的供應項目的一部分。 Azure DNS 目前不支援此做法。

這項功能列入我們的待處理項目追蹤。 您也可以使用我們的意見反應網站[註冊您的支援這項功能以](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape)。

## <a name="using-azure-dns"></a>使用 Azure DNS

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>我是否可以使用 Azure DNS 和另一個 DNS 提供者來共同裝載某個網域？

是。 Azure DNS 支援與其他 DNS 服務共同裝載網域。

toodo 因此，您需要 toomodify hello NS 記錄 （哪一個控制項的提供者會收到 DNS 查詢以取得 hello 網域） 的 hello 網域 toopoint toohello 名稱伺服器的兩個提供者。 這些 NS 記錄需要修改 3 身處 toobe: Azure DNS 中的 在 hello 其他提供者，在 hello 上層區域 （透過 hello 網域名稱註冊機構通常會設定）。 如需有關 DNS 委派的詳細資訊，請參閱 [DNS 網域委派](dns-domain-delegation.md)。

此外，您需要 tooensure hello hello 網域的 DNS 記錄是這兩個 DNS 提供者之間的同步處理。 Azure DNS 目前不支援 DNS 區域傳輸。 您必須使用其中一個 hello toosynchronize DNS 記錄[Azure DNS 管理入口網站](dns-operations-recordsets-portal.md)，我們[REST API](https://docs.microsoft.com/powershell/module/azurerm.dns)， [SDK](dns-sdk.md)， [PowerShell cmdlet](dns-operations-recordsets.md)或[CLI 工具](dns-operations-recordsets-cli.md)。

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>我是否必須 toodelegate 我網域 tooall 4 Azure DNS 名稱伺服器？

是。 Azure DNS 指派 4 名稱伺服器 tooeach DNS 區域，錯誤隔離和增加的恢復功能。 如 tooqualify hello Azure DNS SLA，您需要 toodelegate 您網域 tooall 4 的名稱伺服器。

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>什麼是 Azure DNS 的 hello 使用量限制？

使用 Azure DNS 時，適用下列預設限制 hello:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>我是否可以在資源群組之間或訂用帳戶之間移動 Azure DNS 區域？

是。 您可以在資源群組之間或訂用帳戶之間移動 DNS 區域。

移動 DNS 區域時，對 DNS 查詢並沒有影響。 hello 分派 toohello 區域的名稱伺服器保持的 hello 與 DNS 查詢處理為整個標準。

如需詳細資訊和指示 toomove DNS 區域，請參閱[移動資源 tooa 新資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)。

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>多久需要 DNS 變更 tootake 效果？

新的 DNS 區域與 DNS 記錄會通常被反映在 hello Azure DNS 名稱伺服器快速，在幾秒鐘內。

變更 tooexisting DNS 記錄可能需要較長的時間，但應該仍會反映在 hello Azure DNS 名稱伺服器上 60 秒內。 在此情況下，DNS 快取之外 Azure DNS （藉由 DNS 用戶端和 DNS 遞迴解析程式） 可能也會影響 hello 的時間 DNS 變更 toobe 有效。 可以使用的每個資料錄集的 hello 存留時間 (TTL) 屬性來控制此快取持續時間。

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>我要如何保護我的 DNS 區域免於遭到意外刪除？

使用 Azure 資源管理員，來管理 azure DNS 及 hello 的存取控制功能的 Azure 資源管理員提供。 以角色為基礎的存取控制可以使用的 toocontrol 哪些使用者可以讀取或寫入存取 tooDNS 區域和資料錄集。 資源鎖定可以被套用的 tooprevent 意外修改或刪除 DNS 區域和資料錄集。

如需詳細資訊，請參閱[保護 DNS 區域和記錄](dns-protect-zones-recordsets.md)。

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>我要如何設定 Azure DNS 中的 SPF 記錄？

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>我要如何設定 Azure DNS 中的「國際網域名稱」(IDN)？

「國際網域名稱」(IDN) 的運作方式是使用 '[Punycode](https://en.wikipedia.org/wiki/Punycode)' 將每個 DNS 名稱編碼。 建立 DNS 查詢時，會使用這些以 Punycode 編碼的名稱來建立。

您可以在 Azure DNS 中設定國際網域名稱 (Idn) 的第一個轉換 hello 區域名稱或設定名稱 toopunycode 記錄。 Azure DNS 目前不支援以 Punycode 作為轉換目標或來源的內建轉換。

## <a name="next-steps"></a>後續步驟

[深入了解 Azure DNS](dns-overview.md)
<br>
[深入了解 DNS 區域和記錄](dns-zones-records.md)
<br>
[開始使用 Azure DNS](dns-getstarted-portal.md)

