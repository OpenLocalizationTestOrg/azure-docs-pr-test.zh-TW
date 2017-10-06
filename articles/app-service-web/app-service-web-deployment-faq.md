---
title: "Azure web 應用程式的 aaaDeployment 常見問題集 |Microsoft 文件"
description: "收到 hello Web 應用程式功能的部署 Azure 應用程式服務的相關常見問題的解答 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Azure 中 Web 應用程式的部署常見問題集

這篇文章有解答 toofrequently 集 (Faq) 部署問題的相關 hello [Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>我剛開始使用 App Service Web 應用程式。 如何發佈程式碼？

以下是發佈 Web 應用程式程式碼的一些選項：

*   使用 Visual Studio 進行部署。 如果您有 hello Visual Studio 方案，hello web 應用程式專案，以滑鼠右鍵按一下，然後選取**發行**。
*   使用 FTP 用戶端進行部署。 在 hello Azure 入口網站，下載 hello 發行 hello web 應用程式設定檔的 toodeploy 您的程式碼。 然後上, 傳 hello 檔案 too\site\wwwroot 使用 hello 相同發行設定檔 FTP 認證。

如需詳細資訊，請參閱[部署您的應用程式 tooApp 服務](web-sites-deploy.md)。

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>當我嘗試從 Visual Studio toodeploy，我看到一則錯誤訊息。 如何解決這個問題？

如果您看到下列訊息的 hello，您可能使用較舊版本的 hello SDK: 「 資源群組 'YourResourceGroup' 中的資源 'YourResourceName' 的部署期間發生錯誤： MissingRegistrationForLocation: hello 訂用帳戶未註冊hello 資源類型 '組件' hello 位置 ' Central US '。 請重新註冊此提供者順序 toohave 存取 toothis 位置中。 」 

tooresolve 這個錯誤，升級 toohello[最新的 SDK](https://azure.microsoft.com/downloads/)。 如果您看到此訊息，而且您擁有 hello 最新的 SDK，請提交支援要求。

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>我要如何部署 ASP.NET 應用程式從 Visual Studio tooApp 服務？
<a id="deployasp"></a>

hello 教學課程[在 Azure 中建立第一個 ASP.NET web 應用程式在五分鐘](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/)顯示 toodeploy ASP.NET web 應用程式 tooa web 應用程式，App Service 中的使用 Visual Studio 2015。

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Hello 不同認證類型的部署有哪些？

App Service 支援兩種認證類型，用於本機 Git 部署和 FTP/S 部署。 如需有關如何 tooconfigure 部署認證，請參閱[設定應用程式服務的部署認證](app-service-deployment-credentials.md)。

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>什麼是我的 App Service web 應用程式的 hello 檔案或目錄結構？

Hello 檔案結構，您的 App Service 應用程式的相關資訊，請參閱[檔案在 Azure 中的結構](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)。

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>如何解決 「 FTP 錯誤 550-沒有不 hello 磁碟上的空間不足 」 當我嘗試 tooFTP 我的檔案？

如果您看到此訊息，可能是您正在執行到的磁碟配額 hello 服務計劃中的 web 應用程式。 您可能需要 tooscale 向上 tooa 根據自己的磁碟空間需求較高服務層。 如需定價方案和資源限制的詳細資訊，請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>如何為 App Service Web 應用程式設定持續部署？

您可以從數個資源設定持續部署，包括 Visual Studio Team Services、OneDrive、GitHub、Bitbucket、Dropbox 和其他 Git 存放庫。 可以在 hello 入口網站中使用這些選項。 [連續部署 tooApp 服務](app-service-continuous-deployment.md)是很有幫助的教學課程說明如何 tooset 連續部署。

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>如何針對從 GitHub 和 Bitbucket 持續部署的問題進行疑難排解？

如需調查從 GitHub 或 Bitbucket 持續部署之問題的協助，請參閱[調查持續部署](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)。

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>我無法 FTP toomy 站台和發佈我的程式碼。 如何解決這個問題？

tooresolve FTP 問題：

1. 請確認您輸入 hello 正確的主機名稱和認證。 如需有關不同認證類型的詳細資訊和如何 toouse 它們，請參閱[部署認證](https://github.com/projectkudu/kudu/wiki/Deployment-credentials)。
2. 請確認防火牆不會封鎖 hello FTP 連接埠。 hello 埠都應該具有這些設定：
    * FTP 控制連線連接埠︰21
    * FTP 資料連線連接埠︰989、10001-10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>如何將我的程式碼 tooApp 服務的發行？

hello Azure 快速入門是設計的 toohelp 您部署應用程式使用 hello 部署堆疊和您選擇的方法。 hello Azure 入口網站中的 toouse hello 快速入門，跳過**設定** > **應用程式部署**。

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>為什麼沒有我的應用程式有時後重新啟動部署 tooApp 服務？

toolearn 有關 hello 情況下，應用程式部署可能會導致重新啟動，請參閱[部署與執行階段問題](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts")。 如 hello 文章所述，應用程式服務會將部署檔案 toohello wwwroot 資料夾。 它永遠不會直接重新啟動您的應用程式。

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>如何整合 Visual Studio Team Services 程式碼與 App Service？

您有兩個選項可以使用 Visual Studio Team Services 進行持續部署：

*   使用 Git 專案。 Hello 部署選項使用該儲存機制連接透過應用程式服務。
*   使用 Team Foundation 版本控制 (TFVC) 專案。 使用應用程式服務的 hello 組建代理程式部署。

這兩個選項的持續程式碼部署取決於現有的開發人員工作流程和簽入程序。 如需詳細資訊，請參閱這些文章： 

*   [實作您的應用程式 tooan Azure 網站的連續部署](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [設定 Visual Studio Team Services 帳戶，讓它可以部署 tooa web 應用程式](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>如何使用 FTP 或 FTPS toodeploy 我的應用程式 tooApp 服務？

如需使用 FTP 或 FTPS toodeploy 您 web 應用程式 tooApp 服務，請參閱[使用 FTP/S 部署您的應用程式 tooApp 服務](app-service-deploy-ftp.md)。
