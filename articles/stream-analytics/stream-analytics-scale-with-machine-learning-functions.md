---
title: "調整 Azure Stream Analytics & AzureML 函式的 aaaJob |Microsoft 文件"
description: "了解如何 tooproperly 調整串流分析工作 （資料分割、 SU 數量等等） 時使用 Azure Machine Learning 函式。"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>使用 Azure Machine Learning 函式調整串流分析作業
它通常是相當簡單 tooset 組成資料流分析工作，並透過它來執行一些範例資料。 我們該怎麼當我們需要 toorun hello 相同作業且較高的資料磁碟區？ 我們必須的 toounderstand tooconfigure hello 資料流分析工作，讓它將擴充的方式。 在本文件中，我們將著重在 hello 特殊層面調整資料流分析機器學習服務函式的作業。 如需有關如何 tooscale 串流分析工作的一般請參閱 hello 發行項詳細[工作調整](stream-analytics-scale-jobs.md)。

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>什麼是串流分析中的 Azure Machine Learning 函式？
在 Stream Analytics 中的機器學習服務函式可以當成一般函式中呼叫 hello 串流分析查詢語言。 不過，後面 hello 場景 hello 函式呼叫會實際 Azure Machine Learning Web 服務要求。 機器學習 web 服務支援 「 批次處理 「 多個資料列，也就所謂的迷你批次、 在 hello 相同 web 服務應用程式開發介面呼叫，tooimprove 整體輸送量。 請參閱下列文章中的更多詳細資料; hello[Azure Machine Learning 函式在 Stream Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/)和[Azure 機器學習 Web 服務](../machine-learning/machine-learning-consume-web-services.md)。

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>使用 Machine Learning 函式設定串流分析作業
在設定資料流分析工作的機器學習服務函式時，有兩個參數 tooconsider、 hello 批次大小 hello 機器學習服務函式呼叫，以及資料流單位 (SUs) 佈建的 hello 資料流分析工作的 hello。 toodetermine hello 適當的值為這些第一次必須決定之間延遲和輸送量，也就是延遲 hello 資料流分析作業，以及每個 SU 的輸送量。 SUs 可能都必須加入 tooa 作業 tooincrease 輸送量妥善分割資料流分析查詢時，雖然其他 SUs 增加執行中的 hello 作業 hello 成本。

