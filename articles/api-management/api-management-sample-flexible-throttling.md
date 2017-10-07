---
title: "使用 Azure API 管理節流 aaaAdvanced 要求"
description: "深入了解如何 toocreate 套用彈性配額及限制使用 Azure API 管理原則的速率。"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>以 Azure API 管理進行進階要求節流
無法 toothrottle 傳入要求是 Azure API 管理的重要角色。 藉由控制 hello 速率要求或 hello 總計要求/資料的傳輸，API 管理可讓應用程式開發介面的提供者 tooprotect 濫用從其應用程式開發介面，並建立不同的應用程式開發介面產品層級的值。

## <a name="product-based-throttling"></a>依產品節流
toodate，hello 速率的節流功能已有限範圍的 toobeing tooa 特定產品的訂閱 （基本上是索引鍵），定義在 hello API 管理發行者入口網站。 這可用於 hello API 提供者 tooapply 限制 hello 開發人員已註冊 toouse 其應用程式開發介面，不過，它也沒有用，例如，在節流的 hello API 的個別使用者。 它有可能在單一使用者的 hello 開發人員應用程式 tooconsume hello 整個配額，然後防止 hello 開發人員的其他客戶可以 toouse hello 應用程式。 此外，可能會產生大量的要求數個客戶可能會限制存取 toooccasional 使用者。

## <a name="custom-key-based-throttling"></a>依自訂索引鍵節流
新的 hello[速率與限制由-鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey)和[配額的索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey)原則提供大幅更有彈性的方案 tootraffic 控制項。 這些新原則可讓您 toodefine 運算式 tooidentify hello 金鑰將會使用的 tootrack 流量使用方式。 簡單範例說明 hello 這個運作的方式。 

## <a name="ip-address-throttling"></a>IP 位址節流
hello 下列原則會限制單一用戶端 IP 位址 tooonly 10 呼叫每隔一分鐘，具有總計的 1000000 呼叫和 10000 kb 為單位的每個月的頻寬。 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

如果所有的用戶端 hello 網際網路上使用唯一的 IP 位址，這可能是限制使用者所使用的有效方式。 不過，就有很多個使用者會共用單一公用 IP 位址到期 toothem 存取 hello 網際網路，透過 NAT 裝置。 儘管這 Api，可讓未授權的存取 hello`IpAddress`可能 hello 最佳選項。

## <a name="user-identity-throttling"></a>使用者身分識別節流
如果使用者經過驗證，則可以根據該名使用者的唯一身分識別產生節流索引鍵。

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

在此範例中我們擷取 hello 授權標頭，將它轉換太`JWT`物件和使用 hello 主旨的 hello 語彙基元 tooidentify hello 使用者用來做為 hello 速率限制索引鍵。 如果 hello 使用者識別會儲存在 hello`JWT`為其中一個其他 hello 然後宣告值無法用於它的位置。

## <a name="combined-policies"></a>結合的原則
雖然 hello 新節流原則提供更多的控制，比 hello 現有節流原則，但仍會有值結合這兩個功能。 節流的訂用帳戶的產品金鑰 ([訂用帳戶限制呼叫率](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[訂用帳戶所設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) 是由充電 tooenable monetizing 應用程式開發介面的基礎使用層級的好方法。 hello 精細地的控制要由使用者所能 toothrottle 互補並防止某個使用者的行為 hello 體驗，另一個導致效能變差。 

## <a name="client-driven-throttling"></a>用戶端導向節流
定義 hello 節流索引鍵時使用[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)，這時就選擇如何範圍 hello 節流的 hello API 提供者。 不過，開發人員可能會想的 toocontrol 它們的評等限制他們自己的客戶。 這可以藉由引進自訂標頭 tooallow hello 開發人員的用戶端應用程式 toocommunicate hello 金鑰 toohello API 啟用 hello API 提供者。

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

這可讓開發人員 hello 用戶端應用程式 toochoose 他們要如何 toocreate hello 速率限制索引鍵。 一點的技巧與用戶端開發人員可以建立自己的速率層配置組的索引鍵 toousers 和旋轉 hello 金鑰使用方式。

## <a name="summary"></a>摘要
Azure API 管理提供速率和引號節流 tooboth 保護，然後加入值 tooyour API 服務。 hello 新節流原則與自訂範圍規則可讓您進行更細微的更細緻的控制這些原則 tooenable 客戶 toobuild 更好應用程式。 本文中的 hello 範例示範這些新原則的 hello 使用製造速率限制用戶端 IP 位址、 使用者識別與用戶端產生值的索引鍵。 不過，還有 hello 訊息，例如使用者代理程式、 URL 的路徑片段、 訊息大小也可使用的許多其他組件。

## <a name="next-steps"></a>後續步驟
請提供您的意見 hello Disqus 執行緒在這個主題。 將有關其他可能的索引鍵值已邏輯的選擇，在您的案例的絕佳 toohear。

## <a name="watch-a-video-overview-of-these-policies"></a>觀看這些原則的影片概觀
如需有關 hello[速率與限制由-鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey)和[配額的索引鍵](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey)原則涵蓋在本文中，請密切注意 hello 下列視訊。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

