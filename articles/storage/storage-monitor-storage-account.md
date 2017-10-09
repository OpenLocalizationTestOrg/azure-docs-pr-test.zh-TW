---
title: "aaaHow toomonitor Azure 儲存體帳戶 |Microsoft 文件"
description: "了解如何 toomonitor Azure 中使用的儲存體帳戶 hello Azure 入口網站。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 782873648fdbccc0191a074cd4044f97af8b7c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>監視 hello Azure 入口網站的儲存體帳戶

[Azure 儲存體分析](storage-analytics.md)會提供所有儲存體服務的計量以及 Blob、佇列和資料表的記錄。 您可以使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 哪些度量和記錄檔會記錄為您的帳戶，並設定提供度量資料的視覺化呈現的圖表。

> [!NOTE]
> 沒有與檢查 hello Azure 入口網站中的監視資料相關聯的成本。 如需詳細資訊，請參閱 [儲存體分析及計費](/rest/api/storageservices/Storage-Analytics-and-Billing)。
>
> Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。
>
> 儲存體帳戶的複寫類型的區域備援儲存體 (ZRS) 目前沒有 hello 度量或記錄功能已啟用。
> 
> 如需使用儲存體分析和其他工具 tooidentify 的深度指南，診斷和疑難排解 Azure 儲存體相關問題，請參閱[監視、 診斷和疑難排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)。
>

## <a name="configure-monitoring-for-a-storage-account"></a>設定儲存體帳戶的監視

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選取**儲存體帳戶**，然後 hello 儲存體帳戶名稱 tooopen hello 帳戶儀表板。
1. 選取**診斷**在 hello**監視**hello 功能表 刀鋒視窗的區段。

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. 選取 hello**類型**的每個度量資料**服務**toomonitor，並 hello**保留原則**hello 資料。 您也可以停用監視，可設定**狀態**太**關閉**。

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   您可以為每個服務啟用兩種類型的計量，新的儲存體帳戶預設會同時啟用這兩種類型︰

   * **彙總**︰收集計量，例如入口流量/出口流量、可用性、延遲和成功百分比。 這些度量會彙總的 hello blob、 佇列、 表格和檔案服務。
   * **每個應用程式開發介面**： 在加法 toohello 彙總度量資訊，會收集 hello 同一組 hello Azure 儲存體服務 API 中的每個儲存體作業的度量。

   tooset hello 資料保留原則，移動 hello**保留 （天）**滑桿或輸入 hello 天數的資料 tooretain，從 1 too365。 新的儲存體帳戶的 hello 預設值是七天。 如果您不想 tooset 保留原則，請輸入零。 如果沒有任何保留原則，是由 tooyou toodelete hello 監視資料。

   > [!WARNING]
   > 若您以手動方式刪除計量資料，將需要付費。 不花一毛錢 hello 系統會刪除過時的分析資料 （早於保留原則的資料）。 我們建議您將設定保留原則，根據您的帳戶為您想 tooretain 儲存體分析資料的時間長度。 如需詳細資訊，請參閱[當您啟用儲存體度量時，會產生哪些費用？](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)。
   >

1. 當您完成 hello 監視組態時，選取**儲存**。

