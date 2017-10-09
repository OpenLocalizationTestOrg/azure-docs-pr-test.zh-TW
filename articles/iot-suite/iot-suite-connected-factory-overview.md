---
title: "aaaAzure IoT 套件連線 factory 概觀 |Microsoft 文件"
description: "Hello Azure IoT 套件的描述連接工廠預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>開始使用 hello 連接工廠預先設定的解決方案

Azure IoT 套件[預先設定的解決方案][ lnk-preconfigured-solutions]結合多個 Azure IoT 服務 toodeliver 端對端方案實作常見的 IoT 商務案例。 hello*連接的工廠*預先設定的方案連接 tooand 監視您工業的裝置。 您可以使用 hello 方案 tooanalyze hello 資料資料流，從您的裝置和 toodrive 操作產能和獲利率。

此教學課程會示範如何 tooprovision hello 連接工廠預先設定的解決方案。 它也會引導您透過預先設定的 hello 解決方案的 hello 基本功能。 您可以存取這些功能從 hello 方案*儀表板*部署預先設定的 hello 方案的一部分：

![連線處理站預先設定的解決方案儀表板][img-cf-home]

toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。

> [!NOTE]
> 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。
> 
> 

## <a name="provision-hello-solution"></a>佈建 hello 方案

1. 登入 tooazureiotsuite.com 使用您的 Azure 帳戶的認證，然後按一下 「**+**"toocreate 方案。
2. 按一下**選取**上 hello**連接的工廠**磚。
3. 輸入連線處理站預先設定的解決方案的 [解決方案名稱]。
4. 選取 hello**訂用帳戶**和**區域**希望 toouse tooprovision hello 方案。
5. 按一下**建立方案**toobegin hello 佈建程序。 這個程序通常需要幾分鐘的時間 toorun。

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>當您等候佈建程序 toocomplete hello

1. 按一下具有您方案的 hello 磚**佈建**狀態。
2. 請注意 hello**佈建狀態**您 Azure 訂用帳戶中部署 Azure 服務。
3. 佈建完成之後，hello 狀態變更太**準備**。
4. 按一下您的方案在 hello 右窗格中的 hello 磚 toosee hello 詳細資料。

> [!NOTE]
> 如果您遇到部署預先設定的 hello 解決方案的問題，請檢閱[hello azureiotsuite.com 網站的權限][ lnk-permissions]和 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。 如果 hello 問題仍然存在，則在 hello 上建立服務票證[入口網站][lnk-portal]。

