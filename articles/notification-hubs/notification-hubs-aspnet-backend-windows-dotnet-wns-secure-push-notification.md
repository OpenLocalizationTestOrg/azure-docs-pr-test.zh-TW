---
title: "Azure 通知中心安全推播"
description: "了解如何在 Azure 中傳送安全的推播通知。 程式碼範例是以 C# 撰寫並使用 .NET API。"
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="db20f-104">Azure 通知中心安全推播</span><span class="sxs-lookup"><span data-stu-id="db20f-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db20f-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="db20f-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="db20f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="db20f-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="db20f-107">Android</span><span class="sxs-lookup"><span data-stu-id="db20f-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="db20f-108">Overview</span><span class="sxs-lookup"><span data-stu-id="db20f-108">Overview</span></span>
<span data-ttu-id="db20f-109">Microsoft Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播基礎結構，因而可大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="db20f-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="db20f-110">基於法規或安全性限制，應用程式有時會想要在通知中加入無法透過標準推播通知基礎結構傳送的內容。</span><span class="sxs-lookup"><span data-stu-id="db20f-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="db20f-111">本教學課程說明如何透過用戶端裝置和應用程式後端之間的安全、已驗證連線來傳送敏感資訊，以達到相同體驗。</span><span class="sxs-lookup"><span data-stu-id="db20f-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="db20f-112">概括而言，流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="db20f-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="db20f-113">應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="db20f-113">The app back-end:</span></span>
   * <span data-ttu-id="db20f-114">在後端資料庫中儲存安全裝載。</span><span class="sxs-lookup"><span data-stu-id="db20f-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="db20f-115">將此通知的識別碼傳送至裝置 (不會傳送安全資訊)。</span><span class="sxs-lookup"><span data-stu-id="db20f-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="db20f-116">收到通知時，裝置上的應用程式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="db20f-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="db20f-117">裝置會連絡後端並要求安全裝載。</span><span class="sxs-lookup"><span data-stu-id="db20f-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="db20f-118">應用程式會以通知的形式在裝置上顯示裝載。</span><span class="sxs-lookup"><span data-stu-id="db20f-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="db20f-119">請務必注意在上述流程 (與本教學課程) 中，我們假設使用者登入後，裝置會將驗證權杖儲存在本機儲存體中。</span><span class="sxs-lookup"><span data-stu-id="db20f-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="db20f-120">由於裝置可使用此權杖擷取通知的安全裝載，因此可保證完全順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="db20f-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="db20f-121">如果您的應用程式沒有將驗證權杖儲存在裝置上，或如果這些權杖可能會過期，裝置應用程式應在收到通知時顯示一般通知，以提示使用者啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="db20f-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="db20f-122">應用程式會接著驗證使用者，並顯示通知裝載。</span><span class="sxs-lookup"><span data-stu-id="db20f-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="db20f-123">本安全推播教學課程說明如何以安全的方式傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="db20f-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="db20f-124">本教學課程會以 [通知使用者](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) 教學課程為基礎，因此您應先完成該教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="db20f-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="db20f-125">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Windows 市集)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="db20f-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="db20f-126">另請注意，Windows Phone 8.1 需要 Windows (不是 Windows Phone) 認證，且無法在 Windows Phone 8.0 或 Silverlight 8.1 上使用背景工作。</span><span class="sxs-lookup"><span data-stu-id="db20f-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="db20f-127">若是 Windows 市集應用程式，只有當應用程式已啟用鎖定畫面 (按一下 Appmanifest 中的核取方塊) 時，您才可以透過背景工作接收通知。</span><span class="sxs-lookup"><span data-stu-id="db20f-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="db20f-128">修改 Windows Phone 專案</span><span class="sxs-lookup"><span data-stu-id="db20f-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="db20f-129">在 **NotifyUserWindowsPhone** 專案中，新增下列程式碼至 App.xaml.cs 以註冊推播背景工作。</span><span class="sxs-lookup"><span data-stu-id="db20f-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="db20f-130">在 `OnLaunched()` 方法的結尾新增下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="db20f-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="db20f-131">仍在 App.xaml.cs 中，在 `OnLaunched()` 方法後面立即新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="db20f-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="db20f-132">在 App.xaml.cs 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="db20f-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="db20f-133">從 Visual Studio 的 [檔案] 功能表中，按一下 [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="db20f-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="db20f-134">建立推播背景元件</span><span class="sxs-lookup"><span data-stu-id="db20f-134">Create the Push Background Component</span></span>
