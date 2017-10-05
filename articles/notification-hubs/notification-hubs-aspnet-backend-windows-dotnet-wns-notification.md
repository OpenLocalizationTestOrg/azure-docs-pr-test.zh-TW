---
title: "Azure 通知中樞透過 .NET 後端通知使用者"
description: "了解如何在 Azure 中傳送安全的推播通知。 程式碼範例是以 C# 撰寫並使用 .NET API。"
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
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="ef3e2-104">Azure 通知中樞透過 .NET 後端通知使用者</span><span class="sxs-lookup"><span data-stu-id="ef3e2-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="ef3e2-105">Overview</span><span class="sxs-lookup"><span data-stu-id="ef3e2-105">Overview</span></span>
<span data-ttu-id="ef3e2-106">Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播基礎結構，而大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="ef3e2-107">本教學課程將示範如何使用 Azure 通知中心，來將推播通知傳送到特定裝置上的特定應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="ef3e2-108">ASP.NET WebAPI 後端是用來驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="ef3e2-109">使用驗證的用戶端使用者，後端就會自動將標記新增通知註冊。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="ef3e2-110">後端會傳送此標記，以產生特定使用者的通知。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="ef3e2-111">如需使用應用程式後端註冊通知的詳細資訊，請參閱指引主題 [從應用程式後端註冊](http://msdn.microsoft.com/library/dn743807.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="ef3e2-112">本教學課程會以您在 [開始使用通知中樞] 教學課程中所建立的通知中樞和專案為基礎。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="ef3e2-113">本教學課程還是 [安全推播] 教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="ef3e2-114">完成本教學課程中的步驟後，您可以繼續進行 [安全推播] 教學課程，該教學課程說明如何修改本教學課程中的程式碼，以安全的方式傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef3e2-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="ef3e2-115">Before you begin</span></span>
<span data-ttu-id="ef3e2-116">我們非常重視您的意見反應。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-116">We do take your feedback seriously.</span></span> <span data-ttu-id="ef3e2-117">如果您對於完成此主題有任何困難，或者有改進此內容的建議，非常歡迎您在本頁底部提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="ef3e2-118">您可以在 [此處](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)的 GitHub 上找到本教學課程的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ef3e2-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="ef3e2-119">Prerequisites</span></span>
<span data-ttu-id="ef3e2-120">在開始本教學課程之前，您必須已完成下列行動服務教學課程：</span><span class="sxs-lookup"><span data-stu-id="ef3e2-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="ef3e2-121">[開始使用通知中樞]</span><span class="sxs-lookup"><span data-stu-id="ef3e2-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="ef3e2-122">您要建立通知中樞，然後保留應用程式名稱並註冊以接收本教學課程中的通知。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="ef3e2-123">本教學課程假設您已完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="ef3e2-124">否則，請依照[開始使用通知中樞 (Windows 市集)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 中的步驟進行；尤其是[向 Windows 市集註冊您的應用程式](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store)一節和[向 Windows 市集註冊您的應用程式](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)一節。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="ef3e2-125">尤其請確定您已在入口網站的通知中心內，輸入 [設定] 索引標籤中的 [套件 SID] 和 [用戶端祕密] 值。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="ef3e2-126">此組態程序會在 [設定您的通知中心](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)一節中加以說明。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="ef3e2-127">這是重要步驟：如果入口網站上的認證與您為所選應用程式名稱指定的認證不符，則推播通知將無法順利進行。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="ef3e2-128">如果您使用 Azure App Service 中的 Mobile Apps 作為後端服務，請參閱本教學課程的 [Mobile Apps 版本](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) 。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="ef3e2-129">更新用戶端專案的程式碼</span><span class="sxs-lookup"><span data-stu-id="ef3e2-129">Update the code for the client project</span></span>
<span data-ttu-id="ef3e2-130">在本節中，您會更新已針對 [開始使用通知中樞] 教學課程完成之專案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="ef3e2-131">這應該已經與市集相關聯，並已針對您的通知中樞進行設定。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="ef3e2-132">在本節中，您將加入程式碼以呼叫新的 WebAPI 後端，並使用它來註冊和傳送通知。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="ef3e2-133">在 Visual Studio 中，開啟您為 [開始使用通知中樞] 教學課程所建立的方案。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="ef3e2-134">在 [方案總管] 中，以滑鼠右鍵按一下 [(Windows 8.1)] 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="ef3e2-135">在左側，按一下 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="ef3e2-136">在 [搜尋] 方塊中，輸入 **Http Client**。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="ef3e2-137">按一下結果清單中的 **Microsoft HTTP Client Libraries**，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="ef3e2-138">完成安裝。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-138">Complete the installation.</span></span>
6. <span data-ttu-id="ef3e2-139">回到 NuGet [搜尋] 方塊，輸入 **Json.net**。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="ef3e2-140">安裝 **Json.NET** 套件，然後關閉 [NuGet Package Manager] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="ef3e2-141">針對 [(Windows 8.1)] 專案重複上述步驟，來安裝 Windows Phone 專案的 **JSON.NET** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="ef3e2-142">在 [方案總管] 的 [(Windows 8.1)] 專案中，連按兩下 **MainPage.xaml**，在 Visual Studio 編輯器中開啟該檔案。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="ef3e2-143">在 **MainPage.xaml** XML 程式碼中，使用下列程式碼取代 `<Grid>` 區段。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="ef3e2-144">這個程式碼加入使用者用來進行驗證的使用者名稱和密碼文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="ef3e2-145">它也會加入通知訊息的文字方塊，以及應接收通知的使用者名稱標記：</span><span class="sxs-lookup"><span data-stu-id="ef3e2-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
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
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="ef3e2-146">在 [方案總管] 的 [(Windows Phone 8.1)] 專案中，開啟 **MainPage.xaml**，並將 Windows Phone 8.1 `<Grid>` 區段取代為上述該相同程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="ef3e2-147">介面看起來應該會如下所示。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="ef3e2-148">在 [方案總管] 中，開啟 [(Windows 8.1)] 和 [(Windows Phone 8.1)] 專案的 **MainPage.xaml.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="ef3e2-149">在這兩個檔案頂端加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ef3e2-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="ef3e2-150">在 [(Windows 8.1)] 和 [(Windows Phone 8.1)] 專案的 **MainPage.xaml.cs** 中，將下列成員新增至 `MainPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="ef3e2-151">請務必使用先前取得的實際後端端點來取代 `<Enter Your Backend Endpoint>`：</span><span class="sxs-lookup"><span data-stu-id="ef3e2-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="ef3e2-152">例如，`http://mybackend.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="ef3e2-153">將下面的程式碼新增到 [(Windows 8.1)] 和 [(Windows Phone 8.1)] 專案之 **MainPage.xaml.cs** 中的 MainPage 類別。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="ef3e2-154">`PushClick` 方法是 [傳送推播] 按鈕的 click 處理常式。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="ef3e2-155">它會呼叫後端以觸發所有裝置的通知，而所有裝置都具有符合 `to_tag` 參數的使用者名稱標記。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="ef3e2-156">通知訊息會以要求主體的 JSON 內容形式傳送。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="ef3e2-157">`LoginAndRegisterClick` 方法是 [登入並註冊] 按鈕的 click 處理常式。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="ef3e2-158">它會在本機儲存體中儲存基本驗證權杖 (請注意，這代表驗證結構描述使用的任何權杖)，然後使用 `RegisterClient` 以使用後端來註冊通知。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

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
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
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



1. <span data-ttu-id="ef3e2-159">在 [方案總管] 的 [共用] 專案下，開啟 **App.xaml.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="ef3e2-160">在 `InitNotificationsAsync()` in the `OnLaunched()` 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="ef3e2-161">取消註解或刪除對 `InitNotificationsAsync()`的呼叫。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="ef3e2-162">上面加入的按鈕處理常式會初始化通知註冊。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="ef3e2-163">在 [方案總管] 中，以滑鼠右鍵按一下 [共用] 專案，然後按一下 [新增]，再按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="ef3e2-164">將類別命名為 **RegisterClient.cs**，然後按一下 [確定] 以產生類別。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="ef3e2-165">為了註冊推播通知，此類別會包裝連絡應用程式後端所需的 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="ef3e2-166">它也會在本機儲存通知中心所建立的 *registrationIds* ，如 [從您的應用程式後端註冊](http://msdn.microsoft.com/library/dn743807.aspx)中的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="ef3e2-167">請注意，當您按一下 [Log in and register]  按鈕時，系統便會使用儲存在本機儲存體中的授權權杖。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="ef3e2-168">在 RegisterClient.cs 檔案開頭加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ef3e2-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="ef3e2-169">在 `RegisterClient` 類別定義中加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="ef3e2-170">儲存您的所有變更。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="ef3e2-171">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="ef3e2-171">Testing the Application</span></span>
1. <span data-ttu-id="ef3e2-172">在 Windows 8.1 和 Windows Phone 8.1 上啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="ef3e2-173">對於 Windows Phone 8.1，您可以在模擬器或實際裝置中執行執行個體。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="ef3e2-174">在應用程式的 Windows 8.1 執行個體中，輸入 [使用者名稱]和 [密碼] \(如下列畫面所示)。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="ef3e2-175">它應該與您在 Windows Phone 上輸入的使用者名稱和密碼不同。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="ef3e2-176">按一下 [登入並註冊]  ，並確認顯示您已登入的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="ef3e2-177">這也會啟用 [傳送推播]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="ef3e2-178">在 Windows Phone 8.1 執行個體上，於 [使用者名稱] 和 [密碼] 欄位中輸入使用者名稱字串，然後按一下 [登入和註冊]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="ef3e2-179">然後，在 [收件者使用者名稱標記]  欄位中，輸入在 Windows 8.1 上註冊的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="ef3e2-180">輸入通知訊息，然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="ef3e2-181">只有已經使用相符使用者名稱標記所註冊的裝置才會收到通知訊息。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="ef3e2-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef3e2-182">Next Steps</span></span>
* <span data-ttu-id="ef3e2-183">如果您想要按興趣群組分隔使用者，請參閱 [使用通知中樞傳送即時新聞]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="ef3e2-184">若要深入了解如何使用通知中心，請參閱 [通知中心指引]。</span><span class="sxs-lookup"><span data-stu-id="ef3e2-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="ef3e2-185">[開始使用通知中樞]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="ef3e2-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="ef3e2-186">[安全推播]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="ef3e2-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="ef3e2-187">[使用通知中樞傳送即時新聞]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="ef3e2-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="ef3e2-188">[通知中心指引]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="ef3e2-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
