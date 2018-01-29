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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a>如何整合 ADM 與 Engagement
> [!IMPORTANT]
> 您必須遵循＜如何在 Android 上整合＞文件中所述的整合程序，才能接著遵循本指南。
> 
> 本文件只有在您已經整合觸達模組並打算推送 Amazon 裝置時才適用。 若要在應用程式中整合 Reach 促銷活動，請先閱讀「如何在 Android 上整合 Engagement Reach」。
> 
> 

## <a name="introduction"></a>簡介
整合 ADM 可在目標為 Amazon Android 裝置時推送。

推送到 ADM 裝載的 SDK 一律包含 `azme` 資料物件中的金鑰。 因此，如果您在應用程式中因為其他目的使用 ADM，可以根據該金鑰篩選推送。

> [!IMPORTANT]
> Amazon Device Messaging 只支援執行 Android 4.0.3 或更新版本的 Amazon Kindle 裝置；不過，您仍可將這段程式碼安全地整合至其他裝置。
> 
> 

## <a name="sign-up-to-adm"></a>註冊 ADM
如果尚未這麼做，您必須在 Amazon 帳戶上啟用 ADM。

有關此程序的詳細步驟，請參閱： [<https://developer.amazon.com/sdk/adm/credentials.html>]。

完成此程序後，您會得到：

* OAuth 認證 (用戶端識別碼和用戶端密碼)，讓 Engagement 能夠推播您的裝置。
* API 金鑰，必須整合到您的應用程式。

## <a name="sdk-integration"></a>SDK 整合
### <a name="managing-device-registrations"></a>管理裝置註冊
每個裝置都必須傳送註冊命令給 ADM 伺服器，否則無法連線該裝置。

如果您已經使用 [ADM 用戶端程式庫]，而且已經擁有[整合的 ADM]，則可直接跳至 android-sdk-adm-receive。

如果您還沒有整合的 ADM，Engagement 提供一個在應用程式中啟用的更簡便方式：

編輯 `AndroidManifest.xml` 檔案：

* 新增 Amazon 命名空間，檔案應該類似這樣：
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* 在 `<application/>` 標記中加入此區段：
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* 加入 amazon 標記後，如果您的專案建置目標低於 Android 2.1，可能會出現建置錯誤。 您必須使用 **Android 2.1+** 建置目標 (別擔心，您仍可將 `minSdkVersion` 設為 4)。
* 依照 [此程序]，將 ADM API 金鑰整合為資產。

然後依照下一節的指示進行。

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a>將註冊識別碼傳遞給 Engagement 推播服務，並接收通知
若要將裝置的註冊識別碼傳遞給 Engagement 推播服務並接收其通知，請將下列內容加入 `AndroidManifest.xml` 檔案的 `<application/>` 標記中 (即使您未搭配 Engagement 使用 ADM，也請這麼做)：

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

確定您在 `AndroidManifest.xml` 中具有下列權限 (在 `</application>` 標記之前)。

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>授與 Engagement OAuth 認證
在 Engagement 入口網站中提交您的 OAuth 認證 (用戶端識別碼和用戶端密碼)。

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM 用戶端程式庫]:https://developer.amazon.com/sdk/adm/setup.html
[整合的 ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[此程序]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
