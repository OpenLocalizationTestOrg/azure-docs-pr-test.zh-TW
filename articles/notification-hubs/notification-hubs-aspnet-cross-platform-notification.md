---
title: "aaaSend 跨平台通知 toousers 與通知中樞 (ASP.NET)"
description: "深入了解如何在單一要求中，所有平台為目標的無從驗證平台通知，toouse 通知中樞範本 toosend。"
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="76445-103">傳送跨平台通知 toousers 與通知中樞</span><span class="sxs-lookup"><span data-stu-id="76445-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="76445-104">Hello 上一個教學課程中[向使用者通知中樞通知]，您學到如何 toopush 通知 tooall 裝置註冊特定的已驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="76445-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="76445-105">在此教學課程中，在多個要求提供了必要的 toosend 通知支援 tooeach 用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="76445-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="76445-106">通知中心支援範本，可讓您指定特定的裝置想 tooreceive 通知的方式。</span><span class="sxs-lookup"><span data-stu-id="76445-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="76445-107">這使得傳送跨平台通知變得更簡單。</span><span class="sxs-lookup"><span data-stu-id="76445-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="76445-108">本主題示範如何在單一要求中，所有平台為目標的無從驗證平台通知的範本 toosend tootake 優點。</span><span class="sxs-lookup"><span data-stu-id="76445-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="76445-109">如需這些範本的詳細資訊，請參閱 [Azure 通知中樞概觀][Templates]。</span><span class="sxs-lookup"><span data-stu-id="76445-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76445-110">Windows Phone 8.1 及更早版本的專案不支援使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="76445-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="76445-111">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="76445-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="76445-112">通知中樞可讓裝置 tooregister hello 與多個範本相同的標記。</span><span class="sxs-lookup"><span data-stu-id="76445-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="76445-113">在此情況下，目標標記，會導致多個通知的內送訊息傳遞 toohello 裝置，一個用於每個範本。</span><span class="sxs-lookup"><span data-stu-id="76445-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="76445-114">這樣做可讓您 toodisplay hello 相同訊息中多個視覺通知的詳細資訊，例如同時當做徽章和 Windows 市集應用程式中的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="76445-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="76445-115">完成下列步驟 toosend 跨平台通知使用範本的 hello:</span><span class="sxs-lookup"><span data-stu-id="76445-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="76445-116">在 hello Visual Studio 中的 方案總管 中，展開 hello**控制器**資料夾，然後開啟 hello RegisterController.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="76445-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="76445-117">在 hello 中尋找的程式碼的 hello 區塊**放**建立新註冊的方法取代 hello`switch`內容以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="76445-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="76445-118">此程式碼會呼叫 hello 平台專屬方法 toocreate 範本註冊，而不是原生註冊。</span><span class="sxs-lookup"><span data-stu-id="76445-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="76445-119">不需要修改現有註冊，因為範本註冊源自原生註冊。</span><span class="sxs-lookup"><span data-stu-id="76445-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="76445-120">在 hello**通知**控制站，取代 hello **sendNotification**方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="76445-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="76445-121">此程式碼會傳送通知 tooall 平台在 hello 相同時間，而不需要 toospecify 原生的裝載。</span><span class="sxs-lookup"><span data-stu-id="76445-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="76445-122">通知中樞建置並傳送 hello 以 hello 提供正確的裝載 tooevery 裝置*標記*hello 註冊範本中所指定的值。</span><span class="sxs-lookup"><span data-stu-id="76445-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="76445-123">重新發佈您的 WebApi 後端專案。</span><span class="sxs-lookup"><span data-stu-id="76445-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="76445-124">再次執行 hello 用戶端應用程式，並驗證註冊成功。</span><span class="sxs-lookup"><span data-stu-id="76445-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="76445-125">（選擇性）部署 hello 用戶端應用程式 tooa 第二個裝置，然後執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76445-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="76445-126">請留意到，每個裝置上都會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="76445-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76445-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76445-127">Next Steps</span></span>
<span data-ttu-id="76445-128">您已完成本教學課程，現在可參閱下列主題進一步了解通知中心和範本：</span><span class="sxs-lookup"><span data-stu-id="76445-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="76445-129">**[使用通知中樞 toosend 最新消息]**</span><span class="sxs-lookup"><span data-stu-id="76445-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="76445-130">示範另一個使用範本的案例</span><span class="sxs-lookup"><span data-stu-id="76445-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="76445-131">**[Azure 通知中樞概觀][Templates]**</span><span class="sxs-lookup"><span data-stu-id="76445-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="76445-132">概觀主題包含範本的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="76445-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[使用通知中樞 toosend 最新消息]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[向使用者通知中樞通知]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
