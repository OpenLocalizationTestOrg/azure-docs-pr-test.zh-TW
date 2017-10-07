---
title: "在 Linux 上的 Web 應用程式的.NET Core aaaUse |Microsoft 文件"
description: "在 Linux 上的 Web 應用程式中使用 .NET Core。"
keywords: "azure app service, Web 應用程式, dotnet, core, linux, oss"
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>在 Linux 上的 Azure Web 應用程式中使用 .NET Core #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro)on Linux 會提供可高度擴充、 自我修補 web 主控服務，使用 hello Linux 作業系統。 本教學課程包含逐步解說顯示如何 toocreate [.NET Core](https://docs.microsoft.com/aspnet/core/) on Linux 的 Azure web 應用程式為基礎的應用程式。 

![Linux 上的 Web 應用程式][10]

您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。

## <a name="prerequisites"></a>必要條件 ##

toocomplete 本教學課程： 

* 安裝 hello [.NET Core SDK](https://www.microsoft.com/net/download/core)。
* 安裝 [Git](https://git-scm.com/downloads)。

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>建立本機 .NET Core 應用程式 ##

啟動新的終端機工作階段。 建立名為目錄`hellodotnetcore`，並變更目前目錄 tooit hello。 然後輸入 hello 下列： 

```
dotnet new web
``` 

  此命令會建立三個檔案 (*hellodotnetcore.csproj*， *Program.cs*，和*Startup.cs*) 和一個空的資料夾 (*wwwroot /*)在 hello 目前的目錄。 內容的 hello`.csproj`檔案應該看起來像下列 hello: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

此應用程式是 web 應用程式，因為 ASP.NET Core 套件已自動參考 tooan 加入 toohello *hellodotnetcore.csproj*檔案。 根據選擇 framework toohello 設定 hello 套件 hello 版本號碼。 因為使用 .NET Core 1.1，所以此範例會參考 ASP.NET Core 1.1.2 版。

## <a name="build-and-test-hello-application-locally"></a>建置和測試本機 hello 應用程式 ##

您可以建置並執行.NET Core 應用程式以 hello`dotnet restore`命令，接著 hello`dotnet run`命令，如下所示：

```
dotnet restore
dotnet run
```


Hello 應用程式啟動時，它會顯示訊息，指出 hello 應用程式正在接聽連接埠 tooincoming 要求。 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

測試瀏覽過`http://localhost:5000/`與瀏覽器。 如果一切運作正常，您會看到 "Hello World!" 為 hello 結果文字。

![使用瀏覽器測試][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立.NET Core 應用程式 ##

首先，您需要 toocreate 空 web 應用程式。 登入 toohello [Azure 入口網站](https://portal.azure.com/)並建立新[Linux 上的 Web 應用程式](https://portal.azure.com/#create/Microsoft.AppSvcLinux)。

![建立 Web 應用程式][1]

當 hello**建立**頁面開啟時，提供您的 web 應用程式的詳細資料：

![選擇 .NET Core 執行階段堆疊][2]

使用 hello 下表作為指南 toofill 出 hello**建立**頁面上，然後選取 **確定**和**建立**toocreate hello 應用程式。

| 設定      | 建議的值  | 說明                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| 應用程式名稱 | hellodotnetcore  | hello 應用程式的名稱。 此名稱必須是唯一的。 |
| 訂用帳戶 | 選擇現有的訂用帳戶 | hello Azure 訂用帳戶。 |
| 資源群組 | myResourceGroup |  hello Azure 資源群組 toocontain hello web 應用程式。 |
| App Service 方案 | 現有的 App Service 方案名稱 |  hello 應用程式服務方案。  |
| 設定容器 | .NET Core 1.1 | hello 此 web 應用程式的容器類型： 內建、 Docker 或私人登錄中。 |
| 映像來源  | 內建  |  hello hello 映像的來源。 |
| 執行階段堆疊  | .NET Core 1.1  | 執行階段堆疊時會 hello 和版本。  |

## <a name="deploy-your-application-via-git"></a>透過 Get 部署應用程式 ##

在 Linux 上使用 Git toodeploy hello.NET Core 應用程式 tooAzure App Service Web 應用程式。

hello 新 Azure web 應用程式已經有 Git 部署設定。 您可以藉由瀏覽下列 URL 並插入您的 web 應用程式名稱的 toohello 找到 hello Git 部署 URL:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

hello Git URL 具有下列根據您的 web 應用程式名稱的 hello:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

執行下列命令 toodeploy hello 本機應用程式 tooyour Azure web 應用程式的 hello: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

您不需要 toopush 之下任何檔案*bin /*或*obj /*目錄 hello 雲端中建置應用程式，因為當 hello 應用程式的原始程式檔會推入 tooAzure。 Hello 建置程序完成之後，二進位檔案會複製到在 hello 應用程式的目錄*/住家/網站/wwwroot/*。

確認 hello 遠端部署作業報告成功。 推入作業可能需要一些時間，因為封裝解析度和建置在 hello 雲端中執行的程序。 您會看到數則狀態訊息，包括陳述已複製檔案的訊息。 hello 輸出應該看起來類似 toohello 下列：

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Hello 部署完成後，請重新啟動您的 web 應用程式，hello 部署 tootake 效果。 toodo 這個移 toohello Azure 入口網站及瀏覽 toohello**概觀**web 應用程式頁面。 選取 hello**重新啟動**hello 頁面中的按鈕。 快顯視窗出現時，選取**是**tooconfirm。 您可以瀏覽您的 Web 應用程式，如下所示：

![瀏覽.NET Core 應用程式部署 tooAzure Linux 上的應用程式服務][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>後續步驟
* [Linux 上的 Azure App Service Web 應用程式常見問題集](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
