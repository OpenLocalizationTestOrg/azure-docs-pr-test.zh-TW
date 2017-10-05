---
title: "建立 Azure Time Series Insights 環境 | Microsoft Docs"
description: "在本教學課程中，您將了解如何迅速建立時間序列環境、將它連線到事件來源，以及做好準備以分析事件資料。"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a>在 Azure 入口網站中建立新的 Time Series Insights 環境

Time Series Insights 環境是具有輸入和儲存容量的 Azure 資源。 客戶需透過 Azure 入口網站來佈建環境和所需容量。

## <a name="steps-to-create-the-environment"></a>用以建立環境的步驟

請遵循下列步驟來建立環境：

1.  登入 [Azure 入口網站](https://portal.azure.com)。
2.  按一下左上角的加號 (“+”)。
3.  在搜尋方塊中搜尋「Time Series Insights」。

  ![建立 Time Series Insights 環境](media/get-started/getstarted-create-environment1.png)

4.  選取 [Time Series Insights]，然後按一下 [建立]。

  ![建立 Time Series Insights 資源群組](media/get-started/getstarted-create-environment2.png)

5.  指定環境名稱。 此名稱會代表[時間序列總管](https://insights.timeseries.azure.com)中的環境。
6.  選取一個訂用帳戶。 請選擇包含事件來源的訂用帳戶。 Time Series Insights 可以自動偵測相同訂用帳戶中現有的 Azure IoT 中樞與事件中樞資源。
7.  選取或建立資源群組。 資源群組是一起使用之 Azure 資源的集合。
8.  選取裝載位置。 若要避免在資料中心之間移動資料，請選擇事件來源所在的位置。
9.  選取定價層。
10. 選取容量。 您可以在環境建立後變更其容量。
11. 建立您的環境。 您也可以將環境釘選到儀表板，以方便在登入時存取。

  ![建立 Time Series Insights [釘選到儀表板]](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>後續步驟

* [定義資料存取原則](time-series-insights-data-access.md)以在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中存取您的環境
* [建立事件來源](time-series-insights-add-event-source.md)
* [將事件傳送](time-series-insights-send-events.md)到事件來源
