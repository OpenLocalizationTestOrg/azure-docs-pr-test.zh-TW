---
title: "Azure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="1fc9d-103">如何整合 ADM 與 Engagement</span><span class="sxs-lookup"><span data-stu-id="1fc9d-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1fc9d-104">您必須遵循＜如何在 Android 上整合＞文件中所述的整合程序，才能接著遵循本指南。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="1fc9d-105">本文件只有在您已經整合觸達模組並打算推送 Amazon 裝置時才適用。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="1fc9d-106">若要在應用程式中整合 Reach 促銷活動，請先閱讀「如何在 Android 上整合 Engagement Reach」。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="1fc9d-107">簡介</span><span class="sxs-lookup"><span data-stu-id="1fc9d-107">Introduction</span></span>
<span data-ttu-id="1fc9d-108">整合 ADM 可在目標為 Amazon Android 裝置時推送。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="1fc9d-109">推送到 ADM 裝載的 SDK 一律包含 `azme` 資料物件中的金鑰。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="1fc9d-110">因此，如果您在應用程式中因為其他目的使用 ADM，可以根據該金鑰篩選推送。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fc9d-111">Amazon Device Messaging 只支援執行 Android 4.0.3 或更新版本的 Amazon Kindle 裝置；不過，您仍可將這段程式碼安全地整合至其他裝置。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="1fc9d-112">註冊 ADM</span><span class="sxs-lookup"><span data-stu-id="1fc9d-112">Sign up to ADM</span></span>
<span data-ttu-id="1fc9d-113">如果尚未這麼做，您必須在 Amazon 帳戶上啟用 ADM。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="1fc9d-114">有關此程序的詳細步驟，請參閱： [<https://developer.amazon.com/sdk/adm/credentials.html>]。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="1fc9d-115">完成此程序後，您會得到：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="1fc9d-116">OAuth 認證 (用戶端識別碼和用戶端密碼)，讓 Engagement 能夠推播您的裝置。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="1fc9d-117">API 金鑰，必須整合到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="1fc9d-118">SDK 整合</span><span class="sxs-lookup"><span data-stu-id="1fc9d-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="1fc9d-119">管理裝置註冊</span><span class="sxs-lookup"><span data-stu-id="1fc9d-119">Managing device registrations</span></span>
<span data-ttu-id="1fc9d-120">每個裝置都必須傳送註冊命令給 ADM 伺服器，否則無法連線該裝置。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="1fc9d-121">如果您已經使用 [ADM 用戶端程式庫]，而且已經擁有[整合的 ADM]，則可直接跳至 android-sdk-adm-receive。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="1fc9d-122">如果您還沒有整合的 ADM，Engagement 提供一個在應用程式中啟用的更簡便方式：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="1fc9d-123">編輯 `AndroidManifest.xml` 檔案：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="1fc9d-124">新增 Amazon 命名空間，檔案應該類似這樣：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="1fc9d-125">在 `<application/>` 標記中加入此區段：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="1fc9d-126">加入 amazon 標記後，如果您的專案建置目標低於 Android 2.1，可能會出現建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="1fc9d-127">您必須使用 **Android 2.1+** 建置目標 (別擔心，您仍可將 `minSdkVersion` 設為 4)。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="1fc9d-128">依照 [此程序]，將 ADM API 金鑰整合為資產。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="1fc9d-129">然後依照下一節的指示進行。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="1fc9d-130">將註冊識別碼傳遞給 Engagement 推播服務，並接收通知</span><span class="sxs-lookup"><span data-stu-id="1fc9d-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="1fc9d-131">若要將裝置的註冊識別碼傳遞給 Engagement 推播服務並接收其通知，請將下列內容加入 `AndroidManifest.xml` 檔案的 `<application/>` 標記中 (即使您未搭配 Engagement 使用 ADM，也請這麼做)：</span><span class="sxs-lookup"><span data-stu-id="1fc9d-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="1fc9d-132">確定您在 `AndroidManifest.xml` 中具有下列權限 (在 `</application>` 標記之前)。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="1fc9d-133">授與 Engagement OAuth 認證</span><span class="sxs-lookup"><span data-stu-id="1fc9d-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="1fc9d-134">在 Engagement 入口網站中提交您的 OAuth 認證 (用戶端識別碼和用戶端密碼)。</span><span class="sxs-lookup"><span data-stu-id="1fc9d-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="1fc9d-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="1fc9d-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="1fc9d-136">[ADM 用戶端程式庫]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="1fc9d-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="1fc9d-137">[整合的 ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="1fc9d-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="1fc9d-138">[此程序]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="1fc9d-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