有 toosee 如預期般詳細資料，未列出您的解決方案嗎？ 請在 [使用者心聲](https://feedback.azure.com/forums/321918-azure-iot)中提供功能建議給我們。

## <a name="scenario-overview"></a>案例概觀

當您將部署連接的 hello factory 預先設定的解決方案，都會填入 toostep 透過常見的工業案例可讓您的資源。 在此案例中，數個處理站連接 hello 資料值的必要的 toocompute toohello 方案報表整體設備效率 (OEE) 和關鍵效能指標 (Kpi)。 hello 下列各節說明您如何以：

* 監視處理站、生產線、站區 OEE 和 KPI 值
* 分析產生從這些裝置使用 Azure 時間數列 Insights hello 遙測資料
* 處理警示 toofix 問題

此案例中的主要功能是可以執行所有這些動作從 hello 方案儀表板的遠端。 您不需要實際存取 toohello 裝置。

## <a name="view-hello-solution-dashboard"></a>檢視 hello 方案儀表板

hello 方案儀表板可讓您 toomanage hello 部署方案。 它是全域處理站組態的階層式表示法。 例如，您可以檢視 OEE 和 KPI、針對遙測和動作警示發佈新節點。

1. 當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 連接的工廠方案入口網站的新索引標籤。

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. 根據預設，hello 方案入口網站會顯示 hello*儀表板*。 toonavigate tooother 區域 hello 入口網站的左側 hello hello 頁面使用 hello 功能表。

    ![連線處理站預先設定的解決方案儀表板][cf-img-menu]

hello 儀表板會顯示下列資訊的 hello:

* A **Factory 清單**hello 狀態、 位置以及目前 production 組態會顯示 hello 方案中的面板。 當您第一次執行 hello 方案時，有的模擬的裝置數目。 hello 生產線模擬被由三個實際 OPC UA 每個伺服器產品線，執行模擬的工作，共用資料。 如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。
* A**對應**顯示 hello 位置，每個裝置的連線 toohello 方案。 hello 解決方案可以使用 hello Bing Maps API tooplot 資訊 hello 地圖上。 如果您的訂用帳戶已啟用 Bing 地圖服務企業版 API，則會自動使用這項功能。 如果沒有，請參閱 hello[常見問題集][ lnk-faq] toolearn toomake hello 對應動態的方式。
* **警示**面板，可顯示遙測或 OEE/KPI 值超過特定閾值時所產生的警示。
* **設備的整體效率**顯示 hello 整個企業中或 hello 原廠生產環境的 hello OEE 值行/站台您正在檢視的面板。 這個值是從 hello 站台檢視 toohello 企業層級彙總。 hello OEE 圖和其組成的項目可以進一步分析。
* **關鍵效能指標**面板會顯示 hello 數所產生的單位和 hello 整個企業或 hello factory/實際列所使用的能源 / 站台您正在檢視。 這些值會從站台檢視 toohello 企業層級彙總。

## <a name="view-factories"></a>檢視工廠

hello*工廠*面板顯示 hello hello 方案、 狀態，以及目前 production 組態中的所有 hello factory 的地理位置。 從 hello 位置清單中，您可以瀏覽 toohello hello 方案階層架構中的其他層級。 hello hello 清單中的資料列為連結 hello 生產線在該位置的詳細資料的超連結。 就可能 toodrill 到 hello 生產線詳細資料，並向 toohello 站台層級檢視。 您也可以套用篩選器 toohello 清單。

![連線處理站預先設定的解決方案處理站][cf-img-factories] 

1. hello **Factory 面板**顯示 hello 這個解決方案的處理站清單。

2. hello factory 清單一開始會顯示六個 hello 佈建程序所建立的處理站。 您可以加入其他的虛擬和實體裝置 toohello 方案。

3. tooview hello 詳細資料，處理站，按一下 hello hello factory 清單中的資料列。

4. tooview hello 詳細資料的實際執行列中，按一下 hello hello 清單中的資料列。

5. tooview hello 發佈的站台 hello 生產線上的 OPC UA 節點時，按一下 hello hello 清單中的資料列。

6. tooview hello 站中的特定節點的詳細資訊，按一下 hello hello 清單中的資料列。 此動作會啟動具有時間數列 Insights 視覺效果的 hello 內容面板。 按一下這些圖形 toodo 進一步的分析 hello 時間數列 Insights 總管環境中。

## <a name="view-map"></a>檢視地圖

如果您的訂用帳戶有存取 toohello Bing Maps API，hello*工廠*地圖顯示您 hello 地理位置和狀態的所有 hello factory hello 方案中。 toodrill 到 hello 位置詳細資料，按一下 hello hello 地圖上顯示的位置。

![連線處理站預先設定的解決方案地圖][cf-img-map]

## <a name="view-alerts"></a>檢視警示

hello**警示** 面板會顯示因為產生的警示 tooa 報告值或導出的 OEE/KPI 值超過設定的閾值。 此面板會顯示每個階層的層級 hello，從 hello 站台層級檢視 toohello 全域檢視警示。 hello 警示包含 hello 警示、 日期、 時間、 位置和發生次數的描述。 您可以深入了 toohello 資料造成 hello 警示使用 hello 時間數列 Insights 資料。 資料以視覺化方式檢視中的 hello 時間數列 Insights hello 警示，在適用情況。 如果您是系統管理員，您可以執行預設動作 hello 警示，例如：

* 關閉 hello 警示。
* 了解 hello 警示。

您可以選擇性地採取更複雜的動作。 例如，對於 hello 不足的壓力 OPC UA 節點 hello 組件，您可以：

* 在新的瀏覽器視窗中的網頁顯示支援資訊。
* 降低 hello 警示原因的 hello OPC UA 方法呼叫 hello 裝置上。
* 隱藏 hello 可用性的 hello 預設動作。

    ![連線處理站預先設定的解決方案警示][cf-img-alerts]

> [!NOTE]
> 這些警示在預先設定的 hello 方案中的組態檔中指定的規則所產生。 這些規則 hello OEE 或 OPC UA 節點值或 KPI 圖形已超過設定的閾值時產生警示。

1. hello**警示面板**顯示 hello 這個方案中產生的警示。

2. tooview hello 詳細資料的警示，按一下 hello 警示面板中的 hello 警示。

3. toofurther 分析 hello 警示的資料，請按一下 hello 警示面板 tooopen hello 時間數列 Insights 總管環境中的 hello 圖形。

4. tooaddress hello 警示，hello 警示面板中使用數個動作。 選擇 hello 適當的選項，然後按一下 hello 執行動作的命令按鈕。

## <a name="view-overall-equipment-efficiency"></a>檢視整體設備效率

OEE 率 hello hello 製造程序使用索引鍵與實際執行相關作業參數的效率。 OEE 是一套的業界標準的量值計算而乘以 hello 可用性率、 效能速度及品質速率： OEE = x 效能品質的可用性。

![連線處理站預先設定的解決方案 OEE][cf-img-oee]

1. tooview OEE hello 階層中的任何層級瀏覽 toohello 您需要的特定檢視。 hello OEE 適用於該檢視會顯示 hello 面板，以及每個構成 hello OEE 百分比 hello 項目中。

2. toofurther 分析 hello OEE hello 階層資料中的任何層級，請按一下 hello OEE、 可用性、 效能或品質百分比。 內容面板會顯示時間序列 Insights 供電的視覺效果顯示 hello 過去一小時、 過去 24 小時和過去 7 天的資料。

    ![連線處理站預先設定的解決方案 TSI 視覺效果][cf-img-tsi-visualization]

3. toofurther 分析 hello 警示的資料，請按一下 hello 警示面板中的 hello 圖形。 這個動作會開啟 hello 時間數列 Insights 總管環境。

    ![連線處理站預先設定的解決方案 TSI 總管][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>檢視關鍵效能指標

hello 解決方案提供兩個關鍵效能指標，*每小時的單位*和*能源使用 kwh*。

![連線處理站預先設定的解決方案 KPI][cf-img-kpi]

1. 每個小時或用於 hello 階層中的任何層級的能源 tooview 單位瀏覽 toohello 您需要的特定檢視。 hello 單位，每個小時和能源使用顯示在 [hello] 面板。

2. 每個小時或用於進一步，hello 階層中的任何層級的能源 tooanalyze 單位按一下 hello 量測計中 hello**關鍵效能指標**面板。 內容面板隨即出現，並讓您從 hello 過去一小時、 過去 24 小時，以及過去 7 天的 hello tooview 資料的時間序列 Insights 電源視覺效果。

## <a name="scenario-review"></a>案例檢閱

在此案例中，您可以監視您處理站 OEE 和 Kpi 的值，hello 儀表板中。 您則用於時間序列 Insights tooprovide 詳細資訊 toohelp 鑽研進一步 hello 遙測資料 OEE 和 Kpi toohelp 以偵測異常狀況。 您也會與您處理站使用 hello 警示面板 tooview 問題，而且您使用 hello 動作可用 tooyou tooresolve hello 警示。

## <a name="other-features"></a>其他功能

hello 下列各節說明一些其他功能 hello 連接工廠解決方案的 hello 前一個案例中未描述。

## <a name="apply-filters"></a>套用篩選條件

1. 按一下 hello **> 形箭號**toodisplay hello factory 位置面板或 hello 警示面板中可用的篩選器的清單。

2. hello 篩選面板會顯示您。 

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter]

3. 選擇您需要的 hello 篩選器。 它也是可能 tootype hello 篩選欄位中的任意文字。

4. 然後您套用 hello 篩選。 漏斗圖，顯示 hello 工廠中並且會提醒資料表透過 hello 儀表板中，也會顯示 hello 篩選狀態。

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter-funnel]

    > [!NOTE]
    > 使用中的篩選器不會影響顯示 hello OEE 和 KPI 的值，它只篩選 hello 列出內容。

