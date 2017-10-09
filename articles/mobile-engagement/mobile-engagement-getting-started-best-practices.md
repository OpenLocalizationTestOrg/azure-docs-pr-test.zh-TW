---
title: "aaaAzure Mobile Engagement 入門指南最佳做法"
description: "Azure Mobile Engagement 入門指南與登入最佳作法"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - 入門指南與最佳作法
## <a name="overview"></a>概觀
**hello 行動畫面是很擁擠的空格：**在 2013 中，一項研究發現 hello 平均行動裝置已安裝的 27 應用程式。 使用者每個月通常會花 30 小時在他們的應用程式上。 這些時間大部分是花在社交網路和遊戲上 (大約 20 小時)。 2014，hello Android 市場有大約 1.5 百萬使用者 toochoose 從應用程式。 hello Apple store 包含約 1.2 百萬個應用程式。 隨著開發人員競相投入這個成長中的市場，行動應用程式的使用還在逐漸增長中。 

hello 平均行動使用者將會安裝和解除安裝應用程式，以根據變更的興趣高頻率和在應用程式體驗。 應用程式的順序 toodetermine hello 成功會變得很重要的 tooknow 以上的使用者人數只安裝您的應用程式。 重要 tooknow 如何有助於您的應用程式，而且如果該使用量趨勢會變更它。 下列問題的 hello 變得很重要的：

* 您的使用者開始 toofind 您認為不重要或過時的應用程式嗎？ 
* 有多少使用者完全不再使用您的應用程式？ 
* 應用程式內購買趨勢是向上還是向下？
* 使用者失敗 toocomplete 工作流程因為 hello 應用程式或缺乏感興趣的問題？ 
* 無法讓您的應用程式更加實用與相關推送全新內容 tooyour 使用者基底？ 
* 此全新的內容是相同的所有使用者或著重於根據您的應用程式中的行為的使用者區段 hello？ 

答案 tooquestions 類似 toothese 無法協助從您的應用程式延伸 hello 生命和營收。 此外也有助於您定義和維繫使用者客群。 

媒體相關應用程式通常 toohave 某些 hello 最高的保留使用者之間。 其中一個原因是它們會持續提供全新的內容 toousers。 有用的推播通知的早期採用導向 tooa 使用者區段通常會 toohave 應用程式保留很高的影響。 

hello Azure Mobile Engagement 程式是設計的 toohelp 您 hello 生命週期和保留您的應用程式提供擴充的方法 toogather 及分析 hello 使用您的應用程式的詳細的資訊。 它會協助您分類您使用者的基底根據 toobehavior，並建立已取得焦點的行銷活動來傳送推播通知和應用程式中的訊息 tooidentified 使用者區段。 關鍵效能指標 (KPI) 可測量使用者對於您的應用程式不同層面的使用程度。 Azure Mobile Engagement 提供 hello 方法需要 toodetermine 這些 Kpi。 它有助於提高 hello 傳回您藉由提供 hello 基礎結構的投資報酬率，您必須 tooincrease engagement 與行動應用程式。 

在充分利用 Azure Mobile Engagement 順序 tooget hello，您需要 toostart 設計良好的 engagement 計劃。 您的計劃可協助您識別 hello 精細的資料，您將需要 toobe 無法 toosegment 使用者基底。 這可能隨著行為和應用程式內的使用經驗而不同。 為了讓您計劃 toobe 成功，它是最佳的作法 tooclearly 定義 hello 會測量 hello 目標應用程式的 KPI。 與定義的純效能指標，您可以輕鬆地內嵌 hello 必要的邏輯應用程式 toocollect 正常粗略資料中您將使用 tooanalyze，並評估您的 Kpi。 本主題是用來定義所要使用您的參與計劃的 hello Kpi 的最佳作法指南。 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>步驟 1： 定義 Kpi toofit hello cd-r 光碟片模型
正確定義 Kpi 可以是很困難的工作 toocomplete。 針對不同產業而設計的應用程式，各有其本身的特性和目標。 這可能傾向 tooconfuse 方法。 避免這種 toohelp、 目標和 Kpi 應該分成三大類：**商務**， **Engagement**，和**技術**。 這是我們呼叫 hello **cd-r 光碟片模型**。

