---
title: "aaaNotification 集線器當地語系化重大新聞教學課程"
description: "了解如何 toouse Azure 通知中樞 toosend 當地語系化重大消息通知。"
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
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="a952c-103">使用通知中樞 toosend 當地語系化重大消息</span><span class="sxs-lookup"><span data-stu-id="a952c-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a952c-104">Windows 市集 C#</span><span class="sxs-lookup"><span data-stu-id="a952c-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="a952c-105">iOS</span><span class="sxs-lookup"><span data-stu-id="a952c-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a952c-106">概觀</span><span class="sxs-lookup"><span data-stu-id="a952c-106">Overview</span></span>
<span data-ttu-id="a952c-107">本主題說明如何 toouse hello**範本**Azure 通知中樞 toobroadcast 重大消息通知已當地語系化的語言和裝置的功能。</span><span class="sxs-lookup"><span data-stu-id="a952c-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="a952c-108">在本教學課程就開始 hello Windows 市集應用程式中建立[使用通知中樞 toosend 最新消息]。</span><span class="sxs-lookup"><span data-stu-id="a952c-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="a952c-109">完成時，您將會為您感興趣的類別可以 tooregister，tooreceive hello 通知，在指定的語言，並接收只推播通知 hello 選取類別以該語言。</span><span class="sxs-lookup"><span data-stu-id="a952c-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="a952c-110">有兩個部分 toothis 案例：</span><span class="sxs-lookup"><span data-stu-id="a952c-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="a952c-111">hello Windows 市集應用程式可讓用戶端裝置 toospecify 語言和 toosubscribe toodifferent 重大新聞分類。</span><span class="sxs-lookup"><span data-stu-id="a952c-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="a952c-112">hello 後端廣播 hello 通知，請使用 hello**標記**和**範本**feautres Azure 通知中心。</span><span class="sxs-lookup"><span data-stu-id="a952c-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a952c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="a952c-113">Prerequisites</span></span>
<span data-ttu-id="a952c-114">您必須已經完成 hello[使用通知中樞 toosend 最新消息]教學課程，而且有 hello 程式碼，因為本教學課程是直接在該程式碼時。</span><span class="sxs-lookup"><span data-stu-id="a952c-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="a952c-115">您也需要 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a952c-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="a952c-116">範本概念</span><span class="sxs-lookup"><span data-stu-id="a952c-116">Template concepts</span></span>
<span data-ttu-id="a952c-117">在[使用通知中樞 toosend 最新消息]建置的應用程式，使用**標記**toosubscribe toonotifications 不同新聞分類。</span><span class="sxs-lookup"><span data-stu-id="a952c-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="a952c-118">但有許多應用程式是以多個市場為目標的，因此需要當地語系化。</span><span class="sxs-lookup"><span data-stu-id="a952c-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="a952c-119">這表示 hello 通知會自行 hello 內容有 toobe 當地語系化，而且傳遞的 toohello 一組正確的裝置。</span><span class="sxs-lookup"><span data-stu-id="a952c-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="a952c-120">本主題中我們將示範如何 toouse hello**範本**tooeasily 傳遞的通知中樞的功能當地語系化重大消息通知。</span><span class="sxs-lookup"><span data-stu-id="a952c-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="a952c-121">注意： 其中一種方式 toosend 當地語系化通知是 toocreate 多個版本的每個標記。</span><span class="sxs-lookup"><span data-stu-id="a952c-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="a952c-122">比方說，toosupport 英文、 法文及中文，我們需要三個不同的標記世界新聞:"world_en"，"world_fr，"和"world_ch"。</span><span class="sxs-lookup"><span data-stu-id="a952c-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="a952c-123">我們必須 toosend 這些標記的 hello world 新聞 tooeach 的當地語系化的版本。</span><span class="sxs-lookup"><span data-stu-id="a952c-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="a952c-124">本主題中我們將會使用範本 tooavoid hello 擴散的標記以及將多個訊息傳送的 hello 需求。</span><span class="sxs-lookup"><span data-stu-id="a952c-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="a952c-125">在高的層級中，範本會方式 toospecify 如何特定裝置應該會收到通知。</span><span class="sxs-lookup"><span data-stu-id="a952c-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="a952c-126">hello 範本會指定藉由參考是由您的應用程式後端傳送 hello 訊息部分的 tooproperties hello 確切的裝載格式。</span><span class="sxs-lookup"><span data-stu-id="a952c-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="a952c-127">在此處的範例中，我們將傳送地區設定無從驗證、且包含所有支援語言的訊息：</span><span class="sxs-lookup"><span data-stu-id="a952c-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="a952c-128">然後我們會確保裝置註冊使用的範本，是指 toohello 正確的屬性。</span><span class="sxs-lookup"><span data-stu-id="a952c-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="a952c-129">比方說，想 tooreceive 的 Windows 市集應用程式的簡易快顯通知訊息會註冊下列任何對應的標記具有範本的 hello:</span><span class="sxs-lookup"><span data-stu-id="a952c-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="a952c-130">範本的功能非常強大，您可以在 [範本](notification-hubs-templates-cross-platform-push-messages.md) 一文中了解詳情。</span><span class="sxs-lookup"><span data-stu-id="a952c-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="a952c-131">hello 應用程式使用者介面</span><span class="sxs-lookup"><span data-stu-id="a952c-131">hello app user interface</span></span>
<span data-ttu-id="a952c-132">我們現在將會修改您建立 hello 主題中的 hello 即時新聞應用程式[使用通知中樞 toosend 最新消息]toosend 當地語系化使用範本的重大消息。</span><span class="sxs-lookup"><span data-stu-id="a952c-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="a952c-133">在您的 Windows 市集應用程式中：</span><span class="sxs-lookup"><span data-stu-id="a952c-133">In your Windows Store app:</span></span>

