## <a name="build-iot-edge"></a><span data-ttu-id="892bc-101">建置 IoT Edge</span><span class="sxs-lookup"><span data-stu-id="892bc-101">Build IoT Edge</span></span>

<span data-ttu-id="892bc-102">本教學課程會使用自訂的 IoT 邊緣模組 toocommunicate 以 hello 遠端監視預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="892bc-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="892bc-103">因此，您必須從自訂來源程式碼 toobuild hello IoT 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="892bc-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="892bc-104">hello 下列各節說明如何建置和 tooinstall IoT 邊緣 hello 自訂 IoT 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="892bc-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="892bc-105">安裝 IoT Edge</span><span class="sxs-lookup"><span data-stu-id="892bc-105">Install IoT Edge</span></span>

<span data-ttu-id="892bc-106">hello 下列步驟說明如何 tooinstall hello 預先編譯上 hello Intel NUC IoT 邊緣軟體：</span><span class="sxs-lookup"><span data-stu-id="892bc-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="892bc-107">設定所需的 hello 智慧封裝儲存機制執行下列命令在 hello Intel NUC hello:</span><span class="sxs-lookup"><span data-stu-id="892bc-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="892bc-108">輸入`y`當 hello 命令會提示您太**包含此通道嗎？**。</span><span class="sxs-lookup"><span data-stu-id="892bc-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="892bc-109">藉由執行下列命令的 hello hello 智慧套件管理員更新：</span><span class="sxs-lookup"><span data-stu-id="892bc-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="892bc-110">執行下列命令的 hello 安裝 hello Azure IoT 邊緣封裝：</span><span class="sxs-lookup"><span data-stu-id="892bc-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="892bc-111">確認執行 hello"Hello world"範例 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="892bc-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="892bc-112">這個範例會寫入 hello world 訊息 toohello.log.txt 檔每五秒。</span><span class="sxs-lookup"><span data-stu-id="892bc-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="892bc-113">hello 執行下列命令 hello"Hello world"範例：</span><span class="sxs-lookup"><span data-stu-id="892bc-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="892bc-114">忽略任何**無效的引數**時停止 hello 範例訊息。</span><span class="sxs-lookup"><span data-stu-id="892bc-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="892bc-115">使用下列命令 tooview hello 內容 hello 記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="892bc-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="892bc-116">疑難排解</span><span class="sxs-lookup"><span data-stu-id="892bc-116">Troubleshooting</span></span>

<span data-ttu-id="892bc-117">如果您收到 hello 錯誤 」 的封裝提供 util-linux 開發人員 」，則試著 hello Intel NUC。</span><span class="sxs-lookup"><span data-stu-id="892bc-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
