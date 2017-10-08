---
title: "aaaUnderstand Azure IoT Hub 裝置雙 |Microsoft 文件"
description: "開發人員指南-使用裝置雙 toosynchronize IoT 中樞與您的裝置之間的狀態和組態資料"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>了解和使用 Azure IoT 中樞的裝置對應項
## <a name="overview"></a>概觀
「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。 IoT 中樞保存您連接 tooIoT 中樞的每個裝置的裝置兩個。 本文章說明：

* hello 的 hello 裝置兩個結構：*標記*，*所需*和*報告屬性*，和
* hello 裝置應用程式和後端可以雙裝置執行的作業。

> [!NOTE]
> 目前，只連線 tooIoT 中樞的裝置可以存取裝置雙會使用 hello MQTT 通訊協定。 請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。
> 
> 

### <a name="when-toouse"></a>當 toouse
使用裝置對應項可以：

* Hello 雲端中儲存裝置專屬的中繼資料。 例如，hello 販賣的部署位置。
* 從您的裝置應用程式報告目前狀態資訊，例如可用功能和狀況。 例如，裝置是已連線的 tooyour IoT 中樞 over 行動電話通訊或 Wi-fi。
* 同步處理裝置應用程式與後端應用程式之間的長時間執行工作流程的 hello 的狀態。 比方說，當 hello 方案回結束指定 hello 新的韌體版本 tooinstall，和 hello 裝置應用程式報表 hello hello 更新程序的各個階段。
* 查詢裝置中繼資料、組態或狀態。

請參閱太[裝置到雲端通訊指引][ lnk-d2c-guidance]如需使用報告的內容、 裝置到雲端訊息或檔案上傳的指引。
參照太[雲端到裝置通訊指引][ lnk-c2d-guidance]如需使用所需的屬性、 直接的方法或雲端到裝置訊息的指引。

## <a name="device-twins"></a>裝置對應項
裝置對應項會儲存裝置相關資訊，以供︰

* Toosynchronize 裝置條件和設定，可以使用裝置和後端。
* hello 方案後端可以使用 tooquery，與目標長時間執行的作業。

已連結裝置的兩個 hello 生命週期 toohello 對應[裝置身分識別][lnk-identity]。 在 IoT 中樞建立或刪除新的裝置身分識別時，會隱含地建立和刪除裝置對應項。

裝置的兩個是 JSON 文件，其中含有︰

* **標籤**。 一段 hello 方案後端的 hello JSON 文件可以讀取和寫入。 標記不可見的 toodevice 應用程式。
* **所需屬性**。 使用此選項，以及報告的屬性 toosynchronize 裝置組態或條件。 所需的屬性只能設定回 hello 解決方案結束和 hello 裝置應用程式可以讀取。 hello 裝置應用程式也會即時 hello 預期屬性中的變更通知。
* **報告屬性**。 搭配使用所需的屬性 toosynchronize 裝置組態或條件。 報告的屬性只能 hello 裝置應用程式設定與能夠讀取和查詢 hello 方案後端。

此外，hello 裝置兩個 JSON 文件的 hello 根包含儲存在 hello hello 對應裝置身分識別的 hello 唯讀屬性[身分識別登錄][lnk-identity]。

![][img-twin]

下列範例中的 hello 顯示裝置的兩個 JSON 文件：

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

在 hello 根物件是 hello 系統屬性，並且容器物件`tags`，兩者均`reported`和`desired`屬性。 hello`properties`容器包含某些唯讀項目 (`$metadata`， `$etag`，和`$version`) 所述 hello[裝置兩個中繼資料][ lnk-twin-metadata]和[開放式並行存取][ lnk-concurrency]區段。

### <a name="reported-property-example"></a>報告屬性範例
在 hello 上述範例中，包含 hello 裝置兩個`batteryLevel`hello 裝置應用程式所報告的屬性。 這個屬性可以可能 tooquery，並且根據上次報告的電池電量 hello 在裝置上運作。 其他範例包括 hello 裝置應用程式報告裝置功能或連接選項。

> [!NOTE]
> 報告的內容會簡化其中 hello 方案後端有興趣 hello 最後已知的屬性值的案例。 使用[裝置到雲端訊息][ lnk-d2c] hello 方案後端是否需要 tooprocess 裝置遙測 hello 格式，加上事件，例如時間序列的序列。

### <a name="desired-property-example"></a>所需屬性範例
Hello 上述範例中，在 hello`telemetryConfig`裝置兩個想要與報告的內容可供 hello 方案後端與 hello 裝置應用程式 toosynchronize hello 遙測設定此裝置。 例如：

1. hello 方案後端設定預期的 hello 屬性與預期的 hello 組態值。 以下是 hello hello 文件所需的 hello 屬性設定的一部分：
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. hello 裝置應用程式會收到 hello 變更立即如果連線，或在 hello 先重新連線的通知。 hello 裝置應用程式接著會報告 hello 更新組態 (或使用 hello 的錯誤狀況`status`屬性)。 以下是 hello hello 部分報告屬性：
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. hello 方案後端可以追蹤 hello 作業結果的 hello 組態跨許多裝置，藉由[查詢][ lnk-query]裝置雙。