5. tooclear 篩選中，按一下 hello 漏斗圖，然後按一下 hello 篩選內容面板中的篩選器。 hello 文字**所有**會顯示在 hello 處理站，並發出警示的資料表。

## <a name="browse-an-opc-ua-server"></a>瀏覽 OPC UA 伺服器

當您部署預先設定的 hello 方案時，您會自動佈建模擬的 OPC UA 伺服器，您可以透過 hello 方案瀏覽器瀏覽。 這些伺服器是「模擬的 OPC UA 伺服器」。 模擬的伺服器輕易地為您 tooexperiment 與 hello 預先設定的方案而無須與 hello 需要 toodeploy 真正的實體伺服器。 如果您想 tooconnect 真實世界的 OPC UA 伺服器 toohello 解決方案，請參閱 hello[連接 OPC UA 裝置連線的 toohello 預先設定的處理站解決方案][ lnk-connect-cf]教學課程。

1. 按一下 hello **factory 圖示**hello 儀表板導覽列中。

    ![連線處理站預先設定的解決方案伺服器瀏覽器][cf-img-server-browser]

2. 從 hello 預先設定的清單中選擇其中一個 hello 伺服器。 此清單會顯示為您部署預先設定的 hello 方案中的 hello 伺服器。

    ![連線處理站預先設定的解決方案伺服器選取][cf-img-server-choice]

3. 按一下 [連線]，[安全性] 對話方塊隨即顯示。 Hello 模擬對於安全 tooclick**繼續**

