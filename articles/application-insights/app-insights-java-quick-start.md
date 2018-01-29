---
title: "Azure Application Insights 快速入門 | Microsoft Docs"
description: "提供指示說明如何快速設定 Java Web 應用程式，以透過 Application Insights 來監視"
services: application-insights
keywords: 
author: mrbullwinkle
ms.author: mbullwin
ms.date: 09/10/2017
ms.service: application-insights
ms.custom: mvc
ms.topic: quickstart
manager: carmonm
ms.openlocfilehash: 9246def86fa647213aa3ec12427d829c24fa8034
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="start-monitoring-your-java-web-application"></a>開始監視 Java Web 應用程式

Azure Application Insights 可讓您輕鬆監視 Web 應用程式的可用性、效能和使用情形。 還可讓您快速識別並診斷應用程式的錯誤，不必等使用者回報。 Application Insights Java SDK 可讓您監視常見的第三方套件，包括 MongoDB、MySQL 和 Redis。

本快速入門引導您將 Application Insights SDK 新增至現有的 Java 動態 Web 專案。

## <a name="prerequisites"></a>必要條件

若要完成本快速入門：

- 安裝 Oracle JRE 1.6 或更新版本，或 Zulu JRE 1.6 或更新版本
- 安裝[免費的 Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)。 本快速入門使用 Eclipse Oxygen (4.7)
- 您需要 Azure 訂用帳戶和現有的 Java 動態 Web 專案
 
如果您沒有 Java 動態 Web 專案，請參閱[建立 Java Web 應用程式快速入門](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-java)來建立。

如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="log-in-to-the-azure-portal"></a>登入 Azure 入口網站

