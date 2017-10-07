---
title: "aaaCreate 具有 AD FS 驗證的特定業務 Azure 應用程式 |Microsoft 文件"
description: "了解如何 toocreate 向的 Azure App Service 中的特定業務應用程式在內部部署 STS。 本教學課程的目標為 hello 內部部署 STS 的 AD FS。"
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>使用 AD FS 驗證建立企業營運 Azure 應用程式
本文章將示範如何 toocreate ASP.NET MVC 的特定業務應用程式中[Azure App Service](../app-service/app-service-value-prop-what-is.md)使用內部[Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)為 hello 身分識別提供者。 您希望 toocreate Azure App Service 中的特定業務應用程式，而您的組織需要離站儲存目錄資料 toobe 時，可以處理此案例中。

> [!NOTE]
> 如需 hello 不同的企業驗證和授權選項的 Azure 應用程式服務的概觀，請參閱[與 Azure 應用程式中的內部部署 Active Directory 驗證](web-sites-authentication-authorization.md)。
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>將建置的項目
您會建立基本的 ASP.NET 應用程式在 Azure App Service Web 應用程式中以 hello 下列功能：

* 根據 AD FS 驗證使用者
* 使用`[Authorize]`tooauthorize 使用者不同的動作
* 在 Visual Studio 中偵錯和發行 tooApp Service Web 應用程式的靜態設定 （一次設定、 偵錯及發行任何時間）  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>您需要什麼
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

本教學課程，您需要 hello 下列 toocomplete 中：

