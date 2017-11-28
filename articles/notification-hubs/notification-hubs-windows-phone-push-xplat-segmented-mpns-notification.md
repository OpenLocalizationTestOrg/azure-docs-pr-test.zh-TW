---
title: "aaaUse 通知中樞 toosend 最新消息 (Windows Phone)"
description: "註冊 toosend 重大消息 tooa Windows Phone 應用程式中使用 Azure 通知中樞 toouse 標記。"
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="1158c-103">使用通知中樞 toosend 最新消息</span><span class="sxs-lookup"><span data-stu-id="1158c-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="1158c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1158c-104">Overview</span></span>
<span data-ttu-id="1158c-105">本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooa Windows Phone 8.0/8.1 Silverlight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1158c-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="1158c-106">如果您的目標 Windows 市集或 Windows Phone 8.1 應用程式，請參閱 tootoohello [Windows 通用](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)版本。</span><span class="sxs-lookup"><span data-stu-id="1158c-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="1158c-107">完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="1158c-108">這個案例是許多應用程式的常見模式，通知其中有傳送 toobe toogroups 的先前尚未宣告欄位，例如 RSS 讀取器、 應用程式等的音樂迷感興趣的使用者。</span><span class="sxs-lookup"><span data-stu-id="1158c-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="1158c-109">啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。</span><span class="sxs-lookup"><span data-stu-id="1158c-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="1158c-110">當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="1158c-111">標記是只是字串，因為它們不需要預先佈建 toobe。</span><span class="sxs-lookup"><span data-stu-id="1158c-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="1158c-112">如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="1158c-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1158c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="1158c-113">Prerequisites</span></span>
<span data-ttu-id="1158c-114">本主題是根據您在建立 hello 應用程式[開始使用通知中心]。</span><span class="sxs-lookup"><span data-stu-id="1158c-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="1158c-115">開始本教學課程之前，您必須已完成 [開始使用通知中心]。</span><span class="sxs-lookup"><span data-stu-id="1158c-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="1158c-116">加入類別目錄選取 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="1158c-116">Add category selection toohello app</span></span>
<span data-ttu-id="1158c-117">hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要頁面，啟用 hello 使用者 tooselect 類別 tooregister。</span><span class="sxs-lookup"><span data-stu-id="1158c-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="1158c-118">使用者選取的 hello 類別會儲存在 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="1158c-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="1158c-119">Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。</span><span class="sxs-lookup"><span data-stu-id="1158c-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="1158c-120">開啟 hello MainPage.xaml 專案檔案，然後取代 hello**方格**名為的項目`TitlePanel`和`ContentPanel`以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1158c-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="1158c-121">Hello 專案中建立新的類別，名為**通知**，新增 hello**公用**修飾詞 toohello 類別定義，然後加入下列 hello**使用**陳述式toohello 新程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="1158c-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="1158c-122">複製 hello 下列程式碼至新的 hello**通知**類別：</span><span class="sxs-lookup"><span data-stu-id="1158c-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="1158c-123">這個類別使用新聞此裝置正在 tooreceive hello 隔離儲存體 toostore hello 的類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="1158c-124">它也包含使用這些類別的方法 tooregister[範本](notification-hubs-templates-cross-platform-push-messages.md)通知登錄。</span><span class="sxs-lookup"><span data-stu-id="1158c-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="1158c-125">在 hello App.xaml.cs 專案檔案中，加入下列屬性 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="1158c-126">取代 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*您稍早取得。</span><span class="sxs-lookup"><span data-stu-id="1158c-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="1158c-127">發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1158c-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="1158c-128">接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="1158c-129">hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。</span><span class="sxs-lookup"><span data-stu-id="1158c-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="1158c-130">在您 MainPage.xaml.cs 加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="1158c-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="1158c-131">在 hello MainPage.xaml.cs 專案檔中加入下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="1158c-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="1158c-132">這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。</span><span class="sxs-lookup"><span data-stu-id="1158c-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="1158c-133">類別目錄會變更時，重新建立 hello 註冊 hello 新類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="1158c-134">您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="1158c-135">註冊通知</span><span class="sxs-lookup"><span data-stu-id="1158c-135">Register for notifications</span></span>
<span data-ttu-id="1158c-136">這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="1158c-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="1158c-137">因為 hello 通道 hello Microsoft 推播通知服務 (MPNS) 所指派的 URI 可以隨時變更，您應該註冊通知經常 tooavoid 通知失敗。</span><span class="sxs-lookup"><span data-stu-id="1158c-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="1158c-138">每次該 hello 應用程式啟動時，這個範例會註冊通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="1158c-139">針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。</span><span class="sxs-lookup"><span data-stu-id="1158c-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="1158c-140">開啟 hello App.xaml.cs 檔案並加入 hello**非同步**修飾詞太**Application_Launching**方法，並取代 hello 通知中心註冊您加入程式碼中[開始使用通知中心]以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1158c-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="1158c-141">這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的註冊。</span><span class="sxs-lookup"><span data-stu-id="1158c-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="1158c-142">在 hello MainPage.xaml.cs 專案檔案中，加入下列程式碼會實作 hello hello **OnNavigatedTo**方法：</span><span class="sxs-lookup"><span data-stu-id="1158c-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="1158c-143">此更新 hello 主頁先前根據 hello 狀態儲存類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="1158c-144">hello 應用程式現在已完成，而且可以是儲存一組類別目錄中與 hello 通知中樞的 hello 裝置使用的本機儲存體 tooregister，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="1158c-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="1158c-145">接下來，我們會定義可以傳送類別通知 toothis 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1158c-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="1158c-146">傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="1158c-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="1158c-147">執行 hello 應用程式，並產生通知</span><span class="sxs-lookup"><span data-stu-id="1158c-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="1158c-148">在 Visual Studio 中，按下 F5 toocompile 並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1158c-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="1158c-149">Hello 應用程式 UI 提供一組切換，請注意，可讓您選擇以 hello 類別 toosubscribe。</span><span class="sxs-lookup"><span data-stu-id="1158c-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="1158c-150">啟用一或多個類別切換，然後按一下 [訂閱] 。</span><span class="sxs-lookup"><span data-stu-id="1158c-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="1158c-151">hello 應用程式將選取的 hello 類別轉換成標記，並從 hello 通知中樞要求新的裝置註冊 hello 選取標記。</span><span class="sxs-lookup"><span data-stu-id="1158c-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="1158c-152">hello 已註冊的類別會傳回並顯示在對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="1158c-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="1158c-153">之後收到確認，您類別中的已完成的訂用帳戶，執行 hello 主控台應用程式的每個類別目錄的 toosend 通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="1158c-154">請確認您只收到 hello 類別，您已訂閱的通知。</span><span class="sxs-lookup"><span data-stu-id="1158c-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="1158c-155">您已完成本主題。</span><span class="sxs-lookup"><span data-stu-id="1158c-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[開始使用通知中心]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

