---
title: "在 Azure App Service API 應用程式的 aaaUser 驗證 |Microsoft 文件"
description: "了解 tooprotect 藉由使用 Azure App Service 中的應用程式開發介面應用程式的唯一 tooauthenticated 使用者的存取方式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Azure App Service 中 API Apps 的使用者驗證
## <a name="overview"></a>概觀
這篇文章會示範如何 tooprotect 的 Azure API 應用程式，因此只能驗證的使用者可以呼叫它。 hello 文章假設您已閱讀 hello [Azure 應用程式服務驗證概觀](../app-service/app-service-authentication-overview.md)。

您將了解：

* 如何 tooconfigure 驗證提供者，具有 Azure Active Directory (Azure AD) 的詳細資料。
* Tooconsume 受保護的應用程式開發介面應用程式使用方式 hello [Active Directory 驗證程式庫 (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js)。

hello 文章包含兩個區段：

* hello[如何 tooconfigure Azure App Service 中的使用者驗證](#authconfig)章節將說明一般方式 tooconfigure 任何 API 應用程式的使用者驗證和同樣適用於支援的應用程式服務，包括.NET、 tooall 架構Node.js 和 Java。
* 開頭為 hello[繼續 hello.NET API 的應用程式教學課程](#tutorialstart)區段中，hello 您完成設定的.NET 範例應用程式備份結束和 AngularJS 前端使其使用 Azure Active Directory 使用者的文件指南驗證。 

## <a id="authconfig"></a>如何在 Azure App Service 中的 tooconfigure 使用者驗證
本節提供適用於 tooany API 應用程式的一般指示。 步驟特定 toohello tooDo 清單.NET 範例應用程式，跳過[繼續 hello.NET 使用者入門教學課程](#tutorialstart)。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式的 tooprotect，尋找 hello**功能**區段，，然後按一下**驗證 / 授權**。
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。
3. 選取其中一個 hello 選項從 hello**當要求未經驗證的動作 tootake**下拉式清單。
   
   * 如果您想只驗證的呼叫 tooreach 您 API 應用程式，選擇其中一個 hello**登入...**選項。 此選項可讓您 tooprotect hello API 應用程式而不需要撰寫任何程式碼中執行。
   * 如果您想要的所有電話 tooreach 您 API 應用程式，選擇**允許要求 （無動作）**。 您可以使用這個選項 toodirect 未經驗證的呼叫端 tooa 選擇的驗證提供者。 使用此選項時，您會有 toowrite 程式碼 toohandle 授權。
     
     如需詳細資訊，請參閱 [Azure App Service 中的 API Apps 驗證與授權](app-service-api-authentication.md#multiple-protection-options)。
4. 選取一或多個 hello**驗證提供者**。
   
    hello 影像顯示的選項需要 Azure AD 驗證的所有呼叫端 toobe。
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    當您選擇的驗證提供者時，hello 入口網站組態刀鋒視窗中顯示該提供者。 
   
    如需詳細指示，說明如何 tooconfigure hello 驗證提供者組態刀鋒視窗，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。 （hello 連結是有關在 Azure AD，tooan 發行項，但是本身 hello 文章包含連結的 hello tooarticles 其他驗證提供者的索引標籤）。
5. 當您完成 hello 驗證提供者組態刀鋒視窗中時，按一下 **確定**。
6. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。

完成此動作後，應用程式服務在到達 hello API 應用程式之前，就會驗證所有 API 呼叫。 hello 驗證服務的運作 hello 相同的應用程式的服務支援，包括.NET、 Node.js 和 Java 的所有語言。 

toomake 驗證 API 呼叫、 hello 呼叫端 hello 授權標頭的 HTTP 要求中包含 hello 驗證提供者的 OAuth 2.0 承載權杖。 hello 語彙基元可藉由使用 hello 驗證提供者的 SDK。

## <a id="tutorialstart"></a>繼續 hello.NET API 的應用程式教學課程
如果您要遵照 API 應用程式的 hello Node.js 或 Java 教學課程，請略過 toohello 下一個文件： [API 應用程式的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)。 

如果您要遵照 hello.NET 教學課程系列的 API 應用程式，並已部署 hello 範例應用程式中的 hello[第一個](app-service-api-dotnet-get-started.md)和[第二個](app-service-api-cors-consume-javascript.md)教學課程，請略過 toohello[設定應用程式服務和 Azure AD 中的驗證](#azureauth)> 一節。

如果您想 toofollow 本教學課程無須經過 hello 第一個和第二個教學課程，請勿 hello 下列步驟說明如何使用自動化程序 toodeploy hello 範例應用程式 tooget 啟動。

> [!NOTE]
> hello 下列步驟協助您取得的 toohello 相同起點時，如果您未 hello 前兩個教學課程中的，有一個例外狀況： Visual Studio 不會知道哪些 web 應用程式或每個專案部署至 API 應用程式。 這表示您不需要在此教學課程中說明的確切指示如何 toodeploy toohello 右目標。 如果您不想要找出 toodo hello 部署您自己的步驟，是較佳 toofollow hello 教學課程系列從 hello[第一個教學課程](app-service-api-dotnet-get-started.md)比 toostart 與此自動化部署程序。
> 
> 

1. 請確定您有所有 hello 中所列的 hello 必要條件[第一個教學課程](app-service-api-dotnet-get-started.md)。 中所列的加法 toohello 必要條件，這些驗證教學課程假設您已使用 App Service web 應用程式與 Visual Studio 中的應用程式開發介面應用程式和 hello Azure 入口網站。
2. 按一下 hello**部署 tooAzure**按鈕在 hello [tooDo 清單範例儲存機制讀我檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md)toodeploy hello API 應用程式和 hello web 應用程式。 記下 hello Azure 資源群組的建立，因為您可以使用這個更新 toolook web 應用程式及 API 應用程式名稱。
3. 下載或複製 hello [tooDo 清單範例儲存機制](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)tooget hello 程式碼，您會與本機 Visual Studio 中。

## <a id="azureauth"></a> 在 App Service 和 Azure AD 中設定驗證
您現在可以 hello Azure App Service 中執行，而不需要使用者進行驗證的應用程式。 在本節中，您可以加入驗證執行下列工作的 hello:

* 設定應用程式服務 toorequire Azure Active Directory (Azure AD) 驗證，來呼叫 hello 中介層應用程式開發介面應用程式。
* 建立 Azure AD 應用程式。
* 登入 toohello AngularJS 前端之後設定 hello Azure AD 應用程式 toosend hello 持有人權杖。 

如果您執行下列 hello 教學課程指引時出現問題，請參閱 hello[疑難排解](#troubleshooting)hello 結尾 hello 教學課程 > 一節。 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>設定 hello 中介層應用程式開發介面應用程式的驗證
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**hello API 應用程式，您所建立的刀鋒視窗中的 hello ToDoListAPI 專案中，尋找 hello**功能** 區段中，然後按一下**驗證 / 授權**。
   
    ![Azure 入口網站驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。
3. 在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory**。
   
    此選項可確保任何 unauathenticated 要求會到達 hello API 應用程式。 
4. 在 [驗證提供者] 底下，按一下 [Azure Active Directory]。
   
    ![Azure 入口網站驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. 在 hello **Azure Active Directory 設定**刀鋒視窗中，按一下  **Express**
   
    ![Azure 入口網站驗證/授權表達選項](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    以 hello **Express**選項時，應用程式服務可以自動建立 Azure AD 應用程式在您的 Azure AD 中[租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)。 
   
    您不需要 toocreate 租用戶，因為每個 Azure 帳戶會自動擁有一個。
6. 下**管理模式**，按一下**建立新的 AD 應用程式**如果尚未選取，並請注意在 hello hello 值**建立應用程式**文字方塊中，您將查閱此 AADhello Azure 傳統入口網站更新版本中的應用程式。
   
    ![Azure 入口網站 Azure AD 設定](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure 會自動建立 Azure AD 應用程式與 Azure AD 租用戶中的 hello 指定名稱。 根據預設，名為 hello Azure AD 應用程式相同 hello 與 hello API 應用程式。 如有需要，也可以輸入不同名稱。
7. 按一下 [確定] 。
8. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

現在只有 Azure AD 租用戶的使用者，才可以呼叫 hello API 應用程式。

### <a name="optional-test-hello-api-app"></a>選擇性： 測試 hello API 的應用程式
1. 在瀏覽器中前往 toohello hello API 應用程式 URL: hello 中**API 應用程式**刀鋒視窗中 hello Azure 入口網站中，按一下底下的 hello 連結**URL**。  
   
    您是重新導向的 tooa 登入畫面，因為 tooreach hello API 應用程式不允許未經驗證的要求。
   
    如果您的瀏覽器 toohello 「 成功建立 」 頁面，hello 瀏覽器可能已登入-在此情況下，開啟 InPrivate 或 Incognito 視窗，並移 toohello API 應用程式的 URL。
2. 在 Azure AD 租用戶中以使用者的認證進行登入。
   
    當您登入時，hello"建立成功 」 的頁面會顯示 hello 瀏覽器中。
3. 關閉 hello 瀏覽器。

### <a name="configure-hello-azure-ad-application"></a>Hello Azure AD 應用程式設定
當您設定了 Azure AD 驗證，App Service 就會為您建立 Azure AD 應用程式。 根據預設 hello 新的 Azure AD 應用程式已設定的 tooprovide hello 持有人權杖 toohello API 應用程式的 URL。 本節中，您會設定 hello Azure AD 應用程式 tooprovide hello 持有人權杖 toohello AngularJS 前端而不是直接 toohello 中介層應用程式開發介面應用程式。 hello AngularJS 前端呼叫 hello API 應用程式時，會傳送 hello 語彙基元 toohello API 應用程式。

> [!NOTE]
> tookeep hello 程序越簡單越好，本教學課程會使用單一的 Azure AD 應用程式來進行 hello 前端和 hello 中介層應用程式開發介面應用程式。 另一個選項是 toouse 兩個 Azure AD 應用程式。 在此情況下，您必須 toogive hello 前端的 Azure AD 應用程式的權限 toocall hello 中介層的 Azure AD 應用程式。 此多重應用程式的方法會提供更細微地控制的權限 tooeach 層。
> 
> 

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，跳過**Azure Active Directory**。
   
   您必須 toouse hello 傳統入口網站，因為某些 Azure Active Directory 設定，您需要存取 tooare 尚無法使用 hello 目前的 Azure 入口網站中。
2. 在 hello**目錄**索引標籤上，按一下您的 AAD 租用戶。
   
   ![傳統入口網站的 Azure AD](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. 按一下**應用程式 > 我公司所擁有的應用程式**，然後按一下hello 核取記號。
   
   您可能還有 toorefresh hello 頁面 toosee hello 新的應用程式。
4. Hello 應用程式清單中按一下 hello hello 時您的應用程式開發介面應用程式啟用驗證為您建立 Azure 的其中一個名稱。
   
   ![Azure AD [應用程式] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. 按一下 [設定] 。
   
   ![Azure AD [設定] 索引標籤](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. 設定**登入 URL** toohello URL AngularJS web 應用程式，沒有尾端斜線。
   
   例如：https://todolistangular.azurewebsites.net
   
   ![登入 URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. 設定**回覆 URL** toohello URL，web 應用程式，沒有尾端斜線。
   
   例如：https://todolistsangular.azurewebsites.net
8. 按一下 [儲存] 。
   
   ![回覆 URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. 在 hello hello 頁面底部，按一下**管理資訊清單 > 下載資訊清單**。
   
   ![下載資訊清單](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. 下載 hello 檔案 tooa 位置可在其中編輯它。
11. 在 hello 下載資訊清單檔案，搜尋 hello`oauth2AllowImplicitFlow`屬性。 變更這個屬性從 hello 值`false`太`true`，然後儲存 hello 檔案。
    
    必須要有這項設定才能從 JavaScript 單一頁面應用程式進行存取。 它可讓 hello Oauth 2.0 承載權杖 toobe hello URL 片段中傳回。
12. 按一下**管理資訊清單 > 上傳資訊清單**，和上傳 hello 檔案，您在 hello 前面步驟中更新。
    
    ![上傳資訊清單](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. 複製 hello**用戶端識別碼**值，並將其儲存的地方，就可以從更新版本。

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>設定 hello ToDoListAngular 專案 toouse 驗證
本節中您會變更 hello AngularJS 前端，使其使用 Active Directory 驗證程式庫 (ADAL) for JS tooacquire hello 登入的使用者從 Azure AD 的承載權杖。 hello 程式碼會將包含 hello 語彙基元傳送 toohello 中介層，HTTP 要求中 hello 下列圖表所示。 

![使用者驗證圖表](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

請遵循變更 toofiles hello ToDoListAngular 專案中的 hello。

1. 開啟 hello *index.cshtml*檔案。
2. 參考 JS 指令碼的 hello Active Directory 驗證程式庫 (ADAL) 的 hello 行取消註解。
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. 開啟 hello *app/scripts/app.js*檔案。
4. 註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。
   
    這項變更參考 hello ADAL JS 驗證提供者，並提供組態值 tooit。 您可以在 hello 下列步驟設定 hello API 應用程式和 Azure AD 應用程式的組態值。
5. 設定 hello hello 程式碼中`endpoints`hello API 應用程式，您建立 hello ToDoListAPI 專案，並將設定的變數，將 hello API URL toohello URL hello Azure AD 應用程式識別碼 toohello 用戶端識別碼，您所複製的 hello Azure 傳統入口網站。
   
    下列範例類似 toohello 的現在 hello 程式碼。
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. 在 hello 呼叫太`adalProvider.init`，將`tenant`tooyour 租用戶名稱和`clientId`toosame hello 先前步驟中的值。
   
    下列範例類似 toohello 的現在 hello 程式碼。
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    這些變更太`app.js`指定 hello 呼叫程式碼和呼叫 API 的 hello 位於 hello 相同的 Azure AD 應用程式。
7. 開啟 hello *app/scripts/homeCtrl.js*檔案。
8. 註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。
9. 開啟 hello *app/scripts/indexCtrl.js*檔案。
10. 註解的程式碼的 hello 區塊標示為 「 未驗證 」，並取消註解的程式碼的 hello 區塊標示為 [使用驗證]。

### <a name="deploy-hello-todolistangular-project-tooazure"></a>部署 hello ToDoListAngular 專案 tooAzure
1. 在**方案總管 中**hello ToDoListAngular 專案中，以滑鼠右鍵按一下，然後按**發行**。
2. 按一下 [發行] 。
   
    Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello web 應用程式的基底 URL。 這會顯示 403 錯誤頁面上，也就是從瀏覽器嘗試 toogo tooa Web API 基底 URL 的一般。
   
    您仍然必須 toomake 變更 toohello 中介層應用程式開發介面應用程式之前，您可以測試 hello 應用程式。
3. 關閉 hello 瀏覽器。

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>設定 hello ToDoListAPI 專案 toouse 驗證
目前 hello ToDoListAPI 專案傳送"*"做為 hello`owner`值 tooToDoListDataAPI。 本節中您要變更 hello 程式碼 toosend hello hello 登入的使用者識別碼。

請 hello 遵循 hello ToDoListAPI 專案中的變更。

1. 開啟 hello *Controllers/ToDoListController.cs*檔案，並設定每個動作方法中的 hello 行取消註解`owner`toohello Azure AD`NameIdentifier`宣告值。 例如：
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **重要**： 不要取消註解程式碼中 hello`ToDoListDataAPI`方法; 您將會執行，稍後 hello 服務主體的驗證教學課程。

### <a name="deploy-hello-todolistapi-project-tooazure"></a>部署 hello ToDoListAPI 專案 tooAzure
1. 在**方案總管 中**hello ToDoListAPI 專案中，以滑鼠右鍵按一下，然後按**發行**。
2. 按一下 [發行] 。
   
    Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello API 應用程式的基底 URL。
3. 關閉 hello 瀏覽器。

### <a name="test-hello-application"></a>測試 hello 應用程式
1. 移 toohello hello web 應用程式，URL**使用 HTTPS，而不是 HTTP**。
2. 按一下 hello **tooDo 清單** 索引標籤。
   
    您必須提示的 toolog 中。
3. Hello AAD 租用戶中的使用者的認證登入。
4. hello **tooDo 清單**頁面隨即出現。
   
   ![tooDo 清單頁面](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   目前並不會顯示任何待辦事項項目，因為這些項目到目前為止全都適用於擁有者 "*"。 Hello 中介層現在要求 hello 登入之使用者的項目，並無尚未建立。
5. 加入新的待辦項目 tooverify 正在 hello 應用程式。
6. 在另一個瀏覽器視窗中，移 toohello 的 UI Swagger URL hello ToDoListDataAPI API 應用程式，然後按一下**ToDoList > 取得**。 輸入星號 hello`owner`參數，然後再按一下**現在就試試看**。
   
   hello 回應會顯示 hello 新待辦項目有 hello 實際的 Azure AD 使用者識別碼 hello 擁有者屬性中。
   
   ![JSON 回應中的擁有者識別碼](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>建置從頭 hello 專案
hello 兩個 Web API 專案所建立的 hello **Azure API 應用程式**專案範本和取代 hello 預設值的控制站與 ToDoList 控制站。 

如需有關資訊太建立 AngularJS 單一頁面應用程式 Web API 2 的後端，請參閱[手上實驗室： 建置單一頁面應用程式 (SPA)，使用 ASP.NET Web API 和 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。 如需有關資訊 tooadd Azure AD 驗證程式碼，請參閱下列資源的 hello:

* [使用 Azure AD 保護 AngularJS 單一頁面應用程式](../active-directory/active-directory-devquickstarts-angular.md)。
* [簡介 ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* 請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。 例如，確認您新增 authentication toohello 中介層應用程式開發介面應用程式，hello 資料層。 
* 請確定 hello AngularJS 來源的程式碼參考 hello 中介層應用程式開發介面應用程式 URL （ToDoListAPI、 不 ToDoListDataAPI） 和 hello 修正 Azure AD 用戶端識別碼。 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學會 toouse App Service API 應用程式的驗證和 toocall hello API 應用程式使用的方式 hello JS ADAL 程式庫。 Hello 下一個教學課程中您將學習如何太[tooyour API 應用程式安全地存取服務對服務案例](app-service-api-dotnet-service-principal-auth.md)。

