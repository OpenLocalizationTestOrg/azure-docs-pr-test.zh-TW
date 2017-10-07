---
title: "在 Azure CDN aaaReal 時間統計資料 |Microsoft 文件"
description: "傳遞內容 tooyour 用戶端時，即時統計資料會提供 Azure CDN 的 hello 效能的即時資料。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Microsoft Azure CDN 中的即時統計資料
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overview
本文件說明 Microsoft Azure CDN 中的即時統計資料。  這項功能提供即時的資料，例如頻寬、 快取狀態和並行連接 tooyour CDN 設定檔傳遞內容 tooyour 用戶端時。 這可讓在任何時間，包括移至即時事件的 hello 健全狀況服務的持續監視。

下列圖表中的 hello 可用：

* [頻寬](#bandwidth)
* [狀態碼](#status-codes)
* [快取狀態](#cache-statuses)
* [連線](#connections)

## <a name="accessing-real-time-stats"></a>存取即時統計資料
1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。
   
    ![CDN 設定檔刀鋒視窗](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
3. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**即時統計資料**彈出式視窗。  按一下 [HTTP 大型物件] 。
   
    ![CDN 管理入口網站](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    hello 即時統計資料圖形會顯示。

每個 hello 圖形會顯示 hello 選取時間範圍內，hello 網頁載入時啟動的即時統計資料。  hello 圖形會自動更新每隔幾秒。  hello**重新整理圖形**按鈕時，如果有的話，將會清除 hello 圖形中，其後它只會顯示 hello 選取資料。

## <a name="bandwidth"></a>頻寬
![頻寬圖表](./media/cdn-real-time-stats/cdn-bandwidth.png)

hello**頻寬**圖表顯示 hello 量 hello 目前平台透過 hello 選取時間範圍所用的頻寬。 hello 陰影的一部分 hello 圖形表示頻寬使用量。 hello 目前正在使用的頻寬數量確實會顯示 hello 折線圖的正下方。

## <a name="status-codes"></a>狀態碼
![狀態碼圖表](./media/cdn-real-time-stats/cdn-status-codes.png)

hello**狀態碼**圖形表示透過 hello 選取時間範圍中發生特定 HTTP 回應碼的頻率。

> [!TIP]
> 如需每個 HTTP 狀態碼選項的說明，請參閱 [Azure CDN HTTP 狀態碼](https://msdn.microsoft.com/library/mt759238.aspx)。
> 
> 

HTTP 狀態碼的清單會顯示 hello 圖形上方的直接。 這份清單表示可以包含在 hello 折線圖和 hello 目前發生次數的每秒該狀態碼的每個狀態碼。 根據預設，一條線會顯示每個這些 hello 圖形中的狀態碼。 不過，您可以選擇 tooonly 有特殊意義，您的 CDN 組態的監視 hello 狀態碼。 toodo，檢查所需的 hello 狀態碼和清除所有其他選項]，然後按 [**重新整理圖形**。 

您可以暫時隱藏特定狀態碼的記錄資料。  從 hello 圖例 hello 圖形正下方，按一下您想要 toohide hello 狀態碼。 hello 狀態碼將會立即隱藏 hello 圖形中。 再次按一下該狀態碼將會再次顯示該選項 toobe。

## <a name="cache-statuses"></a>快取狀態
![快取狀態圖表](./media/cdn-real-time-stats/cdn-cache-status.png)

hello**快取狀態**圖形表示透過 hello 選取時間範圍中發生特定類型的快取狀態的頻率。 

> [!TIP]
> 如需每個快取狀態碼選項的說明，請參閱 [Azure CDN 快取狀態碼](https://msdn.microsoft.com/library/mt759237.aspx)。
> 
> 

快取的狀態碼清單會顯示 hello 圖形上方的直接。 這份清單表示可以包含在 hello 折線圖和 hello 目前發生次數的每秒該狀態碼的每個狀態碼。 根據預設，一條線會顯示每個這些 hello 圖形中的狀態碼。 不過，您可以選擇 tooonly 有特殊意義，您的 CDN 組態的監視 hello 狀態碼。 toodo，檢查所需的 hello 狀態碼和清除所有其他選項]，然後按 [**重新整理圖形**。 

您可以暫時隱藏特定狀態碼的記錄資料。  從 hello 圖例 hello 圖形正下方，按一下您想要 toohide hello 狀態碼。 hello 狀態碼將會立即隱藏 hello 圖形中。 再次按一下該狀態碼將會再次顯示該選項 toobe。

## <a name="connections"></a>連線
![連線圖表](./media/cdn-real-time-stats/cdn-connections.png)

此圖表指出多少的連線已建立的 tooyour 邊緣伺服器。 通過 CDN 的每個資產要求都會導致建立一個連線。

## <a name="next-steps"></a>後續步驟
* 透過 [Azure CDN 中的即時警示](cdn-real-time-alerts.md)
* 進一步了解 [進階 HTTP 報告](cdn-advanced-http-reports.md)
* 分析 [使用模式](cdn-analyze-usage-patterns.md)