* 內部部署 AD FS 部署 (如 hello 這個教學課程中使用的測試實驗室的端對端逐步解說，請參閱[測試實驗室： 獨立 STS 使用 AD FS （適用於僅限於測試） 的 Azure VM 中](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* 中 AD FS 管理的權限 toocreate 信賴憑證者信任
* Visual Studio 2013 Update 4 或更新版本
* [Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 或更新版本

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>使用特定業務範本的範例應用程式
hello 範例應用程式，在本教學課程， [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet)，hello Azure Active Directory 團隊所建立。 由於 AD FS 支援 WS-同盟，您可以使用它做為範本 toocreate 特定業務應用程式就能輕鬆。 它有下列功能的 hello:

* 使用[WS-同盟](http://msdn.microsoft.com/library/bb498017.aspx)tooauthenticate 與內部部署 AD FS 部署
* 登入和登出功能
* 使用[Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)是 （而不是 Windows Identity Foundation)，其中 hello 未來的 ASP.NET 和更簡單 tooset 進行驗證和授權比 WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>設定 hello 範例應用程式
1. 複製或下載 hello 範例解決方案在[WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour 本機目錄。
   
   > [!NOTE]
   > hello 指示[README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md)告訴您如何 tooset hello 與 Azure Active Directory 的應用程式。 但在本教學課程中，使用 AD FS 進行設定，因此請改為遵循此處 hello 步驟。
   > 
   > 
2. 開啟 hello 方案，然後開啟 hello 中的 [Controllers\AccountController.cs**方案總管] 中**。
   
   您會看見 hello 程式碼只是發出使用 WS-同盟驗證挑戰 tooauthenticate hello 使用者。 所有驗證都是在 App_Start\Startup.Auth.cs 中設定。
3. 開啟 App_Start\Startup.Auth.cs。 在 hello`ConfigureAuth`方法，請注意 hello 行：
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   在 hello OWIN 世界中，此程式碼片段，實際上是 hello 裸機您需要 tooconfigure WS-同盟驗證最小值。 它是更為簡單且更有質感比 WIF，其中 Web.config 會插入 XML 與整個 hello 的地方。 hello 只有您所需要的資訊為 hello 信賴憑證者合作對象的 (RP) 的 AD FS 服務的中繼資料檔中的識別項和 hello URL。 以下是範例：
   
   * RP 識別碼： `https://contoso.com/MyLOBApp`
   * 中繼資料位址：`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. 在 App_Start\Startup.Auth.cs，來變更下列靜態字串定義 hello:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. 現在，在 Web.config 中請 hello 相對應的變更。開啟 hello Web.config 並修改下列應用程式設定的 hello:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   填滿根據個別環境的 hello 機碼值。
6. 建置應用程式 hello toomake，確定沒有任何錯誤。

就這麼簡單。 Hello 範例應用程式已準備好 toowork 與 AD FS。 您仍然需要 tooconfigure RP trust，稍後在 AD FS 中此應用程式。

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>部署 hello 範例應用程式 tooAzure App Service Web 應用程式
在這裡，您發行 hello 應用程式 tooa web 應用程式在 App Service Web 應用程式中同時保留 hello 偵錯環境。 請注意，您將 toopublish hello 應用程式之前，驗證仍無法運作尚未有與 AD FS RP trust。 不過，如果您這樣做現在您可以有您可以稍後使用 tooconfigure hello RP trust hello web 應用程式 URL。

1. 以滑鼠右鍵按一下專案，然後選取 [發佈] 。
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. 選取 [ **Microsoft Azure App Service**]。
3. 如果您尚未 tooAzure 中，按一下**登入**hello Microsoft 帳戶以用於您的 Azure 訂用帳戶 toosign 中。
4. 一旦登入，請按一下**新增**toocreate web 應用程式。
5. 填寫所有必要欄位。 您即將 tooconnect tooon 內部部署資料更新版本中，因此不會建立此 web 應用程式資料庫。
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. 按一下 [建立] 。 一旦建立 hello web 應用程式時，會開啟 hello 發行 Web 對話方塊。
7. 在**目的地 URL**，變更**http**太**https**。 複製 hello 整個 URL tooa 文字編輯器以供稍後使用。 然後按一下 [發佈] 。
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. 在 Visual Studio 中，開啟專案中的 **Web.Release.config** 。 插入下列 XML 到 hello hello`<configuration>`標記，並以發行 web 應用程式的 URL 取代 hello 索引鍵值。  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

當您完成時，您有兩個 RP 識別項在您的專案，一個用於您在 Visual Studio 中的偵錯環境中設定，一個用於 hello 發行 web 應用程式在 Azure 中。 您會設定 RP trust 每個 AD FS 中的 hello 兩個環境。 偵錯期間，在 Web.config 中的 hello 應用程式設定為使用的 toomake 您**偵錯**與 AD FS 組態工作。 發行時 (根據預設，hello**發行**發行組態)，已轉換的 Web.config 上傳，其中包含 Web.Release.config hello 應用程式設定變更。

如果您想 tooattach hello 已發佈的 web 應用程式 Azure toohello 偵錯工具 （也就是您必須上傳 hello 已發佈的 web 應用程式中的程式碼的偵錯符號），您可以建立複本的 hello 偵錯組態 azure 偵錯，但與它自己的自訂 Web.config 轉換 （例如 Web.AzureDebug.config)，會使用從 Web.Release.config hello 應用程式設定。這可讓您 toomaintain 靜態設定 hello 不同環境下。

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>在 AD FS 管理中設定信賴憑證者信任
現在您需要 tooconfigure RP 中信任 AD FS 管理，才能使用的範例應用程式和實際使用 AD FS 驗證。 您必須設定兩個不同的 RP 信任 tooset 偵錯環境，一個已發行的 web 應用程式。

> [!NOTE]
> 請確定您重複下列步驟，這兩個環境的 hello。
> 
> 

1. 在您的 AD FS 伺服器上的認證登入具有管理 rights tooAD FS。
2. 開啟 [AD FS 管理]。 以滑鼠右鍵按一下 [AD FS]\[信任的關係]\[信賴憑證者信任]，然後選取 [新增信賴憑證者信任]。
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. 在 hello**選取資料來源**頁面上，選取**手動輸入 hello 信賴憑證者的合作對象相關資料**。 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. 在 hello**指定顯示名稱**頁面上，輸入 hello 應用程式的顯示名稱，然後按一下**下一步**。
5. 在 hello**選擇通訊協定**頁面上，按一下**下一步**。
6. 在 hello**設定憑證**頁面上，按一下**下一步**。
   
   > [!NOTE]
   > 由於您應該已在使用 HTTPS，因此可選擇是否使用加密的權杖。 如果您真的想 tooencrypt 語彙基元從這個頁面上的 AD FS，您也必須在程式碼中，將權杖解密的邏輯。 如需詳細資訊，請參閱 [手動設定 OWIN WS-同盟中介軟體和接受加密權杖](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)。
   > 
   > 
7. 在移動到 hello 下一個步驟之前，您需要一段資訊從您的 Visual Studio 專案。 在 hello 專案屬性中，記下 hello **SSL URL** hello 應用程式。 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. 在 AD FS 管理，請在 hello**設定 URL**頁面 hello**新增信賴憑證者信任精靈**，選取**啟用 hello WS-同盟被動式通訊協定的支援**和輸入您記下 hello 上一個步驟中 hello Visual Studio 專案的 SSL URL。 然後按 [下一步] 。
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL 指定 toosend hello 用戶端，在驗證後的成功的位置。 Hello 偵錯環境中，它應該是<code>https://localhost:&lt;port&gt;/</code>。 Hello 已發佈的 web 應用程式中，它應該是 hello web 應用程式 URL。
   > 
   > 
9. 在 hello**設定識別碼**頁面上，確認已列出 您的專案 SSL URL，然後按一下**下一步**。 按一下**下一步**所有 hello 方式 toohello 結尾 hello 精靈預設選取項目。
   
   > [!NOTE]
   > 在 Visual Studio 專案 App_Start\Startup.Auth.cs，這個識別碼比對 hello 值<code>WsFederationAuthenticationOptions.Wtrealm</code>期間同盟驗證。 根據預設，hello 先前步驟中的 hello 應用程式的 URL 會加入做為 RP 識別項。
   > 
   > 
10. 您現在已經完成設定 AD FS 中的 hello RP 應用程式專案。 接下來，您可以設定此應用程式 toosend hello 應用程式所需的宣告。 hello**編輯宣告規則**對話方塊預設會開啟為您在 hello hello 精靈結尾處，您可以立即啟動。 讓我們設定至少 hello 下列宣告 （使用括號括住的結構描述）：
    
    * ASP.NET toohydrate 所使用的名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)- `User.Identity.Name`。
    * 使用者主要名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn)-使用 toouniquely 識別 hello 組織中的使用者。
    * 可以搭配群組成員資格與角色 (http://schemas.microsoft.com/ws/2008/06/identity/claims/role)-`[Authorize(Roles="role1, role2,...")]`裝飾 tooauthorize 控制器/動作。 事實上，這種方法可能不是 hello 進行角色授權的最高效能。 如果您的 AD 使用者所屬的安全性群組 toohundreds，它們就會變成數百個 hello SAML 權杖中的角色宣告。 另一個方法是的 toosend 單一角色宣告有條件地根據特定群組中的 hello 使用者的成員資格。 不過，我們會在本教學課程中簡化該作業。
    * 名稱識別碼 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - 可用於防偽驗證。 如需有關如何 toomake 它搭配防偽驗證的詳細資訊，請參閱 hello**新增的業務功能**區段[建立業務的 Azure 應用程式與 Azure Active Directory 驗證](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > hello 宣告類型與您需要 tooconfigure，您的應用程式由應用程式的需求。 Hello 清單中的 Azure Active Directory 應用程式 （亦即 RP 的信任） 支援的宣告，例如，請參閱[支援權杖和宣告類型](http://msdn.microsoft.com/library/azure/dn195587.aspx)。
    > 
    > 
11. 在 hello 編輯宣告規則 對話方塊中，按一下 **加入規則**。
12. 設定名稱、 UPN 和角色宣告的 hello hello 螢幕擷取畫面所示，按一下**完成**。
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    接下來，您建立暫時性的名稱識別碼宣告中使用 hello 步驟示範[SAML 判斷提示中的名稱識別項](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)。
13. 再按一下 [新增規則]  。
14. 選取 [使用自訂規則傳送宣告] 並按 [下一步]。
15. 貼上 hello 下列規則語言到 hello**自訂規則** 方塊中，名稱 hello 規則**每個工作階段識別碼**按一下**完成**。  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    您的自訂規則看起來應該類似下列螢幕擷取畫面︰
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. 再按一下 [新增規則]  。
17. 選取 [傳輸傳入宣告] 並按 [下一步]。
18. （使用您建立 hello 自訂規則中的 hello 宣告型別） 的 hello 螢幕擷取畫面所示設定 hello 規則，按一下**完成**。
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Hello 暫時性名稱識別碼宣告 hello 步驟的詳細資訊，請參閱[SAML 判斷提示中的名稱識別項](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)。
19. 按一下**套用**在 hello**編輯宣告規則**對話方塊。 它現在應該看起來像下列螢幕擷取畫面的 hello:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > 同樣地，請確定為偵錯環境和已發行的 Web 應用程式重複這些步驟。
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>測試應用程式的同盟驗證
您已準備好 tootest 針對 AD FS 的應用程式的驗證邏輯。 在我 AD FS 實驗室環境中，我有所屬 tooa 測試群組在 Active Directory (AD) 的測試使用者。

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

在 hello 偵錯工具，現在您只需要 toodo tootest 驗證是型別`F5`。 如果您想 tootest 驗證 hello 已發佈的 web 應用程式中，瀏覽 toohello URL。

Hello web 應用程式載入之後，請按一下**登入**。 您現在應該取得登入對話方塊或 hello 登入頁面由 AD FS 中，根據選擇的 AD FS 的 hello 驗證方法。 以下是我在 Internet Explorer 11 中看到的畫面。

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

一旦您登入的 hello AD FS 部署的 hello AD 網域中的使用者，您現在應該會看到一次與 hello 首頁**Hello， <User Name>！** hello 角。 以下是我看到的內容。

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

目前為止，您已經成功地 hello 下列方法：

* 您的應用程式已順利達到 AD FS，並且在 hello AD FS 資料庫中找到相符的 RP 識別項
* AD FS 已成功驗證的 AD 使用者和重新導向回 toohello 應用程式的首頁
* 做為已成功傳送的嗨名稱的 AD FS 的宣告 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour 應用程式中，由該 hello 使用者 hello 事實 hello 角會顯示名稱。 

如果遺失 hello 名稱宣告，您應該會看到**Hello，！**。 如果您看一下 _layout.cshtml\_LoginPartial.cshtml，您會發現它會使用`User.Identity.Name`toodisplay hello 使用者名稱。 如前所述，如果 hello 名稱宣告 hello 驗證的使用者可在 hello SAML 權杖中，ASP.NET hydrates 與其這個屬性。 所有 hello 的 toosee 宣告傳送由 AD FS 在 hello，將中斷點放在 Controllers\HomeController.cs，索引動作方法。 Hello 使用者經過驗證之後，檢查 hello`System.Security.Claims.Current.Claims`集合。

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>授權使用者使用特定的控制器或動作
因為您要加入群組成員資格做為角色宣告您 RP 信任設定，您現在可以使用它們直接在 hello`[Authorize(Roles="...")]`裝飾控制器和動作。 在 hello 建立讀取更新與刪除 (CRUD) 模式的特定業務應用程式，您可以授權特定角色 tooaccess 每個動作。 現在，您將只試用 hello 現有主控制器上的這項功能。

1. 開啟 Controllers\HomeController.cs。
2. 裝飾 hello`About`和`Contact`動作方法類似 toohello 下列程式碼，請使用您已驗證的使用者具有的安全性群組成員資格。  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    因為我加入**測試使用者**太**測試群組**我將我的 AD FS 實驗室環境中使用測試群組 tootest 授權上`About`。 如`Contact`，測試 hello 負的大小寫**Domain Admins**，toowhich**測試使用者**不屬於。
3. 輸入啟動 hello 偵錯工具`F5`並登入，然後按一下 **有關**。 您應該立即檢視 hello`~/About/Index`頁面成功，如果您已驗證的使用者已獲得授權，該動作。
4. 現在按一下**連絡人**，其在這個案例中應該不會授權**測試使用者**hello 動作。 不過，hello 瀏覽器會重新導向的 tooAD FS，最後會顯示此訊息：
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    如果您要調查 hello AD FS 伺服器上的事件檢視器中此錯誤，您會看到這個例外狀況訊息：  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    hello 這個錯誤的原因是根據預設，MVC 會傳回 401 未授權時未獲授權的使用者角色。 這會觸發重新驗證要求 tooyour 身分識別提供者 (AD FS)。 AD FS hello 使用者已經過驗證，因為傳回 toohello 相同頁面上，然後發出另一個 401，建立重新導向迴圈。 您將會覆寫 AuthorizeAttribute 的`HandleUnauthorizedRequest`具有簡單的邏輯 tooshow 方法而不是持續的 hello 重新導向迴圈有意義的項目。
5. 呼叫 AuthorizeAttribute.cs，並貼上下列程式碼中的 hello hello 專案中建立的檔案。
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    hello 覆寫程式碼傳送 HTTP 403 （禁止） 而不是 HTTP 401 （未經授權） 中已驗證，但未經授權的情況。
6. Hello 偵錯工具使用，然後再次執行`F5`。 現在按一下 [連絡人]  會顯示更具參考性的 (雖然不討喜) 錯誤訊息：
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. 同樣地，發行 hello 應用程式 tooAzure App Service Web 應用程式，並測試 hello hello 即時應用程式行為。

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Tooon 內部部署資料連接
您會想 tooimplement 特定業務應用程式與 AD FS，而不是 Azure Active Directory 的原因，是保持組織資料外部部署的相容性問題。 這也表示您在 Azure 中的 web 應用程式必須存取內部部署資料庫，因為不允許 toouse [SQL Database](/services/sql-database/)做為您的 web 應用程式的 hello 資料層。

Azure App Service Web Apps 可透過兩種方式支援存取內部部署資料庫：[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和[虛擬網路](web-sites-integrate-with-vnet.md)。 如需詳細資訊，請參閱 [使用 VNET 整合和混合式連線搭配 Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)。

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>進一步資源
* [在 Azure 應用程式中使用內部部署 Active Directory 進行驗證](web-sites-authentication-authorization.md)
* [使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式](web-sites-dotnet-lob-application-azure-ad.md)
* [使用 Visual Studio 2013 中的 hello 與 ASP.NET 在內部部署組織的驗證選項 (ADFS)](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [移轉 VS2013 Web 專案從 WIF tooKatana](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Active Directory Federation Services 概觀](http://technet.microsoft.com/library/hh831502.aspx)
* [WS-同盟 1.1 規格](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

