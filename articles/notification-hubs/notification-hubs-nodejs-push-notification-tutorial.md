---
title: "使用 Azure 通知中樞和 Node.js 傳送推播通知"
description: "了解如何使用通知中樞，從 Node.js 應用程式傳送推播通知。"
keywords: "推播通知, 推播通知, node.js 推播,ios 推播"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="ac202-104">使用 Azure 通知中樞和 Node.js 傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="ac202-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="ac202-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ac202-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ac202-106">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac202-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ac202-107">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac202-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ac202-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs)。</span><span class="sxs-lookup"><span data-stu-id="ac202-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="ac202-109">本指南將會示範如何透過 Azure 通知中樞的協助，直接從 Node.js 應用程式傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="ac202-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="ac202-110">涵蓋的案例包括在下列平台將推播通知傳送至應用程式：</span><span class="sxs-lookup"><span data-stu-id="ac202-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="ac202-111">Android</span><span class="sxs-lookup"><span data-stu-id="ac202-111">Android</span></span>
* <span data-ttu-id="ac202-112">iOS</span><span class="sxs-lookup"><span data-stu-id="ac202-112">iOS</span></span>
* <span data-ttu-id="ac202-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ac202-113">Windows Phone</span></span>
* <span data-ttu-id="ac202-114">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="ac202-114">Universal Windows Platform</span></span> 

