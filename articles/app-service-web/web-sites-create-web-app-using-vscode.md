---
title: "aaaCreate Visual Studio 程式碼中的 ASP.NET Core web 應用程式"
description: "本教學課程說明如何 toocreate ASP.NET Core web 應用程式使用 Visual Studio 程式碼。"
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>在 Visual Studio Code 中建立 ASP.NET Core Web 應用程式
## <a name="overview"></a>概觀
本教學課程告訴您如何 toocreate ASP.NET Core web 應用程式使用[Visual Studio 程式碼 (VS Code)](http://code.visualstudio.com//Docs/whyvscode)並將它部署到太[Azure App Service](../app-service/app-service-value-prop-what-is.md)。 

> [!NOTE]
> 雖然這篇文章是指 tooweb 應用程式，它也適用於 tooAPI 應用程式和行動裝置應用程式。 
> 
> 

ASP.NET Core 是大幅重新設計的 ASP.NET。 ASP.NET Core 是新的開放原始碼和跨平台架構，用於使用 .NET 建置新代雲端式 Web 應用程式。 如需詳細資訊，請參閱[簡介 tooASP.NET 核心](http://docs.asp.net/latest/conceptual-overview/aspnet.html)。 如需有關 Azure App Service Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](app-service-web-overview.md)。

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>必要條件
* 安裝 [VS Code](http://code.visualstudio.com/Docs/setup)。
* 安裝 Git - 您可以從下列位置安裝它：[Chocolatey](https://chocolatey.org/packages/git) 或 [git-scm.com](http://git-scm.com/downloads)。如果您是新 tooGit，選擇  [git scm.com](http://git-scm.com/downloads)太選取 hello 選項**從 hello Windows 命令提示字元使用 Git**。 一旦您安裝 Git，您還需要 tooset hello Git 使用者名稱和電子郵件時 （從 VS 程式碼中執行認可） 時，稍後在 hello 教學課程所需。  

## <a name="install-aspnet-core"></a>安裝 ASP.NET Core
ASP.NET Core 是精簡的 .NET 堆疊，可建置 OS X、Linux 和 Windows 上執行的新式雲端和 Web 應用程式。 已建置從 hello 地面向上 tooprovide 是其中一個已部署的 toohello 雲端，或執行在內部部署的應用程式是最佳化的開發架構。 其由額外負荷最低的模組化元件組成，以便您可以在建構解決方案時保留彈性。

本教學課程是設計的 tooget 您開始建置 hello 最新開發版本的 ASP.NET Core 應用程式。 下列指示的 hello 是特定 tooWindows。 如需 OS X、Linux 和 Windows 的安裝指示，請參閱[開始使用 ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started)。 


> [!NOTE]
> 如需 OS X、Linux 和 Windows 的更詳細安裝指示，請參閱[安裝 ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)。 
> 
> 

## <a name="create-hello-web-app"></a>建立 hello web 應用程式
本節說明如何 tooscaffold 新應用程式的 ASP.NET web 應用程式使用 hello.NET CLI 工具。 

1. 輸入 hello 下列在 hello 命令提示字元 toocreate hello 專案資料夾，然後 scaffold hello 應用程式。
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 產生器](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello 必要的 NuGet 套件，請執行下列命令的 hello:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>在本機執行 hello web 應用程式
現在，您有建立 hello web 應用程式，並擷取所有 hello NuGet 套件 hello 應用程式，您可以在本機執行 hello web 應用程式。

1. 執行 hello 應用程式 (hello`dotnet run`過期時，命令將會建置 hello 應用程式):
    ```terminal
    dotnet run
    ```
2. 開啟瀏覽器，並瀏覽 toohello 下列 URL。
   
    **http://localhost:5000**
   
    hello hello web 應用程式的預設頁面會出現，如下所示。
   
    ![在瀏覽器中的本機 Web 應用程式](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. 關閉瀏覽器。 在 hello**命令視窗**，按**Ctrl + C**向下 hello 應用程式，然後關閉 hello tooshut**命令視窗**。 

## <a name="create-a-web-app-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立 web 應用程式
hello 下列步驟將引導您完成在 hello Azure 入口網站中建立 web 應用程式。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**新增**hello 在左上方的 hello 入口網站。
3. 按一下 [Web Apps] > [Web Apps]。
   
    ![Azure 的新 Web 應用程式](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. 輸入 [名稱] 的值，例如 **SampleWebAppDemo**。 請注意，此名稱必須唯一，toobe hello 入口網站將會強制執行，當您嘗試 tooenter hello 名稱。 因此，如果您選取輸入不同的值，您將需要值的 toosubstitute 每次發生**SampleWebAppDemo**您在本教學課程中看到。 
5. 選取現有的 **App Service 方案** 或建立新方案。 如果您建立新的計畫，請選取定價層、 位置和其他選項的 hello。 如需有關應用程式服務方案的詳細資訊，請參閱 hello 文章[Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。
   
    ![Azure 的新 Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. 按一下 [建立] 。
   
    ![Web 應用程式刀鋒視窗](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>啟用 Git 發行功能 hello 新 web 應用程式
Git 是分散式的版本控制系統，您可以使用 toodeploy Azure App Service web 應用程式。 想要儲存您的本機 Git 儲存機制，在 web 應用程式所撰寫的 hello 程式碼和您要部署您的程式碼 tooAzure 推送 tooa 遠端儲存機制。   

1. 登入 hello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [瀏覽] 。
3. 按一下**Web 應用程式**tooview hello 與您 Azure 訂用帳戶相關聯的 web 應用程式清單。
4. 選取您在本教學課程中建立的 hello web 應用程式。
5. 在 hello web 應用程式刀鋒視窗中，按一下 **設定** > **連續部署**。 
   
    ![Azure Web 應用程式主機](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. 按一下 [選擇來源] > [本機 Git 儲存機制]。
7. 按一下 [確定] 。
   
    ![Azure 本機 Git 儲存機制](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. 如果您先前尚未設定部署認證以供發佈 Web 應用程式或其他 App Service 應用程式，請立即設定：
   
   * 按一下 [設定] > [部署認證]。 hello**設定部署認證**刀鋒視窗會顯示。
   * 建立使用者名稱和密碼。  稍後設定 Git 時，您將需要此密碼。
   * 按一下 [儲存] 。
9. 在 Web 應用程式的刀鋒視窗中，按一下 [設定] > [屬性]。 hello hello 遠端 Git 儲存機制的 URL，您將會部署 toois 下方顯示**GIT URL**。
10. 複製 hello **GIT URL**供稍後使用 hello 教學課程中的值。
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>發行您的 web 應用程式 tooAzure 應用程式服務
在本節中，您將建立的本機 Git 儲存機制，並從該儲存機制 tooAzure toodeploy 推送您的 web 應用程式 tooAzure。

1. 在 VS 程式碼中，選取 hello **Git** hello 左側的導覽列中的選項。
   
    ![VS Code 中的 Git 圖示](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. 選取**初始化 git 儲存機制**toomake 確定您的工作區是在 git 原始檔控制之下。 
   
    ![初始化 Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. 開啟 hello 命令視窗，並變更您的 web 應用程式的目錄 toohello 目錄。 然後，輸入下列命令的 hello:
   
        git config core.autocrlf false
   
    此命令可防止涉及 CRLF 行尾結束符號和 LF 行尾結束符號之文字的相關問題。
4. 在 VS 程式碼中，加入 「 認可 」 訊息，按一下 hello**認可所有**核取圖示。
   
    ![Git 全部認可](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Git 已完成處理之後，您會看到沒有列在底下的 hello Git 視窗中的檔案**變更**。 
   
    ![Git 沒有變更](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. 變更後 toohello 命令視窗 hello 命令提示字元 toohello 目錄所指位置您 web 應用程式所在的位置。
7. 建立使用您先前複製的 Git URL （結束".git"中） hello 推送更新 tooyour web 應用程式的遠端參考。
   
        git remote add azure [URL for remote repository]
8. 在本機，因此它們會自動附加的 tooyour push 命令從 VS 程式碼產生設定 Git toosave 您的認證。
   
        git config credential.helper store
9. 輸入下列命令的 hello 推送變更 tooAzure。 這個初始的推播 tooAzure 之後, 您將會無法 toodo 所有 hello 發送都命令從 VS 程式碼。 
   
        git push -u azure master
   
    系統提示您輸入您稍早在 Azure 中建立的 hello 密碼。 **注意：將看不到您的密碼。**
   
    從上述命令 hello hello 輸出的最後一則訊息部署成功。
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> 若要變更 tooyour 應用程式，您可以重新發行使用 hello 內建的 Git 功能選取 hello 的 VS 程式碼中直接**認可所有**選項後面 hello**推送**選項。 您會發現 hello**推送**選項可以在 hello 下拉式功能表的 下一步 toohello**認可所有**和**重新整理**按鈕。
> 
> 

如果您需要在專案上的 toocollaborate，您應該考慮推送 tooGitHub 推送 tooAzure 之間。

## <a name="run-hello-app-in-azure"></a>在 Azure 中執行 hello 應用程式
既然您已部署的 hello 應用程式裝載於 Azure 時，我們先執行您 web 應用程式。 

這有兩種方式可以完成：

* 開啟瀏覽器然後輸入 hello 名稱的 web 應用程式，如下所示。   
  
        http://SampleWebAppDemo.azurewebsites.net
* 在 hello Azure 入口網站，找出 hello web 應用程式的 web 應用程式刀鋒視窗並按一下**瀏覽**tooview 您的應用程式 
* 預設瀏覽器

![Azure Web 應用程式](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>摘要
在本教學課程中，您學到如何 toocreate VS 程式碼中的 web 應用程式並將其部署 tooAzure。 如需 VS 程式碼的詳細資訊，請參閱 hello 文件，[為何 Visual Studio 程式碼？](https://code.visualstudio.com/Docs/) 如需 App Service Web Apps 的相關資訊，請參閱 [Web Apps概觀](app-service-web-overview.md)。 

