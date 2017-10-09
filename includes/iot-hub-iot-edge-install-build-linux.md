## <a name="install-hello-prerequisites"></a>安裝必要的 hello

在此教學課程中的 hello 步驟假設您正在 Ubuntu Linux。

開啟命令介面並執行下列命令 tooinstall hello 必要條件套件 hello:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

在 hello 介面中執行下列命令 tooclone hello Azure IoT 邊緣 GitHub 儲存機制 tooyour 本機電腦的 hello:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>如何 toobuild hello 範例

您可以現在會在本機電腦上建置 hello IoT 邊緣執行階段和範例：

1. 開啟殼層。

1. 瀏覽 toohello hello 的本機複本中的根資料夾**iot 邊緣**儲存機制。

1. 執行組建指令碼，如下所示：

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

此指令碼使用**cmake**公用程式 toocreate 資料夾稱為**建置**hello 根資料夾的本機副本中**iot 邊緣**儲存機制，並產生 makefile。 hello 指令碼，然後建置 hello 方案，略過單元測試和結束 tooend 測試。 如果您想 toobuild 且執行 hello 單元測試時，新增 hello`--run-unittests`參數。 如果您想 toobuild 且執行 hello 結束 tooend 測試時，新增 hello `--run-e2e-tests`。

> [!NOTE]
> 每次執行 hello **build.sh**指令碼，它會刪除，然後重新建立 hello**建置**資料夾中的 hello 根資料夾的本機複本的 hello **iot 邊緣**儲存機制。