<span data-ttu-id="db20f-135">下一個步驟說明如何建立推播背景元件。</span><span class="sxs-lookup"><span data-stu-id="db20f-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="db20f-136">在 [方案總管] 中，以滑鼠右鍵按一下解決方案的最上層節點 (在此案例中為 **Solution SecurePush**)，並按一下 [新增]，然後按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="db20f-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="db20f-137">展開 [市集應用程式]，並按一下 [Windows Phone 應用程式]，然後按一下 [Windows 執行階段元件 (Windows Phone)]。</span><span class="sxs-lookup"><span data-stu-id="db20f-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="db20f-138">將專案命名為 **PushBackgroundComponent**，然後按一下 [確定] 以建立專案。</span><span class="sxs-lookup"><span data-stu-id="db20f-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="db20f-139">在 [方案總管] 中，以滑鼠右鍵按一下 **PushBackgroundComponent (Windows Phone 8.1)** 專案，並按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="db20f-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="db20f-140">將新類別命名為 **PushBackgroundTask.cs**。</span><span class="sxs-lookup"><span data-stu-id="db20f-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="db20f-141">按一下 [新增] 以產生類別。</span><span class="sxs-lookup"><span data-stu-id="db20f-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="db20f-142">使用下列程式碼來取代 **PushBackgroundComponent** 命名空間定義的整個內容，並將預留位置 `{back-end endpoint}` 替換成部署後端時所取得的後端端點：</span><span class="sxs-lookup"><span data-stu-id="db20f-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="db20f-143">在 [方案總管] 中，以滑鼠右鍵按一下 **PushBackgroundComponent (Windows Phone 8.1)** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="db20f-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="db20f-144">在左側，按一下 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="db20f-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="db20f-145">在 [搜尋] 方塊中，輸入 **Http Client**。</span><span class="sxs-lookup"><span data-stu-id="db20f-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="db20f-146">按一下結果清單中的 **Microsoft HTTP Client Libraries**，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="db20f-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="db20f-147">完成安裝。</span><span class="sxs-lookup"><span data-stu-id="db20f-147">Complete the installation.</span></span>
9. <span data-ttu-id="db20f-148">回到 NuGet [搜尋] 方塊，輸入 **Json.net**。</span><span class="sxs-lookup"><span data-stu-id="db20f-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="db20f-149">安裝 **Json.NET** 套件，然後關閉 [NuGet Package Manager] 視窗。</span><span class="sxs-lookup"><span data-stu-id="db20f-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="db20f-150">在 **PushBackgroundTask.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="db20f-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="db20f-151">在 [方案總管] 的 **NotifyUserWindowsPhone (Windows Phone 8.1)** 專案中，以滑鼠右鍵按一下 [參考]，然後按一下 [新增參考...]。</span><span class="sxs-lookup"><span data-stu-id="db20f-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="db20f-152">在 [參考管理員] 對話方塊中，核取 **PushBackgroundComponent** 旁邊的方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="db20f-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="db20f-153">在 [方案總管] 中，連按兩下 **NotifyUserWindowsPhone (Windows Phone 8.1)** 專案中的 **Package.appxmanifest**。</span><span class="sxs-lookup"><span data-stu-id="db20f-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="db20f-154">在 [通知] 下，將 [支援快顯通知] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="db20f-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="db20f-155">仍在 **Package.appxmanifest** 中，按一下頂端附近的 [宣告] 功能表。</span><span class="sxs-lookup"><span data-stu-id="db20f-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="db20f-156">在 [可用宣告] 下拉式清單中，按一下 [背景工作]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="db20f-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="db20f-157">在 **Package.appxmanifest** 中，核取 [屬性] 下的 [推播通知]。</span><span class="sxs-lookup"><span data-stu-id="db20f-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="db20f-158">在 **Package.appxmanifest** 中，於 [應用程式設定] 的 [輸入點] 欄位中輸入 **PushBackgroundComponent.PushBackgroundTask**。</span><span class="sxs-lookup"><span data-stu-id="db20f-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="db20f-159">從 [檔案] 功能表中，按一下 [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="db20f-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="db20f-160">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="db20f-160">Run the Application</span></span>
<span data-ttu-id="db20f-161">若要執行應用程式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="db20f-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="db20f-162">在 Visual Studio 中，執行 **AppBackend** Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db20f-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="db20f-163">[ASP.NET Web] 頁面便會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="db20f-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="db20f-164">在 Visual Studio 中，執行 **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db20f-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="db20f-165">Windows Phone 模擬器便會執行，並自動載入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="db20f-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="db20f-166">在 **NotifyUserWindowsPhone** 應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="db20f-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="db20f-167">這些可以是任何字串，但必須是相同值。</span><span class="sxs-lookup"><span data-stu-id="db20f-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="db20f-168">在 **NotifyUserWindowsPhone** 應用程式 UI 中，按一下 [登入並註冊]。</span><span class="sxs-lookup"><span data-stu-id="db20f-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="db20f-169">然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="db20f-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
