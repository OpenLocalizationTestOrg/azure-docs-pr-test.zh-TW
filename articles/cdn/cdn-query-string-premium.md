---
title: "Azure CDN 快取行為，與查詢字串-Premium aaaControl |Microsoft 文件"
description: "Azure CDN 查詢字串快取控制項檔案的 toobe 當其包含查詢字串快取的方式。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>使用查詢字串控制 Azure CDN 快取行為 - Premium
> [!div class="op_single_selector"]
> * [標準](cdn-query-string.md)
> * [來自 Verizon 的 Azure CDN 進階](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>概觀
查詢字串快取檔案的方式 toobe 當其包含查詢字串快取的控制項。

> [!IMPORTANT]
> hello Standard 和 Premium CDN 產品提供 hello 同樣的查詢字串快取功能，但 hello 使用者介面會不同。  本文件說明 hello 介面**Verizon 從 Azure CDN Premium**。  如需利用**來自 Akamai 的 Azure CDN 標準**和**來自 Verizon 的 Azure CDN 標準**查詢字串快取，請參閱[利用查詢字串控制 CDN 要求的快取行為](cdn-query-string.md)。
> 
> 

提供三種可用模式：

* **標準快取**： 這是 hello 預設模式。  hello CDN 邊緣節點將會從傳遞至 hello 查詢字串 hello 要求者 toohello 原點上 hello 第一個要求和快取 hello 資產。  Hello 快取的資產到期之前，所有後續要求資產所服務的 hello 邊緣節點將會忽略 hello 查詢字串。
* **無快取**： 在此模式中，查詢字串的要求不會快取在 hello CDN 邊緣節點。  hello 邊緣節點會直接從 hello 原點擷取 hello 資產，並將其傳遞 toohello 隨著每項要求的要求者。
* **唯一快取**：此模式會將包含查詢字串的每個要求視為具有專屬快取的唯一資產。  例如，hello 回應 hello 原點的要求*foo.ashx?q=bar*會在 hello 邊緣節點快取，後續的快取，以該相同的查詢字串傳回。  要求*foo.ashx?q=somethingelse*做為個別的資產 toolive 自己時間就會快取。

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>變更進階 CDN 設定檔的查詢字串快取設定
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello **HTTP 大型** 索引標籤，然後暫留在 hello**快取設定**彈出式視窗。  按一下 [ **查詢字串快取**]。
   
    查詢字串快取選項隨即顯示。
   
    ![CDN 查詢字串快取選項](./media/cdn-query-string-premium/cdn-query-string.png)
3. 您的選取範圍之後，按一下 [hello**更新**] 按鈕。

> [!IMPORTANT]
> 當它需要花費一些時間透過 hello CDN hello 註冊 toopropagate，可能無法立即看到，hello 設定變更。  若為<b>來自 Verizon 的 Azure CDN</b> 設定檔，則通常會在 90 分鐘之內完成傳播，但在某些情況下可能會更久。
> 
> 

