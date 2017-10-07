---
title: "Machine Learning Studio 中的 aaaUse hello 範例資料集 |Microsoft 文件"
description: "用於範例模型包含在 Machine Learning Studio 中的 hello 資料集的描述。 您可以為您的實驗使用這些範例資料集。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>使用 Azure Machine Learning Studio 中的 hello 範例資料集
[top]: #machine-learning-sample-datasets

在 Azure Machine Learning 中建立新的工作區時，預設會包含一些範例資料集和實驗。 許多這些範例資料集由 hello 範例模型中 hello [Azure Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)。 其他則是機器學習中經常使用的各種範例。

其中的部分資料集可在 Azure Blob 儲存體中使用。 對於這些資料集，hello 下表提供的直接連結。 您可以在您實驗中使用這些資料集使用 hello[匯入資料][ import-data]模組。

hello 的這些範例資料集的其餘部分都是在您的工作區下**儲存的資料集**hello 實驗畫布，當您開啟或建立新的實驗 Machine Learning Studio 中的 hello 模組調色盤 toohello 方。
您可以自己實驗中使用任何這些資料集拖曳 tooyour 實驗畫布。


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>資料集名稱</th>
  <th align=left>資料集說明</th>
</tr>

<tr>
  <td valign=top>成人收入普查二進位分類資料集</td>
  <td valign=top>