良好的計劃通常必須與量值在每個 hello 遵循 hello cd-r 光碟片模型的類別中的 hello 成功的 hello Kpi 的目標。

#### <a name="business-kpis"></a>商務 KPI
商務 Kpi 應該是最簡單部分 toobuild hello。 您在規劃行動應用程式時，即可能已用某種形式加以定義。 這些 KPI 通常有助於衡量應用程式的營收和 ROI。 hello 下列清單提供可協助定義效能指標時，會引導您的業務 Kpi 的一些範例：

* 媒體商務 KPI
  * 點按的廣告數目
  * 每一使用者造訪的頁面數目
  * 目前的訂用帳戶數目
* 遊戲商務 KPI
  * 應用程式內購買數目
  * 每一使用者的平均收益 (ARPU)
  * 每一工作階段花費的時間
  * 已玩天數和目前的遊戲等級
* 電子商務 KPI
  * 應用程式使用天數
  * 每一使用者的平均收益 (ARPU)
  * 結帳時購物車中的平均金額
  * 最多人檢視和購買的產品類別
* 銀行和保險商務 KPI
  * 帳戶數目
  * 啟動的功能
  * 造訪的提供項目頁面
  * 點按或啟動的警示       

#### <a name="engagement-kpis"></a>參與 KPI
Engagement KPI 時，使用者效能指標 toomeasure hello engagement。 此區域中的趨勢協助判斷您的應用程式的 hello 保留。 以下針對此類型的 KPI 提供數個範例效能指標：

* 在 hello 過去 7 天的作用中使用者
* Hello 過去 7 天的非作用中使用者計數
* 使用者不會使用 hello 應用程式在 30 天內的計數  

有些明顯的外部因素可能會影響此區域中的指標。 比方說，您可以考慮與使用者的行動裝置 toobe，隨時都能。 事實不一定是如此。 遊戲應用程式可能傾向周圍假日當玩家播放可能需時關閉工作或學校超出 toohave 較高的使用方式。   

也定義此類別中的 Kpi 應可協助您測量 hello 應用程式與您的客戶之間的關聯性。

#### <a name="technical-kpis"></a>技術 KPI
此類別中的效能指標可協助您判斷是否正常運作，還是懸置或當機。 這些指標可以測量 hello 應用程式的健全狀況，並且判斷可用性可能會防止使用者使用 hello 應用程式的問題。 此類別所收集的資訊也可能包含會是相關 toomarketing 小組的效能資訊。 hello 資料也可能是適用於疑難排解的 IT 和支援小組 toohelp 找出未回報的錯誤。 

以下是技術 KPI 的一些範例：

* 未處理或已處理的例外狀況資訊和計數 
* 前次當機的時間戳記
* 前次點按的按鈕或前次造訪的頁面
* Hello 應用程式的記憶體使用量
* 應用程式的畫面播放速率
* Hello 應用程式的作業系統版本上執行
* 應用程式版本

定義這些 Kpi toohelp 測量應用程式效能，並找出潛在的錯誤。 此指標應有助於減少 hello 您需要的時候 toodeliver 修正您的客戶。 此外也可協助您定義遇到過特定問題的使用者區段。 您可以使用使用者分割 toocreate 活動 toodeliver 通知關於可用的修正和潛在的促銷 toohelp 復原客戶滿意度。 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>腳本練習 1：建立 KPI 儀表板
定義行銷策略時，您的 KPI 應針對每個主要目標呈現個別的檢視。 它們應該清楚定義的資料點，可讓您 toocollect 重要資訊 toomonitor hello 使用者的您的應用程式與 hello 的行為。

