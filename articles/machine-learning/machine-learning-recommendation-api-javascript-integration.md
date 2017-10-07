---
title: "Machine Learning 建議：JavaScript 整合 | Microsoft Docs"
description: "Azure Machine Learning Recommendations - JavaScript 整合 - 文件"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Azure Machine Learning Recommendations - JavaScript 整合
> [!NOTE]
> 您應該開始使用 hello 建議 API 認知服務，而不此版本。 hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。 它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。
> 深入了解[移轉 toohello 新認知的服務](http://aka.ms/recomigrate)
> 
> 

本文件描述如何 toointegrate 您使用 JavaScript 的網站。 hello JavaScript 可讓您 toosend 資料擷取的事件和 tooconsume 建議一旦建置推薦模型。 透過 JS 完成的所有操作也能從伺服器端完成。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1.一般概觀
利用 2 階段所包含的 Azure ML Recommendations 來整合您的網站：

1. 將事件傳送到 Azure ML Recommendations。 這會讓 toobuild 推薦模型。
2. 耗用 hello 建議。 建立 hello 模型之後，您可以使用 hello 建議。 （此文件並未說明如何讀取 toobuild 模型時，會 hello 快速入門指南 tooget 詳細資訊）。

<ins>第一階段</ins>

Hello 中第一個階段，您將插入至 html 頁面小型的 JavaScript 程式庫，可讓 hello 頁面 toosend 事件 hello html 網頁上發生時於 Azure ML 建議伺服器 （透過資料市場）：

![繪圖 1][1]

<ins>第二階段</ins>

在 [hello 第二個階段，當您想在 hello] 頁面上的 tooshow hello 建議您選取其中一個 hello 下列選項：

1.您的伺服器 （在頁面上轉譯的 hello 階段） 會呼叫 Azure ML 建議伺服器 （透過資料市場） tooget 建議。 hello 結果會包含項目 id 的清單。您的伺服器需要 tooenrich hello 結果與 hello 項目中繼資料 （例如影像、 描述），並傳送 hello 建立頁面 toohello 瀏覽器。

![繪圖 2][2]

2.hello 另一個選項是 toouse hello 小 JavaScript 檔案從階段一個 tooget 建議項目的簡單清單。 比 hello 第一個選項 hello 一款這裡收到 hello 資料。

![繪圖 3][3]

## <a name="2-prerequisites"></a>2.必要條件
1. 建立新的模型使用 hello 應用程式開發介面。 請參閱 hello 快速入門指南 toodo 它。
2. 使用 base64 將 &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; 編碼。 （這將用於 hello 基本驗證 tooenable hello JS 程式碼 toocall hello 應用程式開發介面）。

## <a name="3-send-data-acquisition-events-using-javascript"></a>3.使用 JavaScript 傳送資料擷取事件
下列步驟的 hello 促進傳送事件：

1. 在程式碼中納入 JQuery 程式庫。 您可以從下列 URL 的 hello 中的 nuget 下載它。
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. 將從下列 URL 的 hello hello 建議 Java 指令碼程式庫包括： http://aka.ms/RecoJSLib1
3. 初始化 Azure ML 建議程式庫與 hello 適當的參數。
   
     <script>AzureMLRecommendationsStart (「<base64encoding of username:key>"，"< model_id >");</script> 
4.傳送嗨適當的事件。 有關所有型別事件的詳細說明 (Click 事件範例)，請參閱下節  <script> 如果 (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    限制和瀏覽器支援
這是參考實作並依現況提供。 其應該支援所有主要瀏覽器。

### <a name="32----type-of-events"></a>3.2.    事件類型
事件的 5 hello 程式庫支援的類型有： 按一下 []，按一下建議，新增 tooShop 購物車，移除購物車及購買。 沒有使用的 tooset hello 使用者內容呼叫登入的其他事件。

#### <a name="321-click-event"></a>3.2.1. 點選事件
每當使用者點選項目時，都應該會使用這個事件。 只有當使用者按一下項目時，通常以 hello 項目詳細資料; 開啟新的頁面在此頁面應觸發這個事件。

參數：

* event (字串, 強制) - “click”
* 項目 (string，強制)-hello 項目的唯一識別碼
* itemName (string，選用)-hello hello 項目名稱
* itemDescription (string，選用)-hello 項目的 hello 描述
* itemCategory (string，選用)-hello hello 項目分類的
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

或使用選擇性資料：

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. 建議點選事件
每當使用者點選項目 (從 Azure ML Recommendations 接收當成建議的項目) 時，都應該會使用這個事件。 只有當使用者按一下項目時，通常以 hello 項目詳細資料; 開啟新的頁面在此頁面應觸發這個事件。

參數：

* event (字串, 強制) - “recommendationclick”
* 項目 (string，強制)-hello 項目的唯一識別碼
* itemName (string，選用)-hello hello 項目名稱
* itemDescription (string，選用)-hello 項目的 hello 描述
* itemCategory (string，選用)-hello hello 項目分類的
* 種子 （字串陣列，選用）-hello 產生 hello 建議查詢的種子。
* （字串陣列，選用）-recoList hello hello 建議要求產生已按下的 hello 項的結果。
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

或使用選擇性資料：

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. 加入購物車事件
此事件應該用於當 hello 使用者加入購物車的項目 toohello。
參數：

* event (字串, 強制) - “addshopcart”
* 項目 (string，強制)-hello 項目的唯一識別碼
* itemName (string，選用)-hello hello 項目名稱
* itemDescription (string，選用)-hello 項目的 hello 描述
* itemCategory (string，選用)-hello hello 項目分類的
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. 移除購物車事件
Hello 使用者移除項目 toohello 購物車時，應該使用這個事件。

參數：

* event (字串, 強制) - “removeshopcart”
* 項目 (string，強制)-hello 項目的唯一識別碼
* itemName (string，選用)-hello hello 項目名稱
* itemDescription (string，選用)-hello 項目的 hello 描述
* itemCategory (string，選用)-hello hello 項目分類的
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. 購買事件
Hello 使用者購買他購物車時，應該使用這個事件。

參數：

* event (字串) - “purchase”
* items (Purchased[]) - 陣列會為購買的每個項目保留一個項目。<br><br>
  已購買項目的格式︰
  * 項目 （字串）-hello 項目的唯一識別碼。
  * count (整數或字串) - 已購買的項目數。
  * 價格 （float 或字串） 為選擇性欄位-hello 價格 hello 項目。

hello 下面範例 3 購買項目 （33、 34、 35），其中包含所有已填入欄位項目、 計數 （價格） 和一個 （項目 34） 沒有價格的兩個。

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. 使用者登入事件
Azure ML 建議事件程式庫會建立並使用來自順序 tooidentify 事件中的 cookie hello 相同的瀏覽器。 在訂單 tooimprove hello 模型結果 Azure ML 建議可讓 tooset 使用者的唯一識別碼，將會覆寫 hello cookie 使用方式。

Hello 使用者登入 tooyour 網站之後，就應該使用此事件。

參數：

* event (字串) - “userlogin”
* 使用者 （字串）-hello 使用者的唯一識別碼。
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4.透過 JavaScript 取用建議
利用 hello 建議的 hello 程式碼是由用戶端 hello 網頁觸發某些 JavaScript 事件。 hello 建議回應會包含 hello 的建議項目 Id、 其名稱和其分級。 這個選項，只讓清單顯示的建議項目-更複雜處理 （例如將 hello 項目中繼資料） 的 hello 應該在 hello 伺服器端整合的最佳 toouse 它。

### <a name="41-consume-recommendations"></a>4.1 取用建議
您需要 tooinclude hello tooconsume 建議需要在頁面和 toocall AzureMLRecommendationsStart 中的 JavaScript 程式庫。 請參閱第 2 節。

一或多個項目的 tooconsume 建議需要的 toocall 呼叫的方法： AzureMLRecommendationsGetI2IRecommendation。

參數：

* 一或多個項目 tooget 建議的項目 （陣列的字串-）。 如果您取用 Fbt 組建，則您在這裡只能設定一個項目。
* numberOfResults (整數) - 所需結果的數目。
* includeMetadata （布林值，選用）-如果設定 too'true' 表示該 hello 中繼資料必須先填入欄位 hello 結果中。
* 處理函式-處理 hello 建議函式傳回。 hello 資料是以陣列傳回：
  * 項目 - 項目唯一識別碼
  * 名稱 - 項目名稱 (如果存在於目錄中)
  * 評等 - 建議評等
  * 中繼資料的字串，代表 hello hello 項目中繼資料

範例： hello 下列程式碼要求 8 建議項目 」 64f6eb0d-947a-4c18-a16c-888da9e228ba 」 (並不指定 includeMetadata-它隱含地說，無中繼資料，就需要)，它必須接著 hello 結果串連成一個緩衝區。

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
