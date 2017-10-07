---
title: "aaaIoT 遠端監視 Azure 邏輯應用程式使用與通知 |Microsoft 文件"
description: "Azure 邏輯應用程式使用的 IoT 溫度監控您的 IoT 中樞並自動傳送電子郵件通知 tooyour 信箱，偵測到任何異常情況。"
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
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="9933b-104">搭配連接 IoT 中樞和信箱的 Azure Logic Apps 進行 IoT 遠端監視和通知</span><span class="sxs-lookup"><span data-stu-id="9933b-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="9933b-106">Azure 邏輯應用程式提供方式 tooautomate 處理程序，為一系列的步驟。</span><span class="sxs-lookup"><span data-stu-id="9933b-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="9933b-107">邏輯應用程式可以連接多種服務和通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9933b-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="9933b-108">一開始會有觸發程序，例如「新增帳戶時」，後面接著一連串動作，例如「傳送推播通知」。</span><span class="sxs-lookup"><span data-stu-id="9933b-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="9933b-109">此功能可讓 Logic Apps 成為 IoT 監視的絕佳 IoT 解決方案，例如注意異常行為，以及其他使用情況。</span><span class="sxs-lookup"><span data-stu-id="9933b-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9933b-110">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="9933b-110">What you learn</span></span>

<span data-ttu-id="9933b-111">您了解如何 toocreate 邏輯應用程式連接您的 IoT 中樞和溫度監視和通知的信箱。</span><span class="sxs-lookup"><span data-stu-id="9933b-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="9933b-112">當 hello 溫度高於 30 C 時，hello 用戶端應用程式標記`temperatureAlert = "true"`hello 訊息中傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9933b-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="9933b-113">觸發程序 hello 邏輯應用程式 toosend hello 訊息您電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="9933b-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9933b-114">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="9933b-114">What you do</span></span>

* <span data-ttu-id="9933b-115">建立服務匯流排命名空間並加入佇列 tooit。</span><span class="sxs-lookup"><span data-stu-id="9933b-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="9933b-116">加入端點和路由規則 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9933b-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="9933b-117">建立、設定和測試邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9933b-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9933b-118">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="9933b-118">What you need</span></span>

