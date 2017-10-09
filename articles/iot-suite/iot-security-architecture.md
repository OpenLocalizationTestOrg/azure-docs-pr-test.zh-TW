---
title: "安全性架構 aaaIoT |Microsoft 文件"
description: "IoT 安全性架構指導方針與考量"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>物聯網安全性架構
在設計系統時，它是重要的 toounderstand hello 潛在威脅 toothat 系統，而且同理，加入適當的措施，因為 hello 系統是設計和架構。 請務必特別 toodesign 會 hello 的安全性考量事項產品從 hello 開始因為了解如何攻擊者可能會無法 toocompromise 系統可協助確定適當的安全防護處於從 hello 開頭的位置。 

## <a name="security-starts-with-a-threat-model"></a>保障安全從威脅模型開始
Microsoft 已長時間使用其產品威脅模型，並做了 hello 公司的威脅模型公開上市的程序。 hello 公司經驗示範 hello 模型具有未預期的優點超過 hello 立即了解哪些威脅是 hello 的大部分相關。 比方說，它也會建立途徑開啟的討論與其他外部 hello 開發小組可以導致 toonew 想法和改進 hello 產品中。

hello 目標威脅模型是的 toounderstand 攻擊方式可能會無法 toocompromise 系統，並確定適當的安全防護已就緒。 威脅模型在 hello 系統專為強制 hello 設計團隊 tooconsider 防護功能，而非之後部署系統。 這項事實是極為重要，因為裝置 hello 欄位中的安全性防禦措施 tooa 無數的更動而並不可行，容易發生錯誤並讓客戶有風險。

許多開發小組會執行擷取 hello 功能系統的需求 hello 獲益客戶絕佳工作。 不過，識別不容易注意到其他人可能會濫用 hello 系統的方式，是更具挑戰性。 威脅模型化作業可協助開發團隊了解攻擊者可能採取的行動和原因。 威脅模型是一個 hello 系統，會影響安全性的 hello 方式所做的變更 toohello 設計建立 hello 安全性討論的設計決策的結構化程序。 只要文件威脅模型時，這份文件也會代表 tooensure 持續性的知識，保留期課程學到的並快速協助新的小組將產品上架的理想方式。 最後，威脅模型的結果是 tooenable 您 tooconsider 安全性，例如哪些安全性承諾您想 tooprovide tooyour 客戶的其他層面。 將這些承諾與威脅模型化作業搭配使用，即可針對您的物聯網 (IoT) 方案提供分析與行動測試。

### <a name="when-toothreat-model"></a>當 toothreat 模型
[威脅模型](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx)優惠 hello 最大值，如果它就會併入 hello 設計階段。 當您在設計時，您擁有 hello 最大的彈性 toomake 變更 tooeliminate 威脅。 消除威脅的設計是 hello 所要的結果。 這麼做比新增安全防護功能、加以測試，並確保它們保持最新狀態等作業更加容易，因為排除作業不是隨時想做就能做。 它會變成更難 tooeliminate 威脅當產品變得更多落實，及依次最後需要更多工作及比潛在威脅模型在初期 hello 開發中的更不容易權衡取捨。

### <a name="what-toothreat-model"></a>哪一種 toothreat 模型
您應該執行緒模型為整個和也焦點放在下列區域的 hello 的 hello 方案：

* hello 安全性和隱私權功能
* hello 功能其失敗相關的安全性
* 觸控信任界限的 hello 功能 

### <a name="who-threat-models"></a>威脅模型跟誰有關
威脅模型化作業與任何其他程序一樣。  它是個不錯的主意 tootreat hello 威脅模型文件類似 hello 方案的任何其他元件，並進行驗證。 許多開發小組會執行擷取 hello 功能系統的需求 hello 獲益客戶絕佳工作。 不過，識別不容易注意到其他人可能會濫用 hello 系統的方式，是更具挑戰性。 威脅模型化作業可協助開發團隊了解攻擊者可能採取的行動和原因。

### <a name="how-toothreat-model"></a>如何 toothreat 模型
hello 威脅模型程序組成四個步驟。hello 步驟如下：

* 模型的 hello 應用程式
* 列舉威脅
* 降低威脅的風險
* 驗證 hello 補救措施

