---
title: "aaaAzure 集線器安全推播通知"
description: "了解如何安全 toosend 推播通知在 Azure 中。 以 C# 使用 hello.NET API 撰寫的程式碼範例。"
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="6ab35-104">Azure 通知中心安全推播</span><span class="sxs-lookup"><span data-stu-id="6ab35-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ab35-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="6ab35-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="6ab35-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6ab35-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="6ab35-107">Android</span><span class="sxs-lookup"><span data-stu-id="6ab35-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6ab35-108">概觀</span><span class="sxs-lookup"><span data-stu-id="6ab35-108">Overview</span></span>
<span data-ttu-id="6ab35-109">在 Microsoft Azure 推播通知支援可讓您 tooaccess 方便使用、 多平台、 向外延展的推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。</span><span class="sxs-lookup"><span data-stu-id="6ab35-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="6ab35-110">有時候 tooregulatory 或安全性條件約束，因為應用程式可能會想 tooinclude 中無法透過 hello 標準的推播通知基礎結構傳送的 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="6ab35-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="6ab35-111">本教學課程描述 tooachieve 如何透過 hello 用戶端裝置與 hello 應用程式後端之間的安全、 已驗證連線的機密資訊傳送 hello 相同的體驗。</span><span class="sxs-lookup"><span data-stu-id="6ab35-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="6ab35-112">在高層級，hello 流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="6ab35-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="6ab35-113">hello 應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="6ab35-113">hello app back-end:</span></span>
   * <span data-ttu-id="6ab35-114">在後端資料庫中儲存安全裝載。</span><span class="sxs-lookup"><span data-stu-id="6ab35-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="6ab35-115">會傳送 hello （傳送不安全的資訊） 此通知 toohello 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="6ab35-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="6ab35-116">hello 在裝置上，當收到 hello 通知 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="6ab35-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="6ab35-117">hello 裝置會連絡 hello 後端要求 hello 安全內容。</span><span class="sxs-lookup"><span data-stu-id="6ab35-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="6ab35-118">hello 應用程式可以顯示 hello 裝載為 hello 裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="6ab35-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="6ab35-119">請務必 toonote hello 上述流程中 （並在本教學課程），我們會假設該 hello 裝置會儲存在本機儲存體，驗證語彙基元之後 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="6ab35-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="6ab35-120">這樣可保證完全完美無瑕的體驗，如 hello 裝置可以擷取 hello 通知安全裝載使用這個語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6ab35-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="6ab35-121">如果您的應用程式不會儲存驗證語彙基元 hello 在裝置上，或可以過期這些語彙基元，hello 裝置的應用程式，並收到 hello 通知應該會顯示提示 hello 使用者 toolaunch hello 應用程式的一般通知。</span><span class="sxs-lookup"><span data-stu-id="6ab35-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="6ab35-122">hello 應用程式然後驗證 hello 使用者，並顯示 hello 通知裝載。</span><span class="sxs-lookup"><span data-stu-id="6ab35-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="6ab35-123">此安全發送教學課程會示範如何 toosend 推播通知安全的方式。</span><span class="sxs-lookup"><span data-stu-id="6ab35-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="6ab35-124">hello 教學課程是 hello[通知使用者](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)教學課程中，因此，您應該完成 hello 步驟在該教學課程中第一次。</span><span class="sxs-lookup"><span data-stu-id="6ab35-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab35-125">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Windows 市集)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="6ab35-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="6ab35-126">另請注意，Windows Phone 8.1 需要 Windows (不是 Windows Phone) 認證，且無法在 Windows Phone 8.0 或 Silverlight 8.1 上使用背景工作。</span><span class="sxs-lookup"><span data-stu-id="6ab35-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="6ab35-127">對於 Windows 市集應用程式，您才可以接收通知，透過背景工作 hello 應用程式已啟用鎖定畫面 （按一下 hello Appmanifest hello 核取方塊）。</span><span class="sxs-lookup"><span data-stu-id="6ab35-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="6ab35-128">修改 hello Windows Phone 專案</span><span class="sxs-lookup"><span data-stu-id="6ab35-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="6ab35-129">在 hello **NotifyUserWindowsPhone**專案中，加入下列程式碼 tooApp.xaml.cs tooregister hello 發送背景工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ab35-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="6ab35-130">新增下列一行程式碼結尾 hello hello hello`OnLaunched()`方法：</span><span class="sxs-lookup"><span data-stu-id="6ab35-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="6ab35-131">仍在 App.xaml.cs，加入下列程式碼後面 hello hello`OnLaunched()`方法：</span><span class="sxs-lookup"><span data-stu-id="6ab35-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="6ab35-132">新增下列 hello`using`在 hello hello App.xaml.cs 檔案最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="6ab35-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="6ab35-133">從 hello**檔案**功能表在 Visual Studio 中，按一下**全部儲存**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="6ab35-134">建立 hello 推送背景元件</span><span class="sxs-lookup"><span data-stu-id="6ab35-134">Create hello Push Background Component</span></span>
