---
title: "aaaWeb 應用程式的概觀 |Microsoft 文件"
description: "了解 Azure App Service 如何協助您開發和裝載 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Web 應用程式概觀
 是受到完整管理的計算平台，非常適合用來裝載網站和 Web 應用程式。 這[平台做為服務](https://en.wikipedia.org/wiki/Platform_as_a_service)(PaaS) 的 Microsoft Azure 的供應項目可讓您專注於商務邏輯，而 Azure 會負責 hello 基礎結構 toorun 及調整您的應用程式。

hello 後 5 分鐘的影片介紹 Azure App Service Web 應用程式。

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>什麼是 App Service 中的 Web 應用程式？
App Service 中*web 應用程式*為 hello Azure 提供裝載的網站或 web 應用程式的計算資源。  

共用或專用虛擬機器 (Vm)，根據定價層，您所選擇的 hello 可能 hello 計算資源。 應用程式的程式碼會在與其他客戶隔離開來的受管理 VM 中執行。

程式碼可以使用 [Azure App Service](../app-service/app-service-value-prop-what-is.md)所支援的任何語言或架構，例如 ASP.NET、Node.js、Java、PHP 或 Python。 您也可以在 Web 應用程式中，執行使用 [PowerShell 和其他指令碼語言](web-sites-create-web-jobs.md#acceptablefiles) 的指令碼。

一般應用程式案例的範例，可用於 Web 應用程式，請參閱[Web 應用程式情節](https://azure.microsoft.com/documentation/scenarios/web-app/)和 hello**案例與建議**區段[Azure 應用程式服務、 虛擬電腦、 服務網狀架構和雲端服務的比較](choose-web-site-cloud-service-vm.md#scenarios)。

## <a name="why-use-web-apps"></a>為何要使用 Web Apps？
以下是適用於 tooWeb 應用程式的應用程式服務的部分主要功能：

* **多種語言和架構** - App Service有 ASP.NET、Node.js、Java、PHP 和 Python 的頂級支援。 您也可以在 App Service VM 上執行 [PowerShell 和其他指令碼或可執行檔](web-sites-create-web-jobs.md) 。
* **DevOps 最佳化** - 使用 Visual Studio Team Services、GitHub 或 BitBucket 設定 [持續整合和部署](app-service-continuous-deployment.md) 。 透過 [測試和預備環境](web-sites-staged-publishing.md)升級更新。 執行 [A/B 測試](app-service-web-test-in-production-get-start.md)。 管理您的應用程式，App Service 中使用[Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello[跨平台命令列介面 (CLI)](../cli-install-nodejs.md)。
* **具高可用性的全域調整** - 以手動或自動方式相應[增加](web-sites-scale.md)或[放大](../monitoring-and-diagnostics/insights-how-to-scale.md)。 裝載任何位置在 Microsoft 的全域資料中心基礎結構，應用程式和應用程式服務的 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/)承諾高可用性。
* **Connections tooSaaS 平台和內部部署資料**-選擇超過 50[連接器](../connectors/apis-list.md)企業系統 （例如 SAP、 Siebel 和 Oracle），如 SaaS 服務 （例如 Salesforce 和 Office 365） 和網際網路服務 （例如 Facebook 和 Twitter）。 使用[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和 [Azure 虛擬網路](web-sites-integrate-with-vnet.md)存取內部部署資料。
* **安全性和法規遵循** - App Service 為 [ISO、SOC 和 PCI 相容](https://www.microsoft.com/TrustCenter/)。
* **應用程式範本**-從應用程式中的範本 hello 延伸清單中選擇[Azure Marketplace](https://azure.microsoft.com/marketplace/) ，可讓您使用精靈 tooinstall 熱門開放原始碼軟體，例如 WordPress、 Joomla 和 Drupal。
* **Visual Studio 整合**-Visual Studio 中的專用的工具簡化 hello 工作建立、 部署和偵錯。

此外，Web 應用程式可以利用 [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (例如 CORS 支援) 和 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (例如推播通知) 所提供的功能。 如需 App Service 中的應用程式類型詳細資訊，請參閱 [Azure App Service 概觀](../app-service/app-service-value-prop-what-is.md)。

除了 App Service 中的 Web Apps，Azure 還提供可用來裝載網站和 Web 應用程式的其他服務。 大部分情況下，Web 應用程式會是 hello 最佳選擇。  對於微服務的架構，請考慮[Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)，如果您需要更充分掌控 hello Vm 上執行您的程式碼，請考慮和[Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。 如需有關如何 toochoose 之間這些 Azure 服務，請參閱[Azure 應用程式服務、 虛擬機器、 服務網狀架構和雲端服務的比較](choose-web-site-cloud-service-vm.md)。

## <a name="getting-started"></a>開始使用
tooget 啟動部署的範例程式碼 tooa 新 web 應用程式在應用程式服務中，依照下列其中一個 hello 下列下拉式方塊中的 hello 教學課程。 您將需要免費的 Azure 帳戶。

> [!div class="op_single_selector"]
> * [在 5 分鐘內部署您的第一個 ASP.NET web 應用程式 tooAzure](app-service-web-get-started-dotnet.md)
> * [在 5 分鐘內部署第一個的 PHP web 應用程式 tooAzure](app-service-web-get-started-php.md)
> * [在 5 分鐘內部署您的第一個 Node.js web 應用程式 tooAzure](app-service-web-get-started-nodejs.md)
> * [在 5 分鐘內部署第一個的 Java web 應用程式 tooAzure](app-service-web-get-started-java.md)
> * [在 5 分鐘內部署第一個的 Python web 應用程式 tooAzure](app-service-web-get-started-python.md)
> * [在 5 分鐘內部署您的第一個 HTML 網站 tooAzure](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> 您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。 建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。
> 
> 
