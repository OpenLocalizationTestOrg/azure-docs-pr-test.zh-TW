---
title: "aaaPredictive 維護預先設定的解決方案 |Microsoft 文件"
description: "Hello Azure IoT 套件預測性維護描述預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>預先設定的預測性維護解決方案概觀

hello*預測性維護*[預先設定的解決方案][ lnk_preconfigured_solutions]是其中一個 hello [Microsoft Azure IoT 套件][ lnk_iot_suite]預先設定的解決方案。 此解決方案應用了 [Azure Machine Learning][lnk-machine-learning]，整合了即時裝置遙測集合與預測模型。

與 Azure IoT 套件，您可以快速並輕鬆地連接 tooand 監視器資產，並分析即時儀表板和視覺效果中的遙測。 在 hello 預測性維護方案中，hello 儀表板和視覺效果提供您新的資訊，磁碟機效率以及增強的營收的資料流。

## <a name="hello-scenario"></a>hello 案例

Fabrikam 是區域性航空公司，而以優惠的價格為客戶提供優良的服務，是該公司努力的目標。 維護問題是造成航班延誤的原因之一，而引擎維護又是其中最為棘手的項目。 Fabrikam 必須避免引擎失敗期間飛行代價，會定期檢查其引擎和排程根據 tooa 計劃的維護。 不過，引擎不一定有的飛機 hello 相同。 所以有一些引擎維護工作並非必要。 但嚴重者若在執行維護工作之前發生問題，可能會造成飛機停飛。 如果位置則飛機其中 hello 右側的技術人員或零件無法使用，這些問題可能會特別是很費時。

Fabrikam 的飛機 hello 引擎已執行檢測與感應器監視期間飛行 engine 狀況。 Fabrikam 使用 hello 預測性維護方案 toocollect hello 感應器資料收集期間 hello 班機。 引擎操作的累積年和之後資料失敗，Fabrikam 的資料科學家有模型化方式 toopredict hello 剩餘的生命週期 (RUL) 飛機引擎。 hello 模型使用中的 hello 引擎感應器四種資料引擎損耗，導致 tooeventual 失敗之間的相互關聯。 當 Fabrikam 繼續 tooperform 規則視察 tooensure 安全時，它現在可以使用 hello 模型 toocompute hello RUL 每個引擎在每個班機之後。 hello 模型使用 hello 遙測 hello 飛行期間收集從 hello 引擎。 Fabrikam 現在已可以預測未來的失敗點，並預先規劃維護及維修計劃。

> [!NOTE]
> hello 解決方案模型會使用實際的引擎損耗資料。

Fabrikam 可以預測 hello 點，需要維護時，最佳化其操作 tooreduce 成本。

維護協調者會使用排程器︰

- 計劃維護 toocoincide 飛機停止的特定位置。
- 確定有足夠的時間而不會造成排程中斷是供 hello 飛機 toobe 停止服務。
- tooschedule 技術人員 tooensure 飛機會有效率地服務，不含等候時間。

庫存控制管理員因為會收到維護計畫，所以可以據此最佳化其訂單程序與備用零件庫存。

這些活動啟用 Fabrikam toominimize 飛機地面時間並降低作業成本，同時確保乘客和團隊 hello 安全。

toounderstand 如何[Azure IoT 套件][ lnk_iot_suite]提供 hello 功能客戶需要 toorealize hello 可能的預測性維護，請檢閱這[資訊圖][lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>如何建置 hello 預測性維護方案

hello 解決方案會使用現有的 Azure 機器學習模型提供作為範本 tooshow 從裝置透過 IoT 套件服務所收集的遙測使用這些功能。 Microsoft 已建[迴歸模型][ lnk_regression_model]飛機引擎可公開可用的資料為基礎的<sup>\[1\]</sup>，並逐步指引 toouse hello 模型的方式。

hello Azure IoT 預測性維護方案會使用此範本所建立的 hello 迴歸模型。 hello 模型是部署到您的 Azure 訂用帳戶，並透過自動產生的 API 公開。 hello 解決方案包含測試資料表示 （的總計 100) 4 hello 子集引擎和 hello 4 （的總 21) 感應器資料流。 此資料是足夠 tooprovide 精確的結果從 hello 定型的模型。

*\[1\] A. Saxena and K. Goebel (2008)。《渦輪風扇發動機性能下降模擬資料集》(Turbofan Engine Degradation Simulation Data Set)，NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>開始使用預測性維護

本教學課程會示範如何 tooprovision hello 預測性維護方案。 它會引導您完成 hello 預測性維護方案 hello 基本功能。 您可以存取這些功能透過 hello 方案儀表板與 hello 預先設定的方案一起部署。

toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。

> [!NOTE]
> 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。

1. 登入太[azureiotsuite.com] [ lnk-azureiotsuite]使用您的 Azure 帳戶的認證，再按一下 **+**  toocreate 方案。
1. 按一下**選取**hello**預測性維護**磚。
1. 輸入預先設定的預測性維護解決方案的 [解決方案名稱]。
1. 選取 hello**區域**和**訂用帳戶**希望 toouse tooprovision hello 方案。
1. 按一下**建立方案**toobegin hello 佈建程序。 這個程序通常需要幾分鐘的時間 toorun。

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>等候佈建程序 toocomplete hello

1. 按一下具有您方案的 hello 磚**佈建**狀態。
1. 請注意 hello**佈建狀態**您 Azure 訂用帳戶中部署 Azure 服務。
1. 佈建完成之後，hello 狀態變更太**準備**。
1. 按一下您的方案在 hello 右窗格中的 hello 磚 toosee hello 詳細資料。 從這個窗格中，您可以啟動 hello 方案儀表板和存取 hello Machine Learning 工作區。

> [!NOTE]
> 如果您遇到部署預先設定的 hello 解決方案的問題，請檢閱[hello azureiotsuite.com 網站的權限][ lnk-permissions]和 hello[常見問題集][ lnk-faq]. 如果 hello 問題仍然存在，則在 hello 上建立服務票證[入口網站][lnk-portal]。

有 toosee 如預期般詳細資料，未列出您的解決方案嗎？ 請在 [使用者心聲](https://feedback.azure.com/forums/321918-azure-iot)中提供功能建議給我們。

## <a name="view-hello-solution"></a>檢視 hello 方案

本節會引導您完成 hello 方案 UI。

### <a name="predictive-maintenance-dashboard"></a>預測性維護儀表板

此頁面 hello web 應用程式中的使用 PowerBI JavaScript 控制項 (請參閱 hello [PowerBI 視覺效果儲存機制][lnk-powerbi]) toovisualize:

* hello hello blob 儲存體中的資料流分析工作的輸出資料。
* hello RUL 和循環計數每飛機引擎。

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>觀察 hello 雲端解決方案的 hello 行為

在 hello Azure 入口網站中瀏覽 toohello 資源群組 hello 方案名稱與您選擇 tooview 佈建的資源。

![][img-resource-group]

當您佈建 hello 預先設定的方案時，您會收到含有連結 toohello Machine Learning 工作區的電子郵件。 您也可以導覽 toohello Machine Learning 工作區，從 hello [azureiotsuite.com] [ lnk-azureiotsuite]頁面為您佈建的方案。 圖格時，此頁面提供 hello 方案是在 hello**準備**狀態。

![][img-machine-learning]

在 hello 方案入口網站中，您可以看到該 hello 範例使用四個模擬的裝置 toorepresent 兩個飛機佈建與每個飛機各有四個感應器的兩個引擎。 當您第一次瀏覽 toohello 方案入口網站時，就會停止 hello 模擬。

![][img-simulation-stopped]

按一下**開始模擬**toobegin hello 模擬。 hello 感應器歷程記錄、 RUL、 週期和 RUL 記錄填入 hello 儀表板。

![][img-simulation-running]

當 RUL 小於 160 （選擇供示範之用的任意臨界值），hello 方案入口網站會顯示 RUL 顯示警告的符號 下一步 toohello。 hello 方案入口網站也會反白顯示黃色 hello 飛機引擎。 請注意，hello RUL 值需要一般向下趨勢整體，但通常 toobounce 向上和向下。 這個行為會因各種週期長度 hello 和 hello 模型精確度。

![][img-simulation-warning]

hello 完整模擬會大約 35 分鐘 toocomplete 148 循環。 第一個大約 5 分鐘的時間達到 hello 160 RUL 門檻 hello 和這兩個引擎叫用 hello 臨界值，約 8 分鐘。

hello 模擬執行透過 hello 完整資料集 148 循環，settles 最終 RUL 和週期的值。

您可以停止 hello 模擬在任何點，但按一下**開始模擬**重新執行 hello 模擬從 hello 開始 hello 資料集。

## <a name="next-steps"></a>後續步驟

深入了解 Azure IoT 如何讓預測性維護的情況下，讀取 toolearn[擷取值從 hello 物聯網][lnk_capture_value]。

採取[逐步解說][ lnk-predictive-walkthrough]的 hello 預測性維護方案。

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [IoT 套件的常見問題集][lnk-faq]
* [從 hello 接地 IoT 安全性][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/