建立包含下列資訊的 hello KPI 儀表板

1. Hello Kpi hello 應用程式有哪些？
2. 哪些資料點將每一個 KPI 使用 toorepresent？
3. 這項資料在我的應用程式中會位於何處 (即螢幕、設定、系統...)？
4. 此 KPI 是否可以顯示參與系列？

您可以使用 hello **KPI 產生器**工作表中的我們[媒體腳本範本][ Media Playbook link]範例與指引。

## <a name="step-2-your-engagement-program"></a>步驟 2：您的業務開發計劃
絕佳行動業務開發計劃應被視為應用程式的關鍵要素。 這應該絕對包含很棒的  褖畫惎程式使用者 hello 期間第一天的應用程式使用量的執行。 這通常會 toohave engagement 和保留您的應用程式上非常正面的影響。 根據研究顯示 hello 大部分的使用者不再使用應用程式 hello 安裝後的第幾天。 您想 toostrive toomeet 或 hello 使用者仍將焦點放在您的應用程式同時早期超過客戶預期的情況下推動感興趣。 請確定您在 hello 金鑰值與您的應用程式的優點 tooyour 客戶。 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

推播通知是 hello 最佳方法 tooearly 合作與行動裝置使用者。 不過，在區隔推播通知的使用者時，必須十分謹慎。 因為一旦使用者覺得收到的是垃圾郵件或不感興趣的通知，後果可能很嚴重。 在按幾下，使用者可以刪除您的應用程式永遠不會 tooreturn。 hello 使用者應該能夠接收獲得高度個人化的應用程式值，而不是泛型的垃圾郵件。

使用者目前正在進行，一旦 engagement 程式可協助磁碟機 hello 應用程式的其他層面。

比方說，您無法設定的行銷活動，作用中使用者 toorate 會要求您的應用程式。 由於此使用者區段為 hello 最常使用，而且擁有 hello 與您的應用程式的大部分體驗，您希望它們 toogive hello 最精確的評等。 一旦您擁有較高的應用程式的評等，它可以協助 hello 有機下載，以及減少您新的客戶取得成本的應用程式上的磁碟機。

#### <a name="engagement-sequence"></a>參與系列
全域業務開發計劃包含不同的參與系列。 每個序列目標是 tooreach 數個目標。

###### <a name="life-push-sequence"></a>即時推播系列
hello 目標生命發送順序會有所不同 hello hello 使用者的介入 hello 應用程式生命週期。 一個使用者有可能是剛接觸、偶爾玩玩或非常熱衷的。 Engagement 生命週期的不同階段，使用者可能會受益的提示或連結 toodocumentation hello 表單中全新的內容。 

例如新的使用者可能需要協助讓導向的 tooan 應用程式或受益於新遵循 hello 第一次在啟動 hello 應用程式的使用者 incentive 類似 toohello...

*「 高興 toohave 您將產品上架 ！請記住 toologin tooget 您的第 1 個月免費 ！ 」*

###### <a name="behavioral-push-sequence"></a>行為推播系列
hello 行為的推播順序以外的工具 tooincrease 使用量根據收集 hello 應用程式的使用者行為。  

比方說，活躍幻想 football 應用程式的使用者可能受益於正在執行以下列推播通知的 hello...

*「John，您真是個十足的美式足球迷！登入 tooour NFL 區段和 win 免費存取 toohello SuperBowl"！*

###### <a name="alerting-push-sequence"></a>警示推播系列
使用者會關注與其自身權益有關的消息。 警示推播系列可根據使用者已明確顯示的興趣來傳送警示，而強化參與程度。 當使用者選取他們自己的興趣 hello 應用程式中，這可能是明確。 它可能也會取決於隱含 hello 應用程式的使用者互動期間所收集資料。

