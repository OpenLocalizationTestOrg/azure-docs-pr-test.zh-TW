## <a name="build-iot-edge"></a>建置 IoT Edge

本教學課程會使用自訂的 IoT 邊緣模組 toocommunicate 以 hello 遠端監視預先設定的解決方案。 因此，您必須從自訂來源程式碼 toobuild hello IoT 邊緣模組。 hello 下列各節說明如何建置和 tooinstall IoT 邊緣 hello 自訂 IoT 邊緣模組。

### <a name="install-iot-edge"></a>安裝 IoT Edge

hello 下列步驟說明如何 tooinstall hello 預先編譯上 hello Intel NUC IoT 邊緣軟體：

1. 設定所需的 hello 智慧封裝儲存機制執行下列命令在 hello Intel NUC hello:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    輸入`y`當 hello 命令會提示您太**包含此通道嗎？**。

1. 藉由執行下列命令的 hello hello 智慧套件管理員更新：

    ```bash
    smart update
    ```

1. 執行下列命令的 hello 安裝 hello Azure IoT 邊緣封裝：

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. 確認執行 hello"Hello world"範例 hello 安裝。 這個範例會寫入 hello world 訊息 toohello.log.txt 檔每五秒。 hello 執行下列命令 hello"Hello world"範例：

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    忽略任何**無效的引數**時停止 hello 範例訊息。

    使用下列命令 tooview hello 內容 hello 記錄檔的 hello:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>疑難排解

如果您收到 hello 錯誤 」 的封裝提供 util-linux 開發人員 」，則試著 hello Intel NUC。
