以下是 hello 使用限制和其他服務限制 hello Azure Active Directory 服務。

| 類別 | 限制 |
| --- | --- |
| 目錄 |單一使用者最多只能與 20 個 Azure Active Directory 目錄相關聯。<br />可能組合的範例︰ <ul> <li>單一使用者建立 20 個目錄。</li><li>將單一使用者新增 too20 目錄成員。</li><li>單一使用者建立 10 個目錄，稍後再新增其他人所 too10 不同的目錄。</li></ul> |
| 物件 |<ul><li>500,000 個物件最多可在單一目錄中的 hello 免費的 Azure Active Directory 使用者。</li><li>非系統管理員的使用者最多可以建立 250 個物件。</li></ul> |
| 結構描述延伸模組 |<ul><li>字串類型延伸模組最多可有 256 個字元。 </li><li>二進位類型延伸模組是有限的 too256 位元組。</li><li>（跨越所有類型和所有應用程式） 值的 100 個擴充功能可以寫入 tooany 單一物件。</li><li>只能使用「字串」類型或「二進位」類型單一值屬性來擴充 “User”、“Group”、“TenantDetail”、“Device”、“Application” 和 “ServicePrincipal” 實體。</li><li>結構描述延伸模組僅適用於圖形 API 版本 1.21 預覽。 hello 應用程式必須授與的寫入權限 tooregister 擴充功能。</li></ul> |
| 應用程式 |最多 100 個使用者可以成為單一應用程式的擁有者。 |
| 群組 |<ul><li>最多 100 個使用者可以成為單一群組的擁有者。</li><li>任何數目的物件都可以是 Azure Active Directory 中的單一群組的成員。</li><li>您可以從您的內部部署 Active Directory tooAzure Active Directory 同步處理的群組中成員的 hello 數目為有限的 too15K 成員，使用 Azure Active Directory 目錄同步作業 (DirSync)。</li><li>hello 中您可以從您的內部部署 Active Directory tooAzure Active Directory 同步處理群組的成員數目使用 Azure AD Connect 會限制的 too50K 成員。</li></ul> |
| 存取面板 |<ul><li>沒有任何 toohello 數目限制，每名使用者，為使用者指派授權給 Azure AD Premium 或 Enterprise Mobility Suite hello hello 存取面板中，可以看到的應用程式。</li><li>最多 10 個應用程式磚的 (範例： 方塊、 Salesforce 或 Dropbox) hello 存取面板中可以看到每個使用者免費指派授權的使用者或 Azure AD Basic 版本的 Azure Active Directory。 這項限制不適用 tooAdministrator 帳戶。</li></ul> |
| 報告 | 在任何報告中，最多可以檢視或下載 1000 個資料列。 任何其他資料會遭到截斷。 |
| 管理單位 | 物件可以是有不超過 30 個管理單位的成員。 |
