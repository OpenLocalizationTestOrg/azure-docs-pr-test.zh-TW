UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ i <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < 用於資料傳輸的 IP 位址 toobe] [/CSIP<IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

參數：

* / ServerMode：必要。 指定是否應該安裝這兩個 hello 組態和處理序伺服器，或只 hello 處理序伺服器。 輸入值：CS、PS
* InstallLocation：必要。 元件的安裝中的 hello 的 hello 資料夾。
* /MySQLCredsFilePath。 必要。 hello 檔案路徑中的 hello MySQL server 認證會儲存。 hello 檔案應該是以下列格式：
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath。 必要。 hello hello 保存庫認證檔案位置
* /EnvType。 必要。 hello 安裝類型。 值：VMware、NonVMware
* /PSIP 和 /CSIP。 必要。 hello hello 處理序伺服器和組態伺服器的 IP 位址。
* /PassphraseFilePath。 必要。 hello hello 複雜密碼檔案位置。
* /BypassProxy。 選用。 指定該 hello 設定伺服器連接 tooAzure 不使用 proxy。
* /ProxySettingsFilePath。 選用。 （hello 預設 proxy 需要驗證或自訂的 proxy） 的 proxy 設定。 hello 檔案應該是以下列格式：
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort。 選用。 hello 複寫資料的連接埠號碼。
* SkipSpaceCheck。 選用。 略過快取的空間檢查。
* AcceptThirdpartyEULA。 必要。 接受 hello 協力廠商使用者授權合約。
* ShowThirdpartyEULA。 必要。 顯示協力廠商使用者授權合約。 如果提供作為輸入，則會忽略所有其他參數。
