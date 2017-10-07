---
title: "aaaAzure App Service Web 應用程式的供應項目企業"
description: "示範如何 toouse Azure App Service Web 應用程式 toocreate 企業網站解決方案的業務效益"
services: app-service\web
documentationcenter: 
author: apwestgarth
manager: erikre
editor: 
ms.assetid: cf9ac3b2-0493-4461-8b64-251d3a5cd5b5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: anwestg
ms.openlocfilehash: 5d551509219988160858ff35298d3c7275d1d071
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-apps-offerings-for-enterprise-whitepaper"></a>企業的 Azure App Service Web Apps 提供項目白皮書
hello 需要 tooreduce 成本，並提供 IT 方案快快速發展環境為開發人員、 IT 專業人員和管理員建立新的挑戰。 使用者會逐漸尋找其企業營運 (LOB) web 的應用程式有 toobe 快速、 回應、 且可從任何裝置。 在 hello 同時，企業嘗試 toocapitalize 上 hello 增加生產力與效率來自與雲端和行動服務整合，這可能是項目一樣簡單，做為單一登入跨裝置使用 Active Directorytoocollaboration Office365 中使用的資料取自接著會提取的資料從 Salesforce hello 公司實作的內部 LOB 應用程式。 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 是一個企業級的雲端服務，可用來開發、測試，以及執行 Web 和行動應用程式、Web API 及一般網站。 它可以是使用的 toorun 公司網站、 內部網路網站、 企業營運應用程式，及資料中心的全球網路上的數位行銷活動最佳化的延展性和可用性，並支援連續整合和現代 DevOps 作法。  

本白皮書會反白顯示 hello hello 功能[Web 應用程式](/services/app-service/web/)服務特別著重於執行 LOB Web 應用程式，涵蓋移轉現有的 web 應用程式和部署新的 LOB web hello 上的應用程式平台。

## <a name="audience"></a>對象
IT 專業人員、 架構設計人員和管理員對象 toomigrate toohello 雲端 web 工作負載目前正在執行內部部署。 Web 工作負載可以跨越任一個商務 tooEmployee 或商務 tooPartners web 應用程式。

## <a name="introduction"></a>簡介
App Service Web 應用程式是在哪個 toohost 外部和內部的理想平台 web 應用程式和服務可提供符合成本效益、 高擴充性、 受管理的解決方案，可讓您在交付商務價值，為您的使用者，而 tooconcentrate比花費大量時間和金錢維護和支援的個別環境。 Web 應用程式提供彈性的平台的 toodeploy 供應項目 hello 能力 toocontinue tooauthenticate 對內部部署 Active Directory 整合透過與 Microsoft Azure Active Directory 的企業 web 應用程式支援的方便而快速進行部署時使用了您內部連續整合及部署的作法，自動縮放比例 toogrow hello 的商務需求-所有受管理的平台，可讓您 toofocus 上您的應用程式並不是您基礎結構。

## <a name="problem-definition"></a>問題定義
hello IT 版圖正在變更快速，以遠離傳統的伺服器上裝載的具有其高的投資成本長前置重疊時間 tooone 會視使用的自動調整 toohandle 負載的服務上移動。 IT 部門正在挑戰 tooreduce hello 成本和基礎結構的使用量，並將焦點設在降低 CAPEX，也可以提高靈活度花維護。 hello 生命週期結束的舊的基礎結構平台，例如 Windows Server 2003，會導致 IT 部門 tooreview 雲端移轉以潛在方式 tooavoid 新長期的投資成本。 在過去 hello Cio 使得採購決策的其他部門;不過，逐漸 CMOs 及其他商務單位讀寫頭花費的時間中其預算所花費的方式的更多使用中的角色和哪些 hello 投資報酬率。 逐漸，企業需要其工作力 toobe 比以往與員工從遠端工作、 花費更多的時間與需要的存取 toosystems 麻煩的客戶釋放更行動。

