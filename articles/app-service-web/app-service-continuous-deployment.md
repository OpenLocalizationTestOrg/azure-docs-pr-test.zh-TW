---
title: "aaaContinuous 部署 tooAzure 應用程式服務 |Microsoft 文件"
description: "深入了解如何 tooenable 連續部署 tooAzure 應用程式服務。"
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
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>連續部署 tooAzure 應用程式服務
本教學課程示範如何 tooconfigure 連續部署工作流程的程式[Azure App Service]應用程式。 GitHub、 BitBucket 應用程式服務整合和[Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/)啟用連續部署，Azure 會提取 hello 最新的更新從您的專案中的工作流程發行 tooone 這些服務。 持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。

toofind 出 tooconfigure 連續部署，以手動方式從雲端儲存機制不列出 hello Azure 入口網站的方式 (例如[GitLab](https://gitlab.com/))，請參閱[設定連續部署使用手動操作步驟](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)。

## <a name="overview"></a>啟用持續部署
tooenable 連續部署

1. 發行您的應用程式內容 toohello 儲存機制，用於連續部署。  
    如需有關發行您的專案 toothese 服務的詳細資訊，請參閱[建立的儲存機制 (GitHub)]，[建立的儲存機制 (BitBucket)]，和[開始使用 VSTS]。
2. 在您的應用程式功能表] 刀鋒視窗中 hello [Azure 入口網站]，按一下 [**應用程式部署 > 部署選項**。 按一下**選擇來源**，然後選取 hello 部署來源。  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure App Service 部署的 VSTS 帳戶，請參閱這[教學課程](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)。
   > 
   > 
3. 完成 hello 授權工作流程。
4. 在 hello**部署來源**刀鋒視窗中，選擇 hello 專案，以及建立分支 toodeploy 從。 完成後，按一下 [ **確定**]。
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > 啟用搭配 GitHub 或 BitBucket 的持續部署時，將會同時顯示公用和私人專案。
   > 
   > 
   
    應用程式服務建立關聯性與 hello 選取儲存機制、 提取中從指定的分支，hello hello 檔案以及維護您 App Service 應用程式的儲存機制的複製品。 當您設定來自 hello Azure 入口網站的 VSTS 連續部署時，hello 的整合會使用應用程式服務的 hello [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)，已自動建置和部署的工作，與每個`git push`。 您不需要 tooseparately 設定於 VSTS 中的連續部署。 完成此程序，hello 之後**部署選項**應用程式 刀鋒視窗會顯示作用中的部署，表示部署成功。
5. 已成功部署 tooverify hello 應用程式中，按一下 hello **URL**在 hello hello Azure 入口網站中的 hello 應用程式 刀鋒視窗最上方。
6. 從您選擇的 hello 儲存機制進行持續部署 tooverify 推送變更 toohello 儲存機制。 您的應用程式應該更新 tooreflect hello 變更，很快就完成 hello 發送 toohello 儲存機制。 您可以確認它已在 hello hello 更新提取**部署選項**刀鋒視窗中的應用程式。

## <a name="VSsolution"></a>Visual Studio 方案的持續部署
推入 Visual Studio 方案 tooAzure App Service 是推送簡單 index.html 檔案一樣簡單。 hello App Service 部署程序來簡化所有 hello 詳細資料，包括還原 NuGet 相依性和建置 hello 應用程式二進位檔。 您可以遵循的維護程式碼只能在您的 Git 儲存機制中的 hello 來源控制最佳作法，並讓負責 hello rest 應用程式服務部署。

hello 步驟推送服務是您 Visual Studio 方案 tooApp hello 相同如同 hello[上一節](#overview)，前提是您設定您的解決方案和儲存機制，如下所示：

* 使用 hello Visual Studio 原始檔控制選項 toogenerate`.gitignore`例如 hello 圖檔，或手動新增`.gitignore`檔案中儲存機制根目錄中，以內容類似 toothis [.gitignore 範例](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)。
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* 加入 hello 整個方案的目錄樹狀結構 tooyour 儲存機制，與 hello 儲存機制的根目錄中的 hello.sln 檔案。

一旦您設定您的儲存機制，如所述，並在 Azure 中設定您的應用程式的其中一個 hello 線上 Git 儲存機制持續發行，您可以開發您的 ASP.NET 應用程式，Visual Studio 中的本機及持續只是藉由部署您的程式碼推送變更 tooyour 線上 Git 儲存機制。

## <a name="disableCD"></a>停用連續部署
toodisable 連續部署

1. 在您的應用程式功能表] 刀鋒視窗中 hello [Azure 入口網站]，按一下 [**應用程式部署 > 部署選項**。 然後按一下 **中斷連線**在 hello**部署選項**刀鋒視窗。
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. 之後回答**是**toohello 確認訊息中，您可以傳回 tooyour 應用程式 刀鋒視窗，然後按一下**應用程式部署 > 部署選項**如果您想要 tooset 發行從其他來源。

## <a name="additional-resources"></a>其他資源
* [如何 tooinvestigate 常見問題與連續部署](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [如何 toouse PowerShell for Azure]
* [如何 toouse hello 用於 Mac 和 Linux 的 Azure 命令列工具]
* [Git 文件]
* [專案 Kudu](https://github.com/projectkudu/kudu/wiki)
* [使用 Azure tooautomatically 產生 CI/CD 管線 toodeploy ASP.NET 4 應用程式](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure 入口網站]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[如何 toouse PowerShell for Azure]: /powershell/azureps-cmdlets-docs
[如何 toouse hello 用於 Mac 和 Linux 的 Azure 命令列工具]:../cli-install-nodejs.md
[Git 文件]: http://git-scm.com/documentation

[建立的儲存機制 (GitHub)]: https://help.github.com/articles/create-a-repo
[建立的儲存機制 (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[開始使用 VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
