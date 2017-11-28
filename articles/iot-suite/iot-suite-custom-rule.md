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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="7bc41-103">建立 hello 的自訂規則遠端監視預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="7bc41-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="7bc41-104">簡介</span><span class="sxs-lookup"><span data-stu-id="7bc41-104">Introduction</span></span>

<span data-ttu-id="7bc41-105">在預先設定的 hello 方案中，您可以設定[裝置到達特定臨界值的規則時遙測觸發值][lnk-builtin-rule]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="7bc41-106">[使用遠端監視預先設定的解決方案 hello 動態遙測][ lnk-dynamic-telemetry]描述如何在加入自訂遙測的值，例如*ExternalTemperature* tooyour 方案。</span><span class="sxs-lookup"><span data-stu-id="7bc41-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="7bc41-107">本文章將示範如何動態遙測 toocreate 自訂規則類型在您的方案中。</span><span class="sxs-lookup"><span data-stu-id="7bc41-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="7bc41-108">本教學課程使用的簡單 Node.js 模擬的裝置 toogenerate 動態遙測 toosend toohello 預先設定的方案後端。</span><span class="sxs-lookup"><span data-stu-id="7bc41-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="7bc41-109">然後您自訂的規則中加入 hello **RemoteMonitoring** Visual Studio 方案並部署此自訂的後端 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc41-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="7bc41-110">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="7bc41-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="7bc41-111">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc41-111">An active Azure subscription.</span></span> <span data-ttu-id="7bc41-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc41-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7bc41-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="7bc41-114">[Node.js] [ lnk-node]版本 0.12.x 或更新版本 toocreate 模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="7bc41-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="7bc41-115">Visual Studio 2015 或 Visual Studio 2017 toomodify 預先設定的 hello 方案回您的新規則的結尾。</span><span class="sxs-lookup"><span data-stu-id="7bc41-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="7bc41-116">記下您選擇部署的 hello 方案名稱。</span><span class="sxs-lookup"><span data-stu-id="7bc41-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="7bc41-117">本教學課程稍後需要用到此解決方案名稱。</span><span class="sxs-lookup"><span data-stu-id="7bc41-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="7bc41-118">您可以停止 hello Node.js 主控台應用程式，確認它傳送**ExternalTemperature**遙測 toohello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7bc41-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="7bc41-119">保持 hello 主控台視窗開啟，因為您此 Node.js 主控台應用程式之後再次執行新增 hello 自訂規則 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="7bc41-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="7bc41-120">規則的儲存位置</span><span class="sxs-lookup"><span data-stu-id="7bc41-120">Rule storage locations</span></span>

