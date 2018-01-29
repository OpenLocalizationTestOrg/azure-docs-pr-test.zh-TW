## <a name="test-your-code"></a>測試您的程式碼

若要在 Visual Studio 中執行您的專案，請選取 **F5**。 您的應用程式 **MainWindow** 隨即出現，如下所示：

![測試您的應用程式](./media/active-directory-develop-guidedsetup-windesktop-test/samplescreenshot.png)

您第一次執行應用程式並選取 [呼叫 Microsoft Graph API] 按鈕時，系統會提示您登入。 使用 Azure Active Directory 帳戶 (公司或學校帳戶) 或 Microsoft 帳戶 (live.com、outlook.com) 來進行測試。

![登入應用程式](./media/active-directory-develop-guidedsetup-windesktop-test/signinscreenshot.png)

### <a name="provide-consent-for-application-access"></a>同意應用程式存取
您第一次登入應用程式時，系統還會提示您同意允許應用程式存取您的設定檔，並將您登入，如下所示： 

![同意應用程式存取](./media/active-directory-develop-guidedsetup-windesktop-test/consentscreen.png)

### <a name="view-application-results"></a>檢視應用程式結果
登入之後，您應該會看到 Microsoft Graph API 呼叫所傳回的使用者設定檔資訊。 結果即會顯示於 [API 呼叫結果] 方塊中。 在 [權杖資訊] 方塊中，應該顯示透過呼叫 `AcquireTokenAsync` 或 `AcquireTokenSilentAsync` 取得的權杖基本資訊。 結果包含下列屬性：

|屬性  |格式  |說明 |
|---------|---------|---------|
|**名稱** |使用者的全名 |使用者的名字和姓氏。|
|**使用者名稱** |<span>user@domain.com</span> |用來識別使用者的使用者名稱。|
|**權杖到期** |Datetime |權杖的到期時間。 MSAL 會視需要更新權杖來延展到期日。|
|**存取權杖** |字串 |傳送至 HTTP 要求的權杖字串需要授權標頭。|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>與範圍和委派的權限有關的詳細資訊

Microsoft Graph API 需要 user.read 範圍才能讀取使用者的設定檔。 根據預設，在應用程式註冊入口網站註冊的每個應用程式中，都會自動新增此範圍。 Microsoft Graph 的其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。 Microsoft Graph API 需要 Calendars.Read 範圍才能列出使用者的行事曆。

為了在應用程式內容中存取使用者的行事曆，請將 Calendars.Read 委派權限新增至應用程式註冊資訊。 接著，將 Calendars.Read 範圍新增至 `acquireTokenSilent` 呼叫。 

>[!NOTE]
>系統可能會在您增加範圍數目時，提示使用者同意其他事項。

<!--end-collapse-->

[!INCLUDE  [Help and support](./active-directory-develop-help-support-include.md)]