比方說，hello 電子商務應用程式的使用者可能會定期購買咖啡的您擷取商務 KPI 的特定品牌。 hello 下列警示可以加強這位使用者的介入 hello 應用程式。

*"您好 Wes，您最愛的品牌的咖啡的其中一個會在關閉 hello 銷售 25%的 2015 年 9 月的第一週。我們非常感謝您與客戶和想 toomake 確定您已注意 」。*

###### <a name="rentention-push-sequence"></a>保留推播系列
使用重複的推播通知活動 toohelp 這個順序 aims tooretain 使用者磁碟機與 hello 應用程式參與規則習慣。 這有助於提高應用程式保留，如果 hello 使用者喜歡的休閒活動 hello 互動。 

例如，hello 運動相關應用程式的使用者可能會收到下列每週根據 hello 使用者的我的最愛小組的推播通知的 hello:

*「 機率 toowin 200 點，請移投票 hello 紐約洋基隊贏他們的遊戲針對多倫多藍色 Jays 本週是否 ！ 」*

#### <a name="hello-3w-approach"></a>hello 3W 方法
主控 hello 不同的推播順序有助於您要與使用者交流。 不過，您仍然需要 toouse hello 3W 方法個人化您的通知。 hello 3W 方法應該可滿足人員，該怎麼辦，當每個通知。 如果您能釐清這三個問題，您的通知即應可正確聚焦在業務開發上。

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>誰： hello 使用者區段中將會接收訊息
推送通知 tooyour 使用者應該考慮的非常敏感的通訊通道。 請確定目標 toosend tooa 使用者區段 hello 通知該使用者區段也已設定領域的 toohello 利益。 不正確地路由的通知是很有可能 toohave 上使用者的負面影響。 他們可能會認為前置 tooyour 應用程式正在解除安裝垃圾郵件。 

在定義將會收到通知的使用者區段時，請搭配使用特定的技術與行為條件。 定義使用者區段的簡單範例可能是類似 toohello 陳述式之後：

「 啟動的所有使用者 hello 行動應用程式的 hello 第一次 3 天前，和瀏覽過 hello 登入頁面兩次而不實際完成登入 」。

該陳述式可協助您識別您需要 toocollect toosupport 特定案例的 hello 資料。

###### <a name="what-hello-message-that-you-will-send"></a>事項： 您將會傳送 hello 訊息
**語氣**

在開發業務的過程中，請使用您的使用者區段易於接受的語氣。 這是很好的方式 tooconnect 與您的使用者，並將升級應用程式中的使用者感興趣。 

**重新導向**

推播通知可以用於多個開啟 hello 應用程式。 如果 hello 通知訊息提供的內容，例如廣播新聞或產品升級，此通知可能深層連結直接以滑鼠右鍵 toohello hello 應用程式內的內容。 toosupport，您必須建立的 URL 配置 toolet hello 應用程式管理 hello 重新導向。 在處理參與系列時，這是絕不可遺漏的重要步驟。

重新導向也可以用於其他系統。 例如，為動作 URL 很可能 tooredirect 使用者 toomany 包括 hello 下列其他系統：

* 網站
* 已設定電子郵件的信箱
* SMS Box
* 撥號服務
* 直接 toohello 等級 hello 應用程式的應用程式存放區。 

這提供許多機會 tooengage 使用者，並建立的自動規則 tooimprove 的表現。

**格式/內容**

不同類型和推播通知格式：

