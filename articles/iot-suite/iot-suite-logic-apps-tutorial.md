---
title: "aaaAzure IoT 套件和 Logic Apps |Microsoft 文件"
description: "教學課程，說明如何 toohook 組成商務程序的 Logic Apps tooAzure IoT 套件。"
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
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="58b0a-103">教學課程： 連接邏輯應用程式 tooyour Azure IoT 套件遠端監視預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="58b0a-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="58b0a-104">hello [Microsoft Azure IoT 套件][ lnk-internetofthings]遠端監視預先設定的解決方案是很好的方法 tooget 快速地開始使用演化的 IoT 解決方案的端對端功能集。</span><span class="sxs-lookup"><span data-stu-id="58b0a-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="58b0a-105">本教學課程會引導您如何 tooadd 邏輯應用程式 tooyour Microsoft Azure IoT 套件遠端監視預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="58b0a-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="58b0a-106">這些步驟將示範如何連接 tooa 商務程序可以採取進一步的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="58b0a-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="58b0a-107">*如果您想要尋求遠端監視 tooprovision 如何預先設定方案的逐步解說，請參閱[教學課程： 開始使用 hello 預先設定的 IoT 解決方案][lnk-getstarted]。*</span><span class="sxs-lookup"><span data-stu-id="58b0a-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="58b0a-108">在開始本教學課程之前，您應該：</span><span class="sxs-lookup"><span data-stu-id="58b0a-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="58b0a-109">佈建 hello 遠端監視您的 Azure 訂用帳戶中預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="58b0a-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="58b0a-110">建立 SendGrid 帳戶 tooenable toosend 商務程序會觸發一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="58b0a-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="58b0a-111">您可以在 [SendGrid](https://sendgrid.com/) 按一下 [免費試用]，註冊免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58b0a-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="58b0a-112">您註冊免費試用帳戶之後，您需要 toocreate [API 金鑰](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html)SendGrid 授與權限 toosend 郵件中。</span><span class="sxs-lookup"><span data-stu-id="58b0a-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="58b0a-113">您稍後在 hello 教學課程需要此 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="58b0a-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="58b0a-114">toocomplete 本教學課程中，您需要在 hello 預先設定的方案後端中的 Visual Studio 2015 或 Visual Studio 2017 toomodify hello 動作。</span><span class="sxs-lookup"><span data-stu-id="58b0a-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="58b0a-115">假設您已提供遠端監視預先設定的方案中，瀏覽 toohello 資源群組，為該方案在 hello [Azure 入口網站][lnk-azureportal]。</span><span class="sxs-lookup"><span data-stu-id="58b0a-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="58b0a-116">hello 資源群組都有名稱為 hello 方案名稱相同的 hello 選擇佈建遠端監視解決方案時。</span><span class="sxs-lookup"><span data-stu-id="58b0a-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="58b0a-117">在 hello 資源群組中，您可以看到所有 hello 佈都建您的解決方案，除了 hello Azure Active Directory 應用程式，您可以在 hello Azure 傳統入口網站中找到的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="58b0a-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="58b0a-118">hello 下列螢幕擷取畫面顯示範例**資源群組**刀鋒視窗中的遠端監視預先設定的方案：</span><span class="sxs-lookup"><span data-stu-id="58b0a-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="58b0a-119">toobegin，設定以 hello hello 邏輯應用程式 toouse 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="58b0a-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="58b0a-120">設定 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="58b0a-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="58b0a-121">按一下**新增**在資源群組] 刀鋒視窗，在 [hello Azure 入口網站中的 hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="58b0a-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="58b0a-122">搜尋 邏輯應用程式，選取它，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="58b0a-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="58b0a-123">填寫 hello**名稱**和使用 hello 相同**訂用帳戶**和**資源群組**您佈建遠端監視解決方案時使用。</span><span class="sxs-lookup"><span data-stu-id="58b0a-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="58b0a-124">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="58b0a-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="58b0a-125">部署完成時，您可以查看資源 hello 邏輯應用程式會列出資源群組中。</span><span class="sxs-lookup"><span data-stu-id="58b0a-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="58b0a-126">按一下 hello 邏輯應用程式 toonavigate toohello 邏輯應用程式刀鋒視窗中，選取 hello**空白邏輯應用程式**範本 tooopen hello**邏輯應用程式設計師**。</span><span class="sxs-lookup"><span data-stu-id="58b0a-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="58b0a-127">選取 [要求]。</span><span class="sxs-lookup"><span data-stu-id="58b0a-127">Select **Request**.</span></span> <span data-ttu-id="58b0a-128">這個動作會指定以內送 HTTP 要求加上特定 JSON 格式化承載做為觸發程序。</span><span class="sxs-lookup"><span data-stu-id="58b0a-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="58b0a-129">貼上下列程式碼到 hello 要求本文 JSON 結構描述的 hello:</span><span class="sxs-lookup"><span data-stu-id="58b0a-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="58b0a-130">您儲存 hello 邏輯應用程式，但首先您必須將動作之後，您可以複製 hello hello HTTP post 的 URL。</span><span class="sxs-lookup"><span data-stu-id="58b0a-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="58b0a-131">按一下手動觸發程序下的 [+ 新增步驟]。</span><span class="sxs-lookup"><span data-stu-id="58b0a-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="58b0a-132">然後按一下 [加入動作] 。</span><span class="sxs-lookup"><span data-stu-id="58b0a-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="58b0a-133">搜尋 [SendGrid - 傳送電子郵件]  並按一下它。</span><span class="sxs-lookup"><span data-stu-id="58b0a-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="58b0a-134">輸入 hello 連接的名稱，例如**SendGridConnection**，輸入 hello **SendGrid API 金鑰**當您設定您的 SendGrid 帳戶，然後按一下您建立**建立**。</span><span class="sxs-lookup"><span data-stu-id="58b0a-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="58b0a-135">新增電子郵件地址與您自己的 tooboth hello**從**和**至**欄位。</span><span class="sxs-lookup"><span data-stu-id="58b0a-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="58b0a-136">新增**遠端監視警示 [DeviceId]** toohello**主旨**欄位。</span><span class="sxs-lookup"><span data-stu-id="58b0a-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="58b0a-137">在 hello**電子郵件內文**欄位中，加入**裝置 [DeviceId] 已報告 [measurementName] 與 [measuredValue] 值。**</span><span class="sxs-lookup"><span data-stu-id="58b0a-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="58b0a-138">您可以加入**[DeviceId]**， **[measurementName]**，和**[measuredValue]**即可 hello**您可以將資料從先前的步驟**> 一節。</span><span class="sxs-lookup"><span data-stu-id="58b0a-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="58b0a-139">按一下**儲存**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="58b0a-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="58b0a-140">按一下 hello**要求**觸發程序，複製 hello **Http Post toothis URL**值。</span><span class="sxs-lookup"><span data-stu-id="58b0a-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="58b0a-141">稍後在本教學課程中需要此 URL。</span><span class="sxs-lookup"><span data-stu-id="58b0a-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="58b0a-142">Logic Apps 可讓您 toorun[許多不同類型的動作][ lnk-logic-apps-actions]包括在 Office 365 中的動作。</span><span class="sxs-lookup"><span data-stu-id="58b0a-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="58b0a-143">設定 hello EventProcessor Web 工作</span><span class="sxs-lookup"><span data-stu-id="58b0a-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="58b0a-144">在本節中，您可以連接您預先設定的解決方案 toohello 您所建立的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="58b0a-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="58b0a-145">toocomplete 這個工作中，您新增 hello URL tootrigger hello 邏輯應用程式 toohello 動作裝置感應器值超過閾值時所引發。</span><span class="sxs-lookup"><span data-stu-id="58b0a-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="58b0a-146">使用 git 用戶端 tooclone hello 最新版本的 hello [azure iot-遠端-監視 github 儲存機制][lnk-rmgithub]。</span><span class="sxs-lookup"><span data-stu-id="58b0a-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="58b0a-147">例如：</span><span class="sxs-lookup"><span data-stu-id="58b0a-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="58b0a-148">在 Visual Studio 中，開啟 hello **RemoteMonitoring.sln**從 hello 的 hello 儲存機制的本機複本。</span><span class="sxs-lookup"><span data-stu-id="58b0a-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="58b0a-149">開啟 hello **ActionRepository.cs**檔案在 hello**基礎結構\\儲存機制**資料夾。</span><span class="sxs-lookup"><span data-stu-id="58b0a-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="58b0a-150">更新 hello **actionIds**字典以 hello **Http Post toothis URL**您記下從應用程式邏輯，如下所示：</span><span class="sxs-lookup"><span data-stu-id="58b0a-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="58b0a-151">儲存在方案中的 hello 變更並結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="58b0a-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="58b0a-152">從 hello 命令列部署</span><span class="sxs-lookup"><span data-stu-id="58b0a-152">Deploy from hello command line</span></span>
<span data-ttu-id="58b0a-153">在本節中，您要部署您的 hello 遠端監視解決方案 tooreplace hello 版本目前在 Azure 中執行的更新的版本。</span><span class="sxs-lookup"><span data-stu-id="58b0a-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="58b0a-154">下列 hello[開發人員安裝][ lnk-devsetup]指示 tooset 部署環境。</span><span class="sxs-lookup"><span data-stu-id="58b0a-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="58b0a-155">在本機，toodeploy 遵循 hello[本機部署][ lnk-localdeploy]指示。</span><span class="sxs-lookup"><span data-stu-id="58b0a-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="58b0a-156">toodeploy toohello 雲端並更新您現有的雲端部署，請遵循 hello[雲端部署][ lnk-clouddeploy]指示。</span><span class="sxs-lookup"><span data-stu-id="58b0a-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="58b0a-157">您可以使用原始部署的 hello 名稱做為 hello 部署名稱。</span><span class="sxs-lookup"><span data-stu-id="58b0a-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="58b0a-158">例如，如果呼叫 hello 原始部署**demologicapp**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="58b0a-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="58b0a-159">當 hello 建置指令碼執行時，務必 toouse hello 相同 Azure 帳戶、 訂用帳戶、 地區和您佈建 hello 方案時所使用的 Active Directory 執行個體。</span><span class="sxs-lookup"><span data-stu-id="58b0a-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="58b0a-160">了解邏輯應用程式的實際運作</span><span class="sxs-lookup"><span data-stu-id="58b0a-160">See your Logic App in action</span></span>
<span data-ttu-id="58b0a-161">hello 遠端監視預先設定的解決方案都有兩個規則時，設定預設您佈建的方案。</span><span class="sxs-lookup"><span data-stu-id="58b0a-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="58b0a-162">這兩個規則都位於 hello **SampleDevice001**裝置：</span><span class="sxs-lookup"><span data-stu-id="58b0a-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="58b0a-163">溫度 > 38.00</span><span class="sxs-lookup"><span data-stu-id="58b0a-163">Temperature > 38.00</span></span>
* <span data-ttu-id="58b0a-164">溼度 > 48.00</span><span class="sxs-lookup"><span data-stu-id="58b0a-164">Humidity > 48.00</span></span>

<span data-ttu-id="58b0a-165">hello 溫度規則會觸發 hello**引發警示**動作和 hello 溼度規則會觸發 hello **SendMessage**動作。</span><span class="sxs-lookup"><span data-stu-id="58b0a-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="58b0a-166">假設您使用 hello 相同的 URL，這兩個動作 hello **ActionRepository**類別，邏輯應用程式觸發程序，針對任何一項規則。</span><span class="sxs-lookup"><span data-stu-id="58b0a-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="58b0a-167">這兩個規則使用 SendGrid toosend 電子郵件 toohello**至**hello 警示的詳細資料的位址。</span><span class="sxs-lookup"><span data-stu-id="58b0a-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="58b0a-168">hello 邏輯應用程式會繼續 tootrigger，每次達到 hello 門檻。</span><span class="sxs-lookup"><span data-stu-id="58b0a-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="58b0a-169">tooavoid 不必要的電子郵件，您可以將停用 hello 規則在您的方案入口網站或停用 hello 邏輯應用程式在 hello [Azure 入口網站][lnk-azureportal]。</span><span class="sxs-lookup"><span data-stu-id="58b0a-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="58b0a-170">此外 tooreceiving 電子郵件，您也可以查看在 hello 入口網站中的 hello 邏輯應用程式執行時：</span><span class="sxs-lookup"><span data-stu-id="58b0a-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="58b0a-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58b0a-171">Next steps</span></span>
<span data-ttu-id="58b0a-172">既然您已使用邏輯應用程式 tooconnect 預先設定的 hello 方案 tooa 商務程序，您可以深入了解自訂 hello 預先設定的解決方案 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="58b0a-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="58b0a-173">[使用動態遙測以 hello 遠端監視預先設定的解決方案][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="58b0a-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="58b0a-174">[裝置資訊的中繼資料中 hello 遠端監視預先設定的解決方案][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="58b0a-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
