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
# <a name="use-notification-hubs-toosend-breaking-news"></a>使用通知中樞 toosend 最新消息
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>概觀
本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooa Windows Phone 8.0/8.1 Silverlight 應用程式。 如果您的目標 Windows 市集或 Windows Phone 8.1 應用程式，請參閱 tootoohello [Windows 通用](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md)版本。 完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。 這個案例是許多應用程式的常見模式，通知其中有傳送 toobe toogroups 的先前尚未宣告欄位，例如 RSS 讀取器、 應用程式等的音樂迷感興趣的使用者。

啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。 當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。 標記是只是字串，因為它們不需要預先佈建 toobe。 如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。

## <a name="prerequisites"></a>必要條件
本主題是根據您在建立 hello 應用程式[開始使用通知中心]。 開始本教學課程之前，您必須已完成 [開始使用通知中心]。

## <a name="add-category-selection-toohello-app"></a>加入類別目錄選取 toohello 應用程式
hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要頁面，啟用 hello 使用者 tooselect 類別 tooregister。 使用者選取的 hello 類別會儲存在 hello 裝置。 Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。

1. 開啟 hello MainPage.xaml 專案檔案，然後取代 hello**方格**名為的項目`TitlePanel`和`ContentPanel`以下列程式碼的 hello:
   
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
2. Hello 專案中建立新的類別，名為**通知**，新增 hello**公用**修飾詞 toohello 類別定義，然後加入下列 hello**使用**陳述式toohello 新程式碼檔案：
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. 複製 hello 下列程式碼至新的 hello**通知**類別：
   
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

    這個類別使用新聞此裝置正在 tooreceive hello 隔離儲存體 toostore hello 的類別。 它也包含使用這些類別的方法 tooregister[範本](notification-hubs-templates-cross-platform-push-messages.md)通知登錄。


1. 在 hello App.xaml.cs 專案檔案中，加入下列屬性 toohello hello**應用程式**類別。 取代 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*您稍早取得。
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > 發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。 接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。 hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。
   > 
   > 
2. 在您 MainPage.xaml.cs 加入以下的 hello:
   
        using Windows.UI.Popups;
3. 在 hello MainPage.xaml.cs 專案檔中加入下列方法 hello:
   
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
   
    這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。 類別目錄會變更時，重新建立 hello 註冊 hello 新類別。

您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。

## <a name="register-for-notifications"></a>註冊通知
這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。

> [!NOTE]
> 因為 hello 通道 hello Microsoft 推播通知服務 (MPNS) 所指派的 URI 可以隨時變更，您應該註冊通知經常 tooavoid 通知失敗。 每次該 hello 應用程式啟動時，這個範例會註冊通知。 針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。
> 
> 

1. 開啟 hello App.xaml.cs 檔案並加入 hello**非同步**修飾詞太**Application_Launching**方法，並取代 hello 通知中心註冊您加入程式碼中[開始使用通知中心]以下列程式碼的 hello:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的註冊。
2. 在 hello MainPage.xaml.cs 專案檔案中，加入下列程式碼會實作 hello hello **OnNavigatedTo**方法：
   
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
   
    此更新 hello 主頁先前根據 hello 狀態儲存類別。

hello 應用程式現在已完成，而且可以是儲存一組類別目錄中與 hello 通知中樞的 hello 裝置使用的本機儲存體 tooregister，每當 hello 使用者變更 hello 選取的類別。 接下來，我們會定義可以傳送類別通知 toothis 應用程式後端。

## <a name="sending-tagged-notifications"></a>傳送加註標記的通知
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>執行 hello 應用程式，並產生通知
1. 在 Visual Studio 中，按下 F5 toocompile 並啟動 hello 應用程式。
   
    ![][1]
   
    Hello 應用程式 UI 提供一組切換，請注意，可讓您選擇以 hello 類別 toosubscribe。
2. 啟用一或多個類別切換，然後按一下 [訂閱] 。
   
    hello 應用程式將選取的 hello 類別轉換成標記，並從 hello 通知中樞要求新的裝置註冊 hello 選取標記。 hello 已註冊的類別會傳回並顯示在對話方塊中。
   
    ![][2]
3. 之後收到確認，您類別中的已完成的訂用帳戶，執行 hello 主控台應用程式的每個類別目錄的 toosend 通知。 請確認您只收到 hello 類別，您已訂閱的通知。
   
    ![][3]

您已完成本主題。

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

