---
title: "Azure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="28807-103">如何整合 GCM 與 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="28807-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="28807-104">您必須遵循＜如何在 Android 上整合＞文件中所述的整合程序，才能接著遵循本指南。</span><span class="sxs-lookup"><span data-stu-id="28807-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="28807-105">本文件只有在您已經整合觸達模組並打算推送 Google Play 裝置時才適用。</span><span class="sxs-lookup"><span data-stu-id="28807-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="28807-106">若要在應用程式中整合 Reach 促銷活動，請先閱讀「如何在 Android 上整合 Engagement Reach」。</span><span class="sxs-lookup"><span data-stu-id="28807-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="28807-107">簡介</span><span class="sxs-lookup"><span data-stu-id="28807-107">Introduction</span></span>
<span data-ttu-id="28807-108">整合 GCM 可讓您推播應用程式。</span><span class="sxs-lookup"><span data-stu-id="28807-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="28807-109">推送到 GCM 裝載的 SDK 一律包含資料物件中的 `azme` 金鑰。</span><span class="sxs-lookup"><span data-stu-id="28807-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="28807-110">因此，如果您在應用程式中因為其他目的使用 GCM，可以根據該金鑰篩選推送。</span><span class="sxs-lookup"><span data-stu-id="28807-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28807-111">只有執行 Android 2.2 或更高版本，且已安裝 Google Play 並已啟用 Google 背景連線的裝置，才能使用 GCM 推播；不過，您仍可將這段程式碼安全地整合不支援 GCM 的裝置 (只使用對應方式)。</span><span class="sxs-lookup"><span data-stu-id="28807-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="28807-112">利用 API 金鑰建立 Google 雲端通訊專案</span><span class="sxs-lookup"><span data-stu-id="28807-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="28807-113">SDK 整合</span><span class="sxs-lookup"><span data-stu-id="28807-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="28807-114">管理裝置註冊</span><span class="sxs-lookup"><span data-stu-id="28807-114">Managing device registrations</span></span>
<span data-ttu-id="28807-115">每個裝置都必須傳送註冊命令給 Google 伺服器，否則無法連線該裝置。</span><span class="sxs-lookup"><span data-stu-id="28807-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="28807-116">也可以從 GCM 通知取消註冊裝置 (解除安裝應用程式時會自動取消裝置的註冊)。</span><span class="sxs-lookup"><span data-stu-id="28807-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="28807-117">如果您未使用 [Google Play SDK] ，或者尚未自行傳送註冊對應方式，您可以讓 Engagement 自動註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="28807-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="28807-118">若要啟用此功能，請將下列內容加入 `AndroidManifest.xml` 檔案的 `<application/>` 標記中：</span><span class="sxs-lookup"><span data-stu-id="28807-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="28807-119">將註冊識別碼傳遞給 Engagement 推播服務，並接收通知</span><span class="sxs-lookup"><span data-stu-id="28807-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="28807-120">若要將裝置的註冊識別碼傳遞給 Engagement 推播服務並接收其通知，請將下列內容加入 `AndroidManifest.xml` 檔案的 `<application/>` 標記中 (即使您自行管理裝置註冊，也請這麼做)：</span><span class="sxs-lookup"><span data-stu-id="28807-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="28807-121">確定您在 `AndroidManifest.xml` 中具有下列權限 (在 `</application>` 標記之後)。</span><span class="sxs-lookup"><span data-stu-id="28807-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="28807-122">授與 Mobile Engagement 的存取權給 GCM API 金鑰</span><span class="sxs-lookup"><span data-stu-id="28807-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="28807-123">遵循 [本指南](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) 來授與 Mobile Engagement 的存取權給 GCM API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="28807-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="28807-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="28807-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