1. **公告**： 可讓您在不同時間的 toosend 廣告郵件 toousers (不在應用程式中的應用程式，或每當)。
2. **輪詢**： 啟用來提問以它們的 toogather 來自使用者的資訊。 建立準則 tootarget 使用者時，便可那些答案。
3. **資料推送**： 可讓您 toosend 二進位或 base64 資料檔案 tooupdate hello 應用程式。 包含在資料推送的 hello 資訊會傳送 tooyour 應用程式 toopersonalize hello 的使用者經驗，應用程式中。 您的應用程式必須設計 toobe toosupport hello 資料中資料推送。
4. **圖格 (僅限 Windows Phone)** ： 啟用您 toouse hello Microsoft 推播通知服務 (MPNS) toosend 原生推播通知包含 XML 資料 （因為 SDK 版本 0.9.0 的支援。 hello 磚的最終的裝載不得超過 32 kb。）。 直接在面板的磚會顯示 hello 訊息。
5. **Web 檢視** ：Web 檢視是包含 Web 內容的快顯視窗。 Hello 使用者已按下 hello 推播通知時，會出現這個快顯視窗。 網頁檢視可讓您 toohave hello 使用者具有更多的互動。

> [!NOTE]
> 請確定，您要將傳送為推播通知的 hello 內容符合 hello 各平台 (iOS、 Android、 Windows) 來開發應用程式及傳送推播通知的指導方針。
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>何時： hello 活動的時機
何時是最佳時間 tooactivate hello 觸發推播通知的活動？ 應採手動還是自動？ 是否為週期性的？ 決定 hello 正確的時間或頻率是不可或缺的 tooengage hello 獲得最佳結果的使用者。 針對每個參與順序與案例中，您必須指定何時將會是最佳時間 toosend hello 推播通知。 以下是可能的範例：

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

如果您每天都傳送許多通知，您必須慎重考量使用者是否會覺得您的訊息是垃圾郵件。 

Azure Mobile Engagement 提供兩種方式 toohelp 避免您正在為垃圾郵件看得見的通訊。 首先，使用相同的使用者執行未目標 hello 細部分割 tooensure。 此外，Azure Mobile Engagement 提供了「配額」功能。 這項功能可限制針對某個活動傳送的通知。 例如，設定每週預設配額 too5 可確保包含屬於 hello 活動使用者區段那個星期接收超過 5 通知使用者。

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>腳本練習 2：建立業務開發計劃
花費一些時間來摘述您的目標，以及定義您預期使用特定的順序 tooplay hello 活動。 請確定您套用 hello 3W 方法 toohello 通知您的行銷活動中。 

使用 hello **Engagement 程式**工作表中 hello[媒體腳本範本][ Media Playbook link]範例與指引。

## <a name="step-3-app-integration"></a>步驟 3：應用程式整合
#### <a name="create-a-tag-plan"></a>建立標記計劃
Azure Mobile Engagement toointegrate 到應用程式中，您將需要 toocreate 標記計劃。 hello 標記計劃是 hello cornerstone 的 hello 專案。 它會定義 hello 之間行銷規格 hello 工作流程的 hello 應用程式及收集 hello 應用程式 toomeasure Kpi 中的的 hello 真實的標記資料的關聯性。 它會指出哪些分析您將無法 toosee hello 入口網站中的。 它也可協助您定義使用者區段，並傳送您的使用者已取得焦點的推播通知 tooengage。 定義 hello 標記計畫之後，加入 hello 程式碼 toointegrate 到應用程式很簡單使用 hello Azure Mobile Engagement SDK。

標記計劃不應標記應用程式中的所有項目。 它只應包含屬於行動業務開發策略的標記資料。 這可能隨著應用程式而有所不同。 hello[媒體腳本範本][ Media Playbook link]提供 Azure Mobile Engagement 可協助您建置標記計劃與指定的方法。 使用 hello**標記計劃**計劃指南 toobuilding 的工作表索引標籤。

當定義標記區段 hello 工作表中，是非常特定的項目。 這是非常重要的 tooavoid 混淆。 請詳細說明預期將會傳送各個標記的每個案例。 包括 hello 其中每個標記為內嵌的 hello 活動名稱。 這應該所有包含在 hello **Informative** hello 工作表的一部分。 hello 標記計劃的工作表應該是 hello 主要參考進行測試驗證。 

