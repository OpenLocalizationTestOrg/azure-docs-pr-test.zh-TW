---
title: "在 Azure 上的 aaaIntroduction toomicroservices |Microsoft 文件"
description: "建置雲端應用程式與 microservices 方法是很重要的現代應用程式開發，以及如何 Azure Service Fabric 提供平台 tooachieve 這的總覽。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>為什麼 microservices 接近 toobuilding 應用程式嗎？
身為軟體開發人員，已熟悉思考如何將應用程式分解成元件部分。 它是 hello 中央範例物件導向、 軟體的抽象概念和元件化。 現在，這個 factorization 傾向 tootake hello 表單的類別和介面之間共用程式庫和技術層級。 通常是透過一種分層方法，有後端存放區、中間層商務邏輯和前端使用者介面 (UI)。 什麼*具有*變更透過 hello 過去幾年來，我們，身為開發人員，建置是分散式的 hello 雲端應用程式和驅動 hello 的企業。

hello 多變的商務需求如下：

* 服務的建置，且會在新的地理區域中的小數位數 tooreach 客戶運作 （例如）。
* 更快的特色與功能 toobe 無法 toorespond toocustomer 要求敏捷的方式來傳遞。
* 改善的資源使用量 tooreduce 成本。

這些商務需求會影響我們「如何」  建置應用程式。

Azure toomicroservices 的 hello 方法的相關資訊，請參閱[Microservices： 由 hello 雲端應用程式 revolution](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/)。

## <a name="monolithic-vs-microservice-design-approach"></a>單體式與微服務設計方法
所有應用程式會隨著時間而演化。 成功的應用程式的發展因 toopeople 很有用。 失敗的應用程式不會演化，最後會取代。 hello 問題： 多少執行您知道您的需求，而且什麼它們會在未來的 hello？ 例如，假設您要建置某部門的報告應用程式。 您已確定 hello 應用程式保持貴公司的 hello 範圍內，而且 hello 報表是很短。 您所選擇的方法，從不同說，建置的服務傳送數百萬個客戶的視訊內容 tootens。 

某些情況下，使用者入門內容 hello 門做為概念的證明是 hello 驅動因素，而您知道可以稍後會重新 hello 應用程式的設計。 從來不用卻過度設計並沒有太大意義。 它的 hello 一般工程取捨。 在 hello 相反地，當公司談論建置為 hello 雲端，hello 預期成長和使用方式。 hello 問題是，將無法預期的成長和小數位數。 我們希望 toobe 無法 tooprototype 快速時也知道我們會在未來的成功路徑 toodeal 上。 這是 hello 簡式的啟動方式： 建置、 量值、 了解，並逐一查看。

在 hello 用戶端-伺服器紀元，我們傾向 toofocus 建置分層式的應用程式在每個階層中使用特定技術。 hello 詞彙*龐大*應用程式有一種，出現的這些方法。 hello 介面傾向 toobe hello 層之間，並在各層內的元件之間使用更緊密結合的設計。 開發人員設計並分解類別，將類別編譯成程式庫，然後連結起來成為一些可執行檔和 DLL。 

有優點 toosuch 僵化設計方法。 它通常是較簡單的 toodesign，並且它有快速的呼叫之間的元件，因為這些呼叫通常是透過處理序間通訊 (IPC)。 此外，每個人都測試單一產品，通常會 toobe 更多人資源的效率。 hello 缺點是階層式的圖層之間緊密結合在一起，而您無法調整個別的元件。 如果您需要 tooperform 修正或升級，您有其他人 toowait toofinish 其測試。 很難 toobe 敏捷式軟體開發。

Microservices 解決這些缺點，更密切配合 hello 前面業務需求，但還具有優點和負債。 microservices hello 優點為每一個通常會封裝更簡單的商務功能，它相應增加或減少測試、 部署和獨立管理。 小組會導向多個商務案例比 hello 分層的方式的技術的微服務方法的重要優點是鼓勵。 實際上，較小的團隊會採用他們選擇的任何技術，根據客戶案例來開發微服務。 

換句話說，hello 組織不需要 toostandardize 技術 toomaintain 微服務應用程式。 個別團隊什麼意義，根據小組的專業知識，或最適當 toosolve hello 問題，可以自己的服務。 實際上，最好有一組建議的技術，例如特定的 NoSQL 存放區或 Web 應用程式架構。

