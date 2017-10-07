---
title: "aaaCreate Azure 記錄分析的自訂儀表板 |Microsoft 文件"
description: "本指南將協助您了解如何記錄分析儀表板可以視覺效果顯示所有儲存的記錄搜尋，提供您單一透鏡 tooview 您的環境。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>建立用於 Log Analytics 中的自訂儀表板

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您無法建立新的儀表板，或編輯現有的儀表板。 

本指南將協助您了解如何記錄分析儀表板可以視覺效果顯示所有儲存的記錄搜尋，提供您單一透鏡 tooview 您的環境。

![範例儀表板](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

所有 hello 自訂儀表板，您建立 hello OMS 入口網站中也都可用於 hello OMS 行動應用程式。 Hello 遵循頁面 hello 應用程式的詳細資訊，請參閱。

* [OMS hello Microsoft Store 從行動裝置應用程式](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Apple iTunes 中的 OMS 行動應用程式](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![行動儀表板](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>如何建立儀表板？
toobegin 移 toohello OMS 概觀頁面。 您會看到 hello**我的儀表板**hello 左側的方塊。 它 toodrill 向下一直按到您的儀表板。

![概觀](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>新增磚
在儀表板中，磚是由您儲存的記錄搜尋所形成。 OMS 內建許多預先儲存的記錄搜尋，讓您可以隨時開始。 如何使用 hello 下列步驟會該大綱 toobegin。

在 hello 我的儀表板檢視，只要按一下**自訂**tooenter 自訂模式。

![圖示](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 開啟右邊 hello hello 頁面 hello 面板會顯示所有您的工作區儲存的記錄搜尋。 toovisualize 儲存的記錄搜尋為圖格，將滑鼠停留在儲存的搜尋，然後按一下hello**加上**符號。

![新增磚 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

當您按一下 hello**加上**符號、 新的磚會出現在 hello 我的儀表板檢視。

![新增磚 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>編輯磚
在 hello 我的儀表板檢視，只要按一下**自訂**tooenter 自訂模式。 按一下您想要 tooedit hello 磚。 hello 右方面板變更 tooedit，並提供一組選項：

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![編輯磚](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>磚視覺效果
有三種磚視覺效果 toochoose 從：

| 圖表類型 | 作用 |
| --- | --- |
| ![長條圖](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |將已儲存之記錄搜尋結果的時間軸顯示為長條圖，或是依欄位顯示結果清單 (根據您的記錄搜尋是否根據欄位彙總結果而定)。 |
| ![計量](./media/log-analytics-dashboards/oms-dashboards-metric.png) |在圖格中以數字顯示記錄搜尋結果總數。 度量磚可讓您 tooset 就磚發亮顯示 hello 達到 hello 閾值時的臨界值。 |
| ![線條](./media/log-analytics-dashboards/oms-dashboards-line.png) |將已儲存之記錄搜尋結果命中和值的時間軸顯示為折線圖。 |

### <a name="threshold"></a>閾值
您可以使用 hello 度量 」 視覺效果在磚上建立閾值。 選取上 toocreate hello 磚上的臨界值。 選擇是否 toohighlight hello 磚 hello 值高於或低於選擇的 hello 閾值時，然後設定下列 hello 臨界值。

## <a name="organizing-hello-dashboard"></a>組織 hello 儀表板
tooorganize 儀表板，瀏覽 toohello 我的儀表板檢視，然後按一下**自訂**tooenter 自訂模式。 按一下並拖曳您想 toomove，並將其移 toowhere 想磚 toobe hello 磚。

![排列儀表板](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>移除磚
tooremove 磚，請瀏覽 toohello 我的儀表板檢視，然後按一下**自訂**tooenter 自訂模式。 選取 hello 磚 tooremove，然後在 hello 右面板上選取**移除磚**。

![移除磚](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>後續步驟
* 建立[警示](log-analytics-alerts.md)記錄分析 toogenerate 通知和 tooremediate 問題中。
