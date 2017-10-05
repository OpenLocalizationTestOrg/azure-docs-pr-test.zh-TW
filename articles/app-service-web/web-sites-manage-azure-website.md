---
title: "在 Azure App Service 中管理 Web 應用程式"
description: "適用於在 Azure App Service 中管理 Web 應用程式之資源的連結。"
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>在 Azure App Service 中管理 Web 應用程式
本主題含有適合用來在 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中管理 Web 應用程式之資源的連結。 所謂的管理包括所有維持 Web 應用程式順暢運作的工作。 

在 Web 應用程式的生命週期內，從初始部署到正常運作、維護及更新，都需要執行不同的管理工作。

您可以在 Azure 入口網站中執行許多 Web 應用程式管理工作。

## <a name="before-you-deploy-your-web-app-to-production"></a>將 Web 應用程式部署到生產環境之前
### <a name="choose-a-tier"></a>選擇階層。
Azure App Service 提供了五種階層：免費、共用、基本、標準和高階。 如需各階層之功能和定價的相關資訊，請參閱 [網站定價詳細資料](https://azure.microsoft.com/pricing/details/app-service/)。 

* [應用程式服務方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 可讓您將多個 Web 應用程式分組在同一個階層下。
* 建立 Web 應用程式之後，您可以隨時 [切換階層](web-sites-scale.md) 。

### <a name="configuration"></a>組態
使用 [Azure 入口網站](https://portal.azure.com/) 來設定各種組態選項。 如需詳細資料，請參閱 [在 Azure App Service 中設定 Web 應用程式](web-sites-configure.md)。 以下是簡短的檢查清單：

* 視需要選取 .NET、PHP、Java 或 Python 的 **執行階段版本** 。
* 如果您的 Web 應用程式使用 WebSocket 通訊協定，請啟用 **WebSockets** 。 (這包括使用 [ASP.NET SignalR](http://www.asp.net/signalr) (英文) 或 [socket.io](web-sites-nodejs-chat-app-socketio.md) 的應用程式)。
* 您是否執行連續性的 Web 工作？ 如果是的話，請啟用 [Always On] 。
* 設定 **預設文件**(如 index.html)。

除了以上基本組態設定之外，您也許還想要設定以下各項：

* **安全通訊端層 (SSL)** 加密。 若要使用 SSL 搭配自訂網域名稱，您必須取得 SSL 憑證並設定 Web 應用程式來加以使用。 請參閱 [針對 Azure App Service 中的 Web 應用程式啟用 HTTPS](app-service-web-tutorial-custom-ssl.md)。
* **自訂網域名稱。** 您的 Web 應用程式會自動取得 azurewebsites.net 下的子網域。 您可以使其與自訂網域名稱 (如 contoso.com) 相關聯。 請參閱 [在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。

語言特有組態：

* **PHP**： [在 Azure App Service Web Apps 中設定 PHP](web-sites-php-configure.md)。
* **Python**： [使用 Azure App Service Web Apps 設定 Python](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>當 Web 應用程式執行時
當 Web 應用程式執行時，您會想要確認 Web 應用程式是否可供使用，以及是否能根據使用者流量而調整。 您可能也需要疑難排解錯誤。

### <a name="monitoring"></a>監視
* 您可以透過 Azure 入口網站來 [新增效能度量](web-sites-monitor.md) (如 CPU 使用率和用戶端要求數目)。
* [調整 Web 應用程式](web-sites-scale.md) 以因應流量變化。 您可以根據階層來調整 VM 的數目和/或 VM 執行個體的大小。 在標準和高階階層中，您還可以設定自動調整，使 Web 應用程式得以按照固定排程或根據負載自動調整。  

### <a name="backups"></a>備份
* 設定 Web 應用程式的 [自動備份](web-sites-backup.md) 。 透過 [本視訊](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)深入了解備份。
* 深入了解 Azure SQL Database 中的 [資料庫復原](../sql-database/sql-database-business-continuity.md) 選項。

### <a name="troubleshooting"></a>疑難排解
* 發生問題時，您可以在雲端使用診斷記錄和即時偵錯，以 [在 Visual Studio 中疑難排解 Azure 網站](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)。 
* 在 Visual Studio 之外，還有各種方法可用來收集診斷記錄。 請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)。
* 若是 Node.js 應用程式，請參閱 [如何在 Azure App Service 中偵錯 Node.js Web 應用程式](web-sites-nodejs-debug.md)。

### <a name="restoring-data"></a>還原資料
* [還原](web-sites-restore.md) 先前已備份的 Web 應用程式。

## <a name="when-you-update-your-web-app"></a>更新 Web 應用程式時
如果您尚未啟用自動備份，可以建立 [手動備份](web-sites-backup.md)。

請考慮使用 [預備部署](web-sites-staged-publishing.md)。 此選項可讓您將更新發佈到與生產部署並行運作的預備部署。 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