因此是很重要的 toodetermine hello*容錯*的中執行資料流分析工作的延遲。 從執行中的 Azure 機器學習服務要求額外的延遲時間自然會以批次大小，將複合 hello hello 資料流分析作業的延遲增加。 Hello 換句話說，批次的大小增加可讓 hello 資料流分析工作 tooprocess * 更多的事件，以 hello*相同號碼*機器學習 web 服務要求。 通常 hello 增加的機器學習 web 服務延遲是子線性 toohello 批次大小增加，因此很重要的 tooconsider hello 最符合成本效益的批次大小在任何給定的情況下的機器學習 web 服務。 hello 預設批次大小 hello web 服務要求是 1000年，而且可能會修改使用 hello[資料流分析 REST API](https://msdn.microsoft.com/library/mt653706.aspx "資料流分析 REST API")或 hello [PowerShell 用戶端串流分析的](stream-analytics-monitor-and-manage-jobs-use-powershell.md "PowerShell 用戶端的資料流分析")。

尚未決定批次大小，一旦 hello 的數量資料流處理單位 (SUs) 可以是決定，取決於 hello 事件數目 hello 函式需要每秒 tooprocess。 如需串流單位的詳細資訊，請參閱[串流分析調整作業](stream-analytics-scale-jobs.md)。

一般情況下，有 20 個並行連線 toohello 機器學習 web 服務，每隔 6 sus，不同之處在於 1 SU 工作 3 SU 作業會取得和 20 個並行連線也。  比方說，如果 hello 輸入的資料速率是每秒 200,000 事件，並保留 hello 批次大小 1000 hello 產生 web 服務延遲與 1000年事件迷你批次 toohello 預設會是 200 毫秒。 這表示每個連接可以提出 5 toohello 機器學習 web 服務的每秒。 有 20 個連接，hello 資料流分析工作可以處理 20000 事件，在 200 毫秒，因此 100,000 事件每秒。 因此每秒 tooprocess 200,000 事件，hello 資料流分析工作需要 40 的並行連線，推出 too12 SUs。 hello 圖說明從 hello 資料流分析工作 toohello 機器學習 web 服務端點的 hello 要求 – 每隔 6 SUs 在最大值有 20 的並行連線 tooMachine Learning web 服務。

![使用 Machine Learning 函式 2 作業範例調整串流分析](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "使用 Machine Learning 函式 2 作業範例調整串流分析")

一般情況下， ***B***批次大小***L*** hello web 服務以毫秒為單位的批次大小 B 延遲，如 hello 與資料流分析作業的輸送量***N*** SUs 是：

![使用 Machine Learning 函式公式調整串流分析](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "使用 Machine Learning 函式公式調整串流分析")

其他考量可能 hello 'max concurrent calls 5d hello 機器學習 web 服務端上的，建議您 tooset 此 toohello 最大值 (目前 200)。

如需此設定的詳細資訊請參閱 hello[調整文件以取得機器學習 Web 服務](../machine-learning/machine-learning-scaling-webservice.md)。

## <a name="example--sentiment-analysis"></a>範例 – 情感分析
hello 下列範例包含 hello 情緒分析機器學習服務函數，以資料流分析工作 hello 中所述[資料流分析機器學習整合教學課程](stream-analytics-machine-learning-integration-tutorial.md)。

hello 查詢是簡單完全分割的查詢，後面接著 hello**人氣**函式，如下所示：

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

請考慮下列案例; hello輸送量為每秒的 10,000 推文資料流分析工作必須先建立 tooperform 情緒分析的 hello 推文 （事件）。 使用 1 SU，這個資料流分析工作可能無法 toohandle hello 流量？ 使用 hello 預設批次大小 1000 hello 作業應該能夠 tookeep 向上 hello 輸入。 進一步 hello 新增機器學習服務函數應該產生不超過延遲，也就是 hello 一般預設延遲 hello 情緒分析機器學習 web 服務 （與預設批次大小 1000年） 的第二個。 hello 資料流分析工作的**整體**或端對端延遲通常會是幾秒鐘的時間。 納入這個資料流分析工作，更詳細地介紹*特別*hello 機器學習服務函式呼叫。 具有 hello 批次大小為 1000年，10,000 個事件的處理能力需要大約 10 個要求 tooweb 服務。 即使有 1 SU，有足夠的並行連線 tooaccommodate 這個輸入流量。

但如果 hello 輸入的事件速率會增加 100 倍，現在 hello 資料流分析工作需要每秒的 tooprocess 1000000 推文嗎？ 有兩個選項：

1. 增加 hello 批次大小，或
2. 資料分割 hello 輸入資料流 tooprocess hello 事件以平行方式

Hello 第一個選項，與 hello 作業**延遲**會增加。

Hello 第二個選項，就需要 toobe 佈建，因此產生更多的並行的機器學習 web 服務要求詳細 SUs。 這表示 hello 作業**成本**會增加。

假設的 hello 情緒分析機器學習 web 服務的 hello 延遲是 200 毫秒 1000年事件批次或下面 250ms 5000 事件批次，300ms 10000 事件批次或 25000 事件批次的 500ms年。

1. 使用 hello 第一個選項 (**不**佈建更多的 SUs)，可以增加 hello 批次大小太**25000**。 這又會使 hello 作業 tooprocess 1000000 事件與 20 個並行連線 toohello 機器學習 web 服務 （以每個呼叫 500 毫秒的延遲）。 因此 hello hello 資料流分析作業，因為對機器學習 web 服務要求會增加從 hello toohello 人氣函式要求額外的延遲時間**200 毫秒**太**500ms年**。 不過請注意，批次大小**無法**hello Machine Learning web 服務需要的要求中的 hello 承載大小無限增加為 4 MB 或較小 web 服務要求逾時後 100 秒的作業。
2. 使用 hello 第二個選項，hello 批次大小就會留在 1000、 以 web 服務 200 毫秒的延遲表示，每 20 個並行連線 toohello web 服務會是能 tooprocess 1000 * 20 * 5 的事件 = 每秒 100,000。 因此每個第二個，hello 作業 tooprocess 1000000 事件需要 60 SUs。 比較的 toohello 第一個選項，資料流分析工作會讓更多 web 服務的批次要求，接著產生增加的成本。

以下是 hello 輸送量 hello 資料流分析作業的資料表不同 SUs 和批次大小 （以每秒事件數目）。

| 批次大小 (ML 延遲) | 500 (200 毫秒) | 1,000 (200 毫秒) | 5,000 (250 毫秒) | 10,000 (300 毫秒) | 25,000 (500 毫秒) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **3 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **12 SU** |5,000 |10,000 |40,000 |60,000 |100,000 |
| **18 SU** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24 SU** |10,000 |20,000 |80,000 |120,000 |200,000 |
| **…** |… |… |… |… |… |
| **60 SU** |25,000 |50,000 |200,000 |300,000 |500,000 |

現在，您應該已充分了解串流分析中 Machine Learning 函式的運作方式。 您可能也了解從資料來源和 「 提取 」 的 「 提取 」 資料就會傳回批次的事件資料流分析工作 hello 資料流分析工作 tooprocess。 提取模式如何影響 hello 機器學習 web 服務要求？

一般來說，hello 批次大小，我們設定機器學習服務函式將完全無法整除 hello 傳回每個資料流分析工作 「 提取 」 的事件數目。 當發生這種情況 hello 機器學習 web 服務用來呼叫 「 部分 」 的批次。 這是 toonot 帶來額外負荷中從提取 toopull 聯合事件的其他作業延遲。

## <a name="new-function-related-monitoring-metrics"></a>新的函式相關監視計量
Hello 監視區域中的資料流分析工作，在已經加入三個額外的函式相關度量。 它們是函式的要求、 函式的事件和失敗函式的要求下 hello 圖所示。

![使用 Machine Learning 函式計量調整串流分析](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "使用 Machine Learning 函式計量調整串流分析")

hello 的定義方式如下：

**函式要求**: hello 函式的要求數目。

**函式事件**: hello 中的事件數 hello 函式要求。

**失敗函式要求**: hello 的失敗函式要求數目。

## <a name="key-takeaways"></a>重要心得
toosummarize hello 重點，順序 tooscale 機器學習服務函式，資料流分析工作 hello 下列項目，必須考量：

1. hello 輸入的事件速率
2. hello，所容許之 hello 執行資料流分析工作的延遲 （並因此 hello 批次大小 hello 機器學習 web 服務的要求）
3. hello 佈建資料流分析 SUs 和機器學習 web 服務要求 （hello 額外的函式相關費用） 的 hello 數目

以完全分割的串流分析查詢為例。 如果需要更複雜的查詢 hello [Azure 資料流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)是取得 hello Stream Analytics 團隊的其他協助的最佳資源。

## <a name="next-steps"></a>後續步驟
toolearn 有關資料流分析的詳細資訊，請參閱：

* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