使用工作成人歲 hello 16 的已調整的收入索引為 > 100 的 hello 1994 人口普查資料庫子集。<p> </p><b>使用方式：</b>分類個人賺取超過 50 K 一年是否使用 toopredict 人口統計資料的人。<p> </p><b>相關研究：</b>Kohavi, R.、Becker, B. (1996 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>機場代碼資料集</td>
  <td valign=top>
美國機場代碼。<p> </p>此資料集包含每個提供 hello 機場識別碼和名稱以及 hello 位置城市和州的美國機場的一個資料列。
  </td>
</tr>

<tr>
  <td valign=top>汽車價格資料 (原始)</td>
  <td valign=top>
汽車的相關資訊進行，並包括 hello 價格模型功能，例如 hello 數目磁柱和 MPG，以及保險風險分數。<p> </p>hello 風險分數一開始都與自動價格，且再進行調整程序稱為為 symboling tooactuaries 中實際的風險。 + 3 表示 hello 自動會有風險，，和-3 的值，就應該可以安全無虞。<p> </p><b>使用方式：</b>預測 hello 風險分數的功能，使用迴歸或多變量分類。 <p> </p><b>相關研究：</b>Schlimmer, J.C. (1987 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>單車出租 UCI 資料集</td>
  <td valign=top>
根據在華盛頓特區維護單車出租網路的 Capital Bikeshare 公司所提供的實際資料而建立的「UCI 單車出租」資料集。<p> </p>hello 資料集有一個資料列，在 2011年及 2012，17,379 資料列的總計每一天的每個小時。 每小時自行車出租 hello 範圍是從 1 too977。

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Bill Gates RGB 影像</td>
  <td valign=top>
公開可用的映像檔 tooCSV 資料的轉換。<p> </p>hello 轉換 hello 映像的程式碼中提供 hello<strong>色彩量化使用 K-means 群集</strong>模型詳細資料頁面。
  </td>
</tr>

<tr>
  <td valign=top>捐血資料</td>
  <td valign=top>
從 hello 捐血 Transfusion 服務中心的 Hsin 中國連縣 （市），台灣 hello 血捐贈者資料庫的資料子集。<p> </p>捐血資料包含自上次捐贈 hello 月份），和頻率，或 hello 總數捐獻、 最後一個捐贈，之後的時間和血捐贈數量。<p> </p><b>使用方式：</b> hello 的目標是透過分類 toopredict，是否 hello 捐血人捐贈捐血在年 3 月 2007 中，其中 1 代表捐血人期間 hello 目標句號和 0 非捐血人。 <p> </p><b>相關研究：</b>Yeh, I.C. (2008 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science <p> </p>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>來自 Amazon 的書籍評論</td>
  <td valign=top>
檢閱 Amazon，賓夕法尼亞州大學的研究人員取自 hello amazon.com 網站中的書籍 (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">人氣</a>)。 Hello 研究，請參閱 「 傳記、 Bollywood，發展方塊和 Blenders： 情緒分類的網域調"John Blitzer、 標記 Dredze 和 Fernando Pereira;關聯的計算 Linguistics (ACL)，2007年。<p> </p>hello 原始資料集有 975 K 檢閱排名 1、 2、 3、 4 或 5。 hello 檢閱英文版所撰寫，並且是從 hello 時段 1997年 2007年。 此資料集已向下取樣 too10K 評論。
  </td>
</tr>

<tr>
  <td valign=top>乳癌資料</td>
  <td valign=top>
三個 」 相關資料集 hello 機器學習文獻中經常出現的 Oncology Institute 所提供的其中一個。 結合診斷資訊與約 300 個生物組織樣本的實驗室分析中的特性。<p> </p><b>使用方式：</b>分類 cancer hello 類型、 根據 9 個屬性，其中有些是線性而有些是類別。 <p> </p><b>相關研究：</b>Wohlberg, W.H.、Street, W.N. 和 Mangasarian, O.L. (1995 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>乳癌特徵 <td valign=top>
hello 資料集包含的資訊 102 K 可疑的區域 （候選項目） 的 X-ray 映像，每個 117 功能所描述。 hello 功能專屬，而且它們的意義不會由 hello 資料集建立者 (Siemens Healthcare)。 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>乳癌資訊</td>
  <td valign=top>
hello 資料集包含每個可疑的區域 X-ray 映像的其他資訊。 每個範例提供的資訊 (例如，標籤病患識別碼、 修補程式相對 toohello 整個映像的座標) 大約 hello 乳癌 Cancer 功能集中 hello 對應資料列數目。 每個病患有一些範例。 對於有癌症的病患，一些範例是正數，而一些是負數。 對於沒有癌症的病患，所有範例都是負數。 hello 資料集有 102 K 範例。 偏差 hello 資料集，0.6%的 hello 點為正數、 負數 hello rest。 hello 資料集已由 Siemens Healthcare 可用。
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>共用 CRM Appetency 標籤</td>
  <td valign=top>
Hello KDD Cup 2009 客戶關係預測挑戰的標籤 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>)。
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>共用 CRM 流失標籤</td>
  <td valign=top>
Hello KDD Cup 2009 客戶關係預測挑戰的標籤 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>)。
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>共用 CRM 資料集</td>
  <td valign=top>
此資料來自 hello KDD Cup 2009 客戶關係預測挑戰 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>)。<p> </p>hello 資料集包含 50 K 客戶從 hello 法文電信公司橙色。 每個客戶都有 230 項不具名的特性，其中有 190 項數值特性和 40 項類別特性。 hello 功能都很疏鬆。
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>共用 CRM 向上銷售標籤</td>
  <td valign=top>
Hello KDD Cup 2009 客戶關係預測挑戰的標籤 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>)。
  </td>
</tr>

<tr>
  <td valign=top>能量效益迴歸資料</td>
  <td valign=top>
模擬能量分佈曲線的集合，以 12 種不同的建築形狀為基礎。 hello 建築物是 8 的功能，例如 glazing hello glazing 區域發佈和方向 區域，來區別。<p> </p><b>使用方式：</b>使用迴歸或分類 toopredict hello 能源效率分級根據做為其中一個實際值的兩個回應。 多級分類為 round hello 回應變數 toohello 接近的整數。 <p> </p><b>相關研究：</b>Xifara, A. 和 Tsanas, A.(2012 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>航班誤點資料</td>
  <td valign=top>
旅客飛行準時取自 hello hello 美國 TranStats 資料收集的效能資料(<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">準點</a>)。<p> </p>hello 資料集涵蓋 hello 時段年 10 月的 2013年。 上傳之前 tooAzure Machine Learning Studio，hello 資料集處理的時間，如下所示：<ul><li>hello 資料集已篩選的 toocover 只有 hello 70 繁忙機場在 hello 大陸美國</li><li>取消的航班已標示為誤點達 15 分鐘以上</li><li>已篩選掉更改路徑的航班</li><li>hello 下列資料行選取： 年、 月、 DayofMonth、 DayOfWeek、 載波偵測、 OriginAirportID、 DestAirportID、 CRSDepTime、 DepDelay、 DepDel15、 CRSArrTime、 ArrDelay、 ArrDel15、 已取消</li></ul>
</td>
</tr>

<tr>
  <td valign=top>航班準點率 (原始)</td>
  <td valign=top>
2011 年 10 月份美國境內飛機航班起降記錄。<p> </p><b>使用方式：</b>預測航班誤點。 <p> </p><b>相關研究：</b>取自美國交通部 <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>。
  </td>
</tr>

<tr>
  <td valign=top>森林火災資料</td>
  <td valign=top>
包含葡萄牙東北部地區的天候資料 (例如溫度和濕度指數以及風速)，再加上森林火災記錄。<p> </p><b>使用方式：</b>這是很困難的迴歸工作，其中 hello 目的 toopredict hello 燒錄的樹系引發區域。 <p> </p><b>相關研究：</b>Cortez, P. 和 Morais, A.(2008 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science <p> </p>[Cortez and Morais, 2007] P. Cortez and A. Morais。 資料採礦方法 tooPredict 使用 Meteorological 資料的樹系引發。 In J. Neves, M. F. Santos 和 J.Machado Eds.新趨勢的訴訟人工地 Intelligence hello 13 EPIA 2007-葡萄牙文會議上人工地 Intelligence 十二月，Guimarães-葡萄牙至 512-523，2007年。 APPIA, ISBN-13 978-989-95618-0-9. 可在此取得：<a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>。
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>德國信用卡 UCI 資料集</td>
  <td valign=top>
hello UCI Statlog （德文信用卡） 資料集 (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + 德文 + 信用 + 資料</a>)，使用 hello german.data 檔案。<p> </p>hello 資料集分類一組屬性，為低或高信用風險所描述的人員。 每個範例代表一名申請者。 有 20 的功能，數字和類別，以及二進位的標籤 （hello 信用風險值）。 高信用風險項目的標籤 = 2，低信用風險項目的標籤 = 1。 將錯誤分類為高的低風險範例 hello 成本為 1，而將錯誤分類為低的高風險範例 hello 成本是 5。
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>IMDB 影片標題</td>
  <td valign=top>
hello 資料集包含了在 Twitter 推文評等的電影的相關資訊： IMDB 影片識別碼、 電影名稱、 類型和實際執行的年份。 Hello 資料集中有 17 K 電影。 hello 紙張"S 中導入 hello 資料集 Dooms, T. De Pessemier and L. Martens" 中推出。 MovieTweetings：收集自 Twitter 的影片分級資料集。 Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>Iris 雙類別資料</td>
  <td valign=top>
這可能是 hello hello 模式辨識文獻中找到最佳已知資料庫 toobe。 hello 資料集是相當小，50 範例每三個光圈須從瓣花瓣測量。<p> </p><b>使用方式：</b>預測 hello 光圈 hello 度量單位類型。  <p> </p><b>相關研究：</b>Fisher, R.A. (1988 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>影片推文</td>
  <td valign=top>
hello 資料集是 hello 影片 Tweetings 資料集的擴充的版本。 hello 資料集有 170 K 分級的電影，從中 Twitter 上的結構良好推文。 每個執行個體代表推文，並且是 Tuple：使用者識別碼、IMDB 影片識別碼、分級、時間戳記、推文的收藏數，以及這個推文的轉推數。 hello 資料集是所提供 A.說、 S Dooms、 Loni B 和 D Tikk 推薦系統的挑戰 2014。
  </td>
</tr>

<tr>
  <td valign=top>不同汽車的油耗資料</td>
  <td valign=top>
此資料集是稍微修改的 hello 卡內基梅隆大學的 hello StatLib 程式庫所提供的資料集的版本。 hello 資料集用於 hello 1983 American 統計關聯目的。<p> </p>hello 資料列出英哩每加侖，在各種汽車的油耗用量以及資訊這類 hello 數目磁柱、 引擎的位移、 馬力、 總重量和加速。<p> </p><b>使用方式：</b>根據 3 個多重值離散屬性和 5 個連續屬性，預測燃料經濟效益。 <p> </p><b>相關研究：</b>StatLib Carnegie Mellon University (1993 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr>
  <td valign=top>皮馬族印第安人糖尿病二進位分類資料集</td>
  <td valign=top>
Hello 糖尿病 National Institute Digestive 和腎型疾病資料庫中的資料子集。 hello 資料集已篩選的 toofocus Pima 印度相似性的女性病患上。 hello 資料包括像是 glucose 和 insulin 層級，以及 lifestyle 因素的醫療資料。<p> </p><b>使用方式：</b>預測 hello 主體是否具有糖尿病 （二元分類）。 <p> </p><b>相關研究：</b>Sigillito, V.(1990 年)。 UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>. Irvine, CA: University of California, School of Information and Computer Science </td>
</tr>

<tr>
  <td valign=top>餐廳顧客資料</td>
  <td valign=top>
一組關於顧客的中繼資料，包括人口統計和喜好。<p> </p><b>使用方式：</b>使用此資料集、 結合 hello 其他兩個的餐廳資料集，tootrain 和測試推薦系統。 <p> </p><b>相關研究：</b>Bache, K. 和 Lichman, M.(2013 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>餐廳特色資料</td>
  <td valign=top>
一組關於餐廳及其特色的中繼資料，例如食物類型、用餐風格和地點等。<p> </p><b>使用方式：</b>使用此資料集、 結合 hello 其他兩個的餐廳資料集，tootrain 和測試推薦系統。 <p> </p><b>相關研究：</b>Bache, K. 和 Lichman, M.(2013 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>餐廳評等</td>
  <td valign=top>
包含從 0 too2 指定的使用者 toorestaurants 標尺上的分級。<p> </p><b>使用方式：</b>使用此資料集、 結合 hello 其他兩個的餐廳資料集，tootrain 和測試推薦系統。 <p> </p><b>相關研究：</b>Bache, K. 和 Lichman, M.(2013 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>煉鋼多類別資料集</td>
  <td valign=top>
此資料集包含一系列的記錄從鋼鍛鍊試用與 hello 實體屬性 （寬度、 粗細、 型別 （線圈、 工作表等） 產生 hello 鋼型別。<p> </p><b>使用方式：</b>預測任兩個數值類別屬性；硬度或強度。 您也可以分析各屬性之間的關聯。<p> </p>鋼鐵等級會遵循 SAE 和其他組織所定義的一組標準。 您要尋找特定 '等級' （hello 類別變數），而且想需 toounderstand hello 值。 <p> </p><b>相關研究：</b>Sterling, D. 和 Buntine, W.(NA)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information and Computer Science <p> </p>有用的輔助線 toosteel 等級可以在這裡找到： <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>望遠鏡資料</td>
  <td valign=top>
高能伽瑪粒子爆與背景雜訊的記錄，兩者皆使用蒙地卡羅程序來模擬。<p> </p>hello 模擬的 hello 意圖已 tooimprove hello 精確度的接地式 atmospheric Cherenkov gamma 望遠鏡首次發現，使用的統計方法 toodifferentiate 背景噪音 (hadronic hello 所需的信號 （Cherenkov 輻射淋浴） 之間淋浴 cosmic hello 上限氣氛中的一種非由起始）。<p> </p>hello 資料已經預先處理的 toocreate 具有的低端的叢集 hello 長軸是導向 hello 相機中心。 hello 特性 （通常稱為 Hillas 參數） 這個橢圓形皆可以用於辨識的 hello 圖像參數。<p> </p><b>使用方式：</b>預測某個波的影像代表的是訊號還是背景雜訊。<p> </p><b>附註：</b>簡單的分類精確性對這項資料並沒有幫助，因為將背景活動分類為訊號，比將訊號活動分類為背景還要糟。 比較不同的分類器應該使用 hello ROC 圖形。 hello 接受背景事件訊號必須為下列其中一個 hello 遵循臨界值的機率： 0.01、 0.02、 0.05、 0.1 或 0.2。<p> </p>另外請注意，低估 hello 背景事件 (如 hadronic 淋浴 h) 的數目，而在真實的度量，hello h 或雜訊類別代表 hello 大部分的事件。 <p> </p><b>相關研究：</b>Bock, R.K。 (1995 年)。 UCI 機器學習服務儲存機制 <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>。 Irvine, CA: University of California, School of Information </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>天氣資料集</td>
  <td valign=top>
每小時的土地基礎天氣觀測值與 NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">合併資料從 201304 too201310</a>)。<p> </p>hello 天氣資料涵蓋了源自機場天氣站台，涵蓋 hello 時段年 10 月的 2013年的觀察值。 上傳之前 tooAzure Machine Learning Studio，hello 資料集處理的時間，如下所示：<ul><li>氣象 Id 所對應的 toocorresponding 機場代碼</li><li>篩選掉不相關聯 hello 70 繁忙機場天氣站台</li><li>hello 日期資料行已分割成個別年、 月和日的資料行</li><li>hello 下列資料行選取： AirportID、 年份、 月份、 日期、 時間、 時區、 SkyCondition、 可見性、 WeatherType、 DryBulbFarenheit、 DryBulbCelsius、 WetBulbFarenheit、 WetBulbCelsius、 DewPointFarenheit、 DewPointCelsius、 RelativeHumidity，WindSpeed、 WindDirection、 ValueForWindCharacter、 StationPressure、 PressureTendency、 PressureChange、 SeaLevelPressure、 RecordType、 HourlyPrecip、 高度表</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 資料集</td>
  <td valign=top>
資料是從 Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>) 上每家 S&P 500 公司的文章衍生而來 (儲存為 XML 資料)。<p> </p>上傳之前 tooAzure Machine Learning Studio，hello 資料集處理的時間，如下所示：<ul><li>擷取每家特定公司的文字內容</li><li>移除 wiki 格式</li><li>移除非英數字元</li><li>轉換所有文字 toolowercase</li><li>新增了知名公司類別</li></ul><p> </p>請注意，某些公司的發行項不在因此 hello 記錄數目會少於 500。
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
hello 資料集含有客戶資料，以及其回應 tooa 直接郵寄促銷活動的相關指示。 每個資料列都代表一個客戶。 hello 資料集包含有關使用者人口統計或過去的行為，以及 3 個標籤資料行的 9 功能 （瀏覽，轉換，而且會浪費）。  請瀏覽是表示客戶造訪之後 hello 行銷活動中，轉換表示客戶購買某樣東西，而且會浪費 hello 量所花費的二進位資料行。  hello 資料集已由 MineThatData 電子郵件分析和資料採礦挑戰的 Kevin Hillstrom 可用。
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
測試中的範例 hello RCV1 V2 路透社新聞資料集的功能。 hello 資料集有約 781 K 新聞文章，以及其 Id （hello 資料集的第一個資料行）。 每篇文章均執行語彙基元化、停用字詞和詞幹分析。 hello 資料集已由 David 可用。 D. 提供。
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Hello RCV1 V2 路透社新聞資料集中的定型範例的功能。 hello 資料集有 23 K 新聞文章，以及其 Id （hello 資料集的第一個資料行）。 每篇文章均執行語彙基元化、停用字詞和詞幹分析。 hello 資料集已由 David 可用。 D. 提供。
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
從 hello KDD Cup 1999 知識探索的資料集和資料採礦工具競爭對手 (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>)。<p> </p>hello 資料集已下載且儲存在 Azure Blob 儲存體 (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) 和包含定型和測試資料集。 hello 定型資料集大約有 126 K 資料列和 43 資料行，包括 hello 標籤。 三個資料行屬於 hello 標籤資訊，而且 40 個資料行，包含數字和字串/類別的功能，可供定型 hello 模型。 hello 測試資料有大約 22.5 K 測試範例與 hello 相同 43 如同 hello 定型資料的資料行。

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
新聞文章 hello RCV1 V2 路透社新聞資料集中的主題指派。 新聞文章可以指派 tooseveral 主題。 每個資料列的 hello 格式是 「&lt;主題名稱&gt;&lt;文件識別碼&gt;1"。 hello 資料集包含 2.6 M 主題指派。 hello 資料集已由 David 可用。 D. 提供。
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
此資料來自 hello KDD Cup 2010 學生效能評估挑戰 (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">學生效能評估</a>)。 hello 所使用的資料是 hello Algebra_2008_2009 定型集 (戳記程式，J.，Niculescu Mizil，a，Ritter，S Gordon、 G.J.，& Koedinger，K.R. (2010)。 Algebra I 2008-2009。 KDD Cup 2010 教育資料探勘挑戰中的的挑戰資料集。 請在 <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> 或 <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a> 尋找。<p> </p>hello 資料集已下載且儲存在 Azure Blob 儲存體 (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) 且包含從一位學生家教廣告系統記錄檔。 hello 提供功能包含問題識別碼和簡短描述，學生識別碼、 時間戳記，以及多少嘗試 hello 學生之前解決 hello 問題 hello 中的以滑鼠右鍵的方式。 hello 原始資料集有 8.9 M 記錄。此資料集已向下取樣 toohello 前到 100 萬個資料列。 hello 資料集有 23 tab 分隔的資料行不同的類型： numeric、 類別和時間戳記。

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
