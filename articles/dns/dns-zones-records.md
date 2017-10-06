---
title: "aaaDNS 區域，以及記錄概觀-Azure DNS |Microsoft 文件"
description: "將 DNS 區域和記錄，裝載於 Microsoft Azure DNS 中的支援概觀。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>DNS 區域和記錄的概觀

此頁面說明 hello 的網域、 DNS 區域和 DNS 記錄和資料錄集，及它們如何支援 Azure DNS 中的重要概念。

## <a name="domain-names"></a>網域名稱

hello 網域名稱系統是網域的階層。 hello 階層是從 hello 'root' 網域，其名稱只是開始 '**。**'。  下面接著最上層網域，例如 'com'、'net'、'org'、'uk' 或 'jp'。  再往下是第二層網域，例如 'org.uk' 或 'co.jp'。 全域發佈 hello DNS 階層中的 hello 網域，hello 世界各地的 DNS 名稱伺服器所裝載。

網域名稱註冊機構是 toopurchase 網域名稱，例如 'contoso.com' 可讓您的組織。  購買網域名稱提供 hello 右 toocontrol hello DNS 階層該名稱，例如允許 toodirect hello 名稱 'www.contoso.com' tooyour 公司網站。 hello 註冊機構可能裝載在代表您自己名稱伺服器 hello 網域，或者允許您 toospecify 替代名稱伺服器。

Azure DNS 提供全域散發、 高可用性的名稱伺服器基礎結構，您可以使用 toohost 您的網域。 裝載 Azure DNS 中的網域，您可以管理您的 DNS 記錄，以 hello 相同的認證、 Api、 工具、 帳單和支援與其他 Azure 服務。

Azure DNS 目前不支援購買網域名稱。 如果您想 toopurchase 網域名稱，您會需要 toouse 第三方網域名稱註冊機構。 hello 註冊機構通常費用小年費。 hello 網域的 DNS 記錄管理然後裝載在 Azure DNS。 請參閱[委派網域 tooAzure DNS](dns-domain-delegation.md)如需詳細資訊。

## <a name="dns-zones"></a>DNS 區域

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>DNS 記錄

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>存留時間

hello 時間 toolive 或 TTL，會指定多久每一筆記錄快取的用戶端之前重新進行查詢。 在上述範例中的 hello，hello TTL 是 3600 秒或 1 小時。

在 Azure DNS，hello TTL 指定 hello 資料錄集，不會針對每一筆記錄，因此相同的值用於該記錄中的所有記錄的 hello 設定。  您可以指定介於 1 到 2,147,483,647 秒之間的任何 TTL 值。

### <a name="wildcard-records"></a>萬用字元記錄

