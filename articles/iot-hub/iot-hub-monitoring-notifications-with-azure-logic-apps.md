---
title: "搭配 Azure Logic Apps 進行 IoT 遠端監視和通知 | Microsoft Docs"
description: "使用 Azure Logic Apps 進行 IoT 中樞的 IoT 溫度監視，並對於偵測到的任何異常自動將電子郵件通知寄送到您的信箱。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 監視、iot 通知、iot 溫度監視"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="1208f-104">搭配連接 IoT 中樞和信箱的 Azure Logic Apps 進行 IoT 遠端監視和通知</span><span class="sxs-lookup"><span data-stu-id="1208f-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="1208f-106">Azure Logic Apps 可用來以一連串的步驟使程序自動進行。</span><span class="sxs-lookup"><span data-stu-id="1208f-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="1208f-107">邏輯應用程式可以連接多種服務和通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1208f-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="1208f-108">一開始會有觸發程序，例如「新增帳戶時」，後面接著一連串動作，例如「傳送推播通知」。</span><span class="sxs-lookup"><span data-stu-id="1208f-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="1208f-109">此功能可讓 Logic Apps 成為 IoT 監視的絕佳 IoT 解決方案，例如注意異常行為，以及其他使用情況。</span><span class="sxs-lookup"><span data-stu-id="1208f-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="1208f-110">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1208f-110">What you learn</span></span>

<span data-ttu-id="1208f-111">您學會如何建立連接 IoT 中樞和信箱的邏輯應用程式用於溫度監視和通知。</span><span class="sxs-lookup"><span data-stu-id="1208f-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="1208f-112">溫度超過 30°C 時，用戶端應用程式會在傳送到 IoT 中樞的訊息中標示 `temperatureAlert = "true"`。</span><span class="sxs-lookup"><span data-stu-id="1208f-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="1208f-113">該訊息會觸發邏輯應用程式傳送電子郵件通知給您。</span><span class="sxs-lookup"><span data-stu-id="1208f-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1208f-114">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="1208f-114">What you do</span></span>

* <span data-ttu-id="1208f-115">建立服務匯流排命名空間，並將佇列加入到服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="1208f-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="1208f-116">將端點和路由規則加入到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1208f-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="1208f-117">建立、設定和測試邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1208f-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1208f-118">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="1208f-118">What you need</span></span>

