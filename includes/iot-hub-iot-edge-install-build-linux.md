## <a name="install-the-prerequisites"></a><span data-ttu-id="6448c-101">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="6448c-101">Install the prerequisites</span></span>

<span data-ttu-id="6448c-102">本教學課程中的步驟假設您正在執行 Ubuntu Linux。</span><span class="sxs-lookup"><span data-stu-id="6448c-102">The steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="6448c-103">開啟殼層並執行下列命令，來安裝必要條件套件︰</span><span class="sxs-lookup"><span data-stu-id="6448c-103">Open a shell and run the following commands to install the prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="6448c-104">在殼層中，執行下列命令，將 Azure IoT Edge GitHub 存放庫複製到本機電腦：</span><span class="sxs-lookup"><span data-stu-id="6448c-104">In the shell, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="6448c-105">如何建置範例</span><span class="sxs-lookup"><span data-stu-id="6448c-105">How to build the sample</span></span>

<span data-ttu-id="6448c-106">您現在可以在本機電腦上建置 IoT Edge 執行階段和範例：</span><span class="sxs-lookup"><span data-stu-id="6448c-106">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="6448c-107">開啟殼層。</span><span class="sxs-lookup"><span data-stu-id="6448c-107">Open a shell.</span></span>

1. <span data-ttu-id="6448c-108">瀏覽至 **iot-edge** 存放庫的本機複本中的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="6448c-108">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="6448c-109">執行組建指令碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6448c-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="6448c-110">此指令碼使用 **cmake** 公用程式，在 **iot-edge** 存放庫本機複本的根資料夾中建立稱為 **build** 的資料夾，以及產生 Makefile。</span><span class="sxs-lookup"><span data-stu-id="6448c-110">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="6448c-111">此指令碼接著會建置方案，略過單元測試和端對端測試。</span><span class="sxs-lookup"><span data-stu-id="6448c-111">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="6448c-112">如果您想要建置並執行單元測試，請新增 `--run-unittests` 參數。</span><span class="sxs-lookup"><span data-stu-id="6448c-112">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="6448c-113">如果您想要建置並執行端對端測試，請新增 `--run-e2e-tests`。</span><span class="sxs-lookup"><span data-stu-id="6448c-113">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="6448c-114">每次執行 **build.sh** 指令碼時，都會先在 **iot-edge** 存放庫本機複本的根資料夾中刪除再重新建立 **build** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6448c-114">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>