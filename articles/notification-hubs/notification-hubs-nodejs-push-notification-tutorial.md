---
title: "Azure 通知中樞與 Node.js aaaSending 推播通知"
description: "了解如何 toouse 通知中樞 toosend 推播通知從 Node.js 應用程式。"
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
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="1e21b-104">使用 Azure 通知中樞和 Node.js 傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="1e21b-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="1e21b-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1e21b-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1e21b-106">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e21b-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1e21b-107">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e21b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1e21b-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs)。</span><span class="sxs-lookup"><span data-stu-id="1e21b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="1e21b-109">本指南將說明如何 toosend 推播通知與 hello 說明 Azure 通知中心直接從 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="1e21b-110">涵蓋的 hello 案例包括傳送推播通知 tooapplications hello 下列平台上：</span><span class="sxs-lookup"><span data-stu-id="1e21b-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="1e21b-111">Android</span><span class="sxs-lookup"><span data-stu-id="1e21b-111">Android</span></span>
* <span data-ttu-id="1e21b-112">iOS</span><span class="sxs-lookup"><span data-stu-id="1e21b-112">iOS</span></span>
* <span data-ttu-id="1e21b-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="1e21b-113">Windows Phone</span></span>
* <span data-ttu-id="1e21b-114">通用 Windows 平台</span><span class="sxs-lookup"><span data-stu-id="1e21b-114">Universal Windows Platform</span></span> 

