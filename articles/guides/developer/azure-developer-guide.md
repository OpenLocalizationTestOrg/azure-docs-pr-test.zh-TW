---
title: "開發人員在 Azure 上的啟動 aaaGet 指南 |Microsoft 文件"
description: "本主題提供開發人員尋找 tooget 開始開發需要使用 hello Microsoft Azure 平台的重要資訊。"
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Azure 開發人員開始使用指南

## <a name="what-is-azure"></a>何謂 Azure？

Azure 是一個完整的雲端平台，可以裝載的現有應用程式，簡化 hello 開發新的應用程式，而且即使加強在內部部署應用程式。 Azure 整合您需要 toodevelop hello 雲端服務、 測試、 部署和管理您的應用程式，同時利用雲端的 hello 效率的運算。

在 Azure 中裝載應用程式，即可從小規模著手，並隨著客戶需求的成長，輕鬆地調整應用程式。 Azure 還提供高可用性應用程式，甚至包括不同地區之間的容錯移轉所需的 hello 可靠性。 hello [Azure 入口網站](https://portal.azure.com)可讓您輕鬆地管理您所有的 Azure 服務。 您也可以使用服務特定 API 和範本，以程式設計方式管理服務。

**誰應該閱讀這**： 本指南是簡介 toohello Azure 平台應用程式開發人員。 它提供指引和您需要建立新的應用程式在 Azure 或移轉現有的應用程式 tooAzure toostart 的方向。

## <a name="where-do-i-start"></a>我該從哪裡開始？

與所有 hello Azure 所提供服務，它可以是鉅的任務 toofigure 哪些服務您需要 toosupport 您方案的架構。 此區段會反白顯示 hello Azure 服務開發人員常使用。 如需所有 Azure 服務的清單，請參閱 hello [Azure 文件](../../index.md)。

首先，您必須決定如何 toohost 您在 Azure 中的應用程式。 您需要 toomanage 整個基礎結構做為虛擬機器 (VM)。 您可以使用 Azure 提供的 hello 平台管理功能嗎？ 您可能需要的無伺服器架構 toohost 程式碼執行只有嗎？

您的應用程式需要 Azure 提供數個選項的雲端儲存體。 您可以利用 Azure 的企業驗證。 另外還有工具可進行雲端式開發和監視，而且大部分的裝載服務提供 DevOps 整合。

現在，讓我們看看一些 hello 我們建議您調查應用程式的特定服務。

### <a name="application-hosting"></a>應用程式裝載

Azure 提供數個雲端為基礎的計算供應項目 toorun 您的應用程式，讓您不需要 tooworry hello 基礎結構的詳細。 隨著您應用程式使用的成長，您可以輕鬆地向上延展或向外延展資源。

Azure 提供可支援應用程式開發和裝載需求的服務。 Azure 提供基礎結構做為服務 (IaaS) toogive 完整控制您的應用程式託管服務。 Azure 的平台做為服務 (PaaS) 供應項目提供 hello 完全管理所需的服務 toopower 您的應用程式。 沒有在 Azure 中即使無伺服器裝載需要 toodo 是撰寫程式碼。

![Azure 應用程式裝載選項](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure App Service 

當您想快速路徑 toopublish hello web 專案時，請考慮 Azure 應用程式服務。 應用程式服務可讓您輕鬆 tooextend 您 web 應用程式 toosupport 行動用戶端和發佈方便取用的 REST Api。 此平台提供驗證的方式是使用社交提供者、流量自動調整，在生產環境中測試，以及持續的容器部署。

當您建立應用程式，App Service 中時，您可以選取其中一個 hello 下列類型：

- [Web 應用程式](../../app-service-web/app-service-web-overview.md)：可讓您裝載以 .NET、Java、PHP、Node.js 和 Python 撰寫的網站和 Web 應用程式。

- [行動應用程式](../../app-service-mobile/app-service-mobile-value-prop.md)： 可擴充的 Web 應用程式的行動裝置的 toosupport 存取。 它啟用社交提供者和 Azure Active Directory (Azure AD) 的驗證、提供後端儲存體，以及與推播通知的 [Azure 通知中樞](../../notification-hubs/notification-hubs-push-notification-overview.md)整合。

- [API Apps](../../app-service-api/app-service-api-apps-why-best-platform.md)： 可讓您更安全地公開 hello 與 Swagger 中繼資料的雲端中您應用程式開發介面，讓用戶端可以輕鬆使用它們。

因為所有的三個應用程式類型共用 hello 應用程式服務執行階段，您可以主控網站、 支援行動裝置用戶端，並在 Azure 中，您應用程式開發介面公開全部從 hello 相同專案或方案。 toolearn 進一步了解應用程式服務，請參閱[應用程式服務的運作方式](../../app-service/app-service-how-works-readme.md)。

請注意，已使用 DevOps 設計 App Service。 它支援用於發佈和持續整合部署的各種工具，包含 GitHub Webhook、Jenkins、Visual Studio Team Services、TeamCity 和其他工具。

您可以利用 hello 移轉您現有的應用程式 tooApp 服務[線上移轉工具](https://www.migratetoazure.net/)。

>**當 toouse**： 使用應用程式服務，當您移轉現有的 web 應用程式 tooAzure，以及當您的 web 應用程式需要完全受管理的裝載平台。 當您需要 toosupport 行動用戶端，或公開 REST Api 與您的應用程式時，您也可以使用應用程式服務。

>**開始**： 應用程式服務可讓您輕鬆 toocreate 及部署您的第一個[web 應用程式](../../app-service-web/web-sites-dotnet-get-started.md)，[行動裝置應用程式](../../app-service-mobile/app-service-mobile-ios-get-started.md)，或[API 應用程式](../../app-service-api/app-service-api-dotnet-get-started.md)。

>**現在就試試**： 應用程式服務可讓您佈建存留較短的應用程式 tootry hello 平台，而不需要 toosign 註冊 Azure 帳戶。 再試一次 hello 平台和[建立您的 Azure App Service 應用程式](https://tryappservice.azure.com/)。

#### <a name="azure-virtual-machines"></a>Azure 虛擬機器

為基礎結構做為服務 (IaaS) 提供者，Azure 可讓您部署 tooor 移轉您的應用程式 tooeither Windows 或 Linux Vm。 Azure 虛擬網路，以及 Azure 虛擬機器支援 Windows 或 Linux Vm tooAzure hello 的部署。 使用 Vm，您擁有 hello hello 機器組態的完整控制權。 使用 VM 時，您負責所有伺服器軟體安裝、設定、維護和作業系統修補程式。

因為有 Vm 的控制 hello 層級，您可以執行各種不同的伺服器工作負載上並不適合的 Azure PaaS 模型。 這些工作負載包含資料庫伺服器、Windows Server Active Directory 和 Microsoft SharePoint。 如需詳細資訊，請參閱 hello 虛擬機器文件，其中一個[Linux](/azure/virtual-machines/linux/)或[Windows](/azure/virtual-machines/windows/)。

>**當 toouse**： 當您想要完整使用虛擬機器而不需要 toomake 變更控制您應用程式基礎結構或 toomigrate 在內部部署應用程式工作負載 tooAzure。

>**開始**： 建立[Linux VM](../../virtual-machines/virtual-machines-linux-quick-create-portal.md)或[Windows VM](../../virtual-machines/virtual-machines-windows-hero-tutorial.md)從 hello Azure 入口網站。

#### <a name="azure-functions-serverless"></a>Azure Functions (無伺服器)

而不是的擔心建置和管理整個應用程式或 hello 基礎結構 toorun 您的程式碼。 如果您無法只撰寫程式碼，並讓它在回應 tooevents 或根據排程執行嗎？  [Azure 函數](../../azure-functions/functions-overview.md)是 「 無伺服器 」 的-供應項目可讓您撰寫只 hello 您需要的程式碼的樣式。 使用 Functions，程式碼執行是由 HTTP 要求、Webhook、雲端服務事件或依排程觸發。 您也可以使用選擇的開發語言編寫程式碼，例如 C\#、F\#、Node.js、Python 或 PHP。 消費型計費，您只針對付費 hello 您的程式碼執行，而且 Azure 就會隨著所需的時間。

>**當 toouse**： 當您有其他 Azure 服務，由 web 為基礎的事件，或根據排程觸發的程式碼時，使用 Azure 函數。 當您不需要 hello 完整裝載的專案，或當您只想 toopay hello 時間，您的程式碼執行的額外負荷，也可以使用函式。 詳細資訊，請參閱 toolearn [Azure 函式概觀](../../azure-functions/functions-overview.md)。

>**開始**： 太遵循 hello 函式的快速入門教學課程[建立您的第一個函式](../../azure-functions/functions-create-first-azure-function.md)從 hello 入口網站。

>**現在就試試**: Azure 函式可讓您執行程式碼，而不需要 toosign 註冊 Azure 帳戶。 請立即試用，並[建立您的第一個 Azure 函式](https://tryappservice.azure.com/)。

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric 是分散式的系統平台，可讓您輕鬆 toobuild，封裝、 部署及管理可擴充且可靠的 microservices。 還提供完整的應用程式管理功能，以佈建、部署、監視、升級/修補及刪除所部署的應用程式。 應用程式，在機器的共用集區上執行，也可以從小型專案開始並 toohundreds 或數千部電腦，視需要調整。

Service Fabric 支援具有 Open Web Interface for .NET (OWIN) 和 ASP.NET Core 的 WebAPI。 它提供在 Linux 上建置服務的 .NET Core 和 Java SDK。 toolearn 深入了解服務的網狀架構，請參閱 hello [Service Fabric 學習路徑](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)。

>**當 toouse:** Service Fabric 是不錯的選擇，當您在建立應用程式或重寫現有的應用程式 toouse 微服務架構。 當您需要更多控制或直接存取，hello 基礎結構時，請使用 Service Fabric。

>**開始使用**[：建立第一個 Azure Service Fabric 應用程式](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md)。

### <a name="enhance-your-applications-with-azure-services"></a>使用 Azure 服務增強應用程式

此外 tooapplication 裝載，Azure 會提供可強化 hello 功能、 開發和維護您的應用程式，在 hello 雲端和內部部署的服務供應項目。

#### <a name="hosted-storage-and-data-access"></a>託管儲存體和資料存取

大部分的應用程式必須在 Azure 中儲存資料，因此無論您決定如何將 toohost 您的應用程式，請考慮一或多個下列儲存體和資料服務的 hello。

-   **Azure SQL Database**： 為 Azure 為基礎的 hello 雲端中儲存關聯式表格式資料的 hello Microsoft SQL Server 引擎版本。 SQL Database 提供可預測的效能、無停機時間的延展性、商務持續性和資料保護功能。

    >**當 toouse**： 當您的應用程式需要具有參考完整性、 交易支援，以及支援的資料儲存體 TSQL 查詢。

    >**開始**:[利用 hello Azure 入口網站，以分鐘為單位建立 SQL database](../../sql-database/sql-database-get-started.md)。

-   **Azure 儲存體**：提供 Blob、佇列、檔案和其他類型之非關聯式資料的持久性高可用性儲存體。 儲存體提供 Vm hello 儲存體的基礎。

    >**當 toouse**： 當您的應用程式會儲存非關聯式資料，索引鍵-值組 （資料表），例如 blob、 檔案共用，或訊息 （如果是佇列）。

    >**開始使用**：選擇下列其中一種類型的儲存體：[Blob](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)、[資料表](../../cosmos-db/table-storage-how-to-use-dotnet.md)、[佇列](../../storage/queues/storage-dotnet-how-to-use-queues.md)或[檔案](../../storage/files/storage-dotnet-how-to-use-files.md)。

-   **Azure DocumentDB**：完整受管理和可擴充的 NoSQL 資料庫服務，其具備物件資料的 SQL 查詢。 您可以使用現有 MongoDB 驅動程式存取 DocumentDB。
    >**當 toouse:**應用程式需要 toobe 無法 tooexecute SQL 查詢所有 JSON 文件，或如果您使用 MongoDB。

    >**開始使用**：[建置 DocumentDB C# 主控台應用程式](../../documentdb/documentdb-get-started.md)。 如果您是 MongoDB 開發人員，請參閱 [MongoDB 的 DocumentDB 通訊協定支援](../../documentdb/documentdb-protocol-mongodb.md)。

您可以使用[Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove 現有內部部署資料 tooAzure。 如果您不準備 toomove 資料 toohello 雲端，[混合式連線](../../biztalk-services/integration-hybrid-connection-overview.md)在 BizTalk 服務可讓您連接您的應用程式服務會裝載應用程式 tooon 內部部署資源。 您也可以從內部部署應用程式連接 tooAzure 資料和儲存體服務。

#### <a name="docker-support"></a>Docker 支援

Docker 容器是一種 OS 虛擬化，可讓您透過更有效率且可預測的方式部署應用程式。 容器化應用程式適用於生產環境的 hello 相同方式為開發和測試系統上。 您可以使用標準 Docker 工具來管理容器。 您可以使用您現有的技術和熱門的開放原始碼工具 toodeploy 和管理容器應用程式在 Azure 上。

Azure 提供數種方式在應用程式中的 toouse 容器。

-   **Azure 的 Docker VM 擴充功能**： 可讓您設定您的 VM 與 Docker 工具 tooact Docker 主機。

    >**當 toouse**： 當您想 toogenerate 一致的容器部署應用程式在 VM 上，或是當您想 toouse [Docker Compose](https://docs.docker.com/compose/overview/)。

    >**開始**:[使用 hello Docker VM 擴充功能，在 Azure 中建立 Docker 環境](../../virtual-machines/virtual-machines-linux-dockerextension.md)。

-   **Azure 容器服務**： 可讓您建立、 設定和管理叢集的虛擬機器會預先設定 toorun 容器化應用程式。 toolearn 進一步了解容器服務，請參閱[Azure 容器服務簡介](../../container-service/container-service-intro.md)。

    >**當 toouse**： 當您需要 toobuild 備妥、 可擴充式環境，提供額外的排程和管理工具，或當您要部署 Docker Swarm 叢集。

    >**開始使用**：[部署容器服務叢集](../../container-service/dcos-swarm/container-service-deployment.md)。

-   **Docker Machine**：可讓您使用 docker-machine 命令安裝和管理虛擬主機上的 Docker 引擎。

    >**當 toouse**： 當您需要 tooquickly 原型應用程式藉由建立單一的 Docker 主機。

-   **App Service 的自訂 Docker 映像**：在 Linux 上部署 Web 應用程式時，可讓您使用容器登錄或客戶容器中的 Docker 容器。

    >**當 toouse**： 部署 Linux tooa Docker 映像上的 web 應用程式時。

    >**開始使用**：[針對 Linux 上的 App Service 使用自訂 Docker 映像](../../app-service-web/app-service-linux-using-custom-docker-image.md)。

### <a name="authentication"></a>驗證

它的重要 toonot 只知道誰在使用您應用程式，但也 tooprevent 未經授權存取 tooyour 資源。 Azure 提供數種方式 tooauthenticate 您應用程式的用戶端。

-   **Azure Active Directory (Azure AD)**: hello Microsoft 多租用戶、 雲端身分識別和存取管理服務。 您可以新增單一登入 (SSO) tooyour 應用程式，藉由使用 Azure AD 整合。 您可以藉由直接 hello Azure AD Graph API 或 hello Microsoft Graph API 存取目錄內容。 您可以使用原生 HTTP/REST 端點整合 Azure AD 支援 hello OAuth2.0 授權架構，並開啟連接的識別碼，並 hello 多平台 Azure AD 驗證程式庫。

    >**當 toouse**： 當您想 tooprovide SSO 的體驗時，請使用圖形為基礎的資料，或驗證網域的使用者。

    >**開始**: toolearn 詳細資訊，請參閱 hello [Azure Active Directory 開發人員手冊 》](../../active-directory/active-directory-developers-guide.md)。

-   **應用程式服務驗證**： 當您選擇應用程式服務 toohost 您的應用程式時，您也可以取得的 Azure AD，社交身分識別提供者以及內建的驗證支援，包括 Facebook、 Google、 Microsoft 和 Twitter。

    >**當 toouse**： 當您想 tooenable 驗證的 App Service 應用程式中使用 Azure AD，社交身分識別提供者，或兩者。

    >**開始**: toolearn App Service 中的驗證詳細資料請參閱[驗證和授權的 Azure App Service](../../app-service/app-service-authentication-overview.md)。

toolearn 深入了解安全性最佳作法，在 Azure 中，請參閱[Azure 的安全性最佳作法和模式](../../security/security-best-practices-and-patterns.md)。

### <a name="monitoring"></a>監視

應用程式啟動並在 Azure 中執行，您需要 toobe 無法 toomonitor 效能，監看的問題，並請參閱客戶如何使用您的應用程式。 Azure 提供數個監視選項。

-   **Visual Studio Application Insights**： 整合與 Visual Studio toomonitor 即時 web 應用程式的 Azure 託管可延伸的分析服務。 它可提供您所需要 toocontinuously hello 資料改善 hello 效能和可用性的應用程式是否正在 azure 中裝載，或不。

    >**開始**： 後續 hello [Application Insights 教學課程](../../application-insights/app-insights-overview.md)。

-   **Azure 監視**: toovisualize、 查詢、 路由、 封存和在 hello 標準和您的 Azure 基礎結構與資源所產生的記錄檔上運作，可協助您的服務。 監視器 」 提供 hello 資料檢視，您在 hello Azure 入口網站中看到，並為單一來源 Azure 資源的監視。
 
    >**開始使用**：[開始使用 Azure 監視器](../../monitoring-and-diagnostics/monitoring-get-started.md)。

### <a name="devops-integration"></a>DevOps 整合

它是佈建 Vm，或發行您的 web 應用程式，使用持續整合，Azure 會與大部分的 hello 熱門 DevOps 工具整合。 Jenkins、 GitHub、 Puppet、 Chef、 TeamCity、 Ansible、 VSTS，和其他類似的工具支援，您可以使用 hello 工具已經有和最大化您現有的體驗。

>**現在就試試：** [試用的 hello DevOps 整合數個](https://azure.microsoft.com/try/devops/)。

>**開始**: toosee DevOps 選項 App Service 應用程式中，請參閱[連續部署 tooAzure App Service](../../app-service-web/app-service-continuous-deployment.md)。


## <a name="azure-regions"></a>Azure 區域

Azure 是全域的雲端平台 hello 世界各地的許多地區處於正式推出。 當您佈建服務、 應用程式或在 Azure 中的 VM 時，您會詢問 tooselect 的區域，表示特定的資料中心執行應用程式，或儲存資料的地方。 這些區域對應 toospecific 位置，已發行 hello [Azure 區域](https://azure.microsoft.com/regions/)頁面。

### <a name="choose-hello-best-region-for-your-application-and-data"></a>選擇應用程式和資料的 hello 最佳區域

使用 Azure hello 優點的其中一個是您可以部署您的應用程式 toovarious 資料中心周圍 hello 地球。 您選擇的 hello 區域可能會影響應用程式的 hello 效能。 比方說，是較佳 toochoose 接近 toomost 的客戶 tooreduce 延遲的網路要求中的區域。 您也可能會想 tooselect 您地區 toomeet hello 的法律需求散發您的應用程式，在某些國家/地區。 一定會最佳的作法 toostore 應用程式資料在 hello 相同的資料中心或在資料中心，不久做為可能 toohello 資料中心裝載您的應用程式。

### <a name="multi-region-apps"></a>多區域應用程式

雖然不太可能，它不是不可能的整個資料中心 toogo 離線因為例如天然災害或網際網路失敗事件。 它是在多個資料中心 tooprovide 最大的可用性最佳作法 toohost 重要的商務應用程式。 使用多個區域也可以減少全域使用者的延遲，並在更新應用程式時提供彈性的其他機會。

某些服務，虛擬機器和應用程式服務，例如使用[Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) tooenable 多區域支援具有區域 toosupport 高可用性的企業應用程式之間的容錯移轉。 如需範例，請參閱 [Azure 參考架構︰高可用性的 Web 應用程式](../../guidance/guidance-web-apps-multi-region.md)。

>**當 toouse**： 當您有企業和高可用性受益於容錯移轉和複寫的應用程式。

## <a name="how-do-i-manage-my-applications-and-projects"></a>如何管理我的應用程式和專案？

Azure 提供一組豐富的體驗，讓您 toocreate 和管理您的 Azure 資源，應用程式和專案，以程式設計方式和在 hello [Azure 入口網站](https://portal.azure.com/)。

### <a name="command-line-interfaces-and-powershell"></a>命令列介面和 PowerShell

Azure 提供兩種方式 toomanage 應用程式和服務從 hello 命令列使用 Bash、 終端機、 hello 命令提示字元或您選擇的命令列工具。 通常，您可以從 hello 命令列，例如 hello Azure 入口網站執行相同工作的 hello — 例如建立和設定虛擬機器、 虛擬網路、 web 應用程式及其他服務。

-   [Azure 命令列介面 (CLI)](../../xplat-cli-install.md)： 可讓您連接 tooan Azure 訂用帳戶，以及程式針對從 hello 命令列的 Azure 資源的各種工作。

-   [Azure PowerShell](../../powershell-install-configure.md): toomanage Azure cmdlet 可讓您提供之模組的一組使用 Windows PowerShell 的資源。

### <a name="azure-portal"></a>Azure 入口網站

hello Azure 入口網站是網頁型應用程式，您可以使用 toocreate、 管理及移除 Azure 資源和服務。 hello Azure 入口網站位於<https://portal.azure.com>。它包含可自訂的儀表板、 工具來管理 Azure 資源，並存取 toosubscription 設定和帳單資訊。 如需詳細資訊，請參閱 hello [Azure 入口網站總覽](../../azure-portal-overview.md)。

### <a name="rest-apis"></a>REST API

Azure 是一組 REST Api，可支援 hello Azure 入口網站 UI 上所建立。 大部分的這些 REST Api 也會支援的 toolet 您以程式設計方式佈建和管理您的 Azure 資源和應用程式從任何已啟用網際網路的裝置。 Hello 的 REST API 文件的完整集合，請參閱 hello [Azure REST SDK 參考](https://docs.microsoft.com/rest/api/)。

### <a name="apis"></a>API

此外 tooREST 應用程式開發介面，許多 Azure 服務也可讓您以程式設計方式從您的應用程式管理資源，使用平台專屬的 Azure Sdk，包括 hello 遵循開發平台 Sdk:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

這類服務[行動應用程式](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md)和[Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md)提供用戶端 Sdk toolet 您從 web 和行動用戶端應用程式存取服務。

### <a name="azure-resource-manager"></a>Azure Resource Manager 
    
可能在 Azure 上執行您的應用程式牽涉到的工作與多個 Azure 服務，所有的用以 hello 相同生命週期，以及可以視為一個邏輯單位。 例如，Web 應用程式可能使用 Web Apps、SQL Database、Storage、Azure Redis Cache 和 Azure 內容傳遞網路服務。 [Azure 資源管理員](../../azure-resource-manager/resource-group-overview.md)可讓您以群組的應用程式中處理 hello 資源。 您可以部署、 更新或刪除所有的 hello 資源，在單一、 協調作業。

此外 toologically 群組和管理相關的資源，Azure 資源管理員包含部署功能可讓您自訂 hello 部署和設定相關資源。 例如，使用 Resource Manager，即可部署和設定將多個虛擬機器、一個負載平衡器和 Azure SQL Database 當成一個單位處理的應用程式。

透過使用本身為 JSON 格式化文件的 Azure Resource Manager 範本，即可開發這些部署。 範本可讓您定義部署，以及使用宣告式範本而非指令碼來管理應用程式。 您的範本可以用於測試、預備和生產這類不同環境。 比方說，藉由使用範本，您可以將部署的 Azure 服務，只要按一下 hello 儲存機制 tooa 集合中的 hello 程式碼的按鈕 tooa GitHub 儲存機制。

>**當 toouse**： 使用資源管理員範本，當您想 template 為基礎的部署，您可以使用 REST Api 以程式設計方式管理的應用程式時 hello Azure CLI 和 Azure PowerShell。

>**開始**: tooget 開始使用範本，請參閱[撰寫 Azure 資源管理員範本](../../resource-group-authoring-templates.md)。

## <a name="understanding-accounts-subscriptions-and-billing"></a>了解帳戶、訂用帳戶和計費

身為開發人員，我們喜歡 toodive 右到 hello 的程式碼，然後再次嘗試盡量讓我們的應用程式執行與啟動 tooget。 我們可以確定您需要 tooencourage 您 toostart Azure ad 中運作一樣容易。 使得輕鬆，Azure 優惠 toohelp[免費試用版](https://azure.microsoft.com/free/)。 某些服務即使有 「 試試免費 」 的功能，例如[Azure App Service](https://tryappservice.azure.com/)，而這並不需要太甚至建立帳戶。 為有趣，所以 toodive 到程式碼撰寫和部署您的應用程式 tooAzure，也很重要 tootake 某些時間 toounderstand，Azure 的使用者帳戶、 訂閱和帳單的觀點而言的運作方式。

### <a name="what-is-an-azure-account"></a>什麼是 Azure 帳戶？

toobe 無法 toocreate 或 Azure 訂用帳戶的工作，您必須擁有 Azure 帳戶。 Azure 帳戶就是 Azure AD 或目錄 (例如公司或學校組織) 中 Azure AD 所信任的身分識別。 如果您不屬於 toosuch 組織，您一律可以使用您所信任 Azure AD 的 Microsoft 帳戶來建立訂用帳戶。 toolearn 進一步了解在內部部署 Windows Server Active Directory 整合與 Azure AD，請參閱[整合內部部署身分識別與 Azure Active Directory](../../active-directory/active-directory-aadconnect.md)。

每個 Azure 訂用帳戶都會與 Azure AD 執行個體有信任關係。 這表示其信任該目錄 tooauthenticate 使用者、 服務和裝置。 多個訂閱可以信任 hello 相同的目錄，但訂閱只能信任一個目錄。 詳細資訊，請參閱 toolearn[如何 Azure 訂用帳戶相關聯 Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md)。

此外 toodefining 個別 Azure 帳戶的身分識別，也稱為*使用者*，您也可以定義*群組*在 Azure AD 中。 建立使用者群組是訂用帳戶中的好方法 toomanage 存取 tooresources 使用角色型存取控制 (RBAC)。 如何 toocreate 群組，請參閱的 toolearn[預覽 Azure Active Directory 中建立群組](../../active-directory/active-directory-groups-create-azure-portal.md)。 您也可以[使用 PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md) 建立和管理群組。

### <a name="manage-your-subscriptions"></a>管理訂用帳戶

訂用帳戶已是連結的 tooan Azure 帳戶的 Azure 服務的邏輯單元。 在訂用帳戶中，每個相關聯的帳戶都會有一個角色。 Azure 服務是根據訂用帳戶計費。 如需 hello 可用的訂用帳戶提供的類型，請參閱[Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/)。

#### <a name="administrator-roles"></a>系統管理員角色

Azure 訂用帳戶有多個您隨時可指派的帳戶系統管理員角色。

-   **帳戶管理員**： 此角色擁有完整控制權 hello 訂用帳戶，而且負責計費的 hello 帳戶。

-   **服務系統管理員**： 此角色的所有 hello 服務控制 hello 訂用帳戶中。 根據預設，這是 hello hello 帳戶系統管理員為使用相同帳戶。

-   **共同管理員**： 此角色的相同存取 hello 服務系統管理員，為 hello 不同之處在於它不能變更 hello 關聯的 hello 訂用帳戶 tooan Azure 目錄。

toolearn 進一步了解系統管理員角色，請參閱[如何 tooadd 或變更的 Azure 系統管理員角色](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription)。

#### <a name="resource-groups"></a>資源群組

當您佈建新的 Azure 服務時，即可在指定的訂用帳戶中這麼做。 個別 Azure 服務，也稱為資源，會建立資源群組的 hello 內容中。 資源群組使其更容易 toodeploy，且管理您的應用程式資源。 資源群組應該包含您想要做為一個單位使用 toowork 應用程式的所有 hello 資源。 您可以在資源群組及甚至 toodifferent 訂用帳戶之間移動資源。 toolearn 有關移動資源，請參閱[移動資源 toonew 資源群組或訂用帳戶](../../resource-group-move-resources.md)。

hello Azure 資源總管是視覺化您已經建立您的訂用帳戶中的 hello 資源的絕佳工具。 詳細資訊，請參閱 toolearn[使用 Azure 資源總管 tooview 和修改資源](../../resource-manager-resource-explorer.md)。

#### <a name="grant-access-tooresources"></a>授與存取 tooresources

當您允許存取 tooAzure 資源時，一律是最佳做法是提供使用者以 hello 最少權限的必要的 tooperform 指定的工作。

-   **角色型存取控制 (RBAC)**： 在 Azure 中，您可以授與存取 toouser 帳戶 （主體） 在指定的範圍： 訂用帳戶、 資源群組或個別的資源。 RBAC 可讓您將一組資源部署至資源群組，並授與權限 tooa 特定使用者或群組。 它也可讓您限制存取 tooonly hello 資源屬於 toohello 目標資源群組。 您也可以授與存取 tooa 單一資源，例如虛擬機器或虛擬網路。 toogrant 存取您指派角色 toohello 使用者、 群組或服務主體。 有許多預先定義的角色，而且您也可以定義自己的自訂角色。

    >**當 toouse**： 當您需要更細緻的存取管理使用者和群組。

    >**開始**: toolearn 詳細資訊，請參閱[開始使用 hello Azure 入口網站中存取管理](../../active-directory/role-based-access-control-what-is.md)。

-   **服務主體物件**： 此外 tooproviding 存取 toouser 主體和群組，您可以授與 hello 相同存取 tooa 服務主體。

    > **當 toouse**： 當您要以程式設計方式管理 Azure 資源或授與應用程式的存取。 如需詳細資訊，請參閱[建立 Active Directory 供應和服務主體](../../resource-group-create-service-principal-portal.md)。

#### <a name="tags"></a>標記

Azure 資源管理員可讓您將自訂標籤指派 tooindividual 資源。 當您的帳單或監視需要 tooorganize 資源時，標記，這是索引鍵 / 值組，可能很有用。 標記提供您方法 tootrack 資源跨越多個資源群組。 您可以指派 hello 入口網站，在 hello Azure Resource Manager 範本，或以程式設計的方式，使用 hello REST API、 hello Azure CLI 或 PowerShell 中的標記。 您可以將多個標記指派 tooeach 資源。 詳細資訊，請參閱 toolearn[使用標記 tooorganize 您的 Azure 資源](../../resource-group-using-tags.md)。

### <a name="billing"></a>計費

在從內部部署運算 toocloud 託管服務的 hello 移動，追蹤和服務使用方法和相關的成本估計是重要的考量因素。 它是重要的 toobe 無法 tooestimate 何種新的資源成本 toorun 每月為基礎。 您也需要 toobe 無法 tooproject hello 計費根據 hello 目前消費指定月份的外觀。

#### <a name="get-resource-usage-data"></a>取得資源使用量資料

Azure 提供一組計費 REST Api，讓存取 tooresource 耗用量和 Azure 訂用帳戶中繼資料資訊。 Hello 能力 toobetter 這些計費 Api 提供預測和管理 Azure 的成本。 您可以追蹤和分析每小時增加的花費、建立消費警示，並根據目前使用趨勢來預測未來計費。

>**開始**: toolearn 進一步了解使用 hello 計費的 Api，請參閱[Azure 計費的使用量和 RateCard Api 概觀](../../billing-usage-rate-card-overview.md)。

#### <a name="predict-future-costs"></a>預測未來成本

雖然它很困難，事先 tooestimate 成本，Azure 有[定價計算機](https://azure.microsoft.com/pricing/calculator/)評估 hello 成本時可以使用部署資源。 您也可以使用 hello hello 入口網站和 hello 計費 REST Api tooestimate 未來成本，根據目前的耗用量 [帳單] 刀鋒視窗。

>**開始使用**：請參閱 [Azure 計費使用和 RateCard API 概觀](../../billing-usage-rate-card-overview.md)。

#### <a name="set-up-billing-alerts"></a>設定帳務警示

您已部署應用程式或在 Azure 上的方案之後，您可以建立傳送您傳送電子郵件時 hello 的消費限制 hello 警示中所定義的警示。

>**開始**: toolearn 詳細資訊，請參閱[設定計費方式 Microsoft Azure 訂用帳戶的警示](../../billing-set-up-alerts.md)。
