---
title: "持續部署至 Azure App Service | Microsoft Docs"
description: "了解如何啟用持續部署至 Azure App Service。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: ef5924607868bcb3dc35e279539b78d5a0e17c1a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a>持續部署至 Azure App Service
本教學課程將示範如何為您的 [Azure Web Apps](app-service-web-overview.md) 應用程式設定連續部署工作流程。 App Service 與 BitBucket、GitHub 及 [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) 整合，可啟用持續部署工作流程，其中 Azure 會從您已發佈至這其中一個服務的專案中提取最新更新。 持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。

若要了解如何從 Azure 入口網站未列出的雲端存放庫中手動設定連續部署 (例如 [GitLab](https://gitlab.com/))，請參閱[使用手動步驟設定連續部署](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。

## <a name="overview"></a>啟用持續部署
若要啟用持續部署，

1. 將您的應用程式內容發佈至將用於持續部署的儲存機制。  
    如需將專案發佈至這些服務的詳細資訊，請參閱[建立儲存機制 (GitHub)]、[建立儲存機制 (BitBucket)]及[開始使用 VSTS]。
2. 在 [Azure 入口網站]中您應用程式的功能表刀鋒視窗中，按一下 [應用程式部署] > [部署選項]。 按一下 [選擇來源]，然後選取部署來源。  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > 若要設定適用於 App Service 部署的 VSTS 帳戶，請參閱這個 [教學課程](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)。
   > 
   > 
3. 完成授權工作流程。
4. 在 [部署來源] 刀鋒視窗中，選擇專案以及要從中部署的分支。 完成後，按一下 [ **確定**]。
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > 啟用搭配 GitHub 或 BitBucket 的持續部署時，將會同時顯示公用和私人專案。
   > 
   > 
   
    App Service 會建立與所選儲存機制的關聯、從指定的分支提取檔案，並維護適用於 App Service 應用程式的儲存機制複本。 從 Azure 入口網站設定 VSTS 持續部署時，整合會使用 App Service [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)，它已經利用每個 `git push` 自動建置和部署工作。 您不需要在 VSTS 中分別設定持續部署。 此程序完成之後，應用程式刀鋒視窗的 [部署選項] 應用程式刀鋒視窗將會顯示作用中的部署，表示部署成功。
5. 若要確認已成功部署應用程式，請按一下 Azure 入口網站中應用程式刀鋒視窗頂端的 [URL]。
6. 若要確認從您選擇的儲存機制進行連續部署，將變更推送至儲存機制。 在推送至儲存機制完成後不久，您的應用程式應該會更新以反映變更。 您可以在應用程式的 [部署選項] 刀鋒視窗上確認它是否已提取更新。

## <a name="VSsolution"></a>Visual Studio 方案的持續部署
將 Visual Studio 方案推送至 Azure App Service，就像推送簡單的 index.html 檔案一樣容易。 App Service 部署程序會簡化所有細節，包含還原 NuGet 相依性，以及建置應用程式二進位檔。 您可以只在 Git 儲存機制中遵循維護程式碼的原始檔控制最佳做法，然後讓 App Service 部署負責執行剩餘的部分。

將您的 Visual Studio 方案推送至 App Service 的步驟和 [上一節](#overview)的一樣，可提供您設定方案和儲存機制的步驟，如下：

* 使用 Visual Studio 原始檔控制選項來產生 `.gitignore` 檔案 (如下圖所示)，或使用類似這個 [.gitignore 範例](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)的內容，在您的儲存機制根目錄中手動新增 `.gitignore` 檔案。
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* 使用儲存機制根目錄中的 .sln 檔案，將整個解決方案的目錄樹狀結構新增至您的儲存機制。

一旦您設定儲存機制 (如前所述) 並在 Azure 中設定應用程式，以便從其中一個線上 Git 儲存機制持續發佈之後，就能夠在 Visual Studio 中本機開發 ASP.NET 應用程式，並且只需將變更推送至線上 Git 儲存機制，就能持續部署您的程式碼。

## <a name="disableCD"></a>停用連續部署
若要停用持續部署，

1. 在 [Azure 入口網站]中您應用程式的功能表刀鋒視窗中，按一下 [應用程式部署] > [部署選項]。 然後按一下 [部署選項] 刀鋒視窗中的 [中斷連線]。
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. 在確認訊息中回答 [是] 之後，如果您要設定從其他來源發佈，您可以返回應用程式的刀鋒視窗，然後按一下 [應用程式部署] > [部署選項]。

## <a name="additional-resources"></a>其他資源
* [如何調查連續部署的常見問題](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [如何使用適用於 Azure 的 PowerShell]
* [如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]
* [Git 文件]
* [專案 Kudu](https://github.com/projectkudu/kudu/wiki)
* [使用 Azure 自動產生 CI/CD 管線，以部署 ASP.NET 4 應用程式](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；沒有承諾。
> 
> 

[Azure 入口網站]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[如何使用適用於 Azure 的 PowerShell]: /powershell/azureps-cmdlets-docs
[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]:../cli-install-nodejs.md
[Git 文件]: http://git-scm.com/documentation

[建立儲存機制 (GitHub)]: https://help.github.com/articles/create-a-repo
[建立儲存機制 (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[開始使用 VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