登入 [Azure 入口網站](https://portal.azure.com/)。

## <a name="enable-application-insights"></a>啟用 Application Insights

Application Insights 可以從任何連上網際網路的應用程式收集遙測資料，而不論應用程式在內部部署或雲端中執行。 請使用下列步驟來開始檢視此資料。

1. 選取 [新增] > **[監視 + 管理]** > **[Application Insights]**。

   ![新增 Application Insights 資源](./media/app-insights-java-quick-start/001-j.png)

   將會出現設定方塊，請根據下表來填寫輸入欄位。

    | 設定        | 值           | 說明  |
   | ------------- |:-------------|:-----|
   | **名稱**      | 通用唯一值 | 此名稱可識別您要監視的應用程式 |
   | **應用程式類型** | Java Web 應用程式 | 您要監視的應用程式類型 |
   | **資源群組**     | myResourceGroup      | 用於裝載 App Insights 資料之新資源群組的名稱 |
   | **位置** | 美國東部 | 選擇您附近或接近應用程式裝載位置的地點 |

2. 按一下 [建立] 。

## <a name="install-app-insights-plugin"></a>安裝 App Insights 外掛程式

1. 啟用 **Eclipse** > 按一下 [說明] > 選取 [安裝新軟體]。

   ![新增 App Insights 資源表單](./media/app-insights-java-quick-start/000-j.png)

2. 將 ```http://dl.microsoft.com/eclipse``` 複製到 [運用] 欄位 > 勾選 [Azure Toolkit for Java] > 選取 [Application Insights Plugin for Java] > **取消選取 [安裝期間連絡所有更新網站以尋找所需軟體]**。

3. 當安裝完成之後，系統會提示您**重新啟動 Eclipse**。

## <a name="configure-app-insights-plugin"></a>設定 App Insights 外掛程式

1. 啟動 **Eclipse** > 開啟您的**專案** > 在 [專案總管] 中以滑鼠右鍵按一下專案名稱 > 選取 [Azure] > 按一下 [登入]。

2. 選取 [互動] 驗證方法 > 按一下 [登入] > 出現提示時，輸入您的 [Azure 認證] > 選取您的 [Azure訂用帳戶]。

3. 在 [專案總管] 中以滑鼠右鍵按一下您的專案名稱 > 選取 [Azure] > 按一下 [設定 Application Insights]。

4. 勾選 [對 Application Insights 啟用遙測] > 選取您想要連結至 Java 應用程式的 App Insights 資源及相關聯的**檢測金鑰**。

   ![Eclipse Azure 設定功能表](./media/app-insights-java-quick-start/0007-j.png)

> [!NOTE]
> Application Insights SDK for Java 能夠擷取及視覺化即時計量，但當您第一次啟用遙測收集時，可能需要幾分鐘的時間，資料才會出現在入口網站中。 如果此應用程式是低流量測試應用程式，請記住，只在有使用中的要求或作業時，才會擷取大部分的計量。

## <a name="start-monitoring-in-the-azure-portal"></a>在 Azure 入口網站中開始監視

1. 現在，您可以在 Azure 入口網站中重新開啟 Application Insights [概觀] 頁面 (您先前在此擷取檢測金鑰)，以檢視目前執行中應用程式的詳細資料。

   ![Application Insights 概觀功能表](./media/app-insights-java-quick-start/0008-j.png)

2. 按一下 [應用程式對應]，以顯示應用程式元件之間相依性關聯性的視覺化配置。 每個元件會顯示負載、效能、失敗和警示等 KPI。

   ![應用程式對應](./media/app-insights-java-quick-start/005-j.png)

3. 按一下 [應用程式分析] 圖示 ![應用程式對應圖示](./media/app-insights-java-quick-start/006.png)。 這樣會開啟 **Application Insights Analytics**，它提供一種豐富查詢語言，可用於分析 Application Insights 收集的所有資料。 此案例中會為您產生查詢，可將要求計數以圖表呈現。 您可以撰寫自己的查詢來分析其他資料。

   ![經過一段時間的使用者要求分析圖表](./media/app-insights-java-quick-start/0010-j.png)

4. 返回 [概觀] 頁面，檢查 [健康情況概觀時間軸]。  此儀表板會提供應用程式健康情況的統計資料，包括連入要求數量、這些要求的持續時間，以及任何發生的失敗。

   ![健康情況概觀時間軸圖表](./media/app-insights-java-quick-start/0009-j.png)

   若要在 [網頁檢視載入時間] 圖表中填入**用戶端遙測**資料，請將此指令碼新增至您要追蹤的每個頁面：

   ```HTML
   <!-- 
   To collect end-user usage analytics about your application, 
   insert the following script into each page you want to track.
   Place this code immediately before the closing </head> tag,
   and before any other scripts. Your first data will appear 
   automatically in just a few seconds.
   -->
   <script type="text/javascript">
     var appInsights=window.appInsights||function(config){
     function i(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s="AuthenticatedUserContext",h="start",c="stop",l="Track",a=l+"Event",v=l+"Page",y=u.createElement(o),r,f;y.src=config.url||"https://az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(y);try{t.cookie=u.cookie}catch(p){}for(t.queue=[],t.version="1.0",r=["Event","Exception","Metric","PageView","Trace","Dependency"];r.length;)i("track"+r.pop());return i("set"+s),i("clear"+s),i(h+a),i(c+a),i(h+v),i(c+v),i("flush"),config.disableExceptionTracking||(r="onerror",i("_"+r),f=e[r],e[r]=function(config,i,u,e,o){var s=f&&f(config,i,u,e,o);return s!==!0&&t["_"+r](config,i,u,e,o),s}),t
    }({
        instrumentationKey:"<instrumentation key>"
    });

    window.appInsights=appInsights;
    appInsights.trackPageView();
   </script>
    ```

5. 按一下 [即時資料流]。 您在這裡可以找到 Java Web 應用程式效能的相關計量。 **即時計量資料流**包含連入要求數量、這些要求的持續時間及任何發生之失敗的相關資料。 您也可以即時監視重要效能計量，例如處理器和記憶體。

   ![伺服器計量圖表](./media/app-insights-java-quick-start/livemetricsjava.png)

若要深入了解監視 Java，請參閱[其他 App Insights Java 文件](.\app-insights-java-get-started.md)。

## <a name="clean-up-resources"></a>清除資源

如果您打算繼續進行後續的快速入門或教學課程，請勿清除在此快速入門中建立的資源。 如果您不打算繼續，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源。

1. 從 Azure 入口網站的左側功能表中，依序按一下 [資源群組] 和 [myResourceGroup]。
2. 在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入 **myResourceGroup**，然後按一下 [刪除]。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [尋找並診斷效能問題](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)