* <span data-ttu-id="1208f-119">完成涵蓋下列需求的[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)教學課程︰</span><span class="sxs-lookup"><span data-stu-id="1208f-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="1208f-120">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1208f-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="1208f-121">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1208f-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="1208f-122">將訊息傳送到您 Azure IoT 中樞的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1208f-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="1208f-123">建立服務匯流排命名空間，並將佇列加入到服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="1208f-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="1208f-124">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="1208f-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="1208f-125">在 [Azure 入口網站](https://portal.azure.com/)上，按一下 [新增] > [企業整合] > [服務匯流排]。</span><span class="sxs-lookup"><span data-stu-id="1208f-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="1208f-126">請提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1208f-126">Provide the following information:</span></span>

   <span data-ttu-id="1208f-127">**名稱**︰服務匯流排的名稱。</span><span class="sxs-lookup"><span data-stu-id="1208f-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="1208f-128">**定價層**︰ 按一下 [基本] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="1208f-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="1208f-129">「基本」層足供本教學課程之用。</span><span class="sxs-lookup"><span data-stu-id="1208f-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="1208f-130">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="1208f-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="1208f-131">**位置**：使用 IoT 中樞使用的同一個位置。</span><span class="sxs-lookup"><span data-stu-id="1208f-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="1208f-132">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1208f-132">Click **Create**.</span></span>

   ![在 Azure 入口網站中建立服務匯流排命名空間](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="1208f-134">新增服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="1208f-134">Add a service bus queue</span></span>

1. <span data-ttu-id="1208f-135">開啟服務匯流排命名空間，然後按一下 [+ 佇列]。</span><span class="sxs-lookup"><span data-stu-id="1208f-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="1208f-136">輸入佇列的名稱，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1208f-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="1208f-137">開啟服務匯流排佇列，然後按一下 [共用存取原則] > [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="1208f-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="1208f-138">輸入原則名稱，並勾選 [管理]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1208f-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![在 Azure 入口網站中新增服務匯流排佇列](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="1208f-140">將端點和路由規則新增到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="1208f-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="1208f-141">新增端點。</span><span class="sxs-lookup"><span data-stu-id="1208f-141">Add an endpoint</span></span>

1. <span data-ttu-id="1208f-142">開啟 IoT 中樞，並按一下 [端點] > [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="1208f-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="1208f-143">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="1208f-143">Enter the following information:</span></span>

   <span data-ttu-id="1208f-144">**名稱**：端點的名稱。</span><span class="sxs-lookup"><span data-stu-id="1208f-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="1208f-145">**端點類型**：選取**服務匯流排佇列**。</span><span class="sxs-lookup"><span data-stu-id="1208f-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="1208f-146">**服務匯流排命名空間**：選取您建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="1208f-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="1208f-147">**服務匯流排佇列**：選取您建立的佇列。</span><span class="sxs-lookup"><span data-stu-id="1208f-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="1208f-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1208f-148">Click **OK**.</span></span>

   ![將端點新增至 Azure 入口網站的 IoT 中樞](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="1208f-150">新增路由規則</span><span class="sxs-lookup"><span data-stu-id="1208f-150">Add a routing rule</span></span>

1. <span data-ttu-id="1208f-151">在 IoT 中樞，按一下 [路由] > [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="1208f-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="1208f-152">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="1208f-152">Enter the following information:</span></span>

   <span data-ttu-id="1208f-153">**名稱**：路由規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="1208f-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="1208f-154">**資料來源**：選取 [裝置訊息]。</span><span class="sxs-lookup"><span data-stu-id="1208f-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="1208f-155">**端點**：選取您建立的端點。</span><span class="sxs-lookup"><span data-stu-id="1208f-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="1208f-156">**查詢字串**：輸入 `temperatureAlert = "true"`。</span><span class="sxs-lookup"><span data-stu-id="1208f-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="1208f-157">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1208f-157">Click **Save**.</span></span>

   ![在 Azure 入口網站中新增路由規格](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="1208f-159">建立並設定邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="1208f-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="1208f-160">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="1208f-160">Create a logic app</span></span>

1. <span data-ttu-id="1208f-161">在[Azure 入口網站](https://portal.azure.com/)中，按一下 [新增] > [企業整合] > [邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1208f-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="1208f-162">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="1208f-162">Enter the following information:</span></span>

   <span data-ttu-id="1208f-163">**名稱**︰ 邏輯應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="1208f-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="1208f-164">**資源群組**︰使用 IoT 中樞所用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="1208f-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="1208f-165">**位置**：使用 IoT 中樞使用的同一個位置。</span><span class="sxs-lookup"><span data-stu-id="1208f-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="1208f-166">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1208f-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="1208f-167">設定邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="1208f-167">Configure the logic app</span></span>

1. <span data-ttu-id="1208f-168">開啟在邏輯應用程式設計工具中開啟的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1208f-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="1208f-169">在邏輯應用程式設計工具中，按一下 [空白邏輯應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1208f-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![在 Azure 入口網站中，從空白的邏輯應用程式開始。](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="1208f-171">按一下 [服務匯流排]。</span><span class="sxs-lookup"><span data-stu-id="1208f-171">Click **Service Bus**.</span></span>

   ![選取服務匯流排，開始在 Azure 入口網站中建立邏輯應用程式](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="1208f-173">按一下 [服務匯流排 – 一個或多個訊息到達佇列時 (自動完成)]。</span><span class="sxs-lookup"><span data-stu-id="1208f-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="1208f-174">建立服務匯流排連接。</span><span class="sxs-lookup"><span data-stu-id="1208f-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="1208f-175">輸入連線名稱。</span><span class="sxs-lookup"><span data-stu-id="1208f-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="1208f-176">按一下服務匯流排命名空間 > 服務匯流排原則 > [建立]。</span><span class="sxs-lookup"><span data-stu-id="1208f-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![在 Azure 入口網站中建立邏輯應用程式的服務匯流排連接](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="1208f-178">建立服務匯流排連接之後，按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="1208f-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="1208f-179">選取您建立的佇列，並對於 [最大訊息計數] 輸入 `175`</span><span class="sxs-lookup"><span data-stu-id="1208f-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![對於邏輯應用程式中的服務匯流排連接指定最大訊息計數](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="1208f-181">按一下 [儲存] 按鈕可儲存變更。</span><span class="sxs-lookup"><span data-stu-id="1208f-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="1208f-182">建立 SMTP 服務連接。</span><span class="sxs-lookup"><span data-stu-id="1208f-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="1208f-183">按一下 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="1208f-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="1208f-184">輸入 `SMTP`，並按一下搜尋結果中的 **SMTP** 服務，然後按一下 [SMTP - 傳送電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="1208f-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![在 Azure 入口網站的邏輯應用程式中建立 SMTP 連接](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="1208f-186">輸入您信箱的 SMTP 資訊，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1208f-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![在 Azure 入口網站的邏輯應用程式中輸入 SMTP 連接資訊](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="1208f-188">取得 [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970)、[Gmail](https://support.google.com/a/answer/176600?hl=en) 和 [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html) 的 SMTP 資訊。</span><span class="sxs-lookup"><span data-stu-id="1208f-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="1208f-189">輸入**寄件者**和**收件者**的電子郵件地址，並對於**主旨**和**內文**輸入 `High temperature detected`。</span><span class="sxs-lookup"><span data-stu-id="1208f-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="1208f-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1208f-190">Click **Save**.</span></span>

<span data-ttu-id="1208f-191">邏輯應用程式隨即在您儲存時開始運作。</span><span class="sxs-lookup"><span data-stu-id="1208f-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="1208f-192">測試邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="1208f-192">Test the logic app</span></span>

1. <span data-ttu-id="1208f-193">在 [將 ESP8266 連接到 Azure IoT 中樞](iot-hub-arduino-huzzah-esp8266-get-started.md) 中，啟動您部署至裝置的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1208f-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="1208f-194">將 SensorTag 周圍的環境溫度增加到 30°C 以上。例如，在 SensorTag 周圍點蠟燭。</span><span class="sxs-lookup"><span data-stu-id="1208f-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="1208f-195">您應該會收到邏輯應用程式傳送的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="1208f-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1208f-196">您的電子郵件服務提供者可能需要驗證寄件者身分，確定是您傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1208f-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1208f-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1208f-197">Next steps</span></span>

<span data-ttu-id="1208f-198">您已成功建立連接 IoT 中樞的邏輯應用程式，以及溫度監視和通知的信箱。</span><span class="sxs-lookup"><span data-stu-id="1208f-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