<span data-ttu-id="6ab35-135">hello 下一個步驟是 toocreate hello 發送背景元件。</span><span class="sxs-lookup"><span data-stu-id="6ab35-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="6ab35-136">在 [方案總管] 中，以滑鼠右鍵按一下 hello hello 解決方案的最上層的節點 (**方案 SecurePush**在此情況下)，然後按一下**新增**，然後按一下**新專案**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="6ab35-137">展開 [市集應用程式]，並按一下 [Windows Phone 應用程式]，然後按一下 [Windows 執行階段元件 (Windows Phone)]。</span><span class="sxs-lookup"><span data-stu-id="6ab35-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="6ab35-138">名稱 hello 專案**PushBackgroundComponent**，然後按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="6ab35-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="6ab35-139">在 方案總管 中，以滑鼠右鍵按一下 hello **PushBackgroundComponent (Windows Phone 8.1)**專案，然後按一下 **新增**，然後按一下 **類別**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="6ab35-140">Hello 新類別命名**PushBackgroundTask.cs**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="6ab35-141">按一下**新增**toogenerate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="6ab35-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="6ab35-142">取代 hello hello 整個內容**PushBackgroundComponent**命名空間定義，以下列程式碼，以取代 hello 預留位置 hello`{back-end endpoint}`與 hello 後端端點取得部署時您後端：</span><span class="sxs-lookup"><span data-stu-id="6ab35-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="6ab35-143">在 [方案總管] 中，以滑鼠右鍵按一下 hello **PushBackgroundComponent (Windows Phone 8.1)**專案，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="6ab35-144">在 hello 左側，按一下 **線上**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="6ab35-145">在 hello**搜尋**方塊中，輸入**Http 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="6ab35-146">在 hello 結果清單中，按一下  **Microsoft HTTP Client Libraries**，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="6ab35-147">完成 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="6ab35-147">Complete hello installation.</span></span>
9. <span data-ttu-id="6ab35-148">在 hello NuGet**搜尋**方塊中，輸入**Json.net**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="6ab35-149">安裝 hello **Json.NET**封裝，然後關閉 hello NuGet 封裝管理員 視窗。</span><span class="sxs-lookup"><span data-stu-id="6ab35-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="6ab35-150">新增下列 hello`using`在 hello hello 最上方的陳述式**PushBackgroundTask.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="6ab35-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="6ab35-151">在 方案總管中 hello **NotifyUserWindowsPhone (Windows Phone 8.1)**專案中，以滑鼠右鍵按一下**參考**，然後按一下**加入參考...**.在 hello 參考管理員對話方塊中，核取 hello 方塊旁太**PushBackgroundComponent**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="6ab35-152">在 [方案總管] 中，按兩下**Package.appxmanifest**在 hello **NotifyUserWindowsPhone (Windows Phone 8.1)**專案。</span><span class="sxs-lookup"><span data-stu-id="6ab35-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="6ab35-153">在下**通知**，將**快顯能夠**太**是**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="6ab35-154">仍在**Package.appxmanifest**，按一下 hello**宣告**靠近 hello 頂端的功能表。</span><span class="sxs-lookup"><span data-stu-id="6ab35-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="6ab35-155">在 hello**可用宣告**下拉式清單中，按一下**背景工作**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="6ab35-156">在 **Package.appxmanifest** 中，核取 [屬性] 下的 [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="6ab35-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="6ab35-157">在**Package.appxmanifest**下**應用程式設定**，型別**PushBackgroundComponent.PushBackgroundTask**在 hello**進入點**欄位。</span><span class="sxs-lookup"><span data-stu-id="6ab35-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="6ab35-158">從 hello**檔案**功能表上，按一下 **全部儲存**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="6ab35-159">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6ab35-159">Run hello Application</span></span>
<span data-ttu-id="6ab35-160">toorun hello 應用程式中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="6ab35-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="6ab35-161">在 Visual Studio 中，執行 hello **AppBackend** Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ab35-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="6ab35-162">[ASP.NET Web] 頁面便會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="6ab35-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="6ab35-163">在 Visual Studio 中，執行 hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ab35-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="6ab35-164">hello Windows Phone 模擬器中執行，並自動載入 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ab35-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="6ab35-165">在 hello **NotifyUserWindowsPhone**應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6ab35-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="6ab35-166">這些可以是任何字串，但它們必須 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="6ab35-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="6ab35-167">在 hello **NotifyUserWindowsPhone**應用程式 UI 中，按一下**登入並註冊**。</span><span class="sxs-lookup"><span data-stu-id="6ab35-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="6ab35-168">然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="6ab35-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
