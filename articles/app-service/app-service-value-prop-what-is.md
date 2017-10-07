---
title: "適用於 web、 mobile 和應用程式開發介面應用程式的應用程式服務 aaaAzure |Microsoft 文件"
description: "了解 Azure App Service 如何協助您開發、部署和管理 Web 和行動應用程式。"
keywords: "App Service, Azure App Service, App Service 成本, 級別, 可調整, 應用程式部署, Azure 應用程式部署, paas, 平台即服務, 網站, web, azure 行動"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>什麼是 Azure App Service？
 是 Microsoft Azure 的 [平台即服務](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) 供應項目。 建立適用任何平台或裝置的 Web 與行動應用程式。 整合您的應用程式與 SaaS 解決方案、與內部部署應用程式連接，並使您的商務程序自動化。 Azure 會使用您選擇的共用 VM 資源或專用 VM，在完全受管理的虛擬機器 (VM) 上執行您的應用程式。

應用程式服務包括 hello web 和行動我們先前分別以傳遞 Azure 網站和 Azure 行動服務的功能。 此外，它也包含可用來自動執行商務程序及裝載雲端 API 的新功能。 App Service 是單一的整合式服務，可讓您將各種元件 (網站、行動應用程式後端、RESTful API 和商務程序) 撰寫成單一解決方案。

hello 下列 4 分鐘影片提供的簡短說明的應用程式服務與 tooearlier Azure 的相關供應項目，並在其最新消息。

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>為何要使用 App Service？
以下是 App Service 的一些重要功能和能力︰

* **多種語言和架構** - App Service有 ASP.NET、Node.js、Java、PHP 和 Python 的頂級支援。 您也可以在 App Service VM 上執行 [Windows PowerShell 和其他指令碼或可執行檔](../app-service-web/web-sites-create-web-jobs.md) 。
* **DevOps 最佳化** - 使用 Visual Studio Team Services、GitHub 或 BitBucket 設定 [持續整合和部署](../app-service-web/app-service-continuous-deployment.md) 。 透過 [測試和預備環境](../app-service-web/web-sites-staged-publishing.md)升級更新。 執行 [A/B 測試](../app-service-web/app-service-web-test-in-production-get-start.md)。 管理您的應用程式，App Service 中使用[Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello[跨平台命令列介面 (CLI)](../cli-install-nodejs.md)。
* **具高可用性的全域調整** - 以手動或自動方式相應[增加](../app-service-web/web-sites-scale.md)或[放大](../monitoring-and-diagnostics/insights-how-to-scale.md)。 裝載任何位置在 Microsoft 的全域資料中心基礎結構，應用程式和應用程式服務的 hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/)承諾高可用性。
* **Connections tooSaaS 平台和內部部署資料**-選擇超過 50[連接器](../connectors/apis-list.md)企業系統 （例如 SAP、 Siebel 和 Oracle），如 SaaS 服務 （例如 Salesforce 和 Office 365） 和網際網路服務 （例如 Facebook 和 Twitter）。 使用[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和 [Azure 虛擬網路](../app-service-web/web-sites-integrate-with-vnet.md)存取內部部署資料。
* **安全性和法規遵循** - App Service 為 [ISO、SOC 和 PCI 相容](https://www.microsoft.com/TrustCenter/)。
* **應用程式範本**-從延伸 hello 中的範本清單中選擇[Azure Marketplace](https://azure.microsoft.com/marketplace/) ，可讓您使用精靈 tooinstall 熱門開放原始碼軟體，例如 WordPress、 Joomla 和 Drupal。
* **Visual Studio 整合**-Visual Studio 中的專用的工具簡化 hello 工作建立、 部署和偵錯。

## <a name="app-types-in-app-service"></a>App Service 中的應用程式類型
應用程式服務提供數個*應用程式類型*，每個都是預定的 toohost 特定的工作負載：

* [Web Apps](../app-service-web/app-service-web-overview.md) - 用於裝載網站和 Web 應用程式。
* [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) - 用於裝載行動應用程式後端。
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) - 用於裝載 RESTful API。
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) - 用於自動化商務程序和跨雲端整合系統和資料，而不需要撰寫程式碼。

hello word*應用程式*這裡是指 toohello 裝載資源專用的 toorunning 工作負載。 取得做為範例的 「 web 應用程式 」，您很可能是因為 hello 計算資源和應用程式程式碼一起傳遞功能 tooa 瀏覽器慣用 toothinking web 應用程式。 App Service 中，但*web 應用程式*為 hello Azure 提供裝載應用程式程式碼的計算資源。 

您的應用程式可能是由多個各種不同的 App Service 應用程式所組成。 例如，如果您的應用程式包含 Web 前端和RESTful API 後端，您可以︰

- 部署 （前端和應用程式開發介面） tooa 單一 web 應用程式  
- 部署 web 應用程式前端的程式碼 tooa 和 tooan API 應用程式後端程式碼。 



## <a name="app-service-plans"></a>App Service 方案
[應用程式服務計劃](azure-web-sites-web-hosting-plans-in-depth-overview.md)代表 hello 集合，其使用的實體資源 toohost 的應用程式。

App Service 方案可定義：

- **區域** (美國西部、美國東部等)
- **級別計數** (一、二、三個執行個體等)
- **執行個體大小** (小型、中型、大型)
- **SKU** (免費、共用、基本、標準、進階)

所有應用程式指派 tooan **App Service 方案**共用 hello 它允許您 toosave 成本裝載多個應用程式時所定義的資源。

您**App Service 方案**範圍，小從**免費**和**共用**Sku 太**基本**，**標準**，和**Premium** Sku 讓您存取 toomore 資源和沿著 hello 功能的方式。 一旦您 App Service 方案太設定**基本**或更高版本您也可以控制 hello**大小**和調整 hello Vm 的計數。

hello **SKU**和**標尺**的 hello 應用程式服務計劃可決定 hello 成本不 hello 數目及託管於該應用程式。 

如果您需要更多的延展性和網路隔離，則可在 [App Service 環境](../app-service-web/app-service-app-service-environment-intro.md)中執行應用程式。

## <a name="pricing"></a>定價
如需 App Service 費用的詳細資訊，請參閱 [App Service 價格](https://azure.microsoft.com/pricing/details/app-service/)。

## <a name="test-drive-app-service"></a>試驗 App Service
[建立範例 Web 應用程式、行動應用程式或邏輯應用程式](https://azure.microsoft.com/try/app-service/)，並試用一小時，無需信用卡，也無需簽定合約，一切都非常簡單。

或申請 [免費 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)，並試試我們的其中一個入門教學課程︰

* [教學課程︰建立 Web 應用程式](../app-service-web/app-service-web-get-started.md)
* [教學課程︰建立行動應用程式](../app-service-mobile/app-service-mobile-android-get-started.md)
* [教學課程︰建立 API 應用程式](../app-service-api/app-service-api-dotnet-get-started.md)
* [教學課程︰建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)

