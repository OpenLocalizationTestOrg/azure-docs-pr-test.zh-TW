hello 步驟 toounregister 處理序伺服器與 hello 伺服器組態及其連接狀態而有所不同。

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>取消註冊處於已連線狀態的處理序伺服器

1. 遠端 hello 處理序伺服器系統管理員身分登入。
2. 啟動 hello**控制台**並開啟**程式 > 解除安裝程式**
3. 解除安裝程式以 hello 名稱**Microsoft Azure 站台復原設定/處理序伺服器**
4. 完成步驟 3 後，您就可以解除安裝 **Microsoft Azure Site Recovery Configuration/Process Server 相依項目**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>取消註冊處於已中斷連線狀態的處理序伺服器

> [!WARNING]
> 如果處理序伺服器已安裝哪些 hello 沒有方法 toorevive hello 虛擬機器，則應該使用下列步驟使用 hello。

1. 系統管理員身分登入 tooyour 組態伺服器。
2. 開啟 系統管理命令提示字元並瀏覽 toohello 目錄`%ProgramData%\ASR\home\svsystems\bin`。
3. 現在執行 hello 命令。

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. 這將從 hello 系統清除 hello hello 處理序伺服器詳細資料。
