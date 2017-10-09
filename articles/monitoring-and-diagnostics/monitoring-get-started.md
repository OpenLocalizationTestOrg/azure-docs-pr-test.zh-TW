---
title: "aaaGet 開始使用 Azure 監視器 |Microsoft 文件"
description: "開始使用 Azure 監視器 toogain 深入了解您的資源 hello 作業，並採取根據資料的動作。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>開始使用 Azure 監視器
Azure 監視器是 hello 平台服務，提供單一來源，Azure 資源的監視。 Azure 監視，您可以以視覺化方式檢視、 查詢、 路由、 封存，並採取行動 hello 度量和來自 Azure 中的資源記錄。 您可以使用使用 hello 監視入口網站刀鋒視窗中，此資料[監視 PowerShell Cmdlet](insights-powershell-samples.md)，[跨平台 CLI](insights-cli-samples.md)，或[Azure 監視 REST Api](https://msdn.microsoft.com/library/dn931943.aspx)。 在本文中，我們逐步幾個 hello 的 Azure 監視，用於示範 hello 入口網站的主要元件。

1. 在 hello 入口網站中，瀏覽過**更多服務**並尋找 hello**監視器**選項。 按一下 hello 星狀圖示 tooadd 這個選項 tooyour [我的最愛] 清單，因此一律會在 hello 左側導覽列中更容易存取。
   
    ![在 hello 服務清單中監視](./media/monitoring-get-started/monitor-more-services.png)
2. 按一下 hello**監視器**向上 hello 選項 tooopen**監視器**刀鋒視窗。 此刀鋒視窗會將您所有的監視設定和資料結合成一個彙總檢視。 它第一次開啟 toohello**活動記錄檔**> 一節。
   
    ![監視刀鋒視窗瀏覽](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Azure 監視有三個監視資料的基本分類： hello**活動記錄檔**，**度量**，和**診斷記錄檔**。
3. 按一下**活動記錄檔**hello 活動記錄檔區段的 tooensure 隨即出現。
   
    ![活動記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    hello [**活動記錄檔**](monitoring-overview-activity-logs.md)描述您的訂用帳戶中的資源上執行的所有作業。 使用 hello 活動記錄檔，您可以決定 hello '功能，對象、 及何時' 用於任何建立、 更新或刪除您的訂用帳戶中的資源上的作業。 比方說，hello 活動記錄檔會告知您，當 web 應用程式已停止，而且使用者已停止。 活動記錄檔事件會儲存在 hello 平台和可用 tooquery 90 天。
   
    您可以建立及儲存查詢的一般篩選器，然後 pin hello 最重要查詢 tooa 入口網站儀表板，就一定會知道是否發生符合您準則的事件。
4. 透過 hello 過去一週，篩選 hello 檢視 tooa 特定資源群組，然後按一下 [hello**儲存**] 按鈕。
   
    ![儲存活動記錄檔查詢](./media/monitoring-get-started/monitor-act-log-save.png)
5. 現在，按一下 [hello **Pin** ] 按鈕。
   
    ![按一下 [釘選] 取得活動記錄檔](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    大部分的此逐步解說中的 hello 檢視可以是已釘選的 tooa 儀表板。 這可協助您在服務上建立作業資料的單一資訊來源。 
6. 傳回 tooyour 儀表板。 您現在可以看到您儀表板中會顯示 hello 查詢 （和結果數目）。 這非常有用，如果您想 tooquickly，請參閱中所發生最近您訂用帳戶，例如任何很重要的動作。 已指派的新角色或已刪除的 VM。
   
    ![活動記錄檔已釘選 toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. 傳回 toohello**監視器**磚，按一下 hello**度量**> 一節。 您必須先 tooselect 資源篩選，然後選取 [使用在 hello hello 刀鋒視窗頂端的 hello] 下拉式清單選項。
   
    ![度量的篩選器資源](./media/monitoring-get-started/monitor-met-filter.png)
   
    所有 Azure 資源皆會發出[**度量**](monitoring-overview-metrics.md)。 這個檢視將所有度量結合在具單一管理平台下，讓您可以輕鬆地了解執行資源的狀況。
8. 一旦您選取的資源，所有可用的度量會出現在 hello hello 刀鋒視窗的左邊。 您可以一次選取度量圖表多種度量資訊，並修改 hello 圖形類型和時間範圍。 您也可以檢視此資源上設定的所有度量警示。
   
    ![Metric blade](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > 部分度量僅可藉由啟用資源上的 [Application Insights](../application-insights/app-insights-overview.md) 及/或 Windows 或 Linux Azure 診斷提供使用。
   > 
   > 
9. 當您滿意您的圖表時，您可以使用 hello **Pin**按鈕 toopin 它 tooyour 儀表板。
10. 傳回 toohello**監視器**刀鋒視窗，然後按一下**診斷記錄**。
    
    ![診斷記錄檔刀鋒視窗](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**診斷記錄檔**](monitoring-overview-of-diagnostic-logs.md)是記錄發出*由*提供該特定資源的 hello 作業的相關資料的資源。 例如，網路安全性群組規則計數器和邏輯應用程式工作流程記錄檔皆為診斷記錄檔的類型。 這些記錄檔可以是儲存在儲存體帳戶，資料流處理 tooan 事件中樞和/或傳送太[記錄分析](../log-analytics/log-analytics-overview.md)。 Log Analytics 是 Microsoft 的營運情報產品，用以進行進階搜尋和警示。
    
    Hello 入口網站中，您可以檢視和篩選的所有資源的清單中訂用帳戶 tooidentify，如果他們已啟用的診斷記錄檔。
11. 按一下 hello 診斷記錄檔 刀鋒視窗中的資源。 如果診斷記錄檔儲存於儲存體帳戶，您會看到每小時記錄檔的清單，可供您直接下載。
    
    ![一項資源的診斷記錄檔](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    您也可以按一下**診斷設定**，這可讓您設定的 tooset 或修改設定封存 tooa 儲存體帳戶，串流 tooEvent 集線器或傳送 tooa 記錄分析工作區。
    
    ![啟用診斷記錄](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    如果您已經設定診斷記錄檔 tooLog 分析，您即可搜尋它們在 hello**記錄搜尋**hello 入口網站的區段。
12. 瀏覽 toohello**警示**hello 監視器 刀鋒視窗的區段。
    
    ![公用警示刀鋒視窗](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    您可以在這裡管理 Azure 資源上的所有[**警示**](monitoring-overview-alerts.md)。 這包括計量、活動記錄事件、Application Insights Web 測試 (位置) 和 Application Insights 主動診斷的警示。 傳送電子郵件 toobe 或 HTTP POST tooa webhook URL，可以觸發警示。
13. 按一下**新增度量的警示**toocreate 警示。
    
    ![新增度量警示](./media/monitoring-get-started/monitor-alerts-add.png)
    
    接著，您可以釘選的警示 tooyour 儀表板 tooeasily 隨時查看其狀態。
14. hello 監視器 > 一節也包含連結太[Application Insights](../application-insights/app-insights-overview.md)應用程式和[記錄分析](../log-analytics/log-analytics-overview.md)管理解決方案。 這些其他的 Microsoft 產品與 Azure 監視器深入整合。
15. 如果您不使用 Application Insights 或 Log Analytics，有可能是 Azure 監視器已與您目前的監視、記錄和警示產品建立合作關係。 請參閱我們[夥伴頁面](monitoring-partners.md)的完整清單以及有關如何 toointegrate。

藉由執行下列步驟和所有相關的磚 tooa 儀表板釘選，您可以建立應用程式和基礎結構，這類的完整的檢視：

![Azure 監視器儀表板](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>後續步驟
* 讀取 hello [Azure 監視器概觀](monitoring-overview.md)

