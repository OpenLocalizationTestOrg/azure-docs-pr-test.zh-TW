---
title: "aaaUse 通知中樞 toosend 最新消息 （Windows 通用）"
description: "使用 Azure 通知中樞與 hello 註冊 toosend 重大消息 tooa 通用 Windows 應用程式中的標記。"
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="324ec-103">使用通知中樞 toosend 最新消息</span><span class="sxs-lookup"><span data-stu-id="324ec-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="324ec-104">概觀</span><span class="sxs-lookup"><span data-stu-id="324ec-104">Overview</span></span>
<span data-ttu-id="324ec-105">本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooa Windows 市集或 Windows Phone 8.1 (非 Silverlight) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="324ec-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="324ec-106">如果您的目標 Windows Phone 8.1 Silverlight，請參閱 toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md)版本。</span><span class="sxs-lookup"><span data-stu-id="324ec-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="324ec-107">完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="324ec-108">此案例中是通知其中具有先前尚未宣告感興趣，例如 RSS 讀取器，音樂迷，應用程式及等等的使用者傳送 toobe toogroups 許多應用程式的常見模式。</span><span class="sxs-lookup"><span data-stu-id="324ec-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="324ec-109">啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。</span><span class="sxs-lookup"><span data-stu-id="324ec-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="324ec-110">當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="324ec-111">標記是只是字串，因為它們不需要預先佈建 toobe。</span><span class="sxs-lookup"><span data-stu-id="324ec-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="324ec-112">如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="324ec-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="324ec-113">Windows 市集和 Windows Phone 8.1 版與更早版本的專案在 Visual Studio 2017 不受支援。</span><span class="sxs-lookup"><span data-stu-id="324ec-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="324ec-114">如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。</span><span class="sxs-lookup"><span data-stu-id="324ec-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="324ec-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="324ec-115">Prerequisites</span></span>
<span data-ttu-id="324ec-116">本主題是根據您在建立 hello 應用程式[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="324ec-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="324ec-117">開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="324ec-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="324ec-118">加入類別目錄選取 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="324ec-118">Add category selection toohello app</span></span>
<span data-ttu-id="324ec-119">hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要頁面，啟用 hello 使用者 tooselect 類別 tooregister。</span><span class="sxs-lookup"><span data-stu-id="324ec-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="324ec-120">使用者選取的 hello 類別會儲存在 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="324ec-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="324ec-121">Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。</span><span class="sxs-lookup"><span data-stu-id="324ec-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="324ec-122">開啟 hello MainPage.xaml 專案檔案，然後複製下列程式碼中 hello 的 hello**方格**項目：</span><span class="sxs-lookup"><span data-stu-id="324ec-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="324ec-123">以滑鼠右鍵按一下 hello**共用**專案，並加入新的類別，名為**通知**，新增 hello**公用**修飾詞 toohello 類別定義，然後新增下列 hello **使用**陳述式 toohello 新程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="324ec-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="324ec-124">複製 hello 下列程式碼至新的 hello**通知**類別：</span><span class="sxs-lookup"><span data-stu-id="324ec-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="324ec-125">這個類別使用新聞此裝置有 tooreceive hello 本機儲存體 toostore hello 的類別。</span><span class="sxs-lookup"><span data-stu-id="324ec-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="324ec-126">請注意，而不是呼叫 hello *RegisterNativeAsync*方法我們呼叫*RegisterTemplateAsync* tooregister hello 類別使用的範本註冊。</span><span class="sxs-lookup"><span data-stu-id="324ec-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="324ec-127">我們也提供 hello 範本 (「 simpleWNSTemplateExample") 的名稱，因為我們可能會想 tooregister 多個範本 （例如一個快顯通知），另一個圖格，我們需要 tooname 中順序 toobe 無法 tooupdate 或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="324ec-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="324ec-128">請注意，是否裝置具有相同標記，標記會導致為目標的內送訊息的 hello 註冊多個範本的多個通知傳遞 toohello 裝置 （一個用於每個範本）。</span><span class="sxs-lookup"><span data-stu-id="324ec-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="324ec-129">這種行為時相當實用 hello 相同的邏輯訊息 tooresult 在多個視覺通知中，執行個體中的 Windows 市集應用程式中顯示 徽章和快顯通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="324ec-130">如需範本的詳細資訊，請參閱 [範本](notification-hubs-templates-cross-platform-push-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="324ec-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="324ec-131">在 hello App.xaml.cs 專案檔案中，加入下列屬性 toohello hello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="324ec-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="324ec-132">這個屬性是使用的 toocreate 及存取**通知**執行個體。</span><span class="sxs-lookup"><span data-stu-id="324ec-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="324ec-133">在上述程式碼的 hello，取代 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*您稍早取得。</span><span class="sxs-lookup"><span data-stu-id="324ec-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="324ec-134">發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="324ec-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="324ec-135">接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="324ec-136">hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。</span><span class="sxs-lookup"><span data-stu-id="324ec-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="324ec-137">在您 MainPage.xaml.cs 加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="324ec-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="324ec-138">在 hello MainPage.xaml.cs 專案檔中加入下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="324ec-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="324ec-139">這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。</span><span class="sxs-lookup"><span data-stu-id="324ec-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="324ec-140">類別目錄會變更時，重新建立 hello 註冊 hello 新類別。</span><span class="sxs-lookup"><span data-stu-id="324ec-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="324ec-141">您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="324ec-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="324ec-142">註冊通知</span><span class="sxs-lookup"><span data-stu-id="324ec-142">Register for notifications</span></span>
<span data-ttu-id="324ec-143">這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="324ec-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="324ec-144">因為 hello 通道 hello Windows 通知服務 (WNS) 所指派的 URI 可以隨時變更，您應該註冊通知經常 tooavoid 通知失敗。</span><span class="sxs-lookup"><span data-stu-id="324ec-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="324ec-145">每次該 hello 應用程式啟動時，這個範例會註冊通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="324ec-146">針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。</span><span class="sxs-lookup"><span data-stu-id="324ec-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="324ec-147">開啟 hello App.xaml.cs 檔案並更新 hello **InitNotificationsAsync**方法 toouse hello`notifications`類別 toosubscribe 類別為基礎。</span><span class="sxs-lookup"><span data-stu-id="324ec-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="324ec-148">這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的登錄。</span><span class="sxs-lookup"><span data-stu-id="324ec-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="324ec-149">hello **InitNotificationsAsync**方法建立 hello 一部分[開始使用通知中樞][ get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="324ec-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="324ec-150">在 hello MainPage.xaml.cs 專案檔案中，加入下列程式碼 toohello hello *OnNavigatedTo*方法：</span><span class="sxs-lookup"><span data-stu-id="324ec-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="324ec-151">此更新 hello 主頁先前根據 hello 狀態儲存類別。</span><span class="sxs-lookup"><span data-stu-id="324ec-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="324ec-152">hello 應用程式現在已完成，而且可以是儲存一組類別目錄中與 hello 通知中樞的 hello 裝置使用的本機儲存體 tooregister，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="324ec-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="324ec-153">接下來，我們會定義可以傳送類別通知 toothis 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="324ec-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="324ec-154">傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="324ec-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="324ec-155">執行 hello 應用程式，並產生通知</span><span class="sxs-lookup"><span data-stu-id="324ec-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="324ec-156">在 Visual Studio 中，按下 F5 toocompile 並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="324ec-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="324ec-157">Hello 應用程式 UI 提供一組切換，請注意，可讓您選擇以 hello 類別 toosubscribe。</span><span class="sxs-lookup"><span data-stu-id="324ec-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="324ec-158">啟用一或多個類別切換，然後按一下 [訂閱] 。</span><span class="sxs-lookup"><span data-stu-id="324ec-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="324ec-159">hello 應用程式將選取的 hello 類別轉換成標記，並從 hello 通知中樞要求新的裝置註冊 hello 選取標記。</span><span class="sxs-lookup"><span data-stu-id="324ec-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="324ec-160">hello 已註冊的類別會傳回並顯示在對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="324ec-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="324ec-161">將新的通知傳送 hello 後端 hello 下列方式之一：</span><span class="sxs-lookup"><span data-stu-id="324ec-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="324ec-162">**主控台應用程式：**啟動 hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="324ec-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="324ec-163">**Java/PHP：** 執行您的應用程式/指令碼。</span><span class="sxs-lookup"><span data-stu-id="324ec-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="324ec-164">通知 hello 選取類別目錄會顯示為快顯通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="324ec-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="324ec-165">Next steps</span></span>
<span data-ttu-id="324ec-166">在此教學課程中我們學到如何 toobroadcast 依類別目錄中最新消息。</span><span class="sxs-lookup"><span data-stu-id="324ec-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="324ec-167">完成下列其中一個 hello 下列反白顯示其他進階的通知中心案例的教學課程，請考慮：</span><span class="sxs-lookup"><span data-stu-id="324ec-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="324ec-168">[使用通知中樞 toobroadcast 當地語系化重大消息]</span><span class="sxs-lookup"><span data-stu-id="324ec-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="324ec-169">了解如何傳送 tooenable 新聞應用程式的重大 tooexpand hello 當地語系化通知。</span><span class="sxs-lookup"><span data-stu-id="324ec-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[使用通知中樞 toobroadcast 當地語系化重大消息]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
