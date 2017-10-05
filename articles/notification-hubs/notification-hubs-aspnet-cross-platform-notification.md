---
title: "使用通知中樞向使用者傳送跨平台通知 (ASP.NET)"
description: "了解如何使用通知中樞範本，在單一要求中傳送以所有平台為目標的跨平台通知。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="76711-103">使用通知中心向使用者傳送跨平台通知</span><span class="sxs-lookup"><span data-stu-id="76711-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="76711-104">在上一堂教學課程 [使用通知中心來通知使用者]中，您已了解如何將通知推播至所有由特定經驗證使用者所註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="76711-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="76711-105">在該教學課程中，需要用多個要求來傳送通知給每個支援的用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="76711-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="76711-106">通知中心可支援範本，讓您指定特定裝置接收通知的方式。</span><span class="sxs-lookup"><span data-stu-id="76711-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="76711-107">這使得傳送跨平台通知變得更簡單。</span><span class="sxs-lookup"><span data-stu-id="76711-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="76711-108">本主題示範如何運用範本，在單一要求中傳送以所有平台為目標的跨平台通知。</span><span class="sxs-lookup"><span data-stu-id="76711-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="76711-109">如需這些範本的詳細資訊，請參閱 [Azure 通知中樞概觀][Templates]。</span><span class="sxs-lookup"><span data-stu-id="76711-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76711-110">Windows Phone 8.1 及更早版本的專案不支援使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="76711-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="76711-111">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="76711-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="76711-112">通知中心可以讓裝置註冊多個具有相同標籤的範本。</span><span class="sxs-lookup"><span data-stu-id="76711-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="76711-113">在此情況下，當傳入的訊息符合該標籤時，就會有多個通知傳遞至裝置 (每個通知各用於一個範本)。</span><span class="sxs-lookup"><span data-stu-id="76711-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="76711-114">如此一來，您就能讓相同訊息顯示在多個視覺通知中，例如以徽章形式和 Windows 市集應用程式中的快顯通知形式。</span><span class="sxs-lookup"><span data-stu-id="76711-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="76711-115">完成下列步驟，可使用範本傳送跨平台通知：</span><span class="sxs-lookup"><span data-stu-id="76711-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="76711-116">在 Visual Studio 的 [方案總管] 中展開 [控制器]  資料夾，然後開啟 RegisterController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="76711-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="76711-117">在 **Put** 方法中找出建立新註冊的程式碼區塊，並將 `switch` 內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="76711-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    <span data-ttu-id="76711-118">這段程式碼會呼叫平台特有方法來建立範本註冊，而非原生註冊。</span><span class="sxs-lookup"><span data-stu-id="76711-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="76711-119">不需要修改現有註冊，因為範本註冊源自原生註冊。</span><span class="sxs-lookup"><span data-stu-id="76711-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="76711-120">在 [通知] 控制器中，將 **sendNotification** 方法取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="76711-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="76711-121">這段程式碼會同時將通知傳送至所有平台，完全不需要指定原生裝載。</span><span class="sxs-lookup"><span data-stu-id="76711-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="76711-122">通知中樞將以所提供的 *tag* 值 (指定於註冊的範本中) 建置並傳遞正確的裝載到每個裝置。</span><span class="sxs-lookup"><span data-stu-id="76711-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="76711-123">重新發佈您的 WebApi 後端專案。</span><span class="sxs-lookup"><span data-stu-id="76711-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="76711-124">重新執行用戶端應用程式，然後驗證註冊已成功。</span><span class="sxs-lookup"><span data-stu-id="76711-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="76711-125">(選用) 將此用戶端應用程式部署到第二個裝置，然後執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="76711-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="76711-126">請留意到，每個裝置上都會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="76711-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76711-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76711-127">Next Steps</span></span>
<span data-ttu-id="76711-128">您已完成本教學課程，現在可參閱下列主題進一步了解通知中心和範本：</span><span class="sxs-lookup"><span data-stu-id="76711-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="76711-129">**[使用通知中樞傳送即時新聞]**</span><span class="sxs-lookup"><span data-stu-id="76711-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="76711-130">示範另一個使用範本的案例</span><span class="sxs-lookup"><span data-stu-id="76711-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="76711-131">**[Azure 通知中樞概觀][Templates]**</span><span class="sxs-lookup"><span data-stu-id="76711-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="76711-132">概觀主題包含範本的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="76711-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="76711-133">[使用通知中樞傳送即時新聞]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="76711-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="76711-134">[使用通知中心來通知使用者]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="76711-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
