大部分的 hello 階段驗證錯誤是因為不正確或不一致的組態設定。 以下是一些特定建議事項 toocheck。

* 請確定您未遺漏 hello**儲存**按鈕任何地方。 這通常是容易的 toodo 和 hello 結果是您將在入口網站上討論的 hello 正確的值，但它們實際上尚未儲存在 hello Azure 環境或 Azure AD 應用程式。
* Hello 中設定的**應用程式設定**刀鋒視窗中的 hello Azure 入口網站，請確定該 hello 正確 API 應用程式或 web 應用程式時，選取輸入 hello 設定。  也確認 hello 設定已輸入為**應用程式設定**而非**連接字串**，hello 兩個區段的 hello 格式會類似如下。
* 驗證 tooa JavaScript 前端，下載 hello 資訊清單再次 tooverify，`oauth2AllowImplicitFlow`已成功變更太`true`。
* 確認您在設定 URL 的位置都是使用 HTTPS：
  
  * 在專案程式碼中
  * 在 CORS 中
  * 在每個 API 應用程式和 Web 應用程式的 Azure 環境應用程式設定中
  * 在 Azure AD 應用程式設定中。
    
    請注意，如果您從 hello 入口網站複製 API 應用程式的 URL，其通常`http://`，而且您有 toomanually 變更嗎`https://`。
* 請確定已成功部署任何程式碼變更。 例如，在多專案方案中很可能 toochange 專案的程式碼，並不小心選擇其中一個 hello 其他您想 toodeploy hello 變更時。
* 請確定您將 tooHTTPS Url 在瀏覽器中不是 HTTP Url。 根據預設，Visual Studio 會建立發行設定檔與 HTTP Url，而這就是您部署專案後，功能開啟 hello 瀏覽器中。
* 驗證 tooa JavaScript 前端，請確定在 hello JavaScript 程式碼會呼叫 hello API 應用程式已正確設定 CORS。 關於 hello 問題是否 CORS 相關的不確定，請再試一次 「 *"與 hello 允許原始 URL。 
* JavaScript 前端，開啟瀏覽器的開發人員工具主控台 索引標籤 tooget 錯誤更多資訊，並檢查 hello 網路上的 HTTP 要求。 不過，主控台錯誤訊息可能會產生誤導。 如果您收到訊息，指出 CORS 錯誤，hello 真正的問題可能會驗證。 您可以檢查是否使用暫時暫時停用的驗證執行 hello 應用程式為 hello 情況。
* .NET API 應用程式中，確定您取得的資訊，錯誤訊息中儘可能藉由設定[customErrors 模式 tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview)。
* .NET API 應用程式中，啟動[遠端偵錯工作階段](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)，並檢查 hello 傳遞使用 ADAL tooacquire toocode hello 變數值的持有者權杖或程式碼，檢查宣告針對預期的 hello 服務主體的識別碼。 請注意，您的程式碼就可以收取組態值從許多不同來源，因此您很可能 toofind 意外這種方式。 例如，如果您打錯`ida:ClientId`為`ida:ClientID`hello 程式碼時設定 Azure App Service 環境設定時，可能會收到 hello `ida:ClientId` hello Web.config 檔案，忽略 hello Azure 應用程式服務設定中尋找的值。 
* 如果無法在正常的 Internet Explorer 視窗中運作，現有的登入可能會產生干擾；請嘗試 InPrivate 並嘗試使用 Chrome 或 Firefox。