* <span data-ttu-id="9933b-119">教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="9933b-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="9933b-120">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9933b-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="9933b-121">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9933b-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="9933b-122">用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9933b-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="9933b-123">建立服務匯流排命名空間，並加入佇列 tooit</span><span class="sxs-lookup"><span data-stu-id="9933b-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="9933b-124">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="9933b-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="9933b-125">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **企業整合** > **Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="9933b-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="9933b-126">提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="9933b-126">Provide hello following information:</span></span>

   <span data-ttu-id="9933b-127">**名稱**: hello service bus 的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9933b-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="9933b-128">**定價層**︰ 按一下 [基本] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="9933b-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="9933b-129">hello 基本層就足以應付本教學課程。</span><span class="sxs-lookup"><span data-stu-id="9933b-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="9933b-130">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9933b-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="9933b-131">**位置**： 使用 hello 相同 IoT 中樞使用的位置。</span><span class="sxs-lookup"><span data-stu-id="9933b-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="9933b-132">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9933b-132">Click **Create**.</span></span>

   ![在 hello Azure 入口網站中建立服務匯流排命名空間](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="9933b-134">新增服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="9933b-134">Add a service bus queue</span></span>

1. <span data-ttu-id="9933b-135">開啟 hello 服務匯流排命名空間，然後按一下**+ 佇列**。</span><span class="sxs-lookup"><span data-stu-id="9933b-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="9933b-136">輸入 hello 佇列的名稱，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9933b-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="9933b-137">開啟 hello 服務匯流排佇列，然後按一下**共用存取原則** > **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="9933b-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="9933b-138">輸入 hello 原則名稱，核取**管理**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9933b-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![在 hello Azure 入口網站中加入服務匯流排佇列](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="9933b-140">加入端點和路由規則 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="9933b-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="9933b-141">新增端點。</span><span class="sxs-lookup"><span data-stu-id="9933b-141">Add an endpoint</span></span>

1. <span data-ttu-id="9933b-142">開啟 IoT 中樞，並按一下 [端點] > [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="9933b-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="9933b-143">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="9933b-143">Enter hello following information:</span></span>

   <span data-ttu-id="9933b-144">**名稱**: hello hello 端點名稱。</span><span class="sxs-lookup"><span data-stu-id="9933b-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="9933b-145">**端點類型**：選取**服務匯流排佇列**。</span><span class="sxs-lookup"><span data-stu-id="9933b-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="9933b-146">**服務匯流排命名空間**： 選取您所建立的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="9933b-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="9933b-147">**Service Bus 佇列**: hello 選取您所建立的佇列。</span><span class="sxs-lookup"><span data-stu-id="9933b-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="9933b-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9933b-148">Click **OK**.</span></span>

   ![在 hello Azure 入口網站中加入端點 tooyour IoT 中樞](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="9933b-150">新增路由規則</span><span class="sxs-lookup"><span data-stu-id="9933b-150">Add a routing rule</span></span>

1. <span data-ttu-id="9933b-151">在 IoT 中樞，按一下 [路由] > [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="9933b-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="9933b-152">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="9933b-152">Enter hello following information:</span></span>

   <span data-ttu-id="9933b-153">**名稱**: hello hello 路由規則名稱。</span><span class="sxs-lookup"><span data-stu-id="9933b-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="9933b-154">**資料來源**：選取 [裝置訊息]。</span><span class="sxs-lookup"><span data-stu-id="9933b-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="9933b-155">**端點**： 選取您所建立的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="9933b-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="9933b-156">**查詢字串**：輸入 `temperatureAlert = "true"`。</span><span class="sxs-lookup"><span data-stu-id="9933b-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="9933b-157">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9933b-157">Click **Save**.</span></span>

   ![在 hello Azure 入口網站中加入的路由規則](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="9933b-159">建立並設定邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9933b-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="9933b-160">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9933b-160">Create a logic app</span></span>

1. <span data-ttu-id="9933b-161">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **企業整合** > **邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9933b-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="9933b-162">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="9933b-162">Enter hello following information:</span></span>

   <span data-ttu-id="9933b-163">**名稱**: hello hello 邏輯應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9933b-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="9933b-164">**資源群組**： 使用 hello 相同 IoT 中樞使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9933b-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="9933b-165">**位置**： 使用 hello 相同 IoT 中樞使用的位置。</span><span class="sxs-lookup"><span data-stu-id="9933b-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="9933b-166">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9933b-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="9933b-167">Hello 邏輯應用程式設定</span><span class="sxs-lookup"><span data-stu-id="9933b-167">Configure hello logic app</span></span>

1. <span data-ttu-id="9933b-168">開啟在 hello 邏輯應用程式的設計工具中開啟檔案的 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9933b-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="9933b-169">在 hello 邏輯應用程式的設計工具中，按一下 **空白邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9933b-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![開頭空白的邏輯中的應用程式 hello Azure 入口網站](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="9933b-171">按一下 [服務匯流排]。</span><span class="sxs-lookup"><span data-stu-id="9933b-171">Click **Service Bus**.</span></span>

   ![選取服務匯流排 toostart hello Azure 入口網站中建立邏輯應用程式](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="9933b-173">按一下 [服務匯流排 – 一個或多個訊息到達佇列時 (自動完成)]。</span><span class="sxs-lookup"><span data-stu-id="9933b-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="9933b-174">建立服務匯流排連接。</span><span class="sxs-lookup"><span data-stu-id="9933b-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="9933b-175">輸入連線名稱。</span><span class="sxs-lookup"><span data-stu-id="9933b-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="9933b-176">按一下 hello 服務匯流排命名空間 > hello 服務匯流排原則 >**建立**。</span><span class="sxs-lookup"><span data-stu-id="9933b-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![在 hello Azure 入口網站中建立應用程式邏輯的服務匯流排連線](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="9933b-178">按一下**繼續**hello 服務匯流排連線建立之後。</span><span class="sxs-lookup"><span data-stu-id="9933b-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="9933b-179">選取您建立的 hello 佇列，並輸入`175`如**最大訊息數**</span><span class="sxs-lookup"><span data-stu-id="9933b-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![指定在邏輯應用程式中的 hello 服務匯流排連線的 hello 最大訊息計數](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="9933b-181">按一下 [儲存] 按鈕 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="9933b-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="9933b-182">建立 SMTP 服務連接。</span><span class="sxs-lookup"><span data-stu-id="9933b-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="9933b-183">按一下 [新增步驟] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="9933b-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="9933b-184">型別`SMTP`，按一下 hello **SMTP**在 hello 搜尋結果中，服務，然後按一下**SMTP-傳送電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="9933b-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![在 hello Azure 入口網站中的應用程式邏輯中建立 SMTP 連接](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="9933b-186">輸入您的信箱，hello SMTP 資訊，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="9933b-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![在 hello Azure 入口網站中的應用程式邏輯中輸入 SMTP 連接資訊](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="9933b-188">取得 hello SMTP 資訊[Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970)， [Gmail](https://support.google.com/a/answer/176600?hl=en)，和[Yahoo 郵件](https://help.yahoo.com/kb/SLN4075.html)。</span><span class="sxs-lookup"><span data-stu-id="9933b-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="9933b-189">輸入**寄件者**和**收件者**的電子郵件地址，並對於**主旨**和**內文**輸入 `High temperature detected`。</span><span class="sxs-lookup"><span data-stu-id="9933b-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="9933b-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9933b-190">Click **Save**.</span></span>

<span data-ttu-id="9933b-191">hello 邏輯應用程式時將它儲存為工作順序。</span><span class="sxs-lookup"><span data-stu-id="9933b-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="9933b-192">測試 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="9933b-192">Test hello logic app</span></span>

1. <span data-ttu-id="9933b-193">開始部署 tooyour 裝置中的 hello 用戶端應用程式[連接 ESP8266 tooAzure IoT 中樞](iot-hub-arduino-huzzah-esp8266-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9933b-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="9933b-194">增加 hello 環境溫度周圍 hello SensorTag toobe 上方 30 c。例如，光周圍您 SensorTag k。</span><span class="sxs-lookup"><span data-stu-id="9933b-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="9933b-195">您應該會收到 hello 邏輯應用程式所傳送的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="9933b-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9933b-196">您的電子郵件服務提供者可能需要 tooverify hello 寄件者識別 toomake 確定這是您傳送嗨電子郵件的人員。</span><span class="sxs-lookup"><span data-stu-id="9933b-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9933b-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9933b-197">Next steps</span></span>

<span data-ttu-id="9933b-198">您已成功建立連接 IoT 中樞的邏輯應用程式，以及溫度監視和通知的信箱。</span><span class="sxs-lookup"><span data-stu-id="9933b-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