#### <a name="hello-process-steps"></a>hello 程序的步驟
請注意，建立威脅模型時的三個規則的基本 tookeep:

1. 建立參考架構圖表。 
2. 先從廣度下手。 取得概觀，以及整個之前深層深入了解 hello 系統。  這有助於確保您深入了解 hello 右中放置。
3. 磁碟機 hello 程序，請不要讓磁碟機您 hello 程序。 如果您發現問題出在 hello 模型化階段，而且想 tooexplore 它，請為它 ！  不要覺得您 slavishly 必須 toofollow 這些步驟。  

#### <a name="threats"></a>威脅
威脅模型的 hello 四個核心元素包含：

* 處理序 (Web 服務、Win32 服務、*nix daemons 等)請注意，如果無法在這些區域中進行技術性向下鑽研時，可將部分複雜的實體 (例如現場閘道器和感應器) 抽象化為處理序。
* 資料存放區 (儲存資料的任何位置，例如組態檔或資料庫)
* 資料流程 （其中的資料移動 hello 應用程式中的其他項目之間）
* 外部實體 hello 系統互動的任何項目，但不是在 hello hello 應用程式的控制之下 (例如使用者和附屬摘要）

Hello 架構圖表中的所有元素都是主體 toovarious 威脅。我們將使用 hello STRIDE 助憶鍵。 讀取[威脅模型化，分散](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/)tooknow 更多關於 hello STRIDE 項目。

Hello 應用程式圖表不同項目為主體 toocertain STRIDE 威脅：

* 處理程序是主體 tooSTRIDE
* 資料流程是主體 tooTID
* 資料存放區為主體 tooTID 和有時 R，如果 hello 資料存放區記錄檔。
* 外部實體是主體 tooSRD

## <a name="security-in-iot"></a>IoT 中的安全性
特殊用途的連線的裝置有大量的潛在互動的介面區域與互動模式，必須考慮所有的 tooprovide 保護數位存取 toothose 裝置的架構。 hello 詞彙 「 數位存取 」 是透過直接裝置互動實行的任何作業中使用這裡 toodistinguish 即存取安全性提供透過實體的存取控制。 例如，置於 hello 裝置與鎖定聊天室 hello 門。 無法使用軟體和硬體拒絕實體的存取，而量值可以採取 tooprevent 尖 toosystem 干擾實體的存取。 

當我們瀏覽 hello 互動模式，我們將探討 「 裝置控制 」 和 「 裝置資料 」 與 hello 相同層級的注意。 「 裝置控制 」 都能夠分類為 tooa 裝置所提供任何合作對象以 hello 目標變更，或影響其行為，其狀態或其環境的 hello 狀態的任何資訊。 「 裝置資料 」 都能夠分類為裝置發出 tooany 其他合作對象有關其狀態與 hello 觀察到其環境狀態的任何資訊。

在訂單 toooptimize 安全性最佳作法，建議您，一般的 IoT 架構分割成幾個元件/區域 hello 威脅模型練習的一部分。 本節會詳細說明這些區域，並包括下列重點︰

* 裝置、
* 現場閘道器、
* 雲端閘道器以及
* 宣告型授權。

區域是廣泛方式 toosegment 方案;每個區域通常會有它自己的資料和驗證和授權需求。 區域也可以使用的 tooisolation 損毀，並限制 hello 影響較高的信任區域上的低度信任區域。

信任的界限，其為 hello 點在 hello 圖中的紅線，另有說明以區隔每個區域。 它代表轉換的資料/資訊從一個來源 tooanother。 在這項轉換期間 hello 資料/資訊可能會主旨 tooSpoofing、 竄改、 否認、 資訊洩漏、 阻絕服務和的權限提高權限 （分散）。

![IoT 安全性區域](media/iot-security-architecture/iot-security-architecture-fig1.png) 

hello 所描述之每個界限內的元件也會受到 tooSTRIDE，啟用完整 360 威脅模型 hello 解決方案的檢視。 hello 的以下各節詳細說明每個 hello 元件和特定的安全性問題及解決方案應放置的位置。

hello 以下各節將討論這些區域中通常出現在標準元件。

### <a name="hello-device-zone"></a>hello 裝置區域
hello 裝置環境是 hello 立即實體空間周圍的實體存取及/或 「 本機網路 」 對等數位存取 toohello hello 裝置的裝置是可行。 「 本機網路 」 會假設 toobe 相異且從 – 隔離但可能橋接太 – hello 公用網際網路，且包含任何短程無線通訊技術，允許對等的裝置進行通訊的網路。 它會*不*包含建立 hello 假象，本機網路的任何網路虛擬化技術，而且也不包含公用運算子需要與任何兩個裝置 toocommunicate 公用網路空間上的網路就彷彿它們 tooenter 對等端對端通訊關聯性。

### <a name="hello-field-gateway-zone"></a>hello 欄位閘道區域
現場閘道器是一種裝置/應用裝置，或作為通訊啟用器的一般用途伺服器電腦軟體，甚至可能是裝置控制系統和裝置資料處理中心。 hello 欄位閘道區域包含 hello 欄位閘道本身，而且所有的裝置會附加 tooit。 正如 hello 名，閘道欄位做外部專用的資料處理功能，通常位置繫結、 有可能會造成主體 toophysical 入侵，以及將只具備有限操作的備援性。 所有 toosay 欄位閘道通常是一件事可接觸，而且同時在其函式的是破壞。 

現場閘道器和單純的流量路由器不同，它在管理存取與資料流程方面扮演積極的角色，這表示它是由應用程式處理之實體和網路連線或工作階段的終端。 相反地，NAT 裝置或防火牆並不算現場閘道器，因為它們並不是明確的連線或工作階段的終端，而是連線或工作階段經過的路線 (或區塊)。 hello 欄位閘道有兩個不同的介面區域。 一個面臨附加的 tooit hello 裝置，代表 hello hello 區域內，而且 hello 其他正面會面對外部的所有合作對象，hello hello 區域的邊緣。   

### <a name="hello-cloud-gateway-zone"></a>hello 雲端閘道區域
雲端閘道是跨越公用網路空間，通常朝雲端控制項和資料分析系統，這類系統的同盟可讓來自遠端通訊和 toodevices 或欄位的閘道，從數個不同的站台系統。 在某些情況下，雲端閘道可能立即可加速存取 toospecial 用途裝置如平板電腦或手機的終端機。 Hello 所討論的內容中，「 雲端 」 是不是相同站台為 hello 附加的裝置或欄位閘道的繫結的 toohello toorefer tooa 專用資料處理系統。 也在 [雲端] 區域中運作的量值防止目標實體的存取，而且不一定公開的 tooa 「 公用雲端 」 基礎結構。  

雲端閘道可能可對應到網路虛擬化重疊 tooinsulate hello 雲端閘道和所有其連接的裝置或欄位與任何其他網路流量的閘道。 hello 雲端閘道本身是既不裝置控制系統，也不處理或儲存設備的裝置資料;這些功能的介面與 hello 雲端閘道。 hello 雲端閘道區域包含 hello 雲端閘道本身以及所有欄位閘道，以及裝置直接或間接附加 tooit。 hello 區域 hello 邊緣是其中的所有外部合作對象通訊透過不同的介面區。

### <a name="hello-services-zone"></a>hello 服務區域
本內容將「服務」定義為任何軟體元件或模組，其透過現場閘道器或雲端閘道器來與裝置互動、進行資料收集和分析，以及命令與控制等功能。  服務是一種中介程序。 其下其身分識別向閘道及其他子系統處理、 儲存和分析資料，問題命令 toodevices 自發資料洞察能力或排程為基礎且公開資訊和控制功能 tooauthorized 終端使用者。

### <a name="information-devices-vs-special-purpose-devices"></a>資訊裝置與特殊用途的裝置
PC、手機和平板電腦主要的互動式資訊裝置。 手機和平板電腦是特別為了發揮最大電池續航力而最佳化的產品。 他們最好關閉部分和個人，不會立即互動時，或無法提供服務，例如播放音樂或引導他們擁有者 tooa 特定位置。 從系統觀點來看，這些資訊技術裝置主要是作為面對人的 Proxy。 也就是說，它們是建議動作的「人類傳動器」，以及收集輸入的「人類感應器」。 

特殊用途的裝置，從簡單的溫度感應器 toocomplex factory 生產線數千個那些，元件會不同。 這些裝置更以目的範圍，而且即使提供一些使用者介面，它們會與主要範圍的 toointerfacing 或整合至 hello 現實生活中的資產。 它們可以測量和報告環境情況、開啟閥門、 控制伺服、發出警報、切換燈號，以及執行許多其他工作。 它們可以協助 toodo 運作的資訊裝置是太泛型、 過於昂貴，太大，或太容易損毀。 hello 具體目的立即規定其技術的設計為以及 hello 可用貨幣的預算針對其生產環境和作業排程的存留期。 這些兩個關鍵因素 hello 組合限制 hello 可用操作能源預算、 實體磁碟使用量，因此可用的存放裝置計算和安全性功能。  

如果項目 」 屬於錯誤 「 自動化或遠端控制裝置，例如，實體失調異常，或者控制邏輯缺失 toowillful 未經授權入侵及操作。 hello 實際執行許多可能會終結、 建築物可能 looted 或燒錄關機，和的人可能會受傷或甚至無效。 這類損失的等級顯然比信用卡遭竊並被刷爆來得嚴重。 hello 讓事情的裝置的安全性門檻移動，而且也感應器資料，最後導致事項 toomove 命令的結果必須高於任何電子商務或銀行的案例中。 

### <a name="device-control-and-device-data-interactions"></a>裝置控制和裝置資料的互動
特殊用途的連線的裝置有大量的潛在互動的介面區域與互動模式，必須考慮所有的 tooprovide 保護數位存取 toothose 裝置的架構。 hello 詞彙 「 數位存取 」 是透過直接裝置互動實行的任何作業中使用這裡 toodistinguish 即存取安全性提供透過實體的存取控制。 例如，置於 hello 裝置與鎖定聊天室 hello 門。 無法使用軟體和硬體拒絕實體的存取，而量值可以採取 tooprevent 尖 toosystem 干擾實體的存取。 

當我們瀏覽 hello 互動模式，我們將探討 「 裝置控制 」 和 「 裝置資料 」 與 hello 注意事項威脅模型時的相同層級。 「 裝置控制 」 都能夠分類為 tooa 裝置所提供任何合作對象以 hello 目標變更，或影響其行為，其狀態或其環境的 hello 狀態的任何資訊。 「 裝置資料 」 都能夠分類為裝置發出 tooany 其他合作對象有關其狀態與 hello 觀察到其環境狀態的任何資訊。 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>威脅模型 hello Azure IoT 參考架構
Microsoft 會使用上述 toodo 威脅分析模型的 Azure IoT hello 架構。 在 hello 一節我們因此使用 hello Azure IoT 參考架構 toodemonstrate toothink 威脅模型 IoT 和 tooaddress hello 威脅的方式相關的識別方式的具體的範例。 在本案例中，我們會識別下列四個主要的區域︰

* 裝置和資料來源、
* 資料傳輸、
* 裝置和事件處理以及
* 展示

![Azure IoT 的威脅模型化作業](media/iot-security-architecture/iot-security-architecture-fig2.png) 

hello 圖會提供 Microsoft 的 IoT 架構的簡化的檢視使用的資料流程圖模型，以供 hello Microsoft 威脅模型化工具：

![使用 MS 威脅模型化工具進行 Azure IoT 威脅模型化作業](media/iot-security-architecture/iot-security-architecture-fig3.png)

請務必 hello 架構的 toonote 分隔 hello 裝置和閘道功能。 這允許更安全的閘道裝置 hello 使用者 tooleverage: hello 雲端閘道使用安全的通訊協定，通常需要更高的處理負擔，原生裝置-例如 thermostat-無法與通訊的支援提供其本身。 在 hello Azure 服務區域中，我們會假設該雲端閘道由 hello Azure IoT 中心服務的 hello。

### <a name="device-and-data-sourcesdata-transport"></a>裝置與資料來源/資料傳輸
本章節探索的威脅模型化 hello 透鏡透過上述的 hello 架構，並概略我們如何處理某些 hello 固有的考量。 我們將著重在威脅模型 hello 核心項目：

* 處理序 (包括我們所掌控的處理序以及外部項目)
* 通訊 (也稱為資料流程)
* 儲存體 (也稱為資料存放區)

#### <a name="processes"></a>處理序
在每個 hello 類別 hello Azure IoT 架構中所述，我們嘗試數目不同 hello 不同階段的資料/資訊的威脅在於的 toomitigate： 處理序、 通訊，與儲存體。 下面我們提供概觀 hello hello [處理序] 分類中，後面接著概觀如何這些無法最能降低最常見的： 

**詐騙 (S)**： 攻擊者可能是裝置，請在 hello 軟體或硬體層級，從擷取密碼編譯金鑰內容和後續存取具有不同的實體或虛擬裝置 hello 裝置 hello hello 識別之下的 hello 系統從已有人使用金錀資料。 遙控器就是很好的一例，既可以遙控電視機，也是很熱門的惡作劇工具。

**拒絕服務 (D)**：藉由干擾無線電頻率或剪斷線路，導致可以轉譯的裝置無法運作或無法通訊。 例如，蓄意破壞監控攝影機的電源或網路連線，使其完全無法回報資料。

**竄改 (T)**： 攻擊者可能會部分或全部取代 hello hello 裝置上執行的軟體，可能會允許 hello 取代軟體 tooleverage hello 真正的識別 hello 裝置如果 hello 金鑰資料或 hello 密碼編譯保存索引鍵資料的機能是可用 toohello 了其他人違法的程式。 例如，攻擊者可能利用擷取金鑰材料 toointercept 和隱藏 hello hello 通訊路徑上的裝置中的資料和取代 false 驗證與 hello 遭竊金鑰內容的資料。

**(I) 的資訊洩漏**： 如果 hello 裝置正在執行操作的軟體，這類操作的軟體可能有可能會洩漏資料 toounauthorized 合作對象。 例如，攻擊者可能利用擷取金鑰材料 tooinject 本身為 hello hello 裝置控制器或欄位閘道之間的通訊路徑或雲端閘道 toosiphon 關閉資訊。

**權限提高的權限 (E)**： 裝置執行特定的函式，可以強制的 toodo 其他項目。 比方說，是一半方式可以程式化的 tooopen 閥來的 tooopen 所有 hello 的方式。

| **元件** | **威脅** | **緩和** | **風險** | **實作** |
| --- | --- | --- | --- | --- |
| 裝置 |S |指派識別 toohello 裝置並驗證 hello 裝置 |取代其他裝置的裝置 hello 的一部分。 我們如何得知我們會提到 toohello 正確的裝置？ |驗證使用傳輸層安全性 (TLS) 或 IPSec 的 hello 裝置。 如果裝置無法處理完整的非對稱密碼編譯，則基礎結構應該支援在這些裝置上使用預先共用金鑰 (PSK)。 利用 Azure AD、[OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |適用於防拆機制 toohello 裝置如藉由很難 tooimpossible tooextract 機碼和其他 hello 裝置的密碼編譯內容。 |hello 風險是如果有人遭到竄改 hello 裝置 （實體干擾）。 該怎麼確認裝置未受到竄改？ |hello 最有效的緩解作業是可讓您將金鑰儲存在特殊的晶片上的電路系統的 hello 從索引鍵無法讀取，但只能使用 hello 索引鍵，但永遠不會揭露 hello 金鑰的密碼編譯作業的可信賴平台模組 (TPM) 功能. 記憶體 hello 裝置加密。 Hello 裝置的金鑰管理。 Hello 程式碼簽章。 | |
| E |具有 hello 裝置的存取控制。 授權配置。 |如果 hello 裝置允許供個別動作 toobe 根據命令從外部來源，來執行，或甚至危害感應器，它允許 hello 攻擊 tooperform 作業沒有其他可存取。 |需要授權配置 hello 裝置 | |
| 現場閘道器 |S |驗證 hello 欄位閘道 tooCloud 閘道 （憑證為基礎，PSK、 宣告為基礎，..） |如果有心人士可以欺騙現場閘道器，就可以偽裝成任何裝置。 |TLS RSA/PSK、IPSec、[RFC 4279](https://tools.ietf.org/html/rfc4279)。 所有 hello 相同的金鑰儲存，並證明考量中一般 – 最好的情況下的裝置是使用 TPM。 IPSec toosupport 無線感應器的網路 (WSN) 6LowPAN 副檔名。 |
| TRID |保護 hello 欄位閘道遭到竄改 (TPM)？ |詐騙攻擊欺騙考慮它正與其溝通 toofield hello 雲端閘道的閘道可能會導致資訊洩漏與資料遭到竄改 |記憶體加密、TPM、驗證。 | |
| E |現場閘道器的存取控制機制 | | | |

以下是這類威脅的一些範例︰

詐騙： 攻擊者可以擷取密碼編譯金鑰內容從裝置、 在 hello 軟體或硬體層級，以及後續存取不同的實體或虛擬裝置 hello 識別之下的 hello 裝置 hello 金錀 hello 系統已經取自。

**阻斷服務**：藉由干擾無線電頻率或剪斷線路，即可讓裝置變成無法運作或通訊。 例如，蓄意破壞監控攝影機的電源或網路連線，使其完全無法回報資料。

**竄改**： 攻擊者可能會部分或全部取代 hello hello 裝置上執行的軟體，可能會允許 hello 取代軟體 tooleverage hello 真正的識別 hello 裝置如果 hello 金鑰資料或 hello 密碼編譯保存索引鍵資料的機能是可用 toohello 了其他人違法的程式。

**竄改**：監控攝影機如果是顯示空走廊的可見範圍影像，可能會被對著這類走廊的照片拍攝。 煙霧或火災感應器可能會回報下方有人手持打火機。 在任一情況下，hello 裝置可能在技術上完全 trustworthy 朝向 hello 系統，但是它會報告操作的資訊。

**竄改**： 攻擊者可能利用擷取金鑰材料 toointercept 和隱藏 hello hello 通訊路徑上的裝置中的資料，並取代為 false 的資料驗證與 hello 遭竊金鑰內容。

**竄改**： 攻擊者可能會部分或完全取代 hello hello 裝置上執行的軟體，可能會允許 hello 取代軟體 tooleverage hello 真正的識別 hello 裝置如果 hello 金鑰資料或 hello 密碼編譯保存索引鍵資料的機能是可用 toohello 了其他人違法的程式。

**資訊洩漏**： 如果 hello 裝置正在執行操作的軟體，這類操作的軟體可能有可能會洩漏資料 toounauthorized 合作對象。

**資訊洩漏**： 攻擊者可能利用擷取金鑰材料 tooinject 本身為 hello hello 裝置控制器或欄位閘道之間的通訊路徑或雲端閘道 toosiphon 關閉資訊。

**阻絕服務**: hello 裝置可以關閉或開啟為模式通訊不成功 （此為刻意設計中許多工業機器）。

**竄改**: hello 裝置可以重新設定的 toooperate 處於未知的 toohello 控制系統中的 （已知的校正參數），讓資料可能會誤譯

**提高權限**： 裝置執行特定的函式，可以強制的 toodo 其他項目。 比方說，是一半方式可以程式化的 tooopen 閥來的 tooopen 所有 hello 的方式。

**阻絕服務**: hello 裝置可以轉換成通訊不成功的狀態。

**竄改**: hello 裝置可以重新設定的 toooperate 處於未知的 toohello 控制系統中的 （已知的校正參數），讓資料可能會誤譯。

**詐騙/竄改/不可否認性**： 若未受到保護 （這是很少 hello 擃勂厞取用者） 的攻擊可以匿名操作 hello 裝置的狀態。 遙控器就是很好的一例，既可以遙控電視機，也是很熱門的惡作劇工具。

#### <a name="communication"></a>通訊
裝置、裝置和現場閘道器，以及裝置和雲端閘道器之間的通訊路徑周遭，也佈滿威脅。 hello 表開啟的通訊端上 hello 裝置/VPN 周圍有一些指引：

| **元件** | **威脅** | **緩和** | **風險** | **實作** |
| --- | --- | --- | --- | --- |
| 裝置 IoT 中樞 |TID |(D)TLS (PSK/RSA) tooencrypt hello 流量 |竊聽或干擾 hello hello 裝置與 hello 閘道之間的通訊 |Hello 通訊協定層級的安全性。 使用自訂通訊協定，我們需要如何出 toofigure tooprotect 它們。 在大部分情況下，hello 通訊發生從 hello 裝置 toohello IoT 中樞 （裝置啟始 hello 連線）。 |
| 裝置裝置 |TID |(D)TLS (PSK/RSA) tooencrypt hello 流量。 |讀取裝置間傳輸中的資料。 Hello 資料遭到竄改。 多載 hello 裝置與新的連線 |安全性通訊協定層級 hello (MQTT/AMQP/HTTP/CoAP。 使用自訂通訊協定，我們需要如何出 toofigure tooprotect 它們。 hello hello DoS 威脅的防護方式 toopeer 裝置透過雲端或欄位的閘道，並為優先 hello 網路的用戶端有唯一的動作。 對等互連 hello 可能會導致 hello 之後需要 hello 閘道已代理的對等之間的直接連接 |
| 外部實體裝置 |TID |強式配對的 hello 外部實體 toohello 裝置 |竊聽 hello 連接 toohello 裝置。 與 hello 裝置干擾 hello 通訊 |安全地配對 hello 外部實體 toohello 裝置 NFC/藍芽 LE。 控制 hello 操作面板 hello 裝置 （實體） |
| 現場閘道雲端閘道 |TID |TLS (PSK/RSA) tooencrypt hello 流量。 |竊聽或干擾 hello hello 裝置與 hello 閘道之間的通訊 |Hello 通訊協定層級 (MQTT/AMQP/HTTP/CoAP) 上的安全性。 使用自訂通訊協定，我們需要如何出 toofigure tooprotect 它們。 |
| 裝置雲端閘道 |TID |TLS (PSK/RSA) tooencrypt hello 流量。 |竊聽或干擾 hello hello 裝置與 hello 閘道之間的通訊 |Hello 通訊協定層級 (MQTT/AMQP/HTTP/CoAP) 上的安全性。 使用自訂通訊協定，我們需要如何出 toofigure tooprotect 它們。 |

以下是這類威脅的一些範例︰

**阻絕服務**： 受條件約束的裝置通常是受到 DoS 威脅時它們主動接聽輸入的連線或網路上的未經要求即的資料包因為攻擊者可以開啟許多連接以平行方式並不這些服務或服務它們很慢，或 hello 裝置可以是大量湧入未經同意的流量。 在這兩種情況下，hello 裝置可以有效地轉譯 hello 網路上無法運作。

**詐騙、 資訊洩漏**： 受條件約束的裝置和特殊用途的裝置通常會有一個的所有安全性設備，例如密碼或 PIN 保護，或它們完全依賴信任 hello 網路，這表示它們會授與存取權當裝置位於 hello tooinformation 相同網路中，與該網路通常只保護的共用金鑰。 這表示當 hello 共用秘密 toodevice 或公開網路，它是可能 toocontrol hello 裝置或觀察 hello 裝置所發出的資料。  

**詐騙**： 攻擊者可能會進行攔截或部分覆寫 hello 廣播 」 與 「 詐騙 hello 建立者 (hello 中間 man)

**竄改**： 攻擊者可能會攔截或部分覆寫 hello 廣播資訊，並傳送為 false 

**資訊洩漏：**攻擊者可能上廣播竊聽並取得未經授權的資訊**阻絕服務：**攻擊者可能會干擾廣播訊號的 hello 和拒絕資訊散發

#### <a name="storage"></a>儲存體
每個裝置和欄位閘道有某種形式的儲存體 （暫存佇列 hello 資料，作業系統 (OS) 映像儲存體）。

| **元件** | **威脅** | **緩和** | **風險** | **實作** |
| --- | --- | --- | --- | --- |
| 裝置儲存空間 |TRID |儲存體加密、 簽署 hello 記錄檔 |讀取的資料從 hello 儲存體 （PII 資料） 遙測資料遭到竄改。 竄改排入佇列或快取的命令控制資料。 設定或韌體更新套件遭到竄改時快取，或在本機佇列可能會導致而遭到危害 tooOS 及/或系統元件 |加密、訊息驗證碼 (MAC) 或數位簽章。 盡可能透過資源的存取控制清單 (ACL) 或權限，進行強式存取控制。 |
| 裝置 OS 映像 |TRID | |竄改 OS/取代 hello OS 元件 |唯讀 OS 分割區、簽署 OS 映像、加密 |
| 欄位閘道存放裝置 （佇列 hello 資料） |TRID |儲存體加密、 簽署 hello 記錄檔 |讀取資料，從 hello 儲存體 （PII 資料） 遙測資料遭到竄改，竄改排入佇列，或快取命令控制資料。 竄改 （針對裝置或閘道欄位） 的設定或韌體更新套件快取，或在本機佇列時可能會導致而遭到危害 tooOS 及/或系統元件 |BitLocker |
| 現場閘道器 OS 映像 |TRID | |竄改 OS/取代 hello OS 元件 |唯讀 OS 分割區、簽署 OS 映像、加密 |

### <a name="device-and-event-processingcloud-gateway-zone"></a>裝置和事件處理/雲端閘道器區域
雲端閘道是跨越公用網路空間，通常朝雲端控制項和資料分析系統，這類系統的同盟可讓來自遠端通訊和 toodevices 或欄位的閘道，從數個不同的站台的系統。 在某些情況下，雲端閘道可能立即可加速存取 toospecial 用途裝置如平板電腦或手機的終端機。 Hello 所討論的內容中，「 雲端 」 是不是相同的站台為 hello 附加裝置或欄位閘道，以及操作的量值防止目標的實體存取，但不是繫結的 toohello toorefer tooa 專用資料處理系統一定是 tooa 「 公用雲端 」 基礎結構。  雲端閘道可能可對應到網路虛擬化重疊 tooinsulate hello 雲端閘道和所有其連接的裝置或欄位與任何其他網路流量的閘道。 hello 雲端閘道本身是既不裝置控制系統，也不處理或儲存設備的裝置資料;這些功能的介面與 hello 雲端閘道。 hello 雲端閘道區域包含 hello 雲端閘道本身以及所有欄位閘道，以及裝置直接或間接附加 tooit。

雲端閘道是大部分自訂內建軟體與公開的端點 toowhich 欄位閘道以服務方式執行，以及裝置連線。 因此，它的設計必須完全考慮到安全性問題。 請遵循 [SDL](http://www.microsoft.com/sdl) 程序來設計和建置此服務。 

#### <a name="services-zone"></a>服務區域
控制系統 （或控制站） 是一種軟體解決方案，介面與裝置，或欄位閘道或雲端閘道的 hello 目的是要控制一個或多個裝置及/或 toocollect 和/或存放區和/或分析簡報，裝置資料或後續的控制項的用途。 控制系統是討論的 hello hello 本文範圍，可能會立即以便與使用者互動中的唯一實體。 hello 例外狀況為中繼實體裝置，例如允許個人 tooturn hello 裝置關閉的交換器上的控制項介面，或變更其他屬性，以及功能的對等可以以數位方式存取的項目是。 

中繼的實體控制項介面是指其中任何類型的控管邏輯限制 hello 實體控制項介面的 hello 函式時，對等的函式可以從遠端起始或遠端的輸入與輸入的衝突可以避免 – 這種intermediated 的控制項介面是在概念上附加的 tooa 本機控制系統，可利用 hello 相同的基礎功能，因為其他 hello 裝置的遠端控制系統可能會附加的 tooin 平行。 最上層的威脅 toohello 雲端運算可以在讀取[雲端安全性聯盟 (CSA)](https://cloudsecurityalliance.org/research/top-threats/)頁面。

## <a name="additional-resources"></a>其他資源
Toohello 下列文章中的其他資訊，請參閱：

* [SDL 威脅模型化工具](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Microsoft Azure IoT 參考架構](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>另請參閱
toolearn 深入了解保護您的 IoT 解決方案，請參閱[保護 IoT 部署][lnk-security-deployment]。

您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：

* [預先設定的預防性維護解決方案概觀][lnk-predictive-overview]
* [IoT 套件的常見問題集][lnk-faq]

您可以閱讀 IoT 中樞中的安全性[控制存取 tooIoT 中樞][ lnk-devguide-security] hello IoT 中樞開發人員指南 》 中。

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md