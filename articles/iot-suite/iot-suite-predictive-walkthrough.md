---
title: "aaaPredictive 維護逐步解說 |Microsoft 文件"
description: "逐步解說中的 hello Azure IoT 預測性維護預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>預先設定的預測性維護解決方案逐步解說

hello 預先設定的預測性維護方案是預測 hello 點失敗時可能 toooccur 商務案例的端對端解決方案。 您可以針對最佳化維護等活動，主動使用此預先設定的解決方案。 hello 解決方案結合索引鍵的 Azure IoT 套件服務，例如 IoT 中樞，串流分析和[Azure Machine Learning] [ lnk-machine-learning]工作區。 此工作區包含公用的範例資料集，toopredict hello 剩餘的生命週期 (RUL) 飛機引擎為基礎的模型。 hello 方案完整實作做為您 tooplan 起點 hello IoT 商務案例，並實作符合特定的業務需求的解決方案。

## <a name="logical-architecture"></a>邏輯架構

下列圖表中的 hello 概述 hello 邏輯解決方案元件的預先設定的 hello:

![][img-architecture]

hello 藍色項目是在 hello hello 預先設定方案的部署所在的地區中佈建的 Azure 服務。 hello 您可以在其中部署預先設定的 hello 方案的地區清單會顯示 hello[佈建頁面][lnk-azureiotsuite]。

hello 綠色項目是模擬的裝置，表示飛機引擎。 您可以深入了解這些模擬的裝置 hello 下列區段中。

hello 灰色項目代表可實作元件*裝置管理*功能。 hello hello 預先設定的預測性維護方案目前版本不會提供這些資源。 toolearn 有關裝置管理的詳細資訊，請參閱 toohello[遠端監視預先設定的解決方案][lnk-remote-monitoring]。

## <a name="simulated-devices"></a>模擬的裝置

在預先設定的 hello 解決方案中，模擬的裝置會表示飛機引擎。 hello 方案會使用兩個引擎對應 tooa 單一飛機佈建。 每個引擎會發出四種類型的遙測： 感應器 9、 感應器 11、 感應器 14 和 15 感應器提供 hello 機器學習模型 toocalculate hello RUL hello 引擎所需的 hello 資料。 每個模擬的裝置會傳送下列遙測訊息 tooIoT 中樞 hello:

*週期計數*。 週期表示已完成持續期間介於 2 小時與 10 小時之間的飛行。 Hello 飛行期間擷取每隔半小時遙測資料。

*遙測*。 有四個代表引擎屬性的感應器。 hello 感應器以一般方式標示為感應器 9、 感應器 11、 感應器 14 和 15 感應器。 這些四個感應器從 hello RUL 模型代表遙測足夠 tooobtain 有用的結果。 使用預先設定的 hello 方案中的 hello model 是從公用的資料集，其中包含實際的引擎感應器資料建立。 如需有關如何從原始資料集 hello hello 模型的建立方式的詳細資訊，請參閱 hello [Cortana 智慧組件庫預測維護範本][lnk-cortana-analytics]。

hello 模擬裝置可以處理下列命令從 hello 方案中的 hello IoT 中樞傳送的 hello:

| 命令 | 說明 |
| --- | --- |
| StartTelemetry |控制項 hello hello 模擬的狀態。<br/>啟動 hello 裝置傳送遙測 |
| StopTelemetry |控制項 hello hello 模擬的狀態。<br/>停駐點 hello 裝置傳送遙測 |

IoT 中樞會提供裝置命令通知。

## <a name="azure-stream-analytics-job"></a>Azure 串流分析作業

**作業： 遙測**運作 hello 傳入裝置遙測資料流上使用兩個陳述式：

* hello 第一次從 hello 裝置會選取所有的遙測資料，並傳送這個資料 tooblob 儲存體。 從這裡開始，它會視覺化在 hello web 應用程式。
* 平均感應器值兩分鐘的滑動視窗之上，並且傳送嗨事件中樞 tooan 透過此資料，第二個會計算 hello**事件處理器**。

## <a name="event-processor"></a>事件處理器
hello**事件處理器主機**Azure Web 工作中執行。 hello**事件處理器**hello 平均感應器值所需完成的循環。 接著，將這些值 tooan 引擎，定型的模型 toocalculate hello RUL 公開 （expose) 的 API。 hello API 公開 Machine Learning 工作區佈建為 hello 方案的一部分。

## <a name="machine-learning"></a>機器學習服務
hello 機器學習服務元件會使用衍生自真實飛機引擎從收集的資料模型。 您可以瀏覽 toohello Machine Learning 工作區，從上 hello hello 磚[azureiotsuite.com] [ lnk-azureiotsuite]頁面為您佈建的方案。 hello 磚時，使用 hello 方案是在 hello**準備**狀態。


## <a name="next-steps"></a>後續步驟
現在您已看過 hello 的 hello 預先設定的預測性維護方案的重要元件，您可能會想 toocustomize 它。 請參閱[自訂預先設定的解決方案指引][lnk-customize]。

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [IoT 套件的常見問題集][lnk-faq]
* [從 hello 接地 IoT 安全性][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/