<span data-ttu-id="ac202-115">如需通知中心的詳細資訊，請參閱 [後續步驟](#next) 一節。</span><span class="sxs-lookup"><span data-stu-id="ac202-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="ac202-116">什麼是通知中心？</span><span class="sxs-lookup"><span data-stu-id="ac202-116">What are Notification Hubs?</span></span>
<span data-ttu-id="ac202-117">Azure 通知中樞提供易用、多平台、可調整的基礎結構，用以將推播通知傳送至行動裝置。</span><span class="sxs-lookup"><span data-stu-id="ac202-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="ac202-118">如需服務基礎結構的詳細資訊，請參閱 [Azure 通知中樞](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) 頁面。</span><span class="sxs-lookup"><span data-stu-id="ac202-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="ac202-119">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac202-119">Create a Node.js Application</span></span>
<span data-ttu-id="ac202-120">本教學課程的第一個步驟是建立新的空白 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac202-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="ac202-121">如需有關建立 Node.js 應用程式的指示，請參閱[建立 Node.js 應用程式並將其部署到 Azure 網站][nodejswebsite]、使用 Windows PowerShell 的 [Node.js 雲端服務][Node.js Cloud Service]，或[使用 WebMatrix 的網站]。</span><span class="sxs-lookup"><span data-stu-id="ac202-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="ac202-122">將應用程式設為使用通知中樞</span><span class="sxs-lookup"><span data-stu-id="ac202-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="ac202-123">若要使用 Azur通知中樞，您需要下載並使用 Node.js [azure 封裝](https://www.npmjs.com/package/azure)，這包含一組內建的協助程式庫，能與推播通知 REST 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="ac202-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="ac202-124">使用 Node Package Manager (NPM) 取得封裝</span><span class="sxs-lookup"><span data-stu-id="ac202-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="ac202-125">使用命令列介面 (例如 **PowerShell** (Windows)、**終端機** (Mac) 或 **Bash** (Linux))，瀏覽至建立空白應用程式所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ac202-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="ac202-126">在命令視窗中輸入 **npm install azure-sb** 。</span><span class="sxs-lookup"><span data-stu-id="ac202-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="ac202-127">您可以手動執行 **ls** 或 **dir** 命令，確認已建立 **node\_modules** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ac202-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="ac202-128">在該資料夾內，找出 **azure** 套件，此套件包含您存取「通知中樞」所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="ac202-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ac202-129">您可以從官方 [NPM 部落格](http://blog.npmjs.org/post/85484771375/how-to-install-npm)進一步了解如何安裝 NPM。</span><span class="sxs-lookup"><span data-stu-id="ac202-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="ac202-130">匯入模組</span><span class="sxs-lookup"><span data-stu-id="ac202-130">Import the module</span></span>
<span data-ttu-id="ac202-131">使用文字編輯器，將以下內容新增至應用程式的 **server.js** 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="ac202-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="ac202-132">設定 Azure 通知中樞連線</span><span class="sxs-lookup"><span data-stu-id="ac202-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="ac202-133">**NotificationHubService** 物件可讓您使用通知中心。</span><span class="sxs-lookup"><span data-stu-id="ac202-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="ac202-134">下列程式碼會為名為 **hubname** 的通知中樞建立 **NotificationHubService** 物件。</span><span class="sxs-lookup"><span data-stu-id="ac202-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="ac202-135">請將程式碼新增至 **server.js** 檔案的頂端附近，放置在匯入 azure 模型的陳述式後方：</span><span class="sxs-lookup"><span data-stu-id="ac202-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="ac202-136">執行下列步驟，即可從 **Azure 入口網站** 取得連線的 [connectionstring] 值：</span><span class="sxs-lookup"><span data-stu-id="ac202-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="ac202-137">在左導覽窗格中，按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="ac202-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="ac202-138">選取 [通知中樞] ，然後尋找您要用於範例的中樞。</span><span class="sxs-lookup"><span data-stu-id="ac202-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="ac202-139">如果您需要建立新通知中樞的說明，您可以參考 [Windows 市集開始使用教學課程](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 。</span><span class="sxs-lookup"><span data-stu-id="ac202-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="ac202-140">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="ac202-140">Select **Settings**.</span></span>
4. <span data-ttu-id="ac202-141">按一下 [存取原則] 。</span><span class="sxs-lookup"><span data-stu-id="ac202-141">Click on **Access Policies**.</span></span> <span data-ttu-id="ac202-142">您會看到兩個共用和完整存取連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac202-142">You will see both shared and full access connection strings.</span></span>

![Azure 入口網站 - 通知中樞](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="ac202-144">您也可以使用 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 所提供的 **Get-AzureSbNamespace** Cmdlet，或搭配 [Azure 命令列介面 (Azure CLI)](../cli-install-nodejs.md) 使用 **azure sb namespace show** 命令，來擷取連接字串。</span><span class="sxs-lookup"><span data-stu-id="ac202-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="ac202-145">一般架構</span><span class="sxs-lookup"><span data-stu-id="ac202-145">General architecture</span></span>
<span data-ttu-id="ac202-146">**NotificationHubService** 物件會公開下列可將推播通知傳送至特定裝置和應用程式的物件執行個體：</span><span class="sxs-lookup"><span data-stu-id="ac202-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="ac202-147">**Android** - 請使用 **GcmService** 物件，此物件可從 **notificationHubService.gcm** 取得</span><span class="sxs-lookup"><span data-stu-id="ac202-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="ac202-148">**iOS** - 請使用 **ApnsService** 物件，此物件可從 **notificationHubService.apns** 存取</span><span class="sxs-lookup"><span data-stu-id="ac202-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="ac202-149">**Windows Phone** - 請使用 **MpnsService** 物件，此物件可從 **notificationHubService.mpns** 取得</span><span class="sxs-lookup"><span data-stu-id="ac202-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="ac202-150">**通用 Windows 平台** - 請使用 **WnsService** 物件，此物件可從 **notificationHubService.wns** 取得</span><span class="sxs-lookup"><span data-stu-id="ac202-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="ac202-151">做法：將推播通知傳送至 Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac202-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="ac202-152">**GcmService** 物件會提供可用來將推播通知傳送至 Android 應用程式的 **send** 方法。</span><span class="sxs-lookup"><span data-stu-id="ac202-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="ac202-153">此 **send** 方法可接受下列參數：</span><span class="sxs-lookup"><span data-stu-id="ac202-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="ac202-154">**Tags** - 標籤識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac202-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="ac202-155">若未提供標籤，通知將會傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac202-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="ac202-156">**Payload** - 訊息的 JSON 或原始字串承載。</span><span class="sxs-lookup"><span data-stu-id="ac202-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="ac202-157">**Callback** - 回呼函數。</span><span class="sxs-lookup"><span data-stu-id="ac202-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="ac202-158">如需有關裝載格式的詳細資訊，請參閱 **Implementing GCM Server (實作 GCM 伺服器)** 文件的 [Payload (承載)](http://developer.android.com/google/gcm/server.html#payload) 一節。</span><span class="sxs-lookup"><span data-stu-id="ac202-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="ac202-159">下列程式碼會使用 **NotificationHubService** 所公開的 **GcmService** 執行個體，將推播通知傳送至所有註冊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac202-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="ac202-160">做法：將推播通知傳送至 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac202-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="ac202-161">與上述的 Android 應用程式一樣，**ApnsService** 物件會提供可用來將推播通知傳送至 iOS 應用程式的 **send** 方法。</span><span class="sxs-lookup"><span data-stu-id="ac202-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="ac202-162">此 **send** 方法可接受下列參數：</span><span class="sxs-lookup"><span data-stu-id="ac202-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="ac202-163">**Tags** - 標籤識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac202-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="ac202-164">若未提供標籤，通知將會傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac202-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="ac202-165">**Payload** - 訊息的 JSON 或字串承載。</span><span class="sxs-lookup"><span data-stu-id="ac202-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="ac202-166">**Callback** - 回呼函數。</span><span class="sxs-lookup"><span data-stu-id="ac202-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="ac202-167">如需有關承載格式的詳細資訊，請參閱 **Local and Push Notification Programming Guide (本機與推播通知程式設計指南)** 文件的 [Notification Payload (通知承載)](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) 一節。</span><span class="sxs-lookup"><span data-stu-id="ac202-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="ac202-168">下列程式碼會使用 **NotificationHubService** 所公開的 **ApnsService** 執行個體，將警示訊息傳送至所有用戶端：</span><span class="sxs-lookup"><span data-stu-id="ac202-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="ac202-169">做法：將推播通知傳送至 Windows Phone 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac202-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="ac202-170">**MpnsService** 物件會提供可用來將推播通知傳送至 Windows Phone 應用程式的 **send** 方法。</span><span class="sxs-lookup"><span data-stu-id="ac202-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="ac202-171">此 **send** 方法可接受下列參數：</span><span class="sxs-lookup"><span data-stu-id="ac202-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="ac202-172">**Tags** - 標籤識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac202-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="ac202-173">若未提供標籤，通知將會傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac202-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="ac202-174">**Payload** - 訊息的 XML 承載。</span><span class="sxs-lookup"><span data-stu-id="ac202-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="ac202-175">**TargetName** - 快顯通知的 `toast`。</span><span class="sxs-lookup"><span data-stu-id="ac202-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="ac202-176">`token` 代表磚通知。</span><span class="sxs-lookup"><span data-stu-id="ac202-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="ac202-177">**NotificationClass** - 通知的優先順序。</span><span class="sxs-lookup"><span data-stu-id="ac202-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="ac202-178">如需有效值，請參閱[來自伺服器的推播通知](http://msdn.microsoft.com/library/hh221551.aspx)文件的＜HTTP 標頭元素＞一節。</span><span class="sxs-lookup"><span data-stu-id="ac202-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="ac202-179">**Options** - 選用的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="ac202-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="ac202-180">**Callback** - 回呼函數。</span><span class="sxs-lookup"><span data-stu-id="ac202-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="ac202-181">如需有效 **TargetName**、**NotificationClass** 及標頭選項的清單，請參閱[來自伺服器的推播通知](http://msdn.microsoft.com/library/hh221551.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="ac202-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="ac202-182">下列範例程式碼會使用 **NotificationHubService** 所公開的 **MpnsService** 執行個體來傳送快顯推播通知：</span><span class="sxs-lookup"><span data-stu-id="ac202-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="ac202-183">做法：將推播通知傳送至通用 Windows 平台 (UWP) 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac202-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="ac202-184">**WnsService** 物件會提供可用來將推播通知傳送至「通用 Windows 平台」應用程式的 **send** 方法。</span><span class="sxs-lookup"><span data-stu-id="ac202-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="ac202-185">此 **send** 方法可接受下列參數：</span><span class="sxs-lookup"><span data-stu-id="ac202-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="ac202-186">**Tags** - 標籤識別碼。</span><span class="sxs-lookup"><span data-stu-id="ac202-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="ac202-187">若未提供標籤，通知將會傳送至所有註冊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac202-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="ac202-188">**Payload** - XML 訊息承載。</span><span class="sxs-lookup"><span data-stu-id="ac202-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="ac202-189">**Type** - 通知類型。</span><span class="sxs-lookup"><span data-stu-id="ac202-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="ac202-190">**Options** - 選用的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="ac202-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="ac202-191">**Callback** - 回呼函數。</span><span class="sxs-lookup"><span data-stu-id="ac202-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="ac202-192">如需有效類型和要求標頭的清單，請參閱 [推播通知服務要求和回應標頭](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ac202-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="ac202-193">下列程式碼會使用 **NotificationHubService** 所公開的 **WnsService** 執行個體，將快顯推播通知傳送至 UWP 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ac202-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="ac202-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac202-194">Next Steps</span></span>
<span data-ttu-id="ac202-195">上述的範例程式碼片段可讓您輕鬆地建置服務基礎結構，將推播通知傳遞到各種裝置。</span><span class="sxs-lookup"><span data-stu-id="ac202-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="ac202-196">了解基本的透過 node.js 的通知中樞使用方式之後，請參考下列連結以了解如何進一步延伸這些功能。</span><span class="sxs-lookup"><span data-stu-id="ac202-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="ac202-197">請參閱 [Azure 通知中樞](https://msdn.microsoft.com/library/azure/jj927170.aspx)的 MSDN 參考。</span><span class="sxs-lookup"><span data-stu-id="ac202-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="ac202-198">造訪 GitHub 上的 [Azure SDK for Node] 儲存機制，以取得更多範例和實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ac202-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="ac202-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="ac202-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
<span data-ttu-id="ac202-200">[使用 WebMatrix 的網站]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="ac202-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="ac202-201">[connectionstring]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ac202-201">[Azure Portal]: https://portal.azure.com</span></span>
