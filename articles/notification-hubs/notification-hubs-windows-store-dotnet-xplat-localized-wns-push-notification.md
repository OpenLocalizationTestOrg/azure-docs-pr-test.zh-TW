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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>使用通知中樞 toosend 當地語系化重大消息
> [!div class="op_single_selector"]
> * [Windows 市集 C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
本主題說明如何 toouse hello**範本**Azure 通知中樞 toobroadcast 重大消息通知已當地語系化的語言和裝置的功能。 在本教學課程就開始 hello Windows 市集應用程式中建立[使用通知中樞 toosend 最新消息]。 完成時，您將會為您感興趣的類別可以 tooregister，tooreceive hello 通知，在指定的語言，並接收只推播通知 hello 選取類別以該語言。

有兩個部分 toothis 案例：

* hello Windows 市集應用程式可讓用戶端裝置 toospecify 語言和 toosubscribe toodifferent 重大新聞分類。
* hello 後端廣播 hello 通知，請使用 hello**標記**和**範本**feautres Azure 通知中心。

## <a name="prerequisites"></a>必要條件
您必須已經完成 hello[使用通知中樞 toosend 最新消息]教學課程，而且有 hello 程式碼，因為本教學課程是直接在該程式碼時。

您也需要 Visual Studio 2012 或更新版本。

## <a name="template-concepts"></a>範本概念
在[使用通知中樞 toosend 最新消息]建置的應用程式，使用**標記**toosubscribe toonotifications 不同新聞分類。
但有許多應用程式是以多個市場為目標的，因此需要當地語系化。 這表示 hello 通知會自行 hello 內容有 toobe 當地語系化，而且傳遞的 toohello 一組正確的裝置。
本主題中我們將示範如何 toouse hello**範本**tooeasily 傳遞的通知中樞的功能當地語系化重大消息通知。

注意： 其中一種方式 toosend 當地語系化通知是 toocreate 多個版本的每個標記。 比方說，toosupport 英文、 法文及中文，我們需要三個不同的標記世界新聞:"world_en"，"world_fr，"和"world_ch"。 我們必須 toosend 這些標記的 hello world 新聞 tooeach 的當地語系化的版本。 本主題中我們將會使用範本 tooavoid hello 擴散的標記以及將多個訊息傳送的 hello 需求。

在高的層級中，範本會方式 toospecify 如何特定裝置應該會收到通知。 hello 範本會指定藉由參考是由您的應用程式後端傳送 hello 訊息部分的 tooproperties hello 確切的裝載格式。 在此處的範例中，我們將傳送地區設定無從驗證、且包含所有支援語言的訊息：

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

然後我們會確保裝置註冊使用的範本，是指 toohello 正確的屬性。 比方說，想 tooreceive 的 Windows 市集應用程式的簡易快顯通知訊息會註冊下列任何對應的標記具有範本的 hello:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



範本的功能非常強大，您可以在 [範本](notification-hubs-templates-cross-platform-push-messages.md) 一文中了解詳情。 

## <a name="hello-app-user-interface"></a>hello 應用程式使用者介面
我們現在將會修改您建立 hello 主題中的 hello 即時新聞應用程式[使用通知中樞 toosend 最新消息]toosend 當地語系化使用範本的重大消息。

在您的 Windows 市集應用程式中：

變更您 MainPage.xaml tooinclude 地區設定下拉式方塊：

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

## <a name="building-hello-windows-store-client-app"></a>建立 hello Windows 市集用戶端應用程式
1. 在通知類別中，加入地區設定參數 tooyour *StoreCategoriesAndSubscribe*和*SubscribeToCateories*方法。
   
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
   
    請注意，而不是呼叫 hello *RegisterNativeAsync*方法我們呼叫*RegisterTemplateAsync*： 登錄中的 hello 範本取決於 hello 地區設定特定的通知格式。 我們也提供 hello 範本 (「 localizedWNSTemplateExample") 的名稱，因為我們可能會想 tooregister 多個範本 （例如一個快顯通知），另一個圖格，我們需要 tooname 中順序 toobe 無法 tooupdate 或刪除它們。
   
    請注意，是否裝置具有相同標記，標記會導致為目標的內送訊息的 hello 註冊多個範本的多個通知傳遞 toohello 裝置 （一個用於每個範本）。 這種行為時相當實用 hello 相同的邏輯訊息 tooresult 在多個視覺通知中，執行個體中的 Windows 市集應用程式中顯示 徽章和快顯通知。
2. 新增下列方法 tooretrieve hello 儲存的地區設定的 hello:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. 在您 mainpage.xaml.cs 中，更新您的按鈕 click 處理常式擷取 hello hello 地區設定下拉式方塊的目前值，並提供 toohello 呼叫 toohello 通知類別，如下所示：
   
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
4. 最後，在 App.xaml.cs 檔案中，請確定 tooupdate 您`InitNotificationsAsync`方法 tooretrieve hello 地區設定和訂閱時使用它：
   
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

## <a name="send-localized-notifications-from-your-back-end"></a>從後端傳送已當地語系化的通知
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
