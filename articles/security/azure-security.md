---
title: "aaaIntroduction tooAzure 安全性 |Microsoft 文件"
description: "了解 Azure 安全性、它的服務及運作方式。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>簡介 tooAzure 安全性
## <a name="overview"></a>概觀
我們知道安全性是 hello 定域機組中的其中一個工作，而且重要，您會看到 Azure 安全性的精確且即時資訊。 Tootake 利用其廣泛的安全性工具和功能的其中一個 hello 最佳原因 toouse Azure 應用程式與服務。 這些工具和功能協助您更 hello 安全 Azure 平台上可能 toocreate 安全解決方案。 Microsoft Azure 提供客戶資料的機密性、完整性和可用性，同時也能釐清責任。

深入了解從 hello 客戶和 Microsoft operations' 檢視方塊，這份技術白皮書，"簡介 tooAzure 安全性 」，在 Microsoft Azure 內實作的安全性控制項的集合，hello toohelp 寫入 tooprovide在適用於 Microsoft Azure 的 hello 安全性的詳細討論。

### <a name="azure-platform"></a>Azure 平台
Azure 是一個公用雲端服務平台，支援廣泛的作業系統、程式設計語言、架構、工具、資料庫及裝置等選擇。 它可以透過 Docker 整合執行 Linux 容器；使用 JavaScript、Python、.NET、PHP、Java 及 Node.js 建置應用程式；為 iOS、Android 及 Windows 裝置建置後端。

Azure 公用雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。 當您建置，或移轉到 IT 資產時，您依賴該組織的能力 tooprotect 應用程式和 hello 服務與 hello 控制項資料的公用雲端服務提供者提供 toomanage hello 安全性您雲端架構資產。

從裝載吸引數百萬的客戶同時設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。

此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂的組織部署的安全性 toomeet hello 獨特需求。 本文件有助於您了解 Azure 安全性功能如何協助您滿足這些需求。

