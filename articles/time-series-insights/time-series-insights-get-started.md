---
title: "aaaCreate Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在本教學課程中，您將學習如何 toocreate 時間數列環境中，將它連接 tooan 事件來源和準備 tooanalyze 事件資料，以分鐘為單位。"
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立新的時間序列 Insights 環境

Time Series Insights 環境是具有輸入和儲存容量的 Azure 資源。 客戶會使用所需的 hello 容量佈建透過 hello Azure 入口網站的環境。

## <a name="steps-toocreate-hello-environment"></a>步驟 toocreate hello 環境

請遵循這些步驟 toocreate 您的環境：

1.  登入 toohello [Azure 入口網站](https://portal.azure.com)。
2.  按一下 hello 加上正負號 （"+"） 中的 hello 左上角。
3.  搜尋 「 時間序列見解"hello [搜尋] 方塊中。

  ![建立 hello 時間數列 Insights 環境](media/get-started/getstarted-create-environment1.png)

4.  選取 [Time Series Insights]，然後按一下 [建立]。

  ![建立 hello 時間數列 Insights 資源群組](media/get-started/getstarted-create-environment2.png)

5.  指定環境名稱。 這個名稱會表示中的 hello 環境[時間數列總管](https://insights.timeseries.azure.com)。
6.  選取一個訂用帳戶。 請選擇包含事件來源的訂用帳戶。 時間序列 Insights 可自動偵測 Azure IoT 中樞，並在現有的事件中樞資源 hello 相同訂用帳戶。
7.  選取或建立資源群組。 資源群組是一起使用之 Azure 資源的集合。
8.  選取裝載位置。 tooavoid 移動資料在資料中心中，選擇包含您的事件來源的位置。
9.  選取定價層。
10. 選取容量。 您可以在環境建立後變更其容量。
11. 建立您的環境。 每當您登入，您也可以釘選環境 toohello 儀表板，以方便存取。

  ![建立 hello 時間數列 Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>後續步驟

* [定義資料存取原則](time-series-insights-data-access.md)tooaccess 您的環境中[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)
* [建立事件來源](time-series-insights-add-event-source.md)
* [傳送事件](time-series-insights-send-events.md)toohello 事件來源