在 hello**資料 toocollect**區段中，您的開發小組應該尋找 hello 類型、 名稱、 值和每個所需的額外資訊的索引鍵/值組標記，將會內嵌在 hello 應用程式。

建議您檢閱 hello 標記計劃與 hello 專案相關聯的所有小組。 請進行必要的更正，並確認行銷和開發團隊都可確實了解。

hello**陳述式的工作**工作表可以使用的 toohelp 指南所有參與 hello 專案。

#### <a name="data-types"></a>資料類型
這些是 Azure Mobile Engagement 所支援的一般資料類型。

###### <a name="devices-and-users"></a>裝置和使用者
Azure Mobile Engagement 會為每個裝置產生唯一識別碼來識別使用者。 這個識別項稱為 hello 裝置識別碼 （或 deviceid）。 它會產生該相同的裝置共用上執行的所有應用程式 hello 相同裝置識別碼的方式。

###### <a name="sessions-and-activities"></a>工作階段和活動
工作階段是一個使用者正在執行的 hello 應用程式的執行個體。 hello 工作階段所跨從 hello hello 使用者次啟動 hello 應用程式，直到它停止為止。

活動是一組件事，hello 應用程式可能會在工作階段期間的邏輯群組。 它通常是特定畫面中 hello 應用程式，但它可以是任何項目 hello hello 應用程式邏輯所定義。 您至少應標記應用程式的每個螢幕或活動。 這可讓您 toounderstand hello 使用者-路徑。

###### <a name="events"></a>事件
事件是使用的 tooreport 使用者與 hello 應用程式互動。 事件可以是即時的動作，像是共用內容或啟動影片。 標記事件會提供顯示使用者如何與 hello 應用程式互動的資料集合。 

###### <a name="jobs"></a>工作
作業是使用的 tooreport 動作，持續期間。 其範例包括：

* API 呼叫的執行
* 廣告的顯示時間
* 背景工作持續時間 
* 購買程序持續時間
* 觀看影片

###### <a name="errors"></a>Errors
錯誤是使用的 tooreport hello 應用程式所偵測到的問題。 例如，不正確的使用者動作，或 API 呼叫失敗。

###### <a name="application-information"></a>應用程式資訊
使用應用程式資訊 (App-info) tootag 資料相關 tooa 使用者的應用程式體驗。 它會產生與 hello 應用程式的使用者互動。 

對於給定的應用程式資訊的金鑰，Azure Mobile Engagement 只會追蹤的 hello 最新的值 （沒有記錄）。 應用程式資訊會顯示您的應用程式或使用者 hello 狀態。 例如 hello 登入狀態或使用者的最愛的產品群組。

###### <a name="crash-data"></a>當機資料
自動 hello Mobile Engagement SDK 報表應用程式失敗不會處理 hello 應用程式所收集的資料會損毀。 例如，已發生而未處理的例外狀況。

###### <a name="extra-data"></a>額外的資料
事件、錯誤、活動和工作皆可使用參數來處理。 這是開發人員可能會為從 hello 應用程式的特定資料提供額外資訊。 這很重要，因為可以定義精細的客群區隔。 

比方說，hello 值的 「 發行項"標記可讓您根據使用者檢視該特定的發行項的 toosegment 使用者。 不過，這樣可能還不夠。 如果相同「文章」標記的值也包含額外資訊 (例如活動中的 "news_category")，可能會更好。 這可能很實用 toodetermine 動態 hello hello 使用者最愛的分類。 

額外的資訊會以索引鍵/值組的形式報告。 Hello 範例中為此媒體應用程式，在 「 news_category"的 hello 額外的資訊將為該分類的 hello 值。 例如「體育」、「經濟」或「政治」。

#### <a name="tag-and-sdk-integration"></a>標記和 SDK 整合
逐步解說指示，以整合到應用程式 hello Azure Mobile Engagement SDK，按照 hello [Engagement SDK 整合](mobile-engagement-windows-store-integrate-engagement.md)Azure 網站上的文件。 從在 hello 該頁面頂端的 hello 連結進行選擇目標平台。

