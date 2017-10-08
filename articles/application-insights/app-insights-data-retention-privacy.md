---
title: "aaaData 保留和儲存在 Azure Application Insights |Microsoft 文件"
description: "保留和隱私權原則聲明"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Application Insights 中的資料收集、保留和儲存


當您安裝[Azure Application Insights] [ start] SDK 在應用程式中的，它會傳送有關您的應用程式 toohello 雲端的遙測。 當然，負責的開發人員會想 tooknow 完全傳送的資料，會發生什麼事 toohello 資料和它們如何讓它的控制項。 特別是，是否可能傳送敏感資料？資料儲存於何處？其安全性為何？ 

首先，hello 簡短的答案：

* 執行 「 立即可用 hello"的 hello 標準遙測模組是不太可能 toosend 敏感性資料 toohello 服務。 hello 遙測被關於負載、 效能和使用計量、 例外狀況報告和其他診斷資料。 hello hello 診斷報告中顯示的主要使用者資料是 Url。但是，您的應用程式不應該在任何情況下將敏感資料放在 URL 中的純文字。
* 您可以撰寫程式碼會傳送其他的自訂遙測 toohelp 您診斷和監視的使用方式。 (此擴充性是 Application Insights 的絕佳功能之一)。它是可行的錯誤、 toowrite 此程式碼，使其包含個人和其他機密資料。 如果您的應用程式會使用這類資料，您應該套用徹底檢閱處理程序 tooall hello 您撰寫程式碼。
* 同時開發和測試您的應用程式時，很容易 tooinspect 什麼正在傳送的 hello SDK。 hello 資料會出現在偵錯輸出的 hello IDE 和瀏覽器的 windows hello。 
* hello 資料保存在[Microsoft Azure](http://azure.com) hello 美國或歐洲的伺服器。 (但是您的 App 可以在任何地方執行)。Azure 有[嚴密的安全性程序，並符合各種法規遵循標準](https://azure.microsoft.com/support/trust-center/)。 只有您和您指定的小組有存取 tooyour 資料。 Microsoft 人員可以有限制存取 tooit 只能在特定限制的情況下與您的知識。 即使未在 hello 伺服器，它會加密傳輸中。

hello 本文其餘部分會更完整 elaborates 上上述問題的答案。 它設計 toobe 各自獨立，以便您可以將其顯示 toocolleagues 管理員不是立即小組的一部分。

## <a name="what-is-application-insights"></a>什麼是 Application Insights？
[Azure 的 Application Insights] [ start]是可協助您的 Microsoft 所提供之服務改善 hello 效能和可用性的即時應用程式。 它會監視您的應用程式它正在執行，在測試期間和之後您已經發行或部署它的所有 hello 時間。 Application Insights 建立圖表和顯示您的資料表，例如，每天何時取得大部分的使用者，方式是回應 hello 應用程式，以及如何也由任何外部服務，這取決於。 如果損毀、 失敗或效能問題，您可以搜尋，透過詳細 toodiagnose hello 原因 hello 遙測資料。 而 hello 服務會傳送您的電子郵件是否有 hello 可用性和效能的應用程式中的任何變更。

在順序 tooget 這項功能，您會安裝 Application Insights SDK 在應用程式中，這會成為其程式碼的一部分。 當您的應用程式執行時，hello SDK 監視其作業，並傳送遙測 toohello Application Insights 服務。 這是由 [Microsoft Azure](http://azure.com)裝載的雲端服務。 (但 Application Insights 適用於任何應用程式，而不只是 Azure 中裝載的應用程式)。

![在您的應用程式中的 hello SDK 傳送遙測 toohello Application Insights 服務。](./media/app-insights-data-retention-privacy/01-scheme.png)

hello Application Insights 服務儲存及分析 hello 遙測。 toosee hello 分析或搜尋 hello 儲存遙測，您登入 tooyour Azure 帳戶並開啟 hello Application Insights 資源的應用程式。 您也可以共用存取 toohello 資料與您小組的其他成員或指定的 Azure 訂閱者。

您可以從 hello Application Insights 服務匯出的資料，例如 tooa 資料庫或 tooexternal 工具。 您會將每項工具提供您從 hello 服務取得的特殊按鍵。 如有必要，可以撤銷 hello 索引鍵。 

Application Insights Sdk 會使用應用程式類型的範圍： web 服務裝載於自己 J2EE 或 ASP.NET 的伺服器，或在 Azure 中。web 用戶端-也就是執行網頁; 中的 hello 程式碼桌面應用程式和服務。例如 Windows Phone、 iOS 和 Android 的裝置應用程式。 在所有傳送遙測 toohello 相同的服務。

## <a name="what-data-does-it-collect"></a>它會收集哪些資料？
### <a name="how-is-hello-data-is-collected"></a>收集的 hello 資料的方式為何？
來源資料共有三種：

* hello SDK，請與您的應用程式整合[開發](app-insights-asp-net.md)或[在執行階段](app-insights-monitor-performance-live-website-now.md)。 不同的應用程式類型有不同的 SDK。 另外還有[SDK 的 web 網頁](app-insights-javascript.md)，載入至 hello 頁面以及 hello 使用者的瀏覽器。
  
  * 每一套 SDK 有一些[模組](app-insights-configuration-with-applicationinsights-config.md)，會使用不同的技術 toocollect 不同類型的遙測資料。
  * 如果您在開發安裝 hello SDK，您可以使用其應用程式開發介面 toosend 您自己的遙測，加法 toohello 標準模組內。 這個自訂的遙測可以包含您想要 toosend 任何資料。
* 在某些網頁伺服器，也有一些與 hello 應用程式一起執行，並傳送有關 CPU、 記憶體和網路的佔用量遙測代理程式。 例如，Azure VM、Docker 主機和 [J2EE 伺服器](app-insights-java-agent.md) 都可能有這類代理程式。
* [可用性測試](app-insights-monitor-web-app-availability.md)會定期傳送要求 tooyour web 應用程式的 Microsoft 所執行的處理序。 hello 結果會傳送 toohello Application Insights 服務。

### <a name="what-kinds-of-data-are-collected"></a>會收集哪些類型的資料？
hello 主要類別如下：

* [Web 伺服器遙測](app-insights-asp-net.md) - HTTP 要求。  Uri，花費時間 tooprocess hello 要求、 回應程式碼、 用戶端 IP 位址。 工作階段識別碼。
* [網頁](app-insights-javascript.md) - 頁面、使用者和工作階段計數。 頁面載入時間。 例外狀況。 Ajax 呼叫。
* 效能計數器 - 記憶體、CPU、IO、網路佔用量。
* 用戶端和伺服器內容 - OS、地區設定、裝置類型、瀏覽器和螢幕解析度。
* [例外狀況](app-insights-asp-net-exceptions.md) 和當機 - **堆疊傾印**、組建識別碼、CPU 類型。 
* [相依性](app-insights-asp-net-dependencies.md)-呼叫 REST，SQL、 AJAX 等 tooexternal 服務。 URI 或連接字串、持續時間、成功、命令。
* [可用性測試](app-insights-monitor-web-app-availability.md) - 測試的持續時間、步驟、回應。
* [追蹤記錄檔](app-insights-asp-net-trace-logs.md)和[自訂遙測](app-insights-api-custom-events-metrics.md) - **任何您以程式碼撰寫到記錄檔或遙測中的項目**。

[詳細資訊](#data-sent-by-application-insights)。

## <a name="how-can-i-verify-whats-being-collected"></a>如何確認收集到什麼？
如果您正在開發使用 Visual Studio 中，執行 hello 應用程式中偵錯 (F5) 模式中的 hello 應用程式。 hello 遙測會顯示 hello [輸出] 視窗中。 在這裡，您可以將其複製並格式化為 JSON，以便進行檢查。 

![](./media/app-insights-data-retention-privacy/06-vs.png)

另外還有更容易閱讀檢視中 hello 診斷視窗。

針對網頁，請開啟瀏覽器的偵錯視窗。

![按下 f12 鍵，然後開啟 hello 網路 索引標籤。](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>傳送之前可以撰寫程式碼 toofilter hello 遙測？
這可以藉由撰寫 [遙測處理器外掛程式](app-insights-api-filtering-sampling.md)來達成。

## <a name="how-long-is-hello-data-kept"></a>Hello 資料保存的時間？
向上 too90 天會保存原始資料點 （也就是項目，就可以在分析中查詢，然後在搜尋中檢查）。 如果您需要超過 tookeep 資料時，您可以使用[連續匯出](app-insights-export-telemetry.md)toocopy 它 tooa 儲存體帳戶。

彙總的資料 (也就是您在計量瀏覽器中看到的計數、平均和其他統計資料) 在 1 分鐘的資料粒度中保存 90 天。

## <a name="who-can-access-hello-data"></a>誰可以存取 hello 資料？
hello 資料是可見的 tooyou 而且，如果您有組織帳戶，您的小組成員。 

它可以匯出由您和您的小組成員可能是複製的 tooother 位置，並傳遞 tooother 人員。

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Microsoft 的作用是 hello 資訊與我的應用程式傳送 tooApplication Insights？
Microsoft 會使用僅在順序 tooprovide hello 服務 tooyou hello 資料。

## <a name="where-is-hello-data-held"></a>Hello 資料保留在何處？
* Hello 美國或歐洲。 當您建立新的 Application Insights 資源，您可以選取 hello 位置。 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>這表示我的應用程式已裝載於美國或歐洲 hello toobe 嗎？
* 否。 您的應用程式可以執行任何位置，在內部部署主機中或在 hello 雲端中。

## <a name="how-secure-is-my-data"></a>我的資料有多安全？
Application Insights 是一項 Azure 服務。 安全性原則所述 hello [Azure 安全性、 隱私權和相容性的技術白皮書](http://go.microsoft.com/fwlink/?linkid=392408)。

hello 資料會儲存在 Microsoft Azure 的伺服器。 Hello Azure 入口網站中的帳戶，帳戶的限制詳述於 hello [Azure 安全性、 隱私權和相容性文件](http://go.microsoft.com/fwlink/?linkid=392408)。

存取 tooyour 資料由 Microsoft 人員會受到限制。 我們存取您的資料只能搭配您的權限，以及是否可以必要 toosupport 貴用戶使用 Application Insights。 

使用的 tooimprove Application Insights 中跨所有客戶的應用程式 （例如資料速率和追蹤的平均大小） 的彙總的資料。

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>其他人的遙測是否會干擾我的 Application Insights 資料？
他們可以傳送其他遙測 tooyour 帳戶使用 hello 檢測金鑰，可以在 hello 的 web 網頁的程式碼中找到。 有足夠的額外資料，您的計量將不會正確地代表您應用程式的效能和使用方式。

如果您與其他專案共用程式碼，請記得 tooremove 檢測金鑰。

## <a name="is-hello-data-encrypted"></a>Hello 資料加密？
不是在目前的 hello 伺服器內。

所有資料在資料中心之間移動時會予以加密。

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>從我的應用程式 tooApplication Insights 伺服器傳輸中加密的 hello 資料？
是，我們會使用 https toosend 資料 toohello 入口網站幾乎所有的 sdk，包括網頁伺服器、 裝置及 HTTPS 的網頁。 hello 唯一的例外狀況是從純 HTTP 網頁傳送資料。 

## <a name="personally-identifiable-information"></a>個人識別資訊
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>個人識別資訊 (PII) 則會傳送 tooApplication Insights？
是，可以的。 

一般指引為：

* 大部分的標準遙測 (即，在未撰寫任何程式碼的情況下所傳送的遙測) 都不包括明確的 PII。 不過，可能很可能 tooidentify 個人所推斷的事件集合。
* 例外狀況和追蹤訊息可能包含 PII
* 自訂遙測-也就是呼叫您在使用 hello 應用程式開發介面或記錄檔追蹤程式碼中撰寫的 TrackEvent 例如-可以包含任何您選擇的資料。

在這份文件的 hello 結尾處的 hello 資料表包含詳細的描述 hello 所收集的資料。

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>我責任遵從出口法規之限制而考慮 tooPII 中？
是。 它是您的責任 tooensure hello 收集與使用 hello 資料符合法律和規定與 hello Microsoft 線上服務合約。

您應該適當地通知您的客戶，有關 hello 資料會收集您的應用程式，以及如何使用 hello 資料。

#### <a name="can-my-users-turn-off-application-insights"></a>我的使用者是否可以關閉 Application Insights？
無法直接進行。 我們不提供一個交換器，您的使用者可以操作 tooturn 關閉 Application Insights。

不過，您可以在應用程式中實作這類功能。 所有 hello Sdk 都包含一個應用程式開發介面設定，會關閉遙測收集。 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>我的應用程式不小心收集到機密資訊。 Application Insights 是否可以刪除此資料，不予保留？
Application Insights 不會篩選或刪除資料。 您應該適當地管理 hello 資料，並避免傳送這類資料 tooApplication 深入資訊。

## <a name="data-sent-by-application-insights"></a>Application Insights 所傳送的資料
hello Sdk 平台，而有所不同，而且有數個元件可以安裝。 (請參閱太[Application Insights-概觀][start]。)每個元件都會傳送不同的資料。

#### <a name="classes-of-data-sent-in-different-scenarios"></a>不同情況下所傳送資料的類別
| 您的動作 | 收集的資料類別 (請參閱下一個資料表) |
| --- | --- |
| [新增 Application Insights SDK tooa.NET web 專案][greenbrown] |ServerContext<br/>推斷<br/>效能計數器<br/>要求<br/>**例外狀況**<br/>工作階段<br/>users |
| [在 IIS 上安裝狀態監視器][redfield] |相依項目<br/>ServerContext<br/>推斷<br/>效能計數器 |
| [加入 Application Insights SDK tooa Java web 應用程式][java] |ServerContext<br/>推斷<br/>要求<br/>工作階段<br/>users |
| [加入 JavaScript SDK tooweb 頁面][client] |ClientContext  <br/>推斷<br/>Page<br/>ClientPerf<br/>Ajax |
| [定義預設屬性][apiproperties] |**屬性**  |
| [呼叫 TrackMetric][api] |數值<br/>**屬性** |
| [呼叫 Track*][api] |事件名稱<br/>**屬性** |
| [呼叫 TrackException][api] |**例外狀況**<br/>堆疊傾印<br/>**屬性** |
| SDK 無法收集資料。 例如： <br/> - 無法存取效能計數器<br/> - 遙測初始設定式中發生例外狀況 |SDK 診斷 |

如需[適用於其他平台的 SDK][platforms]，請參閱其文件。

#### <a name="hello-classes-of-collected-data"></a>所收集的資料的 hello 類別
| 收集的資料類別 | 包含 (不是詳盡的清單) |
| --- | --- |
| **屬性** |**任何資料 - 取決於您的程式碼** |
| DeviceContext |識別碼、IP、地區設定、裝置型號、網路、網路類型、OEM 名稱、螢幕解析度、角色執行個體、角色名稱、裝置類型 |
| ClientContext  |作業系統、地區設定、語言、網路、視窗解析度 |
| 工作階段 |工作階段識別碼 |
| ServerContext |電腦名稱、地區設定、作業系統、裝置、使用者工作階段、使用者內容、作業 |
| 推斷 |從 IP 位址的地區位置、時間戳記、作業系統、瀏覽器 |
| 度量 |計量名稱和值 |
| 事件 |事件名稱和值 |
| PageViews |URL 和頁面名稱或螢幕名稱 |
| 用戶端效能 |URL/頁面名稱、瀏覽器載入時間 |
| Ajax |從網頁 tooserver HTTP 呼叫 |
| Requests |URL、持續時間、回應碼 |
| 相依性 |類型 (SQL、HTTP、...)、連接字串或 URI、同步/非同步、持續時間、成功、SQL 陳述式 (含狀態監視器) |
| **例外狀況** |類型、 **訊息**、呼叫堆疊、來源檔案和行號、執行緒識別碼 |
| 損毀 |處理序識別碼、父處理序識別碼、損毀執行緒識別碼；應用程式修補程式、識別碼、組建；例外狀況類型、位址、原因；模糊符號和暫存器、二進位開始和結束位址、二進位檔名稱和路徑、CPU 類型 |
| 追蹤 |**訊息** 和嚴重性層級 |
| 效能計數器 |處理器時間、可用記憶體、要求率、例外狀況率、處理序私用位元組、IO 率、要求持續期間、要求佇列長度 |
| Availability |Web 測試回應程式碼、每個測試步驟的持續時間、測試名稱、時間戳記、成功、回應時間、測試位置 |
| SDK 診斷 |追蹤訊息或例外狀況 |

您可以[藉由編輯 ApplicationInsights.config 關閉某些 hello 資料][config]

## <a name="credits"></a>學分
此產品包含由 MaxMind 建立的 GeoLite2 資料，可從 [http://www.maxmind.com](http://www.maxmind.com)取得。



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

