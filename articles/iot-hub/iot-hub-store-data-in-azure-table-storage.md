---
title: "aaaSave IoT 中樞訊息 tooAzure 資料存放區 |Microsoft 文件"
description: "使用 Azure 的函式應用程式 toosave 您的 IoT 中樞訊息 tooyour Azure 資料表儲存體。 hello IoT 中樞訊息包含的資訊，例如傳送從 IoT 裝置感應器資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 資料儲存體, iot 感應器資料存儲存體"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="ccc34-105">儲存包含感應器資料 tooyour Azure 資料表儲存體的 IoT 中樞訊息</span><span class="sxs-lookup"><span data-stu-id="ccc34-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="ccc34-107">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ccc34-107">What you learn</span></span>

<span data-ttu-id="ccc34-108">您了解如何 toocreate Azure 儲存體帳戶和 Azure 函式應用程式在您的資料表儲存體 toostore IoT 中樞訊息。</span><span class="sxs-lookup"><span data-stu-id="ccc34-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ccc34-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="ccc34-109">What you do</span></span>

- <span data-ttu-id="ccc34-110">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccc34-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="ccc34-111">準備您的 IoT 中樞連接 tooread 訊息。</span><span class="sxs-lookup"><span data-stu-id="ccc34-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="ccc34-112">建立並部署 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ccc34-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="ccc34-113">What you need</span></span>

