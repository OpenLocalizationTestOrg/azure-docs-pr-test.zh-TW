> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>簡介

在[開始使用 IoT 中樞裝置雙][lnk-twin-tutorial]，您學會如何從您的方案回 tooset 裝置中繼資料結束使用*標記*，報告裝置從裝置的應用程式的條件使用*報告屬性*，及查詢使用類似 SQL 的語言的這個資訊。

在此教學課程中，您將學習如何 toouse hello hello 裝置兩個的*所需屬性*連同*報告屬性*，tooremotely 設定裝置的應用程式。 更具體來說，本教學課程示範如何報告裝置兩個，而且想要的屬性啟用多重步驟的組態裝置應用程式，並將跨所有裝置提供 hello 可視性 toohello 方案後端的 hello 的這項作業的狀態。 您可以找到裝置組態中的 hello 角色的更多關於[裝置管理概觀與 IoT 中樞][lnk-dm-overview]。

在高層級，使用裝置雙可讓 hello 方案後端 toospecify hello 所需的設定 hello 受管理的裝置，而不是傳送特定的命令。 這會使 hello 裝置負責設定最佳的方式 tooupdate hello 其組態 （其中特定裝置的條件會影響特定命令的 hello 能力 tooimmediately 攜帶 IoT 案例中很重要），同時持續報告 toohello傳回方案結束 hello 目前狀態和潛在的錯誤狀況的 hello 更新程序。 此模式是狀態的很有幫助 toohello 管理大量的裝置，在所有裝置上啟用 hello 方案後端 toohave 完整的可見性 hello hello 設定程序。

> [!NOTE]
> 在裝置是以更為互動的方式控制的案例中 (從使用者控制的應用程式開啟風扇)，請考量使用[直接方法][lnk-methods]。
> 
> 

在本教學課程，hello 方案後端變更 hello 遙測組態的目標裝置，以及因 hello 裝置應用程式，而會遵循多步驟程序 tooapply 組態更新 （例如需要軟體模組重新啟動，這個教學課程會模擬具有簡單的延遲）。

hello 方案後端儲存 hello 組態 hello 裝置兩個的所需的屬性中 hello 下列方式,：

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
> 組態可能很複雜的物件，因為它們通常會指派唯一識別碼 (雜湊或[Guid][lnk-guid]) toosimplify 其比較。
> 
> 

hello 裝置應用程式會報告其目前組態鏡像 hello 預期屬性**telemetryConfig** hello 中報告的屬性：

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

請注意如何 hello 報告**telemetryConfig**有額外的屬性**狀態**，使用 tooreport hello 狀態 hello 組態更新程序。

當收到新所需的組態時，hello 裝置應用程式會報告暫止的組態變更 hello 資訊：

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

然後，在稍後，hello 裝置應用程式將會報告 hello 成功或失敗的這項作業藉由更新 hello 屬性上方。
請注意如何 hello 方案後端，在任何時候，tooquery hello hello 組態處理序狀態之所有 hello 裝置上。

本教學課程說明如何：

* 建立模擬的裝置應用程式的組態更新接收 hello 方案後端，並將報告做為多個更新*報告屬性*hello 組態上的更新程序。
* 建立後端應用程式更新 hello 的裝置，所需的組態，然後查詢 hello 組態更新程序。

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
