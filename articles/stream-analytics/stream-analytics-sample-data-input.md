---
title: "在 Azure Stream Analytics aaa 取樣輸入 |Microsoft 文件"
description: "針對串流分析作業進行移難排解時精準找出問題。"
keywords: "對輸入進行疑難排解、輸入取樣"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a>Azure 資料流分析輸入串流的取樣

藉由使用 Azure Stream Analytics 中，您可以取樣輸入的事件來自檔案並測試 hello 入口網站中的查詢，而不需要 toostart 或停止的作業。

## <a name="testing-your-query"></a>測試查詢

在 hello 資料流分析工作詳細資料窗格中，開啟 hello**查詢編輯器**刀鋒視窗中按一下底下的 hello 查詢名稱**查詢**。 (在我們的範例案例，因為尚未建立任何查詢，按一下 hello **< >**預留位置。)

![hello 資料流分析查詢編輯器](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

hello 先前版本中，會顯示 hello 豐富編輯器刀鋒視窗中建立您的查詢。 現在已使用新的更新 hello 刀鋒視窗左窗格中，該顯示 hello 輸入和輸出 hello 查詢所使用且定義為此工作。

![hello 資料流分析查詢編輯器中輸入及輸出 清單](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

此外也會顯示尚未定義的其他一組輸入與輸出。 這些是來自 hello 新的查詢範本您開始使用。 這些變更，或甚至就會完全消失，當您編輯 hello 查詢。 您目前可以放心地忽略這組輸入與輸出。

tootest 範例輸入資料，與任何輸入，以滑鼠右鍵按一下，然後選取**從檔案的範例資料上傳**。

![hello 資料流分析查詢編輯器 上傳的範例資料檔案命令](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

Hello 上傳完成後，按一下**測試**tootest hello 針對此查詢範例您剛才提供的資料。

![hello 資料流分析查詢編輯器 [測試] 按鈕](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

如果您想要稍後使用 toosave hello 測試輸出，hello 查詢的輸出會顯示在 hello 瀏覽器連結 toohello 下載的結果中。 您現在可以輕鬆並反覆地修改查詢並測試它重複 toosee hello 輸出如何變更。

![串流分析查詢編輯器樣本輸出](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

在上述映像的 hello，已加入第二個輸出，稱為**HighAvgTempOutput**。

當您在查詢中使用多個輸出時，您可以查看每個輸出的 hello 結果分別，且兩者之間輕鬆切換。

您滿意 hello 結果之後，您可以儲存您的查詢、 啟動您的工作、 耐心及監看的資料流分析的 hello 魔力。

## <a name="get-help"></a>取得說明

如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
