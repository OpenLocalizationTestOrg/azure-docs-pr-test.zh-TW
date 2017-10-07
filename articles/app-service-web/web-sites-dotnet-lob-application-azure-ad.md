---
title: "aaaCreate 業務的 Azure 應用程式與 Azure Active Directory 驗證 |Microsoft 文件"
description: "深入了解如何在 Azure App Service 中 toocreate ASP.NET MVC 的特定業務應用程式，向 Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式
本文章將示範如何 toocreate.NET 的特定業務應用程式中[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)使用 hello[驗證 / 授權](../app-service/app-service-authentication-overview.md)功能。 它也會示範如何 toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery hello 應用程式中的目錄資料。

您使用的 hello Azure Active Directory 租用戶可以是僅 Azure 」 的目錄。 或者，它可以是[與您在內部部署 Active Directory 同步處理](../active-directory/active-directory-aadconnect.md)toocreate 單一登入體驗的內部部署和遠端的背景工作。 本文使用 hello 預設目錄，為您的 Azure 帳戶。

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>將建置的項目
您將建置簡單的特定業務建立讀取更新與刪除 (CRUD) 應用程式，App Service Web 應用程式中追蹤工作項目，以 hello 下列功能：

* 比對 Azure Active Directory 驗證使用者
* 使用 [Azure Active Directory 圖形 API](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* 使用 hello ASP.NET MVC*非驗證*範本

如果您在 Azure 中的企業營運應用程式需要角色型存取控制 (RBAC)，請參閱 [後續步驟](#next)。

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>您需要什麼
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

本教學課程，您需要 hello 下列 toocomplete 中：

* Azure Active Directory 租用戶與不同的群組中的使用者
* Hello Azure Active Directory 租用戶上的權限 toocreate 應用程式
* Visual Studio 2013 Update 4 或更新版本
* [Azure SDK 2.8.1 或更新版本](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>建立及部署 web 應用程式 tooAzure
1. 從 Visual Studio，按一下 [檔案] > [新增] > [專案]。
2. 選取 [ASP.NET Web 應用程式]、為專案命名，然後按一下 [確定]。
3. 選取 hello **MVC**範本，然後變更太 hello 驗證**非驗證**。 請確定**hello 雲端中的主機**已選取並按**確定**。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. 在 hello**建立 App Service**  對話方塊中，按一下**將帳戶加入**(然後**將帳戶加入**hello 下拉式清單中) toolog tooyour Azure 帳戶中的。
5. 登入後，請設定 Web 應用程式。 建立資源群組和新的 App Service 方案，按一下個別的 hello**新增** 按鈕。 按一下**瀏覽其他 Azure 服務**toocontinue。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. 在 hello**服務**索引標籤上，按一下   **+**  tooadd 應用程式的 SQL 資料庫。 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. 在**設定 SQL Database**，按一下 **新增**toocreate SQL Server 執行個體。
8. 在 [設定 SQL Server] 中，設定 SQL Server 執行個體。 然後按一下  **確定**，**確定**，和**建立**tookick hello Azure 中的應用程式建立功能。
9. 在**Azure 應用程式服務活動**，您可以看到 hello 應用程式建立完成時。 按一下**發行&lt;* appname*> toothis Web 應用程式現在 * *，然後按一下 **發行**。 
   
    一旦完成 Visual Studio 時，它會開啟 hello hello 瀏覽器中發行的應用程式。 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>設定驗證和目錄存取
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從 hello 左窗格中，按一下 **應用程式服務** > **&lt;*appname*> * * >**驗證 / 授權**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. 按一下 [於] > [Azure Active Directory] > [Express] > [確定] 以開啟 Azure Active Directory 驗證。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. 按一下**儲存**hello 命令列中。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    已成功儲存 hello 驗證設定之後, 再試一次巡覽 tooyour 再次 hello 瀏覽器中的應用程式。 您的預設設定強制執行 hello 整個應用程式為基礎的驗證。 如果您沒有已登入，您必須重新導向的 tooa 登入畫面。 登入之後，您會看到應用程式已受到 HTTPS 的保護。 接下來，您需要 tooenable 存取 toodirectory 資料。 
5. 瀏覽 toohello[傳統入口網站](https://manage.windowsazure.com)。
6. 從 hello 左窗格中，按一下  **Active Directory** > **預設目錄** > **應用程式** >   **&lt;* appname*> * *。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    這是您 tooenable hello 授權的建立應用程式服務的 hello Azure Active Directory 應用程式 / 驗證功能。
7. 按一下**使用者**和**群組**toomake 確定 hello 目錄中有某些使用者和群組。 如果沒有，請建立一些測試使用者和群組。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. 按一下**設定**tooconfigure 此應用程式。
9. 捲動 toohello**金鑰**區段，然後選取 持續時間中加入的機碼。 然後按一下 [委派的權限] 並選取 [讀取目錄資料]。 
   按一下 [儲存] 。
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. 在您的設定會儲存後，向上捲動回到 toohello**金鑰**區段，然後按一下 hello**複製**按鈕 toocopy hello 用戶端金鑰。 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > 如果現在離開此頁面，您必須能夠 tooaccess 此用戶端金鑰過一次。
    > 
    > 
11. 接下來，您需要 tooconfigure 您 web 應用程式與這個機碼。 登入 toohello [Azure 資源總管](https://resources.azure.com)與 Azure 帳戶。
12. 在 hello hello 頁面頂端，按一下**讀/寫**toomake hello Azure 資源總管中的變更。
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. 尋找您應用程式中，位於 訂用帳戶的驗證設定 hello >   **&lt;*訂用帳戶名稱*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * >**提供者** > **Microsoft.Web** > **網站** > **&lt;*appname*> * * > **config**  > **authsettings**。
14. 按一下 [ **編輯**]。
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. 在編輯窗格中的 hello，設定 hello`clientSecret`和`additionalLoginParams`，如下所示的屬性。
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. 按一下**放**在 hello 頂端 toosubmit 您的變更。
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. 現在，如果您擁有 hello 授權權杖 tooaccess hello Azure Active Directory Graph API，只要瀏覽至 tootest 才 **https://&lt;*appname*>.azurewebsites.net/.auth/me** 中的您瀏覽器。 如果您的所有項目已正確設定，您應該會看見 hello `access_token` hello JSON 回應中的屬性。
    
    hello `~/.auth/me` URL 路徑受應用程式服務驗證 / 授權 toogive 您所有的 hello 資訊相關 tooyour 驗證工作階段。 如需詳細資訊，請參閱 [Azure App Service 中的驗證與授權](../app-service/app-service-authentication-overview.md)。
    
    > [!NOTE]
    > hello`access_token`具有到期期間。 不過，App Service 驗證/授權會以 `~/.auth/refresh`提供權杖重新整理功能。 如需有關如何 toouse，請參閱[應用程式服務語彙基元存放區](https://cgillum.tech/2016/03/07/app-service-token-store/)。
    > 
    > 

接下來，您會使用目錄資料進行一些有用的操作。

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>新增的業務功能 tooyour 應用程式
現在，您可以建立簡單的 CRUD 工作項目追蹤器。  

1. 在 hello ~\Models 資料夾中，建立一個稱為 WorkItem.cs 的類別檔案，並取代`public class WorkItem {...}`以下列程式碼的 hello:
   
     using System.ComponentModel.DataAnnotations;
   
     public class WorkItem   {
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     public enum WorkItemStatus   {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. 建立 hello 專案 toomake 您新模型存取 toohello scaffolding 邏輯 Visual Studio 中。
3. 加入新的 scaffold 項目`WorkItemsController`toohello ~\Controllers 資料夾 (以滑鼠右鍵按一下**控制器**，點太**新增**，然後選取**新的 scaffold 項目**)。 
4. 選取 [使用 Entity Framework，包含檢視的 MVC 5 控制器]，再按一下 [新增]。
5. 選取 hello 您所建立模型，然後按一下 **+** 然後**新增**tooadd 資料內容，然後按一下**新增**。
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. 在 ~\Views\WorkItems\Create.cshtml （自動 scaffold 項目），尋找 hello `Html.BeginForm` helper 方法，並進行下列反白顯示的變更的 hello:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   請注意，`token`和`tenant`所使用的 hello`AadPicker`物件 toomake Azure Active Directory Graph API 呼叫。 您稍後會新增 `AadPicker` 。     
   
   > [!NOTE]
   > 您也可以取得`token`和`tenant`從用戶端 hello 與`~/.auth/me`，但那是額外的伺服器呼叫。 例如：
   > 
   > $.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });
   > 
   > 
7. 具有相同的變更進行 hello ~ \Views\WorkItems\Edit.cshtml。
8. hello`AadPicker`定義物件的指令碼中，您需要 tooadd tooyour 專案。 Hello ~\Scripts 資料夾上按一下滑鼠右鍵，指向太**新增**，然後按一下**JavaScript 檔案**。 型別`AadPickerLibrary`hello 檔案名稱，然後按一下**確定**。
9. 複製 hello 內容從[這裡](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js)到 ~ \Scripts\AadPickerLibrary.js。
   
   在 hello 指令碼 hello`AadPicker`物件會呼叫[Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch 使用者和群組的比對輸入 hello。  
10. ~\Scripts\AadPickerLibrary.js 也會使用 hello [jQuery UI 自動完成 widget](https://jqueryui.com/autocomplete/)。 因此，您需要 tooadd jQuery UI tooyour 專案。 以滑鼠右鍵按一下專案，然後按一下 [管理 NuGet 套件] 。
11. 在 hello NuGet 套件管理員中，按一下 瀏覽，類型**jquery ui**在 hello 搜尋列中，然後按一下**jQuery.UI.Combined**。
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Hello 右窗格中，按一下 **安裝**，然後按一下 **確定**tooproceed。
13. 開啟 ~\App_Start\BundleConfig.cs 然後進行下列反白顯示的變更的 hello:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    有更多的高效能的方式 toomanage JavaScript 和 CSS 檔案中您的應用程式。 不過，為了簡單起見就得 toopiggyback 上已用的每個檢視載入的 hello 組合。
14. 最後，在 ~ \Global.asax，加入下列一行程式碼 hello hello`Application_Start()`方法。 `Ctrl`+`.`在每個命名的解析錯誤太修正此問題。
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > 您需要這行程式碼，因為 hello 預設 MVC 範本使用<code>[ValidateAntiForgeryToken]</code>上某些 hello 動作裝飾。 因為所描述的 toohello 行為[Brock Allen](https://twitter.com/BrockLAllen)在[MVC 4、 AntiForgeryToken 和宣告](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/)HTTP POST 可能會因為失敗防偽語彙基元驗證：
    > 
    > * Azure Active Directory 不會傳送 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello 防偽語彙基元所需要的預設值。
    > * 如果 Azure Active Directory 與 AD FS 進行同步處理目錄，預設的 hello AD FS 信任不會傳送 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider 宣告，雖然您可以手動設定 AD FS toosend這個宣告中。
    > 
    > `ClaimTypes.NameIdentifies`指定 hello 宣告`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`，Azure Active Directory 並提供它。  
    > 
    > 
15. 現在，發佈您的變更。 以滑鼠右鍵按一下專案，然後按一下 [發佈] 。
16. 按一下**設定**，請確定沒有連線字串 tooyour SQL 資料庫，選取**更新資料庫**toomake hello 為您的模型結構描述變更，然後按一下**發行**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. 在 hello 瀏覽器中，瀏覽 toohttps: / /&lt;*appname*>.azurewebsites.net/workitems，然後按一下**新建**。
18. 按一下 hello **AssignedToName**方塊。 現在您應該可以在下拉式清單中看到 Azure Active Directory 租用戶中的使用者和群組。 您可以輸入 toofilter，或使用 hello`Up`或`Down`索引鍵或按一下 tooselect hello 使用者或群組。 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. 按一下**建立**toosave hello 變更。 然後，按一下 **編輯**hello 建立工作項目 tooobserve hello 相同的行為。

恭喜，您現在已使用目錄存取在 Azure 中執行企業營運應用程式！ 沒有更多您可以使用 hello Graph API 執行。 請參閱 [Azure AD 圖形 API 參考](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)。

<a name="next"></a>

## <a name="next-step"></a>後續步驟
如果您需要以角色為基礎的存取控制 (RBAC) 為您在 azure 中的特定業務應用程式，請參閱[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)的 hello Azure Active Directory 團隊中的範例。 它為您示範如何為 Azure Active Directory 應用程式，tooenable 角色，然後再授權使用者以 hello`[Authorize]`裝飾。

如果您的特定業務應用程式需要存取 tooon 內部部署資料，請參閱[存取內部部署混合式連線使用 Azure App Service 中的資源](web-sites-hybrid-connection-get-started.md)。

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>進一步資源
* [Azure App Service 中的驗證與授權](../app-service/app-service-authentication-overview.md)
* [在 Azure 應用程式中使用內部部署 Active Directory 進行驗證](web-sites-authentication-authorization.md)
* [在 Azure 中使用 AD FS 驗證建立企業營運應用程式](web-sites-dotnet-lob-application-adfs.md)
* [應用程式服務快速地驗證並 hello Azure AD Graph API](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Microsoft Azure Active Directory 範例與文件](https://github.com/AzureADSamples)
* [Azure Active Directory 支援的權杖和宣告類型](http://msdn.microsoft.com/library/azure/dn195587.aspx)
