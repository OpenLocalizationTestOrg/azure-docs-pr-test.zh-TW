
## <a name="create-an-application-express"></a>建立應用程式 (快速)
現在您需要在「Microsoft 應用程式註冊入口網站」註冊應用程式：
1. 透過 [Microsoft 應用程式註冊入口網站 (英文)](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure) 註冊您的應用程式
2.  輸入應用程式的名稱和您的電子郵件
3.  確定已選取 [Guided Setup (引導式設定)] 選項
4.  依照指示將重新導向 URL 新增到您的應用程式

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a>將您的應用程式註冊資訊新增到方案 (進階)
現在您需要在「Microsoft 應用程式註冊入口網站」註冊應用程式：
1. 前往 [Microsoft 應用程式註冊入口網站 (英文)](https://apps.dev.microsoft.com/portal/register-app) 註冊應用程式
2. 輸入應用程式的名稱和您的電子郵件 
3.  確定已取消選取 [Guided Setup (引導式設定)] 選項
4.  按一下 `Add Platform`，然後選取 `Web`
5.  回到 Visual Studio，在「方案總管」中，選取專案並查看 [屬性] 視窗 (如果您沒有看到 [屬性] 視窗，請按 F4)
6.  將 [SSL 已啟用] 變更為 `True`
7.  複製 SSL URL 並將這個 URL 新增到註冊入口網站的重新導向 URL 清單：<br/><br/>![專案屬性](media/active-directory-develop-guidedsetup-aspnetwebapp-configure/vsprojectproperties.png)<br />
8.  在位於根資料夾之 `web.config` 的 `configuration\appSettings` 區段下新增下列內容：

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
用您剛剛註冊的應用程式識別碼取代 `ClientId`
</li>
<li>
用您專案的 SSL URL 取代 `redirectUri`
</li>
</ol>
<!-- End Docs -->
