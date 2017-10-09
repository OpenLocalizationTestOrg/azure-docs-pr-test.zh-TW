## <a name="install-hello-prerequisites"></a><span data-ttu-id="c08ba-101">安裝必要的 hello</span><span class="sxs-lookup"><span data-stu-id="c08ba-101">Install hello prerequisites</span></span>

<span data-ttu-id="c08ba-102">在此教學課程中的 hello 步驟假設您正在 Ubuntu Linux。</span><span class="sxs-lookup"><span data-stu-id="c08ba-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="c08ba-103">開啟命令介面並執行下列命令 tooinstall hello 必要條件套件 hello:</span><span class="sxs-lookup"><span data-stu-id="c08ba-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="c08ba-104">在 hello 介面中執行下列命令 tooclone hello Azure IoT 邊緣 GitHub 儲存機制 tooyour 本機電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="c08ba-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="c08ba-105">如何 toobuild hello 範例</span><span class="sxs-lookup"><span data-stu-id="c08ba-105">How toobuild hello sample</span></span>

<span data-ttu-id="c08ba-106">您可以現在會在本機電腦上建置 hello IoT 邊緣執行階段和範例：</span><span class="sxs-lookup"><span data-stu-id="c08ba-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="c08ba-107">開啟殼層。</span><span class="sxs-lookup"><span data-stu-id="c08ba-107">Open a shell.</span></span>

1. <span data-ttu-id="c08ba-108">瀏覽 toohello hello 的本機複本中的根資料夾**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c08ba-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="c08ba-109">執行組建指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c08ba-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="c08ba-110">此指令碼使用**cmake**公用程式 toocreate 資料夾稱為**建置**hello 根資料夾的本機副本中**iot 邊緣**儲存機制，並產生 makefile。</span><span class="sxs-lookup"><span data-stu-id="c08ba-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="c08ba-111">hello 指令碼，然後建置 hello 方案，略過單元測試和結束 tooend 測試。</span><span class="sxs-lookup"><span data-stu-id="c08ba-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="c08ba-112">如果您想 toobuild 且執行 hello 單元測試時，新增 hello`--run-unittests`參數。</span><span class="sxs-lookup"><span data-stu-id="c08ba-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="c08ba-113">如果您想 toobuild 且執行 hello 結束 tooend 測試時，新增 hello `--run-e2e-tests`。</span><span class="sxs-lookup"><span data-stu-id="c08ba-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="c08ba-114">每次執行 hello **build.sh**指令碼，它會刪除，然後重新建立 hello**建置**資料夾中的 hello 根資料夾的本機複本的 hello **iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c08ba-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