企業需求無時無刻不在變化。 企業正在尋找由協力廠商或內部提供、新功能應有盡有，且可定期更新服務的即時全球布局。  在某些情況下，企業也要尋找的 hello 功能 tooisolate 其應用程式和存取 tooresources，同時也讓公用雲端設備的使用。 許多使用者會對企業有較高的期望，他們在私生活中享受許多服務 (例如 Office365)。 他們希望 toohave 存取 toosimilar toodate，其工作的生命週期中的功能豐富服務註冊。 與此需求，toocope IT 必須查看 toohelp hello 商務 tooenable 這透過選取範圍和與協力廠商的整合服務，謹慎選取的平台可以調整 toohello 的商務需求，而同時又可靠總降低成本擁有權。

開發小組尋找 toodeliver 立即商業利益，經常在提供的新功能。 所需符合成本效益、 可信賴平台以便將現有的工具和作法 – 開發、 測試與整合，請放開。而與 IT 部門的工作會自動部署、 管理和警示時，所有的 hello 目的零停機時間。

<a name="highlevel"></a>
## <a name="high-level-solution"></a>高階解決方案
越來越多的 web 平台和架構使用 toodevelop、 測試和主機企業營運應用程式。  與一般企業營運應用程式，例如內部員工費用系統，經常組成單獨 web 應用程式與備份資料庫 toostore hello 資料連接與 hello 應用程式。

App Service Web Apps 是裝載此類應用程式的最佳選項，提供可擴充和十分可靠的基礎結構，可在幾乎零手動介入和零停機時間的情況下進行管理和修正。 hello Microsoft Azure 平台還提供許多資料儲存體選項 toosupport web 應用程式裝載 Web 應用程式，從 Microsoft Azure SQL Database，受管理可擴充關聯式資料庫做為服務，toopopular 從我們的合作夥伴，例如 ClearDB 服務MySQL 資料庫，而且 MongoDB。

另一個方法是 toomake 使用您現有的投資在內部部署。 在 hello 範例案例中，員工費用系統，您可能希望 toomaintain 資料存放區內部的基礎結構內。 這可用於與報告、 薪資 （計費等） 的內部系統或 toosatisfy 整合 IT 控管需求。  Web 應用程式提供多種方法，讓您 tooconnect tooyour 在內部部署基礎結構：

* [應用程式服務環境](app-service-app-service-environment-intro.md)-應用程式服務環境 (ASE) 是新 Premium 功能，這是最近新增 toohello Microsoft Azure 應用程式服務供應項目。  ASE 提供一個完全隔離且專用的環境，在相當高的程度上可安全地執行 Azure App Service app，同時又提供隔離且安全的網路存取。   
* [混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)– 混合式連線是 Microsoft Azure BizTalk 服務的功能，並安全地儲存，例如 SQL Server、 MySQL、 Web Api 和自訂的 web 服務啟用 Web 應用程式 tooconnect tooon 內部部署資源。
* [虛擬網路整合](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)– 使用 Azure 虛擬網路的 Web 應用程式整合可讓您 tooconnect 您 web 應用程式 tooan Azure 虛擬網路的進而可以是在內部部署基礎結構，透過站對站 VPN 連線的 tooyour。

hello 下列圖表描述範例整體解決方案與內部部署資源的連線選項。  hello 第一個範例顯示如何這可以使用標準功能的 Azure 應用程式服務來達成和 hello 第二個顯示這可以是使用供應項目，應用程式服務環境的 hello premium 達成。

使用標準 App Service 功能： ![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions.png "Using Standard App Service Features")

使用 App Service 環境： ![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions-ASE.png "Using an App Service Environment")

## <a name="business-benefits"></a>商業利益
App Service Web 應用程式提供可讓您的函式 toobe 更符合成本效益且 hello 的商務需求提供敏捷式軟體開發的商業優勢的主機。

### <a name="paas-model"></a>PaaS 模型
App Service Web Apps 採用平台即服務模型，能夠大幅節省成本又可提高效率。  您不再需要 toospend 小時管理 Vm、 修補作業系統和架構。 Web 應用程式是可讓您管理您的 web 應用程式和不 Vm，保留 小組可用 tooprovide 其他商務價值 toofocus 的自動修補的環境。

hello 簽訂 Web 應用程式 PaaS 模型可讓從業 hello DevOps 方法 toofulfill 的目標。 身為企業，這表示完整的管理及整合在 hello 應用程式完整生命週期，包括開發、 測試、 發行、 監視與管理的支援。

