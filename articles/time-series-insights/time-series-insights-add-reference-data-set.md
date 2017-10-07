---
title: "aaaAdd 參考資料集 tooyour Azure 時間數列 Insights 環境 |Microsoft 文件"
description: "在本教學課程中，您會新增參考資料集 tooyour 時間數列 Insights 環境"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>建立時間序列 Insights 環境使用 hello Ibiza 入口網站參考資料集

參考資料集是會夾帶 hello 事件來自事件來源的項目集合。 Time Series Insights 輸入引擎會將事件來源的事件和參考資料集中的項目聯結在一起。 然後此增強的事件可用於查詢。 這項聯結根據參考資料集中定義的 hello 索引鍵。

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>步驟 tooadd 參考資料集 tooyour 環境

1. 登入 toohello [Ibiza 入口網站](https://portal.azure.com)。
2. 按一下 [所有資源] 功能表中的 hello 左邊 hello hello Ibiza 入口網站。
3. 選取 Time Series Insights 環境。

    ![建立 hello 時間數列 Insights 參考資料集](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. 選取 [參考資料集]，並按一下 [+ 新增]。

    ![建立 hello 時間數列 Insights 參考資料集詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. 指定 hello hello 參考資料集名稱。
6. 指定 hello 索引鍵名稱和型別。 這個名稱和型別是使用的 toopick hello 正確屬性從事件來源中的 hello 事件。 比方說，如果您提供為"DeviceId"的索引鍵名稱和類型為 「 字串 」，然後 hello 時間數列 Insights ingress 引擎會尋找具有 hello 名稱"DeviceId"hello 內送事件中的 「 字串 」 類型的屬性。 您可以提供一個以上的索引鍵 toojoin 與 hello 事件。 hello 屬性名稱比對會區分大小寫的。

     ![建立 hello 時間數列 Insights 參考資料集詳細資料](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. 按一下 [建立]。

## <a name="next-steps"></a>後續步驟

* 以程式設計的方式[管理參考資料](time-series-insights-manage-reference-data-csharp.md)。
* Hello 完整的 API 參考，請參閱[參考資料 API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api)文件。