- <span data-ttu-id="ccc34-114">[將裝置設定](iot-hub-raspberry-pi-kit-node-get-started.md)toocover hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="ccc34-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="ccc34-115">作用中的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ccc34-115">An active Azure subscription</span></span>
  - <span data-ttu-id="ccc34-116">您訂用帳戶下的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="ccc34-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="ccc34-117">執行的應用程式所傳送訊息 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="ccc34-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ccc34-118">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ccc34-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="ccc34-119">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **儲存體** > **儲存體帳戶** >  **建立**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="ccc34-120">輸入 hello hello 儲存體帳戶的必要資訊：</span><span class="sxs-lookup"><span data-stu-id="ccc34-120">Enter hello necessary information for hello storage account:</span></span>

   ![在 hello Azure 入口網站中建立儲存體帳戶](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="ccc34-122">**名稱**: hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ccc34-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="ccc34-123">hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="ccc34-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="ccc34-124">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ccc34-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="ccc34-125">**Pin toodashboard**： 選取此選項，讓您輕鬆存取 tooyour IoT 中樞從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="ccc34-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="ccc34-126">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="ccc34-127">準備您的 IoT 中樞連接 tooread 訊息</span><span class="sxs-lookup"><span data-stu-id="ccc34-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="ccc34-128">IoT 中樞公開內建事件中樞相容端點 tooenable 應用程式 tooread IoT 中樞訊息。</span><span class="sxs-lookup"><span data-stu-id="ccc34-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="ccc34-129">同時，應用程式使用 IoT 中樞取用者群組 tooread 資料。</span><span class="sxs-lookup"><span data-stu-id="ccc34-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="ccc34-130">從您的 IoT 中樞建立 Azure 的函式應用程式 tooread 資料之前，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="ccc34-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="ccc34-131">收到 hello 的 IoT 中心端點的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ccc34-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="ccc34-132">為 IoT 中樞建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="ccc34-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="ccc34-133">取得 hello 的 IoT 中心端點的連接字串</span><span class="sxs-lookup"><span data-stu-id="ccc34-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="ccc34-134">開啟 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ccc34-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="ccc34-135">在 hello **IoT 中樞**窗格下**傳訊**，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="ccc34-136">在 hello 右窗格中，在**內建端點**，按一下 **事件**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="ccc34-137">在 hello**屬性**窗格中，注意 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="ccc34-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="ccc34-138">事件中樞相容端點</span><span class="sxs-lookup"><span data-stu-id="ccc34-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="ccc34-139">事件中樞相容名稱</span><span class="sxs-lookup"><span data-stu-id="ccc34-139">Event hub-compatible name</span></span>

   ![取得在 hello Azure 入口網站中的 hello 的 IoT 中心端點的連接字串](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="ccc34-141">在 hello **IoT 中樞**窗格下**設定**，按一下 **共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="ccc34-142">按一下 [iothubowner]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="ccc34-143">請注意 hello**主索引鍵**值。</span><span class="sxs-lookup"><span data-stu-id="ccc34-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="ccc34-144">建立 IoT 中心端點 hello 連接字串，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ccc34-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="ccc34-145">取代`<Event Hub-compatible endpoint>`和`<Primary key>`與您先前記下的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="ccc34-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="ccc34-146">為 IoT 中樞建立取用者群組</span><span class="sxs-lookup"><span data-stu-id="ccc34-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="ccc34-147">開啟 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ccc34-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="ccc34-148">在 hello **IoT 中樞**窗格下**傳訊**，按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="ccc34-149">在 hello 右窗格中，在**內建端點**，按一下 **事件**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="ccc34-150">在 hello**屬性**窗格下**取用者群組**，輸入名稱，然後記下它。</span><span class="sxs-lookup"><span data-stu-id="ccc34-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="ccc34-151">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="ccc34-152">建立並部署 Azure 函式應用程式</span><span class="sxs-lookup"><span data-stu-id="ccc34-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="ccc34-153">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **計算** > **函式應用程式** >  **建立**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="ccc34-154">輸入 hello 的 hello 函式應用程式的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="ccc34-154">Enter hello necessary information for hello function app.</span></span>

   ![在 hello Azure 入口網站中建立函式應用程式](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="ccc34-156">**應用程式名稱**: hello 的 hello 函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ccc34-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="ccc34-157">hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="ccc34-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="ccc34-158">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ccc34-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="ccc34-159">**儲存體帳戶**: hello 您所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccc34-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="ccc34-160">**Pin toodashboard**： 核取此選項，讓您輕鬆存取 toohello 函式應用程式從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="ccc34-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="ccc34-161">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-161">Click **Create**.</span></span>

4. <span data-ttu-id="ccc34-162">建立 hello 函式應用程式之後，請開啟它。</span><span class="sxs-lookup"><span data-stu-id="ccc34-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="ccc34-163">在 hello 函式應用程式，建立新的函式執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ccc34-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="ccc34-164">a.</span><span class="sxs-lookup"><span data-stu-id="ccc34-164">a.</span></span> <span data-ttu-id="ccc34-165">按一下 [新函式]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-165">Click **New Function**.</span></span>

   <span data-ttu-id="ccc34-166">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-166">b.</span></span> <span data-ttu-id="ccc34-167">選取 [JavaScript] 作為 [語言]，選取 [資料處理] 作為 [案例]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="ccc34-168">c.</span><span class="sxs-lookup"><span data-stu-id="ccc34-168">c.</span></span> <span data-ttu-id="ccc34-169">按一下 建立此函式，然後按一下新增函式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="ccc34-170">d.</span><span class="sxs-lookup"><span data-stu-id="ccc34-170">d.</span></span> <span data-ttu-id="ccc34-171">選取**JavaScript** hello 語言和**資料處理**hello 案例。</span><span class="sxs-lookup"><span data-stu-id="ccc34-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="ccc34-172">e.</span><span class="sxs-lookup"><span data-stu-id="ccc34-172">e.</span></span> <span data-ttu-id="ccc34-173">按一下 hello **EventHubTrigger JavaScript**範本。</span><span class="sxs-lookup"><span data-stu-id="ccc34-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="ccc34-174">f.</span><span class="sxs-lookup"><span data-stu-id="ccc34-174">f.</span></span> <span data-ttu-id="ccc34-175">輸入 hello hello 範本所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="ccc34-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="ccc34-176">**命名您的函式**: hello hello 函式名稱。</span><span class="sxs-lookup"><span data-stu-id="ccc34-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="ccc34-177">**事件中樞名稱**: hello 您先前記下事件中樞相容名稱。</span><span class="sxs-lookup"><span data-stu-id="ccc34-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="ccc34-178">**事件中樞連線**: tooadd hello 連接字串 hello 您建立 IoT 中心端點按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="ccc34-179">g.</span><span class="sxs-lookup"><span data-stu-id="ccc34-179">g.</span></span> <span data-ttu-id="ccc34-180">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-180">Click **Create**.</span></span>

6. <span data-ttu-id="ccc34-181">藉由 hello 下列設定 hello 函式的輸出：</span><span class="sxs-lookup"><span data-stu-id="ccc34-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="ccc34-182">a.</span><span class="sxs-lookup"><span data-stu-id="ccc34-182">a.</span></span> <span data-ttu-id="ccc34-183">按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![在 hello Azure 入口網站中加入資料表儲存體 tooyour 函式應用程式](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="ccc34-185">b.</span><span class="sxs-lookup"><span data-stu-id="ccc34-185">b.</span></span> <span data-ttu-id="ccc34-186">輸入 hello 的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="ccc34-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="ccc34-187">**資料表參數名稱**： 使用`outputTable`，用來在 Azure 的 hello 函式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ccc34-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="ccc34-188">**資料表名稱**：使用 `deviceData`。</span><span class="sxs-lookup"><span data-stu-id="ccc34-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="ccc34-189">**儲存體帳戶連線**︰按一下 [新增]，然後選取或輸入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccc34-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="ccc34-190">如果未顯示 hello 儲存體帳戶，請參閱[儲存體帳戶的需求](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)。</span><span class="sxs-lookup"><span data-stu-id="ccc34-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="ccc34-191">c.</span><span class="sxs-lookup"><span data-stu-id="ccc34-191">c.</span></span> <span data-ttu-id="ccc34-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-192">Click **Save**.</span></span>

7. <span data-ttu-id="ccc34-193">在 [觸發程序] 底下，按一下 [Azure 事件中樞 (eventHubMessages)]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="ccc34-194">在下**事件中樞取用者群組**，輸入 hello 取用者群組，您建立，然後按一下 hello 名稱**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ccc34-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="ccc34-195">按一下您已建立剩餘的 hello 的 hello 函式，然後按一下**檢視檔案**hello 右上。</span><span class="sxs-lookup"><span data-stu-id="ccc34-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="ccc34-196">中的 hello 程式碼取代`index.js`hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ccc34-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="ccc34-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccc34-197">Click **Save**.</span></span>

<span data-ttu-id="ccc34-198">您現在已建立 hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-198">You have now created hello function app.</span></span> <span data-ttu-id="ccc34-199">它會將 IoT 中樞收到的訊息儲存在您的表格儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ccc34-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc34-200">您可以使用 hello**執行**按鈕 tootest hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="ccc34-201">當您按一下**執行**，tooyour IoT 中樞傳送 hello 測試訊息。</span><span class="sxs-lookup"><span data-stu-id="ccc34-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="ccc34-202">hello 抵達的 hello 訊息應該 hello 函式應用程式 toostart 觸發程序，然後再儲存 hello 訊息 tooyour 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="ccc34-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="ccc34-203">hello**記錄**窗格記錄 hello hello 程序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ccc34-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="ccc34-204">確認訊息位於資料表儲存體中</span><span class="sxs-lookup"><span data-stu-id="ccc34-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="ccc34-205">在您裝置 toosend 訊息 tooyour IoT 中樞執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccc34-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="ccc34-206">[下載並安裝 Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="ccc34-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="ccc34-207">開啟 [儲存體總管] 中，按一下**新增 Azure 帳戶** > **登入**，再於 tooyour Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="ccc34-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="ccc34-208">按一下您的 Azure 訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [資料表] > [deviceData]。</span><span class="sxs-lookup"><span data-stu-id="ccc34-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="ccc34-209">您應該會看到從登入 hello 您裝置 tooyour IoT 中樞傳送的訊息`deviceData`資料表。</span><span class="sxs-lookup"><span data-stu-id="ccc34-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccc34-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccc34-210">Next steps</span></span>

<span data-ttu-id="ccc34-211">您已成功建立 Azure 儲存體帳戶和 Azure 函式應用程式，以將您的 IoT 中樞收到的訊息儲存在表格儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ccc34-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
