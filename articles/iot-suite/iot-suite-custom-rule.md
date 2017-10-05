---
title: "在 Azure IoT 套件中建立自訂規則 | Microsoft Docs"
description: "如何在 IoT 套件所預先設定的解決方案中建立自訂規則。"
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="51731-103">在遠端監視預先設定的解決方案中建立自訂規則</span><span class="sxs-lookup"><span data-stu-id="51731-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="51731-104">簡介</span><span class="sxs-lookup"><span data-stu-id="51731-104">Introduction</span></span>

<span data-ttu-id="51731-105">在預先設定的解決方案中，您可以設定[會在裝置的遙測值觸達特定臨界值時觸發的規則][lnk-builtin-rule]。</span><span class="sxs-lookup"><span data-stu-id="51731-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="51731-106">[搭配使用動態遙測與遠端監視預先設定解決方案][lnk-dynamic-telemetry]會說明如何在解決方案中新增自訂遙測值，例如 ExternalTemperature。</span><span class="sxs-lookup"><span data-stu-id="51731-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="51731-107">本文則會示範如何在解決方案中建立動態遙測類型的自訂規則。</span><span class="sxs-lookup"><span data-stu-id="51731-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="51731-108">本教學課程使用簡單的 Node.js 模擬裝置，來產生要傳送至預先設定之解決方案後端的動態遙測。</span><span class="sxs-lookup"><span data-stu-id="51731-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="51731-109">然後，您要在 **RemoteMonitoring** Visual Studio 解決方案中新增自訂規則，並將此自訂後端部署至 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51731-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="51731-110">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="51731-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="51731-111">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51731-111">An active Azure subscription.</span></span> <span data-ttu-id="51731-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51731-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="51731-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="51731-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="51731-114">[Node.js][lnk-node] 0.12.x 版或更新版本，以建立模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="51731-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="51731-115">Visual Studio 2015 或 Visual Studio 2017，以使用新規則修改預先設定的解決方案後端。</span><span class="sxs-lookup"><span data-stu-id="51731-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="51731-116">請記下您為部署選擇的解決方案名稱。</span><span class="sxs-lookup"><span data-stu-id="51731-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="51731-117">本教學課程稍後需要用到此解決方案名稱。</span><span class="sxs-lookup"><span data-stu-id="51731-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="51731-118">當您確認 Node.js 主控台應用程式會將 **ExternalTemperature** 遙測傳送至預先設定的解決方案時，便可將其停止。</span><span class="sxs-lookup"><span data-stu-id="51731-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="51731-119">在將自訂規則新增至解決方案後，您會再次執行此 Node.js 主控台應用程式，因此請將主控台視窗保持開啟狀態。</span><span class="sxs-lookup"><span data-stu-id="51731-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="51731-120">規則的儲存位置</span><span class="sxs-lookup"><span data-stu-id="51731-120">Rule storage locations</span></span>

