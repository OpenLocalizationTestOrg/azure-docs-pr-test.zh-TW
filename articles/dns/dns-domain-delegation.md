---
title: "aaaAzure DNS 委派概觀 |Microsoft 文件"
description: "了解如何 toochange 網域委派和使用 Azure DNS 名稱伺服器 tooprovide 網域裝載。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: eaf2d2e345004b4d631e8d81d548b8ca23277d05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegation-of-dns-zones-with-azure-dns"></a>使用 Azure DNS 的 DNS 區域委派

Azure DNS 可讓您 toohost DNS 區域，並管理網域，以在 Azure 中的 hello DNS 記錄。 為了讓網域 tooreach Azure DNS 的 DNS 查詢，hello 網域有 toobe 從 hello 父系網域委派 tooAzure DNS。 請記住 Azure DNS 不 hello 網域註冊機構。 本文件說明網域委派的運作方式以及 toodelegate 網域 tooAzure DNS。

## <a name="how-dns-delegation-works"></a>DNS 委派的運作方式

### <a name="domains-and-zones"></a>網域和區域

hello 網域名稱系統是網域的階層。 hello 階層是從 hello 'root' 網域，其名稱只是開始 '**。**'。  下面接著最上層網域，例如 'com'、'net'、'org'、'uk' 或 'jp'。  最上層網域下面是第二層網域，例如 'org.uk' 或 'co.jp'。  依此類推。 hello DNS 階層中的 hello 網域裝載使用不同的 DNS 區域。 全域發佈這些區域，hello 世界各地的 DNS 名稱伺服器所裝載。

**DNS 區域**-網域是在網域名稱系統，例如 'contoso.com' hello 的唯一名稱。 DNS 區域是使用的 toohost hello 針對特定網域的 DNS 記錄。 例如，hello 網域 'contoso.com' 可能會包含數個 DNS 記錄，例如 （郵件伺服器） 的 ' mail.contoso.com' 和 'www.contoso.com' （適用於網站）。

**網域註冊機構** - 網域註冊機構是指可以提供網際網路網域名稱的公司。 如果您想要的 hello 的網際網路網域 toouse 而且 toopurchase 可讓您確認它。 Hello 網域名稱註冊後，會是合法 hello hello 網域名稱擁有者。 如果您已經有網際網路網域，您將使用 hello 目前網域註冊機構 toodelegate tooAzure DNS。

誰擁有指定的網域名稱，或如需詳細資訊的詳細資訊的 toofind toobuy 網域，請參閱[Azure AD 中的網際網路網域管理](https://msdn.microsoft.com/library/azure/hh969248.aspx)。

### <a name="resolution-and-delegation"></a>解析和委派

有兩種類型的 DNS 伺服器：

* *授權* DNS 伺服器裝載 DNS 區域。 它只會回答這些區域中的 DNS 記錄查詢。
* *遞迴* DNS 伺服器不裝載 DNS 區域。 它會藉由呼叫授權 DNS 伺服器 toogather hello 資料需要回答所有 DNS 查詢。

Azure DNS 提供具權威性的 DNS 服務。  它不提供遞迴 DNS 服務。 雲端服務和 Azure 中的 Vm 會自動設定的 toouse 個別提供做為 Azure 基礎結構一部分的遞迴 DNS 服務。 如需有關如何 toochange 這些 DNS 設定，請參閱詳細[在 Azure 中的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。

DNS 用戶端電腦或行動裝置通常呼叫遞迴 DNS 伺服器 tooperform hello 用戶端應用程式需要任何 DNS 查詢。

當遞迴 DNS 伺服器收到的查詢，例如 'www.contoso.com' DNS 記錄時，就必須 toofind hello 名稱伺服器主控 hello 區域 hello 'contoso.com' 網域。 toofind hello 名稱伺服器，它會從 hello 根名稱伺服器，然後從那裡找到 hello 裝載 hello 'com' 區域的名稱伺服器。 然後，它會查詢 hello 'com' 名稱伺服器 toofind hello 名稱伺服器裝載 hello 'contoso.com' 區域。  最後，它是無法 tooquery 這些名稱伺服器 'www.contoso.com'。

此程序稱為 hello DNS 名稱解析。 嚴格來說，DNS 解析包含額外的步驟，例如下列 Cname，但這不是重要 toounderstanding DNS 委派的運作方式。

如何沒有上層區域 '點' toohello 子區域的名稱伺服器？ 作法是使用一種特殊的 DNS 記錄，稱為 NS 記錄 (NS 代表「名稱伺服器」)。 例如，hello 根區域包含 'com' NS 記錄，並顯示 hello hello 'com' 區域的名稱伺服器。 接著，hello 'com' 區域包含 'contoso.com'，其中顯示 hello hello 'contoso.com' 區域的名稱伺服器 NS 記錄。 設定子區域的上層區域中的 hello NS 記錄，會呼叫委派 hello 網域。

hello 下列影像顯示的範例 DNS 查詢。 hello contoso.net 和 partners.contoso.net 是 Azure DNS 區域。

![Dns-nameserver](./media/dns-domain-delegation/image1.png)

1. hello 用戶端要求`www.partners.contoso.net`從其本機 DNS 伺服器。
1. hello 本機 DNS 伺服器沒有 hello 記錄，因此它會建立要求 tootheir 根名稱伺服器。
1. hello 根名稱伺服器沒有 hello 記錄，但知道 hello hello 位址`.net`名稱伺服器，它會提供該位址 toohello DNS 伺服器
1. hello DNS 傳送嗨要求 toohello`.net`名稱伺服器，它並沒有 hello 記錄但不會知道 hello hello contoso.net 名稱伺服器位址。 在此情況下，這是在 Azure DNS 中託管的 DNS 區域。
1. hello 區域`contoso.net`沒有 hello 記錄，但知道 hello 名稱伺服器`partners.contoso.net`並與回應。 在此情況下，這是在 Azure DNS 中託管的 DNS 區域。
1. hello DNS 伺服器要求 hello IP 位址`partners.contoso.net`從 hello`partners.contoso.net`區域。 它包含 hello A 記錄，然後會回應 hello IP 位址。
1. hello DNS 伺服器提供 IP 位址 toohello 用戶端 hello
1. hello 用戶端連線 toohello 網站`www.partners.contoso.net`。

每個委派實際上有兩個複本的 hello NS 記錄。其中一個指向 toohello 子網域與另一個本身 hello 子區域中的 hello 上層區域中。 hello 'contoso.net' 含有 'contoso.net' hello NS 記錄 （在 'net' 中的加法 toohello NS 記錄）。 這些記錄稱為權威 NS 記錄和它們的位置可以在 hello 區域的 hello 子區域的 apex。

## <a name="next-steps"></a>後續步驟

了解如何太[委派您網域 tooAzure DNS](dns-delegate-domain-azure-dns.md)

