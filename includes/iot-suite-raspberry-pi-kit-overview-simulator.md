## <a name="overview"></a>概觀

在本教學課程中，您完成下列步驟的 hello:

- 部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。 這個步驟會自動部署並設定多個 Azure 服務。
- 設定您的裝置 toocommunicate 與您的電腦 hello 遠端監視解決方案。
- 更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的模擬的遙測。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。

> [!NOTE]
> 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。

### <a name="required-software"></a>必要的軟體

需要 SSH 用戶端上您 tooremotely 存取 hello 命令列 hello 覆盆子 Pi 您桌面的電腦 tooenable。

- Windows 不包含 SSH 用戶端。 我們建議使用 [PuTTY](http://www.putty.org/)。
- 多數 Linux 散發套件和 Mac OS 包含 hello 命令列 SSH 公用程式。 如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。

### <a name="required-hardware"></a>必要的硬體

桌上型電腦 tooenable 您 tooconnect 遠端 toohello 命令列上 hello 覆盆子 Pi。

[適用於 Raspberry Pi 3 的 Microsoft IoT 入門套件][lnk-starter-kits]或對等的元件。 本教學課程使用下列項目從 hello 套件 hello:

- Raspberry Pi 3
- MicroSD 卡 (具有 NOOBS)
- USB Mini 連接線
- 乙太網路連接線

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/