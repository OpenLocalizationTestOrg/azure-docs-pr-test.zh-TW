## <a name="download-install-and-register-hello-azure-backup-agent"></a>下載、 安裝及註冊 hello Azure 備份代理程式
應該在每個資料和應用程式的備份可讓您 Windows 電腦 （Windows Server、 Windows 用戶端、 System Center Data Protection Manager 伺服器或 Azure 備份伺服器的電腦） 上安裝代理程式建立 hello Azure 備份保存庫之後tooAzure。

1. 登入 toohello[管理入口網站](https://manage.windowsazure.com/)
2. 按一下**復原服務**，然後選取您想要與伺服器 tooregister hello 備份保存庫。 該備份保存庫的 hello 快速入門頁面隨即出現。
   
    ![快速入門](./media/backup-install-agent/quickstart.png)
3. 在 hello 快速入門] 頁面上，按一下 [hello**適用於 Windows Server 或 System Center Data Protection Manager 或 Windows 用戶端**選項在**下載代理程式**。 按一下**儲存**toocopy 它 toohello 本機電腦。
   
    ![儲存代理程式](./media/backup-install-agent/agent.png)
4. Hello 代理程式安裝之後，按兩下 MARSAgentInstaller.exe toolaunch hello 安裝 hello Azure Backup agent。 選擇 hello 安裝資料夾和 hello 代理程式所需的臨時資料夾。 指定的 hello 快取位置必須有可用空間可供至少 5%的 hello 備份資料。
5. 如果您使用 proxy 伺服器 tooconnect toohello 網際網路 hello **Proxy 組態**畫面上，輸入 hello proxy 伺服器的詳細資料。 如果您使用驗證的 proxy，請在此畫面輸入 hello 使用者名稱與密碼詳細資料。
6. hello Azure 備份代理程式會安裝 Windows PowerShell 和.NET Framework 4.5 （如果它尚未提供） toocomplete hello 安裝。
7. Hello 代理程式安裝之後，按一下 hello**繼續 tooRegistration**按鈕 toocontinue 與 hello 的工作流程。
   
   ![註冊](./media/backup-install-agent/register.png)
8. 在 [hello 保存庫認證] 畫面上，瀏覽 tooand 選取 hello 保存庫認證檔案先前已下載。
   
    ![保存庫認證](./media/backup-install-agent/vc.png)
   
    hello 保存庫認證檔案無效，只 48 小時 （下載後，從 hello 入口網站）。 如果您遇到此畫面 （例如 「 保存庫認證檔案提供的已到期 」） 中的任何錯誤時，登入 toohello Azure 入口網站並下載 hello 保存庫認證一次的檔案。
   
    確定該 hello 保存庫認證檔案可用在 hello 安裝應用程式可以存取的位置。 如果您遇到存取相關的錯誤，請複製 hello 保存庫認證檔案在這部機器 tooa 暫存位置，然後重試 hello 作業。
   
    如果您遇到無效的保存庫認證錯誤 （例如 「 無效的保存庫認證提供 」） hello 檔案可能已損毀或不具有 hello 最新的認證與服務相關聯 hello 復原。 Hello 作業之後從 hello 入口網站下載新的保存庫認證檔案重試一次。 如果 hello 使用者在 hello，通常會發生這個錯誤**下載保存庫認證**hello 中快速且連續的 Azure 入口網站中的選項。 在此情況下，只有 hello 第二個保存庫認證檔案無效。
9. 在 [hello**加密設定**] 畫面上，您可以產生複雜密碼，或提供複雜密碼 （最少 16 個字元）。 請記住 toosave hello 複雜密碼，在安全的位置。
   
    ![加密](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > 如果 hello 已遺失或忘記複雜密碼。Microsoft 無法協助您復原 hello 備份資料。 hello 終端使用者擁有 hello 加密複雜密碼，且 Microsoft 不會顯示出來 hello hello 終端使用者所使用的複雜密碼。 請視需要執行復原作業時，請在安全的位置儲存 hello 檔案。
   > 
   > 
10. 一旦您按一下 hello**完成**按鈕，hello 電腦註冊成功 toohello 保存庫，您現在已準備好 toostart tooMicrosoft Azure 備份。
11. 使用 Microsoft Azure 備份獨立時，您就可以修改 hello 設定指定 hello 註冊工作流程期間按一下 hello**變更屬性**hello Azure 備份 mmc 嵌入式管理單元中的選項。
    
    ![變更屬性](./media/backup-install-agent/change.png)
    
    或者，當使用 Data Protection Manager，您可以修改 hello 設定指定 hello 註冊工作流程期間按一下 hello**設定**選項選取**線上**下 hello**管理** 索引標籤。
    
    ![設定 Azure 備份](./media/backup-install-agent/configure.png)