管理不同的實體和處理更複雜的部署和版本控制的 hello 增加數目傳入 hello microservices 缺點。 Hello microservices 之間的網路流量增加以及 hello 對應的網路延遲。 經過大量論述之後，可知細微的服務是效能夢魘的解決良方。 沒有工具 toohelp 檢視這些相依性，很難太 「 看見 」 hello 整個系統。 

標準進行 hello 微服務方法的運作方式是同意 toocommunicate 且容錯的只有 hello 事項您需要如何從一項服務，而不是固定的合約。 重要 toodefine hello 中這些最前面位置的合約設計，是因為服務彼此獨立更新。 另一個在設計微服務方法時出現的描述是「細緻的服務導向架構 (SOA)」。

***在最簡單 hello microservices 設計方式是關於解除解合通訊的服務，同意標準的獨立變更 tooeach 與同盟。***

人探索更多雲端應用程式所產生，因為此分解成獨立的案例已取得焦點的服務應用程式整體 hello 是長期更好的方法。

## <a name="comparison-between-application-development-approaches"></a>應用程式開發方法的比較
![Service Fabric 平台應用程式開發][Image1]

1) 單體式應用程式包含領域特定功能，通常會依功能層來劃分，例如 Web、商務和資料。

2) 單體式應用程式可藉由複製到多部伺服器/虛擬機器/容器上進行擴充。

3) 微服務應用程式會將個別功能分隔成個別較小的服務。

4) hello microservices 方法標尺出藉由部署每個服務各自獨立地建立跨伺服器/虛擬機器的執行個體的這些服務/容器。

設計與微服務方法並不是萬靈丹所有專案，但其未與先前所述的 hello 的商務目標更密切地對齊。 開始使用整合型的方法可以接受如果您知道，您將必須 hello 機會 toorework hello 將程式碼稍後 microservices 設計。 更常見的是，您以開頭整合的應用程式，緩時變分解在階段中，從 hello 需要 toobe 更可擴充或敏捷式軟體開發的功能區域。

toosummarize，hello 微服務的方法是 toocompose 應用程式的許多小型的服務。 hello 服務執行跨機器的叢集部署的容器中。 以小型小組開發著重於案例的服務和獨立測試版本、 部署及調整每個服務，以便能持續改進 hello 整個應用程式。

## <a name="what-is-a-microservice"></a>什麼是微服務？
有不同的微服務定義。 如果您搜尋 hello 網際網路時，您會發現許多實用的資源，提供他們自己的觀點和定義。 不過，大部分的下列特性的 microservices hello 會廣泛地同意：

* 封裝客戶或商務案例。 什麼是 hello 所解決的問題？
* 由小型工程團隊開發。
* 使用任何程式設計語言撰寫並使用任何架構。
* 由獨立控制版本、部署及調整的程式碼和 (選擇性) 狀態所組成。
* 透過定義完善的介面和通訊協定，與其他微服務互動。
* 唯一的名稱 (Url) 使用的是 tooresolve 它們的位置。
* 保持一致，而且用於失敗 hello 存在。

您可以彙整這些特性︰

***微服務應用程式是由獨立控制版本和可調整的客戶焦點式服務所組成，這些服務透過標準通訊協定和定義完善的介面彼此通訊。***

現在我們在上展開並釐清 hello 其他人和我們涵蓋 hello hello 前面一節中的前兩個點。

### <a name="written-in-any-programming-language-and-use-any-framework"></a>使用任何程式設計語言撰寫並使用任何架構。
身為開發人員，我們應該可用 toochoose 我們想根據我們的技術或 hello hello 服務需求的語言或架構。 在某些服務，您可能值優先於所有其他的 c + + hello 效能優點。 在其他服務，以 C# 或 Java managed 開發 hello 輕鬆可能是最重要。 在某些情況下，您可能需要 toouse 特定夥伴文件庫中，資料儲存技術，或公開的方法 hello 服務 tooclients。

您已選擇一種技術之後，您會回到 toohello 操作或生命週期管理和調整 hello 服務。

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>可讓程式碼和狀態 toobe 獨立版本設定，部署，以及縮放
不過您選擇 toowrite 您 microservices、 hello 程式碼和 （選擇性） hello 狀態應該獨立部署、 升級和縮放。 這是實際的困難問題 toosolve hello，因為這時候您就要 tooyour 技術的選擇。 縮放比例，了解如何 toopartition （或分區） 兩者會 hello 程式碼和狀態是一項挑戰。 當 hello 程式碼和狀態會使用不同的技術，是常見的今天，hello 部署指令碼，為您的微服務會需要 toobe 無法 toocope，連同調整兩者。 這也是關於靈活度和彈性，讓您可以升級 hello microservices 部分而不需要 tooupgrade 全部一次。