<span data-ttu-id="1e21b-115">如需有關通知中樞的詳細資訊，請參閱 hello[接下來的步驟](#next)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1e21b-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="1e21b-116">什麼是通知中心？</span><span class="sxs-lookup"><span data-stu-id="1e21b-116">What are Notification Hubs?</span></span>
<span data-ttu-id="1e21b-117">Azure 通知中樞傳送推播通知 toomobile 裝置提供方便使用、 多平台、 可擴充的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="1e21b-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="1e21b-118">如需 hello 服務基礎結構的詳細資訊，請參閱 hello [Azure 通知中樞](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="1e21b-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="1e21b-119">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e21b-119">Create a Node.js Application</span></span>
<span data-ttu-id="1e21b-120">本教學課程中的 hello 第一個步驟，建立新的空白 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="1e21b-121">如需建立 Node.js 應用程式的指示，請參閱[建立及部署 Node.js 應用程式 tooAzure 網站][nodejswebsite]， [Node.js 雲端服務][Node.js Cloud Service]使用 Windows PowerShell 或[使用 WebMatrix 的網站]。</span><span class="sxs-lookup"><span data-stu-id="1e21b-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="1e21b-122">設定您的應用程式 tooUse 通知中樞</span><span class="sxs-lookup"><span data-stu-id="1e21b-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="1e21b-123">toouse Azure 通知中樞，您需要 toodownload 和使用 hello Node.js [azure 封裝](https://www.npmjs.com/package/azure)，其中包含一組內建的協助程式程式庫與 hello 推播通知 REST 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1e21b-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="1e21b-124">使用節點封裝管理員 (NPM) tooobtain hello 套件</span><span class="sxs-lookup"><span data-stu-id="1e21b-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="1e21b-125">使用命令列介面，例如**PowerShell** (Windows)**終端機**(Mac)，或**撞**(Linux)，瀏覽 toohello 資料夾建立空白的應用程式的位置.</span><span class="sxs-lookup"><span data-stu-id="1e21b-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="1e21b-126">型別**npm 安裝 azure sb** hello 命令視窗中。</span><span class="sxs-lookup"><span data-stu-id="1e21b-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="1e21b-127">您可以手動執行 hello **ls**或**dir**命令 tooverify，**節點\_模組**建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="1e21b-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="1e21b-128">在該資料夾中，找出 hello **azure**包含需要 tooaccess hello 程式庫套件 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="1e21b-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="1e21b-129">您可以進一步了解上 hello 官方安裝 NPM [NPM 部落格](http://blog.npmjs.org/post/85484771375/how-to-install-npm)。</span><span class="sxs-lookup"><span data-stu-id="1e21b-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="1e21b-130">匯入 hello 模組</span><span class="sxs-lookup"><span data-stu-id="1e21b-130">Import hello module</span></span>
<span data-ttu-id="1e21b-131">使用文字編輯器中，加入下列 toohello 頂端 hello hello**立即轉譯 server.js** hello 應用程式檔案：</span><span class="sxs-lookup"><span data-stu-id="1e21b-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="1e21b-132">設定 Azure 通知中樞連線</span><span class="sxs-lookup"><span data-stu-id="1e21b-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="1e21b-133">hello **NotificationHubService**物件可讓您使用通知中樞。</span><span class="sxs-lookup"><span data-stu-id="1e21b-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="1e21b-134">hello 下列程式碼會建立**NotificationHubService**物件名為 hello nofication 中樞**hubname**。</span><span class="sxs-lookup"><span data-stu-id="1e21b-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="1e21b-135">新增 hello hello 頂端附近**立即轉譯 server.js** hello 陳述式 tooimport hello azure 模組之後的檔案：</span><span class="sxs-lookup"><span data-stu-id="1e21b-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="1e21b-136">hello 連接**connectionstring**值可以取自 hello [Azure 入口網站]藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="1e21b-137">在 hello 左側瀏覽窗格中，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="1e21b-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="1e21b-138">選取**通知中樞**，，然後尋找 hello 中樞想 toouse hello 範例。</span><span class="sxs-lookup"><span data-stu-id="1e21b-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="1e21b-139">您可以使用參照 toohello [Windows 存放區快速入門教學課程](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)如果您需要建立新的通知中樞的說明。</span><span class="sxs-lookup"><span data-stu-id="1e21b-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="1e21b-140">選取 [Settings] \(設定) 。</span><span class="sxs-lookup"><span data-stu-id="1e21b-140">Select **Settings**.</span></span>
4. <span data-ttu-id="1e21b-141">按一下 [存取原則] 。</span><span class="sxs-lookup"><span data-stu-id="1e21b-141">Click on **Access Policies**.</span></span> <span data-ttu-id="1e21b-142">您會看到兩個共用和完整存取連接字串。</span><span class="sxs-lookup"><span data-stu-id="1e21b-142">You will see both shared and full access connection strings.</span></span>

![Azure 入口網站 - 通知中樞](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="1e21b-144">您也可以擷取 hello 連接字串使用 hello **Get AzureSbNamespace**所提供的 cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello **azure sb 命名空間顯示**命令搭配hello [Azure 命令列介面 (Azure CLI)](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="1e21b-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="1e21b-145">一般架構</span><span class="sxs-lookup"><span data-stu-id="1e21b-145">General architecture</span></span>
<span data-ttu-id="1e21b-146">hello **NotificationHubService**物件會公開下列物件來傳送推播通知 toospecific 裝置和應用程式的執行個體的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="1e21b-147">**Android** -使用 hello **GcmService**物件，將會位於**notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="1e21b-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="1e21b-148">**iOS** -使用 hello **ApnsService**物件，可存取**notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="1e21b-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="1e21b-149">**Windows Phone** -使用 hello **MpnsService**物件，將會位於**notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="1e21b-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="1e21b-150">**通用 Windows 平台**-使用 hello **WnsService**物件，將會位於**notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="1e21b-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="1e21b-151">如何： 傳送推播通知 tooAndroid 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e21b-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="1e21b-152">hello **GcmService**物件提供**傳送**可以是使用的 toosend 推播通知 tooAndroid 應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="1e21b-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="1e21b-153">hello**傳送**方法可接受下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="1e21b-154">**標記**-hello 標記識別項。</span><span class="sxs-lookup"><span data-stu-id="1e21b-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="1e21b-155">如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1e21b-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="1e21b-156">**裝載**-hello 訊息的 JSON 或原始字串裝載。</span><span class="sxs-lookup"><span data-stu-id="1e21b-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="1e21b-157">**回呼**-hello 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="1e21b-158">如需有關 hello 裝載格式的詳細資訊，請參閱 hello**裝載**區段 hello[實作 GCM 伺服器](http://developer.android.com/google/gcm/server.html#payload)文件。</span><span class="sxs-lookup"><span data-stu-id="1e21b-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="1e21b-159">hello 下列程式碼使用 hello **GcmService** hello 所公開的執行個體**NotificationHubService** toosend 推播通知 tooall 註冊用戶端。</span><span class="sxs-lookup"><span data-stu-id="1e21b-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="1e21b-160">如何： 傳送推播通知 tooiOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e21b-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="1e21b-161">相同如同上面所述的 Android 應用程式 hello **ApnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooiOS 應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="1e21b-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="1e21b-162">hello**傳送**方法可接受下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="1e21b-163">**標記**-hello 標記識別項。</span><span class="sxs-lookup"><span data-stu-id="1e21b-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="1e21b-164">如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1e21b-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="1e21b-165">**裝載**-hello 訊息的 JSON 或字串裝載。</span><span class="sxs-lookup"><span data-stu-id="1e21b-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="1e21b-166">**回呼**-hello 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="1e21b-167">如需詳細資訊 hello 裝載格式，請參閱 hello**通知裝載**區段 hello[本機和推播通知程式設計指南](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html)文件。</span><span class="sxs-lookup"><span data-stu-id="1e21b-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="1e21b-168">hello 下列程式碼使用 hello **ApnsService** hello 所公開的執行個體**NotificationHubService** toosend 警示訊息 tooall 用戶端：</span><span class="sxs-lookup"><span data-stu-id="1e21b-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="1e21b-169">如何： 傳送推播通知 tooWindows 電話應用程式</span><span class="sxs-lookup"><span data-stu-id="1e21b-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="1e21b-170">hello **MpnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooWindows 電話應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="1e21b-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="1e21b-171">hello**傳送**方法可接受下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="1e21b-172">**標記**-hello 標記識別項。</span><span class="sxs-lookup"><span data-stu-id="1e21b-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="1e21b-173">如果提供沒有標記，則 hello 會傳送通知 tooall 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1e21b-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="1e21b-174">**裝載**-hello 訊息的 XML 內容。</span><span class="sxs-lookup"><span data-stu-id="1e21b-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="1e21b-175">**TargetName** - 快顯通知的 `toast`。</span><span class="sxs-lookup"><span data-stu-id="1e21b-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="1e21b-176">`token` 代表磚通知。</span><span class="sxs-lookup"><span data-stu-id="1e21b-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="1e21b-177">**通知類別**-hello hello 通知的優先順序。</span><span class="sxs-lookup"><span data-stu-id="1e21b-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="1e21b-178">請參閱 hello **HTTP 標頭項目**區段 hello[推播通知從伺服器](http://msdn.microsoft.com/library/hh221551.aspx)文件適用於有效的值。</span><span class="sxs-lookup"><span data-stu-id="1e21b-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="1e21b-179">**Options** - 選用的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1e21b-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="1e21b-180">**回呼**-hello 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="1e21b-181">取得一份有效**TargetName**，**通知類別**和標頭檔選項，請參閱 hello[推播通知從伺服器](http://msdn.microsoft.com/library/hh221551.aspx)頁面。</span><span class="sxs-lookup"><span data-stu-id="1e21b-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="1e21b-182">下列範例程式碼的 hello 使用 hello **MpnsService** hello 所公開的執行個體**NotificationHubService** toosend 快顯通知推播通知：</span><span class="sxs-lookup"><span data-stu-id="1e21b-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="1e21b-183">如何： 傳送推播通知 tooUniversal Windows 平台 (UWP) 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e21b-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="1e21b-184">hello **WnsService**物件提供**傳送**可以是使用的 toosend 推播通知 tooUniversal Windows 平台應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="1e21b-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="1e21b-185">hello**傳送**方法可接受下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e21b-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="1e21b-186">**標記**-hello 標記識別項。</span><span class="sxs-lookup"><span data-stu-id="1e21b-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="1e21b-187">如果提供沒有標記，則 hello 會傳送通知 tooall 註冊用戶端。</span><span class="sxs-lookup"><span data-stu-id="1e21b-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="1e21b-188">**裝載**-hello XML 訊息裝載。</span><span class="sxs-lookup"><span data-stu-id="1e21b-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="1e21b-189">**型別**-hello 通知類型。</span><span class="sxs-lookup"><span data-stu-id="1e21b-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="1e21b-190">**Options** - 選用的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="1e21b-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="1e21b-191">**回呼**-hello 回呼函式。</span><span class="sxs-lookup"><span data-stu-id="1e21b-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="1e21b-192">如需有效類型和要求標頭的清單，請參閱 [推播通知服務要求和回應標頭](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e21b-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="1e21b-193">hello 下列程式碼使用 hello **WnsService** hello 所公開的執行個體**NotificationHubService** toosend 快顯通知推播通知 tooa UWP 應用程式：</span><span class="sxs-lookup"><span data-stu-id="1e21b-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="1e21b-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e21b-194">Next Steps</span></span>
<span data-ttu-id="1e21b-195">可讓您 tooeasily 組建服務基礎結構 toodeliver 推播通知 tooa 各式各樣的裝置 hello 範例程式碼片段上方。</span><span class="sxs-lookup"><span data-stu-id="1e21b-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="1e21b-196">既然您已經學會使用 node.js 通知中樞的 hello 基本概念，請遵循這些連結 toolearn 深入了解如何擴充進一步這些功能。</span><span class="sxs-lookup"><span data-stu-id="1e21b-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="1e21b-197">請參閱 hello 的 MSDN 參考[Azure 通知中樞](https://msdn.microsoft.com/library/azure/jj927170.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e21b-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="1e21b-198">請瀏覽 hello [Azure SDK for 節點]GitHub 上的儲存機制，如需詳細的範例和實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1e21b-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK for 節點]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
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
[使用 WebMatrix 的網站]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure 入口網站]: https://portal.azure.com
