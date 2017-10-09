---
title: "在 Azure 堆疊 aaaDNS |Microsoft 文件"
description: "Azure Stack 中的 DNS"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/27/2017
ms.author: victorh
ms.openlocfilehash: 8620178833ac29e9653cce332b7c5d89bbdea0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dns-in-azure-stack"></a>Azure Stack 中的 DNS
Azure 堆疊包含 hello 下列 DNS 的功能：
* 支援 DNS 主機名稱解析
* 使用 API 建立和管理 DNS 區域和記錄

## <a name="support-for-dns-hostname-resolution"></a>支援 DNS 主機名稱解析
您可以指定建立對應的公用 IP 資源的 DNS 網域名稱標籤*domainnamelabel.location*。 cloudapp.azurestack.external toohello 公用 IP 位址在 hello Azure 堆疊中的受管理 DNS 伺服器。  

例如，如果您建立的公用 IP 資源**contoso** hello 本機 Azure 堆疊位置中的網域名稱標籤，為 hello 完整的網域名稱 (FQDN) **contoso.local.cloudapp.azurestack.external** toohello 公用 IP 位址 hello 資源的解析。 您可以使用這個 FQDN toocreate 自訂網域指向 Azure 堆疊中 toohello 公用 IP 位址的 CNAME 記錄。

> [!IMPORTANT]
> 每個所建立的網域名稱標籤，皆必須具有唯一的 Azure Stack 位置。

如果您建立 hello 公用 IP 位址使用 hello 入口網站時，它看起來像這樣：

![建立公用 IP 位址](media/azure-stack-whats-new-dns/image01.png)

此設定很有用，如果您想 tooassociate 公用 IP 位址與負載平衡的資源。 例如，您將可能有負載平衡器處理來自 Web 應用程式的要求。 後方 hello 負載平衡器是一或多個虛擬機器的網站。 現在您可以存取 hello 負載平衡的網站的 DNS 名稱，而非 IP 位址。

## <a name="create-and-manage-dns-zones-and-records-using-api"></a>使用 API 建立和管理 DNS 區域和記錄
您可以建立和管理 DNS 區域和 Azure Stack 中的記錄。  

Azure Stack 提供就像 Azure 的 DNS 服務，使用與 Azure DNS API 一致的 API。  裝載 Azure 堆疊 DNS 中的網域，您可以管理您的 DNS 記錄，以 hello 相同的認證、 Api、 工具、 帳單和支援與其他 Azure 服務。 

明顯原因是更簡潔比 Azure 的 hello Azure 堆疊 DNS 基礎結構。 因此，hello 範圍、 小數位數和效能取決於 hello Azure 堆疊部署和部署的 hello 環境的 hello 小數位數。  因此，之類的效能、 可用性、 全域發佈和高可用性 (HA) 可能會與部署 toodeployment 有所不同。

## <a name="comparison-with-azure-dns"></a>與 Azure DNS 比較
Azure 堆疊中的 DNS 是類似 tooDNS 在 Azure 中，有兩種主要的例外：
* **不支援 AAAA 記錄**

    Azure Stack「不」支援 AAAA 記錄，因為 Azure Stack 並不支援 IPv6 位址。  這是 Azure 和 Azure Stack DNS 之間的主要差異。
* **不是多租用戶**

    不同於 Azure hello Azure 堆疊中的 DNS 服務不是多租用戶。 讓每個租用戶無法建立 hello 相同 DNS 區域。 只有 hello 嘗試 toocreate hello 區域的第一個訂閱成功，及後續的要求會失敗。  這是已知問題，也是 Azure 和 Azure Stack DNS 之間的主要差異。 此問題將在未來版本中解決。

此外，Azure Stack DNS 如何實作標記、中繼資料、Etag 和限制皆有細微差異。

hello 下列資訊適用於特別 tooAzure 堆疊 DNS 並稍有不同 Azure DNS。 toolearn 進一步了解 Azure DNS，請參閱[DNS 區域，以及記錄](../dns/dns-zones-records.md)hello Microsoft Azure 文件站台。

### <a name="tags-metadata-and-etags"></a>標記、中繼資料和 Etag

**標記**

Azure Stack DNS 支援在 DNS 區域資源上，使用 Azure Resource Manager 標記。 不支援在 DNS 記錄集上使用標記，不過，支援在 DNS 記錄集上使用「中繼資料」作為替代，接下來會詳述。

**Metadata**

做為替代的 toorecord 集標記，Azure 堆疊 DNS 支援註釋使用 'metadata' 的資料錄集。 類似 tootags，中繼資料可讓您 tooassociate 名稱 / 值組，而且每個資料錄集。 比方說，這可以是很有用的 toorecord hello 目的每個資料錄集。 與標記不同中繼資料無法使用的 tooprovide Azure 帳單的篩選的檢視，而不指定 Azure Resource Manager 原則中。

**Etag**

假設兩位或兩個處理序嘗試 toomodify DNS 記錄 hello 在相同的時間。 何者獲勝？ 和 hello 成功者知道他們已經覆寫其他人建立的變更嗎？

Azure 的堆疊 DNS 會使用 Etag toohandle 並行的變更 toohello 相同資源安全。 Etag 和 Azure Resource Manager「標籤」分開。 每個 DNS 資源 (區域或記錄集) 都有一個相關聯的 Etag。 每當擷取資源時，也會擷取其 Etag。 在更新資源，您可以選擇 toopass 回 hello Etag，讓 Azure 堆疊 DNS 可以確認該 hello Etag hello 伺服器比對。 因為每個更新 tooa 資源產生 hello 正在重新產生的 Etag，Etag 不符表示已發生並行的變更。 建立新的資源 tooensure hello 資源已經存在時，也可以使用 Etag。

根據預設，Azure 堆疊 DNS PowerShell 會使用 Etag tooblock 並行的變更 toozones 資料錄集。 選擇性的 hello *-覆寫*參數可以是使用的 toosuppress Etag 檢查，在此情況下任何並行發生的變更會覆寫。

在 hello 的 hello Azure 堆疊 DNS REST API 層級的 Etag 會使用 HTTP 標頭所指定的。 下表中的 hello 中提供它們的行為：

| 標頭 | 行為|
|--------|---------|
| None   | PUT 一定成功 (沒有 Etag 檢查)|
| If-match| 唯有當資源存在且 Etag 符合時，PUT 才會成功|
| If-match *| 唯有當資源存在時，PUT 才會成功|
| If-none-match *| 唯有當資源不存在時，PUT 才會成功|

### <a name="limits"></a>限制

使用 Azure 堆疊 DNS 時，適用下列預設限制 hello:

| 資源| 預設限制|
|---------|--------------|
| 每一訂用帳戶的區域| 100|
| 每一區域的記錄集| 5000|
| 每一記錄集的記錄| 20|

## <a name="next-steps"></a>後續步驟
[適用於 Azure Stack 的 iDNS 簡介](azure-stack-understanding-dns.md)