Azure DNS 支援 [萬用字元記錄](https://en.wikipedia.org/wiki/Wildcard_DNS_record)。 萬用字元記錄都會傳回到具有相符名稱的回應 tooany 查詢 （除非接近的相符項目，從非萬用字元的資料錄集）。 Azure DNS 支援 NS 和 SOA 以外的所有記錄類型的萬用字元記錄集。

toocreate 萬用字元記錄設定，請使用 hello 記錄集名稱 '\*'。 或者，也可以使用最左邊標籤是 '\*' 的名稱，例如 '\*.foo'。

### <a name="cname-records"></a>CNAME 記錄

CNAME 記錄集不能共存在 hello 與其他資料錄集具有相同名稱。 例如，您無法建立 CNAME 記錄集相對名稱 'www' hello 和 A 記錄以 hello 相對名稱 'www' hello 在相同的時間。

因為 hello 區域的 apex (名稱 = ' @') 一定會包含 hello NS 與 SOA 記錄 hello 區域建立時所建立的設定，您無法建立在 hello 區域的 apex 設定 CNAME 記錄。

這些條件約束會發生的 hello DNS 標準，而且不會限制的 Azure DNS。

### <a name="ns-records"></a>NS 記錄

在 hello 區域的 apex 設定 hello NS 記錄 (名稱 ' @') 會自動建立的每個 DNS 區域，並刪除 hello 區域時自動刪除 （無法刪除個別）。

此記錄集包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。 您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。 您也可以修改 hello TTL 和此記錄集的中繼資料。 不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。 

請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。 可以建立、 修改和刪除條件約束沒有其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。

### <a name="soa-records"></a>SOA 記錄

SOA 記錄集建立而自動建立 hello 區域的每個區域的 apex (名稱 = ' @')，並刪除 hello 區域時自動刪除。  無法個別建立或刪除 SOA 記錄。

您可以修改 hello SOA 記錄 hello 'host' 屬性，就是預先設定的 toorefer toohello 主要名稱伺服器提供的 Azure DNS 除外的所有屬性。

### <a name="spf-records"></a>SPF 記錄

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>SRV 記錄

[SRV 記錄](https://en.wikipedia.org/wiki/SRV_record)所使用的各種服務 toospecify 伺服器位置。 在 Azure DNS 中指定 SRV 記錄時︰

* hello*服務*和*通訊協定*必須是指定為 hello 記錄集名稱的一部分，加上底線。  例如，'\_sip.\_tcp.name'。  在 hello 區域的 apex 記錄，則會有任何需要 toospecify '@' 在 hello 記錄名稱，只要使用 hello 服務和通訊協定，例如'\_sip。\_tcp'。
* hello*優先順序*，*加權*，*連接埠*，和*目標*已指定為 hello 記錄組中的每一筆記錄的參數。

### <a name="txt-records"></a>TXT 記錄

TXT 記錄會使用的 toomap 網域名稱 tooarbitrary 文字字串。 用於多個應用程式，特別相關的 tooemail 組態，例如 hello[寄件者原則架構 (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework)和[DomainKeys 識別郵件 (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)。

hello DNS 標準允許單一的 TXT 記錄 toocontain 多個字串，其中每個可能是 up too254 字元的長度。 使用多個字串時，用戶端會將這些字串連接並視為單一字串。

在呼叫 hello Azure DNS REST API 時，您需要 toospecify TXT 的每個字串分開。  當使用 hello Azure 入口網站、 PowerShell 或 CLI 介面應該指定每筆記錄，如有必要就會自動劃分為段 254 個字元的單一字串。

在 DNS 記錄中的多個字串不應與混淆的 hello hello TXT 記錄組中的多個 TXT 記錄。  TXT 記錄集可以包含多個記錄，「每一個」記錄可以包含多個字串。  Azure DNS 支援每個設定 （透過結合的所有記錄） 的 TXT 記錄總字串長度為 too1024 字元組成。

## <a name="tags-and-metadata"></a>標記和中繼資料

### <a name="tags"></a>標記

標記是名稱 / 值組的清單，以及所使用的 Azure Resource Manager toolabel 資源。  Azure 資源管理員會使用您的 Azure 帳單標記 tooenable 篩選檢視，並讓您 tooset 哪些標籤上的原則所需。 如需標記的詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](../azure-resource-manager/resource-group-using-tags.md)。

Azure DNS 支援在 DNS 區域資源上，使用 Azure Resource Manager 標記。  不支援在 DNS 記錄集上使用標記，不過，支援在 DNS 記錄集上使用「中繼資料」作為替代，如下所述。

### <a name="metadata"></a>中繼資料

做為替代的 toorecord 集標記，Azure DNS 支援註釋使用 'metadata' 的資料錄集。  類似 tootags，中繼資料可讓您 tooassociate 名稱 / 值組，而且每個資料錄集。  這會很有用，例如 toorecord hello 目的每一筆記錄的設定。  與標記不同中繼資料無法使用的 tooprovide Azure 帳單的篩選的檢視，而不指定 Azure Resource Manager 原則中。

## <a name="etags"></a>Etag

假設兩位或兩個處理序嘗試 toomodify DNS 記錄 hello 在相同的時間。 何者獲勝？ 和 hello 成功者知道他們已經覆寫其他人建立的變更嗎？

Azure DNS 會使用 Etag toohandle 並行的變更 toohello 相同資源安全。 Etag 和 [Azure Resource Manager「標籤」](#tags)分開。 每個 DNS 資源 (區域或記錄集) 都有一個相關聯的 Etag。 每當擷取資源時，也會擷取其 Etag。 在更新資源，您可以選擇 toopass 回 hello Etag，讓 Azure DNS 可以確認該 hello Etag hello 伺服器比對。 因為每個更新 tooa 資源產生 hello 正在重新產生的 Etag，Etag 不符表示已發生並行的變更。 建立新的資源 tooensure hello 資源已經存在時，也可以使用 Etag。

根據預設，Azure DNS PowerShell 會使用 Etag tooblock 並行的變更 toozones 資料錄集。 選擇性的 hello *-覆寫*參數可以是使用的 toosuppress Etag 檢查，在此情況下任何並行發生的變更會覆寫。

在 hello 的 hello Azure DNS REST API 層級的 Etag 會使用 HTTP 標頭所指定的。  下表中的 hello 中提供它們的行為：

| 標頭 | 行為 |
| --- | --- |
| None |PUT 一定成功 (沒有 Etag 檢查) |
| If-match <etag> |唯有當資源存在且 Etag 符合時，PUT 才會成功 |
| If-match * |唯有當資源存在時，PUT 才會成功 |
| If-none-match * |唯有當資源不存在時，PUT 才會成功 |


## <a name="limits"></a>限制

使用 Azure DNS 時，適用下列預設限制 hello:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>後續步驟

* 使用 Azure DNS，toostart 深入了解如何太[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。
* toomigrate 現有的 DNS 區域，深入了解如何太[匯入和匯出 DNS 區域檔案](dns-import-export.md)。