一組預設的度量資訊會顯示在圖表上 hello 儲存體帳戶 刀鋒視窗，以及 hello 個別服務刀鋒視窗 （blob、 佇列、 表格和檔案）。 一旦您啟用度量服務，就會在其圖表中的資料 tooappear tooan 小時。 您可以選取**編輯**上任何的度量圖表 太[設定的度量](#how-to-customize-metrics-charts)hello 圖表中會顯示。

您可以設定停用度量收集和記錄**狀態**太**關閉**。

> [!NOTE]
> Azure 儲存體使用[資料表儲存體](storage-introduction.md#table-storage)toostore hello 和度量資訊，您儲存體帳戶，帳戶中的資料表中的存放區 hello 度量。 如需詳細資訊，請參閱： [度量的儲存方式](storage-analytics.md#how-metrics-are-stored)。
>

## <a name="customize-metrics-charts"></a>自訂計量圖表

使用下列程序 toochoose hello 的儲存體度量 tooview 度量圖表中。 

1. 啟動儲存體度量的圖表顯示 hello Azure 入口網站。 您可以找到上 hello 圖表**儲存體帳戶 刀鋒視窗**在 hello**度量**刀鋒視窗中的個別服務 （blob、 佇列、 表格及檔案）。

   在此範例中，我們使用下列圖表顯示在 [hello hello**儲存體帳戶] 刀鋒視窗**:

   ![Azure 入口網站中的圖表選擇](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. 接下來，按一下 hello 圖表 tooopen hello 內的任何位置**度量**刀鋒視窗。 選取**編輯圖表**tooopen hello**編輯圖表**刀鋒視窗。

   ![[圖表] 刀鋒視窗上的 [編輯圖表] 按鈕](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. 在 hello**編輯圖表**刀鋒視窗中，選取 hello**時間範圍**hello 度量 toodisplay hello 圖表和 hello 的**服務**（blob、 佇列、 資料表、 檔案） 您希望其度量toodisplay。 這裡我們選取 toodisplay hello 過去一週的度量 hello blob 服務：

   ![在 hello 編輯圖表 刀鋒視窗的時間範圍和服務選項](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. 選取 hello 個別**度量**像您具有 hello 圖表中顯示，請按一下 **確定**。 例如，這裡我們選擇 toodisplay hello *ContainerCount*和*ObjectCount*度量：

   ![[編輯圖表] 刀鋒視窗中的個別計量選擇](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

圖表設定不會影響 hello 集合、 彙總或儲存體監視 hello 儲存體帳戶中的資料，請只 hello 度量資料的檢視。

### <a name="metrics-availability-in-charts"></a>計量在圖表中的可用性

可用的度量變更 hello 清單已選擇 hello 下拉式清單中的服務和您正在編輯的 hello 圖表 hello 單位類型。 例如，只有在編輯以百分比顯示單位的圖表時，才能選取百分比計量，例如 PercentNetworkError 和 PercentThrottlingError︰

![Hello Azure 入口網站中的要求錯誤百分比圖表](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>計量解析

您選取診斷中的 hello 度量資訊會決定 hello 解析度 hello 度量可供您的帳戶：

* **彙總**監視會提供入口流量/出口流量、可用性、延遲和成功百分比等計量。 這些度量會彙總從 hello blob、 資料表、 檔案和佇列服務。
* **每個應用程式開發介面**提供更精細的解析度 （包括計量） 適用於個別儲存作業，此外 toohello 服務層級彙總。

## <a name="configure-metrics-alerts"></a>設定計量警示

您可以建立警示 toonotify 時已達到儲存體資源度量的閾值。

1. tooopen hello**警示規則 刀鋒視窗**，捲動 toohello**監視**區段 hello**功能表刀鋒視窗**選取**警示規則**。
1. 選取**新增警示**tooopen hello**加入警示規則**刀鋒視窗
1. 選取**資源**（blob、 檔案、 佇列、 資料表） 從 hello 下拉式清單中，然後輸入**名稱**和**描述**針對新的警示規則。
1. 選取 hello**度量**，您想要 tooadd 警示，警示**條件**，和**閾值**。 您選擇 hello 閾值單位類型而有所不同 hello 度量。 例如，「 計數 」 是 hello 的單位類型*ContainerCount*，hello hello 單位時*PercentNetworkError*度量是百分比。
1. 選取 hello**期間**。 度量達到或超過 hello 臨界值內 hello 期間觸發警示。
1. (選擇性) 設定 [電子郵件] 和 [Webhook] 通知。 如需 Webhook 的詳細資訊，請參閱[針對 Azure 度量警示設定 Webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。 如果您未設定電子郵件或 webhook 通知，通知只會出現在 hello Azure 入口網站。

![Hello Azure 入口網站中的 [新增警示規則] 刀鋒視窗](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>新增度量圖表 toohello 入口網站儀表板

您可以針對任何儲存體帳戶 tooyour 入口網站儀表板新增 Azure 儲存體度量圖表。

1. 選取按一下**編輯儀表板**hello 中檢視儀表板時[Azure 入口網站](https://portal.azure.com)。
1. 在 hello**並排組件庫**，選取**尋找磚所** > **類型**。
1. 選取 [類型] > [儲存體帳戶]。
1. 在**資源**，選取您想 tooadd toohello 儀表板的度量的 hello 儲存體帳戶。
1. 選取 [類別] > [監視]。
1. 拖放 hello 圖表圖層到 hello 度量您想要顯示的儀表板。 針對所有您想要顯示的度量 hello 儀表板上重複。 在下列映像的 hello，hello"Blob 的總要求 」 圖表會反白顯示為例，但所有 hello 圖表都可供儀表板上的位置。

   ![Azure 入口網站中的圖格庫](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. 選取**完成自訂**hello hello 儀表板當您完成新增圖表頂端附近。

一旦您已經新增圖表 tooyour 儀表板，您可以進一步自訂這些中所述[自訂度量圖表](#how-to-customize-metrics-charts)。

## <a name="configure-logging"></a>設定記錄

您可以指示 Azure 儲存體 toosave 診斷記錄檔的讀取、 寫入和刪除 hello blob、 資料表和佇列服務的要求。 hello 資料保留原則設定也適用於 toothese 記錄檔。

> [!NOTE]
> Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。
>

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，選取**儲存體帳戶**，然後 hello 儲存體帳戶 tooopen hello 儲存體帳戶] 刀鋒視窗的 hello 名稱。
1. 選取**診斷**在 hello**監視**hello 功能表 刀鋒視窗的區段。

    ![診斷功能表項目 監視中 hello Azure 入口網站。](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. 確保**狀態**設定得**上**，並選取 hello**服務**，您想要 tooenable 記錄。

    ![設定登入 hello Azure 入口網站。](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. 按一下 [儲存] 。

hello 診斷記錄檔會儲存在名為 $logs 儲存體帳戶中的 blob 容器。 您可以檢視 hello 記錄資料使用儲存體總管類似 hello [Microsoft 儲存體總管](http://storageexplorer.com)，或以程式設計方式使用 hello 儲存體用戶端程式庫或 PowerShell。

如需存取 hello $logs 容器資訊，請參閱[啟用儲存體記錄和存取記錄資料](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data)。

## <a name="next-steps"></a>後續步驟

* 尋找更多關於儲存體分析之[計量、記錄和帳單](storage-analytics.md)的詳細資料。
* 使用 PowerShell 和程式設計方式 (利用 C#) [啟用 Azure 儲存體計量和檢視計量資料](storage-enable-and-view-metrics.md)。
