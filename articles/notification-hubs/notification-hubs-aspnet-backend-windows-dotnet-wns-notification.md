---
title: "與.NET 後端 aaaAzure 通知中樞通知使用者"
description: "了解如何安全 toosend 推播通知在 Azure 中。 以 C# 使用 hello.NET API 撰寫的程式碼範例。"
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="eb44d-104">Azure 通知中樞透過 .NET 後端通知使用者</span><span class="sxs-lookup"><span data-stu-id="eb44d-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="eb44d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="eb44d-105">Overview</span></span>
<span data-ttu-id="eb44d-106">在 Azure 中的推播通知支援可讓您 tooaccess 方便使用、 多平台，並向外延展推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。</span><span class="sxs-lookup"><span data-stu-id="eb44d-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="eb44d-107">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 特定的應用程式使用者在特定的裝置上。</span><span class="sxs-lookup"><span data-stu-id="eb44d-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="eb44d-108">ASP.NET WebAPI 後端會使用的 tooauthenticate 用戶端。</span><span class="sxs-lookup"><span data-stu-id="eb44d-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="eb44d-109">使用 hello 驗證用戶端的使用者，且標記將會自動加入 hello 後端 toonotification 登錄。</span><span class="sxs-lookup"><span data-stu-id="eb44d-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="eb44d-110">此標籤將會使用的 toosend hello 後端 toogenerate 通知特定使用者所。</span><span class="sxs-lookup"><span data-stu-id="eb44d-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="eb44d-111">如需有關註冊使用應用程式後端的通知的詳細資訊，請參閱 hello 指引主題[從您的應用程式後端註冊](http://msdn.microsoft.com/library/dn743807.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eb44d-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="eb44d-112">本教學課程是 hello 通知中樞及您在 hello 中建立的專案[開始使用通知中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb44d-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="eb44d-113">本教學課程也是 hello 必要條件 toohello[安全推送]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb44d-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="eb44d-114">您已完成本教學課程中的 hello 步驟之後，您可以繼續 toohello[安全推送]教學課程，其中顯示 toomodify hello 程式碼如何在此教學課程 toosend 推播通知安全的方式。</span><span class="sxs-lookup"><span data-stu-id="eb44d-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eb44d-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="eb44d-115">Before you begin</span></span>
<span data-ttu-id="eb44d-116">我們非常重視您的意見反應。</span><span class="sxs-lookup"><span data-stu-id="eb44d-116">We do take your feedback seriously.</span></span> <span data-ttu-id="eb44d-117">如果您有任何問題，完成此主題中或改善此內容的建議，我們非常感謝您在 hello hello 頁面底部的意見反應。</span><span class="sxs-lookup"><span data-stu-id="eb44d-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="eb44d-118">hello 完成本教學課程中的程式碼可以在 GitHub 上找到[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)。</span><span class="sxs-lookup"><span data-stu-id="eb44d-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb44d-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="eb44d-119">Prerequisites</span></span>
<span data-ttu-id="eb44d-120">在開始本教學課程之前，您必須已完成下列行動服務教學課程：</span><span class="sxs-lookup"><span data-stu-id="eb44d-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="eb44d-121">[開始使用通知中樞]</span><span class="sxs-lookup"><span data-stu-id="eb44d-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="eb44d-122">您建立通知中樞保留 hello 應用程式名稱，並在本教學課程中註冊 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="eb44d-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="eb44d-123">本教學課程假設您已完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="eb44d-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="eb44d-124">如果沒有，請依照中的 hello 步驟[開始使用通知中樞 （Windows 市集）](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)，明確地說 hello 區段[註冊 hello Windows 市集應用程式](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store)和[設定您的通知中樞](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)。</span><span class="sxs-lookup"><span data-stu-id="eb44d-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="eb44d-125">特別是，確定您已輸入 hello**封裝 SID**和**用戶端密碼**值在 hello 入口網站中 hello**設定**通知中樞 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="eb44d-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="eb44d-126">此組態程序以 hello 一節所述[設定通知中樞](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)。</span><span class="sxs-lookup"><span data-stu-id="eb44d-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="eb44d-127">這是一個重要步驟： hello 推播通知若 hello hello 入口網站上的認證不符合所指定如您所選擇的 hello 應用程式名稱，將會失敗。</span><span class="sxs-lookup"><span data-stu-id="eb44d-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="eb44d-128">如果您使用行動應用程式在 Azure App Service 中作為後端服務，請參閱 hello[行動應用程式版本](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb44d-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="eb44d-129">更新 hello hello 用戶端專案的程式碼</span><span class="sxs-lookup"><span data-stu-id="eb44d-129">Update hello code for hello client project</span></span>
<span data-ttu-id="eb44d-130">在本節中，您更新您已完成 hello hello 專案中的 hello 程式碼[開始使用通知中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb44d-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="eb44d-131">hello 應該已經與 hello 存放區相關聯及設定通知中樞。</span><span class="sxs-lookup"><span data-stu-id="eb44d-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="eb44d-132">在本節中，您會加入程式碼 toocall hello 新 WebAPI 的後端，以及使用它來註冊及傳送通知。</span><span class="sxs-lookup"><span data-stu-id="eb44d-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="eb44d-133">在 Visual Studio 中，開啟您建立 hello hello 方案[開始使用通知中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb44d-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="eb44d-134">在 [方案總管] 中，以滑鼠右鍵按一下 hello **(Windows 8.1)**專案，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="eb44d-135">在 hello 左側，按一下 **線上**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="eb44d-136">在 hello**搜尋**方塊中，輸入**Http 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="eb44d-137">在 hello 結果清單中，按一下  **Microsoft HTTP Client Libraries**，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="eb44d-138">完成 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="eb44d-138">Complete hello installation.</span></span>
6. <span data-ttu-id="eb44d-139">在 hello NuGet**搜尋**方塊中，輸入**Json.net**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="eb44d-140">安裝 hello **Json.NET**封裝，並再關閉 hello NuGet 套件管理員 視窗。</span><span class="sxs-lookup"><span data-stu-id="eb44d-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="eb44d-141">重複上述步驟，hello hello **(Windows Phone 8.1)**專案 tooinstall hello **JSON.NET** hello Windows Phone 專案的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="eb44d-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="eb44d-142">在 方案總管中 hello **(Windows 8.1)**專案中，按兩下**MainPage.xaml** tooopen hello Visual Studio 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="eb44d-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="eb44d-143">在 hello **MainPage.xaml** XML 程式碼，取代 hello `<Grid>` hello 下列程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="eb44d-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="eb44d-144">這個程式碼加入使用者名稱和密碼的文字方塊中的 hello 使用者進行驗證時。</span><span class="sxs-lookup"><span data-stu-id="eb44d-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="eb44d-145">它也會加入 hello 通知訊息和 hello 應該會收到 hello 通知的使用者名稱標籤的文字方塊：</span><span class="sxs-lookup"><span data-stu-id="eb44d-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="eb44d-146">在 方案總管中 hello **(Windows Phone 8.1)**專案中，開啟**MainPage.xaml**和取代 hello Windows Phone 8.1`<Grid>`與上述相同的程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="eb44d-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="eb44d-147">hello 介面應該看起來類似 toowhats 如下所示。</span><span class="sxs-lookup"><span data-stu-id="eb44d-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="eb44d-148">在 方案總管 中，開啟 hello **MainPage.xaml.cs**檔案 hello **(Windows 8.1)**和**(Windows Phone 8.1)**專案。</span><span class="sxs-lookup"><span data-stu-id="eb44d-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="eb44d-149">新增下列 hello`using`在 hello 這兩個檔案最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="eb44d-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="eb44d-150">在**MainPage.xaml.cs** hello **(Windows 8.1)**和**(Windows Phone 8.1)**專案中，加入下列成員 toohello hello`MainPage`類別。</span><span class="sxs-lookup"><span data-stu-id="eb44d-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="eb44d-151">要確定 tooreplace `<Enter Your Backend Endpoint>` hello 與實際的後端端點先前取得。</span><span class="sxs-lookup"><span data-stu-id="eb44d-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="eb44d-152">例如： `http://mybackend.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="eb44d-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="eb44d-153">新增下列 toohello MainPage 類別中的 hello 程式碼**MainPage.xaml.cs** hello **(Windows 8.1)**和**(Windows Phone 8.1)**專案。</span><span class="sxs-lookup"><span data-stu-id="eb44d-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="eb44d-154">hello`PushClick`方法為 hello click 處理常式的 hello**傳送推播** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb44d-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="eb44d-155">它會呼叫 hello 後端 tootrigger 通知 tooall 裝置與使用者名稱標籤符合 hello`to_tag`參數。</span><span class="sxs-lookup"><span data-stu-id="eb44d-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="eb44d-156">hello 通知訊息會傳送 hello 要求主體中的 JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="eb44d-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="eb44d-157">hello`LoginAndRegisterClick`方法為 hello click 處理常式的 hello**登入並註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb44d-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="eb44d-158">它會儲存 hello basic 驗證權杖中本機儲存體 （注意，這表示您的驗證配置會使用語彙基元），然後使用`RegisterClient`tooregister 使用 hello 後端的通知。</span><span class="sxs-lookup"><span data-stu-id="eb44d-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="eb44d-159">在 方案總管在 hello**共用**專案、 開啟 hello **App.xaml.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="eb44d-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="eb44d-160">尋找 hello 呼叫太`InitNotificationsAsync()`在 hello`OnLaunched()`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="eb44d-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="eb44d-161">標記為註解或刪除 hello 電話太`InitNotificationsAsync()`。</span><span class="sxs-lookup"><span data-stu-id="eb44d-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="eb44d-162">上述新增的 hello 按鈕處理常式將會初始化通知註冊。</span><span class="sxs-lookup"><span data-stu-id="eb44d-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="eb44d-163">在 [方案總管] 中，以滑鼠右鍵按一下 hello**共用**專案，然後按一下**新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="eb44d-164">Hello 類別命名**RegisterClient.cs**，然後按一下 **確定**toogenerate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="eb44d-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="eb44d-165">這個類別會包裝 hello REST 呼叫需要的 toocontact hello 應用程式後端，在訂單 tooregister 推播通知。</span><span class="sxs-lookup"><span data-stu-id="eb44d-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="eb44d-166">它也在本機儲存 hello *Registrationid*中所述的通知中樞建立 hello[從您的應用程式後端註冊](http://msdn.microsoft.com/library/dn743807.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eb44d-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="eb44d-167">請注意，它會使用儲存在本機儲存體，當您按一下 hello 授權權杖**登入並註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb44d-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="eb44d-168">新增下列 hello`using`在 hello hello RegisterClient.cs 檔案最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="eb44d-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="eb44d-169">新增下列程式碼內 hello hello`RegisterClient`類別定義。</span><span class="sxs-lookup"><span data-stu-id="eb44d-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="eb44d-170">儲存您的所有變更。</span><span class="sxs-lookup"><span data-stu-id="eb44d-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="eb44d-171">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="eb44d-171">Testing hello Application</span></span>
1. <span data-ttu-id="eb44d-172">啟動 Windows 8.1 和 Windows Phone 8.1 上的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb44d-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="eb44d-173">適用於 Windows Phone 8.1 中，您可以執行 hello 執行個體在 hello 模擬器或實際裝置。</span><span class="sxs-lookup"><span data-stu-id="eb44d-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="eb44d-174">Hello Windows 8.1 執行個體中的 hello 應用程式，輸入**Username**和**密碼**囉 」 畫面下方所示。</span><span class="sxs-lookup"><span data-stu-id="eb44d-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="eb44d-175">它應該從 hello 使用者名稱和您在 Windows Phone 輸入的密碼不同。</span><span class="sxs-lookup"><span data-stu-id="eb44d-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="eb44d-176">按一下 [登入並註冊]  ，並確認顯示您已登入的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eb44d-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="eb44d-177">這也會讓 hello**傳送推播** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eb44d-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="eb44d-178">Windows Phone 8.1 hello 執行個體上，輸入使用者名稱字串中這兩個 hello **Username**和**密碼**欄位然後按一下 **登入和註冊**。</span><span class="sxs-lookup"><span data-stu-id="eb44d-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="eb44d-179">接著在 hello**收件者的使用者名稱標記**欄位中，輸入 hello 註冊 Windows 8.1 上的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="eb44d-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="eb44d-180">輸入通知訊息，然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="eb44d-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="eb44d-181">僅限 hello 與 hello 相符的使用者名稱標記已註冊的裝置收到 hello 通知訊息。</span><span class="sxs-lookup"><span data-stu-id="eb44d-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="eb44d-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb44d-182">Next Steps</span></span>
* <span data-ttu-id="eb44d-183">如果您希望 toosegment 使用者感興趣的群組，請參閱[使用通知中樞 toosend 最新消息]。</span><span class="sxs-lookup"><span data-stu-id="eb44d-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="eb44d-184">深入了解如何 toolearn toouse 通知中心，請參閱[通知中樞指引]。</span><span class="sxs-lookup"><span data-stu-id="eb44d-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[開始使用通知中樞]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[安全推送]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
