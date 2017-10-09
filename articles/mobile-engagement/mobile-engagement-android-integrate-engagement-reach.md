---
title: "aaaAzure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="f0748-103">如何在 Android 上的 tooIntegrate Engagement 連接</span><span class="sxs-lookup"><span data-stu-id="f0748-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f0748-104">您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。</span><span class="sxs-lookup"><span data-stu-id="f0748-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="f0748-105">標準整合</span><span class="sxs-lookup"><span data-stu-id="f0748-105">Standard integration</span></span>

<span data-ttu-id="f0748-106">複製觸達資源檔從您的專案中的 hello SDK:</span><span class="sxs-lookup"><span data-stu-id="f0748-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="f0748-107">Hello 檔案複製 hello`res/layout`資料夾傳遞以 hello SDK 到 hello`res/layout`應用程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0748-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="f0748-108">Hello 檔案複製 hello`res/drawable`資料夾傳遞以 hello SDK 到 hello`res/drawable`應用程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0748-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="f0748-109">編輯 `AndroidManifest.xml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="f0748-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="f0748-110">新增下列區段的 hello (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="f0748-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* <span data-ttu-id="f0748-111">您必須開機所未按下此權限 tooreplay 系統通知 （否則它們將會保留在磁碟上，但不會再顯示，您只需要 tooinclude 這）。</span><span class="sxs-lookup"><span data-stu-id="f0748-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="f0748-112">指定用於複製和編輯 hello 下列區段 （在應用程式及系統的兩者） 的通知圖示 (之間 hello`<application>`和`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="f0748-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="f0748-113">如果您打算在建立 Reach 活動時使用系統通知，則「務必」使用此區段。</span><span class="sxs-lookup"><span data-stu-id="f0748-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="f0748-114">Android 禁止顯示沒有圖示的系統通知。</span><span class="sxs-lookup"><span data-stu-id="f0748-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="f0748-115">因此，如果您省略這個區段，您的使用者將都能 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="f0748-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="f0748-116">如果您建立使用大圖片的系統通知的活動時，您需要下列權限的 tooadd hello (hello 之後`</application>`標記) 如果遺失：</span><span class="sxs-lookup"><span data-stu-id="f0748-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="f0748-117">在 Android M 上，若您的應用程式目標為 Android API 層級 23 或更高層級， ``WRITE_EXTERNAL_STORAGE`` 權限需要使用者核准。</span><span class="sxs-lookup"><span data-stu-id="f0748-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="f0748-118">請閱讀 [本節](mobile-engagement-android-integrate-engagement.md#android-m-permissions)。</span><span class="sxs-lookup"><span data-stu-id="f0748-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="f0748-119">您也可以指定在 hello 系統通知到達活動 hello 裝置應該環和/或震動。</span><span class="sxs-lookup"><span data-stu-id="f0748-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="f0748-120">它 toowork，您必須確定宣告下列權限的 hello toomake (hello 之後`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="f0748-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="f0748-121">沒有這個權限，Android 可防止系統通知，使其不要顯示當您核取 hello 信號或 hello 震動 hello 到達活動管理員中的選項。</span><span class="sxs-lookup"><span data-stu-id="f0748-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="f0748-122">原生推送</span><span class="sxs-lookup"><span data-stu-id="f0748-122">Native Push</span></span>
<span data-ttu-id="f0748-123">現在您已設定觸達模組，您需要 tooconfigure 原生推送 toobe 無法 tooreceive hello 活動 hello 裝置上。</span><span class="sxs-lookup"><span data-stu-id="f0748-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="f0748-124">我們在 Android 上支援兩種服務：</span><span class="sxs-lookup"><span data-stu-id="f0748-124">We support two services on Android:</span></span>

* <span data-ttu-id="f0748-125">Google Play 的裝置： 使用[Google Cloud Messaging]由下列 hello [tooIntegrate 與 Engagement GCM 如何引導](mobile-engagement-android-gcm-integrate.md)指南。</span><span class="sxs-lookup"><span data-stu-id="f0748-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="f0748-126">Amazon 裝置： 使用[Amazon 裝置傳訊]由下列 hello [tooIntegrate 與 Engagement ADM 如何引導](mobile-engagement-android-adm-integrate.md)指南。</span><span class="sxs-lookup"><span data-stu-id="f0748-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="f0748-127">如果您想 tootarget Amazon 和 Google Play 的裝置，其可能 toohave 開發 1 AndroidManifest.xml/APK 內的所有項目。</span><span class="sxs-lookup"><span data-stu-id="f0748-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="f0748-128">但是，如果他們找到 GCM 程式碼時送出 tooAmazon，它們可能會拒絕您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0748-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="f0748-129">您應該在此情況下使用多個 APK。</span><span class="sxs-lookup"><span data-stu-id="f0748-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="f0748-130">**現在準備 tooreceive 和顯示達到行銷活動，就會是您的應用程式 ！**</span><span class="sxs-lookup"><span data-stu-id="f0748-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="f0748-131">Toohandle 資料的推播</span><span class="sxs-lookup"><span data-stu-id="f0748-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="f0748-132">整合</span><span class="sxs-lookup"><span data-stu-id="f0748-132">Integration</span></span>
<span data-ttu-id="f0748-133">如果您想要應用程式 toobe 無法 tooreceive 觸達資料推播通知、 的子類別有 toocreate `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` hello 中參考它`AndroidManifest.xml`檔案 (之間 hello`<application>`及/或`</application>`標記):</span><span class="sxs-lookup"><span data-stu-id="f0748-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="f0748-134">然後您可以覆寫 hello`onDataPushStringReceived`和`onDataPushBase64Received`回呼。</span><span class="sxs-lookup"><span data-stu-id="f0748-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="f0748-135">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="f0748-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="f0748-136">類別</span><span class="sxs-lookup"><span data-stu-id="f0748-136">Category</span></span>
<span data-ttu-id="f0748-137">hello 分類參數是選擇性的當您建立將資料推送活動時，可讓您 toofilter 資料推播通知。</span><span class="sxs-lookup"><span data-stu-id="f0748-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="f0748-138">這是適用於有數個廣播的接收者處理不同類型的資料推播通知，或如果您想 toopush 不同種類的`Base64`資料而且想 tooidentify 其類型，再剖析它們。</span><span class="sxs-lookup"><span data-stu-id="f0748-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="f0748-139">回呼的傳回參數</span><span class="sxs-lookup"><span data-stu-id="f0748-139">Callbacks' return parameter</span></span>
<span data-ttu-id="f0748-140">以下是一些指導方針 tooproperly 處理 hello 傳回參數的`onDataPushStringReceived`和`onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="f0748-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="f0748-141">廣播的接收者應該傳回`null`如果不知道如何 toohandle 資料推送的 hello 回呼中。</span><span class="sxs-lookup"><span data-stu-id="f0748-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="f0748-142">您應該使用 hello 類別 toodetermine 是否您廣播的接收者應該要或不處理 hello 資料推送。</span><span class="sxs-lookup"><span data-stu-id="f0748-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="f0748-143">其中一個 hello 廣播接收者應該傳回`true`如果它接受 hello 資料推送的 hello 回呼中。</span><span class="sxs-lookup"><span data-stu-id="f0748-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="f0748-144">其中一個 hello 廣播接收者應該傳回`false`hello 回呼會辨識 hello 資料推入，但因故捨棄它。</span><span class="sxs-lookup"><span data-stu-id="f0748-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="f0748-145">例如，傳回`false`hello 收到資料時無效。</span><span class="sxs-lookup"><span data-stu-id="f0748-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="f0748-146">如果其中一個廣播接收者傳回`true`而另一個會傳回`false`hello 相同資料推入，hello 行為是未定義，您應該永遠不會這麼做。</span><span class="sxs-lookup"><span data-stu-id="f0748-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="f0748-147">hello 傳回型別只適用於 hello 觸達統計資料：</span><span class="sxs-lookup"><span data-stu-id="f0748-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="f0748-148">`Replied`如果是傳回 hello 廣播接收者其中之一，就會遞增`true`或`false`。</span><span class="sxs-lookup"><span data-stu-id="f0748-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="f0748-149">`Actioned`其中一個 hello 廣播接收者傳回時，才會遞增`true`。</span><span class="sxs-lookup"><span data-stu-id="f0748-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="f0748-150">如何 toocustomize 活動</span><span class="sxs-lookup"><span data-stu-id="f0748-150">How toocustomize campaigns</span></span>
<span data-ttu-id="f0748-151">toocustomize 活動時，您可以修改 hello hello Reach SDK 中提供的配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="f0748-152">您應該在 hello 版面配置中所使用的所有 hello 識別碼保留，以及使用識別項，特別是針對檢視文字和影像檢視的 hello 檢視 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="f0748-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="f0748-153">部分檢視只使用的 toohide 或顯示區域，所以可能會變更其類型。</span><span class="sxs-lookup"><span data-stu-id="f0748-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="f0748-154">請如果您想檢視的 toochange hello 類型提供的 hello 版面配置中，檢查 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="f0748-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="f0748-155">通知</span><span class="sxs-lookup"><span data-stu-id="f0748-155">Notifications</span></span>
<span data-ttu-id="f0748-156">有兩種類型的通知：系統和應用程式內通知，它們使用不同的配置檔。</span><span class="sxs-lookup"><span data-stu-id="f0748-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="f0748-157">系統通知</span><span class="sxs-lookup"><span data-stu-id="f0748-157">System notifications</span></span>
<span data-ttu-id="f0748-158">您需要 toouse hello toocustomize 系統通知**類別**。</span><span class="sxs-lookup"><span data-stu-id="f0748-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="f0748-159">您可以再跳過[類別](#categories)。</span><span class="sxs-lookup"><span data-stu-id="f0748-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="f0748-160">應用程式內通知</span><span class="sxs-lookup"><span data-stu-id="f0748-160">In-app notifications</span></span>
<span data-ttu-id="f0748-161">根據預設，應用程式內通知是以動態方式加入的 toohello 目前活動的使用者介面感謝您 toohello Android 方法的檢視`addContentView()`。</span><span class="sxs-lookup"><span data-stu-id="f0748-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="f0748-162">這稱為通知重疊。</span><span class="sxs-lookup"><span data-stu-id="f0748-162">This is called a notification overlay.</span></span> <span data-ttu-id="f0748-163">通知的影像覆疊非常適合在快速地整合在一起，因為它們不需要您 toomodify 應用程式中的任何配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="f0748-164">toomodify hello 查詢通知重疊的您可以只修改 hello 檔案`engagement_notification_area.xml`tooyour 需要。</span><span class="sxs-lookup"><span data-stu-id="f0748-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="f0748-165">hello 檔案`engagement_notification_overlay.xml`是 hello 是使用的 toocreate 通知重疊，它包含 hello 檔案`engagement_notification_area.xml`。</span><span class="sxs-lookup"><span data-stu-id="f0748-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="f0748-166">您也可以自訂它 toosuit 您的需求 （例如定位 hello 通知區域內 hello 重疊）。</span><span class="sxs-lookup"><span data-stu-id="f0748-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="f0748-167">包含通知配置做為活動配置的一部分</span><span class="sxs-lookup"><span data-stu-id="f0748-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="f0748-168">覆疊非常適合快速整合，但可能在特殊情況下造成不便或有副作用。</span><span class="sxs-lookup"><span data-stu-id="f0748-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="f0748-169">您可以自訂 hello 重疊系統在活動層級，讓您輕鬆 tooprevent 副作用的特殊活動。</span><span class="sxs-lookup"><span data-stu-id="f0748-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="f0748-170">您可以決定 tooinclude 通知配置在您現有的版面配置感謝您 toohello Android**包含**陳述式。</span><span class="sxs-lookup"><span data-stu-id="f0748-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="f0748-171">hello 的範例如下的已修改`ListActivity`配置只包含`ListView`。</span><span class="sxs-lookup"><span data-stu-id="f0748-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="f0748-172">**Engagement 整合之前：**</span><span class="sxs-lookup"><span data-stu-id="f0748-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="f0748-173">**Engagement 整合之後：**</span><span class="sxs-lookup"><span data-stu-id="f0748-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="f0748-174">在此範例中我們會加入父容器，因為 hello 原始配置的清單檢視做為 hello 上層項目。</span><span class="sxs-lookup"><span data-stu-id="f0748-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="f0748-175">我們也加入`android:layout_weight="1"`toobe 無法 tooadd 下方的清單檢視的檢視設定`android:layout_height="fill_parent"`。</span><span class="sxs-lookup"><span data-stu-id="f0748-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="f0748-176">hello Engagement 觸達 SDK 會自動偵測 hello 通知版面配置包含在此活動，且不會加入這項活動的重疊。</span><span class="sxs-lookup"><span data-stu-id="f0748-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="f0748-177">如果您在應用程式中使用 ListActivity，可見的觸達覆疊會防止您對回應 hello 清單檢視中的 tooclicked 項目不再。</span><span class="sxs-lookup"><span data-stu-id="f0748-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="f0748-178">這是已知的問題。</span><span class="sxs-lookup"><span data-stu-id="f0748-178">This is a known issue.</span></span> <span data-ttu-id="f0748-179">toowork 解決這個問題我們建議您在自己清單活動的配置，例如 hello 前一個範例中的 tooembed hello 通知版面配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="f0748-180">停用關於活動的應用程式通知</span><span class="sxs-lookup"><span data-stu-id="f0748-180">Disabling application notification per activity</span></span>
<span data-ttu-id="f0748-181">如果您不想 hello 重疊 toobe 加入 tooyour 活動，而且如果您不想加入 hello 通知配置自己版面配置中，您可以停用這項活動在 hello hello 重疊`AndroidManifest.xml`加`meta-data`區段如同在 hello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="f0748-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="f0748-182"><a name="categories"></a> 類別</span><span class="sxs-lookup"><span data-stu-id="f0748-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="f0748-183">當您修改提供的版面配置的 hello 時，您會修改您的通知 hello 外觀。</span><span class="sxs-lookup"><span data-stu-id="f0748-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="f0748-184">類別可讓您 toodefine 各種目標會尋找通知 （可能是行為）。</span><span class="sxs-lookup"><span data-stu-id="f0748-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="f0748-185">當您建立觸達活動時可以指定類別。</span><span class="sxs-lookup"><span data-stu-id="f0748-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="f0748-186">請記住，類別也可讓您自訂宣告與輪詢，本文件稍後將會說明。</span><span class="sxs-lookup"><span data-stu-id="f0748-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="f0748-187">tooregister 您的通知的類別處理常式，您需要 tooadd 呼叫，hello 應用程式初始化時。</span><span class="sxs-lookup"><span data-stu-id="f0748-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0748-188">請閱讀警告 hello android： 處理序屬性的 hello \<android sdk-engagement 處理\>hello 中如何 tooIntegrate Engagement Android 主題後再繼續。</span><span class="sxs-lookup"><span data-stu-id="f0748-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="f0748-189">hello 下列範例假設您認可 hello 先前的警告，且使用的子類別`EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="f0748-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="f0748-190">hello`MyNotifier`物件是 hello hello 通知類別處理常式實作。</span><span class="sxs-lookup"><span data-stu-id="f0748-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="f0748-191">其中一個是實作的 hello`EngagementNotifier`介面或子類別的 hello 預設實作： `EngagementDefaultNotifier`。</span><span class="sxs-lookup"><span data-stu-id="f0748-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="f0748-192">請注意，hello 相同通知程式可以處理數種類別，就能註冊它們像這樣：</span><span class="sxs-lookup"><span data-stu-id="f0748-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="f0748-193">tooreplace hello 預設類別實作中，您可以在下列範例中的 hello 註冊您的實作，例如：</span><span class="sxs-lookup"><span data-stu-id="f0748-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="f0748-194">使用處理常式中的 hello 目前類別會傳遞做為參數，您可以覆寫中的大部分方法中`EngagementDefaultNotifier`。</span><span class="sxs-lookup"><span data-stu-id="f0748-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="f0748-195">這能以 `String` 參數的形式傳遞，或是間接在 `EngagementReachContent` 物件中傳遞 (使用 `getCategory()` 方法)。</span><span class="sxs-lookup"><span data-stu-id="f0748-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="f0748-196">您可以重新定義上的方法來變更大部分的 hello 通知建立程序`EngagementDefaultNotifier`，針對更進階的自訂覺得可用 tootake 在 hello 技術文件，而 hello 原始程式碼在一起來看看。</span><span class="sxs-lookup"><span data-stu-id="f0748-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="f0748-197">應用程式內通知</span><span class="sxs-lookup"><span data-stu-id="f0748-197">In-app notifications</span></span>
<span data-ttu-id="f0748-198">如果您只想 toouse 替代配置特定分類，您可以實作此如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f0748-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="f0748-199">**`my_notification_overlay.xml` 的範例：**</span><span class="sxs-lookup"><span data-stu-id="f0748-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="f0748-200">如您所見，hello 重疊檢視識別項是比 hello 標準一個不同的。</span><span class="sxs-lookup"><span data-stu-id="f0748-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="f0748-201">很重要的是，每個配置要針對覆疊使用唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0748-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="f0748-202">**`my_notification_area.xml` 的範例：**</span><span class="sxs-lookup"><span data-stu-id="f0748-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="f0748-203">如您所見，hello 通知區域中檢視識別項是比 hello 標準一個不同的。</span><span class="sxs-lookup"><span data-stu-id="f0748-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="f0748-204">很重要的是，每個配置要針對通知區域使用唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0748-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="f0748-205">類別目錄的這個簡單的範例可讓應用程式 （或在應用程式） 顯示在 hello 囉 」 畫面最上方的通知。</span><span class="sxs-lookup"><span data-stu-id="f0748-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="f0748-206">我們不會變更 hello 本身 hello 通知區域中所使用的標準識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0748-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="f0748-207">如果您想要您有 tooredefine hello toochange`EngagementDefaultNotifier.prepareInAppArea`方法。</span><span class="sxs-lookup"><span data-stu-id="f0748-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="f0748-208">建議在 hello 技術文件和 hello 原始程式碼 toolook`EngagementNotifier`和`EngagementDefaultNotifier`如果您要的進階自訂層級。</span><span class="sxs-lookup"><span data-stu-id="f0748-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="f0748-209">系統通知</span><span class="sxs-lookup"><span data-stu-id="f0748-209">System notifications</span></span>
<span data-ttu-id="f0748-210">藉由擴充`EngagementDefaultNotifier`，您可以覆寫`onNotificationPrepared`tooalter hello 通知已準備好 hello 預設實作。</span><span class="sxs-lookup"><span data-stu-id="f0748-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="f0748-211">例如：</span><span class="sxs-lookup"><span data-stu-id="f0748-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="f0748-212">這個範例會顯示為 進行中的事件時 hello 「 進行中 」 類別使用內容的系統通知。</span><span class="sxs-lookup"><span data-stu-id="f0748-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="f0748-213">如果您想 toobuild hello`Notification`物件從頭情況下，您可以傳回`false`toohello 方法，並呼叫`notify`自行在 hello `NotificationManager`。</span><span class="sxs-lookup"><span data-stu-id="f0748-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="f0748-214">在此情況下很重要，保留`contentIntent`、 `deleteIntent` hello 所使用的通知識別碼和`EngagementReachReceiver`。</span><span class="sxs-lookup"><span data-stu-id="f0748-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="f0748-215">以下是這類實作的正確範例：</span><span class="sxs-lookup"><span data-stu-id="f0748-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="f0748-216">僅通知的公告</span><span class="sxs-lookup"><span data-stu-id="f0748-216">Notification only announcements</span></span>
<span data-ttu-id="f0748-217">hello 管理 hello 按一下通知，可以藉由覆寫自訂唯一公告`EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared`toomodify hello 備妥`Intent`。</span><span class="sxs-lookup"><span data-stu-id="f0748-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="f0748-218">使用此方法可讓您 tootune hello 旗標輕鬆。</span><span class="sxs-lookup"><span data-stu-id="f0748-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="f0748-219">例如 tooadd hello`SINGLE_TOP`旗標：</span><span class="sxs-lookup"><span data-stu-id="f0748-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="f0748-220">針對舊版 Engagement 使用者，請注意，而不進行動作的系統通知 URL 現在會啟動 hello 應用程式是否它是在背景中，因此可以與通知動作 URL 沒有呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="f0748-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="f0748-221">自訂 hello 意圖時，您應該考慮的。</span><span class="sxs-lookup"><span data-stu-id="f0748-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="f0748-222">您也可以從頭實作 `EngagementNotifier.executeNotifAnnouncementAction` 。</span><span class="sxs-lookup"><span data-stu-id="f0748-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="f0748-223">通知生命週期</span><span class="sxs-lookup"><span data-stu-id="f0748-223">Notification life cycle</span></span>
<span data-ttu-id="f0748-224">使用 hello 預設分類，某些存留週期方法會呼叫在 hello`EngagementReachInteractiveContent`物件 tooreport 統計資料和更新 hello 活動狀態：</span><span class="sxs-lookup"><span data-stu-id="f0748-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="f0748-225">當 hello 通知會顯示在應用程式，或將放在 hello 狀態列時，hello`displayNotification`方法呼叫 （它會報告統計資料） 所`EngagementReachAgent`如果`handleNotification`傳回`true`。</span><span class="sxs-lookup"><span data-stu-id="f0748-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="f0748-226">如果關閉 hello 通知，hello`exitNotification`呼叫方法時，統計資料會報告，並可立即處理下一個活動。</span><span class="sxs-lookup"><span data-stu-id="f0748-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="f0748-227">如果按一下 hello 通知，`actionNotification`是呼叫，統計資料會報告與相關聯的 hello 意圖會啟動。</span><span class="sxs-lookup"><span data-stu-id="f0748-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="f0748-228">如果您實作`EngagementNotifier`略過 hello 預設行為，您自己有 toocall 這些生命週期的方法。</span><span class="sxs-lookup"><span data-stu-id="f0748-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="f0748-229">hello 遵循範例將說明某些情況下，會在略過 hello 預設行為：</span><span class="sxs-lookup"><span data-stu-id="f0748-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="f0748-230">您不延伸 `EngagementDefaultNotifier`，例如從頭開始實作類別處理。</span><span class="sxs-lookup"><span data-stu-id="f0748-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="f0748-231">系統通知您已覆寫 hello`onNotificationPrepared`您修改`contentIntent`或`deleteIntent`在 hello`Notification`物件。</span><span class="sxs-lookup"><span data-stu-id="f0748-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="f0748-232">應用程式內通知您已覆寫`prepareInAppArea`，至少是確定 toomap `actionNotification` tooone U.I 控制項。</span><span class="sxs-lookup"><span data-stu-id="f0748-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="f0748-233">如果`handleNotification`擲回例外狀況，hello 內容會刪除與`dropContent`呼叫。</span><span class="sxs-lookup"><span data-stu-id="f0748-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="f0748-234">這報告在統計資料中，並且立即可以處理接下來的活動。</span><span class="sxs-lookup"><span data-stu-id="f0748-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="f0748-235">宣告和輪詢</span><span class="sxs-lookup"><span data-stu-id="f0748-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="f0748-236">版面配置</span><span class="sxs-lookup"><span data-stu-id="f0748-236">Layouts</span></span>
<span data-ttu-id="f0748-237">您可以修改 hello `engagement_text_announcement.xml`，`engagement_web_announcement.xml`和`engagement_poll.xml`toocustomize 文字公告、 web 宣告與輪詢檔案。</span><span class="sxs-lookup"><span data-stu-id="f0748-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="f0748-238">這些檔案共用 hello 標題區域與 hello 按鈕區域的兩個一般配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="f0748-239">hello 標題 hello 配置有`engagement_content_title.xml`和使用 hello 得名 drawable hello 背景檔案。</span><span class="sxs-lookup"><span data-stu-id="f0748-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="f0748-240">hello hello 動作和 [結束] 按鈕的配置是`engagement_button_bar.xml`和使用 hello 得名 drawable hello 背景檔案。</span><span class="sxs-lookup"><span data-stu-id="f0748-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="f0748-241">在投票，hello 問題版面配置和其選項動態膨脹使用多次 hello `engagement_question.xml` hello 問題與 hello 的版面配置檔`engagement_choice.xml`hello 選擇的檔案。</span><span class="sxs-lookup"><span data-stu-id="f0748-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="f0748-242">類別</span><span class="sxs-lookup"><span data-stu-id="f0748-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="f0748-243">替代版面配置</span><span class="sxs-lookup"><span data-stu-id="f0748-243">Alternate layouts</span></span>
<span data-ttu-id="f0748-244">通知，如同 hello 活動的類別可以是您的宣告與輪詢使用的 toohave 替代配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="f0748-245">例如，toocreate 文字公告的類別，您可以擴充`EngagementTextAnnouncementActivity`參照該 hello`AndroidManifest.xml`檔案：</span><span class="sxs-lookup"><span data-stu-id="f0748-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="f0748-246">請注意在 hello 意圖該 hello 類別目錄會使用篩選器與 hello 預設公告活動 toomake hello 差異。</span><span class="sxs-lookup"><span data-stu-id="f0748-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="f0748-247">hello Reach SDK 使用 hello 意圖系統 tooresolve hello 正確的活動特定分類，則會回到上 hello 預設分類如果 hello 解析失敗。</span><span class="sxs-lookup"><span data-stu-id="f0748-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="f0748-248">就會有 tooimplement `MyCustomTextAnnouncementActivity`，如果您只想 toochange hello 配置 （但保留 hello 相同檢視識別項），您只在 toodefine hello 類別，例如下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0748-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="f0748-249">只要取代文字公告 tooreplace hello 預設分類`android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"`由您的實作。</span><span class="sxs-lookup"><span data-stu-id="f0748-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="f0748-250">可以以類似的方式自訂 web 公告與輪詢。</span><span class="sxs-lookup"><span data-stu-id="f0748-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="f0748-251">Web 公告，您可以擴充`EngagementWebAnnouncementActivity`並宣告您的活動 hello`AndroidManifest.xml`如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f0748-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="f0748-252">針對輪詢您可以延伸`EngagementPollActivity`並宣告您在 hello`AndroidManifest.xml`如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f0748-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="f0748-253">從頭實作</span><span class="sxs-lookup"><span data-stu-id="f0748-253">Implementation from scratch</span></span>
<span data-ttu-id="f0748-254">您可以通知 （與輪詢） 活動的實作類別，而不用擴充一個 hello`Engagement*Activity`類別所提供 hello Reach SDK。</span><span class="sxs-lookup"><span data-stu-id="f0748-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="f0748-255">這非常有用，例如是否要讓 toodefine 未使用相同檢視的 hello hello 標準配置的配置。</span><span class="sxs-lookup"><span data-stu-id="f0748-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="f0748-256">類似的進階的通知自訂建議 toolook 在 hello 標準實作 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="f0748-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="f0748-257">以下是一些事情 tookeep 記住： 觸達將會啟動 hello 活動特定的意圖 （對應 toohello 意圖篩選），再加上額外的參數也就是 hello 內容識別項。</span><span class="sxs-lookup"><span data-stu-id="f0748-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="f0748-258">tooretrieve hello 內容物件會包含您指定當建立 hello 活動 hello 網站上您的 hello 欄位可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f0748-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="f0748-259">統計資料，則應該報告 hello 內容會顯示在 hello`onResume`事件：</span><span class="sxs-lookup"><span data-stu-id="f0748-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="f0748-260">然後，請不要忘記 toocall`actionContent(this)`或`exitContent(this)`hello 內容物件之前先發掘背景的 hello 活動上。</span><span class="sxs-lookup"><span data-stu-id="f0748-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="f0748-261">如果您不可以呼叫`actionContent`或`exitContent`、 統計資料將不會傳送 （也就是在 hello 活動上的任何分析） 和多個重要的是，hello hello 應用程式處理序重新啟動之前，不會通知下一個活動。</span><span class="sxs-lookup"><span data-stu-id="f0748-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="f0748-262">方向或其他組態變更可以讓 hello 程式碼很難解釋 toodetermine 是否 hello 活動便會進入背景，或不、 hello 標準實作可確定 hello 內容報告為離開如果 hello 使用者離開 hello 活動 （無論是由按下`HOME`或`BACK`) 但不是如果 hello 方向變更。</span><span class="sxs-lookup"><span data-stu-id="f0748-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="f0748-263">以下是 hello 值得注意的 hello 實作：</span><span class="sxs-lookup"><span data-stu-id="f0748-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="f0748-264">如您所見，如果您呼叫`actionContent(this)`然後完成 hello 活動`exitContent(this)`影響的情況下可以安全地呼叫。</span><span class="sxs-lookup"><span data-stu-id="f0748-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon 裝置傳訊]:https://developer.amazon.com/sdk/adm.html
