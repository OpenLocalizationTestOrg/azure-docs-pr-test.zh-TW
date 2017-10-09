## <a name="install-hello-prerequisites"></a>安裝必要的 hello

1. 安裝 [Visual Studio 2015 或 2017](https://www.visualstudio.com)。 您可以使用 hello 釋放 Community Edition，如果您符合 hello 授權需求。 為確定 tooinclude Visual c + + 和 NuGet 套件管理員。

1. 安裝[git](http://www.git-scm.com) ，並確定您可以從 hello 命令列執行 git.exe。

1. 安裝[CMake](https://cmake.org/download/) ，並確定您可以從 hello 命令列執行 cmake.exe。 建議使用 CMake 3.7.2 版本或更新版本。 hello **.msi**安裝程式是在 Windows 上的 hello 最簡單選項。 新增 CMake toohello 路徑至少 hello 目前的使用者，當 hello 安裝程式會提示您。

1. 安裝 [Python 2.7](https://www.python.org/downloads/release/python-27)。 請確認您新增 Python tooyour`PATH`中的環境變數**控制台]-> [系統]-> [進階系統設定]-> [環境變數**。

1. 在命令提示字元執行下列命令 tooclone hello Azure IoT 邊緣 GitHub 儲存機制 tooyour 本機電腦的 hello:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>如何 toobuild hello 範例

您可以現在會在本機電腦上建置 hello IoT 邊緣執行階段和範例：

1. 開啟「VS 2015 開發人員命令提示字元」或「VS 2017 開發人員命令提示字元」命令提示字元。

1. 瀏覽 toohello hello 的本機複本中的根資料夾**iot 邊緣**儲存機制。

1. 執行組建指令碼，如下所示：

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

此指令碼會建立 Visual Studio 方案檔，並建置 hello 的解決方案。 您可以在 hello 找到 hello Visual Studio 方案**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。 如果您想 toobuild 且執行 hello 單元測試時，新增 hello`--run-unittests`參數。 如果您想 toobuild 且執行 hello 結束 tooend 測試時，新增 hello `--run-e2e-tests`。

> [!NOTE]
> 每次執行 hello **build.cmd**指令碼，它會刪除，然後重新建立 hello**建置**資料夾中的 hello 根資料夾的本機複本的 hello **iot 邊緣**儲存機制。
