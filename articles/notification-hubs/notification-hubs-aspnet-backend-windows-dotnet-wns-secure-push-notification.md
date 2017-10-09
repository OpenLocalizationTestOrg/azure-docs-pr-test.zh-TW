---
title: "aaaAzure 集線器安全推播通知"
description: "了解如何安全 toosend 推播通知在 Azure 中。 以 C# 使用 hello.NET API 撰寫的程式碼範例。"
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure 通知中心安全推播
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
在 Microsoft Azure 推播通知支援可讓您 tooaccess 方便使用、 多平台、 向外延展的推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。

有時候 tooregulatory 或安全性條件約束，因為應用程式可能會想 tooinclude 中無法透過 hello 標準的推播通知基礎結構傳送的 hello 通知。 本教學課程描述 tooachieve 如何透過 hello 用戶端裝置與 hello 應用程式後端之間的安全、 已驗證連線的機密資訊傳送 hello 相同的體驗。

在高層級，hello 流程如下所示：

1. hello 應用程式後端：
   * 在後端資料庫中儲存安全裝載。
   * 會傳送 hello （傳送不安全的資訊） 此通知 toohello 裝置識別碼。
2. hello 在裝置上，當收到 hello 通知 hello 應用程式：
   * hello 裝置會連絡 hello 後端要求 hello 安全內容。
   * hello 應用程式可以顯示 hello 裝載為 hello 裝置上的通知。

請務必 toonote hello 上述流程中 （並在本教學課程），我們會假設該 hello 裝置會儲存在本機儲存體，驗證語彙基元之後 hello 使用者登入。 這樣可保證完全完美無瑕的體驗，如 hello 裝置可以擷取 hello 通知安全裝載使用這個語彙基元。 如果您的應用程式不會儲存驗證語彙基元 hello 在裝置上，或可以過期這些語彙基元，hello 裝置的應用程式，並收到 hello 通知應該會顯示提示 hello 使用者 toolaunch hello 應用程式的一般通知。 hello 應用程式然後驗證 hello 使用者，並顯示 hello 通知裝載。

此安全發送教學課程會示範如何 toosend 推播通知安全的方式。 hello 教學課程是 hello[通知使用者](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)教學課程中，因此，您應該完成 hello 步驟在該教學課程中第一次。

> [!NOTE]
> 本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Windows 市集)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)中所述。
> 另請注意，Windows Phone 8.1 需要 Windows (不是 Windows Phone) 認證，且無法在 Windows Phone 8.0 或 Silverlight 8.1 上使用背景工作。 對於 Windows 市集應用程式，您才可以接收通知，透過背景工作 hello 應用程式已啟用鎖定畫面 （按一下 hello Appmanifest hello 核取方塊）。
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>修改 hello Windows Phone 專案
1. 在 hello **NotifyUserWindowsPhone**專案中，加入下列程式碼 tooApp.xaml.cs tooregister hello 發送背景工作的 hello。 新增下列一行程式碼結尾 hello hello hello`OnLaunched()`方法：
   
        RegisterBackgroundTask();
2. 仍在 App.xaml.cs，加入下列程式碼後面 hello hello`OnLaunched()`方法：
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. 新增下列 hello`using`在 hello hello App.xaml.cs 檔案最上方的陳述式：
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. 從 hello**檔案**功能表在 Visual Studio 中，按一下**全部儲存**。

## <a name="create-hello-push-background-component"></a>建立 hello 推送背景元件
hello 下一個步驟是 toocreate hello 發送背景元件。

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello hello 解決方案的最上層的節點 (**方案 SecurePush**在此情況下)，然後按一下**新增**，然後按一下**新專案**。
2. 展開 [市集應用程式]，並按一下 [Windows Phone 應用程式]，然後按一下 [Windows 執行階段元件 (Windows Phone)]。 名稱 hello 專案**PushBackgroundComponent**，然後按一下**確定**toocreate hello 專案。
   
    ![][12]
3. 在 方案總管 中，以滑鼠右鍵按一下 hello **PushBackgroundComponent (Windows Phone 8.1)**專案，然後按一下 **新增**，然後按一下 **類別**。 Hello 新類別命名**PushBackgroundTask.cs**。 按一下**新增**toogenerate hello 類別。
4. 取代 hello hello 整個內容**PushBackgroundComponent**命名空間定義，以下列程式碼，以取代 hello 預留位置 hello`{back-end endpoint}`與 hello 後端端點取得部署時您後端：
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **PushBackgroundComponent (Windows Phone 8.1)**專案，然後按一下**管理 NuGet 封裝**。
6. 在 hello 左側，按一下 **線上**。
7. 在 hello**搜尋**方塊中，輸入**Http 用戶端**。
8. 在 hello 結果清單中，按一下  **Microsoft HTTP Client Libraries**，然後按一下**安裝**。 完成 hello 安裝。
9. 在 hello NuGet**搜尋**方塊中，輸入**Json.net**。 安裝 hello **Json.NET**封裝，然後關閉 hello NuGet 封裝管理員 視窗。
10. 新增下列 hello`using`在 hello hello 最上方的陳述式**PushBackgroundTask.cs**檔案：
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. 在 方案總管中 hello **NotifyUserWindowsPhone (Windows Phone 8.1)**專案中，以滑鼠右鍵按一下**參考**，然後按一下**加入參考...**.在 hello 參考管理員對話方塊中，核取 hello 方塊旁太**PushBackgroundComponent**，然後按一下**確定**。
12. 在 [方案總管] 中，按兩下**Package.appxmanifest**在 hello **NotifyUserWindowsPhone (Windows Phone 8.1)**專案。 在下**通知**，將**快顯能夠**太**是**。
    
    ![][3]
13. 仍在**Package.appxmanifest**，按一下 hello**宣告**靠近 hello 頂端的功能表。 在 hello**可用宣告**下拉式清單中，按一下**背景工作**，然後按一下**新增**。
14. 在 **Package.appxmanifest** 中，核取 [屬性] 下的 [推播通知]。
15. 在**Package.appxmanifest**下**應用程式設定**，型別**PushBackgroundComponent.PushBackgroundTask**在 hello**進入點**欄位。
    
    ![][13]
16. 從 hello**檔案**功能表上，按一下 **全部儲存**。

## <a name="run-hello-application"></a>執行 hello 應用程式
toorun hello 應用程式中，執行下列 hello:

1. 在 Visual Studio 中，執行 hello **AppBackend** Web API 應用程式。 [ASP.NET Web] 頁面便會隨即顯示。
2. 在 Visual Studio 中，執行 hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone 應用程式。 hello Windows Phone 模擬器中執行，並自動載入 hello 應用程式。
3. 在 hello **NotifyUserWindowsPhone**應用程式 UI 中，輸入使用者名稱和密碼。 這些可以是任何字串，但它們必須 hello 相同的值。
4. 在 hello **NotifyUserWindowsPhone**應用程式 UI 中，按一下**登入並註冊**。 然後按一下 [傳送推播] 。

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