> [!NOTE]
> hello 上述程式碼片段的例子，最佳化來提高可讀性，其中一種方式 tooencode 的裝置組態和它的狀態。 IoT 中樞並無特定的結構描述，如 hello 裝置兩個想要與報告 hello 裝置雙中的屬性。
> 
> 

您可以使用雙 toosynchronize 長時間執行作業，例如韌體更新。 如需有關如何 toouse 屬性 toosynchronize 及追蹤長時間執行的作業，跨裝置，請參閱[使用想要的話屬性 tooconfigure 裝置][lnk-twin-properties]。

## <a name="back-end-operations"></a>後端作業
使用下列不可部分完成的作業，透過 HTTP 公開 hello hello 裝置兩個操作 hello 方案後端：

1. **依識別碼擷取裝置對應項**。此操作會傳回報告 hello 裝置兩個文件，包括標記，且想要，和系統屬性。
2. **部份更新裝置對應項**。 Hello 方案後端 toopartially 更新 hello 標記或中裝置的兩個所需的屬性，可讓這項作業。 加入或更新任何屬性的 JSON 文件以 hello 部分更新。 屬性設定太`null`會移除。 hello 下列範例會建立新的所需的屬性值與`{"newProperty": "newValue"}`，會覆寫的 hello 現有值`existingProperty`與`"otherNewValue"`，並移除`otherOldProperty`。 預期的 tooexisting 屬性或標記，則會不進行任何其他變更：
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **取代所需屬性**。 此作業可讓 hello 方案後端 toocompletely 覆寫所有現有的所需的內容，並以取代為新的 JSON 文件`properties/desired`。
4. **取代標籤**。 此作業可讓 hello 方案後端 toocompletely 覆寫所有現有的標記，並以取代為新的 JSON 文件`tags`。
5. **接收對應項通知**。 這項作業允許 hello 方案後端 toobe hello 兩個已修改時收到通知。 toodo 因此，您的 IoT 解決方案需要 toocreate 路由和 tooset hello 資料來源等太*twinChangeEvents*。 根據預設，不會傳送任何對應項通知，亦即預先不存在這類路由。 如果 hello 變動率過高，或其他原因，例如內部失敗，可能會將只有一個包含所有變更的通知傳送 hello IoT 中樞。 因此，如果您的應用程式需要可靠地稽核和記錄所有中間狀態，則仍建議您使用 D2C 訊息。 hello 兩個通知訊息包含屬性和內文。

    - 屬性

    | 名稱 | 值 |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  傳送嗨通知時間 |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | Hello 裝置識別碼 |
    hubName | IoT 中樞名稱 |
    operationTimestamp | 作業的 [ISO8601] 時間戳記 |
    iothub-message-schema | deviceLifecycleNotification |
    opType | "replaceTwin" 或 "updateTwin" |

    訊息系統屬性會加上 hello`'$'`符號。

    - 內文
        
    本節包含所有 hello 兩個變更，以 JSON 格式。 它是修補程式使用相同格式的 hello、 hello 的差異，就可以包含所有的兩個區段： 標記、 properties.reported、 properties.desired，和它包含 hello"$metadata"項目。 例如，
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

所有 hello 上述作業支援[開放式並行存取][ lnk-concurrency] ，而且需要 hello **ServiceConnect**權限，如同 hello[安全性] [ lnk-security]發行項。

此外 toothese 作業，hello 方案後端可以：

* 查詢使用 hello hello 裝置雙類似 SQL 的[IoT 中樞的查詢語言][lnk-query]。
* 使用[作業][lnk-jobs]在大型裝置對應項集合上執行作業。

## <a name="device-operations"></a>裝置作業
hello 裝置應用程式對 hello 裝置兩個使用 hello 下列不可部分完成的作業：

1. **擷取裝置對應項**。 此操作會傳回 hello 裝置兩個文件 (包含標記和預期、 報告和系統屬性) 的 hello 目前連接的裝置。
2. **部分更新的報告屬性**。 此作業可讓 hello 部分更新的 hello 報告 hello 目前連接裝置的屬性。 此作業會使用 hello 更新相同的 JSON 格式，它 hello 方案後端使用的部分更新的所需的屬性。
3. **觀察所需屬性**。 hello 目前連接的裝置可以選擇 toobe 所發生的任何更新需要 toohello 內容的通知。 hello 裝置收到的 hello hello 方案後端所執行的相同形式的更新 （部分或完整取代）。

所有 hello 先前執行的作業需要 hello **DeviceConnect**權限，如同 hello[安全性][ lnk-security]發行項。

hello [Azure IoT 裝置 Sdk] [ lnk-sdks]使其容易 toouse hello 前從多種語言和平台的作業。 Hello 的 IoT 中樞所需的內容同步處理基本類型的詳細資訊位於[裝置重新連線流程][lnk-reconnection]。

