## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>使用保存庫認證 tooauthenticate 以 hello Azure 備份服務
hello 在內部部署伺服器 （Windows 用戶端或 Windows Server 或 Data Protection Manager 的伺服器） 必須先驗證用戶端向備份保存庫可以備份資料 tooAzure toobe。 hello 驗證是使用 「 保存庫認證 」 來達成。 hello 概念保存庫認證是使用 Azure PowerShell 中的 「 發行設定 」 檔案類似 toohello 概念。

### <a name="what-is-hello-vault-credential-file"></a>什麼是 hello 保存庫認證檔案？
hello 保存庫認證檔案是由每個備份保存庫的 hello 入口網站所產生的憑證。 hello 入口網站再上傳 hello 公用金鑰 toohello 存取控制服務 (ACS)。 hello hello 憑證私密金鑰進行可用 toohello 使用者指定做為輸入 hello 機器註冊工作流程中的 hello 工作流程的一部分。 這會驗證 hello 機器 toosend 備份資料 tooan 識別保存庫中 hello Azure 備份服務。

只有在 hello 註冊工作流程期間使用 hello 保存庫認證。 Hello 保存庫認證檔案不會洩露的 hello 使用者的責任 tooensure 它。 它會落在任何惡意使用者的 hello 未授權者手中，如果 hello 保存庫認證檔案可以使用的 tooregister 針對其他機器 hello 相同保存庫。 不過，因為 hello 備份資料已加密的複雜密碼所屬 toohello 客戶，現有的備份資料不會遭到洩漏。 toomitigate 考慮此保存庫認證中所設定 tooexpire 48hrs。 您可以下載 hello 保存庫認證備份保存庫的任何數目的時間 – 但是只有 hello 最新的保存庫認證檔案都適用 hello 註冊工作流程期間。

### <a name="download-hello-vault-credential-file"></a>下載 hello 保存庫認證檔案
透過從 hello Azure 入口網站的安全通道會下載 hello 保存庫認證檔案。 hello Azure 備份服務不會知道 hello hello 憑證私密金鑰和 hello 私密金鑰不會保存在 hello 入口網站或 hello 服務中。 使用下列步驟 toodownload hello 保存庫認證檔案 tooa 本機電腦的 hello。

1. 登入 toohello[管理入口網站](https://manage.windowsazure.com/)
2. 按一下**復原服務**hello 左側的導覽窗格和您建立的選取 hello 備份保存庫中。 按一下 hello 雲端圖示 tooget toohello hello 備份保存庫的快速入門 檢視。
   
   ![快速檢視](./media/backup-download-credentials/quickview.png)
3. 在 hello 快速入門 頁面上，按一下 **下載保存庫認證**。 hello 入口網站會產生 hello 保存庫認證檔案，會成為可供下載。
   
   ![下載](./media/backup-download-credentials/downloadvc.png)
4. hello 入口網站將會產生保存庫認證使用組合的 hello 保存庫名稱和 hello 目前的日期。 按一下**儲存**toodownload hello 保存庫認證 toohello 本機帳戶的下載資料夾中，或從 hello 另存新檔選取儲存功能表 toospecify hello 保存庫認證的位置。

### <a name="note"></a>注意
* 請確定 hello 保存庫認證儲存在可從您的電腦存取的位置。 如果它儲存在檔案共用 SMB，檢查 hello 存取權限。
* 只有在 hello 註冊工作流程會使用 hello 保存庫認證檔案。
* hello 保存庫認證檔案 48hrs 後會到期，而您可以從 hello 入口網站下載。
* 請參閱 toohello Azure Backup[常見問題集](../articles/backup/backup-azure-backup-faq.md)hello 工作流程上的任何問題。

