---
title: "Azure IoT 套件中的自訂規則 aaaCreate |Microsoft 文件"
description: "如何 toocreate IoT 套件中的自訂規則預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>建立 hello 的自訂規則遠端監視預先設定的解決方案

## <a name="introduction"></a>簡介

在預先設定的 hello 方案中，您可以設定[裝置到達特定臨界值的規則時遙測觸發值][lnk-builtin-rule]。 [使用遠端監視預先設定的解決方案 hello 動態遙測][ lnk-dynamic-telemetry]描述如何在加入自訂遙測的值，例如*ExternalTemperature* tooyour 方案。 本文章將示範如何動態遙測 toocreate 自訂規則類型在您的方案中。

本教學課程使用的簡單 Node.js 模擬的裝置 toogenerate 動態遙測 toosend toohello 預先設定的方案後端。 然後您自訂的規則中加入 hello **RemoteMonitoring** Visual Studio 方案並部署此自訂的後端 tooyour Azure 訂用帳戶。

toocomplete 本教學課程中，您需要：

* 有效的 Azure 訂用帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。
* [Node.js] [ lnk-node]版本 0.12.x 或更新版本 toocreate 模擬的裝置。
* Visual Studio 2015 或 Visual Studio 2017 toomodify 預先設定的 hello 方案回您的新規則的結尾。

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

記下您選擇部署的 hello 方案名稱。 本教學課程稍後需要用到此解決方案名稱。

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

您可以停止 hello Node.js 主控台應用程式，確認它傳送**ExternalTemperature**遙測 toohello 預先設定的解決方案。 保持 hello 主控台視窗開啟，因為您此 Node.js 主控台應用程式之後再次執行新增 hello 自訂規則 toohello 方案。

## <a name="rule-storage-locations"></a>規則的儲存位置

規則的相關資訊會保存在兩個位置︰

* **DeviceRulesNormalizedTable**資料表-這個資料表會儲存正規化參考 toohello hello 方案入口網站所定義的規則。 Hello 方案入口網站會顯示裝置的規則，它會查詢此資料表的 hello 規則定義。
* **DeviceRules** blob-此 blob 會儲存所有 hello 規則中定義的所有已註冊的裝置，且定義為參考輸入的 toohello Azure Stream Analytics 工作。
 
當您更新現有的規則，或在 hello 方案入口網站中定義新的規則時，hello 資料表和 blob 會更新的 tooreflect hello 變更。 定義顯示 hello 入口網站中的 hello 規則來自於 hello 資料表存放區，以及定義 hello 串流分析工作所參考來自 hello blob hello 規則。 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>更新 hello RemoteMonitoring Visual Studio 方案

hello 下列步驟說明如何 toomodify 會 hello RemoteMonitoring Visual Studio 方案 tooinclude 新規則，以便使用 hello **ExternalTemperature**遙測傳送嗨模擬的裝置：

1. 如果您有您尚未這樣做，複製 hello **azure iot-遠端-監視**使用 hello 下列 Git 命令在本機電腦上的儲存機制 tooa 適合位置：

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. 在 Visual Studio 中，開啟 hello RemoteMonitoring.sln 檔案從您的本機複本的 hello **azure iot-遠端-監視**儲存機制。

3. 開啟 hello 檔案 Infrastructure\Models\DeviceRuleBlobEntity.cs 並加入**ExternalTemperature**屬性，如下所示：

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. 在 hello 同一個檔案中新增**ExternalTemperatureRuleOutput**屬性，如下所示：

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. 開啟 hello 檔案 Infrastructure\Models\DeviceRuleDataFields.cs 並加入下列 hello **ExternalTemperature**屬性之後 hello 現有**溼度**屬性：

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. 在 hello 同一個檔案中更新 hello **_availableDataFields**方法 tooinclude **ExternalTemperature** ，如下所示：

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. 開啟並修改 hello hello 檔案 Infrastructure\Repository\DeviceRulesRepository.cs **BuildBlobEntityListFromTableRows**方法，如下所示：

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>重建並重新部署 hello 方案。

您現在可以部署更新的 hello 方案 tooyour Azure 訂用帳戶。

1. 開啟提升權限的命令提示字元並瀏覽 toohello 根 hello azure iot-遠端-監視儲存機制的本機副本。

2. toodeploy 更新的方案中，執行下列命令以替代的 hello **{部署名稱}** hello 名稱，為您先前所述的預先設定的解決方案部署：

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>更新 hello 資料流分析工作

Hello 部署完成時，您可以更新 hello 資料流分析工作 toouse hello 新規則的定義。

1. 在 hello Azure 入口網站，瀏覽 toohello 資源群組，其中包含您預先設定的解決方案的資源。 此資源群組具有您指定的名稱相同的 hello hello hello 部署期間的方案。

2. 瀏覽 toohello {部署 name} 的規則資料流分析工作。 

3. 按一下**停止**toostop hello 資料流分析工作無法執行。 （您必須等候 hello 串流工作 toostop，才能編輯 hello 查詢）。

4. 按一下 [查詢]。 編輯 hello 查詢 tooinclude hello**選取**陳述式**ExternalTemperature**。 hello 下列範例顯示以 hello hello 完整查詢新**選取**陳述式：

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. 按一下**儲存**toochange hello 更新規則查詢。

6. 按一下**啟動**toostart hello 資料流分析工作一次執行。

## <a name="add-your-new-rule-in-hello-dashboard"></a>Hello 儀表板中加入您的新規則

您現在可以新增 hello **ExternalTemperature**規則 tooa 裝置 hello 方案儀表板中的。

1. 瀏覽 toohello 方案入口網站。

2. 瀏覽 toohello**裝置**面板。

3. 找出 hello 自訂您建立的裝置傳送**ExternalTemperature**遙測和 hello**裝置詳細資料**] 面板中，按一下 [**加入規則**。

4. 在 [資料欄位] 中選取 [ExternalTemperature]。

5. 設定**閾值**too56。 然後按一下 [儲存及檢視規則]。

6. 傳回 toohello 儀表板 tooview hello 警示歷程記錄。

7. 開始在 hello 保持在開啟的主控台視窗中的 hello Node.js 主控台應用程式 toobegin 傳送**ExternalTemperature**遙測資料。

8. 請注意該 hello**警示歷程記錄**觸發 hello 新規則時，表格會顯示新的警示。
 
## <a name="additional-information"></a>其他資訊

變更 hello 運算子 **>** 更複雜，而且超出此教學課程中所述的 hello 步驟。 雖然您可以變更 hello 資料流分析工作 toouse 任何您喜歡的運算子，反映 hello 方案入口網站中的運算子是更複雜的工作。 

## <a name="next-steps"></a>後續步驟
既然您已經看到如何 toocreate 自訂規則，您可以深入了解預先設定的 hello 方案：

- [連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案][lnk-logic-app]
- [在 hello 遠端監視的裝置資訊中繼資料已預先設定的解決方案][lnk-devinfo]。

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md