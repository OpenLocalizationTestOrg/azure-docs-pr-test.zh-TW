---
title: "aaaManage Azure App Service 中的 web 應用程式"
description: "管理 Azure App Service 中的 web 應用程式的連結 tooresources。"
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>在 Azure App Service 中管理 Web 應用程式
本主題包含管理 web 應用程式中的連結 tooresources [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。 管理包含所有保留順暢執行您 web 應用程式的 hello 工作。 

Hello 存留期的 web 應用程式，您將執行不同的管理工作，當您移動從初始部署 toonormal 操作、 維護和更新。

許多 web 應用程式管理工作，可以在 hello Azure 入口網站中執行。

## <a name="before-you-deploy-your-web-app-tooproduction"></a>部署您的 web 應用程式 tooproduction 之前
### <a name="choose-a-tier"></a>選擇階層。
Azure App Service 提供了五種階層：免費、共用、基本、標準和高階。 Hello 功能和定價的每一層的相關資訊，請參閱[定價詳細資料](https://azure.microsoft.com/pricing/details/app-service/)。 

* [應用程式服務計劃](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)可以讓您將多個 web 應用程式在 hello 同一層。
* 建立 Web 應用程式之後，您可以隨時 [切換階層](web-sites-scale.md) 。

### <a name="configuration"></a>組態
使用 hello [Azure 入口網站](https://portal.azure.com/)tooset 各種組態選項。 如需詳細資料，請參閱 [在 Azure App Service 中設定 Web 應用程式](web-sites-configure.md)。 以下是簡短的檢查清單：

* 視需要選取 .NET、PHP、Java 或 Python 的 **執行階段版本** 。
* 啟用**WebSockets**如果您的 web 應用程式使用 hello WebSocket 通訊協定。 (這包括使用 [ASP.NET SignalR](http://www.asp.net/signalr) (英文) 或 [socket.io](web-sites-nodejs-chat-app-socketio.md) 的應用程式)。
* 您是否執行連續性的 Web 工作？ 如果是的話，請啟用 [Always On] 。
* 設定 hello**預設文件**，例如 index.html。

在加法 toothese 基本組態設定，您可能想 tooconfigure hello 下列：

* **安全通訊端層 (SSL)** 加密。 toouse SSL 的自訂網域名稱，您必須取得 SSL 憑證，並設定您的 web 應用程式 toouse 它。 請參閱 [針對 Azure App Service 中的 Web 應用程式啟用 HTTPS](app-service-web-tutorial-custom-ssl.md)。
* **自訂網域名稱。** 您的 Web 應用程式會自動取得 azurewebsites.net 下的子網域。 您可以使其與自訂網域名稱 (如 contoso.com) 相關聯。請參閱 [在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md)。

語言特有組態：

* **PHP**： [在 Azure App Service Web Apps 中設定 PHP](web-sites-php-configure.md)。
* **Python**： [使用 Azure App Service Web Apps 設定 Python](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>當 Web 應用程式執行時
執行您 web 應用程式時，您會想 toomake 確定可用，但它縮放 toomeet 使用者流量。 您可能也需要 tootroubleshoot 錯誤。

### <a name="monitoring"></a>監視
* 您可以透過 hello Azure 入口網站，[新增效能度量](web-sites-monitor.md)CPU 使用狀況等用戶端要求數量。
* [調整您的 web 應用程式](web-sites-scale.md)回應 tootraffic 中。 根據您的層，您可以調整 Vm 的 hello 數目及/或 hello hello VM 執行個體大小。 在 hello Standard 和 Premium 層，您也可以設定自動調整，讓您 web 應用程式在固定排程，或在回應 tooload 自動縮放。  

### <a name="backups"></a>備份
* 設定 Web 應用程式的 [自動備份](web-sites-backup.md) 。 透過 [本視訊](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/)深入了解備份。
* 了解如何 hello 方式[資料庫復原](../sql-database/sql-database-business-continuity.md)Azure SQL Database 中。

### <a name="troubleshooting"></a>疑難排解
* 如果發生錯誤，您可以[Visual Studio 中疑難排解](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)、 使用 診斷記錄檔，以及即時偵錯 hello 雲端中。 
* 外部 Visual Studio 中，有各種方式 toocollect 診斷記錄檔。 請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)。
* Node.js 應用程式，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。

### <a name="restoring-data"></a>還原資料
* [還原](web-sites-restore.md) 先前已備份的 Web 應用程式。

## <a name="when-you-update-your-web-app"></a>更新 Web 應用程式時
如果您尚未啟用自動備份，可以建立 [手動備份](web-sites-backup.md)。

請考慮使用 [預備部署](web-sites-staged-publishing.md)。 此選項可讓您發行更新 tooa 預備環境部署執行的並行與生產環境部署。 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


