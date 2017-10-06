---
title: "在 Azure 中的反向 DNS 的 aaaOverview |Microsoft 文件"
description: "了解反向 DNS 如何運作以及如何在 Azure 中使用"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Azure 反向 DNS 和支援概觀

本文提供如何反向 DNS 的運作方式，以及 hello 概觀反向 DNS 案例，Azure 支援。

## <a name="what-is-reverse-dns"></a>什麼是反向 DNS？

傳統的 DNS 記錄啟用從 DNS 名稱 （例如，'www.contoso.com') tooan 的 IP 位址 （例如 64.4.6.100) 對應。  反向 DNS 可讓 hello 轉譯的 IP 位址 (64.4.6.100) 後 tooa 名稱 ('www.contoso.com')。

反向 DNS 記錄使用於多種情況。 例如，反向 DNS 記錄都廣泛利用驗證的電子郵件訊息的寄件者 hello 抵抗電子垃圾郵件。  hello 接收的郵件伺服器擷取 hello hello 傳送伺服器的 IP 位址，反向 DNS 記錄，並確認是否裝載的授權的 toosend hello 傳來的電子郵件原始網域。 

## <a name="how-reverse-dns-works"></a>反向 DNS 的運作方式

反向 DNS 記錄託管於特殊的 DNS 區域，稱為 'ARPA' 區域。  這些區域都會以平行方式，與裝載 'contoso.com'，像是 hello 一般階層構成個別 DNS 階層。

例如，hello 'www.contoso.com' 的 DNS 記錄被實作 hello 名稱在 hello 區域 'contoso.com'，' www' 搭配使用的 DNS 'A' 記錄。  此 A 記錄點 toohello 對應的 IP 位址，在此情況下 64.4.6.100。  hello 反向對應實作分別使用 'PTR' 記錄，名為 '100' hello 區域 '6.4.64.in-addr.arpa' （IP 位址會反轉 ARPA 區域中附註）。此 PTR 記錄，如果它已正確地設定指向 toohello 名稱 'www.contoso.com'。

當組織被指派 IP 位址區塊時，因此也會擷取 hello 右 toomanage hello 對應 ARPA 區域。 hello 對應 toohello IP 位址區塊是供 Azure 所裝載和管理 microsoft ARPA 區域。 您的 ISP 可能會裝載您自己的 IP 位址的 hello ARPA 區域，或可能會允許您選擇，例如 Azure DNS 的 DNS 服務中的 hello ARPA 區域 tooyou 主機。

> [!NOTE]
> 正向 DNS 對應與反向 DNS 對應會在個別的平行 DNS 階層中實作。 hello 'www.contoso.com' 的反向對應是**不**裝載在 hello 區域 'contoso.com'，而是裝載於 hello 對應 IP 位址區塊的 hello ARPA 區域。 IPv4 和 IPv6 位址區塊使用不同的區域。

### <a name="ipv4"></a>IPv4