<span data-ttu-id="a952c-134">變更您 MainPage.xaml tooinclude 地區設定下拉式方塊：</span><span class="sxs-lookup"><span data-stu-id="a952c-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="a952c-135">建立 hello Windows 市集用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="a952c-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="a952c-136">在通知類別中，加入地區設定參數 tooyour *StoreCategoriesAndSubscribe*和*SubscribeToCateories*方法。</span><span class="sxs-lookup"><span data-stu-id="a952c-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="a952c-137">請注意，而不是呼叫 hello *RegisterNativeAsync*方法我們呼叫*RegisterTemplateAsync*： 登錄中的 hello 範本取決於 hello 地區設定特定的通知格式。</span><span class="sxs-lookup"><span data-stu-id="a952c-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="a952c-138">我們也提供 hello 範本 (「 localizedWNSTemplateExample") 的名稱，因為我們可能會想 tooregister 多個範本 （例如一個快顯通知），另一個圖格，我們需要 tooname 中順序 toobe 無法 tooupdate 或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="a952c-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="a952c-139">請注意，是否裝置具有相同標記，標記會導致為目標的內送訊息的 hello 註冊多個範本的多個通知傳遞 toohello 裝置 （一個用於每個範本）。</span><span class="sxs-lookup"><span data-stu-id="a952c-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="a952c-140">這種行為時相當實用 hello 相同的邏輯訊息 tooresult 在多個視覺通知中，執行個體中的 Windows 市集應用程式中顯示 徽章和快顯通知。</span><span class="sxs-lookup"><span data-stu-id="a952c-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="a952c-141">新增下列方法 tooretrieve hello 儲存的地區設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="a952c-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="a952c-142">在您 mainpage.xaml.cs 中，更新您的按鈕 click 處理常式擷取 hello hello 地區設定下拉式方塊的目前值，並提供 toohello 呼叫 toohello 通知類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a952c-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="a952c-143">最後，在 App.xaml.cs 檔案中，請確定 tooupdate 您`InitNotificationsAsync`方法 tooretrieve hello 地區設定和訂閱時使用它：</span><span class="sxs-lookup"><span data-stu-id="a952c-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="a952c-144">從後端傳送已當地語系化的通知</span><span class="sxs-lookup"><span data-stu-id="a952c-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[使用通知中樞 toosend 最新消息]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
