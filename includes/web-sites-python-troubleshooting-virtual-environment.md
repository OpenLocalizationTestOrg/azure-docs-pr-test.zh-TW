hello 部署指令碼將會略過建立虛擬環境的 hello Azure 上偵測到相容的虛擬環境已經存在。  這樣做會大幅加速部署。  PIP 將會略過已安裝的封裝。

在某些情況下，您可能想 tooforce 刪除該虛擬環境。  您會想 toodo 這如果您決定 tooinclude 虛擬環境，做為您的儲存機制的一部分。  您也可以 toodo 這如果您需要 tooget 排除特定的封裝，或測試變更 toorequirements.txt。

有幾個選項 toomanage hello 現有 Azure 上的虛擬環境：

### <a name="option-1-use-ftp"></a>選項 1：使用 FTP
使用 FTP 用戶端，toohello 伺服器連接，您將無法 toodelete hello env 資料夾。  請注意，有些 （例如網頁瀏覽器） 的 FTP 用戶端可能處於唯讀模式不允許您 toodelete 資料夾，因此您會想 toomake 確定 toouse FTP 用戶端使用該功能。  hello FTP 主機名稱和使用者會顯示在您的 web 應用程式 刀鋒視窗上 hello [Azure 入口網站](https://portal.azure.com)。

### <a name="option-2-toggle-runtime"></a>選項 2：切換執行階段
以下是利用 hello 部署指令碼，將會不符 hello 所要的 Python 版本刪除 hello env 資料夾 hello 事實的替代方案。  實際上，這將刪除 hello 現有的環境，與另外新建一個。

1. 交換器 tooa 不同版本的 Python (透過 runtime.txt 或 hello**應用程式設定**hello Azure 入口網站中的刀鋒視窗)
2. Git 推送部分變更 (忽略任何 PIP 安裝錯誤 (如果有的話))
3. 切換後 tooinitial Python 版本
4. 再次 Git 推送部分變更

### <a name="option-3-customize-deployment-script"></a>選項 3：自訂部署指令碼
如果您已自訂 hello 部署指令碼，您可以變更 hello 中的程式碼 deploy.cmd tooforce 它 toodelete hello env 資料夾。

