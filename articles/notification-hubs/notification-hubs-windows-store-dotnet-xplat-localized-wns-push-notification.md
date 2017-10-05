---
title: "通知中樞已當地語系化的即時新聞教學課程"
description: "了解如何使用 Azure 通知中樞傳送本地化即時新聞通知。"
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="48f7f-103">使用通知中心傳送當地語系化的即時新聞</span><span class="sxs-lookup"><span data-stu-id="48f7f-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48f7f-104">Windows 市集 C#</span><span class="sxs-lookup"><span data-stu-id="48f7f-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="48f7f-105">iOS</span><span class="sxs-lookup"><span data-stu-id="48f7f-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="48f7f-106">Overview</span><span class="sxs-lookup"><span data-stu-id="48f7f-106">Overview</span></span>
<span data-ttu-id="48f7f-107">本主題將說明如何使用 Azure 通知中心的 **範本** 功能，廣播已由語言和裝置當地語系化的即時新聞通知。</span><span class="sxs-lookup"><span data-stu-id="48f7f-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="48f7f-108">在本教學課程中，首先您會執行在 [使用通知中樞傳送即時新聞]中建立的 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="48f7f-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="48f7f-109">完成之後，您將可註冊您感興趣的類別、指定您要接收哪種語言的通知，並以該語言針對選取的類別接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="48f7f-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="48f7f-110">此案例分成兩部分：</span><span class="sxs-lookup"><span data-stu-id="48f7f-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="48f7f-111">Windows 市集應用程式允許用戶端裝置指定語言，以及訂閱不同的即時新聞類別；</span><span class="sxs-lookup"><span data-stu-id="48f7f-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="48f7f-112">後端使用 Azure 通知中樞的**標籤**和**範本**功能廣播通知。</span><span class="sxs-lookup"><span data-stu-id="48f7f-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48f7f-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="48f7f-113">Prerequisites</span></span>
<span data-ttu-id="48f7f-114">您必須已完成 [使用通知中樞傳送即時新聞] 教學課程，並具有可用的程式碼，因為此教學課程是直接根據該程式碼而建置的。</span><span class="sxs-lookup"><span data-stu-id="48f7f-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="48f7f-115">您也需要 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="48f7f-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="48f7f-116">範本概念</span><span class="sxs-lookup"><span data-stu-id="48f7f-116">Template concepts</span></span>
<span data-ttu-id="48f7f-117">在 [使用通知中樞傳送即時新聞] ，您建置了使用 **標籤** 來訂閱不同即時新聞類別之通知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48f7f-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="48f7f-118">但有許多應用程式是以多個市場為目標的，因此需要當地語系化。</span><span class="sxs-lookup"><span data-stu-id="48f7f-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="48f7f-119">這表示通知本身的內容必須進行當地語系化，並傳遞至正確的裝置集。</span><span class="sxs-lookup"><span data-stu-id="48f7f-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="48f7f-120">在此主題中，我們將說明如何使用通知中樞的 **範本** 功能，輕鬆地傳遞已當地語系化的即時新聞通知。</span><span class="sxs-lookup"><span data-stu-id="48f7f-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="48f7f-121">注意：傳送當地語系化通知的方法之一，是為每個標籤建立多個版本。</span><span class="sxs-lookup"><span data-stu-id="48f7f-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="48f7f-122">例如，若要支援英文、法文和中文，我們將必須為世界新聞建立三個不同的標籤："world_en"、"world_fr" 和 "world_ch"。</span><span class="sxs-lookup"><span data-stu-id="48f7f-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="48f7f-123">接著，我們必須將當地語系化版本的世界新聞分別傳送至這三個標籤。</span><span class="sxs-lookup"><span data-stu-id="48f7f-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="48f7f-124">在此主題中我們會使用範本，以避免使用過多的標籤和傳送過多訊息。</span><span class="sxs-lookup"><span data-stu-id="48f7f-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="48f7f-125">以較高的層級而言，範本可用來指定特定裝置接收通知的方式。</span><span class="sxs-lookup"><span data-stu-id="48f7f-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="48f7f-126">範本可參照您的應用程式後端所傳送的訊息中包含的屬性，藉以指定確切的裝載格式。</span><span class="sxs-lookup"><span data-stu-id="48f7f-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="48f7f-127">在此處的範例中，我們將傳送地區設定無從驗證、且包含所有支援語言的訊息：</span><span class="sxs-lookup"><span data-stu-id="48f7f-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="48f7f-128">接著，我們將確保裝置會為參照正確屬性的範本進行註冊。</span><span class="sxs-lookup"><span data-stu-id="48f7f-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="48f7f-129">例如，要接收簡易快顯通知訊息的 Windows 市集應用程式，會註冊下列包含任何對應標籤的範本：</span><span class="sxs-lookup"><span data-stu-id="48f7f-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="48f7f-130">範本的功能非常強大，您可以在 [範本](notification-hubs-templates-cross-platform-push-messages.md) 一文中了解詳情。</span><span class="sxs-lookup"><span data-stu-id="48f7f-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="48f7f-131">應用程式使用者介面</span><span class="sxs-lookup"><span data-stu-id="48f7f-131">The app user interface</span></span>
<span data-ttu-id="48f7f-132">現在，我們將修改您在 [使用通知中樞傳送即時新聞] 主題中建立的即時新聞應用程式，以使用範本傳送當地語系化的即時新聞。</span><span class="sxs-lookup"><span data-stu-id="48f7f-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="48f7f-133">在您的 Windows 市集應用程式中：</span><span class="sxs-lookup"><span data-stu-id="48f7f-133">In your Windows Store app:</span></span>

