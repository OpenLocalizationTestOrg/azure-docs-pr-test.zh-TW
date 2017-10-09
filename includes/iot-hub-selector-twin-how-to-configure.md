> [!div class="op_single_selector"]
> * [<span data-ttu-id="af6bd-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="af6bd-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="af6bd-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="af6bd-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="af6bd-103">C#</span><span class="sxs-lookup"><span data-stu-id="af6bd-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="af6bd-104">簡介</span><span class="sxs-lookup"><span data-stu-id="af6bd-104">Introduction</span></span>

<span data-ttu-id="af6bd-105">在[開始使用 IoT 中樞裝置雙][lnk-twin-tutorial]，您學會如何從您的方案回 tooset 裝置中繼資料結束使用*標記*，報告裝置從裝置的應用程式的條件使用*報告屬性*，及查詢使用類似 SQL 的語言的這個資訊。</span><span class="sxs-lookup"><span data-stu-id="af6bd-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="af6bd-106">在此教學課程中，您將學習如何 toouse hello hello 裝置兩個的*所需屬性*連同*報告屬性*，tooremotely 設定裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="af6bd-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="af6bd-107">更具體來說，本教學課程示範如何報告裝置兩個，而且想要的屬性啟用多重步驟的組態裝置應用程式，並將跨所有裝置提供 hello 可視性 toohello 方案後端的 hello 的這項作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="af6bd-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="af6bd-108">您可以找到裝置組態中的 hello 角色的更多關於[裝置管理概觀與 IoT 中樞][lnk-dm-overview]。</span><span class="sxs-lookup"><span data-stu-id="af6bd-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="af6bd-109">在高層級，使用裝置雙可讓 hello 方案後端 toospecify hello 所需的設定 hello 受管理的裝置，而不是傳送特定的命令。</span><span class="sxs-lookup"><span data-stu-id="af6bd-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="af6bd-110">這會使 hello 裝置負責設定最佳的方式 tooupdate hello 其組態 （其中特定裝置的條件會影響特定命令的 hello 能力 tooimmediately 攜帶 IoT 案例中很重要），同時持續報告 toohello傳回方案結束 hello 目前狀態和潛在的錯誤狀況的 hello 更新程序。</span><span class="sxs-lookup"><span data-stu-id="af6bd-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="af6bd-111">此模式是狀態的很有幫助 toohello 管理大量的裝置，在所有裝置上啟用 hello 方案後端 toohave 完整的可見性 hello hello 設定程序。</span><span class="sxs-lookup"><span data-stu-id="af6bd-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="af6bd-112">在裝置是以更為互動的方式控制的案例中 (從使用者控制的應用程式開啟風扇)，請考量使用[直接方法][lnk-methods]。</span><span class="sxs-lookup"><span data-stu-id="af6bd-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="af6bd-113">在本教學課程，hello 方案後端變更 hello 遙測組態的目標裝置，以及因 hello 裝置應用程式，而會遵循多步驟程序 tooapply 組態更新 （例如需要軟體模組重新啟動，這個教學課程會模擬具有簡單的延遲）。</span><span class="sxs-lookup"><span data-stu-id="af6bd-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="af6bd-114">hello 方案後端儲存 hello 組態 hello 裝置兩個的所需的屬性中 hello 下列方式,：</span><span class="sxs-lookup"><span data-stu-id="af6bd-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="af6bd-115">組態可能很複雜的物件，因為它們通常會指派唯一識別碼 (雜湊或[Guid][lnk-guid]) toosimplify 其比較。</span><span class="sxs-lookup"><span data-stu-id="af6bd-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="af6bd-116">hello 裝置應用程式會報告其目前組態鏡像 hello 預期屬性**telemetryConfig** hello 中報告的屬性：</span><span class="sxs-lookup"><span data-stu-id="af6bd-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="af6bd-117">請注意如何 hello 報告**telemetryConfig**有額外的屬性**狀態**，使用 tooreport hello 狀態 hello 組態更新程序。</span><span class="sxs-lookup"><span data-stu-id="af6bd-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="af6bd-118">當收到新所需的組態時，hello 裝置應用程式會報告暫止的組態變更 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="af6bd-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="af6bd-119">然後，在稍後，hello 裝置應用程式將會報告 hello 成功或失敗的這項作業藉由更新 hello 屬性上方。</span><span class="sxs-lookup"><span data-stu-id="af6bd-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="af6bd-120">請注意如何 hello 方案後端，在任何時候，tooquery hello hello 組態處理序狀態之所有 hello 裝置上。</span><span class="sxs-lookup"><span data-stu-id="af6bd-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="af6bd-121">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="af6bd-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="af6bd-122">建立模擬的裝置應用程式的組態更新接收 hello 方案後端，並將報告做為多個更新*報告屬性*hello 組態上的更新程序。</span><span class="sxs-lookup"><span data-stu-id="af6bd-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="af6bd-123">建立後端應用程式更新 hello 的裝置，所需的組態，然後查詢 hello 組態更新程序。</span><span class="sxs-lookup"><span data-stu-id="af6bd-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
