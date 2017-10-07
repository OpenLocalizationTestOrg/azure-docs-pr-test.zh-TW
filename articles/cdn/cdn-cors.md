---
title: "Azure CDN 與 CORS aaaUsing |Microsoft 文件"
description: "了解如何 toouse hello Azure 內容傳遞網路 (CDN) toowith 跨原始資源共用 (CORS)。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>搭配 CORS 使用 Azure CDN
## <a name="what-is-cors"></a>CORS 是什麼？
CORS （跨原始資源共用） 是一種 HTTP 功能，可讓 web 應用程式執行另一個網域中的下一個網域 tooaccess 資源。 在訂單 tooreduce hello 跨網站指令碼攻擊的可能性，所有現代化 web 瀏覽器實作稱為安全性限制[相同來源原則](http://www.w3.org/Security/wiki/Same_Origin_Policy)。  這樣可以防止網頁呼叫其他網域中的 API。  CORS 提供安全的方式 tooallow 一個原始主機 （hello 原始網域） toocall 應用程式開發介面中另一個來源。

## <a name="how-it-works"></a>運作方式
CORS 要求有兩種類型，*簡單要求*和*複雜要求*。

### <a name="for-simple-requests"></a>對於簡單要求︰

1. hello 瀏覽器傳送 hello CORS 要求具有其他**原點**HTTP 要求標頭。 此標頭的 hello 值是服務的定義為 hello 組合 hello 父系分頁的 hello 原點*通訊協定，* *網域*和*連接埠。*  當頁面從 https://www.contoso.com 嘗試 tooaccess hello fabrikam.com 原點中的使用者資料時，下列要求標頭的 hello 就會傳送 toofabrikam.com:

   `Origin: https://www.contoso.com`

2. hello 伺服器可能回應 hello 下列任何一項：

   * 回應中的 **Access-Control-Allow-Origin** 標頭指出所允許的來源網站。 例如：

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * HTTP 錯誤碼 403 例如如果 hello 伺服器不允許檢查 hello Origin 標頭之後的 hello 跨原始要求

   * **Access-Control-Allow-Origin** 標頭包含允許所有來源的萬用字元：

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>對於複雜要求︰

複雜的要求是 CORS 要求其中 hello 瀏覽器需要的 toosend*預檢要求*（也就是初步探查） 傳送嗨實際 CORS 要求之前。 hello 預檢要求會要求 hello server 權限是否 hello 原始 CORS 要求可以繼續執行，且未`OPTIONS`要求 toohello 相同的 URL。

> [!TIP]
> 如需有關 CORS 流程和常見的問題的詳細資訊，請檢視 hello [REST api 引導 tooCORS](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/)。
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>萬用字元或單一來源的狀況
在 Azure CDN 的 CORS 會自動運作，不需要額外的組態時 hello**存取控制-允許-原始**toowildcard （*） 或單一來源，設定標頭。  hello CDN 將會快取 hello 第一個回應，且後續要求將會使用 hello 相同的標頭。

如果要求已完成您的原點 hello 上會設定 toohello CDN 先前 tooCORS，您將需要 toopurge 內容上您的端點內容 tooreload hello 內容以 hello**存取控制-允許-原始**標頭。

## <a name="multiple-origin-scenarios"></a>多重來源的狀況
如果您需要 tooallow origins toobe CORS 所允許的特定清單，事情就得較複雜。 hello 問題發生於 hello CDN 快取 hello**存取控制-允許-原始**hello 第一個 CORS 原始的標頭。  Hello CDN 時不同的 CORS 原始後續要求，將服務快取的 hello**存取控制-允許-原始**標頭，並不相符。  有數種方式 toocorrect 這。

### <a name="azure-cdn-premium-from-verizon"></a>來自 Verizon 的 Azure CDN 進階
hello 最佳方式 tooenable 這是 toouse **Verizon 從 Azure CDN Premium**，而這會公開一些進階功能。 

您必須太[建立規則](cdn-rules-engine.md)toocheck hello**原點**hello 要求標頭。  如果它是有效的來源，您的規則將會設定 hello**存取控制-允許-原始**hello 要求中提供的 hello origin 標頭。  如果在 hello 指定 hello 原點**原點**標頭不允許，您的規則應該省略 hello**存取控制-允許-原始**這會導致 hello 瀏覽器 tooreject hello 要求標頭。 

有兩種方式 toodo 這與 hello 規則引擎。  在這兩種情況下，hello**存取控制-允許-原始**從 hello 檔案的原始伺服器的標頭會完全忽略，hello CDN 規則引擎便會完全管理 hello 允許出處 CORS。

#### <a name="one-regular-expression-with-all-valid-origins"></a>包含所有有效來源的規則運算式
在此情況下，您將建立規則運算式，其中包含所有 hello origins 想 tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **來自 Verizon 的 Azure CDN** 會使用 [Perl 相容的規則運算式](http://pcre.org/)做為其規則運算式的引擎。  您可以使用這類工具[規則運算式 101](https://regex101.com/) toovalidate 規則運算式。  請注意，hello"/"字元在規則運算式中有效，而且不需要逸出 toobe，不過，逸出該字元會被視為最佳作法和某些 regex 驗證程式所預期的。
> 
> 

Hello 規則運算式比對，如果您的規則將會取代 hello**存取控制-允許-原始**與 hello 要求傳送嗨原點的 hello 原始標題 （如果有的話）。  您也可以加入額外的 CORS 標頭，例如 **Access-Control-Allow-Methods**。

![包含規則運算式的規則範例](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>針對每個來源要求標頭規則
而不是規則運算式中，您可以改為建立個別的每個來源規則您想使用 hello tooallow**要求標頭萬用字元**[符合條件](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1)。 為使用 hello 規則運算式方法時，hello 規則引擎單獨集 hello CORS 標頭。 

![不含規則運算式的規則範例](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> Hello 上述範例中，在 hello hello 萬用字元使用 * 告訴 hello 規則引擎 toomatch HTTP 和 HTTPS。
> 
> 

### <a name="azure-cdn-standard"></a>Azure CDN 標準
在 Azure CDN 標準設定檔，hello 只有多個來源，而不需 hello hello 萬用字元原點使用的機制 tooallow toouse[查詢字串快取](cdn-query-string.md)。  您要 hello CDN 端點 tooenable 查詢字串設定，以及接著要求從每個允許的網域使用唯一的查詢字串。 如此一來，將會導致 hello CDN 快取每個唯一的查詢字串的個別物件。 這個方法並不理想，不過，因為它會導致多個副本 hello 相同檔案快取上 hello CDN。  