開發小組、 持續整合和部署工作流程可以設定從 Visual Studio Team Services、 GitHub、 TeamCity、 Hudson 或 BitBucket，啟用自動化的組建、 測試和部署啟用更快速發行週期可以儘管減少hello 人事參與釋放現有的基礎結構中。 Web 應用程式也支援 hello 建立多個測試和預備環境以供您發行的工作流程，不再執行您需要 tooreserve 或硬體配置用於這些用途，您可以建立為許多環境，並定義您自己的升級toorelease 工作流程。 身為企業您可能決定 toorelease tooa 測試位置從原始檔控制、 執行一系列的測試成功完成時升級 tooa 階段位置並沒有停機的情況下，以 hello 交換 tooproduction 最後加入裝載的 web 應用程式的優點Web 應用程式已預先載入和熱 tooprovide hello 最佳可能的客戶經驗。  此外企業可以將使用 hello toodirect App Service Web 應用程式的實際執行功能測試部分流量 tooa 不同位置，先驗證 hello 變更再切換所有流量 toohello 新部署或還原的所有流量toohello 先前的部署。

作業小組可以信心它們在與任何 web 應用程式內建的監視和警示功能的 hello 與裝載 Web 應用程式處於 hello 最佳可能位置 tooreact tooany 問題。 營運團隊已針對分析與監視方案進行投資，例如 Microsoft Visual Studio Application Insights、New Relic 和 AppDynamics。 這些也完全支援在啟用持續性和熟悉的環境，從哪些 toomonitor web 應用程式的 Web 應用程式上。

最後，Web 應用程式提供功能 tooautomatically 備份您的應用程式與裝載的資料庫直接 tooan Azure Blob 儲存體容器。 能提供較簡單的方式與非常符合成本效益的方法有哪些 toorecover 從損毀，減少 hello 需要複雜的內部部署硬體和軟體。

### <a name="ease-of-migration"></a>簡化移轉
隨著硬體和作業系統的發行週期速度加快，硬體維護和輪替會是企業的重點。 或許您有 Windows Server 2003 R2 伺服器全都來自 toohello 結束 2015 支援其中的數字，但它們仍裝載您公司的索引鍵的 web 應用程式嗎？ App Service Web 應用程式是在哪個 toohost 的 web 應用程式的絕佳候選項目和您 toorationalize hello 商務硬體資產。 Web 應用程式可讓您存取 tooa 範圍的硬體規格的管理和維護 hello service 的一部分做為您的基礎結構預算一部分消除 hello 需要 toofactor 取代型和管理成本。  移轉可以簡單地複製和貼上從您現有的部署 tooWeb 應用程式或複雜的移轉作業可供使用 hello Web 應用程式移轉小幫手加入加入值。 已移轉的 web 應用程式享有 hello 的 Azure 服務，整合其他服務 toohello web 應用程式的完整範圍。 例如，您可以考慮加入 Azure Active Directory toocontrol 存取 tooyour 應用程式根據使用者的關聯 toosecurity 群組。 另一個範例可以加入快取服務 tooimprove 效能並降低延遲，提供整體更好的使用者體驗。

