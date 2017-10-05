---
title: "使用通知中樞傳送即時新聞 (Windows Universal)"
description: "使用 Azure 通知中樞搭配註冊中的標籤，將重大新聞傳送至通用 Windows 應用程式。"
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
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a>使用通知中心傳送即時新聞
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>概觀
本主題將說明如何使用 Azure 通知中樞，將即時新聞通知廣播至 Windows Store 或 Windows Phone 8.1 (非 Silverlight) 應用程式。 如果您的目標是 Windows Phone 8.1 Silverlight，請參閱 [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) 版本。 完成時，您便能夠註冊您所感興趣的即時新聞類別，並僅接收這些類別的推播通知。 此情況是許多應用程式的共同模式，這些應用程式必須將通知傳送給先前宣告對通知有興趣的使用者群組，例如，RSS 閱讀程式、供樂迷使用的應用程式等等。 

在通知中樞內建立註冊時，您可以透過包含一或多個 *tags* 來啟用廣播案例。 當標籤收到通知時，所有已註冊此標籤的裝置都會收到通知。 由於標籤只是簡單的字串而已，您無需預先佈建標籤。 如需標籤的詳細資訊，請參閱 [通知中樞路由與標記運算式](notification-hubs-tags-segment-push-message.md)。

> [!NOTE]
> Windows 市集和 Windows Phone 8.1 版與更早版本的專案在 Visual Studio 2017 不受支援。  如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。 

## <a name="prerequisites"></a>必要條件
本主題會以您在[開始使用通知中樞][get-started]中所建立的應用程式為基礎。 開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。

## <a name="add-category-selection-to-the-app"></a>在應用程式中新增類別選項
第一個步驟是在您的現有主頁面上新增 UI 元素，以便使用者選取要註冊的類別。 使用者所選取的類別會儲存在裝置上。 啟動應用程式時，您的通知中心內會建立以所選取類別作為標籤的裝置註冊。

1. 開啟 MainPage.xaml 專案檔案，然後在 **Grid** 元素中複製下列程式碼：
   
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
2. 以滑鼠右鍵按一下 [共用] 專案中、新增名為 **Notifications** 的新類別、將 **public** 修飾詞新增至類別定義，然後在新的程式碼檔案中新增下列 **using** 陳述式：
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. 將下列程式碼複製到新的 **Notifications** 類別：
   
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
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    本類別會使用本機儲存體來儲存此裝置必須接收的新聞類別。 請注意，我們呼叫 *RegisterTemplateAsync* 而非 *RegisterNativeAsync* 方法來註冊使用範本註冊的類別。 
   
    我們也為範本提供名稱 ("simpleWNSTemplateExample")，因為我們可能會想註冊多個範本 (例如，一個供快顯通知使用，一個供磚使用)，而且我們必須為其命名，才能加以更新或刪除。
   
    請注意，如果有裝置使用相同的標籤註冊多個範本，一個以該標籤為目標的傳入訊息將會使多個通知傳遞至裝置 (每個範本各一個)。 此行為在相同的邏輯訊息必須產生多個視覺化通知時將有所幫助，例如，在一個 Windows 市集應用程式中同時顯示徽章和快顯通知。
   
    如需範本的詳細資訊，請參閱 [範本](notification-hubs-templates-cross-platform-push-messages.md)。
4. 在 App.xaml.cs 專案檔案中，新增下列屬性至 **App** 類別：
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    此屬性可用來建立並存取 **Notifications** 執行個體。
   
    在上述程式碼中，使用您的通知中樞名稱及先前取得的 *DefaultListenSharedAccessSignature* 連接字串，來取代 `<hub name>` 和 `<connection string with listen access>` 預留位置。
   
   > [!NOTE]
   > 因為隨用戶端應用程式散佈的憑證通常不安全，您應只將接聽存取權的金鑰隨用戶端應用程式散佈。 您的應用程式可透過接聽存取權來註冊通知，但無法修改現有的註冊或無法傳送通知。 在安全的後端服務中，會使用完整存取金鑰來傳送通知和變更現有的註冊。
   > 
   > 
5. 在 MainPage.xaml.cs 中新增下列程式碼行：
   
        using Windows.UI.Popups;
6. 在 MainPage.xaml.cs 專案檔案中新增下列方法：
   
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
   
    此方法會建立一份類別清單，並使用 **Notifications** 類別在本機儲存體中儲存清單，並在通知中心註冊對應標籤。 變更類別時，系統會使用新類別重新建立註冊。

您的應用程式現在可以在裝置上的本機儲存體中儲存一組類別，並在使用者每次變更類別選項時在通知中心註冊。

## <a name="register-for-notifications"></a>註冊通知
這些步驟會在啟動時，使用已儲存在本機儲存體中的類別在通知中心註冊。

> [!NOTE]
> 由於 Windows 通知服務 (WNS) 所指派的通道 URI 可以隨時變更，您應經常註冊通知以避免通知失敗。 此範例會在應用程式每次啟動時註冊通知。 若是經常執行 (一天多次) 的應用程式，如果距離上次註冊的時間不到一天，則您可能可以略過註冊以保留頻寬。
> 
> 

1. 開啟 App.xaml.cs 檔案並更新 **InitNotificationsAsync** 方法，以使用 `notifications` 類別根據類別來訂閱。
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    這會確保應用程式每次啟動時都會從本機儲存體擷取類別，並要求這些類別的註冊。 [開始使用通知中樞][get-started]教學課程的一部分是建立 **InitNotificationsAsync** 方法。
2. 在 MainPage.xaml.cs 專案檔案中，在 *OnNavigatedTo* 方法中新增下列程式碼：
   
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
   
    這會根據原先儲存的類別狀態更新主頁面。

現在已完成此應用程式，且可在裝置本機儲存體中儲存一組類別，以供每次使用者變更類別選項在通知中心註冊時使用。 接著，我們會定義可將類別通知傳送至此應用程式的後端。

## <a name="sending-tagged-notifications"></a>傳送加註標記的通知
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a>執行應用程式並產生通知
1. 在 Visual Studio 中，按 F5 以編譯並啟動應用程式。
   
    ![][1]
   
    請注意，應用程式 UI 提供一組切換，可讓您選擇要訂閱的類別。
2. 啟用一或多個類別切換，然後按一下 [訂閱] 。
   
    應用程式會將選取的類別轉換成標籤，並在通知中心內為選取的標籤要求新裝置註冊。 系統會傳回已註冊類別並顯示在對話方塊中。
   
    ![][19]
3. 若要從後端傳送新通知，您可以使用下列其中一種方式：
   
   * **主控台應用程式：** 啟動主控台應用程式。
   * **Java/PHP：** 執行您的應用程式/指令碼。
     
     選取的類別通知會以快顯通知方式出現。
     
     ![][14]

## <a name="next-steps"></a>後續步驟
在本教學課程中，我們了解到如何按類別廣播即時新聞。 請考慮完成下列其中一個強調其他進階通知中心案例的教學課程：

* [使用通知中樞廣播已當地語系化的即時新聞]
  
    了解如何擴充即時新聞應用程式，以啟用傳送已當地語系化的通知。

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[使用通知中樞廣播已當地語系化的即時新聞]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
