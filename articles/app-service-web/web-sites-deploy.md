---
title: "aaaDeploy 您應用程式服務的應用程式 tooAzure |Microsoft 文件"
description: "深入了解如何 toodeploy 您應用程式 tooAzure 應用程式服務。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>部署您的應用程式 tooAzure 應用程式服務
這篇文章可協助您判斷 hello 最佳選項 toodeploy hello 檔案給 web 應用程式、 行動裝置應用程式後端或應用程式開發介面應用程式太[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，並接著會引導您指示特定 tooyour tooappropriate 資源慣用的選項。

## <a name="overview"></a>Azure App Service 部署概觀
Azure App Service 自動維護的 （ASP.NET、 PHP、 Node.js 等等） 的 hello 應用程式架構。 有些架構像 Java 和 Python 時，預設會啟用，可能就需要簡單的核取記號組態 tooenable 它。 此外，您可以自訂您的應用程式架構，例如 hello PHP 版本或 hello 位元版本的程式執行階段。 如需詳細資訊，請參閱 [在 Azure App Service 中設定您的應用程式](web-sites-configure.md)。

您還沒有 tooworry 有關 hello web 伺服器或應用程式架構，因為部署您的應用程式 tooApp 服務是要部署您的程式碼、 二進位檔、 內容檔案和其各自的目錄結構，toohello [   **/站台/wwwroot**目錄](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)在 Azure 中 (或 hello **/站台/wwwroot/App_Data/工作/** WebJobs 目錄)。 App Service 支援三種不同的部署程序。 這篇文章中的所有 hello 部署方法可都使用其中一種 hello 下列處理程序： 

* [FTP 或 FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol)： 使用您喜愛的 FTP 或 FTPS 工具 toomove 您檔案 tooAzure，從啟用[FileZilla](https://filezilla-project.org) toofull 精選 Ide 喜歡[NetBeans](https://netbeans.org)。 這完全是檔案上傳程序。 App Service 不會提供其他服務，例如版本控制、檔案結構管理等等。 
* [Kudu （Git/Mercurial 或 OneDrive/Dropbox）](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu 為 hello[部署引擎](https://github.com/projectkudu/kudu/wiki)App Service 中。 將您的程式碼 tooKudu 推送直接從任何儲存機制。 Kudu 也提供新增的服務，每當程式碼 tooit，包括版本控制，封裝還原，MSBuild，和[web 攔截](https://github.com/projectkudu/kudu/wiki/Web-hooks)連續部署和其他自動化工作。 hello Kudu 部署引擎支援 3 種不同部署來源：   
  
  * OneDrive 和 Dropbox 的內容同步處理   
  * 以儲存機制為基礎的持續部署，其使用 GitHub、Bitbucket 和 Visual Studio Team Services 的自動同步處理  
  * 以儲存機制為基礎的部署，其使用本機 Git 手動同步處理  
* [Web 部署](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy)： 部署程式碼 tooApp 服務直接從您喜愛的 Microsoft 工具，例如 Visual Studio 使用 hello 自動化部署 tooIIS 伺服器的相同工具。 這項工具支援僅限差異比對的部署、資料庫建立、連接字串等的轉換等等。Web Deploy 與 Kudu 的二進位檔之前，所建立的應用程式部署 tooAzure。 類似 tooFTP，應用程式服務不提供任何其他服務。

熱門的 Web 開發工具支援一或多個這些部署程序。 Hello 您選擇的工具判斷 hello 部署程序時您可以利用、 hello 實際達成的 DevOps 功能取決於 hello 組合 hello 部署程序和 hello 特定工具您選擇。 例如，如果您從 [Visual Studio 搭配 Azure SDK](#vspros)執行 Web Deploy，即使您未從 Kudu 獲得自動化，仍可在 Visual Studio 中獲得套件還原和 MSBuild 自動化。 

> [!NOTE]
> 這些部署處理程序實際上不[佈建 hello Azure 資源](../azure-resource-manager/resource-group-template-deploy-portal.md)可能需要您的應用程式。 不過，大部分的 hello 連結如何 tooarticles 示範 tooprovision hello 應用程式和部署您的程式碼 tooit 端對端的方式。 您也可以尋找佈建在 hello Azure 資源的其他選項[使用命令列工具來自動化部署](#automate)> 一節。
> 
> 

## <a name="ftp"></a>透過 FTP 上傳檔案來手動部署
如果您是使用的 toomanually 複製您的網頁內容 tooa web 伺服器時，您可以使用[FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)公用程式 toocopy 檔案，例如 Windows 檔案總管或[FileZilla](https://filezilla-project.org/)。

hello 專業人員的手動複製檔案︰

* FTP 工具易於上手且複雜性最小。 
* 可明確掌握檔案的走向。
* FTPS 的高安全性。

手動複製檔案的 hello 缺點如下：

* 具有 tooknow toodeploy 如何在 App Service 中檔案 toohello 正確的目錄。 
* 當發生失敗時沒有回復的版本控制。
* 沒有內建的部署歷程記錄可針對部署問題進行疑難排解。
* 可能很長的部署時間許多 FTP 工具不提供差異比對僅限複製，因此直接複製 hello 的所有檔案。  

### <a name="howtoftp"></a>Tooupload 如何透過 FTP 檔案
hello [Azure 入口網站](https://portal.azure.com)提供您所有的 hello 資訊，您需要使用 FTP 或 FTPS tooconnect tooyour 應用程式的目錄。

* [部署您的應用程式 tooAzure 應用程式服務使用 FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>與雲端資料夾同步處理以進行部署
理想的替代方法太[手動複製檔案](#ftp)同步的檔案和資料夾 tooApp 服務從雲端儲存體服務，例如 OneDrive 和 Dropbox。 正在雲端資料夾與同步處理會利用部署的 hello Kudu 程序 (請參閱[部署程序的概觀](#overview))。

hello 專業人員的同步處理與雲端資料夾是：

* 部署的簡潔性。 部分服務 (例如 OneDrive 和 Dropbox) 提供桌面同步處理用戶端，使您的本機工作目錄也是部署目錄。
* 單鍵部署。
* Hello Kudu 部署引擎中的所有功能 （例如封裝還原，自動化）。

與雲端資料夾同步處理 hello 優缺點如下：

* 當發生失敗時沒有回復的版本控制。
* 沒有自動化的部署，需要手動同步處理。

### <a name="howtodropbox"></a>如何 toodeploy 由雲端資料夾與同步處理
在 hello [Azure 入口網站](https://portal.azure.com)，您可以在 OneDrive 或 Dropbox 雲端儲存體中指定的資料夾內容的同步處理、 工作與您的應用程式程式碼中該資料夾中，內容和同步 tooApp 服務以 hello 按一下按鈕。

* [同步處理內容，從雲端資料夾 tooAzure App Service](app-service-deploy-content-sync.md)。 

## <a name="continuousdeployment"></a>從雲端型原始檔控制服務進行持續部署
如果您的開發小組會使用這類程式碼以雲端為基礎的來源管理 (SCM) 服務[Visual Studio Team Services](http://www.visualstudio.com/)， [GitHub](https://www.github.com)，或[BitBucket](https://bitbucket.org/)，您可以設定應用程式服務 toointegrate 與您的儲存機制，並持續部署。 

會從雲端架構的原始檔控制服務部署的 hello 專業人員：

* 版本控制 tooenable 復原。
* 能力 tooconfigure 連續部署 git （和 Mercurial 適用的話） 儲存機制。 
* 分公司特定部署中，可以部署不同的分支 toodifferent[插槽](web-sites-staged-publishing.md)。
* Hello Kudu 部署引擎中的所有功能 （例如部署版本控制、 復原、 封裝還原，自動化）。

從雲端架構的原始檔控制服務部署的 hello con 是：

* Hello 個別 SCM 所需要的服務的一些知識。

### <a name="vsts"></a>Toodeploy 持續從雲端架構的原始檔控制服務的方式
在 hello [Azure 入口網站](https://portal.azure.com)，您可以設定從 GitHub、 Bitbucket 和 Visual Studio Team Services 的連續部署。

* [連續部署 tooAzure App Service](app-service-continuous-deployment.md)。 

toofind 出 tooconfigure 連續部署，以手動方式從雲端儲存機制不列出 hello Azure 入口網站的方式 (例如[GitLab](https://gitlab.com/))，請參閱[設定連續部署使用手動操作步驟](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。

## <a name="localgitdeployment"></a>從本機 Git 進行部署
如果您的開發小組會使用根據 Git 在內部部署本機來源的程式碼管理 (SCM) 服務，您可以設定此服務的部署來源 tooApp 為。 

從本機 Git 進行部署的優點如下：

* 版本控制 tooenable 復原。
* 分公司特定部署中，可以部署不同的分支 toodifferent[插槽](web-sites-staged-publishing.md)。
* Hello Kudu 部署引擎中的所有功能 （例如部署版本控制、 復原、 封裝還原，自動化）。

從本機 Git 進行部署的缺點如下：

* Hello 需要個別 SCM 系統的一些知識。
* 沒有任何持續部署的現成解決方案。 

### <a name="vsts"></a>如何從本機 Git toodeploy
在 hello [Azure 入口網站](https://portal.azure.com)，您可以設定本機 Git 部署。

* [本機 Git 部署 tooAzure App Service](app-service-deploy-local-git.md)。 
* [發佈 tooWeb 應用程式從任何 git/hg 位儲存機制](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html)。  

## <a name="deploy-using-an-ide"></a>使用整合式開發環境 (IDE) 部署
如果您已經在使用[Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)與[Azure SDK](https://azure.microsoft.com/downloads/)，或其他 IDE 套件 like [Xcode](https://developer.apple.com/xcode/)， [Eclipse](https://www.eclipse.org)，和[IntelliJ 概念](https://www.jetbrains.com/idea/)，您可以部署 tooAzure 直接從您的 IDE 中。 此選項適用於個別的開發人員。

Visual Studio 支援所有三種部署處理程序 （FTP、 Git、 和 Web Deploy），根據您的喜好設定，而如果有 FTP 或 Git 整合其他 Ide 可以部署 tooApp 服務 (請參閱[部署程序的概觀](#overview))。

hello 專業人員的部署使用的 IDE 是：

* 可能會最小化工具來您端對端應用程式生命週期的 hello。 開發、 偵錯、 追蹤和部署應用程式 tooAzure 而不需移動您的 IDE 之外。 

部署使用的 IDE 的 hello 缺點如下：

* 工具的複雜度增加。
* 仍然需要團隊專案的原始檔控制系統。

<a name="vspros"></a> 使用 Visual Studio 搭配 Azure SDK 進行部署的其他優點包括：

* Azure SDK 會優先使用 Visual Studio 中的 Azure 資源。 建立、 刪除、 編輯、 啟動及停止應用程式、 查詢 hello 後端 SQL 資料庫、 即時偵錯 hello Azure 應用程式，以及執行更多。 
* 即時編輯在 Azure 上的程式碼檔案。
* 即時偵錯在 Azure 上的應用程式。
* 整合式 Azure Explorer。
* 僅限差異比對的部署。 

### <a name="vs"></a>如何直接從 Visual Studio toodeploy
* [開始使用 Azure 和 ASP.NET](app-service-web-get-started-dotnet.md)。 如何 toocreate 和使用 Visual Studio 和 Web Deploy 來部署簡單的 ASP.NET MVC web 專案。
* [如何使用 Visual Studio 的 Azure WebJobs tooDeploy](websites-dotnet-deploy-webjobs.md)。 如何 tooconfigure 主控台應用程式的專案，讓它們為 WebJobs。  
* [使用 Visual Studio 的 ASP.NET Web 部署](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction)。 12 一部分教學課程的系列，它涵蓋了比其他 hello 這份清單中的部署工作更完整範圍。 因為 hello 教學課程所撰寫，但稍後新增附註說明何謂遺漏已加入一些 Azure 部署功能。
* [直接部署從 Git 儲存機制的 Visual Studio 2012 中的 ASP.NET 網站 tooAzure](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881)。 說明如何 toodeploy ASP.NET web 專案在 Visual Studio 中，使用 hello Git 外掛程式 toocommit hello 程式碼 tooGit 並連接 Azure toohello Git 儲存機制。 自 Visual Studio 2013 起，Git 支援已是內建的功能，不需安裝外掛程式。

### <a name="aztk"></a>如何使用 toodeploy hello Azure 工具套件 Eclipse 和 IntelliJ 概念
Microsoft 對於它可能 toodeploy Web 應用程式 tooAzure，直接從 Eclipse 和 IntelliJ 透過 hello [Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse.md)和[Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md)。 hello 下列教學課程說明部署簡單"Hello"世界 Web 應用程式 tooAzure 使用任一 IDE 所涉及的 hello 步驟：

* [Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)](app-service-web-eclipse-create-hello-world-web-app.md)。 本教學課程會示範 toouse hello Azure Toolkit for Eclipse toocreate 和部署 Azure Hello World 網頁應用程式的方式。
* [在 IntelliJ 中建立 Azure Hello World Web 應用程式](app-service-web-intellij-create-hello-world-web-app.md)。 本教學課程會示範 toouse hello Azure Toolkit for IntelliJ toocreate 和部署 Azure Hello World 網頁應用程式的方式。

## <a name="automate"></a>使用命令列工具進行自動化部署
如果您想做選擇的 hello 開發環境的 hello 命令列的終端機，您可以使用命令列工具的應用程式服務應用程式編寫部署工作。 

使用命令列工具進行部署的優點如下：

* 啟用指令碼式部署案例。
* 整合 Azure 資源與程式碼部署的佈建。
* 將 Azure 部署整合至現有的連續整合指令碼。

使用命令列工具進行部署的缺點如下：

* 不適用於偏好 GUI 的開發人員。

### <a name="automatehow"></a>如何使用命令列工具的 tooautomate 部署

請參閱[自動化部署您的 Azure 應用程式的命令列工具](app-service-deploy-command-line.md)命令列工具和連結 tootutorials 的清單。 

## <a name="nextsteps"></a>後續步驟
在某些情況下，您可能想 toobe 無法 tooeasily 來回之間切換的臨時區域與您的應用程式的實際執行版本。 [如需詳細資訊，請參閱 Web Apps 上的預備部署](web-sites-staged-publishing.md)。

具有備份及還原計劃是部署工作流程中相當重要的環節。 Hello 應用程式服務備份和還原功能的相關資訊，請參閱[Web 應用程式備份](web-sites-backup.md)。  

如需如何 toouse Azure 角色型存取控制 toomanage 存取 tooApp 服務部署資訊，請參閱[RBAC 和 Web 應用程式發佈](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/)。