傳回在當下 toohello 整合與微服務方法，hello 下列圖表顯示 hello 方法 toostoring 狀態中的 hello 差異。

#### <a name="state-storage-between-application-styles"></a>應用程式樣式之間的狀態儲存
![Service Fabric 平台狀態儲存體][Image2]

***hello 左側的 hello 整合型方法有單一資料庫以及階層的特定技術。***

***在右邊的 hello 的 hello microservices 方法有互連 microservices 其中狀態是通常已設定領域的 toohello 微服務，而使用各種技術的圖形。***

在整合的方法中，通常 hello 應用程式會使用單一資料庫。 hello 優點是，它可讓您輕鬆 toodeploy 的單一位置。 每個元件可以有單一資料表 toostore 其狀態。 團隊必須 toostrictly 不同狀態，這是一項挑戰。 無可避免地有 temptations tooadd 新資料行 tooan 現有客戶資料表、 資料表之間進行 join 作業而建立 hello 儲存層的相依性。 發生這種情況後，您無法調整個別的元件。 

在 hello microservices 方法中，每個服務會管理及儲存自己的狀態。 每項服務負責縮放比例的 hello 服務的程式碼和狀態一起 toomeet hello 需求。 一個缺點是需要 toocreate 時檢視或查詢，您的應用程式資料，您需要跨不同的狀態存放區 tooquery。 為了解決此問題，通常是由一個獨立的微服務建置一個跨許多微服務的檢視。 如果您需要 tooperform hello 資料上的多個即席查詢，每個微服務應該考慮撰寫其資料 tooa 資料倉儲服務進行離線分析。

版本設定是部署的特定 toohello 版微服務因此多個，不同版本的部署和並存執行。 版本控制位址 hello 案例較新版的微服務在升級期間發生失敗而需要 tooroll 後 tooan 較舊版本。 hello 其他案例進行版本控制正在執行 A/B 樣式測試不同的使用者體驗 hello 服務的不同版本的位置。 比方說，然後再發送多廣泛是常見 tooupgrade 一組特定的客戶 tootest 新功能的微服務。 之後的 microservices 生命週期管理時，現在這個引出 toocommunication 兩者之間。

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>透過定義完善的介面和通訊協定，與其他微服務互動
本主題需要少注意，因為已透過 hello 發行過去 10 年的服務導向架構的廣泛文獻描述通訊模式。 一般而言，服務通訊會使用其他方法 HTTP 和 TCP 通訊協定和 XML 或 JSON 做為 hello 序列化格式。 從介面的觀點而言，它是關於採用此種設計 hello web 方法。 但並不禁止您使用二進位通訊協定或您自己的資料格式。 準備的人 toohave 更難時間，使用您 microservices，如果公開使用這些項目。

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>唯一的名稱 (URL) 使用 tooresolve 具有它的位置
還記得我們如何保留說 hello 微服務方法，就像是 hello web 嗎？ 就像 hello web、 您的微服務需要 toobe 可定址只要它正在執行。 如果您正在考慮機器及哪一部要執行特定的微服務，很快就會陷入困境。 

在 hello 相同方式 DNS 會解析特定 URL tooa 特定電腦，您的微服務需要 toohave 唯一的名稱，使其目前位置是可探索。 Microservices 需要可定址的名稱，因此獨立於 hello 基礎結構上執行。 這暗示會如何部署您的服務和其探索的方式之間的互動因為需要 toobe 服務登錄。 同樣地，當電腦失敗時，則 「 hello 登錄服務 」 必須告訴您其中 hello 服務現在正在執行。 

這會帶我們 toohello 下一個主題： 恢復功能和一致性。

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>會維持一致且適用於失敗 hello 存在
處理未預期的錯誤是其中一個最困難的問題 toosolve hello，尤其是在分散式系統。 大部分的 hello 我們身為開發人員撰寫的程式碼會處理例外狀況，而且這也 hello 大部分時間的測試。 hello 問題會比撰寫程式碼 toohandle 失敗更為複雜。 Hello hello 微服務執行所在的電腦失敗時，會發生什麼情況？ 不只執行您需要 toodetect 微服務失敗 （本身困難的問題），但您也需要的項目 toorestart 您的微服務。 

