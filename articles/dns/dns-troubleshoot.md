---
title: "aaaAzure DNS 疑難排解指南 |Microsoft 文件"
description: "Tootroubleshoot 常見方式，與 Azure DNS 問題"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Azure DNS 疑難排解指南

此頁面提供 Azure DNS 常見問題的疑難排解資訊。

如果這些步驟未能解決問題，您也可以在 [MSDN 上的社群支援論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)搜尋或張貼您的問題。 或者，開啟 Azure 支援要求。


## <a name="i-cant-create-a-dns-zone"></a>我無法建立 DNS 區域

tooresolve 常見的問題，再試一次一或多個步驟的 hello:

1.  檢閱 hello Azure DNS 稽核記錄 toodetermine hello 失敗原因。
2.  每個 DNS 區域名稱都必須是其資源群組中唯一的。 也就是兩個 DNS 區域與 hello 相同名稱不能共用的資源群組。 請嘗試使用不同的區域名稱，或不同的資源群組。
3.  您可能會看到錯誤 「 您已達到或超過 hello 的訂用帳戶 {訂閱 id} 中的區域數目上限。 」 使用不同的 Azure 訂用帳戶、 刪除某些區域中，或連絡 Azure 支援 tooraise 訂用帳戶限制。
4.  您可能會看到錯誤 「 hello 區域 '{區域 name}' 不可以使用。 」 此錯誤表示 Azure DNS 已無法 tooallocate 名稱伺服器的 DNS 區域。 請嘗試使用不同的區域名稱。 或者，如果您 hello 網域名稱擁有者，請連絡 Azure 支援人員可以配置名稱伺服器。


### <a name="recommended-documents"></a>**建議的文件**

[DNS 區域和記錄](dns-zones-records.md)
<br>
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>我無法建立 DNS 記錄

tooresolve 常見的問題，再試一次一或多個步驟的 hello:

1.  檢閱 hello Azure DNS 稽核記錄 toodetermine hello 失敗原因。
2.  Hello 記錄集並已經存在嗎？  Azure DNS 管理使用記錄的記錄*設定*，這是相同的名稱和 hello 相同的 hello 之記錄的 hello 集合型別。 如果存在具有相同名稱，且已輸入的 hello 的記錄，然後 tooadd 這類的另一個記錄，您應該編輯現有記錄的 hello 設定。
3.  您嘗試 toocreate 在 hello DNS 區域 apex (hello 'root' hello 區域的) 的記錄嗎？ 如果所以 hello DNS 慣例是 toouse hello ' @' 字元做為 hello 記錄名稱。 也請注意 hello DNS 標準不會在 hello 區域的 apex 在允許的 CNAME 記錄。
4.  您有 CNAME 衝突嗎？  hello DNS 標準不允許為任何其他類型的記錄名稱相同的 hello 的 CNAME 記錄。 如果您有現有的 CNAME，以相同名稱的不同型別失敗的 hello 建立記錄。  同樣地，建立 CNAME 失敗如果 hello 名稱符合不同類型的現有記錄。 藉由移除 hello 移除 hello 衝突，其他的記錄，或選擇不同的記錄名稱。
5.  您已達到允許 DNS 區域中的記錄集的 hello 數目 hello 上限嗎？hello 目前的記錄集數而且 hello 資料錄集的最大數目會顯示 hello hello '屬性' hello 區域底下的 Azure 入口網站。 如果您已達到此限制，然後刪除某些資料錄集或連絡 Azure 支援 tooraise 此區域的資料錄集限制，然後再試一次。 


### <a name="recommended-documents"></a>**建議的文件**

[DNS 區域和記錄](dns-zones-records.md)
<br>
[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>我無法解析我的 DNS 記錄

DNS 名稱解析是多步驟程序，可能會因為許多原因而失敗。 hello 下列步驟協助您調查 DNS 記錄裝載於 Azure DNS 區域中的 DNS 解析失敗的原因。

1.  確認 hello DNS 記錄已正確設定 Azure DNS 中。 檢閱 hello hello 檢查 hello 區域名稱、 記錄名稱，以及記錄類型正確的 Azure 入口網站中的 DNS 記錄。
2.  確認 hello DNS 記錄正確解析 hello Azure DNS 名稱伺服器上。
    - 如果您從本機電腦進行 DNS 查詢，您可能會看到快取不會反映 hello hello 名稱伺服器的目前狀態的結果。  此外，公司網路通常會使用 DNS proxy 伺服器，這可以防止 DNS 查詢正在導向 toospecific 名稱伺服器。  tooavoid 這些問題，使用網頁型名稱解析服務例如[digwebinterface](http://digwebinterface.com)。
    - 為確定 toospecify hello 正確的名稱伺服器，您的 DNS 區域，hello Azure 入口網站中所示。
    - 請檢查 hello DNS 名稱正確 （必須 toospecify hello 完整限定名稱，包括 hello 區域名稱），以及 hello 記錄類型正確
3.  確認已正確設定該 hello DNS 網域名稱[委派 toohello Azure DNS 名稱伺服器](dns-domain-delegation.md)。 有[許多第三方網站可提供 DNS 委派驗證](https://www.bing.com/search?q=dns+check+tool)。 這項測試很*區域*委派測試，因此您應該只輸入 hello DNS 區域名稱，而不 hello 完整記錄名稱。
4.  已完成上述 hello，您的 DNS 記錄應現在正確解析。 tooverify，您可以再次使用[digwebinterface](http://digwebinterface.com)，這次使用 hello 預設名稱的伺服器設定。


### <a name="recommended-documents"></a>**建議的文件**

[委派網域 tooAzure DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>如何指定 hello 'service' 和 'protocol' SRV 記錄？

Azure DNS 管理 DNS 記錄，做為資料錄集 — 以相同的名稱和 hello 相同的 hello hello 記錄的集合型別。 SRV 記錄集，hello 'service' 和 'protocol' 需要 toobe hello 記錄集名稱的一部分。 hello SRV 指定其他參數 （'priority'、 'weight'、 'port' 和 'target'） 會分別 hello 記錄組中的每一筆記錄。

例如，SRV 記錄名稱 (服務名稱 'sip'，通訊協定 'tcp')：

- \_sip。\_tcp （建立之記錄集在 hello 區域的 apex）
- \_sip.\_tcp.sipservice (建立名為 'sipservice' 的記錄集)

### <a name="recommended-documents"></a>**建議的文件**

[DNS 區域和記錄](dns-zones-records.md)
<br>
[建立 DNS 資料錄集，並使用記錄 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)
<br>
[SRV 記錄類型 (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>後續步驟

* 了解 [DNS 區域和記錄](dns-zones-records.md)
* 使用 Azure DNS，toostart 深入了解如何太[建立 DNS 區域](dns-getstarted-create-dnszone-portal.md)和[建立 DNS 記錄](dns-getstarted-create-recordset-portal.md)。
* toomigrate 現有的 DNS 區域，深入了解如何太[匯入和匯出 DNS 區域檔案](dns-import-export.md)。

