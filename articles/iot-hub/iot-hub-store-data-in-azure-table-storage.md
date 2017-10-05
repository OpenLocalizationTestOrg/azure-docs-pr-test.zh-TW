---
title: "將 IoT 中樞訊息儲存至 Azure 資料儲存體 | Microsoft Docs"
description: "使用 Azure 函式應用程式將 IoT 中樞訊息儲存到 Azure 表格儲存體。 IoT 中樞訊息包含從 IoT 裝置傳送的資訊，例如感應器資料。"
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
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="3f4a4-105">將包含感應器資料的 IoT 中樞訊息儲存到 Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="3f4a4-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="3f4a4-107">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="3f4a4-107">What you learn</span></span>

<span data-ttu-id="3f4a4-108">您會了解如何建立 Azure 儲存體帳戶和 Azure 函式應用程式，以將 IoT 中樞訊息儲存在 Azure 表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3f4a4-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="3f4a4-109">What you do</span></span>

- <span data-ttu-id="3f4a4-110">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="3f4a4-111">準備 IoT 中樞連線以讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="3f4a4-112">建立並部署 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3f4a4-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3f4a4-113">What you need</span></span>

- <span data-ttu-id="3f4a4-114">[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)以涵蓋下列需求︰</span><span class="sxs-lookup"><span data-stu-id="3f4a4-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="3f4a4-115">作用中的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f4a4-115">An active Azure subscription</span></span>
  - <span data-ttu-id="3f4a4-116">您訂用帳戶下的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3f4a4-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="3f4a4-117">將訊息傳送到 IoT 中樞的執行中應用程式</span><span class="sxs-lookup"><span data-stu-id="3f4a4-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="3f4a4-118">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3f4a4-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="3f4a4-119">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [新增] > [儲存體] > [儲存體帳戶] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="3f4a4-120">輸入儲存體帳戶的必要資訊︰</span><span class="sxs-lookup"><span data-stu-id="3f4a4-120">Enter the necessary information for the storage account:</span></span>

   ![在 Azure 入口網站中建立儲存體帳戶](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="3f4a4-122">**名稱**︰儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="3f4a4-123">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="3f4a4-124">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="3f4a4-125">**釘選到儀表板**：選取此選項可讓您從儀表板輕鬆地存取 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="3f4a4-126">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="3f4a4-127">準備 IoT 中樞連線以讀取訊息</span><span class="sxs-lookup"><span data-stu-id="3f4a4-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="3f4a4-128">IoT 中樞會公開內建的事件中樞相容端點，以便讓應用程式能夠讀取 IoT 中樞訊息。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="3f4a4-129">同時，應用程式會使用取用者群組從 IoT 中樞讀取資料。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="3f4a4-130">在建立 Azure 函式應用程式以從 IoT 中樞讀取資料之前，您必須執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="3f4a4-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="3f4a4-131">取得 IoT 中樞端點的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="3f4a4-132">為 IoT 中樞建立取用者群組。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="3f4a4-133">取得 IoT 中樞端點的連接字串</span><span class="sxs-lookup"><span data-stu-id="3f4a4-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="3f4a4-134">開啟 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="3f4a4-135">在 [IoT 中樞] 窗格上，按一下 [傳訊] 底下的 [端點]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="3f4a4-136">在右窗格中，按一下 [內建端點] 底下的 [事件]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="3f4a4-137">記下 [屬性] 窗格的下列值︰</span><span class="sxs-lookup"><span data-stu-id="3f4a4-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="3f4a4-138">事件中樞相容端點</span><span class="sxs-lookup"><span data-stu-id="3f4a4-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="3f4a4-139">事件中樞相容名稱</span><span class="sxs-lookup"><span data-stu-id="3f4a4-139">Event hub-compatible name</span></span>

   ![在 Azure 入口網站中取得 IoT 中樞端點的連接字串](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="3f4a4-141">在 [IoT 中樞] 窗格上，按一下 [設定] 底下的 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="3f4a4-142">按一下 [iothubowner]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="3f4a4-143">請記下**主索引鍵**值。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="3f4a4-144">建立 IoT 中樞端點的連接字串，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3f4a4-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="3f4a4-145">以您之前記下的值取代 `<Event Hub-compatible endpoint>` 和 `<Primary key>`。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="3f4a4-146">為 IoT 中樞建立取用者群組</span><span class="sxs-lookup"><span data-stu-id="3f4a4-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="3f4a4-147">開啟 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="3f4a4-148">在 [IoT 中樞] 窗格上，按一下 [傳訊] 底下的 [端點]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="3f4a4-149">在右窗格中，按一下 [內建端點] 底下的 [事件]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="3f4a4-150">在 [屬性] 窗格中，於 [取用者群組] 底下輸入名稱，並記下該名稱。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="3f4a4-151">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="3f4a4-152">建立並部署 Azure 函式應用程式</span><span class="sxs-lookup"><span data-stu-id="3f4a4-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="3f4a4-153">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [新增] > [計算] > [函數應用程式] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="3f4a4-154">輸入函式應用程式的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-154">Enter the necessary information for the function app.</span></span>

   ![在 Azure 入口網站中建立函式應用程式](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="3f4a4-156">**應用程式名稱**︰函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="3f4a4-157">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="3f4a4-158">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="3f4a4-159">**儲存體帳戶**︰您建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="3f4a4-160">**釘選至儀表板**︰核取此選項可讓您從儀表板輕鬆地存取函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="3f4a4-161">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-161">Click **Create**.</span></span>

4. <span data-ttu-id="3f4a4-162">建立函式應用程式之後，請開啟它。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="3f4a4-163">在函式應用程式中，執行下列動作建立新的函式：</span><span class="sxs-lookup"><span data-stu-id="3f4a4-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="3f4a4-164">a.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-164">a.</span></span> <span data-ttu-id="3f4a4-165">按一下 [新函式]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-165">Click **New Function**.</span></span>

   <span data-ttu-id="3f4a4-166">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-166">b.</span></span> <span data-ttu-id="3f4a4-167">選取 [JavaScript] 作為 [語言]，選取 [資料處理] 作為 [案例]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="3f4a4-168">c.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-168">c.</span></span> <span data-ttu-id="3f4a4-169">按一下 [建立此函式]，然後按一下 [新增函式]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="3f4a4-170">d.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-170">d.</span></span> <span data-ttu-id="3f4a4-171">選取 [JavaScript] 作為 [語言]，選取 [資料處理] 作為 [情節]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="3f4a4-172">e.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-172">e.</span></span> <span data-ttu-id="3f4a4-173">按一下 **EventHubTrigger-JavaScript** 範本。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="3f4a4-174">f.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-174">f.</span></span> <span data-ttu-id="3f4a4-175">輸入範本的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="3f4a4-176">**替您的函式命名**：函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="3f4a4-177">**事件中樞名稱**：您之前記下的事件中樞相容名稱。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="3f4a4-178">**事件中樞連線**：按一下 [新增] 以新增您所建立之 IoT 中樞端點的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="3f4a4-179">g.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-179">g.</span></span> <span data-ttu-id="3f4a4-180">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-180">Click **Create**.</span></span>

6. <span data-ttu-id="3f4a4-181">執行下列作業以設定函式的輸出：</span><span class="sxs-lookup"><span data-stu-id="3f4a4-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="3f4a4-182">a.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-182">a.</span></span> <span data-ttu-id="3f4a4-183">按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![在 Azure 入口網站中將表格儲存體新增至函式應用程式](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="3f4a4-185">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-185">b.</span></span> <span data-ttu-id="3f4a4-186">輸入必要資訊。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="3f4a4-187">**資料表參數名稱**︰使用 `outputTable`，它會用於 Azure 函式的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="3f4a4-188">**資料表名稱**：使用 `deviceData`。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="3f4a4-189">**儲存體帳戶連線**︰按一下 [新增]，然後選取或輸入儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="3f4a4-190">如果未顯示儲存體帳戶，請參閱[儲存體帳戶的需求](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="3f4a4-191">c.</span><span class="sxs-lookup"><span data-stu-id="3f4a4-191">c.</span></span> <span data-ttu-id="3f4a4-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-192">Click **Save**.</span></span>

7. <span data-ttu-id="3f4a4-193">在 [觸發程序] 底下，按一下 [Azure 事件中樞 (eventHubMessages)]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="3f4a4-194">在 [事件中樞取用者群組] 底下，輸入您所建立之取用者群組的名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="3f4a4-195">按一下您在左側建立的函式，然後按一下右側的 [檢視檔案]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="3f4a4-196">以下列內容取代 `index.js` 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="3f4a4-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="3f4a4-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-197">Click **Save**.</span></span>

<span data-ttu-id="3f4a4-198">您現在建立了函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-198">You have now created the function app.</span></span> <span data-ttu-id="3f4a4-199">它會將 IoT 中樞收到的訊息儲存在您的表格儲存體中。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="3f4a4-200">您可以使用 [執行] 按鈕來測試函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="3f4a4-201">當您按一下 [執行]，系統就會將測試訊息傳送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="3f4a4-202">訊息送達時應該會觸發函式應用程式啟動，然後將訊息儲存至您的表格儲存體。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="3f4a4-203">[記錄] 窗格會記錄處理程序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="3f4a4-204">確認訊息位於資料表儲存體中</span><span class="sxs-lookup"><span data-stu-id="3f4a4-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="3f4a4-205">在裝置上執行應用程式範例以將訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="3f4a4-206">[下載並安裝 Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="3f4a4-207">開啟儲存體總管，按一下 [新增 Azure 帳戶] > [登入]，然後登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="3f4a4-208">按一下您的 Azure 訂用帳戶 > [儲存體帳戶] > 您的儲存體帳戶 > [資料表] > [deviceData]。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="3f4a4-209">您應該會看到從裝置傳送到 IoT 中樞的訊息記錄在 `deviceData` 資料表中。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f4a4-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f4a4-210">Next steps</span></span>

<span data-ttu-id="3f4a4-211">您已成功建立 Azure 儲存體帳戶和 Azure 函式應用程式，以將您的 IoT 中樞收到的訊息儲存在表格儲存體中。</span><span class="sxs-lookup"><span data-stu-id="3f4a4-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