微服務需要 toobe 彈性 toofailures 並重新啟動通常基於可用性的另一部電腦上。 這也會提供關閉儲存代表 hello 微服務，其中 hello 微服務可以復原，從這個狀態，以及是否 hello 微服務已成功為可以 toorestart toohello 狀態。 換句話說，需要 toobe 更有恢復 hello 計算 （hello 程序重新啟動） 以及更有恢復 hello 狀態或資料 （無資料遺失和 hello 資料保持一致的）。

hello 的恢復功能的問題會在其他案例，例如失敗時發生應用程式升級期間會更加惡化。 hello 微服務，使用 hello 部署系統，不需要 toorecover。 它也需要 toothen 決定它是否可以繼續 toomove 轉寄 toohello 較新版本，或改為復原先前版本 toomaintain tooa 一致的狀態。 這類電腦足以是否可用 tookeep 起 toorecover 舊版 hello 微服務需要 toobe 視為如何的問題。 這需要 hello 微服務 tooemit 健全狀況資訊 toobe 無法 toomake 這些決策。

### <a name="reports-health-and-diagnostics"></a>報告狀況和診斷
微服務必須報告其健全狀況和診斷，這一點看似明顯，但卻經常被輕忽。 否則，難以從操作觀點上深入了解。 一組獨立的服務和處理很困難，toomake 意義 hello 事件順序的電腦時鐘偏差之間的關聯的診斷事件。 在 hello 您在透過同意通訊協定與資料互動的微服務相同的方式格式化、 那里轉換的標準化方式 toolog 健全狀況，以及最終都會在事件中的診斷事件存放區進行查詢和檢視中的需求。 在微服務方法中，關鍵在於不同團隊同意採用單一記錄格式。 需要 toobe hello 整個應用程式中的一致方法 tooviewing 診斷事件。

狀況與診斷不同。 健全狀況是關於 hello 微服務報告其目前狀態 tootake 適當的動作。 升級與部署機制 toomaintain 可用性使用一個良好範例。 雖然服務可能是目前狀況不良，因為 tooa 處理序當機或電腦重新開機，hello 服務可能依然可運作。 您必須 hello 最後一件事是此變差 toomake 執行升級。 hello 最好的方法的第一個 toodo 進行調查，或允許 hello 微服務 toorecover 的時間。 微服務的健全狀況事件可協助我們做出明智的決策，實際上有助於建立自我修復的服務。

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric 做為微服務平台
Azure Service Fabric 中從方塊產品，已在樣式中，toodelivering 服務通常龐大出現從 microsoft 的轉換。 建立和操作大型的服務，例如 Azure SQL Database 和 Azure Cosmos DB 形狀 Service Fabric hello 體驗。 經過一段時間的 hello 平台發展，因為越來越多的服務採用它。 重要的是，Service Fabric 必須 toorun，而不只是在 Azure 中獨立 Windows 伺服器部署中。

***Service Fabric hello 目的 toosolve 建置和執行服務的 hello 艱難問題，且有效率地利用基礎結構資源，以便小組可以解決商務問題使用 microservices 方法。***

Service Fabric 提供三個主要 toohelp 您建置應用程式，請使用 microservices 方法：

* 提供系統服務 toodeploy，平台升級、 偵測，並重新啟動失敗的服務探索服務、 將訊息路由、 狀態，和監視健全狀況。 這些系統服務作用中實現許多 hello 特性 microservices 先前所述。
* 在容器中，或做為任一個執行的處理能力 toodeploy 應用程式。 Service Fabric 是一個容器和處理序協調者。
* 高生產力程式設計 Api，您建置應用程式為 microservices toohelp: [ASP.NET Core、 Reliable Actors 和可靠的服務](service-fabric-choose-framework.md)。 您可以選擇任何程式碼 toobuild 您的微服務。 但是這些 Api，讓 hello 工作更簡單，而且它們與更深層級的 hello 平台整合。 例如，您可以取得健康狀態和診斷資訊，或利用內建的高可用性。

***Service Fabric 不會限制您建置服務的方式，您可以使用任何技術。不過，它提供內建的程式設計 Api，讓您更輕鬆 toobuild microservices。***