<span data-ttu-id="7bc41-121">規則的相關資訊會保存在兩個位置︰</span><span class="sxs-lookup"><span data-stu-id="7bc41-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="7bc41-122">**DeviceRulesNormalizedTable**資料表-這個資料表會儲存正規化參考 toohello hello 方案入口網站所定義的規則。</span><span class="sxs-lookup"><span data-stu-id="7bc41-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="7bc41-123">Hello 方案入口網站會顯示裝置的規則，它會查詢此資料表的 hello 規則定義。</span><span class="sxs-lookup"><span data-stu-id="7bc41-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="7bc41-124">**DeviceRules** blob-此 blob 會儲存所有 hello 規則中定義的所有已註冊的裝置，且定義為參考輸入的 toohello Azure Stream Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="7bc41-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="7bc41-125">當您更新現有的規則，或在 hello 方案入口網站中定義新的規則時，hello 資料表和 blob 會更新的 tooreflect hello 變更。</span><span class="sxs-lookup"><span data-stu-id="7bc41-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="7bc41-126">定義顯示 hello 入口網站中的 hello 規則來自於 hello 資料表存放區，以及定義 hello 串流分析工作所參考來自 hello blob hello 規則。</span><span class="sxs-lookup"><span data-stu-id="7bc41-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="7bc41-127">更新 hello RemoteMonitoring Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="7bc41-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="7bc41-128">hello 下列步驟說明如何 toomodify 會 hello RemoteMonitoring Visual Studio 方案 tooinclude 新規則，以便使用 hello **ExternalTemperature**遙測傳送嗨模擬的裝置：</span><span class="sxs-lookup"><span data-stu-id="7bc41-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="7bc41-129">如果您有您尚未這樣做，複製 hello **azure iot-遠端-監視**使用 hello 下列 Git 命令在本機電腦上的儲存機制 tooa 適合位置：</span><span class="sxs-lookup"><span data-stu-id="7bc41-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="7bc41-130">在 Visual Studio 中，開啟 hello RemoteMonitoring.sln 檔案從您的本機複本的 hello **azure iot-遠端-監視**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7bc41-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="7bc41-131">開啟 hello 檔案 Infrastructure\Models\DeviceRuleBlobEntity.cs 並加入**ExternalTemperature**屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7bc41-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="7bc41-132">在 hello 同一個檔案中新增**ExternalTemperatureRuleOutput**屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7bc41-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="7bc41-133">開啟 hello 檔案 Infrastructure\Models\DeviceRuleDataFields.cs 並加入下列 hello **ExternalTemperature**屬性之後 hello 現有**溼度**屬性：</span><span class="sxs-lookup"><span data-stu-id="7bc41-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="7bc41-134">在 hello 同一個檔案中更新 hello **_availableDataFields**方法 tooinclude **ExternalTemperature** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7bc41-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="7bc41-135">開啟並修改 hello hello 檔案 Infrastructure\Repository\DeviceRulesRepository.cs **BuildBlobEntityListFromTableRows**方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7bc41-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="7bc41-136">重建並重新部署 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="7bc41-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="7bc41-137">您現在可以部署更新的 hello 方案 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bc41-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="7bc41-138">開啟提升權限的命令提示字元並瀏覽 toohello 根 hello azure iot-遠端-監視儲存機制的本機副本。</span><span class="sxs-lookup"><span data-stu-id="7bc41-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="7bc41-139">toodeploy 更新的方案中，執行下列命令以替代的 hello **{部署名稱}** hello 名稱，為您先前所述的預先設定的解決方案部署：</span><span class="sxs-lookup"><span data-stu-id="7bc41-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="7bc41-140">更新 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="7bc41-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="7bc41-141">Hello 部署完成時，您可以更新 hello 資料流分析工作 toouse hello 新規則的定義。</span><span class="sxs-lookup"><span data-stu-id="7bc41-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="7bc41-142">在 hello Azure 入口網站，瀏覽 toohello 資源群組，其中包含您預先設定的解決方案的資源。</span><span class="sxs-lookup"><span data-stu-id="7bc41-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="7bc41-143">此資源群組具有您指定的名稱相同的 hello hello hello 部署期間的方案。</span><span class="sxs-lookup"><span data-stu-id="7bc41-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="7bc41-144">瀏覽 toohello {部署 name} 的規則資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7bc41-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="7bc41-145">按一下**停止**toostop hello 資料流分析工作無法執行。</span><span class="sxs-lookup"><span data-stu-id="7bc41-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="7bc41-146">（您必須等候 hello 串流工作 toostop，才能編輯 hello 查詢）。</span><span class="sxs-lookup"><span data-stu-id="7bc41-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="7bc41-147">按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-147">Click **Query**.</span></span> <span data-ttu-id="7bc41-148">編輯 hello 查詢 tooinclude hello**選取**陳述式**ExternalTemperature**。</span><span class="sxs-lookup"><span data-stu-id="7bc41-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="7bc41-149">hello 下列範例顯示以 hello hello 完整查詢新**選取**陳述式：</span><span class="sxs-lookup"><span data-stu-id="7bc41-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="7bc41-150">按一下**儲存**toochange hello 更新規則查詢。</span><span class="sxs-lookup"><span data-stu-id="7bc41-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="7bc41-151">按一下**啟動**toostart hello 資料流分析工作一次執行。</span><span class="sxs-lookup"><span data-stu-id="7bc41-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="7bc41-152">Hello 儀表板中加入您的新規則</span><span class="sxs-lookup"><span data-stu-id="7bc41-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="7bc41-153">您現在可以新增 hello **ExternalTemperature**規則 tooa 裝置 hello 方案儀表板中的。</span><span class="sxs-lookup"><span data-stu-id="7bc41-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="7bc41-154">瀏覽 toohello 方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="7bc41-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="7bc41-155">瀏覽 toohello**裝置**面板。</span><span class="sxs-lookup"><span data-stu-id="7bc41-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="7bc41-156">找出 hello 自訂您建立的裝置傳送**ExternalTemperature**遙測和 hello**裝置詳細資料**] 面板中，按一下 [**加入規則**。</span><span class="sxs-lookup"><span data-stu-id="7bc41-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="7bc41-157">在 [資料欄位] 中選取 [ExternalTemperature]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="7bc41-158">設定**閾值**too56。</span><span class="sxs-lookup"><span data-stu-id="7bc41-158">Set **Threshold** too56.</span></span> <span data-ttu-id="7bc41-159">然後按一下 [儲存及檢視規則]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="7bc41-160">傳回 toohello 儀表板 tooview hello 警示歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="7bc41-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="7bc41-161">開始在 hello 保持在開啟的主控台視窗中的 hello Node.js 主控台應用程式 toobegin 傳送**ExternalTemperature**遙測資料。</span><span class="sxs-lookup"><span data-stu-id="7bc41-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="7bc41-162">請注意該 hello**警示歷程記錄**觸發 hello 新規則時，表格會顯示新的警示。</span><span class="sxs-lookup"><span data-stu-id="7bc41-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="7bc41-163">其他資訊</span><span class="sxs-lookup"><span data-stu-id="7bc41-163">Additional information</span></span>

<span data-ttu-id="7bc41-164">變更 hello 運算子 **>** 更複雜，而且超出此教學課程中所述的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7bc41-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="7bc41-165">雖然您可以變更 hello 資料流分析工作 toouse 任何您喜歡的運算子，反映 hello 方案入口網站中的運算子是更複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="7bc41-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7bc41-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7bc41-166">Next steps</span></span>
<span data-ttu-id="7bc41-167">既然您已經看到如何 toocreate 自訂規則，您可以深入了解預先設定的 hello 方案：</span><span class="sxs-lookup"><span data-stu-id="7bc41-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="7bc41-168">[連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="7bc41-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="7bc41-169">[在 hello 遠端監視的裝置資訊中繼資料已預先設定的解決方案][lnk-devinfo]。</span><span class="sxs-lookup"><span data-stu-id="7bc41-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md