<span data-ttu-id="51731-121">規則的相關資訊會保存在兩個位置︰</span><span class="sxs-lookup"><span data-stu-id="51731-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="51731-122">**DeviceRulesNormalizedTable** 資料表 – 此資料表會儲存解決方案入口網站所定義之規則的標準化參考。</span><span class="sxs-lookup"><span data-stu-id="51731-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="51731-123">解決方案入口網站在顯示裝置規則時，會查詢此資料表以取得規則定義。</span><span class="sxs-lookup"><span data-stu-id="51731-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="51731-124">**DeviceRules** Blob – 此 Blob 會儲存所有註冊裝置已定義的所有規則，並且會定義為 Azure 串流分析作業的參考輸入。</span><span class="sxs-lookup"><span data-stu-id="51731-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="51731-125">當您在解決方案入口網站中更新現有規則或定義新規則時，資料表和 Blob 皆會更新，以反映所做的變更。</span><span class="sxs-lookup"><span data-stu-id="51731-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="51731-126">入口網站中顯示的規則定義來自資料表存放區，串流分析作業所參考的規則定義則來自 Blob。</span><span class="sxs-lookup"><span data-stu-id="51731-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="51731-127">更新 RemoteMonitoring Visual Studio 解決方案</span><span class="sxs-lookup"><span data-stu-id="51731-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="51731-128">下列步驟說明如何修改 RemoteMonitoring Visual Studio 解決方案，以納入使用模擬裝置所傳來之 **ExternalTemperature** 遙測的新規則︰</span><span class="sxs-lookup"><span data-stu-id="51731-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="51731-129">如果您尚未這麼做，請使用下列 Git 命令將 **azure-iot-remote-monitoring** 儲存機制複製到本機電腦上的適當位置︰</span><span class="sxs-lookup"><span data-stu-id="51731-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="51731-130">在 Visual Studio 中，從 **azure-iot-remote-monitoring** 儲存機制的本機複本開啟 RemoteMonitoring.sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="51731-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="51731-131">開啟檔案 Infrastructure\Models\DeviceRuleBlobEntity.cs 並新增 **ExternalTemperature** 屬性，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51731-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="51731-132">在相同的檔案中新增 **ExternalTemperatureRuleOutput** 屬性，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51731-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="51731-133">開啟檔案 Infrastructure\Models\DeviceRuleDataFields.cs，並在現有的 **Humidity** 屬性後新增下列 **ExternalTemperature** 屬性：</span><span class="sxs-lookup"><span data-stu-id="51731-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="51731-134">在相同的檔案中更新 **_availableDataFields** 方法，以納入 **ExternalTemperature**，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51731-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="51731-135">開啟檔案 Infrastructure\Repository\DeviceRulesRepository.cs 並修改 **BuildBlobEntityListFromTableRows** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51731-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="51731-136">重建並重新部署解決方案。</span><span class="sxs-lookup"><span data-stu-id="51731-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="51731-137">您現在可以在 Azure 訂用帳戶中部署已更新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="51731-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="51731-138">開啟提高權限的命令提示字元，並瀏覽至 azure-iot-remote-monitoring 儲存機制本機複本的根目錄。</span><span class="sxs-lookup"><span data-stu-id="51731-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="51731-139">若要部署已更新的解決方案，請執行下列命令，並將 **{deployment name}** 換成您先前記下之預先設定解決方案部署的名稱︰</span><span class="sxs-lookup"><span data-stu-id="51731-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="51731-140">更新串流分析作業</span><span class="sxs-lookup"><span data-stu-id="51731-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="51731-141">部署完成時，您可以將串流分析作業更新為使用新的規則定義。</span><span class="sxs-lookup"><span data-stu-id="51731-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="51731-142">在 Azure 入口網站中，瀏覽至預先設定之解決方案資源所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="51731-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="51731-143">此資源群組的名稱和您在部署期間為解決方案所指定的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="51731-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="51731-144">瀏覽至 {deployment name}-Rules 串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="51731-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="51731-145">按一下 [停止] 讓串流分析作業停止執行 </span><span class="sxs-lookup"><span data-stu-id="51731-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="51731-146">(您必須等到串流作業停止後，才能編輯查詢)。</span><span class="sxs-lookup"><span data-stu-id="51731-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="51731-147">按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="51731-147">Click **Query**.</span></span> <span data-ttu-id="51731-148">編輯查詢以納入 **ExternalTemperature** 的 **SELECT** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="51731-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="51731-149">下列範例示範具有全新 **SELECT** 陳述式的完整查詢︰</span><span class="sxs-lookup"><span data-stu-id="51731-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="51731-150">按一下 [儲存] 來變更已更新的規則查詢。</span><span class="sxs-lookup"><span data-stu-id="51731-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="51731-151">按一下 [啟動] 讓串流分析作業再次開始執行。</span><span class="sxs-lookup"><span data-stu-id="51731-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="51731-152">在儀表板中新增規則</span><span class="sxs-lookup"><span data-stu-id="51731-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="51731-153">您現在可以在解決方案儀表板中對裝置新增 **ExternalTemperature** 規則。</span><span class="sxs-lookup"><span data-stu-id="51731-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="51731-154">瀏覽至解決方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="51731-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="51731-155">瀏覽至 [裝置] 面板。</span><span class="sxs-lookup"><span data-stu-id="51731-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="51731-156">找出您所建立會傳送 **ExternalTemperature** 遙測的自訂裝置，然後在 [裝置詳細資料] 面板上按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="51731-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="51731-157">在 [資料欄位] 中選取 [ExternalTemperature]。</span><span class="sxs-lookup"><span data-stu-id="51731-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="51731-158">將 [閾值] 設定為 56。</span><span class="sxs-lookup"><span data-stu-id="51731-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="51731-159">然後按一下 [儲存及檢視規則]。</span><span class="sxs-lookup"><span data-stu-id="51731-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="51731-160">返回儀表板以檢視警示歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="51731-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="51731-161">在您保持開啟的主控台視窗中，啟動 Node.js 主控台應用程式，以開始傳送 **ExternalTemperature** 遙測資料。</span><span class="sxs-lookup"><span data-stu-id="51731-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="51731-162">請注意，當有新規則觸發時，[警示歷程記錄] 資料表便會顯示新警示。</span><span class="sxs-lookup"><span data-stu-id="51731-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="51731-163">其他資訊</span><span class="sxs-lookup"><span data-stu-id="51731-163">Additional information</span></span>

<span data-ttu-id="51731-164">變更運算子 **>** 的程序更為複雜，不在本教學課程所述步驟的適用範圍內。</span><span class="sxs-lookup"><span data-stu-id="51731-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="51731-165">雖然您可以變更串流分析作業，以使用您所想要的任何運算子，但在解決方案入口網站中反映該運算子是更為複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="51731-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="51731-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51731-166">Next steps</span></span>
<span data-ttu-id="51731-167">既然您已了解如何建立自訂規則，您可以進一步了解預先設定的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="51731-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="51731-168">[將邏輯應用程式連接至 Azure IoT 套件遠端監視預先設定解決方案][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="51731-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="51731-169">[遠端監視預先設定方案中的裝置資訊中繼資料][lnk-devinfo]。</span><span class="sxs-lookup"><span data-stu-id="51731-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md