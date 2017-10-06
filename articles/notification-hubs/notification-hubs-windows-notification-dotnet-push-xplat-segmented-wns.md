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
# <a name="use-notification-hubs-toosend-breaking-news"></a>使用通知中樞 toosend 最新消息
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>概觀
本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooa Windows 市集或 Windows Phone 8.1 (非 Silverlight) 應用程式。 如果您的目標 Windows Phone 8.1 Silverlight，請參閱 toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md)版本。 完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。 此案例中是通知其中具有先前尚未宣告感興趣，例如 RSS 讀取器，音樂迷，應用程式及等等的使用者傳送 toobe toogroups 許多應用程式的常見模式。 

啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。 當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。 標記是只是字串，因為它們不需要預先佈建 toobe。 如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。

> [!NOTE]
> Windows 市集和 Windows Phone 8.1 版與更早版本的專案在 Visual Studio 2017 不受支援。  如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。 

## <a name="prerequisites"></a>必要條件
本主題是根據您在建立 hello 應用程式[開始使用通知中樞][get-started]。 開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。

## <a name="add-category-selection-toohello-app"></a>加入類別目錄選取 toohello 應用程式
hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要頁面，啟用 hello 使用者 tooselect 類別 tooregister。 使用者選取的 hello 類別會儲存在 hello 裝置。 Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。

1. 開啟 hello MainPage.xaml 專案檔案，然後複製下列程式碼中 hello 的 hello**方格**項目：
   
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
2. 以滑鼠右鍵按一下 hello**共用**專案，並加入新的類別，名為**通知**，新增 hello**公用**修飾詞 toohello 類別定義，然後新增下列 hello **使用**陳述式 toohello 新程式碼檔案：
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. 複製 hello 下列程式碼至新的 hello**通知**類別：
   
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
   
    這個類別使用新聞此裝置有 tooreceive hello 本機儲存體 toostore hello 的類別。 請注意，而不是呼叫 hello *RegisterNativeAsync*方法我們呼叫*RegisterTemplateAsync* tooregister hello 類別使用的範本註冊。 
   
    我們也提供 hello 範本 (「 simpleWNSTemplateExample") 的名稱，因為我們可能會想 tooregister 多個範本 （例如一個快顯通知），另一個圖格，我們需要 tooname 中順序 toobe 無法 tooupdate 或刪除它們。
   
    請注意，是否裝置具有相同標記，標記會導致為目標的內送訊息的 hello 註冊多個範本的多個通知傳遞 toohello 裝置 （一個用於每個範本）。 這種行為時相當實用 hello 相同的邏輯訊息 tooresult 在多個視覺通知中，執行個體中的 Windows 市集應用程式中顯示 徽章和快顯通知。
   
    如需範本的詳細資訊，請參閱 [範本](notification-hubs-templates-cross-platform-push-messages.md)。
4. 在 hello App.xaml.cs 專案檔案中，加入下列屬性 toohello hello**應用程式**類別：
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    這個屬性是使用的 toocreate 及存取**通知**執行個體。
   
    在上述程式碼的 hello，取代 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*您稍早取得。
   
   > [!NOTE]
   > 發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。 接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。 hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。
   > 
   > 
5. 在您 MainPage.xaml.cs 加入以下的 hello:
   
        using Windows.UI.Popups;
6. 在 hello MainPage.xaml.cs 專案檔中加入下列方法 hello:
   
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
   
    這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。 類別目錄會變更時，重新建立 hello 註冊 hello 新類別。

您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。

## <a name="register-for-notifications"></a>註冊通知
這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。

> [!NOTE]
> 因為 hello 通道 hello Windows 通知服務 (WNS) 所指派的 URI 可以隨時變更，您應該註冊通知經常 tooavoid 通知失敗。 每次該 hello 應用程式啟動時，這個範例會註冊通知。 針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。
> 
> 

1. 開啟 hello App.xaml.cs 檔案並更新 hello **InitNotificationsAsync**方法 toouse hello`notifications`類別 toosubscribe 類別為基礎。
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的登錄。 hello **InitNotificationsAsync**方法建立 hello 一部分[開始使用通知中樞][ get-started]教學課程。
2. 在 hello MainPage.xaml.cs 專案檔案中，加入下列程式碼 toohello hello *OnNavigatedTo*方法：
   
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
   
    ![][19]
3. 將新的通知傳送 hello 後端 hello 下列方式之一：
   
   * **主控台應用程式：**啟動 hello 主控台應用程式。
   * **Java/PHP：** 執行您的應用程式/指令碼。
     
     通知 hello 選取類別目錄會顯示為快顯通知。
     
     ![][14]

## <a name="next-steps"></a>後續步驟
在此教學課程中我們學到如何 toobroadcast 依類別目錄中最新消息。 完成下列其中一個 hello 下列反白顯示其他進階的通知中心案例的教學課程，請考慮：

* [使用通知中樞 toobroadcast 當地語系化重大消息]
  
    了解如何傳送 tooenable 新聞應用程式的重大 tooexpand hello 當地語系化通知。

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