> [!Note]
> 本文件 hello 主要焦點在於是客戶對向控制項上，您可以使用 toocustomize 和提高安全性，您的應用程式和服務。
>
> 我們提供一些概觀資訊，但詳細資訊，Microsoft 如何保護 hello Azure 平台本身，請參閱 hello 中提供的資訊[Microsoft 信任中心](https://www.microsoft.com/TrustCenter/default.aspx)。

### <a name="abstract"></a>摘要
一開始，公用雲端移轉所驅動的成本節約和靈活度 tooinnovate。 經過一段時間之後，才將安全性視為公用雲端移轉的主要考量，甚至是個關鍵因素。 不過，公用雲端安全性已從轉換主要考量 tooone hello 雲端移轉驅動程式。 hello 這背後的基本原理是大型的公用雲端服務提供者 tooprotect 應用程式的 hello 上層能力和以雲端為基礎的資產 hello 資料。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂安全性 toomeet hello 獨特需求的部署 toomeet 您的 IT 控制原則，並遵循 tooexternal法規。

本文列出 Microsoft 方法 toosecurity 內 hello Microsoft Azure 雲端平台：
* Microsoft toosecure hello Azure 基礎結構、 客戶資料和應用程式所實作的安全性功能。
* Azure 服務和安全性功能使用 tooyou toomanage hello hello 服務與您 Azure 訂用帳戶中的資料的安全性。

## <a name="summary-azure-security-capabilities"></a>Azure 安全性功能摘要
hello 資料表下列提供 Microsoft toosecure hello Azure 基礎結構、 客戶資料及安全的應用程式所實作的 hello 安全性功能的簡短描述。
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>安全性實作的功能 tooSecure hello Azure 平台：
hello 功能列出下列是您可以檢閱 tooprovide hello 保證 Azure 平台以安全的方式管理該 hello 的功能。 其中提供了連結，讓您可以進一步深入了解 Microsoft 如何在下列四個領域中處理客戶信任問題：安全的平台、隱私權與控制、合規性及透明度。


| [安全的平台](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [隱私權與控制](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[合規性](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [透明度](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [安全性開發週期 (英文)](https://www.microsoft.com/en-us/sdl/)、內建稽核 | [管理您的資料 hello world](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [信任中心](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Microsoft 如何保護 Azure 服務中的客戶資料 (英文)](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [必要的安全性訓練、背景檢查 (英文)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [資料位置控制 (英文)](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Common Controls Hub (英文)](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Microsoft 如何管理 Azure 服務中的資料位置 (英文)](http://azuredatacentermap.azurewebsites.net/)|
| [滲透測試 (英文)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc)、[入侵偵測、DDoS (英文)](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen)、[稽核和記錄(英文)](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [根據您的條款提供資料存取 (英文)](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [hello 雲端服務到期勤加注意檢查清單](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Microsoft 內部的哪些人員可根據哪些條款存取您的資料 (英文)](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [技術資料中心的狀態 (英文)](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)、實體安全性、[安全網路](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [回應 toolaw 強制](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [依服務、位置和產業的合規性 (英文)](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Microsoft 如何保護 Azure 服務中的客戶資料 (英文)](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [安全性事件回應 (英文)](http://aka.ms/SecurityResponsepaper)[共同責任 (英文)](http://aka.ms/sharedresponsibility) |[嚴格的隱私權標準 (英文)](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [檢閱 Azure 服務的憑證、透明度中樞 (英文)](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>由 Azure tooSecure 資料所提供的安全性功能和應用程式
根據 hello 雲端服務模型時，沒有變數責任的人員必須負責管理 hello hello 應用程式或服務的安全性。 沒有 hello Azure 平台 tooassist 您滿足這些責任透過內建功能，以及透過合作夥伴可以部署到 Azure 訂用帳戶的解決方案中提供的功能。

hello 內建功能分成六個 （6） 功能區域： 作業、 應用程式、 儲存體、 網路、 運算及身分識別。 Hello 特色與功能用於 hello 這些六 （6） 區域中的 Azure 平台上的其他詳細資料提供摘要資訊。

## <a name="operations"></a>作業
本節提供關於安全性作業中主要功能的其他資訊，以及這些功能的摘要資訊。

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Operations Management Suite 安全性與稽核儀表板
hello [OMS 安全性和稽核 」 解決方案](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started)讓您完整檢視您組織的 IT 安全性狀況與[內建的搜尋查詢](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/)針對值得您注意的問題。 hello[安全性和稽核](https://technet.microsoft.com/library/mt484091.aspx)儀表板是所有項目 hello 主畫面相關 toosecurity 在 OMS 中的。 它提供高層級深入了解 hello 在電腦的安全性狀態。 它也包含 hello 能力 tooview hello 過去 24 小時、 7 天的所有事件或任何其他自訂的時間範圍。

此外，您可以設定 OMS 安全性和規範太[自動執行特定動作](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/)偵測到特定事件時。

### <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure 資源管理員](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model)可讓您與您的解決方案，為群組中的 hello 資源 toowork。 您可以部署、 更新或刪除您的解決方案是單一的協調作業，在 hello 的所有資源。 您會使用 [Azure Resource Manager 範本 (英文)](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) 部署，該範本可用於不同的環境，例如測試、預備和生產環境。 資源管理員提供安全性、 稽核和標記功能 toohelp 部署後管理您的資源。

Azure 資源管理員範本為基礎的部署協助改善的方案，因為標準的安全性控制設定，而且可以在 Azure 中部署的 hello 安全性整合到標準化範本為基礎的部署。 這可降低 hello 風險可能需要進行手動部署期間的安全性組態錯誤。

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) 是適用於 Web 開發人員的可延伸「應用程式效能管理」(APM) 服務。 使用 Application Insights，您可以即時監視 Web 應用程式，並自動偵測效能異常。 它包括強大的分析工具 toohelp 您診斷問題和 toounderstand 哪些使用者實際執行應用程式。 它會監視您的應用程式它正在執行，在測試期間和之後您已經發行或部署它的所有 hello 時間。

Application Insights 建立圖表和顯示您的資料表，例如，每天何時取得大部分的使用者，方式是回應 hello 應用程式，以及如何也由任何外部服務，這取決於。

如果損毀、 失敗或效能問題，您可以搜尋，透過詳細 toodiagnose hello 原因 hello 遙測資料。 和 hello 服務會傳送給您電子郵件是否有 hello 可用性和效能的應用程式中的任何變更。 Application Insight 因此變成重要的安全性工具，因為它可協助在 hello 機密性、 完整性和可用性安全性三角理論的 hello 可用性。

### <a name="azure-monitor"></a>Azure 監視器
[Azure 監視](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)從 hello Azure 基礎結構提供視覺效果、 查詢、 路由、 警示、 自動調整規模及自動化這兩個資料 ([活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) 和每個個別的 Azure 資源 ([診斷記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs))。 您可以使用 Azure 監視器 tooalert 您在 Azure 記錄檔中產生的安全性相關事件。

### <a name="log-analytics"></a>Log Analytics
[記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)屬於[Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) – 提供 IT 管理解決方案的內部和協力廠商雲端基礎結構 （例如 AWS) 此外 tooAzure 資源。 從 Azure 監視的資料可以路由傳送直接 tooLog 分析，以便您可以看到在同一個地方整個環境度量和記錄檔。

記錄分析可在資料安全相當有用的工具和其他安全性分析 hello 工具可讓您 tooquickly 搜尋大量的彈性查詢方法的安全性相關項目。 此外，內部部署的[防火牆和 Proxy 記錄可匯出到 Azure，並使用 Log Analytics 來分析它們。](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure 建議程式
[Azure Advisor](https://docs.microsoft.com/azure/advisor/)是 toooptimize 可協助您的個人化的雲端顧問您的 Azure 部署。 它會分析您的資源及用量遙測， 然後它會建議解決方案 toohelp 改善 hello[效能](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations)，[安全性](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations)，和[高可用性](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations)資源太尋找商機時的[減少整體 Azure 花](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations)。 Azure Advisor 提供安全性建議，讓您能夠大幅改善您部署於 Azure 中之解決方案的整體安全性狀態。 這些建議均取自 [Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)所執行的安全性分析。

### <a name="azure-security-center"></a>Azure 資訊安全中心
[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)幫助您防止、 偵測，並以進一步掌握回應 toothreats 及控制 hello 您的 Azure 資源的安全性。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

此外，Azure 資訊安全中心可協助進行安全性作業，方法是提供單一儀表板來顯示可立即採取行動的警示和建議。 通常，您可以補救問題，只要按一下 hello Azure 資訊安全中心主控台內。
## <a name="applications"></a>應用程式
hello > 一節提供有關這些功能的應用程式安全性和摘要資訊中的主要功能有關的其他資訊。

### <a name="web-application-vulnerability-scanning"></a>Web 應用程式弱點掃描
其中一個最簡單方式 tooget hello 入門測試的弱點可能會在您[App Service 應用程式](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)為 toouse hello[與 Tinfoil Security 整合](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)tooperform 單鍵弱點上的掃描您的應用程式。 您可以在容易瞭解報表中，檢視 hello 測試結果，並了解如何 toofix 每項弱點的逐步指示。

### <a name="penetration-testing"></a>滲透測試
如果您偏好 tooperform 自己滲透測試，或想 toouse，另一個掃描器套件或提供者，您必須依照 hello [Azure 滲透測試核准程序](https://security-forms.azure.com/penetration-testing/terms)並取得預先核准 tooperform hello 預期入侵測試。

### <a name="web-application-firewall"></a>Web 應用程式防火牆
在 hello web 應用程式防火牆 (WAF) [Azure 應用程式閘道](https://azure.microsoft.com/services/application-gateway/)協助保護 web 應用程式從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段攔截。 它會從 hello 所識別的威脅保護預先設定[開啟 Web 應用程式安全性專案 (OWASP) 為 hello 前 10 個常見弱點](https://msdn.microsoft.com/library/)。

### <a name="authentication-and-authorization-in-azure-app-service"></a>Azure App Service 中的驗證與授權
[應用程式服務驗證 / 授權](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)是使用者在您的應用程式 toosign 提供一個方法，因此 hello 應用程式後端沒有 toochange 程式碼的功能。 提供簡單的方式 tooprotect 應用程式和工作每個使用者資料。

### <a name="layered-security-architecture"></a>分層式安全性架構
由於 [App Service 環境](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro)提供部署至 [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)的隔離執行階段環境，因此開發人員能夠建立分層式安全性架構，針對每個應用程式層提供不同層級的網路存取。 常見的 desire toohide API 的後端從一般的網際網路存取，並只允許由上游的 web 應用程式呼叫 Api toobe。 [網路安全性群組 (Nsg)](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)可以包含應用程式服務環境 toorestrict 公用存取 tooAPI 應用程式的 Azure 虛擬網路子網路上使用。

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Web 伺服器診斷和應用程式診斷
App Service web 應用程式提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷的功能。 這些資訊邏輯上可區分為 [Web 伺服器診斷](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log)與[應用程式診斷](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx)。 Web 伺服器在針對網站和應用程式進行診斷及疑難排解方面包含了兩個重大進展。

hello 第一項新功能是關於應用程式集區、 工作者處理序、 網站、 應用程式定義域和執行要求的即時狀態資訊。 hello 第二個新的優點是 hello 詳細的追蹤事件可追蹤整個 hello 完整要求和回應程序的要求。

tooenable hello 集合，這些追蹤事件，IIS 7 可以設定的 tooautomatically 擷取完整追蹤記錄檔，以 XML 格式，針對任何特定的要求，根據經歷時間或錯誤回應碼。

#### <a name="web-server-diagnostics"></a>Web 伺服器診斷
您可以啟用或停用下列種類的記錄檔的 hello:

-   詳細的錯誤記錄：對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。 這可能包含可協助您判斷為什麼 hello 伺服器傳回 hello 錯誤碼的資訊。

-   失敗的要求追蹤的詳細資訊，失敗的要求，包括 hello IIS 使用的元件 tooprocess hello 要求和取得每個元件中的 hello 時間的追蹤。 如果您正嘗試 tooincrease 站台效能或隔離造成特定的 HTTP 錯誤 toobe 傳回時，這可能會很有用。

-   Web 伺服器記錄-HTTP 交易使用 hello W3C 擴充的記錄檔格式的相關資訊。 判斷整體站台的度量資訊，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時，這非常有用。

#### <a name="application-diagnostics"></a>應用程式診斷
[應用程式診斷](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log)可讓您的 web 應用程式所產生的 toocapture 資訊。 ASP.NET 應用程式可以使用 hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)類別 toolog 資訊 toohello 應用程式診斷記錄。 在 Application Diagnostics 中有兩個主要事件類型的事件，這些相關 tooapplication 效能和那些相關 tooapplication 失敗和錯誤。 hello 失敗和錯誤可以再細分為連線、 安全性和失敗的問題。 失敗的問題是 hello 應用程式程式碼通常相關的 tooa 問題。

在應用程式診斷中，您可以檢視以下列方式分組的事件：

-   全部 (顯示所有事件)
-   應用程式錯誤 (顯示例外狀況事件)
-   效能 (顯示效能事件)

## <a name="storage"></a>儲存體
hello > 一節提供有關這些功能的 Azure 儲存體安全性和摘要資訊中的主要功能有關的其他資訊。

### <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
您可以使用角色型存取控制 (RBAC) 來保護儲存體帳戶。 限制存取根據 hello[需要 tooknow](https://en.wikipedia.org/wiki/Need_to_know)和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則是命令式 tooenforce 安全性原則所需的資料存取的組織。 這些存取權限會授與指定適當 RBAC 角色 toogroups hello 與應用程式在特定範圍內。 您可以使用[內建的 RBAC 角色](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles)，例如儲存體帳戶參與者 tooassign 權限 toousers。 存取儲存體帳戶使用 hello toohello 儲存體金鑰[Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide)模型可以由角色型存取控制 (RBAC)。

### <a name="shared-access-signature"></a>共用存取簽章
A[共用的存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)提供儲存體帳戶中的委派的存取 tooresources。 hello SAS 表示您可以授與用戶端有限的權限 tooobjects 在儲存體帳戶在指定期間內，並與指定權限集。 您可以授與這些有限權限，而不需要 tooshare 帳戶存取金鑰。

### <a name="encryption-in-transit"></a>傳輸中加密
傳輸中加密是透過網路傳輸資料時用來保護資料的機制。 透過 Azure 儲存體，您可以使用下列各項來保護資料：
-   [傳輸層級加密](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit)，例如從 Azure 儲存體傳入或傳出資料時的 HTTPS。

-   [連線加密](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares)，例如 [Azure 檔案共用](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files)的 [SMB 3.0 加密](https://docs.microsoft.com/azure/storage/storage-security-guide)。

-   用戶端加密、 tooencrypt hello 資料傳輸到儲存體之前和之後傳送超出儲存體的 toodecrypt hello 資料。

### <a name="encryption-at-rest"></a>待用加密
對許多組織來說，待用資料加密是達到資料隱私權、合規性及資料主權的必要步驟。 有三個 Azure 儲存體安全性功能可提供「待用」資料的加密：

-   [儲存體服務加密](https://docs.microsoft.com/azure/storage/storage-service-encryption)可讓您 toorequest 寫入它 tooAzure 儲存體時，hello 儲存體服務會自動加密資料。

-   [用戶端加密](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)也提供的加密在靜止 hello 功能。

-   [Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器所使用的資料磁碟。

### <a name="storage-analytics"></a>儲存體分析
[Azure 儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)會執行記錄，並提供儲存體帳戶的計量資料。 您可以使用此資料 tootrace 要求、 分析使用趨勢，以及診斷儲存體帳戶的問題。 儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。 這項資訊可以使用的 toomonitor 個別要求和 toodiagnose 與儲存體服務的問題。 系統會以最佳方式來記錄要求。 會記錄下列類型的驗證要求的 hello:
-   成功的要求。

-   失敗的要求，包括逾時、節流、網路、授權和其他錯誤。

-   使用共用存取簽章 (SAS) 的要求，包括失敗和成功的要求。

-   要求 tooanalytics 資料。

### <a name="enabling-browser-based-clients-using-cors"></a>使用 CORS 啟用瀏覽器型用戶端
[跨原始資源共用 (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services)是一套機制，可讓網域 toogive 彼此存取彼此的資源的權限。 hello 使用者代理程式會將傳送的額外標頭 tooensure hello JavaScript 程式碼載入來自特定網域允許 tooaccess 資源位於另一個網域。 然後會以允許或拒絕 hello 原始網域存取 tooits 資源的額外標頭回覆 hello 第二個網域。

Azure 儲存體服務現在都支援 CORS，以便設定之後 hello hello 服務的 CORS 規則，對 hello 服務發出來自不同網域的適當驗證的要求是否允許根據 toohello 規則，您必須是評估的 toodetermine指定。
## <a name="networking"></a>網路
hello > 一節提供有關這些功能的 Azure 網路安全性和摘要資訊中的主要功能有關的其他資訊。

### <a name="network-layer-controls"></a>網路層控制
網路存取控制會限制從特定裝置或子網路的連線能力 tooand hello 動作，並代表 hello 的網路安全性的核心。 網路存取控制 hello 目標是確認您的虛擬機器和服務可以存取 tooonly 使用者，且裝置 toowhich 您想要存取 toomake。

#### <a name="network-security-groups"></a>網路安全性群組
A[網路安全性群組 (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)是基本可設定狀態篩選封包的防火牆，它可讓您 toocontrol 存取權限[5-tuple](https://www.techopedia.com/definition/28190/5-tuple)。 NSG 未提供應用程式層級檢查或已驗證的存取控制。 可以使用 Azure 虛擬網路內的子網路與 Azure 虛擬網路與 hello 網際網路之間的流量之間移動 toocontrol 流量。

#### <a name="route-control-and-forced-tunneling"></a>路由控制和強制通道
在 Azure 虛擬網路上的 hello 能力 toocontrol 路由行為是嚴重的網路安全性和存取控制功能。 例如，如果您想 toomake 確定從 Azure 虛擬網路的所有流量 tooand 都通過該虛擬的安全性應用裝置，您需要 toobe 無法 toocontrol 並自訂路由行為。 做法是在 Azure 中設定使用者定義的路由。

[使用者定義的路由](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)toocustomize 可讓您移動個別的虛擬機器或子網路 tooinsure 出入流量的輸入和輸出路徑 hello 最安全的路由可能。 [強制通道](https://www.petri.com/azure-forced-tunneling)的機制，您可以使用您的服務不 tooensure 允許 tooinitiate 連接 toodevices hello 網際網路上。

這點不同於所能 tooaccept 連入連線，然後回應 toothem。 前端網頁伺服器需要從網際網路主機 toorespond toorequests，因此允許來自網際網路的流量輸入的 toothese 網頁伺服器與 hello 網頁伺服器可以回應。

強制通道是常用的 tooforce 輸出流量 toohello 網際網路 toogo 透過內部部署安全性 proxy 和防火牆。

#### <a name="virtual-network-security-appliances"></a>虛擬網路安全性應用裝置
雖然網路安全性群組、 使用者定義的路由及強制通道可提供您的 hello hello 網路和傳輸層級的安全性層級[OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，有時可能會想 tooenable 的較高層級的安全性hello 堆疊。 您可以使用 Azure 合作夥伴網路安全性設備解決方案，來存取這些增強的網路安全性功能。 您可以找到 hello 最新的 Azure 合作夥伴網路安全性解決方案瀏覽 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/)並搜尋 「 安全性 」 及 「 網路安全性 」。

### <a name="azure-virtual-network"></a>Azure 虛擬網路

Azure 虛擬網路 (VNet) 是網路的您自己 hello 雲端中的表示法。 它是 hello 的隔離的邏輯 Azure 網路網狀架構專用 tooyour 訂用帳戶。 您也可以完全控制 hello IP 位址區塊、 DNS 設定、 安全性原則，以及此網路內的路由表。 您可以將 VNet 分成數個子網路，並在 Azure 虛擬網路上放置 Azure IaaS 虛擬機器 (VM) 和/或[雲端服務 (PaaS 角色執行個體)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)。

此外，您可以 hello 虛擬網路 tooyour 在內部部署網路連線使用其中一種 hello[連線選項](https://docs.microsoft.com/azure/vpn-gateway/)Azure 中可用。 基本上，您可以展開您的網路 tooAzure，並且可以完全控制在使用 Azure 提供的企業規模的 hello 優點的 IP 位址區塊。

Azure 網路功能支援各種安全遠端存取案例。 其中包含：

-   [連接個別的工作站 tooan Azure 虛擬網路](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [使用 VPN 連接內部部署網路 tooan Azure 虛擬網路](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [使用專用的 WAN 連結連線在內部部署網路 tooan Azure 虛擬網路](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [連接 Azure 虛擬網路 tooeach 其他](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN 閘道
toosend Azure 虛擬網路與內部部署網站之間的網路流量，您必須建立 Azure 虛擬網路的 VPN 閘道。 [VPN 閘道](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways)是一種虛擬網路閘道，可透過公用連接傳送加密的流量。 您也可以使用 Azure 虛擬網路透過 hello Azure 網路網狀架構之間的 VPN 閘道 toosend 流量。

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)是一個專用的 WAN 連結，可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的專用私人連接。

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 CRM Online。 從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。

ExpressRoute 連線不會經過 hello 公用網際網路，因此可以視為 VPN 為基礎的方案比更安全。 這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。


### <a name="application-gateway"></a>應用程式閘道
Microsoft [Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)會以服務形式提供[應用程式傳遞控制器 (ADC) (英文)](https://en.wikipedia.org/wiki/Application_delivery_controller)，為您的應用程式提供各種第 7 層負載平衡功能。

![應用程式閘道](./media/azure-security/azure-security-fig2.png)

它可讓您 toooptimize web 伺服陣列產能卸載大量 SSL 終止 toohello CPU （也稱為 「 SSL 卸載"或"SSL 橋接 」） 的應用程式閘道。 它也提供其他層 7 路由功能，包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 單一應用程式閘道背後的多個網站。 Azure 應用程式閘道是第 7 層負載平衡器。

無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。

應用程式提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、[安全通訊端層 (SSL)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell) 卸載、自訂健康狀態探查、支援多網站，以及許多其他功能。

### <a name="web-application-firewall"></a>Web 應用程式防火牆
Web 應用程式防火牆是一項功能[Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)tooweb 應用程式閘道用於標準的應用程式傳遞控制項 (ADC) 函式的應用程式提供保護。 Web 應用程式防火牆的運作方式保護他們針對大部分的 hello OWASP 前 10 個常見 web 弱點。

![Web 應用程式防火牆](./media/azure-security/azure-security-fig1.png)

-   SQL 插入式攻擊保護

-   常見 Web 攻擊保護，例如命令插入式攻擊、HTTP 要求走私、HTTP 回應分割和遠端檔案包含攻擊

-   防範 HTTP 通訊協定違規

-   防範 HTTP 通訊協定異常行為，例如遺漏主機使用者代理程式和接受標頭

-   防範 Bot、編目程式和掃描器

-   偵測一般應用程式錯誤組態 (也就是 Apache、IIS 等)


Web 攻擊的集中式的 web 應用程式防火牆 tooprotect 讓安全性管理簡單許多，而且會提供更好的保證 toohello 應用程式對 hello 威脅的入侵。 WAF 方案也可以回應 tooa 更快的安全性威脅的修補與保護每個個別的 web 應用程式的中央位置的已知的弱點。 閘道可以是現有的應用程式輕鬆地轉換 tooan 應用程式閘道與 web 應用程式的防火牆。
### <a name="traffic-manager"></a>流量管理員
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)可讓您在不同資料中心的服務端點的使用者流量 toocontrol hello 分散。 流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。 您也可以將流量管理員使用於外部、非 Azure 端點。 Traffic Manager 會使用 hello 網域名稱系統 (DNS) toodirect 用戶端要求 toohello 最適當的端點，根據[流量路由方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)和 hello hello 端點健全狀況。

Traffic Manager 所提供的流量路由方法 toosuit 不同的應用程式的需求，端點健全狀況範圍[監視](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)，以及自動容錯移轉。 Traffic Manager 是彈性 toofailure，包括整個 Azure 地區的 hello 失敗。
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Azure 負載平衡器](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview)tooyour 應用程式提供高可用性和網路效能。 這是 Layer 4 (TCP、UDP) 負載平衡器，可將連入流量分配到負載平衡集中所定義服務的狀況良好執行個體。 Azure Load Balancer 可以設定為：

-   負載平衡連入網際網路流量 toovirtual 機器。 這個組態稱為 [網際網路面向的負載平衡](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview)。

-   平衡虛擬網路中的虛擬機器之間、雲端服務中的虛擬機器之間，或內部部署電腦與跨單位部署虛擬網路中的虛擬機器之間的流量負載。 這個組態稱為 [內部負載平衡](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview)。 

- 將外部流量 tooa 特定虛擬機器

### <a name="internal-dns"></a>內部 DNS
您可以管理 hello VNet 或 hello 網路組態檔中 hello 管理入口網站中使用的 DNS 伺服器清單。 客戶可以新增每個 VNet too12 DNS 伺服器。 指定 DNS 伺服器時，重要 tooverify 您列出客戶的客戶環境的 hello 正確順序的 DNS 伺服器。 DNS 伺服器清單不會使用循環配置資源， 所指定的 hello 順序中的使用。 如果無法到達的 toobe hello 第一部 DNS 伺服器 hello 清單上的，hello 用戶端會使用該 DNS 伺服器，而不管是否 hello DNS 伺服器是否運作正常。 toochange hello 客戶的虛擬網路的 DNS 伺服器順序從 hello 清單中移除 hello DNS 伺服器並將其新增回順序 hello 該客戶想。 DNS 支援 hello"CIA 」 安全性三角理論 hello 可用性層面。

### <a name="azure-dns"></a>Azure DNS
hello[網域名稱系統](https://technet.microsoft.com/library/bb629410.aspx)，或 DNS，負責將轉譯 （或解決） 的網站或服務名稱 tooits IP 位址。 [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) 是 DNS 網域的主機服務，採用 Microsoft Azure 基礎結構提供名稱解析。 裝載您在 Azure 中的網域，您可以管理您的 DNS 記錄使用相同的認證、 Api、 工具和計費 hello 與其他 Azure 服務。 DNS 支援 hello"CIA 」 安全性三角理論 hello 可用性層面。
### <a name="log-analytics-nsgs"></a>Log Analytics NSG
您可以啟用下列診斷記錄檔分類的 Nsg hello:
-   事件： 包含哪些 nsg 規則會套用的 tooVMs 和 MAC 位址為基礎的執行個體角色的項目。 hello 狀態，這些規則會收集每隔 60 秒。

-   規則計數器： 項目包含每個 NSG 規則會套用的 toodeny 多少次，或允許流量。

### <a name="azure-security-center"></a>Azure 資訊安全中心
資訊安全中心可協助您防止、 偵測，並回應 toothreats，並提供您增加可見性，並控制 hello 您的 Azure 資源的安全性。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理、協助偵測可能忽略的威脅，並適用於廣泛的安全性解決方案生態系統。 網路建議集中圍繞在防火牆、網路安全性群組、設定輸入流量規則等等。

可用的網路建議如下：

-   [加入下一個層代防火牆](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall)建議您將加入 下一步產生防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護

-   [只有透過 NGFW 流量路由傳送](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only)呤魽您設定您的網路安全性群組 (NSG) 規則強制傳入的流量 tooyour 透過您 NGFW VM。

-   [啟用子網路/虛擬機器上的網路安全性群組](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups)：建議您在子網路或 VM 上啟用 NSG。

-   [透過網際網路面向端點限制存取](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints)：建議您為 NSG 設定輸入流量規則。


## <a name="compute"></a>計算

hello > 一節提供有關這些功能區域和摘要資訊中的主要功能的其他資訊。

### <a name="antimalware--antivirus"></a>反惡意程式碼與防毒軟體
與 Azure IaaS 中，您可以使用反惡意程式碼軟體，例如 Microsoft、 Symantec、 趨勢科技、 McAfee 和 Kaspersky tooprotect 安全性廠商惡意檔案、 廣告軟體和其他威脅傷害您的虛擬機器。 適用於 Azure 雲端服務和虛擬機器的 [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) 是一項保護功能，有助於識別和移除病毒、間諜軟體和其他惡意軟體。 Microsoft 反惡意程式碼提供已知惡意或垃圾軟體嘗試 tooinstall 本身，或在您的 Azure 系統上執行時可設定的警示。 您也可以使用 Azure 資訊安全中心來部署 Microsoft Antimalware。

### <a name="hardware-security-module"></a>硬體安全性模型
加密及驗證並未改善安全性除非 hello 金鑰本身會受到保護。 您可以藉由將它們儲存在簡化 hello 管理和安全性關鍵的密碼和金鑰的[Azure 金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)。 金鑰保存庫提供 hello 選項 toostore 您的硬體安全性模組 (Hsm) 認證的 tooFIPS 140-2 Level 2 標準中的索引鍵。 備份或 [透明資料加密](https://msdn.microsoft.com/library/bb934049.aspx) 的 SQL Server 加密金鑰都能與應用程式的任何金鑰或密碼一起存放在金鑰保存庫中。 權限和存取 toothese 受保護的項目透過[Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)。

### <a name="virtual-machine-backup"></a>虛擬機器備份
[Azure 備份](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)是一種解決方案，可以不需成本地保護您的應用程式資料，以及將操作成本降到最低。 應用程式錯誤可能會損毀您的資料，並發生人員錯誤可能引入可能會導致 toosecurity 問題的應用程式的 bug。 使用 Azure 備份，您執行 Windows 與 Linux 的虛擬機器會受到保護。

### <a name="azure-site-recovery"></a>Azure Site Recovery
您的組織的重要部分[商務持續性/災害復原 (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)策略找出如何 tookeep 企業工作負載和應用程式設定和執行計畫時和未規劃的中斷發生。 [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) 有助於協調工作負載和應用程式的複寫、容錯移轉及復原，因此能夠在主要位置發生故障時，透過次要位置提供工作負載和應用程式。

### <a name="sql-vm-tde"></a>SQL VM TDE
[透明資料加密 (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault)和資料行層級加密 (CLE) 都是 SQL Server 加密功能。 這種形式的加密需要客戶 toomanage 和市集 hello 用來加密的密碼編譯金鑰。

hello Azure 金鑰保存庫 (AKV) 服務是設計的 tooimprove hello 安全性和管理高可用性的位置中的這些索引鍵。 hello SQL Server 連接器可讓 SQL Server toouse Azure 金鑰保存庫中的這些索引鍵。

如果您沒有執行 SQL Server 在內部部署機器，有您可以依照 tooaccess Azure 金鑰保存庫，從內部部署 SQL Server 電腦的步驟。 但是，對於在 Azure Vm 中的 SQL Server，您可以使用 hello Azure 金鑰保存庫整合功能來節省時間。 少數的 Azure PowerShell cmdlet tooenable 這項功能，您可以使用自動化 hello 組態所需的 SQL VM tooaccess 金鑰保存庫。

### <a name="vm-disk-encryption"></a>VM 磁碟加密
[Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)是一項新功能，可協助您加密 Windows 和 Linux IaaS 虛擬機器磁碟。 它適用於 hello 業界標準 BitLocker 功能的 Windows 和 Linux tooprovide 磁碟區加密 hello OS hello DM Crypt 功能和 hello 資料磁碟。 hello 方案整合 Azure 金鑰保存庫 toohelp 您控制和管理您金鑰保存庫的訂用帳戶中的 hello 磁碟加密金鑰和密碼。 hello 方案也能確保 hello 虛擬機器磁碟上的所有資料會留在您 Azure 儲存體都加密。

### <a name="virtual-networking"></a>虛擬網路
虛擬機器需要遠端連線。 toosupport 該需求，Azure 需要連接的虛擬機器 toobe tooan Azure 虛擬網路。 Azure 虛擬網路是建立在 hello Azure 的實體網路網狀架構之上一個邏輯結構。 每個邏輯 [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)都會與其他所有 Azure 虛擬網路隔離。 此隔離有助於確保您的部署中的網路流量不是可存取 tooother Microsoft Azure 客戶。

### <a name="patch-updates"></a>修補程式更新
修補程式更新提供對於尋找並修正潛在問題 hello 基礎和簡化 hello 軟體更新管理程序，藉由減少您必須在企業中部署的軟體更新的 hello 數目，藉由增加能力 toomonitor相容性。

### <a name="security-policy-management-and-reporting"></a>安全性原則管理和報告
[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)可協助您防止、 偵測，並回應 toothreats，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理、協助偵測可能忽略的威脅，並適用於廣泛的安全性解決方案生態系統。

### <a name="azure-security-center"></a>Azure 資訊安全中心
資訊安全中心可協助您防止、 偵測，並回應 toothreats 增加的可見性與您的 Azure 資源的 hello 安全性控制。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

## <a name="identify-and-access-management"></a>身分識別和存取管理

保護系統、應用程式及資料是從以身分識別為基礎的存取控制開始。 hello 身分識別和存取管理功能，在 Microsoft 商業產品和服務內建保護您的組織和個人資訊免於未經授權存取同時可讓可用 toolegitimate 使用者時，無論在何處他們需要它。

### <a name="secure-identity"></a>安全的身分識別
Microsoft 會使用其產品和服務 toomanage 身分識別和存取跨多個安全性作法和技術。
-   [Multi-factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)需要使用者 toouse 多個方法進行存取，在內部部署和 hello 雲端中。 它使用一些簡單驗證選項來提供堅固的驗證，同時透過簡易登入程序來因應使用者。

-   [Microsoft Authenticator (英文)](https://aka.ms/authenticator) 提供易於使用的 Multi-Factor Authentication 體驗，可搭配 Microsoft Azure Active Directory 和 Microsoft 帳戶一起使用，並包括對於穿戴式裝置與指紋式核准的支援。

-   [密碼原則強制執行](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/)增加 hello 由諸長度和複雜性需求，強制定期更換，傳統密碼的安全性和帳戶鎖定計數器的時間失敗驗證嘗試。

-   [權杖型驗證](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/)會透過 Active Directory 同盟服務 (AD FS) 或協力廠商的安全性權杖系統來啟用驗證。

-   [角色型存取控制 (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/)可讓您 toogrant 存取權限 hello 使用者指派角色，以輕鬆 toogive 使用者只有 hello 數量存取它們所需 tooperform 他們工作的工作。 您可以針對每個組織的商務模型和風險承受度自訂 RBAC。

-   [整合式身分識別管理 （混合式身分識別）](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/)可讓您跨內部部署資料中心和雲端平台上建立單一使用者識別進行驗證和授權 tooall 資源的 toomaintain 控制項的使用者存取權。

### <a name="secure-apps-and-data"></a>保護應用程式和資料
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)，完整身分識別和存取管理雲端方案，可協助安全地存取 toodata hello 雲端和站台上的應用程式中，以簡化 hello 管理使用者和群組。 它結合了核心目錄服務、 進階身分識別控管、 安全性及應用程式存取管理，並簡化成自己的應用程式的開發人員 toobuild 以原則為基礎的身分識別管理。 tooenhance Azure Active Directory，您可以新增使用 hello Azure Active Directory Basic、 Premium P1 和 Premium P2 edition 的付費的功能。

| 免費/常用功能     | 基本功能    |Premium P1 功能 |Premium P2 功能 | Azure Active Directory Join – 僅適用於 Windows 10 的相關功能|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [目錄物件](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects)，[使用者/群組管理 （加入/更新/刪除） 使用者型佈建裝置註冊](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration)，[單一登入 (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso)，[自助服務雲端使用者的密碼變更](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users)，[連接 （擴充內部部署目錄 tooAzure Active Directory 同步處理引擎）](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory)，[安全性 / 使用量報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [以群組為基礎的存取管理/佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning)、[雲端使用者的自助式密碼重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users)、[創建公司品牌 (登入頁面/存取面板自訂)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization)、[ Proxy](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy)、[SLA 99.9%](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [自助式群組和應用程式管理/自助式應用程式新增/動態群組](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group)、[使用內部部署回寫來進行的自助式密碼重設/變更/解除鎖定](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back)、[Multi-Factor Authentication (雲端與內部部署 (MFA Server))](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server)、[MIM CAL + MIM 伺服器](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server)、[Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery)、[Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health)、[群組帳戶的自動密碼變換](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Identity Protection](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection)、[Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [加入裝置 tooAzure AD，桌面 SSO，Azure AD 中，系統管理員的 Bitlocker 修復的 Microsoft Passport](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery)， [MDM 自動註冊，自助 Bitlocker 修復，其他的本機系統管理員 tooWindows 10 裝置透過 Azure加入 AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [雲端應用程式探索](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis)是的可供您組織中的 hello 員工 tooidentify 雲端應用程式可讓您的 Azure Active Directory premium 功能。

- [Azure Active Directory 識別身分保護](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/)是一種安全性服務，使用 Azure Active Directory 異常偵測功能 tooprovide 合併檢視風險事件和潛在的弱點可能會影響您組織的身分識別。

- [Azure Active Directory 網域服務](https://azure.microsoft.com/services/active-directory-ds/)可以您讓 toojoin Azure Vm tooa 網域，而 hello 需要 toodeploy 網域控制站。 使用者使用其公司的 Active Directory 認證，登入 toothese Vm，而且可以順暢地存取資源。

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)是消費者導向應用程式，可以調整 toohundreds 數百萬個身分識別，以及整合各個行動裝置的高可用性、 全域的身分識別管理服務和 web 平台。 您的客戶可以登入 tooall 您的應用程式，透過可自訂的方式，使用現有的社交媒體帳戶，或您可以建立新的獨立認證。

- [Azure Active Directory B2B 共同作業](https://aka.ms/aad-b2b-collaboration)是藉由啟用支援跨公司關聯性的協力廠商安全整合解決方案合作夥伴 tooaccess 公司應用程式和資料選擇性地透過其自我管理身分識別。

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)可讓您集中管理 tooextend 雲端功能 tooWindows 10 裝置。 它可讓使用者 tooconnect toohello 公司或組織雲端透過 Azure Active Directory，並簡化存取 tooapps 和資源。

- [Azure Active Directory 應用程式 Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) 為內部部署裝載的 Web 應用程式提供 SSO 及安全的遠端存取。

## <a name="next-steps"></a>後續步驟
- [開始使用 Microsoft Azure 安全性](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Azure 服務和功能，您可以使用 toohelp 保護您的服務和 Azure 中的資料

- [Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)

防止、 偵測，並回應 toothreats 增加的可見性與您的 Azure 資源的 hello 安全性控制

- [Azure 資訊安全中心的安全性健康情況監視](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

hello Azure 資訊安全中心 toomonitor 符合原則中的監視功能。
