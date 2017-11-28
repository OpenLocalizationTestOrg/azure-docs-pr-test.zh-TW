---
title: "aaaAzure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="22d69-103">如何 tooIntegrate GCM 與 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="22d69-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22d69-104">您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。</span><span class="sxs-lookup"><span data-stu-id="22d69-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="22d69-105">這份文件會很有用，只有當您已經整合的 hello 送達的模組和計劃 toopush Google Play 的裝置。</span><span class="sxs-lookup"><span data-stu-id="22d69-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="22d69-106">在您的應用程式，請先閱讀如何 toointegrate 觸達活動 tooIntegrate Engagement 觸達在 Android 上。</span><span class="sxs-lookup"><span data-stu-id="22d69-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="22d69-107">簡介</span><span class="sxs-lookup"><span data-stu-id="22d69-107">Introduction</span></span>
<span data-ttu-id="22d69-108">整合 GCM 可讓您的應用程式 toobe 推入。</span><span class="sxs-lookup"><span data-stu-id="22d69-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="22d69-109">GCM 裝載一律推入 toohello SDK 包含 hello `azme` hello 資料物件中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="22d69-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="22d69-110">因此，如果您在應用程式中因為其他目的使用 GCM，可以根據該金鑰篩選推送。</span><span class="sxs-lookup"><span data-stu-id="22d69-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22d69-111">只有執行 Android 2.2 或更高版本，且已安裝 Google Play 並已啟用 Google 背景連線的裝置，才能使用 GCM 推播；不過，您仍可將這段程式碼安全地整合不支援 GCM 的裝置 (只使用對應方式)。</span><span class="sxs-lookup"><span data-stu-id="22d69-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="22d69-112">利用 API 金鑰建立 Google 雲端通訊專案</span><span class="sxs-lookup"><span data-stu-id="22d69-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="22d69-113">SDK 整合</span><span class="sxs-lookup"><span data-stu-id="22d69-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="22d69-114">管理裝置註冊</span><span class="sxs-lookup"><span data-stu-id="22d69-114">Managing device registrations</span></span>
<span data-ttu-id="22d69-115">每個裝置必須傳送註冊命令 toohello Google 伺服器，否則為也無法到達。</span><span class="sxs-lookup"><span data-stu-id="22d69-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="22d69-116">從 GCM 通知 （hello 裝置是自動解除登錄如果 hello 應用程式已解除安裝），也可以取消登錄裝置。</span><span class="sxs-lookup"><span data-stu-id="22d69-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="22d69-117">如果您不使用[Google 播放 SDK]或您不要已經傳送 hello 註冊意圖自行，您可以進行註冊 hello 裝置會自動為您的參與。</span><span class="sxs-lookup"><span data-stu-id="22d69-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="22d69-118">tooenable，新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記：</span><span class="sxs-lookup"><span data-stu-id="22d69-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="22d69-119">註冊識別碼 toohello Engagement 推送服務進行通訊，並且接收通知</span><span class="sxs-lookup"><span data-stu-id="22d69-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="22d69-120">中的 hello 裝置 toohello Engagement 推送順序 toocommunicate hello 註冊 id 服務和接收其通知，請新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記 （即使您自行管理裝置註冊）：</span><span class="sxs-lookup"><span data-stu-id="22d69-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="22d69-121">請確定您有下列權限中的 hello 您`AndroidManifest.xml`(hello 之後`</application>`標記)。</span><span class="sxs-lookup"><span data-stu-id="22d69-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="22d69-122">授與 Mobile Engagement 存取 tooyour GCM API 金鑰</span><span class="sxs-lookup"><span data-stu-id="22d69-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="22d69-123">請遵循[本指南](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key)toogrant Mobile Engagement 存取 tooyour GCM API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="22d69-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google 播放 SDK]:https://developers.google.com/cloud-messaging/android/start
