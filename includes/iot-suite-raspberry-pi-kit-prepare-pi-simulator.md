## <a name="prepare-your-raspberry-pi"></a>準備您的 Raspberry Pi

### <a name="install-raspbian"></a>安裝 Raspbian

如果這是 hello 用覆盆子 Pi 的第一次，您會需要 tooinstall hello Raspbian 使用作業系統 NOOBS hello 套件中包含的 hello SD 卡上。 hello[覆盆子 Pi 軟體指南][ lnk-install-raspbian]描述如何 tooinstall 覆盆子 Pi 上的作業系統。 本教學課程假設您已安裝 hello Raspbian 作業系統覆盆子 pi。

> [!NOTE]
> 包含在 hello hello sd 記憶卡[覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件][ lnk-starter-kits]已經有 NOOBS 安裝。 您可以開機 hello 覆盆子 Pi 從這張介面卡，並選擇 tooinstall hello Raspbian OS。

您需要 toocomplete hello 硬體安裝程式：

- 連接 hello 套件中包含您覆盆子 Pi toohello 電源供應器。
- 您覆盆子 Pi tooyour 的網路連線使用包含在您的套件中的 hello 乙太網路纜線。 或者，您可以為 Raspberry Pi 設定[無線連線能力][lnk-pi-wireless]。

您現在已完成覆盆子 Pi 的 hello 硬體安裝。

### <a name="sign-in-and-access-hello-terminal"></a>登入及存取 hello 終端機

您有兩個選項 tooaccess 終端機環境覆盆子 Pi 上：

- 如果您有鍵盤，監視連線的 tooyour 覆盆子 Pi，您可以使用 hello Raspbian GUI tooaccess 終端機視窗。

- 從您桌面的電腦使用 SSH 您覆盆子 pi hello 命令列存取。

#### <a name="use-a-terminal-window-in-hello-gui"></a>在 hello GUI 中的終端機視窗

Raspbian hello 預設認證是使用者名稱**pi**和密碼**覆盆子**。 您可以在 hello 工作列 hello GUI 中，啟動 hello**終端機**使用 hello 圖示看起來像監視器公用程式。

#### <a name="sign-in-with-ssh"></a>使用 SSH 登入

您可以使用 SSH 的命令列存取 tooyour 覆盆子 Pi。 hello 文章[SSH (Secure Shell)] [ lnk-pi-ssh]描述如何 tooconfigure SSH 您覆盆子 pi，以及如何從 tooconnect [Windows] [ lnk-ssh-windows]或[Linux 和 Mac OS][lnk-ssh-linux]。

以使用者名稱 **pi** 和密碼 **raspberry** 登入。

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>選擇性︰共用 Raspberry Pi 上的資料夾

或者，您可能想覆盆子 pi tooshare 資料夾與您的桌面環境。 共用資料夾可讓您 toouse 慣用桌面的文字編輯器 (例如[Visual Studio Code](https://code.visualstudio.com/)或[適文字](http://www.sublimetext.com/)) tooedit 檔案，而不是使用您覆盆子 pi`nano`或`vi`.

隨 Windows 資料夾 tooshare Samba 上設定伺服器 hello 覆盆子 Pi。 或者，使用內建的 hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) SFTP 用戶端在桌面上的伺服器。

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/