### <a name="enterprise-class-hosting"></a>企業類別裝載
App Service Web 應用程式提供穩定、 可信賴平台證明 toobe 無法 toohandle 各種商務需要從小型內部開發和測試工作負載，調整 toohighly 高流量網站。 藉由使用 Web 應用程式，您正在使用的 hello 相同裝載平台是利用針對最高值 web 工作負載的 Microsoft 公司的企業類別。 Web 應用程式，以及 hello Azure 平台上的所有服務所建置的安全性和法規需求，例如 ISO (ISO/IEC 27001:2005;) 的相容性SOC1 和 SOC2 SSAE 16/ISAE 3402 認證、 HIPAA BAA、 PCI 和 fedramp 是，在 hello 其實每個項目和功能，如需詳細資訊，請參閱[http://aka.ms/azurecompliance](/support/trust-center/compliance/)。

Microsoft Azure 平台可讓角色型授權控制項啟用的控制項 tooresources Web 應用程式內的企業層級。 RBAC 可讓企業 hello 電源 tooimplement 他們自己的存取管理原則的所有其 hello Azure 環境中的資產藉由指派使用者 toogroups 並接著指派 hello 資產，例如 web toothose 群組 hello 所需的權限應用程式。 如需有關 Azure 中 RBAC 的詳細資訊，請參閱 [http://aka.ms/azurerbac](../active-directory/role-based-access-control-configure.md)。 透過使用 Web Apps，您可以確定您的 Web 應用程式會在安全的環境中進行部署，而且您會擁有部署資產所在領域的完整控制權。

Azure App Service 環境[http://aka.ms/aseintro](http://aka.ms/aseintro)是新的高階服務計劃選項，企業客戶希望 toomake 使用的 Azure 應用程式服務，這些資料行會提供完全隔離且專用的環境。  這可讓企業客戶 toodeploy 應用程式可以充分利用非常高的標尺，儘管也具有 完全控制傳入和傳出網路流量，因而 ASEs 啟用應用程式 toohave 高速安全連線透過虛擬網路 tooon 內部部署資源。

App Service Web 應用程式也是您在內部部署投資 toomake 可以完整使用藉由提供 hello 能力 tooconnect 後 tooyour 內部資源，例如您的資料倉儲或 SharePoint 環境。 中所述[高的層級方案](#high-level-solution)進行混合式連線和虛擬網路連線 tooestablish 連線 tooon 使用內部部署基礎結構和服務。

### <a name="global-scale"></a>全球規模
App Service Web 應用程式是通用且可擴充的平台，可讓您的 web 應用程式 toogrow 快速及最小的長期規劃調整 toohello 持續成長的商務需求和成本。 在內部部署基礎結構案例，一般擴充需求增加本機和地理位置會需要大量的管理、 規劃和支出 tooprovision 並管理其他基礎結構。 Web 應用程式提供 hello 能力 tooscale web 應用程式與 hello ebb 和資料流程的需求。 做為範例，例如使用 hello 費用應用程式，hello 多數 hello 月份中的使用者是淺色 hello 應用程式使用者但 hello 期限費用提交 toobe 輸入和使用方式的每個月會增加您的應用程式，因為 Web 應用程式hello 功能 tooautomatically 佈建您的應用程式的較多基礎結構，然後一旦去除 hello 使用量再次它可以調整後 toohello 基準基礎結構，您定義。

全球 24 個 (且不斷增加) 資料中心都有提供 Web Apps。 區域和位置的 hello 最更新清單，請參閱[http://aka.ms/azlocations](http://aka.ms/azlocations)。 有了 Web Apps，您可以擴充企業並將它輕鬆地遍及全球。 隨著您的公司成長成新的區域，hello 報告您使用的應用程式儀表板及 Web 應用程式上的主機可以輕鬆部署到其他資料中心，並提供服務給透過 hello 組合的 Web 應用程式與 Azure 流量管理員 中，更快速的本機使用者所有以 hello 加入下面所能 toocontract hello 可擴充的基礎結構的優點，並展開 hello 需要 hello 處地區性辦公室的變更。

## <a name="solution-details"></a>解決方案詳細資料
讓我們看看應用程式移轉的案例。 這將概述 App Service Web 應用程式功能都 tootogether tooprovide 棒的解決方案，商務價值的是 hello 詳細的資料。

在本範例 hello 企業營運應用程式，我們將討論是 expense reporting 應用程式可讓員工 toosubmit 補償的費用。 hello 應用程式由執行 IIS6 的 Windows Server 2003 R2 上，而且 hello 資料庫是 SQL Server 2005 資料庫。 hello 的原因，我們選擇較舊的伺服器是出 hello 即將結束的服務的 Windows Server 2003 R2 和 SQL Server 2005，而且我們有[工具](http://aka.ms/websitesmigration)和[指引](http://aka.ms/websitesmigrationresources)tooautomatically 移轉至 Azure 的工作負載。 這一點之後，在此範例中所使用的 hello 模式適用於 tooa 寬供移轉案例。

### <a name="migrate-existing-application"></a>移轉現有的應用程式
步驟 1 的 hello 整體移動特定業務應用程式 tooWeb 應用程式的解決方案，是 tooidentify hello 現有應用程式資產和架構。 本白皮書中的 hello 範例是 hello 圖所示，單一的 IIS 伺服器上裝載與 hello 資料庫裝載於不同的 SQL Server，將 ASP.NET web 應用程式。 使用使用者名稱和密碼組合，員工登入 toohello 系統輸入費用的詳細資料並上載的回條、 掃描的複本到 hello 資料庫，每個項目的費用。

![](./media/web-sites-enterprise-offerings/on-premise-app-example.png)

#### <a name="items-tooconsider"></a>項目 tooconsider
從內部部署環境的移轉應用程式，您可能想 tookeep 請記住幾個 Web 應用程式的條件約束。 以下是一些重要主題 toobe 留意移轉當 web 應用程式 tooWeb 應用程式 ([http://aka.ms/websitesmigrationresources](http://aka.ms/websitesmigrationresources)):

* 連接埠繫結 - Web Apps 僅支援連接埠 80 (適用於 HTTP) 和連接埠 443 (適用於 HTTPS 流量)。 如果您的應用程式使用任何其他連接埠，然後一次移轉的 hello 應用程式將針對 HTTP 使用連接埠 80 和連接埠 443 的 HTTPS 流量。 這通常是因為它是在內部部署部署 toomake 使用不同的網域名稱，特別是在開發和測試環境中的順序 tooovercome hello 使用連接埠中常見無害的問題
* 驗證 - Web Apps 預設支援匿名驗證以及應用程式所指定的表單驗證。 只有整合 Azure Active Directory 與 ADFS hello 應用程式時，web 應用程式可以提供 Windows 驗證。 有關此功能更詳細的討論請參閱 [此處](http://aka.ms/azurebizapp)
* GAC 基礎組件 – Web 應用程式不允許 hello 部署的組件 toohello 全域組件快取 (GAC)。 因此，如果正在移轉 hello 應用程式會利用這在內部部署的功能，請考慮移動 hello 組件 toohello hello 應用程式 bin 資料夾。
* IIS5 相容模式 – Web 應用程式不支援 IIS5 相容模式，而且每個 Web 應用程式執行個體和 hello 父 Web 應用程式中執行的執行個體下的所有 web 應用程式在這種情況 hello 相同的工作者處理序內的單一應用程式集區。
* 使用 COM 程式庫-Web 應用程式不允許 hello 平台上的 hello 註冊的 COM 元件。 因此如果 hello 應用程式正在使用的任何 COM 元件，這些會需要 toobe 中 managed 程式碼重寫，而且與 hello 應用程式一起部署。
* ISAPI 篩選器 – Web Apps 上可支援 ISAPI 篩選器。 他們必須 toobe hello 應用的一部分部署與註冊 hello web 應用程式的 web.config 檔案中。 如需詳細資訊，請參閱 [http://aka.ms/azurewebsitesxdt](web-sites-transform-extend.md)。

一旦這些主題已經列入考慮，web 應用程式應該準備好進行 hello 雲端。 而且別擔心如果不完全符合一些主題，hello 移轉工具會提供最佳的投入時間 toomigration。

hello hello 移轉程序中的下一個步驟是 toocreate App Service web 應用程式和 Azure SQL Database。 有可供您 tooselect 根據您的 web 應用程式需求的多個具有不同的 CPU 核心數及 RAM 數量的 Web 應用程式執行個體的大小。 如需詳細資訊與價格，請參閱 [https://azure.microsoft.com/pricing/details/app-service/](https://azure.microsoft.com/pricing/details/app-service/)。 同樣地，Microsoft Azure SQL Database 皆代表 tooall 的商務需求與各種服務層和效能層級 toofulfill 需求。 在 [https://azure.microsoft.com/pricing/details/app-service/](https://azure.microsoft.com/pricing/details/sql-database/) 可以找到進一步的資訊。 一旦建立，hello 應用程式會是上傳的 tooApp Service Web 應用程式，透過 FTP 或 WebDeploy，然後再移到 hello 資料庫。

在此移轉 hello 解決方案會使用 Azure SQL Database，但是也就不是 hello 唯一的資料庫支援在 Azure。 公司也可使用的 MySQL、 MongoDB、 Azure Cosmos DB 和透過附加元件可以在 hello 購買更多[Azure 市集](/marketplace/partner-program/)。

在建立 Azure SQL Database 有多種選項會使用 tooimport 現有的資料庫從內部部署伺服器產生的指令碼的現有的資料庫 toousing hello[資料層應用程式匯出和匯入](http://aka.ms/dacpac).

藉由建立新的 Azure SQL Database，連接 toohello 資料庫使用 SQL Server Management Studio 建立 hello 費用應用程式資料庫，然後執行指令碼 toobuild hello 資料庫結構描述，並填入從 hello 內部的資料資料庫。

hello hello 移轉的第一個階段中的最後一個步驟需要 hello hello 應用程式的連接字串 toohello 資料庫更新。 這可以透過 hello Azure 入口網站來達成。 每個 web 應用程式中，您可以修改應用程式特定設定，包括所使用的 hello 應用程式 tooconnect tooany 資料庫正在使用的任何連接字串。

### <a name="alternatives-toousing-azure-sql-database"></a>替代項目 toousing Azure SQL Database
hello Azure 平台提供了許多替代方案 toousing 做為 web 應用程式的主要資料庫的 Azure SQL Database，這是 tooenable 不同工作負載，也就是使用 NoSQL 解決方案或 tooenable hello 平台 toosuit 需要 business 的資料。 比方說，企業可能保留離站或公用雲端環境中，不得儲存的資料，因此看起來會 toomaintain hello 使用其內部部署資料庫。

#### <a name="connectivity-tooon-premises-resources"></a>連線 tooOn 內部部署資源
App Service Web 應用程式提供了多個選項可以連接 tooon 內部部署資源，例如資料庫、 重複使用現有的高價值基礎結構。 hello 選項為如下所示：

* 應用程式服務環境會隔離，並建立虛擬網路的子網路內，因此啟用 hello 環境 toocommunicate 具有私用端點位於 hello 相同虛擬網路- [http://aka.ms/appserviceasenetworking](http://aka.ms/appserviceasenetworking)
* Web 應用程式虛擬網路整合支援 Web 應用程式之間的整合和 Azure 虛擬網路，可讓您存取 tooresources 如此，如果有站對站 VPN 連接內部部署網路上的 tooyour 連線虛擬網路中執行直接在內部部署系統上 tooyour。
* 混合式連線是 Azure BizTalk 服務的功能，並提供簡單的方式 tooconnect tooindividual 在內部部署 」 資源，例如 SQL Server、 MySQL、 HTTP 的 Web Api 和大部分的自訂 Web 服務。

#### <a name="scale-and-resiliency"></a>調整和復原
隨著企業成長其工作力，透過併購或自然有機成長，因此太必須 web 應用程式的擴充 toomeet 這些新需求。 確實今天常見 toosee 更佳的散佈共的小組和遠端員工，例如公司辦公室 hello 美國、 歐洲和亞洲、 在具有許多更多的領域中的行動銷售團隊。 Web 應用程式在標尺中有 hello 功能 toohandle 彈性變更，方便且自動。

App Service Web 應用程式可讓 web 應用程式設定 toobe tooscale 自動透過 hello Azure 入口網站中，根據兩個向量 – 排定的時間或依 CPU 使用量。 Web 應用程式自動調整大小的所有商務應用程式，從這類報告系統 toomarketing 網站體驗流量高載我們費用的 web 應用程式的使用量大於變更提供符合成本效益且極具彈性的方式 toocater升級在短時間內。 如需詳細資訊和調整 web 應用程式使用 Web 應用程式的指引，請參閱[如何 tooScale 網站](web-sites-scale.md)。

此外 toohello 調整彈性的 Web 應用程式中，跨多個資料中心和地理區域 hello 整體的平台可讓商務持續性和透過 hello 可能發佈的 web 應用程式和其資產的恢復功能。

## <a name="summary"></a>摘要
App Service Web 應用程式提供彈性、 符合成本效益、 回應方案 toohello 動態快速發展的環境中的商務需求。 Web Apps 利用具備現代 DevOps 功能的受管理平台並減少實際操作管理，同時提供調整、彈性、安全性及與內部部署資產整合等方面的企業功能，協助企業提高產能和效率。

## <a name="call-tooaction"></a>呼叫 tooAction
如需有關 hello Azure App Service Web 應用程式服務的詳細資訊，請瀏覽[http://aka.ms/enterprisewebsites](/services/websites/enterprise/)的詳細資訊，可以為來源，並簽署今天的試用版註冊[https://azure.microsoft.com/價格/免費試用 /](https://azure.microsoft.com/pricing/free-trial/) tooevaluate hello 服務及探索您公司的 hello 優點。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]
