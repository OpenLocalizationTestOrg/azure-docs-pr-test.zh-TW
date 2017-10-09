## <a name="install-hello-prerequisites"></a><span data-ttu-id="fad3d-101">安裝必要的 hello</span><span class="sxs-lookup"><span data-stu-id="fad3d-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="fad3d-102">安裝 [Visual Studio 2015 或 2017](https://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="fad3d-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="fad3d-103">您可以使用 hello 釋放 Community Edition，如果您符合 hello 授權需求。</span><span class="sxs-lookup"><span data-stu-id="fad3d-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="fad3d-104">為確定 tooinclude Visual c + + 和 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="fad3d-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="fad3d-105">安裝[git](http://www.git-scm.com) ，並確定您可以從 hello 命令列執行 git.exe。</span><span class="sxs-lookup"><span data-stu-id="fad3d-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="fad3d-106">安裝[CMake](https://cmake.org/download/) ，並確定您可以從 hello 命令列執行 cmake.exe。</span><span class="sxs-lookup"><span data-stu-id="fad3d-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="fad3d-107">建議使用 CMake 3.7.2 版本或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fad3d-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="fad3d-108">hello **.msi**安裝程式是在 Windows 上的 hello 最簡單選項。</span><span class="sxs-lookup"><span data-stu-id="fad3d-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="fad3d-109">新增 CMake toohello 路徑至少 hello 目前的使用者，當 hello 安裝程式會提示您。</span><span class="sxs-lookup"><span data-stu-id="fad3d-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="fad3d-110">安裝 [Python 2.7](https://www.python.org/downloads/release/python-27)。</span><span class="sxs-lookup"><span data-stu-id="fad3d-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="fad3d-111">請確認您新增 Python tooyour`PATH`中的環境變數**控制台]-> [系統]-> [進階系統設定]-> [環境變數**。</span><span class="sxs-lookup"><span data-stu-id="fad3d-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="fad3d-112">在命令提示字元執行下列命令 tooclone hello Azure IoT 邊緣 GitHub 儲存機制 tooyour 本機電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="fad3d-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="fad3d-113">如何 toobuild hello 範例</span><span class="sxs-lookup"><span data-stu-id="fad3d-113">How toobuild hello sample</span></span>

<span data-ttu-id="fad3d-114">您可以現在會在本機電腦上建置 hello IoT 邊緣執行階段和範例：</span><span class="sxs-lookup"><span data-stu-id="fad3d-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="fad3d-115">開啟「VS 2015 開發人員命令提示字元」或「VS 2017 開發人員命令提示字元」命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="fad3d-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="fad3d-116">瀏覽 toohello hello 的本機複本中的根資料夾**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fad3d-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="fad3d-117">執行組建指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fad3d-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="fad3d-118">此指令碼會建立 Visual Studio 方案檔，並建置 hello 的解決方案。</span><span class="sxs-lookup"><span data-stu-id="fad3d-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="fad3d-119">您可以在 hello 找到 hello Visual Studio 方案**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fad3d-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="fad3d-120">如果您想 toobuild 且執行 hello 單元測試時，新增 hello`--run-unittests`參數。</span><span class="sxs-lookup"><span data-stu-id="fad3d-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="fad3d-121">如果您想 toobuild 且執行 hello 結束 tooend 測試時，新增 hello `--run-e2e-tests`。</span><span class="sxs-lookup"><span data-stu-id="fad3d-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="fad3d-122">每次執行 hello **build.cmd**指令碼，它會刪除，然後重新建立 hello**建置**資料夾中的 hello 根資料夾的本機複本的 hello **iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fad3d-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
