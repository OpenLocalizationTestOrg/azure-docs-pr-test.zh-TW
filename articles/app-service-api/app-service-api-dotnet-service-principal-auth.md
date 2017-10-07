---
title: "Azure App Service 中的 API Apps aaaService 主體驗證 |Microsoft 文件"
description: "深入了解如何在 Azure App Service 中的服務對服務案例的 tooprotect API 應用程式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>在 Azure App Service 中 API Apps 的服務主體驗證
## <a name="overview"></a>概觀
這篇文章說明如何 toouse 應用程式服務驗證*內部*存取 tooAPI 應用程式。 內部的案例是您必須要 toobe 您可以使用自己的應用程式程式碼只能由 API 應用程式的位置。 hello 建議的方式 tooimplement 這種情況下在應用程式服務 toouse Azure AD tooprotect hello 稱為 API 應用程式。 您可以呼叫受保護的 hello API 應用程式，以從 Azure AD 取得藉由提供應用程式識別 （服務主體） 認證的承載權杖。 替代項目 toousing Azure AD，請參閱 hello**服務對服務驗證**區段 hello [Azure 應用程式服務驗證概觀](../app-service/app-service-authentication-overview.md#service-to-service-authentication)。

在本文中，您將了解：

* 如何從 toouse Azure Active Directory (Azure AD) tooprotect API 應用程式未經驗證的存取。
* 如何從應用程式開發介面應用程式、 web 應用程式或行動裝置應用程式使用 Azure AD 服務主體 （應用程式身分識別） 認證 tooconsume 受保護的應用程式開發介面應用程式。 如需有關資訊 tooconsume 從邏輯應用程式，請參閱[使用您裝載邏輯應用程式的 App Service 上的自訂 API](../logic-apps/logic-apps-custom-hosted-api.md)。
* 如何 toomake 確認該 hello 保護 API 應用程式無法從瀏覽器呼叫登入的使用者。
* Toomake 確認該 hello 保護 API 應用程式只能由特定呼叫 Azure AD 服務主體。

hello 文章包含兩個區段：

* hello [tooconfigure 服務主體驗證 Azure App Service 中的方式](#authconfig)章節將說明一般方式 tooconfigure 驗證的任何應用程式開發介面應用程式和 tooconsume hello 如何保護應用程式開發介面應用程式。 本章節同樣適用於 tooall 架構應用程式服務，包括.NET、 Node.js 和 Java 支援。
* 開頭為 hello[繼續 hello.NET 使用者入門教學課程](#tutorialstart) 區段中，hello 教學課程引導您設定 App Service 中執行的.NET 範例應用程式的 「 內部存取 」 案例。 

## <a id="authconfig"></a>Tooconfigure 服務主體驗證 Azure App Service 中的方式
本節提供適用於 tooany API 應用程式的一般指示。 步驟特定 toohello tooDo 清單.NET 範例應用程式，跳過[繼續 hello.NET API 的應用程式的教學課程系列](#tutorialstart)。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式，tooprotect，並找出 hello**功能**區段，然後按一下**驗證 / 授權**。
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。
3. 在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory** 。
4. 在 [驗證提供者] 底下，選取 [Azure Active Directory]。
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. 設定 hello **Azure Active Directory 設定**刀鋒視窗 toocreate 新的 Azure AD 應用程式或使用現有 Azure AD 的應用程式如果您已經有您想 toouse。
   
    內部案例通常涉及 API 應用程式呼叫 API 應用程式。 您可以為每一個 API 應用程式使用個別的 Azure AD 應用程式，或是全都使用同一個 Azure AD 應用程式。
   
    如需此刀鋒視窗的詳細指示，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。
6. 當您完成 hello 驗證提供者組態刀鋒視窗中時，按一下 **確定**。
7. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

完成此動作後，應用程式服務僅允許要求呼叫端在 hello 設定 Azure AD 租用戶。 受保護的 hello API 應用程式中不需要任何驗證或授權的程式碼。 hello 持有人權杖會傳入 toohello API 應用程式，以及常用的宣告 HTTP 標頭，而且您可以讀取該要求是從特定的呼叫者，例如服務主體的程式碼 toovalidate 中的資訊。

此驗證功能的運作方式 hello 一樣適用於所有語言的應用程式服務支援，包括.NET、 Node.js 和 Java。 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Tooconsume hello 如何保護應用程式開發介面應用程式
hello 呼叫者必須提供應用程式開發介面呼叫 Azure AD 持有人權杖。 tooget 持有者權杖，使用服務主體認證，hello 呼叫端會使用 Active Directory Authentication Library (ADAL for [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory)， [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs)，或[Java](https://github.com/AzureAD/azure-activedirectory-library-for-java))。 tooget 語彙基元，呼叫 ADAL 的 hello 程式碼提供下列資訊 tooADAL hello:

* hello Azure AD 租用戶名稱。
* hello 用戶端識別碼和用戶端 （應用程式金鑰） 的密碼與 hello 呼叫端相關聯的 hello Azure AD 應用程式。
* hello 用戶端識別碼 hello hello 與相關聯的 Azure AD 應用程式的受保護的應用程式開發介面應用程式。 (如果使用只在一個 Azure AD 應用程式時，這是 hello 相同的用戶端識別碼為 hello 一個 hello 呼叫端。)

這些值為 hello 的 hello Azure AD 頁面中提供[Azure 傳統入口網站](https://manage.windowsazure.com/)。

一旦取得的 hello 語彙基元，hello 呼叫端會包含它與 hello 授權標頭中的 HTTP 要求。  應用程式服務會驗證 hello 語彙基元，並允許 hello 要求 tooreach hello 保護 API 應用程式。

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>如何從 hello 中的使用者存取 tooprotect hello API 應用程式相同租用戶
持有者權杖供使用者在同一個租用戶會被視為有效的 hello hello 受保護的應用程式開發介面應用程式。  如果您想要只服務主體可以呼叫的 tooensure hello 受保護的應用程式開發介面應用程式，新增 hello 中的程式碼保護應用程式開發介面應用程式 toovalidate hello 遵循 hello 語彙基元的宣告：

* `appid`應該 hello 與 hello 呼叫端相關聯的 hello Azure AD 應用程式的用戶端識別碼。 
* `oid`(`objectidentifier`) 應該是 hello hello 呼叫端的服務主體識別碼。 

應用程式服務也提供 hello `objectidentifier` hello X MS-用戶端-主體識別碼標頭中的宣告。

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>如何 tooprotect hello 從瀏覽器存取的 API 應用程式
如果您不要驗證在 hello 受保護的應用程式開發介面應用程式中的程式碼中的宣告，如果您使用不同的 Azure AD 應用程式 hello 受保護的應用程式開發介面應用程式，請確定該 hello Azure AD 應用程式的回覆 URL 是不 hello 與 hello API 應用程式的基底 URL 相同。 如果 hello 回覆 URL 直接點 toohello 受保護的應用程式開發介面應用程式、 hello 相同的 Azure AD 租用戶中的使用者無法瀏覽 toohello API 應用程式、 登入，並且成功呼叫 hello API。

## <a id="tutorialstart"></a>繼續 hello.NET API 的應用程式的教學課程
如果您要遵照 hello Node.js 或 Java 教學課程系列的 API 應用程式，請略過 toohello[後續步驟](#next-steps)> 一節。 

hello 本文其餘部分會繼續 hello.NET API 的應用程式的教學課程，而且假設您已經完成 hello[使用者驗證教學課程](app-service-api-dotnet-user-principal-auth.md)，而且有 hello 範例應用程式在 Azure 中執行的使用者驗證啟用。

## <a name="set-up-authentication-in-azure"></a>在 Azure 中設定驗證
本節中您設定應用程式服務因此它可讓 tooreach hello 資料層應用程式開發介面應用程式的只有 HTTP 要求該 hello hello 的有有效的 Azure AD 持有者權杖。 

在下列章節的 hello，設定 hello 中介層應用程式開發介面應用程式 toosend 應用程式認證 tooAzure AD、 取回持有者權杖，並傳送 hello 持有人權杖 toohello 資料層應用程式開發介面應用程式。 此程序如下所示 hello 圖表。

![服務驗證圖表](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

如果您執行下列 hello 教學課程指引時出現問題，請參閱 hello[疑難排解](#troubleshooting)hello 結尾 hello 教學課程 > 一節。 

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 toohello**設定**刀鋒視窗中的 hello API 應用程式，您建立 hello ToDoListDataAPI （資料層） API 應用程式，然後按一下**設定**。
2. 在 hello**設定**刀鋒視窗中，尋找 hello**功能**區段，然後再按一下**驗證 / 授權**。
   
    ![Azure 入口網站中的驗證/授權](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **上**。
4. 在 hello**當要求未經驗證的動作 tootake**下拉式清單中，選取**登入 Azure Active Directory**。
   
    這是造成只有已驗證要求觸達 hello API 應用程式的應用程式服務 tooensure hello 設定。 具有有效的持有者權杖的要求，應用程式服務傳遞 hello 語彙基元沿著 toohello API 應用程式並於其中填入的 HTTP 標頭與常用的宣告 toomake 該資訊更易於使用 tooyour 程式碼。
5. 在 [驗證提供者] 底下，按一下 [Azure Active Directory]。
   
    ![Azure 入口網站中的驗證/授權刀鋒視窗](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. 在 hello **Azure Active Directory 設定**刀鋒視窗中，按一下  **Express**。
   
    以 hello **Express**選項 Azure 可以自動建立 AAD 應用程式，您的 Azure AD 中[租用戶](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)。 
   
    您不需要 toocreate 租用戶，因為每個 Azure 帳戶會自動擁有一個。
7. 在 [管理模式] 底下，按一下 [建立新的 AD 應用程式] \(若尚未選取)。
   
    hello 入口網站外掛 hello**建立應用程式**輸入的方塊中，預設值。 根據預設，名為 hello Azure AD 應用程式相同 hello 與 hello API 應用程式。 如有需要，也可以輸入不同名稱。
   
    ![Azure AD 設定](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **請注意**： 或者，您可以使用單一的 Azure AD 應用程式的同時 hello 呼叫 API 的應用程式和 hello 保護 API 應用程式。 如果您選擇其他的替代方法，您不需要 hello**建立新的 AD 應用程式**這裡選項，因為您稍早在 hello 使用者驗證教學課程中，已經建立 Azure AD 應用程式。 此教學課程中，您將使用不同 Azure AD 應用程式呼叫 API 應用程式和 hello hello 受保護的應用程式開發介面應用程式。
8. 請記下在 hello hello 值**建立應用程式**輸入的方塊中，您將此 AAD 應用程式中查閱 hello Azure 傳統入口網站更新版本。
9. 按一下 [確定] 。
10. 在 hello**驗證 / 授權**刀鋒視窗中，按一下 **儲存**。
    
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    應用程式服務會建立 Azure Active Directory 應用程式與**登入 URL**和**回覆 URL**自動設定 toohello API 應用程式的 URL。 在您 AAD 租用戶 toolog 中的使用者和存取 hello API 應用程式，可讓 hello 第二個值。

### <a name="verify-that-hello-api-app-is-protected"></a>確認該 hello API 應用程式受到保護
1. 在瀏覽器中前往 toohello hello API 應用程式 URL: hello 中**API 應用程式**刀鋒視窗中 hello Azure 入口網站中，按一下底下的 hello 連結**URL**。 
   
    您是重新導向的 tooa 登入畫面，因為 tooreach hello API 應用程式不允許未經驗證的要求。 
   
    如果您的瀏覽器並移 toohello Swagger UI，您的瀏覽器可能已經登入--在此情況下，開啟 InPrivate 或 Incognito 視窗和移 toohello 的 UI Swagger URL。
2. 使用 AAD 租用戶中使用者的認證進行登入。
   
   當您登入時，hello"建立成功 」 的頁面會顯示 hello 瀏覽器中。

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>設定 hello ToDoListAPI 專案 tooacquire 和傳送 hello Azure AD 權杖
本節中您不要 hello 下列工作：

* 加入程式碼 hello 中介層應用程式開發介面應用程式中使用 Azure AD 應用程式認證 tooacquire 語彙基元，並傳送的 HTTP 要求 toohello 資料層應用程式開發介面應用程式。
* 從 Azure AD 取得您需要的 hello 認證。
* Hello 認證輸入 hello 中介層應用程式開發介面應用程式中的 Azure 應用程式服務執行階段環境設定。 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>設定 hello ToDoListAPI 專案 tooacquire 和傳送 hello Azure AD 權杖
請遵循 Visual Studio 中的 hello ToDoListAPI 專案中的變更 hello。

1. 取消所有 hello hello 中的程式碼註解*ServicePrincipal.cs*檔案。
   
    這是.NET tooacquire hello Azure AD 持有人權杖中會使用 ADAL 的 hello 程式碼。  它會使用幾個可在 hello Azure 執行階段環境中設定更新版本的組態值。 Hello 程式碼如下： 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **注意：**此程式碼需要.NET NuGet 套件 (Microsoft.IdentityModel.Clients.ActiveDirectory)，已安裝在 hello 專案中的 hello ADAL。 如果您從頭開始建立這個專案，您必須 tooinstall 此封裝。 此套件不會自動安裝由 hello API 應用程式的新專案範本。
2. 在*控制器/ToDoListController*，請取消註解 hello hello 中的程式碼`NewDataAPIClient`將 hello 授權標頭中的 hello tooHTTP 權杖要求方法。
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. 部署 hello ToDoListAPI 專案。 (Hello 專案上按一下滑鼠右鍵，然後按一下 **發行 > 發行**。)
   
    Visual Studio 部署 hello 專案，並開啟瀏覽器 toohello web 應用程式的基底 URL。 這會顯示 403 錯誤頁面上，也就是從瀏覽器嘗試 toogo tooa Web API 基底 URL 的一般。
4. 關閉 hello 瀏覽器。

### <a name="get-azure-ad-configuration-values"></a>取得 Azure AD 設定值
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，跳過**Azure Active Directory**。
2. 在 hello**目錄**索引標籤上，按一下您的 AAD 租用戶。
3. 按一下**應用程式 > 我公司所擁有的應用程式**，然後按一下hello 核取記號。
4. Hello 應用程式清單中按一下 hello hello 時啟用 hello ToDoListDataAPI （資料層） API 的應用程式的驗證為您建立 Azure 的其中一個名稱。
5. 按一下 hello**設定** 索引標籤。
6. 複製 hello**用戶端識別碼**值，並將其儲存位置，就可以從更新版本。 
7. 在 hello Azure 傳統入口網站移回 toohello 清單**我公司所擁有的應用程式**，然後按一下您建立 hello 中介層 ToDoListAPI API 應用程式 (不在 hello 上一個教學課程中，建立一個 hello hello AAD 應用程式hello 本教學課程中建立)。
8. 按一下 hello**設定** 索引標籤。
9. 複製 hello**用戶端識別碼**值，並將其儲存位置，就可以從更新版本。
10. 在下**金鑰**，選取**1 年**從 hello**選取持續時間**下拉式清單。
11. 按一下 [儲存] 。
    
     ![產生應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. 複製 hello 索引鍵值，並將其儲存位置，就可以從更新版本。
    
     ![複製新的應用程式金鑰](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>在 hello 中介層應用程式開發介面應用程式的執行階段環境中設定 Azure AD
1. 移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **API 應用程式**刀鋒視窗中的 hello API 應用程式裝載 hello TodoListAPI （中介層） 專案。
2. 按一下 [設定] > [應用程式設定]。
3. 在 hello**應用程式設定**區段中，加入下列的 hello 索引鍵和值：
   
   | **金鑰** | ida:Authority |
   | --- | --- |
   | **值** |https://login.microsoftonline.com/{您的 Azure AD 租用戶名稱} |
   | **範例** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Key** | ida:ClientId |
   | --- | --- |
   | **值** |用戶端識別碼 hello 呼叫應用程式 （中介層-ToDoListAPI） |
   | **範例** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **金鑰** | ida:ClientSecret |
   | --- | --- |
   | **值** |Hello 呼叫應用程式 （中介層-ToDoListAPI） 的應用程式金鑰 |
   | **範例** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **金鑰** | ida:Resource |
   | --- | --- |
   | **值** |Hello 呼叫應用程式的用戶端識別碼 （資料層-ToDoListDataAPI） |
   | **範例** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **請注意**： 的`ida:Resource`，請確定您使用呼叫應用程式的 hello**用戶端識別碼**而非其**應用程式識別碼 URI**。
   
    `ida:ClientId`和`ida:Resource`不同本教學課程中的值，因為您正在使用分隔 Azure AD applicaations hello 中介層和資料層。 如果您使用單一 Azure AD 應用程式呼叫 API 應用程式和 hello hello 受保護的應用程式開發介面應用程式，您會使用相同的值中的 hello`ida:ClientId`和`ida:Resource`。
   
    hello 程式碼會使用 ConfigurationManager tooget 這些值，因此它們無法在 hello 專案的 Web.config 檔案或 hello Azure 執行階段環境中儲存。 當 ASP.NET 應用程式在 Azure App Service 中執行時，環境設定會自動覆寫 Web.config 的設定。環境設定通常是[更安全方式 toostore 機密資訊比較 tooa Web.config 檔案](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。
4. 按一下 [儲存] 。
   
    ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>測試 hello 應用程式
1. 在瀏覽器移 toohello hello AngularJS 前端 web 應用程式的 HTTPS URL。
2. 按一下 hello **tooDo 清單** 索引標籤並登入 Azure AD 租用戶中使用者的認證。 
3. 加入待辦項目 tooverify 正在 hello 應用程式。
   
    ![tooDo 清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    如果 hello 應用程式不會在如預期般運作，請仔細檢查所有您輸入 hello Azure 入口網站中的 hello 設定。 如果所有的 hello 設定出現 toobe 正確，請參閱 hello[疑難排解](#troubleshooting)稍後在本教學課程 > 一節。

## <a name="protect-hello-api-app-from-browser-access"></a>防止瀏覽器存取的 hello API 應用程式
在此教學課程中，您建立個別 hello ToDoListDataAPI （資料層） API 應用程式的 Azure AD 應用程式。 如您所見，當應用程式服務建立 AAD 應用程式，它會設定 hello AAD 應用程式上啟用使用者 toogo toohello API 應用程式的 URL 在瀏覽器和記錄檔中的方式。 這表示這是可能的 Azure AD 租用戶中，不只是服務主體使用者，tooaccess hello 應用程式開發介面。 

如果您想 tooprevent 瀏覽器存取，且不受 hello 中撰寫任何程式碼保護 API 應用程式，您可以變更 hello**回覆 URL** hello AAD 應用程式中，讓它與 hello API 應用程式的不同基底 URL。 

### <a name="disable-browser-access"></a>停用瀏覽器存取
1. Hello 傳統入口網站中的**設定**hello AAD 應用程式所建立的 hello TodoListService 索引標籤上，變更在 hello hello 值**回覆 URL**欄位，讓它是有效的 URL，但不是 hello API 的應用程式URL。
2. 按一下 [儲存] 。

### <a name="verify-browser-access-no-longer-works"></a>確認瀏覽器存取無法再運作
您稍早驗證，您可以移 toohello API 應用程式 URL 從瀏覽器以個別使用者的認證登入。 在本節中，您將要確認此動作已不可行。 

1. 在新的瀏覽器視窗中，會再次 toohello hello API 應用程式 URL。
2. 記錄檔中時，提示 toodo。
3. 登入成功，但會導致 tooan 錯誤頁面。
   
    您已設定 hello AAD 應用程式，所以 hello AAD 租用戶中的使用者無法登入，並從瀏覽器存取 hello API。 您仍然可以使用服務主體 token，您可以確認進入 toohello web 應用程式的 URL，並加入更多待辦項目，以存取 hello API 應用程式。

## <a name="restrict-access-tooa-particular-service-principal"></a>限制存取 tooa 特定的服務主體
以滑鼠右鍵，可以為使用者取得權杖的任何呼叫端，或在 Azure AD 租用戶中的服務主體可以呼叫 hello TodoListDataAPI （資料層） API 應用程式。 您可能想 toomake 確定該 hello 資料層應用程式開發介面應用程式只接受呼叫從 hello TodoListAPI （中介層） 應用程式開發介面應用程式，而且是從特定的服務主體。 

您可以加入程式碼 toovalidate hello，以便將這些限制`appid`和`objectidentifier`宣告上的連入呼叫。

本教學課程中，您將會驗證應用程式識別碼，並直接在控制器動作中的服務主體 ID 的 hello 程式碼。  替代方式為 toouse 自訂`Authorize`屬性或 toodo 這項驗證在您啟動序列 （例如 OWIN 中介軟體）。 如需 hello 後面的範例，請參閱[此範例應用程式](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs)。 

請遵循變更 toohello TodoListDataAPI 專案 hello。

1. 開啟 hello *Controllers/TodoListController.cs*檔案。
2. 設定的 hello 行取消註解`trustedCallerClientId`和`trustedCallerServicePrincipalId`。
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. 取消註解 hello hello CheckCallerId 方法中的程式碼。 這個方法是在 hello 開始 hello 控制器中的每個動作方法的呼叫。 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. 重新部署 hello ToDoListDataAPI 專案 tooAzure 應用程式服務。
5. 在瀏覽器中前往 toohello AngularJS 前端 web 應用程式的 HTTPS URL，並在 hello 首頁上，按一下 [hello **tooDo 清單**] 索引標籤。
   
    hello 應用程式不會運作，因為回 toohello 結尾的呼叫失敗。 hello 新的程式碼會檢查實際 appid 和 objectidentifier，但它還沒有 hello 正確值 toocheck 針對它們。 hello 瀏覽器開發人員工具主控台會報告該 hello 伺服器傳回 HTTP 401 錯誤。
   
    ![開發人員工具主控台中發生錯誤](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    Hello 步驟中，您會設定 hello 預期的值。
6. 使用 Azure AD PowerShell 時，取得 hello 值 hello 服務主體的 hello hello TodoListWebApp 專案建立的 Azure AD 應用程式。
   
    a. 如需有關指示 tooinstall Azure PowerShell 及連接 tooyour 訂用帳戶，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。
   
    b. 服務主體清單 tooget 執行 hello`Login-AzureRmAccount`命令，然後 hello`Get-AzureRmADServicePrincipal`命令。
   
    c. 找到 hello objectid hello TodoListAPI 應用程式的服務主體，並將它儲存在您可以從複製稍後的位置。
7. 在 hello Azure 入口網站，瀏覽 toohello hello API 應用程式部署至 hello ToDoListDataAPI 專案的應用程式開發介面應用程式刀鋒視窗。
8. 按一下 [設定] > [應用程式設定]。
9. 在 hello**應用程式設定**區段中，加入下列的 hello 索引鍵和值：
   
   | **金鑰** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **值** |呼叫端應用程式的服務主體識別碼 |
   | **範例** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **金鑰** | todo:TrustedCallerClientId |
   | --- | --- |
   | **值** |呼叫應用程式-複製從 hello TodoListAPI Azure AD 應用程式的用戶端識別碼 |
   | **範例** |960adec2-b74a-484a-960adec2-b74a-484a |
10. 按一下 [儲存] 。
    
     ![按一下 [Save] \(儲存)。](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. 在瀏覽器中傳回 toohello web 應用程式的 URL，然後在 hello 首頁上，按一下 hello **tooDo 清單** 索引標籤。
    
     此時間 hello 應用程式可以正常運作因為 hello 信任的呼叫端應用程式識別碼和服務主體識別碼 hello 預期的值。
    
     ![tooDo 清單頁面](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>建置從頭 hello 專案
hello 兩個 Web API 專案所建立的 hello **Azure API 應用程式**專案範本和取代 hello 預設值的控制站與 ToDoList 控制站。 取得 Azure AD 服務主體語彙基元 hello ToDoListAPI 專案中的，hello [Active Directory 驗證程式庫 (ADAL) for.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/)已安裝 NuGet 套件。

如需太建立 AngularJS 單一頁面應用程式類似 ToDoListAngular Web API 後端，請參閱[手上實驗室： 建置單一頁面應用程式 (SPA)，使用 ASP.NET Web API 和 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)。 如需有關資訊 tooadd Azure AD 驗證程式碼，請參閱[保護 AngularJS 單一頁面應用程式與 Azure AD](../active-directory/active-directory-devquickstarts-angular.md)。

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* 請確定不要混淆 ToDoListAPI (中介層) 和 ToDoListDataAPI (資料層)。 例如，本教學課程中您要加入驗證 toohello 資料層應用程式開發介面應用程式， **hello 應用程式金鑰必須來自 hello hello 中介層應用程式開發介面應用程式所建立的 Azure AD 應用程式，但**。

## <a name="next-steps"></a>後續步驟
這是 hello hello API Apps 數列中的最後一個教學課程。 

如需 Azure Active Directory 的詳細資訊，請參閱下列資源的 hello。

* [Azure AD 開發人員指南](http://aka.ms/aaddev)
* [Azure AD 案例](http://aka.ms/aadscenarios)
* [Azure AD 範例](http://aka.ms/aadsamples)
  
    hello [WebApp-WebAPI-OAuth2-[appidentity]-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet)範例是類似 toowhat 會顯示在本教學課程中，但不會使用應用程式服務驗證。

如需其他方式 toodeploy Visual Studio 專案 tooAPI 應用程式，使用 Visual Studio 或[自動化部署](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)從[原始檔控制系統](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)，請參閱[如何 toodeployAzure App Service 應用程式](../app-service-web/web-sites-deploy.md)。

