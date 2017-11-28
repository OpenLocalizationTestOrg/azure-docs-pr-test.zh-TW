---
title: "Azure IoT 套件和 Logic Apps | Microsoft Docs"
description: "如何將 Logic Apps 連結至 Azure IoT 套件以執行商務程序的教學課程。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ba52d-103">教學課程：將邏輯應用程式連接至 Azure IoT 套件遠端監視預先設定解決方案</span><span class="sxs-lookup"><span data-stu-id="ba52d-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="ba52d-104">[Microsoft Azure IoT 套件][lnk-internetofthings]遠端監視預先設定解決方案以一套端對端功能集來示範 IoT 解決方案，是快速入門的好工具。</span><span class="sxs-lookup"><span data-stu-id="ba52d-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="ba52d-105">本教學課程逐步引導您將邏輯應用程式連接至 Microsoft Azure IoT 套件遠端監視預先設定解決方案。</span><span class="sxs-lookup"><span data-stu-id="ba52d-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ba52d-106">這些步驟示範如何將 IoT 解決方案連接至商務程序，以進一步發展此 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ba52d-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="ba52d-107">如果您要尋找有關如何佈建遠端監視預先設定解決方案的逐步解說，請參閱[教學課程：開始使用 IoT 預先設定的解決方案][lnk-getstarted]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="ba52d-108">在開始本教學課程之前，您應該：</span><span class="sxs-lookup"><span data-stu-id="ba52d-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="ba52d-109">在您的 Azure 訂用帳戶中佈建遠端監視預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="ba52d-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="ba52d-110">建立 SendGrid 帳戶，用來讓您傳送可觸發商務程序的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ba52d-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="ba52d-111">您可以在 [SendGrid](https://sendgrid.com/) 按一下 [免費試用]，註冊免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba52d-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="ba52d-112">註冊免費試用帳戶後，您必須在 SendGrid 中建立 [API 金鑰](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) 來授權傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="ba52d-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="ba52d-113">稍後在教學課程中需要此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="ba52d-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="ba52d-114">若要完成本教學課程，您需要 Visual Studio 2015 或 Visual Studio 2017，才能在預先設定的解決方案後端中修改動作。</span><span class="sxs-lookup"><span data-stu-id="ba52d-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="ba52d-115">假設您已佈建遠端監視預先設定解決方案，請在 [Azure 入口網站][lnk-azureportal]中瀏覽至該解決方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ba52d-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="ba52d-116">資源群組的名稱與您在佈建遠端監視解決方案時所選擇的解決方案名稱相同。</span><span class="sxs-lookup"><span data-stu-id="ba52d-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ba52d-117">在資源群組中，您可以看到解決方案已佈建的所有 Azure 資源，但在 Azure 傳統入口網站中可找到的 Azure Active Directory 應用程式除外。</span><span class="sxs-lookup"><span data-stu-id="ba52d-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="ba52d-118">下列螢幕擷取畫面顯示遠端監視預先設定解決方案的 [資源群組]  刀鋒視窗範例︰</span><span class="sxs-lookup"><span data-stu-id="ba52d-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="ba52d-119">若要開始，請設定邏輯應用程式來使用預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="ba52d-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="ba52d-120">設定邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ba52d-120">Set up the Logic App</span></span>
1. <span data-ttu-id="ba52d-121">在 Azure 入口網站中，按一下資源群組刀鋒視窗頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="ba52d-122">搜尋 [邏輯應用程式]，選取它，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="ba52d-123">填寫 [名稱]，並使用您佈建遠端監視解決方案時使用的相同 [訂用帳戶] 和 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ba52d-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ba52d-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="ba52d-125">部署完成時，您會看到邏輯應用程式列為資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="ba52d-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="ba52d-126">按一下邏輯應用程式來瀏覽至 [邏輯應用程式] 刀鋒視窗，選取 [空白邏輯應用程式] 範本以開啟 [Logic Apps 設計工具]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="ba52d-127">選取 [要求]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-127">Select **Request**.</span></span> <span data-ttu-id="ba52d-128">這個動作會指定以內送 HTTP 要求加上特定 JSON 格式化承載做為觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ba52d-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="ba52d-129">將下列程式碼貼到 [要求本文 JSON 結構描述] 中：</span><span class="sxs-lookup"><span data-stu-id="ba52d-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ba52d-130">您可以在儲存邏輯應用程式之後複製 HTTP post 要求的 URL，但必須先新增動作。</span><span class="sxs-lookup"><span data-stu-id="ba52d-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="ba52d-131">按一下手動觸發程序下的 [+ 新增步驟]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="ba52d-132">然後按一下 [加入動作] 。</span><span class="sxs-lookup"><span data-stu-id="ba52d-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="ba52d-133">搜尋 [SendGrid - 傳送電子郵件]  並按一下它。</span><span class="sxs-lookup"><span data-stu-id="ba52d-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="ba52d-134">輸入連接的名稱 (如 **SendGridConnection**)，並輸入您設定 SendGrid 帳戶時設定的 **SendGrid API 金鑰**，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="ba52d-135">將您擁有的電子郵件地址新增至 [寄件者] 和 [收件者] 欄位。</span><span class="sxs-lookup"><span data-stu-id="ba52d-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="ba52d-136">將**遠端監視警示 [DeviceId]** 新增至 [主旨] 欄位。</span><span class="sxs-lookup"><span data-stu-id="ba52d-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="ba52d-137">在 [電子郵件內文] 欄位中，新增**裝置 [DeviceId] 已報告 [measurementName] 與 [measuredValue] 值**。</span><span class="sxs-lookup"><span data-stu-id="ba52d-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="ba52d-138">您可以按一下 [您可以從先前步驟中插入資料] 區段，以新增 **[DeviceId]**、**[measurementName]** 和 **[measuredValue]**。</span><span class="sxs-lookup"><span data-stu-id="ba52d-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="ba52d-139">按一下頂端功能表中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="ba52d-140">按一下 [要求] 觸發程序，複製**此 URL 的 Http Post** 值。</span><span class="sxs-lookup"><span data-stu-id="ba52d-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="ba52d-141">稍後在本教學課程中需要此 URL。</span><span class="sxs-lookup"><span data-stu-id="ba52d-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ba52d-142">Logic Apps 可讓您執行[許多不同類型的動作][lnk-logic-apps-actions]，包括 Office 365 中的動作。</span><span class="sxs-lookup"><span data-stu-id="ba52d-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="ba52d-143">設定 EventProcessor Web 作業</span><span class="sxs-lookup"><span data-stu-id="ba52d-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="ba52d-144">在本節中，您會將您預先設定的解決方案連接到您建立的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba52d-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="ba52d-145">為了完成此工作，您要將用於觸發邏輯應用程式的 URL，加入當裝置感應器值超過臨界值時引發的動作。</span><span class="sxs-lookup"><span data-stu-id="ba52d-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="ba52d-146">使用您的 git 用戶端複製最新版的 [azure-iot-remote-monitoring github 儲存機制][lnk-rmgithub]。</span><span class="sxs-lookup"><span data-stu-id="ba52d-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="ba52d-147">例如：</span><span class="sxs-lookup"><span data-stu-id="ba52d-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="ba52d-148">在 Visual Studio 中，從儲存機制的本機複本開啟 **RemoteMonitoring.sln**。</span><span class="sxs-lookup"><span data-stu-id="ba52d-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="ba52d-149">開啟 **Infrastructure\\Repository** 資料夾中的 **ActionRepository.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba52d-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="ba52d-150">使用您從邏輯應用程式記下的**此 URL 的 Http Post** 更新 **actionIds** 字典，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="ba52d-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="ba52d-151">在方案中儲存所做的變更並結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ba52d-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="ba52d-152">從命令列部署</span><span class="sxs-lookup"><span data-stu-id="ba52d-152">Deploy from the command line</span></span>
<span data-ttu-id="ba52d-153">本節中，您要部署已更新的遠端監視解決方案，取代目前在 Azure 中執行的版本。</span><span class="sxs-lookup"><span data-stu-id="ba52d-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="ba52d-154">遵循[開發設定][lnk-devsetup]的指示，設定您的環境準備部署。</span><span class="sxs-lookup"><span data-stu-id="ba52d-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="ba52d-155">若要在本機部署，請遵循[本機部署][lnk-localdeploy]指示。</span><span class="sxs-lookup"><span data-stu-id="ba52d-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="ba52d-156">若要部署至雲端並更新現有的雲端部署，請遵循[雲端部署][lnk-clouddeploy]指示。</span><span class="sxs-lookup"><span data-stu-id="ba52d-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="ba52d-157">使用原始部署的名稱做為部署名稱。</span><span class="sxs-lookup"><span data-stu-id="ba52d-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="ba52d-158">例如，如果原始部署為 **demologicapp**，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ba52d-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="ba52d-159">當建置指令碼執行時，請務必使用您佈建解決方案時所使用的相同 Azure 帳戶、訂用帳戶、區域和 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ba52d-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="ba52d-160">了解邏輯應用程式的實際運作</span><span class="sxs-lookup"><span data-stu-id="ba52d-160">See your Logic App in action</span></span>
<span data-ttu-id="ba52d-161">當您佈建解決方案時，根據預設，遠端監視預先設定的解決方案會設定兩個規則。</span><span class="sxs-lookup"><span data-stu-id="ba52d-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="ba52d-162">這兩個規則都在 **SampleDevice001** 裝置上︰</span><span class="sxs-lookup"><span data-stu-id="ba52d-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="ba52d-163">溫度 > 38.00</span><span class="sxs-lookup"><span data-stu-id="ba52d-163">Temperature > 38.00</span></span>
* <span data-ttu-id="ba52d-164">溼度 > 48.00</span><span class="sxs-lookup"><span data-stu-id="ba52d-164">Humidity > 48.00</span></span>

<span data-ttu-id="ba52d-165">溫度規則會觸發 [引發警示] 動作，溼度規則會觸發 **SendMessage** 動作。</span><span class="sxs-lookup"><span data-stu-id="ba52d-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="ba52d-166">假設您在 **ActionRepository** 類別中對這兩個動作使用相同的 URL，邏輯應用程式將會觸發其中一條規則。</span><span class="sxs-lookup"><span data-stu-id="ba52d-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="ba52d-167">兩條規則皆使用 SendGrid 將警示的詳細資料透過電子郵件傳送至 [收件者]  地址。</span><span class="sxs-lookup"><span data-stu-id="ba52d-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ba52d-168">邏輯應用程式會在每次達到臨界值時繼續觸發。</span><span class="sxs-lookup"><span data-stu-id="ba52d-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="ba52d-169">若要避免不必要的電子郵件，您可以在解決方案入口網站中停用規則，或在 [Azure 入口網站][lnk-azureportal]中停用邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba52d-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="ba52d-170">除了接收電子郵件，您也可以查看邏輯應用程式在入口網站中運作情形︰</span><span class="sxs-lookup"><span data-stu-id="ba52d-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="ba52d-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba52d-171">Next steps</span></span>
<span data-ttu-id="ba52d-172">既然您已使用邏輯應用程式將預先設定的解決方案連接到商務程序，您可以深入了解自訂預先設定的解決方案的選項。</span><span class="sxs-lookup"><span data-stu-id="ba52d-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="ba52d-173">[搭配使用動態遙測與遠端監視預先設定解決方案][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="ba52d-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="ba52d-174">[遠端監視預先設定方案中的裝置資訊中繼資料][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="ba52d-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