建議您為兩個建置於 Azure Mobile Engagement 之上的應用程式建立專案。 一個用於開發和測試預備和生產預備其他 hello。 您的 IT 團隊然後可以從暫存 tooproduction hello 使用者接受度測試成功時的測試升級。

#### <a name="user-acceptance-testing-uat"></a>使用者接受度測試 (UAT)
使用者接受度測試 (UAT) 必須確認一切運作皆符合設計。 工作流程可以完成，並根據標記計劃收集所有必要的資料：

* 標記資訊應該就地根據 toodocumented AZME 概念
* 收集您所需的所有資訊 (包括額外的資訊值、應用程式資訊值)
* 術語符合相應 tooyout 標記計劃
* 未傳送重複的標記

徹底測試您已在您的應用程式中嵌入的通知行為的所有 hello 類型

* 應用程式外和應用程式內的公告、投票、資料推播
* 文字/Web 檢視
* 徽章更新、類別

#### <a name="setup"></a>設定
設定 Azure Mobile Engagement 其實很簡單。 所有的 hello 文件相關的 toohello 使用者介面是 hello Azure Mobile Engagement 的網站，提供[toonavigate hello 使用者介面的方式](mobile-engagement-user-interface-home.md)。

建議您先設定 hello 正確的角色和角色成員資格 hello 使用者，您的專案。 這可協助您管理的所有使用者適當的存取權 toohello 平台。 您的角色可能包括：

* 系統管理員
* 開發人員
* 檢視者 

之後︰

* 註冊您的 deviceID tootest 您自己的裝置上。
* 移 toohello 設定您的帳戶和設定 hello 時區 toohave 圖表和通知的傳遞時間的時區設定。
* 移 toohello 設定您的應用程式，並註冊 hello"應用程式資訊 」 需要 tootarget 使用者得以實現。

如需有關如何 toorun 您的第一個推播通知宣傳活動中，檢閱[如何 tooget 開始使用，並管理推播通知出 tooyour 使用者 tooreach](mobile-engagement-how-tos.md)。

## <a name="conclusion"></a>結論
業務開發計劃是反覆進行的，您應持續加以改善，透過實驗找出您的應用程式最適用的計劃。 

一開始，在開發經驗與 engagement 策略不試 toobuild 整個全域 engagement 策略。 運用用來識別 Kpi 的逐步解說方法以及 tooleverage 它們。 每個應用程式都應有獨特的業務開發策略。

在開發經驗之後，您可以考慮新增下列 tooyour engagement 程式 hello:

* 追蹤：爭取到使用者後，您可能會定義資料收集來源。 Azure mobile Engagement 可連結的 toodata 集合來源。 它可讓您每個來源的 toomonitor 表現。 這項資訊將會擷取投資有趣 toomaximize。 
* A/B 測試：這是業務開發計劃不可或缺的一部分。 每個應用程式都有本身的特性。 透過 A/B 測試，您將可改善業務開發計劃。
* 地理位置：這是發展品牌的大好機會。 感謝您 toothis 功能可達到在 hello 正確的位置和時間。 我們建議您確認您已經收集足夠的使用者行為資料之前啟動 toouse 地理位置。
* 資料推播：資料推播是不可見的推播。 資料推播可讓您根據使用者行為自訂您的應用程式。 例如，如果使用者區段通常參照高科技產品，hello 應用程式擁有者可以傳送資料推入其中的個人與高科技內容她首頁。

## <a name="next-steps"></a>後續步驟
* [建立 Azure Mobile Engagement 帳戶](mobile-engagement-create.md)。
* 請瀏覽[定義您的 Mobile Engagement 策略](mobile-engagement-define-your-mobile-engagement-strategy.md)toolearn 深入了解定義您的 Mobile Engagement 策略。

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