<span data-ttu-id="48f7f-134">變更 MainPage.xaml 以加入地區設定下拉式方塊：</span><span class="sxs-lookup"><span data-stu-id="48f7f-134">Change your MainPage.xaml to include a locale combobox:</span></span>

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="48f7f-135">建置 Windows 市集用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="48f7f-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="48f7f-136">在您的 Notifications 類別中，將地區設定參數新增至 *StoreCategoriesAndSubscribe* 和 *SubscribeToCateories* 方法。</span><span class="sxs-lookup"><span data-stu-id="48f7f-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="48f7f-137">請注意，我們不會呼叫 *RegisterNativeAsync* 方法，而是會呼叫 *RegisterTemplateAsync*：我們將會註冊讓範本依循地區設定的特定通知格式。</span><span class="sxs-lookup"><span data-stu-id="48f7f-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="48f7f-138">我們也為範本提供名稱 ("localizedWNSTemplateExample")，因為我們可能會想註冊多個範本 (例如，一個供快顯通知使用，一個供磚使用)，而且我們必須為其命名，才能加以更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="48f7f-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="48f7f-139">請注意，如果有裝置使用相同的標籤註冊多個範本，一個以該標籤為目標的傳入訊息將會使多個通知傳遞至裝置 (每個範本各一個)。</span><span class="sxs-lookup"><span data-stu-id="48f7f-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="48f7f-140">此行為在相同的邏輯訊息必須產生多個視覺化通知時將有所幫助，例如，在一個 Windows 市集應用程式中同時顯示徽章和快顯通知。</span><span class="sxs-lookup"><span data-stu-id="48f7f-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="48f7f-141">新增下列方法，以擷取已儲存的地區設定：</span><span class="sxs-lookup"><span data-stu-id="48f7f-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="48f7f-142">在您的 MainPage.xaml.cs 中，擷取地區設定下拉式方塊的現行值，並將其提供給 Notifications 類別的呼叫，以更新您的按鈕點選處理常式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="48f7f-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. <span data-ttu-id="48f7f-143">最後，在 App.xaml.cs 檔案中，請務必更新 `InitNotificationsAsync` 方法來擷取地區設定，並在訂閱時使用它：</span><span class="sxs-lookup"><span data-stu-id="48f7f-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="48f7f-144">從後端傳送已當地語系化的通知</span><span class="sxs-lookup"><span data-stu-id="48f7f-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="48f7f-145">[使用通知中樞傳送即時新聞]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="48f7f-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
