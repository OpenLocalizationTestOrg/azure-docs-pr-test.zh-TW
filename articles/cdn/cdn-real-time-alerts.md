---
title: "aaaAzure CDN 的即時警示 |Microsoft 文件"
description: "Microsoft Azure CDN 中的即時警示。 即時警示提供有關 hello 效能，您的 CDN 設定檔中的 hello 端點的通知。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Microsoft Azure CDN 中的即時警示
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overview
本文件說明 Microsoft Azure CDN 中的即時警示。 這項功能提供您的 CDN 設定檔中的 hello 端點的 hello 效能的即時通知。  您可以根據以下狀況設定電子郵件或 HTTP 警示︰

* 頻寬
* 狀態碼
* 快取狀態
* 連線

## <a name="creating-a-real-time-alert"></a>建立即時警示
1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
3. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**即時統計資料**彈出式視窗。  按一下 [即時警示] 。
   
    ![CDN 管理入口網站](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    會顯示 hello 清單的現有警示的組態 （如果有的話）。
4. 按一下 hello**新增警示** 按鈕。
   
    ![新增警示按鈕](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    隨即會顯示可供建立新警示的表單。
   
    ![新增警示表單](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. 如果您想要此警示 toobe active 當您按一下**儲存**，檢查 hello**啟用警示**核取方塊。
6. 輸入您的警示的描述性名稱在 hello**名稱**欄位。
7. 在 hello**媒體類型**下拉式清單中，選取**HTTP 大型物件**。
   
    ![選取了 HTTP 大型物件的媒體類型](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > 您必須選取**HTTP 大型物件**為 hello**媒體類型**。  hello 其他選項不會使用**Verizon 從 Azure CDN**。  失敗 tooselect **HTTP 大型物件**會導致您的警示觸發 toonever。
   > 
   > 
8. 建立**運算式**選取 toomonitor**度量**，**運算子**，和**觸發值**。
   
   * 如**度量**，選取您想要監視的狀況 hello 類型。  **頻寬 Mbps**是 hello mbps 的頻寬使用量的數量。  **總連線**是 hello 數字的並行 HTTP 連線 tooour 邊緣伺服器。  如需 hello 的定義各種快取狀態和狀態碼，請參閱[Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)和[Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)
   * **運算子**是 hello 數學運算子，以建立 hello hello 度量和 hello 觸發程序的值之間的關聯性。
   * **觸發值**通知將送出之前，必須符合的 hello 臨界值。
     
     在下列範例中的 hello，我已經建立 hello 運算式會表示我希望 toobe hello 404 狀態碼的數目大於 25 時收到通知。
     
     ![即時警示的範例運算式](./media/cdn-real-time-alerts/cdn-expression.png)
9. 如**間隔**，輸入您想要評估的 hello 運算式的頻率。
10. 在 hello**通知**下拉式清單中，選取您想要 toobe 時收到通知 hello 運算式為 true 時。
    
    * **條件開始**指出 hello 指定首次偵測到條件時，將收到通知。
    * **條件結束**指出 hello 可讓您指定不會再偵測到條件時，將收到通知。 網路監視系統偵測到指定的 hello 之後，可以只觸發此通知條件發生。
    * **連續**表示通知會傳送 hello 網路監視系統每次偵測到指定的 hello 條件。 請記住 hello 網路監視系統將只檢查一次每個間隔 hello 指定條件。
    * **條件開始和結束**指出 hello 偵測到 hello 指定的條件的第一次，然後再次 hello 條件不會再偵測到時，將收到通知。
11. 如果您想要 tooreceive 通知電子郵件，請檢查 hello**透過電子郵件通知**核取方塊。  
    
    ![透過電子郵件通知表單](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    在 hello**至**欄位中，輸入您想通知傳送嗨電子郵件地址。 如**主旨**和**主體**、 您可能會讓 hello 預設值，或您可以自訂 hello 訊息使用 hello**可用關鍵字**清單 toodynamically 插入警示資料時傳送 hello 訊息。
    
    > [!NOTE]
    > 您可以測試 hello 電子郵件通知，依序按一下 hello**測試通知**按鈕，但僅限於儲存 hello 警示設定後。
    > 
    > 
12. 如果您想通知 toobe 張貼 tooa web 伺服器，請檢查 hello**通知，透過 HTTP Post**核取方塊。
    
    ![透過 HTTP Post 通知表單](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    在 hello **Url**欄位中，輸入您想讓 hello HTTP 訊息公佈的 hello URL。 在 hello**標頭**文字方塊中，輸入 hello HTTP 標頭 toobe hello 要求中傳送。  如**主體**您呇簏濻 hello 訊息使用 hello**可用關鍵字**清單 toodynamically 傳送 hello 訊息時，插入警示資料。  **標頭**和**主體**預設下列範例中的 tooan XML 裝載類似 toohello。
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > 您可以按一下 hello 測試 hello HTTP Post 通知**測試通知**按鈕，但僅限於儲存 hello 警示設定後。
    > 
    > 
13. 按一下 hello**儲存**按鈕 toosave 您警示設定。  如果您在步驟 5 中核取了 [已啟用警示]  ，您的警示現在便已啟用。

## <a name="next-steps"></a>後續步驟
* 分析 [Azure CDN 中的即時統計資料](cdn-real-time-stats.md)
* 進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)
* 分析 [使用模式](cdn-analyze-usage-patterns.md)