> [!NOTE]
> 目前，只連線 tooIoT 中樞的裝置可以存取裝置雙會使用 hello MQTT 通訊協定。
> 
> 

## <a name="reference-topics"></a>參考主題：
hello 下列參考主題提供您有關控制存取 tooyour IoT 中樞的詳細資訊。

## <a name="tags-and-properties-format"></a>標籤和屬性格式
標記，想要的並報告的屬性是具有下列限制的 hello 的 JSON 物件：

* JSON 物件中的所有索引鍵是區分大小寫的 64 個位元組的 UTF-8 UNICODE 字串。 允許的字元會排除 UNICODE 控制字元 (區段 C0 和 C1)，以及 `'.'`、`' '` 和 `'$'`。
* JSON 物件中的所有值可以都是 hello 下列 JSON 型別： 布林值、 數字、 字串、 物件。 不允許使用陣列。
* 標籤、所需屬性和報告屬性中所有 JSON 物件的深度上限為 5。 比方說，hello 接物件是有效的：

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* 所有字串值的最大長度為 512 個位元組。

## <a name="device-twin-size"></a>裝置對應項大小
IoT 中樞會強制執行 hello 值為 8 KB 大小限制`tags`， `properties/desired`，和`properties/reported`，排除唯讀項目。
hello 大小的計算，來計算所有的字元不包括 UNICODE 控制字元 （區段 C0 和 C1） 和空間`' '`出現以外的字串常數時。
IoT 中樞拒絕，發生錯誤，會增加 hello 大小超過 hello 限制這些文件的所有作業。

## <a name="device-twin-metadata"></a>裝置對應項中繼資料
IoT 中樞維護 hello 時間戳記的 hello 上次更新的每個 JSON 物件中裝置的兩個想要與報告的屬性。 hello 時間戳記都是 UTC 和編碼中 hello [ISO8601]格式`YYYY-MM-DDTHH:MM:SS.mmmZ`。
例如：

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

在物件索引鍵中移除每個層級 （hello JSON 結構的不只是 hello 分葉） toopreserve 更新保留這項資訊。

## <a name="optimistic-concurrency"></a>開放式並行存取
標籤、所需屬性和報告屬性全都支援開放式並行存取。
標記的 ETag，為每個有[RFC7232]，代表 hello 標記 JSON 表示法。 您可以從 hello 方案後端 tooensure 一致性的條件式更新作業中使用的 Etag。

裝置的兩個想要與報告屬性沒有 Etag，但有`$version`保證 toobe 累加值。 同樣地 tooan hello 版本的 ETag，可供 hello 更新合作對象 tooenforce 一致性的更新。 例如，裝置應用程式的報告屬性或 hello 方案後端所需的屬性。

版本也很有用的當 observing 代理程式 （例如 hello 觀察 hello 預期屬性的裝置應用程式），必須協調 hello 作業的結果，擷取和更新通知之間的競爭情況。 hello 區段[裝置重新連線流程][ lnk-reconnection]提供詳細資訊。

## <a name="device-reconnection-flow"></a>裝置重新連線流程
IoT 中樞不會保留已中斷連線之裝置的所需屬性更新通知。 它會遵循連接的裝置必須擷取 hello 完整的所需的內容的文件，在加法 toosubscribing 更新通知。 指定的更新通知和完整擷取之間的競爭情況的 hello 可能性，必須確保 hello 下列流程：

1. 裝置應用程式會連接 tooan IoT 中樞。
2. 裝置應用程式訂閱所需屬性更新通知。
3. 裝置應用程式擷取 hello 需屬性的完整文件。

hello 裝置應用程式可以忽略所有通知使用`$version`小於或等於 hello hello 完整擷取的文件版本。 IoT 中樞保證版本一定會遞增，因此這是可行的方法。

> [!NOTE]
> Hello 中已實作此邏輯[Azure IoT 裝置 Sdk][lnk-sdks]。 只有當 hello 裝置應用程式無法使用任何 Azure IoT 裝置 Sdk，而且必須直接程式 hello MQTT 介面，這項描述會很有用。
> 
> 

## <a name="additional-reference-material"></a>其他參考資料
Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：

* hello [IoT 中樞端點][ lnk-endpoints]文章說明 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。
* hello[節流和配額][ lnk-quotas]文章說明 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。
* hello [Azure IoT 裝置和服務 Sdk] [ lnk-sdks]文章列出 hello 互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用各種語言 Sdk。
* hello[裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][ lnk-query]文章說明 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞.
* hello [IoT 中樞 MQTT 支援][ lnk-devguide-mqtt]文章提供 IoT 中樞支援 hello MQTT 通訊協定的詳細資訊。

## <a name="next-steps"></a>後續步驟
現在您已經學會有關裝置雙，您可能想要遵循 IoT 中樞開發人員指南主題 hello:

* [在裝置上叫用直接方法][lnk-methods]
* [排程多個裝置上的作業][lnk-jobs]

如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程的 hello:

* [如何 toouse hello 裝置兩個][lnk-twin-tutorial]
* [如何 toouse 裝置 twin 屬性][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
