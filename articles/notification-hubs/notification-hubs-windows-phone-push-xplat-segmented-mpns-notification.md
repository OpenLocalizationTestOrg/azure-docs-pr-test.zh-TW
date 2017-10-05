---
title: "使用通知中樞傳送即時新聞 (Windows Phone)"
description: "使用 Azure 通知中樞在註冊中使用標籤，將重大新聞傳送至通用 Windows Phone 應用程式。"
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
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="7cf86-103">使用通知中心傳送即時新聞</span><span class="sxs-lookup"><span data-stu-id="7cf86-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="7cf86-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7cf86-104">Overview</span></span>
<span data-ttu-id="7cf86-105">本主題將說明如何使用 Azure 通知中樞，將即時新聞通知廣播至 Windows Phone 8.0/8.1 Silverlight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cf86-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="7cf86-106">如果您的目標是 Windows Store 或 Windows Phone 8.1 應用程式，請參閱 [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) 版本。</span><span class="sxs-lookup"><span data-stu-id="7cf86-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="7cf86-107">完成時，您便能夠註冊您所感興趣的即時新聞類別，並僅接收這些類別的推播通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="7cf86-108">此情況是許多應用程式的共同模式，這些應用程式必須將通知傳送給先前宣告對通知有興趣的使用者群組，例如，RSS 閱讀程式、供樂迷使用的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="7cf86-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="7cf86-109">在通知中樞內建立註冊時，您可以透過包含一或多個 *tags* 來啟用廣播案例。</span><span class="sxs-lookup"><span data-stu-id="7cf86-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="7cf86-110">當標籤收到通知時，所有已註冊此標籤的裝置都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="7cf86-111">由於標籤只是簡單的字串而已，您無需預先佈建標籤。</span><span class="sxs-lookup"><span data-stu-id="7cf86-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="7cf86-112">如需標籤的詳細資訊，請參閱 [通知中樞路由與標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="7cf86-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cf86-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7cf86-113">Prerequisites</span></span>
<span data-ttu-id="7cf86-114">本主題會以您在 [開始使用通知中心]中所建立的應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="7cf86-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="7cf86-115">開始本教學課程之前，您必須已完成 [開始使用通知中心]。</span><span class="sxs-lookup"><span data-stu-id="7cf86-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="7cf86-116">在應用程式中新增類別選項</span><span class="sxs-lookup"><span data-stu-id="7cf86-116">Add category selection to the app</span></span>
<span data-ttu-id="7cf86-117">第一個步驟是在您的現有主頁面上新增 UI 元素，以便使用者選取要註冊的類別。</span><span class="sxs-lookup"><span data-stu-id="7cf86-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="7cf86-118">使用者所選取的類別會儲存在裝置上。</span><span class="sxs-lookup"><span data-stu-id="7cf86-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="7cf86-119">啟動應用程式時，您的通知中心內會建立以所選取類別作為標籤的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="7cf86-120">開啟 MainPage.xaml 專案檔，然後使用下列程式碼來取代名為 `TitlePanel` 和 `ContentPanel` 的 **Grid** 元素：</span><span class="sxs-lookup"><span data-stu-id="7cf86-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
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
2. <span data-ttu-id="7cf86-121">在此專案中，建立名為 **Notifications** 的新類別，並將 **public** 修飾詞新增至類別定義，然後在新的程式碼檔案中新增下列 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7cf86-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="7cf86-122">將下列程式碼複製到新的 **Notifications** 類別：</span><span class="sxs-lookup"><span data-stu-id="7cf86-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
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
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
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
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
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
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="7cf86-123">本類別使用獨立儲存體，來儲存此裝置接收的新聞類別。</span><span class="sxs-lookup"><span data-stu-id="7cf86-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="7cf86-124">它也包含使用 [範本](notification-hubs-templates-cross-platform-push-messages.md) 通知來註冊這些類別的方法。</span><span class="sxs-lookup"><span data-stu-id="7cf86-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="7cf86-125">在 App.xaml.cs 專案檔案中，新增下列屬性至 **App** 類別。</span><span class="sxs-lookup"><span data-stu-id="7cf86-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="7cf86-126">以您的通知中樞名稱與先前取得的 *DefaultListenSharedAccessSignature* 連接字串，取代 `<hub name>` 和 `<connection string with listen access>` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="7cf86-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="7cf86-127">因為隨用戶端應用程式散佈的憑證通常不安全，您應只將接聽存取權的金鑰隨用戶端應用程式散佈。</span><span class="sxs-lookup"><span data-stu-id="7cf86-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="7cf86-128">您的應用程式可透過接聽存取權來註冊通知，但無法修改現有的註冊或無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="7cf86-129">在安全的後端服務中，會使用完整存取金鑰來傳送通知和變更現有的註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="7cf86-130">在 MainPage.xaml.cs 中新增下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="7cf86-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="7cf86-131">在 MainPage.xaml.cs 專案檔案中新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="7cf86-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="7cf86-132">此方法會建立一份類別清單，並使用 **Notifications** 類別在本機儲存體中儲存清單，並在通知中心註冊對應標籤。</span><span class="sxs-lookup"><span data-stu-id="7cf86-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="7cf86-133">變更類別時，系統會使用新類別重新建立註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="7cf86-134">您的應用程式現在可以在裝置上的本機儲存體中儲存一組類別，並在使用者每次變更類別選項時在通知中心註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="7cf86-135">註冊通知</span><span class="sxs-lookup"><span data-stu-id="7cf86-135">Register for notifications</span></span>
<span data-ttu-id="7cf86-136">這些步驟會在啟動時，使用已儲存在本機儲存體中的類別在通知中心註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf86-137">由於 Microsoft 推播通知服務 (WPNS) 所指派的通道 URI 可能隨時會變更，因此您應經常註冊通知以避免通知失敗。</span><span class="sxs-lookup"><span data-stu-id="7cf86-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="7cf86-138">此範例會在應用程式每次啟動時註冊通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="7cf86-139">若是經常執行 (一天多次) 的應用程式，如果距離上次註冊的時間不到一天，則您可能可以略過註冊以保留頻寬。</span><span class="sxs-lookup"><span data-stu-id="7cf86-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="7cf86-140">開啟 App.xaml.cs 檔案，並將 **async** 修飾詞新增至 **Application_Launching** 方法，同時使用以下代碼，取代您新增至[開始使用通知中心]中的通知中樞註冊代碼：</span><span class="sxs-lookup"><span data-stu-id="7cf86-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="7cf86-141">這會確保應用程式每次啟動時都會從本機儲存體擷取類別，並要求這些類別的註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="7cf86-142">在 MainPage.xaml.cs 專案檔案中，新增下列實作 **OnNavigatedTo** 方法的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7cf86-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="7cf86-143">這會根據原先儲存的類別狀態更新主頁面。</span><span class="sxs-lookup"><span data-stu-id="7cf86-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="7cf86-144">現在已完成此應用程式，且可在裝置本機儲存體中儲存一組類別，以供每次使用者變更類別選項在通知中心註冊時使用。</span><span class="sxs-lookup"><span data-stu-id="7cf86-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="7cf86-145">接著，我們會定義可將類別通知傳送至此應用程式的後端。</span><span class="sxs-lookup"><span data-stu-id="7cf86-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="7cf86-146">傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="7cf86-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="7cf86-147">執行應用程式並產生通知</span><span class="sxs-lookup"><span data-stu-id="7cf86-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="7cf86-148">在 Visual Studio 中，按 F5 以編譯並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cf86-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="7cf86-149">請注意，應用程式 UI 提供一組切換，可讓您選擇要訂閱的類別。</span><span class="sxs-lookup"><span data-stu-id="7cf86-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="7cf86-150">啟用一或多個類別切換，然後按一下 [訂閱] 。</span><span class="sxs-lookup"><span data-stu-id="7cf86-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="7cf86-151">應用程式會將選取的類別轉換成標籤，並在通知中心內為選取的標籤要求新裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="7cf86-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="7cf86-152">系統會傳回已註冊類別並顯示在對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="7cf86-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="7cf86-153">收到確認已完成您各項類別的訂閱之後，執行主控台應用程式，傳送每種類別的通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="7cf86-154">請確認您只會收到所訂閱類別的通知。</span><span class="sxs-lookup"><span data-stu-id="7cf86-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="7cf86-155">您已完成本主題。</span><span class="sxs-lookup"><span data-stu-id="7cf86-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="7cf86-156">[開始使用通知中心]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="7cf86-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

