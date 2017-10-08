---
title: "使用 hello Azure CDN 規則引擎 aaaOverride HTTP 行為 |Microsoft 文件"
description: "hello 規則引擎可讓您 toocustomize 如何 HTTP 要求會由 Azure CDN，例如封鎖 hello 傳遞某些類型的內容，定義快取的原則，並修改 HTTP 標頭。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>覆寫使用 hello Azure CDN 規則引擎的 HTTP 行為
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>概觀
hello 規則引擎可讓您 toocustomize 如何 HTTP 要求處理，例如封鎖 hello 傳遞某些類型的內容、 定義快取的原則，以及修改 HTTP 標頭。  本教學課程將示範建立規則，將會變更快取行為的 CDN 資產的 hello。  另外還有視訊內容用於 hello"[另請參閱](#see-also)」 一節。

   > [!TIP] 
   > 如需詳細參考 toohello 語法，請參閱[規則引擎參考](cdn-rules-engine-reference.md)。
   > 


## <a name="tutorial"></a>教學課程
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 按一下 hello **HTTP 大型** 索引標籤，後面接著**規則引擎**。
   
    隨即顯示新規則的選項。
   
    ![CDN 新規則選項](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > 多個規則列中的 hello 順序會影響處理的方式。 後續的規則可能會覆寫先前規則所指定的 hello 動作。
   > 
   > 
3. 輸入的名稱在 hello**名稱 / 描述**文字方塊。
4. 識別 hello 的 hello 規則將套用到要求的類型。  根據預設，hello**永遠**已選取相符的條件。  本教學課程將使用 [永遠]  ，因此請維持選取。
   
   ![CDN 相符條件](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > 有許多類型的相符項目可用在 hello 下拉式清單中的條件。  按一下 hello 藍色資訊圖示 toohello hello 符合條件的左將說明詳細資料中的 hello 目前選取的條件。
   > 
   >  如需詳細資料中的條件式運算式 hello 完整清單，請參閱[規則引擎的條件運算式](cdn-rules-engine-reference-match-conditions.md)。
   >  
   > Hello 的詳細資料中的比對條件的完整清單，請參閱[規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)。
   > 
   > 
5. 按一下 hello  **+** 太下一步按鈕**功能**tooadd 的新功能。  在左側 hello hello 下拉式清單中選取**強制內部 Max-age**。  在出現的 hello 文字方塊中，輸入**300**。  將保留 hello 剩餘預設值。
   
   ![CDN 功能](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > 因為與比對條件，按一下 hello 藍色資訊圖示 toohello hello 的新功能會顯示有關這項功能的詳細資料。  Hello 案例**強制內部 Max-age**，我們會覆寫 hello 資產**Cache-control**和**Expires**標頭 toocontrol 時 hello CDN 邊緣節點將會重新整理 hello從 hello 原點的資產。  我們的範例 300 秒表示 hello CDN 邊緣節點就會快取 hello 資產 5 分鐘後再重新整理從其原來的 hello 資產。
   > 
   > Hello 的功能的詳細資料的完整清單，請參閱[規則引擎功能詳細資料](cdn-rules-engine-reference-features.md)。
   > 
   > 
6. 按一下 hello**新增**按鈕 toosave hello 新規則。  hello 新規則現在正在等待核准。 一旦核准之後，將會變更 hello 狀態**暫止 XML**太**作用中的 XML**。
   
   > [!IMPORTANT]
   > Too90 分鐘 toopropagate 透過 hello CDN 會在規則變更。
   > 
   > 

## <a name="see-also"></a>另請參閱
* [Azure CDN 概觀](cdn-overview.md)
* [規則引擎參考](cdn-rules-engine-reference.md)
* [規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)
* [規則引擎條件運算式](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎功能](cdn-rules-engine-reference-features.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
* [Azure Fridays: Azure CDN's powerful new Premium Features (影片：Azure 星期五：Azure CDN 強大的新高階功能)](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)