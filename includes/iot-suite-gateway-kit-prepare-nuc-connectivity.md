## <a name="prepare-your-intel-nuc"></a>準備您的 Intel NUC

您需要 toocomplete hello 硬體安裝程式：

- 連接 hello 套件中包含您 Intel NUC toohello 電源供應器。
- 連接 Intel NUC tooyour 網路使用乙太網路纜線。

您現在已完成 Intel NUC 閘道裝置 hello 硬體的安裝。

### <a name="sign-in-and-access-hello-terminal"></a>登入及存取 hello 終端機

您有兩個選項 tooaccess 終端機環境 Intel NUC 上：

- 如果您有鍵盤，監視連線的 tooyour Intel NUC，您可以直接存取 hello 殼層。 hello 預設認證是使用者名稱**根**和密碼**根**。

- 從您桌面的電腦使用 SSH 您 Intel NUC 上存取 hello 殼層。

#### <a name="sign-in-with-ssh"></a>使用 SSH 登入

使用 SSH toosign，您需要 Intel NUC hello IP 位址。 如果您有鍵盤，監視連線的 tooyour Intel NUC 使用 hello`ifconfig`命令 toofind hello IP 位址。 或者，連線 tooyour 路由器 toolist hello 位址的網路上的裝置。

以使用者名稱 **root** 和密碼 **root** 登入。

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>選擇性︰共用 Intel NUC 上的資料夾

（選擇性） 您可能想在 Intel NUC tooshare 資料夾與您的桌面環境。 共用資料夾可讓您 toouse 慣用桌面的文字編輯器 (例如[Visual Studio Code](https://code.visualstudio.com/)或[適文字](http://www.sublimetext.com/)) tooedit 檔案而不是使用您 Intel NUC`nano`或`vi`.

tooshare 資料夾，以使用 Windows hello Intel NUC 上設定 Samba 伺服器。 或者，使用 hello SFTP 伺服器 hello Intel NUC 具有 SFTP 用戶端上您桌面的電腦上。
