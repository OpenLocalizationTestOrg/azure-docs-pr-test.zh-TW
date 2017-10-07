---
title: "應用程式服務、 虛擬機器、 服務網狀架構和雲端服務的比較 aaaAzure |Microsoft 文件"
description: "深入了解如何 toochoose 之間 Azure 應用程式服務、 虛擬機器、 服務網狀架構和雲端服務以託管的 web 應用程式。"
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Azure App Service、虛擬機器、Service Fabric 及雲端服務的比較
## <a name="overview"></a>概觀
Azure 提供數種方法 toohost 網站： [Azure App Service][Azure App Service]，[虛擬機器][Virtual Machines]， [Service Fabric] [ Service Fabric]，和[雲端服務][Cloud Services]。 這篇文章可協助您了解 hello 選項並且 hello 適用於 web 應用程式。

Azure App Service 是 hello 大部分 web 應用程式的最佳選擇。 部署和管理已整合為 hello 平台、 站台可以調整快速 toohandle 高流量負載，和 hello 內建的負載平衡與流量管理員提供高可用性。 您可以移動現有的站台 tooAzure 應用程式服務輕鬆地與[線上移轉工具](https://www.migratetoazure.net/)、 使用開放原始碼應用程式從 hello Web 應用程式庫，或建立新的網站使用 hello 架構和您選擇的工具。 hello [WebJobs] [ WebJobs]功能可讓您輕鬆 tooadd 背景工作處理 tooyour App Service web 應用程式。

如果您在建立新的應用程式或重新撰寫現有的應用程式，Service Fabric 是不錯的選擇 toouse 微服務架構。 應用程式，在機器的共用集區上執行，也可以從小型專案開始，而且成長 toomassive 具有數百部或數千部電腦所需的小數位數。 可設定狀態服務使其更容易 tooconsistently 且可靠地儲存應用程式狀態和 Service Fabric 自動服務資料分割、 調整及可用性會為您管理。  Service Fabric 也支援具有 Open Web Interface for .NET (OWIN) 和 ASP.NET Core 的 WebAPI。  比較的 tooApp 服務，Service Fabric 還提供更多控制或直接存取，hello 基礎結構。 您可以從遠端進入您的伺服器，或設定伺服器啟動工作。 雲端服務是類似 tooService 網狀架構中的控制和容易使用，但它現在是舊版的服務，Service Fabric 建議新的程式開發。

如果您有現有的應用程式需要大幅修改 toorun 應用程式服務或服務的網狀架構中，您可以選擇順序 toosimplify 移轉 toohello 雲端中的虛擬機器。 不過，正確設定，保護和維護 Vm 需要更多的時間和 IT 專業比較 tooAzure 應用程式服務和服務網狀架構。 如果您考慮 Azure 虛擬機器，請確定您納入帳戶 hello 持續性維護所需的投入時間 toopatch 更新和管理您 VM 的環境。 Azure 虛擬機器是基礎結構即服務 (IaaS)，而 App Service 和 Service Fabric 是平台即服務 (Paas)。 

## <a name="features"></a>功能比較
下表中的 hello 比較應用程式服務的 hello 功能，雲端服務、 虛擬機器和服務網狀架構 toohelp 做出 hello 最佳的選擇。 目前每個選項的 hello SLA 的詳細資訊，請參閱[Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

| 功能 | App Service (Web 應用程式) | 雲端服務 (Web 角色) | 虛擬機器 | Service Fabric | 注意事項 |
| --- | --- | --- | --- | --- | --- |
| 近乎即時的部署 |X | | |X |部署應用程式或應用程式更新 tooa 雲端服務，或建立 VM 時，需要數分鐘至少;部署應用程式 tooa web 應用程式需要秒的時間。 |
| 向上擴充 toolarger 機器，不需重新部署 |X | | |X | |
| 網頁伺服器執行個體共用內容和組態，這表示您尚未 tooredeploy 或重新設定調整。 |X | | |X | |
| 多個部署環境 (生產環境和預備環境) |X |X | |X |服務網狀架構可讓您 toohave toodeploy 不同您應用程式的並存版本或應用程式的多個環境。 |
| 自動管理 OS 更新 |X |X | | |已針對未來的 Service Fabric 版本規劃自動 OS 更新。 |
| 順暢切換平台 (輕鬆地切換到 32 位元或 64 位元) |X |X | | | |
| 利用 GIT、FTP 來部署程式碼 |X | |X | | |
| 利用 Web Deploy 來部署程式碼 |X | |X | |雲端服務支援 hello 使用 Web Deploy toodeploy 更新 tooindividual 角色執行個體。 不過，您無法將它用於初始部署角色，而且如果您使用 Web Deploy 更新您另外有 toodeploy tooeach 角色執行個體。 在實際執行環境的 hello 雲端服務的 SLA 的順序 tooqualify 會需要多個執行個體。 |
| 支援 WebMatrix |X | |X | | |
| 服務匯流排、 儲存體、 SQL Database 等存取 tooservices |X |X |X |X | |
| 裝載多層式架構的 Web 或 Web 服務層 |X |X |X |X | |
| 裝載多層式架構的中間層 |X |X |X |X |App Service web 應用程式可以輕鬆地裝載的 REST API 中介層，並 hello [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226)功能可以裝載背景處理工作。 您可以執行 WebJobs hello 層的專用的網站 tooachieve 獨立延展性。 hello 預覽[API apps](../app-service-api/app-service-api-apps-why-best-platform.md)功能提供更多的功能，來主控 REST 服務。 |
| 整合 MySQL 即服務的支援 |X |X |X | |雲端服務可以整合 MySQL 做為服務，透過 ClearDB 的供應項目，但不是能作為 hello Azure 入口網站工作流程的一部分。 |
| 支援 ASP.NET、傳統 ASP、Node.js、PHP、Python |X |X |X |X |Service Fabric 支援 hello 建立的 web 前端 using [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md)或將任何類型 （Node.js、 Java 等） 的應用程式部署為[客體可執行檔](../service-fabric/service-fabric-deploy-existing-app.md)。 |
| 擴充 toomultiple 不需重新部署的執行個體 |X |X |X |X |虛擬機器可以擴充 toomultiple 執行個體，但在其上執行的 hello 服務必須寫入 toohandle 此向外延展。您有 tooconfigure hello 機器間的負載平衡器 tooroute 要求，並建立同質群組 tooprevent 到期 toomaintenance 或硬體失敗的所有執行個體同時重新啟動。 |
| 支援 SSL |X |X |X |X |在 App Service Web 應用程式中，只有基本和標準模式才支援自訂網域名稱的 SSL。 如需 Web 應用程式使用 SSL 的相關資訊，請參閱[設定 Azure 網站的 SSL 憑證](app-service-web-tutorial-custom-ssl.md)。 |
| 整合 Visual Studio |X |X |X |X | |
| 遠端偵錯 |X |X |X | | |
| 利用 TFS 來部署程式碼 |X |X |X |X | |
| 利用 [Azure 虛擬網路](/azure/virtual-network/) |X |X |X |X |另請參閱＜ [Azure 網站虛擬網路整合](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| 支援 [Azure 流量管理員](/azure/traffic-manager/) |X |X |X |X | |
| 整合式端點監視 |X |X |X | | |
| 遠端桌面存取 tooservers | |X |X |X | |
| 安裝任何自訂 MSI | |X |X |X |服務網狀架構可讓您任何可執行檔的檔案做為 toohost[客體可執行檔](../service-fabric/service-fabric-deploy-existing-app.md)或您可以在 hello Vm 上安裝任何應用程式。 |
| Toodefine/執行啟動工作的能力 | |X |X |X | |
| 可以接聽 tooETW 事件 | |X |X |X | |

## <a name="scenarios"></a>案例和建議
以下是一些常見的應用程式案例的建議為可能最適合用於每個 toowhich Azure web 裝載選項。

* [我需要與背景處理和資料庫後端 toorun 商務應用程式與內部部署資產整合的 web 前端。](#onprem)
* [我需要可靠的方式 toohost 連線到縮放區域和全域優惠我公司網站。](#corp)
* [我有一個在 Windows Server 2003 上執行的 IIS6 應用程式。](#iis6)
* [我是小型企業的擁有者，以及需要經濟的方式 toohost 我的站台但記住未來成長使用。](#smallbusiness)
* [Web 角色或圖形設計人員，我和我想 toodesign 並建置網站的 我的客戶。](#designer)
* [我正在移轉我的多層式應用程式與 web 前端 toohello 雲端。](#multitier)
* [我的應用程式相依於高度自訂的 Windows 或 Linux 的環境，而且我想 toomove 它 toohello 雲端。](#custom)
* [我的站台使用開放原始碼軟體，而我想要 toohost 它在 Azure 中。](#oss)
* [我有一個需要 tooconnect toohello 公司網路的特定業務應用程式。](#lob)
* [我想 toohost 行動用戶端的 REST API 或 web 服務。](#mobile)

### <a id="onprem"></a>我需要與背景處理和資料庫後端 toorun 商務應用程式與內部部署資產整合的 web 前端。
Azure App Service 是複雜商業應用程式的絕佳解決方案。 它可讓您開發應用程式的負載平衡的平台上的自動調整規模、 使用 Active Directory、 保護和 tooyour 在內部部署資源連接。 它會建立管理簡單的世界級的入口網站和 Api，透過這些應用程式，並可讓您 toogain 深入了解客戶如何使用它們以應用程式深入解析工具。 hello [Webjobs] [ Webjobs]功能可讓您執行背景處理程序和工作做為您的 web 層，在混合式連線和 VNET 功能時的一部分讓您輕鬆 tooconnect 後 tooon 內部部署資源。 Azure App Service 為 Web 應用程式提供三個 9 的 SLA，可讓您：

* 在自我修復、自動修補的雲端平台上可靠地執行應用程式。
* 在全球的資料中心網路上自動調整。
* 針對災害復原進行備份與還原。
* 符合 ISO、SOC2 和 PCI。
* 與 Active Directory 整合

### <a id="corp"></a>我需要可靠的方式 toohost 連線到縮放區域和全域優惠我公司網站。
Azure App Service 是裝載公司網站的絕佳解決方案。 它可讓 web 應用程式 tooscale 快速並輕鬆地 toomeet 要求的資料中心全球網路。 它提供本機存取、容錯和智慧型流量管理。 所有平台上，提供世界級的管理工具，可讓您 toogain 深入了解站台健全狀況和站台流量快速輕鬆。 Azure App Service 為 Web 應用程式提供三個 9 的 SLA，可讓您：

* 在自我修復、自動修補的雲端平台上可靠地執行網站。
* 在全球的資料中心網路上自動調整。
* 針對災害復原進行備份與還原。
* 使用整合式工具來管理記錄和流量。
* 符合 ISO、SOC2 和 PCI。
* 與 Active Directory 整合

### <a id="iis6"></a> 我有一個在 Windows Server 2003 上執行的 IIS6 應用程式。
Azure App Service 可讓您輕鬆 tooavoid hello 移轉較舊的 IIS6 應用程式相關聯的基礎結構成本。 Microsoft 已建立[輕鬆 toouse 移轉工具和詳細的移轉指引](https://www.movemetowebsites.net/)，可讓您 toocheck 相容性並識別任何需要 toobe 所做的變更。 與 Visual Studio、 TFS、 如何和常見的 CMS 工具整合可讓您輕鬆 toodeploy IIS6 應用程式直接 toohello 雲端。 一旦部署之後，hello Azure 入口網站提供強大的管理工具，可讓您 tooscale toomanage 成本下和向上視 toomeet 需求。 您可以使用 hello 移轉工具：

* 快速且輕鬆地移轉舊版 Windows Server 2003 web 應用程式 toohello 雲端。
* 選擇 tooleave 您附加的 SQL 資料庫內部 toocreate 混合式應用程式。
* 自動隨著舊式應用程式一起移動 SQL 資料庫。

### <a id="smallbusiness"></a>我是小型企業的擁有者，以及需要經濟的方式 toohost 我的站台但記住未來成長使用。
Azure App Service 是此案例的絕佳解決方案，因為您可先免費使用它，等到需要更多功能時再新增功能即可。 每個可用的 web 應用程式隨附 Azure 提供的網域 (*your_company*。 名稱是.azurewebsites.net)，和 hello 平台包含整合的部署和管理工具，以及應用程式庫，可讓您輕鬆 tooget 啟動。 還有許多其他服務和縮放選項，可讓 hello 網站 tooevolve 以提高的使用者要求。 使用 Azure App Service，您可以：

* Hello 免費層的開頭，並視需要調整。
* 使用 hello 應用程式庫 tooquickly 設定熱門的 web 應用程式，例如 WordPress。
* 視需要新增其他 Azure 服務和功能 tooyour 應用程式。
* 使用 HTTPS 來保護 Web 應用程式。

### <a id="designer"></a>Web 角色或圖形設計人員，我和我想 toodesign 並建置網站的 我的客戶
對於 Web 開發人員和設計人員，Azure App Service 可輕鬆整合各種架構和工具、提供 Git 和 FTP 的部署支援，並與 Visual Studio 和 SQL Database 等工具和服務密切整合。 使用 App Service，您可以：

* 使用命令列工具執行[自動化工作][scripting]。
* 使用熱門語言，例如 [.Net][dotnet]、[PHP][PHP]、[Node.js][nodejs] 及 [Python][Python]。
* 選取三個不同縮放層級的向上擴充 toovery 高容量。
* 與其他 Azure 服務，例如整合[SQL Database][sqldatabase]， [Service Bus] [ servicebus]和[儲存體][ Storage]，或合作夥伴供應項目從 hello [Azure 市集][azurestore]，例如 MySQL 和 MongoDB。
* 與 Visual Studio、Git、WebMatrix、WebDeploy、TFS 和 FTP 等工具整合。

### <a id="multitier"></a>我正在移轉我的多層式應用程式與 web 前端 toohello 雲端
如果您正在執行的多層式應用程式，例如連接 tooa 資料庫的 web 伺服器 Azure App Service 是一個不錯的選項，可提供與 Azure SQL Database 的緊密整合。 而且，您可以使用 hello WebJobs 功能的執行後端處理程序。

如果您需要更多控制 hello server 環境，例如 hello 能力 tooremote 到您的伺服器，或設定伺服器啟動工作，請選擇 Service Fabric 的一個或多個您層。

虛擬機器的一或多個您層如果您想選擇 toouse 電腦映像，或執行伺服器軟體或服務，您無法設定服務的網狀架構上。

### <a id="custom"></a>我的應用程式相依於高度自訂的 Windows 或 Linux 的環境，而且我想 toomove 它 toohello 雲端。
如果您的應用程式需要複雜的安裝或軟體和 hello 作業系統設定，虛擬機器可能是 hello 最佳解決方案。 虛擬機器可讓您：

* Hello 虛擬機器資源庫 toostart 使用作業系統，例如 Windows 或 Linux，，然後為您的應用程式需求加以自訂。
* 建立並上傳現有內部部署伺服器 toorun 在 Azure 中的虛擬機器上的自訂映像。

### <a id="oss"></a>我的站台使用開放原始碼軟體，而我想要 toohost 它在 Azure 中
如果應用程式服務，hello 語言支援開放原始碼架構應用程式所需的架構將會為您自動設定。 App Service 可讓您：

* 使用許多熱門的開放原始碼語言，例如 [.NET][dotnet]、[PHP][PHP]、[Node.js][nodejs] 和 [Python][Python]。
* 設定 WordPress、Drupal、Umbraco、DNN 及其他許多協力廠商 Web 應用程式。
* 移轉現有的應用程式，或建立一個新的 hello 應用程式庫。

如果應用程式服務不支援開放原始碼架構，您可以執行它 hello 的其中一個上其他裝載選項的 Azure web。 虛擬機器，安裝和設定上 hello 機器映像，這可以是 Windows hello 軟體或以 Linux 為基礎。

### <a id="lob"></a>我有一個需要 tooconnect toohello 公司網路的特定業務應用程式
如果您想 toocreate 特定業務應用程式，您的網站可能需要直接存取 tooservices 或 hello 公司網路上的資料。 這是可行的應用程式服務，Service Fabric 和虛擬機器上使用 hello [Azure 虛擬網路服務](/azure/virtual-network/)。 App Service 上，您可以使用 hello [VNET 整合功能](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)，可讓您的 Azure 應用程式 toorun，如同它們是在您的公司網路上。

### <a id="mobile"></a>我想 toohost 行動用戶端的 REST API 或 web 服務
以 HTTP 為基礎的 web 服務可讓您 toosupport 各種不同的用戶端，包括行動用戶端。 ASP.NET Web API 類似的架構整合 Visual Studio toomake 它更容易 toocreate 並取用 REST 服務。  這些服務由 web 端點公開，因此您很可能 toouse 任何 web 裝載技術在 Azure toosupport 這種情況。 不過，App Service 是裝載 REST API 的絕佳選擇。 使用 App Service，您可以：

* 快速建立[行動裝置應用程式](../app-service-mobile/app-service-mobile-value-prop.md)或[API 應用程式](../app-service-api/app-service-api-apps-why-best-platform.md)toohost hello HTTP web 服務，其中一種 Azure 的全域散發的資料中心。
* 移轉現有的服務或建立新服務。
* 達到 SLA 的可用性是單一執行個體，或擴充 toomultiple 專用機器。
* 使用 hello 發佈站台 tooprovide REST Api tooany HTTP 用戶端，包括行動用戶端。

> [!NOTE]
> 如果您想 tooget 開始使用 Azure App Service 的帳戶註冊前，請移至太<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>，其中您可以立即建立存留較短的起始應用程式在 Azure App Service 中免費。 不需要信用卡，沒有承諾。
> 
> 

## <a id="nextsteps"></a> 後續步驟
如需 hello 三個 web 裝載選項的詳細資訊，請參閱[Azure 簡介](../fundamentals-introduction-to-azure.md)。

tooget 入門 hello 選擇選項，您的應用程式，請參閱下列資源的 hello:

* [Azure App Service](/azure/app-service/)
* [Azure 雲端服務](/azure/cloud-services/)
* [Azure 虛擬機器](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
