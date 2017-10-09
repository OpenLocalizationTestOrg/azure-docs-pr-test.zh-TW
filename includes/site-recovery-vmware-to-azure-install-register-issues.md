
### <a name="installation-failures"></a>安裝失敗
| **範例錯誤訊息** | **建議的動作** |
|--------------------------|------------------------|
|錯誤失敗 tooload 帳戶。 錯誤： System.IO.IOException： 安裝及註冊 hello CS 伺服器時，無法 tooread hello 資料傳輸連線。| 請確定 hello 電腦上已啟用 TLS 1.0。 |

### <a name="registration-failures"></a>註冊失敗
註冊失敗，可以藉由檢閱 hello hello 中的記錄檔偵錯**%ProgramData%\ASRLogs**資料夾。

| **範例錯誤訊息** | **建議的動作** |
|--------------------------|------------------------|
|**09:20:06**：InnerException.Type: SrsRestApiClientLib.AcsException,InnerException。<br>訊息︰ACS50008：SAML 權杖無效。<br>追蹤識別碼︰1921ea5b-4723-4be7-8087-a75d3f9e1072<br>相互關聯識別碼︰62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>時間戳記︰**2016-12-12 14:50:08Z<br>** | 請在您的系統時鐘的 hello 時間不超過 15 分鐘關閉 hello 本地時間。 重新執行 hello installer toocomplete hello 註冊。|
|**09:35:27** ： 在嘗試 tooget 所有 hello 選憑證的災害復原保存庫 DRRegistrationException:: 擲回 Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException、 Exception.Message:ACS50008: SAML 權杖無效。<br>追蹤識別碼︰e5ad1af1-2d39-4970-8eef-096e325c9950<br>相互關聯識別碼︰abe9deb8-3e64-464d-8375-36db9816427a<br>時間戳記︰**2016-05-19 01:35:39Z**<br> | 請在您的系統時鐘的 hello 時間不超過 15 分鐘關閉 hello 本地時間。 重新執行 hello installer toocomplete hello 註冊。|
|06:28:45： 失敗的 toocreate 憑證<br>06:28:45：安裝程式無法繼續。 無法建立復原 tooauthenticate tooSite 需要憑證。 重新執行安裝程式 | 確定您是以本機系統管理員身分執行安裝程式。 |