IPv4 反向對應區域的 hello 名稱應為下列格式的 hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`。

例如，在建立反向對應區域 toohost 記錄與 Ip hello 192.0.2.0/24 前置詞中的主機時，hello 區域名稱來建立隔離的 hello 位址 (192.0.2) 然後反轉 hello 順序 (2.0.192) 並加入 hello hello 網路首碼後置詞`.in-addr.arpa`。

|子網路類別|網路首碼  |反轉的網路首碼  |標準後置詞  |反向區域名稱 |
|-------|----------------|------------|-----------------|---------------------------|
|類別 A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|類別 B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|類別 C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>無類別 IPv4 委派

在某些情況下，配置 tooan 組織 hello IP 範圍小於類別 C （/ 24） 範圍。 在此情況下，hello IP 範圍不是落在區域界限內 hello`.in-addr.arpa`區域階層，因此無法做為子區域委派。

相反地，使用不同的機制是 tootransfer 控制項的個別的反向對應 (PTR) 記錄 tooa 專用 DNS 區域。 這項機制會委派子區域的每個 IP 範圍，然後對應 hello 的每個 IP 位址範圍個別 toothat 子區域使用 CNAME 記錄。

例如，假設組織已授與 hello IP 範圍 192.0.2.128/26 isp。 這代表 64 個 IP 位址，從 192.0.2.128 too192.0.2.191。 此範圍的反向 DNS 實作如下：
- hello 組織會建立稱為 128 26.2.0.192.in-in-addr.arpa 反向對應區域。 hello 前置詞 ' 128-26' 代表 hello 內的網路區段指派 toohello 組織 hello 類別 C （/ 24） 範圍。
- hello ISP hello 類別 C 上層區域從建立 NS 記錄 tooset 向上 hello hello 上方區域的 DNS 委派。 它也會建立 CNAME 記錄在 hello 父 (類別 C) 反向對應區域中，對應 hello IP 範圍 toohello 新區域建立 hello 組織中的每個 IP 位址：

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- 然後 hello 組織管理其子區域中的 hello 個別 PTR 記錄。

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
Hello PTR 記錄的 IP 位址 '192.0.2.129' 查詢的反向查閱名為 '129.2.0.192.in-addr.arpa'。 此查詢會透過 hello CNAME hello 父區域 toohello PTR 記錄中 hello 子區域解析。

### <a name="ipv6"></a>IPv6

IPv6 反向對應區域的 hello 名稱應為下列形式的 hello:`<IPv6 network prefix in reverse order>.ip6.arpa`

例如： 為與 Ip 主機位於 hello 2001:db8:1000:abdc toohost 記錄建立反向對應區域時:: / 64 的前置詞，會藉由隔離 hello 的 hello 位址的網路首碼建立 hello 區域名稱 (2001:db8:abdc::)。 接下來展開 hello IPv6 網路首碼 tooremove[零壓縮](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)，如果它是使用的 tooshorten hello IPv6 位址首碼 (2001:0db8:abdc:0000::)。 反向 hello 順序，因為 hello hello 前置詞中的每個十六進位數字之間的分隔符號，請使用句號，toobuild hello 反轉網路首碼 (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) 並加入 hello 尾碼`.ip6.arpa`。


|網路首碼  |已展開並反轉的網路首碼 |標準後置詞 |反向區域名稱  |
|---------|---------|---------|---------|
|2001:db8:abdc::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>Azure 的反向 DNS 支援

Azure 支援兩個不同的案例與相關 tooreverse DNS:

**裝載 hello 反向對應區域對應 tooyour IP 位址區塊。**
可以使用 azure DNS 太[裝載反向對應區域和管理 hello PTR 記錄的每個反向 DNS 查閱](dns-reverse-dns-hosting.md)、 IPv4 和 IPv6。  hello 建立 hello (ARPA) 的反向對應區域，設定 hello 委派的程序，並設定 PTR 記錄是 hello 相同與一般的 DNS 區域。  hello 只差異是，必須設定 hello 委派，透過您的 ISP，而不是 DNS 註冊機構，以及應該用於 hello PTR 記錄類型。

**設定 hello 反向 DNS 記錄 hello 分派 tooyour Azure 服務的 IP 位址。** Azure 可讓您太[hello IP 位址配置 tooyour Azure 服務設定 hello 反向對應](dns-reverse-dns-for-azure-services.md)。  Azure 會設定此反向對應為 hello 對應 ARPA 區域中的 PTR 記錄。  由 Microsoft 主控這些 ARPA 區域中，對應 Azure 中，所使用的 tooall hello IP 範圍

## <a name="next-steps"></a>後續步驟

如需反向 DNS 的詳細資訊，請參閱維基百科的 [reverse DNS lookup](http://en.wikipedia.org/wiki/Reverse_DNS_lookup) (反向 DNS 對應)。
<br>
了解如何太[主機 hello 反向對應區域，為您的 ISP 指派的 IP 範圍，在 Azure DNS](dns-reverse-dns-for-azure-services.md)。
<br>
了解如何太[管理您的 Azure 服務的反向 DNS 記錄](dns-reverse-dns-for-azure-services.md)。