4. tooexpand hello 節點 hello 伺服器樹狀目錄中，按一下它。 正在發佈遙測的節點旁邊有勾號。

    ![連線處理站預先設定的解決方案伺服器樹狀目錄][cf-img-server-tree]

5. 以滑鼠右鍵按一下項目 tooread、 撰寫、 發行或呼叫該節點。 hello 動作可用 tooyou 取決於您的權限和 hello 節點的 hello 屬性。 hello 讀取選項 toodisplays 內容面板顯示 hello 的 hello 特定節點的值。 hello 撰寫選項顯示的內容面板，您可以在此輸入新值。 hello 呼叫選項可顯示的節點，您可以在其中輸入 hello 呼叫 hello 參數。

## <a name="publish-a-node"></a>發佈節點

當您瀏覽*模擬的 OPC UA 伺服器*，您也可以選擇 toopublish 新節點。 您可以分析這些節點 hello 方案中的 hello 遙測。 這些*模擬 OPC UA 伺服器*讓它與 hello 預先設定的解決方案容易 tooexperiment 而不需部署實際的實體裝置。

1. 瀏覽 tooa hello 想 toopublish 的 OPC UA 伺服器瀏覽器樹狀目錄中的節點。

2. 以滑鼠右鍵按一下 hello 節點。

3. 選擇 [發佈]。

    ![連線的處理站發佈節點][cf-img-publish-node]

4. 這會告訴您 hello 發行內容面板會顯示已成功。 hello 節點會出現在它旁邊的核取記號 hello 站台層級檢視。

    ![連線處理站預先設定的解決方案發佈成功][cf-img-publish-success]

## <a name="command-and-control"></a>命令與控制

命令，並控制您直接從 hello 雲端的業界裝置，可讓 hello 連線的 factory。 您可以使用此功能 toorespond tooalerts hello 裝置所產生。 例如，您可以傳送命令 toohello 裝置從 hello 雲端。 您可以找到 hello 可用命令 hello **StationCommands** hello OPC UA 伺服器瀏覽器樹狀目錄中的節點。 在此案例中，您可以開啟不足的壓力發行閥 hello 生產環境中的行慕尼黑的組件站台上。 toouse hello 命令和控制功能，您必須在 hello**管理員**hello 角色預先設定的方案部署。

1. 瀏覽 toohello **StationCommands** hello OPC UA 伺服器瀏覽器樹狀目錄中的節點。

2. 選擇您想使用 hello 命令。

3. 以滑鼠右鍵按一下 hello 節點。

4. 選擇 [呼叫]。

    ![連線處理站預先設定的解決方案呼叫命令][cf-img-call-command]

5. 內容面板會出現告知您哪一種方法您即將 toocall 和任何參數的詳細資料不適用。

6. 選擇 [呼叫]。

    ![連線處理站預先設定的解決方案呼叫內容][cf-img-call-context]

7. hello 內容面板會更新的 tooinform 您 hello 方法呼叫成功。 您可以確認 hello 呼叫成功讀取 hello hello 不足的壓力節點更新 hello 呼叫的結果值。

    ![連線處理站預先設定的解決方案呼叫成功][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Hello 幕後

當您部署預先設定的解決方案時，hello 部署程序會在 hello 您選取的 Azure 訂用帳戶中建立多個資源。 您可以檢視這些資源中 hello Azure[入口網站][lnk-portal]。 hello 部署程序會建立**資源群組**根據您選擇您預先設定的解決方案 hello 名稱的名稱：

![Hello Azure 入口網站中預先設定的解決方案][img-cf-portal]

您可以檢視每個資源的 hello 設定 hello 資源群組中的 hello 清單中選取。

您也可以檢視預先設定的 hello 方案 hello 原始程式碼。 hello 預先設定連接的工廠方案原始程式碼處於 hello [azure-iot-連線-原廠][ lnk-cfgithub] GitHub 儲存機制：

完成之後，您可以從您的 Azure 訂閱 hello 上刪除 hello 預先設定的解決方案[azureiotsuite.com] [ lnk-azureiotsuite]站台。 此站台可讓您 tooeasily 刪除所有 hello 當您建立預先設定的 hello 方案已佈建的資源。

> [!NOTE]
> 刪除所有項目 tooensure 相關 toohello 預先設定的解決方案，刪除上 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台。 請勿刪除 hello hello 入口網站中的資源群組。

## <a name="next-steps"></a>後續步驟

既然您已部署預先設定的有效的解決方案，您可以繼續閱讀下列文章 hello 入門 IoT 套件：

* [連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]
* [連接裝置 toohello 預先設定連接的工廠解決方案][lnk-connect-cf]
* [Hello azureiotsuite.com 網站的權限][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md