### <a name="migrating-existing-applications-tooservice-fabric"></a>移轉現有的應用程式 tooService 網狀架構
索引鍵方法 tooService 網狀架構是 tooreuse 現有程式碼，然後可以使用新 microservices 現代化。 有五個階段 tooapplication 現代化，而且您可以啟動及停止在任何 hello 階段。 這些階段包括：

1) 選擇一個傳統單體式應用程式
2) 提起並移位-用於 Service Fabric 的容器或客體可執行檔 toohost 現有程式碼。
3) 現代化 - 在現有的容器化程式碼之外，再加上新的微服務。 
4) 創新-中斷 hello 龐大 microservices 單純地根據需求。
5) 轉換成 microservices-hello 轉換現有的整合應用程式，或建立新的 「 綠地應用程式。

![移轉 tooMicroservices][Image3]

它是重要 tooemphasis 同樣地，您可以**啟動及停止在任何這些階段**，您不是被迫 toomoved toohello 下一個階段。 現在，讓我們看看這每一個階段的範例。

**遷移**-會提升大量的公司和移位到容器 toofor 整合的現有應用程式的兩個原因;

- 可能是因為 tooconsolidation 和移除的現有硬體或執行的應用程式在更高的密度的降低成本。 
- 開發與作業之間的一致性部署合約。

成本大幅降低是容易了解，在 Microsoft 內會大量的現有應用程式容器化只要 toomillions 的 （美元）。 一致的部署是更難 tooevaluate，但同樣重要。 該處會指示開發人員可能仍為可用 toochoose hello 技術，該套件它們，不過 hello 作業只會接受單一方式 toodeploy 並管理這些應用程式。 它可減輕 hello 作業不需要的許多不同技術的 hello 複雜度 toodeal 或強制執行開發人員 tooonly 選擇特定的。 基本上，每個應用程式都會透過容器化成為獨立性部署映像。

許多組織都在此停止。 他們已經有容器的 hello 優點，Service Fabric 提供 hello 完整管理體驗，包括部署、 升級、 版本控制、 復原等健全狀況監視。

**現代化**-是新的服務，與現有的容器化程式碼一起 hello 新增。 如果您正在 toowrite 新的程式碼，則最佳 toodecide tootake 小步驟 hello microservices 路徑。 這可能是新增新的 REST API 端點，或是新的商務邏輯。 如此一來，您會開始建置新 microservices 和開發和部署的 hello 旅。

**創新**-請記住這些原始多變的商務需求在 hello 開頭的本文中，隨著驅使 hello microservices 方法？ 在此階段 hello 決策是，這些狀況 toomy 目前應用程式，而且如果是，我需要 toostart 分割 hello monolith 或開創電腦科技。 這裡的其中一個範例，就是當資料庫因為作為工作流程佇列而變成處理瓶頸的時候。 做為工作流程的 hello 數增加 hello 的要求運作需求 toobe 發佈適用於小數位數。 因此 hello 應用程式不該特定部分的縮放比例，或您需要 tooupdate 多經常時分割成微服務及創新。 

**轉換成微服務** - 這是應用程式完全由微服務構成 (或解構成微服務) 的階段。 tooreach 這裡，您所做 hello microservices 旅程。 您可以從這裡開始，但 toodo 這 microservices 平台 toohelp 不是大量投資。 

### <a name="are-microservices-right-for-my-application"></a>微服務適合我的應用程式嗎？
可能。 我們的體驗已隨著 Microsoft 越來越多的小組開始 toobuild hello 雲端針對商業用途，其中許多實現 hello 優點採用類似微服務的方法。 例如，Bing 多年來一直在開發搜尋方面的微服務。 對於其他小組，hello microservices 方法，就是新。 小組發現了艱難問題 toosolve 強度核心範圍之外。 這就是為什麼 Service Fabric 獲得從此以後做選擇，來建置服務的 hello 技術。

Service Fabric hello 目標 tooreduce hello 的微服務方法使用建置應用程式變得複雜，許多最密切相關，所以您不需要為透過 toogo redesigns。 從小型專案開始和調整其規模需要時，服務已被取代，加入新的發展與客戶使用量是 hello 方法。 我們也會知道，還有許多其他問題 toobe 解決大部分的開發人員更容易實行 toomake microservices。 容器和 hello 執行者程式設計模型是小步驟，在該方向中的範例，而且我們確定的更多的創新便會浮現 toomake 這更容易。
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>後續步驟
* [Service Fabric 術語概觀](service-fabric-technical-overview.md)
* [Microservices： 由 hello 雲端應用程式 revolution](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
