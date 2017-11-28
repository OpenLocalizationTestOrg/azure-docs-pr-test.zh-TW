---
title: "aaaAzure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="4c463-103">如何與 Engagement ADM tooIntegrate</span><span class="sxs-lookup"><span data-stu-id="4c463-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4c463-104">您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。</span><span class="sxs-lookup"><span data-stu-id="4c463-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="4c463-105">本文件是您已經整合 hello 觸達模組和計劃 toopush Amazon 裝置時，才有用。</span><span class="sxs-lookup"><span data-stu-id="4c463-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="4c463-106">在您的應用程式，請先閱讀如何 toointegrate 觸達活動 tooIntegrate Engagement 觸達在 Android 上。</span><span class="sxs-lookup"><span data-stu-id="4c463-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="4c463-107">簡介</span><span class="sxs-lookup"><span data-stu-id="4c463-107">Introduction</span></span>
<span data-ttu-id="4c463-108">整合 ADM 可讓您的應用程式 toobe 推入 Amazon Android 裝置為目標時。</span><span class="sxs-lookup"><span data-stu-id="4c463-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="4c463-109">ADM 裝載一律推入 toohello SDK 包含 hello `azme` hello 資料物件中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4c463-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="4c463-110">因此，如果您在應用程式中因為其他目的使用 ADM，可以根據該金鑰篩選推送。</span><span class="sxs-lookup"><span data-stu-id="4c463-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c463-111">Amazon Device Messaging 只支援執行 Android 4.0.3 或更新版本的 Amazon Kindle 裝置；不過，您仍可將這段程式碼安全地整合至其他裝置。</span><span class="sxs-lookup"><span data-stu-id="4c463-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="4c463-112">註冊 tooADM</span><span class="sxs-lookup"><span data-stu-id="4c463-112">Sign up tooADM</span></span>
<span data-ttu-id="4c463-113">如果尚未這麼做，您必須在 Amazon 帳戶上啟用 ADM。</span><span class="sxs-lookup"><span data-stu-id="4c463-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="4c463-114">hello 程序中有詳細說明在： [ <https://developer.amazon.com/sdk/adm/credentials.html>]。</span><span class="sxs-lookup"><span data-stu-id="4c463-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="4c463-115">完成 hello 程序，您會收到：</span><span class="sxs-lookup"><span data-stu-id="4c463-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="4c463-116">OAuth 認證 （用戶端識別碼和用戶端密碼） Engagement toobe 無法 toopush 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="4c463-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="4c463-117">API 金鑰，必須整合到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c463-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="4c463-118">SDK 整合</span><span class="sxs-lookup"><span data-stu-id="4c463-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="4c463-119">管理裝置註冊</span><span class="sxs-lookup"><span data-stu-id="4c463-119">Managing device registrations</span></span>
<span data-ttu-id="4c463-120">每個裝置必須傳送註冊命令 toohello ADM 伺服器，否則為也無法到達。</span><span class="sxs-lookup"><span data-stu-id="4c463-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="4c463-121">如果您已經使用 hello [ADM 用戶端程式庫]，而且已經擁有[整合 ADM]您可以直接移 tooandroid sdk-adm-接收。</span><span class="sxs-lookup"><span data-stu-id="4c463-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="4c463-122">如果您未整合 ADM 尚未 Engagement 有更簡單的方式 tooenable 在您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4c463-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="4c463-123">編輯 `AndroidManifest.xml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="4c463-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="4c463-124">加入 hello Amazon 命名空間、 hello 檔案應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="4c463-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="4c463-125">內部 hello`<application/>`標記中，新增此區段：</span><span class="sxs-lookup"><span data-stu-id="4c463-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="4c463-126">加入之後 hello amazon 標記，您可能必須建置錯誤，如果您的專案建置目標低於 Android 2.1。</span><span class="sxs-lookup"><span data-stu-id="4c463-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="4c463-127">您有 toouse **Android 2.1 +**建置目標 (請不要擔心，您仍舊可以擁有`minSdkVersion`設定 too4)。</span><span class="sxs-lookup"><span data-stu-id="4c463-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="4c463-128">為資產整合 hello ADM API 金鑰，依照[此程序]。</span><span class="sxs-lookup"><span data-stu-id="4c463-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="4c463-129">然後遵循下一節中 hello hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="4c463-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="4c463-130">註冊識別碼 toohello Engagement 推送服務進行通訊，並且接收通知</span><span class="sxs-lookup"><span data-stu-id="4c463-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="4c463-131">中的 hello 裝置 toohello Engagement 推送順序 toocommunicate hello 註冊 id 服務和接收其通知，請新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記 （即使您使用不含 Engagement ADM）：</span><span class="sxs-lookup"><span data-stu-id="4c463-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="4c463-132">請確定您有下列權限中的 hello 您`AndroidManifest.xml`(之前 hello`</application>`標記)。</span><span class="sxs-lookup"><span data-stu-id="4c463-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="4c463-133">授與 Engagement OAuth 認證</span><span class="sxs-lookup"><span data-stu-id="4c463-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="4c463-134">在 Engagement 入口網站中提交您的 OAuth 認證 (用戶端識別碼和用戶端密碼)。</span><span class="sxs-lookup"><span data-stu-id="4c463-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM 用戶端程式庫]:https://developer.amazon.com/sdk/adm/setup.html
[整合 ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[此程序]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
