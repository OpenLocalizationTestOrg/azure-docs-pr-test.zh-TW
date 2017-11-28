---
title: "與 Azure 通知中心 aaaSending 推播通知 tooiOS |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooan iOS 應用程式。"
services: notification-hubs
documentationcenter: ios
keywords: "推播通知,推播通知,ios 推播通知"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="b7dd5-104">使用 Azure 通知中樞傳送推播通知 tooiOS</span><span class="sxs-lookup"><span data-stu-id="b7dd5-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="b7dd5-105">概觀</span><span class="sxs-lookup"><span data-stu-id="b7dd5-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="b7dd5-106">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b7dd5-107">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b7dd5-108">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="b7dd5-109">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooan iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="b7dd5-110">您將建立空白 iOS 應用程式透過使用 hello 接收推播通知[Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html)。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="b7dd5-111">完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7dd5-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="b7dd5-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="b7dd5-113">此教學課程中的 hello 完成程式碼可以找到[GitHub 上](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted)。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b7dd5-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="b7dd5-114">Prerequisites</span></span>
<span data-ttu-id="b7dd5-115">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="b7dd5-116">[行動服務 iOS SDK 版本 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="b7dd5-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="b7dd5-117">最新版的 [Xcode]</span><span class="sxs-lookup"><span data-stu-id="b7dd5-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="b7dd5-118">支援 iOS 8 (或更新版本) 的裝置</span><span class="sxs-lookup"><span data-stu-id="b7dd5-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="b7dd5-119">[Apple Developer Program](https://developer.apple.com/programs/) 成員資格。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b7dd5-120">由於推播通知的設定需求，您必須部署並測試實體 iOS 裝置 （iPhone 或 iPad） 上的推播通知，而不是 hello iOS 模擬器。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="b7dd5-121">完成本教學課程是參加 iOS app 所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="b7dd5-122">針對 iOS 推播通知設定您的通知中樞</span><span class="sxs-lookup"><span data-stu-id="b7dd5-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="b7dd5-123">本節將引導您建立新的通知中樞及與使用 hello APNS 設定驗證**.p12**您所建立的推播憑證。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="b7dd5-124">如果您想 toouse 您已經建立通知中樞，您可以略過 toostep 5。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="b7dd5-125">按一下 hello <b>Notification Services</b>按鈕在 hello<b>設定</b>刀鋒視窗中，然後選取<b>Apple (APNS)</b>。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="b7dd5-126">按一下<b>上傳憑證</b>和選取 hello <b>.p12</b>您稍早匯出的檔案。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="b7dd5-127">請確定您也可以指定 hello 正確的密碼。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="b7dd5-128">請確定 tooselect<b>沙箱</b>模式，因為這是進行開發。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="b7dd5-129">只使用 hello<b>生產</b>如果您想 toosend 推播通知 toousers 購買您的應用程式從 hello 存放區。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="b7dd5-130">&emsp;&emsp;&emsp;&emsp;![在 Azure 入口網站中設定 APNS](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="b7dd5-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![在 Azure 入口網站中設定 APNS 憑證](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="b7dd5-132">您的通知中樞現在是設定的 toowork 使用 APNS，而且您擁有 hello 連接字串 tooregister 您的應用程式，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="b7dd5-133">連接您的 iOS 應用程式 tooNotification 集線器</span><span class="sxs-lookup"><span data-stu-id="b7dd5-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="b7dd5-134">在 Xcode 中，建立新的 iOS 專案，並選取 hello**單一檢視應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - 單一檢視應用程式][8]
    
2. <span data-ttu-id="b7dd5-136">當設定為新專案的 hello 選項，請確定 toouse hello 相同**產品名稱**和**組織識別碼**時您先前為設定 hello 套件組合識別碼 hello Apple 開發人員使用入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - 專案選項][11]
    
3. <span data-ttu-id="b7dd5-138">下**目標**，按一下您的專案名稱，按一下 hello**組建設定**索引標籤上，展開 **程式碼簽署識別**，然後在**偵錯**，設定您的程式碼簽署識別。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="b7dd5-139">切換**層級**從**基本**太**所有**，並設定**佈建設定檔**toohello 佈建您先前建立的設定檔.</span><span class="sxs-lookup"><span data-stu-id="b7dd5-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="b7dd5-140">如果您沒有看到 hello 新佈建在 Xcode 中所建立的設定檔，請嘗試重新整理您的簽署識別的 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="b7dd5-141">按一下**Xcode** hello 功能表列上，按一下 [**喜好設定**，按一下 hello**帳戶**索引標籤上，按一下 hello**檢視詳細資料**按鈕上，按一下您簽署身分識別，然後按一下hello 右下角 hello 重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - 佈建設定檔][9]
4. <span data-ttu-id="b7dd5-143">下載 hello[行動服務 iOS SDK 版本 1.2.4]並解壓縮 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="b7dd5-144">在 Xcode 中，以滑鼠右鍵按一下您的專案，按一下 hello**將檔案新增至**選項 tooadd hello **WindowsAzureMessaging.framework**資料夾 tooyour Xcode 專案。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="b7dd5-145">選取 必要時複製項目，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b7dd5-146">hello 通知中樞 SDK 目前不支援 bitcode Xcode 7 上。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="b7dd5-147">您必須設定**啟用 Bitcode**太**否**在 hello**建置選項**為您的專案。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![解壓縮 Azure SDK][10]
5. <span data-ttu-id="b7dd5-149">新標頭檔 tooyour 將專案加入名為`HubInfo.h`。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="b7dd5-150">這個檔案會保留您的通知中樞的 hello 常數。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="b7dd5-151">新增下列定義 hello 和 hello 與字串常值預留位置取代您*中樞名稱*和 hello *DefaultListenSharedAccessSignature*您先前記下。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="b7dd5-152">開啟您`AppDelegate.h`檔案新增下列 import 指示詞的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7dd5-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="b7dd5-153">在您`AppDelegate.m file`，加入下列程式碼中 hello hello`didFinishLaunchingWithOptions`方法會根據您的 iOS 版本。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="b7dd5-154">此程式碼會向 APN 註冊裝置控制代碼：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="b7dd5-155">對於 iOS 8：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="b7dd5-156">針對 iOS 版本先前 too8:</span><span class="sxs-lookup"><span data-stu-id="b7dd5-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="b7dd5-157">在 hello 同一個檔案中新增下列方法 hello。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="b7dd5-158">此程式碼會連接 toohello 通知中樞使用 hello HubInfo.h 中所指定的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="b7dd5-159">它接著會給予發生 hello 裝置權杖 toohello 通知中樞讓 hello 通知中樞可以傳送通知：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="b7dd5-160">在 hello 同一個檔案中新增下列方法 toodisplay hello **UIAlert**如果 hello 應用程式作用中時，會收到 hello 通知：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="b7dd5-161">建置並執行您不有任何失敗的裝置 tooverify 上 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="b7dd5-162">傳送測試推播通知</span><span class="sxs-lookup"><span data-stu-id="b7dd5-162">Send test push notifications</span></span>
<span data-ttu-id="b7dd5-163">您可以測試應用程式中接收通知，傳送推播通知給 hello 以[Azure 入口網站]透過 hello**疑難排解**hello 中樞刀鋒視窗中的區段 (使用 hello*測試傳送*選項)。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Azure 入口網站 - 測試傳送][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="b7dd5-165">（選擇性）從 hello 應用程式中傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="b7dd5-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b7dd5-166">基於學習的目的只提供這個範例的 hello 用戶端應用程式從傳送通知。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="b7dd5-167">因為這將需要 hello `DefaultFullSharedAccessSignature` toobe 在於 hello 用戶端應用程式，它會公開使用者會獲得存取未經授權的 toosend 通知 tooyour 用戶端通知中樞 toohello 風險。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="b7dd5-168">如果您想 toosend 推播通知從應用程式中的，本節提供如何的範例 toodo 此使用 hello REST 介面。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="b7dd5-169">在 Xcode 中，開啟`Main.storyboard`和新增 hello hello 物件程式庫 tooallow hello 使用者 toosend 推播通知 hello 應用程式中的下列 UI 元件：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="b7dd5-170">沒有標籤文字的標籤。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-170">A label with no label text.</span></span> <span data-ttu-id="b7dd5-171">它將會使用的 tooreport 傳送通知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="b7dd5-172">hello**行**屬性應該設定太**0** ，讓它將會自動調整的大小限制的 toohello 右邊和左邊的界和 hello hello 檢視的頂端。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="b7dd5-173">文字欄位與**預留位置**太設定文字**輸入通知訊息**。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="b7dd5-174">限制 hello hello 標籤，如下所示的正下方的欄位。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="b7dd5-175">將 hello 檢視控制站設定為 hello 插座委派。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="b7dd5-176">標題按鈕**傳送通知**限制 hello 文字欄位的正下方且在 hello 水平置中。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="b7dd5-177">hello 檢視應如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-177">hello view should look as follows:</span></span>
     
     ![Xcode 設計工具][32]
2. <span data-ttu-id="b7dd5-179">[新增插座](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html)hello 標籤和文字欄位已連接您的檢視，並更新您`interface`定義 toosupport`UITextFieldDelegate`和`NSXMLParserDelegate`。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="b7dd5-180">新增 hello toohelp 支援呼叫 REST API hello 和剖析 hello 回應如下所示三個屬性宣告。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="b7dd5-181">您的 ViewController.h 檔案應該類似下列內容：</span><span class="sxs-lookup"><span data-stu-id="b7dd5-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="b7dd5-182">開啟`HubInfo.h`並新增下列常數用於傳送通知 tooyour 中樞 hello。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="b7dd5-183">以您實際取代預留位置字串常值 hello *DefaultFullSharedAccessSignature*連接字串。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="b7dd5-184">新增下列 hello`#import`陳述式 tooyour`ViewController.h`檔案。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="b7dd5-185">在`ViewController.m`新增下列程式碼 toohello 介面實作的 hello。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="b7dd5-186">此程式碼將會剖析您的 *DefaultFullSharedAccessSignature* 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="b7dd5-187">Hello 中所述[REST API 參考](http://msdn.microsoft.com/library/azure/dn495627.aspx)，這個已剖析的資訊將會使用的 toogenerate hello 的 SaS token**授權**要求標頭。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="b7dd5-188">在`ViewController.m`，更新 hello`viewDidLoad`方法 tooparse hello 連接字串 hello 檢視載入時。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="b7dd5-189">也新增 hello 公用程式方法，如下所示 toohello 介面實作。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="b7dd5-190">在`ViewController.m`，加入下列程式碼 toohello 介面實作 toogenerate hello SaS 授權權杖，而將提供在 hello hello**授權**標頭，hello 中所述[REST API參考](http://msdn.microsoft.com/library/azure/dn495627.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="b7dd5-191">Ctrl + 拖曳從 hello**傳送通知**太按鈕`ViewController.m`tooadd 名為動作**SendNotificationMessage** hello**觸控向**事件。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="b7dd5-192">下列程式碼 toosend hello 通知使用 hello REST API 的 hello 與更新方法。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="b7dd5-193">在`ViewController.m`，加入下列委派方法 toosupport 關閉 hello 文字欄位的 hello 鍵盤 hello。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="b7dd5-194">Ctrl + 拖曳從 hello 文字欄位 toohello 檢視控制器中圖示 hello 介面設計工具 tooset hello 檢視控制站與 hello 插座委派。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="b7dd5-195">在`ViewController.m`，加入下列 hello 使用委派方法 toosupport 剖析 hello 回應`NSXMLParser`。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="b7dd5-196">建置 hello 專案並確認沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="b7dd5-197">如果您遇到有關 bitcode 支援 Xcode7 中的建置錯誤，您應該變更 hello**組建設定** > **啟用 Bitcode (ENABLE_BITCODE)**太**否**在 Xcode 中。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="b7dd5-198">hello 通知中樞 SDK 目前不支援 bitcode。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="b7dd5-199">您可以在 hello Apple 找到所有 hello 可能通知裝載[本機和推播通知程式設計指南]。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="b7dd5-200">檢查您的應用程式是否可接收推播通知</span><span class="sxs-lookup"><span data-stu-id="b7dd5-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="b7dd5-201">在 iOS 上的 tootest 推播通知，您必須部署 hello 應用程式 tooa 實體 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="b7dd5-202">您無法使用 hello iOS 模擬器來傳送 Apple 推播通知。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="b7dd5-203">執行 hello 應用程式，並確認登錄成功，然後按下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![iOS 應用程式推播通知註冊測試][33]
2. <span data-ttu-id="b7dd5-205">您可以傳送測試推播通知從 hello [Azure 入口網站]，如上面所述。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="b7dd5-206">如果您加入程式碼，以便在 hello 應用程式中傳送推播通知，觸控內 hello 文字欄位 tooenter 通知訊息。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="b7dd5-207">然後按 hello**傳送**hello 鍵盤或 hello 按鈕**傳送通知**hello 檢視 toosend hello 通知訊息中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![iOS 應用程式推播通知傳送測試][34]
3. <span data-ttu-id="b7dd5-209">hello 推播通知傳送 tooall 的裝置已註冊的 tooreceive hello 通知 hello 特定通知中樞。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![iOS 應用程式推播通知接收測試][35]

## <a name="next-steps"></a><span data-ttu-id="b7dd5-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7dd5-211">Next steps</span></span>
<span data-ttu-id="b7dd5-212">在這個簡單的範例中，您傳播推播通知 tooall 已註冊的 iOS 裝置。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="b7dd5-213">我們建議您繼續 toohello 您了解下一個步驟[Azure 通知中樞通知使用者與.NET 後端 ios]教學課程，將引導您完成建立後端 toosend 推播通知使用標記。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="b7dd5-214">如果您想 toosegment 您感興趣群組的使用者，您可以另外將移 toohello[使用通知中樞 toosend 最新消息]教學課程。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="b7dd5-215">如需有關通知中樞的一般資訊，請參閱 [通知中樞指引]。</span><span class="sxs-lookup"><span data-stu-id="b7dd5-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[行動服務 iOS SDK 版本 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure 通知中樞通知使用者與.NET 後端 ios]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[本機和推播通知程式設計指南]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure 入口網站]: https://portal.azure.com
