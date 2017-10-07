---
title: "aaaPredict vehicle 健全狀況和驅動習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>車輛遙測分析解決方案腳本
這**功能表**連結 toohello 章節，在這個腳本中的。 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>概觀
超級電腦都移出 hello 實驗室，而且現在會保存在我們機庫 ！ 這些尖端汽車包含各種感應器，提供它們 hello 能力 tootrack 和監視每秒數以百萬計的事件。 我們預期的由 2020，大部分的這些車輛將已經連接的 toohello 網際網路。 想像一下接通這些豐富的資料 tooprovide 更安全、 可靠性及驅動更好的體驗 ！ Microsoft 透過 Cortana Intelligence 讓此一美好想像成真。

Microsoft 的 Cortana 智慧是完全受管理的巨量資料，並為智慧型動作 advanced analytics suite，可讓您 tootransform 您的資料。 我們希望 toointroduce toohello Cortana 智慧 Vehicle 遙測分析方案範本。 這個解決方案示範了如何汽車經銷商、 汽車的製造商和保險的公司可以使用 Cortana 智慧 toogain 即時 hello 功能及預測的洞察能力 vehicle 健全狀況和驅動習慣。 

hello 方案會實作為[lambda 架構模式](https://en.wikipedia.org/wiki/Lambda_architecture)顯示 hello 潛力 hello Cortana 智慧平台的即時和批次處理。 hello 解決方案： 

* 提供車輛遠程資訊服務模擬器
* 運用事件中樞，以將數百萬計的模擬車輛遙測事件擷取至 Azure 
* 使用資料流分析 toogain 即時 insights vehicle 健全狀況
* hello 資料保存到更豐富的批次分析的長期的儲存體。 
* 利用機器學習中的異常偵測的即時和批次處理處理 toogain 預測深入資訊。
* 會利用在標尺和 Data Factory toohandle 協調流程、 排程、 資源管理及監視 hello 批次處理管線的 HDInsight tootransform 資料 
* 使用 Power BI 為此解決方案提供一個豐富的儀表板，來提供即時資料和預測性分析視覺效果

## <a name="architecture"></a>架構
![解決方案架構圖表](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*圖 1 – 車輛遙測分析解決方案架構*

此解決方案包括 hello 下列**Cortana 智慧元件**並展示其結束 tooend 整合：

* **事件中樞** 可將數百萬計的車輛遙測事件擷取至 Azure。
* **串流分析** 」可取得關於車輛健全狀態的即時情資，同時以長期儲存的方式保存這些資料，供日後進行更豐富廣泛的批次分析之用。
* **機器學習**以便進行異常偵測即時和批次處理 toogain 預測的深入資訊。
* **HDInsight**運用 tootransform 大規模的資料
* **Data Factory**處理協調流程排程、 資源管理和監視 hello 批次處理管線。
* **Power BI** 為此解決方案提供具備即時資料與預測性分析視覺效果等豐富功能的儀表板。

此解決方案可存取兩種不同的 **資料來源**： 

* **模擬 vehicle 訊號和診斷**: vehicle 車用通訊模擬器會發出診斷資訊，並對應 toohello 狀態 hello vehicle 和 hello 推動特定時點的模式，時間的訊號。 
* **一種載具，目錄**： 包含 VIN toomodel 對應的參考資料集。

