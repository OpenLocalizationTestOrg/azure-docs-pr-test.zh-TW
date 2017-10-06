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
# <a name="how-toointegrate-adm-with-engagement"></a>如何與 Engagement ADM tooIntegrate
> [!IMPORTANT]
> 您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。
> 
> 本文件是您已經整合 hello 觸達模組和計劃 toopush Amazon 裝置時，才有用。 在您的應用程式，請先閱讀如何 toointegrate 觸達活動 tooIntegrate Engagement 觸達在 Android 上。
> 
> 

## <a name="introduction"></a>簡介
整合 ADM 可讓您的應用程式 toobe 推入 Amazon Android 裝置為目標時。

ADM 裝載一律推入 toohello SDK 包含 hello `azme` hello 資料物件中的索引鍵。 因此，如果您在應用程式中因為其他目的使用 ADM，可以根據該金鑰篩選推送。

> [!IMPORTANT]
> Amazon Device Messaging 只支援執行 Android 4.0.3 或更新版本的 Amazon Kindle 裝置；不過，您仍可將這段程式碼安全地整合至其他裝置。
> 
> 

## <a name="sign-up-tooadm"></a>註冊 tooADM
如果尚未這麼做，您必須在 Amazon 帳戶上啟用 ADM。

hello 程序中有詳細說明在： [ <https://developer.amazon.com/sdk/adm/credentials.html>]。

完成 hello 程序，您會收到：

* OAuth 認證 （用戶端識別碼和用戶端密碼） Engagement toobe 無法 toopush 您的裝置。
* API 金鑰，必須整合到您的應用程式。

## <a name="sdk-integration"></a>SDK 整合
### <a name="managing-device-registrations"></a>管理裝置註冊
每個裝置必須傳送註冊命令 toohello ADM 伺服器，否則為也無法到達。

如果您已經使用 hello [ADM 用戶端程式庫]，而且已經擁有[整合 ADM]您可以直接移 tooandroid sdk-adm-接收。

如果您未整合 ADM 尚未 Engagement 有更簡單的方式 tooenable 在您的應用程式：

編輯 `AndroidManifest.xml` 檔案：

* 加入 hello Amazon 命名空間、 hello 檔案應該像這樣：
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* 內部 hello`<application/>`標記中，新增此區段：
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* 加入之後 hello amazon 標記，您可能必須建置錯誤，如果您的專案建置目標低於 Android 2.1。 您有 toouse **Android 2.1 +**建置目標 (請不要擔心，您仍舊可以擁有`minSdkVersion`設定 too4)。
* 為資產整合 hello ADM API 金鑰，依照[此程序]。

然後遵循下一節中 hello hello 指示進行。

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>註冊識別碼 toohello Engagement 推送服務進行通訊，並且接收通知
中的 hello 裝置 toohello Engagement 推送順序 toocommunicate hello 註冊 id 服務和接收其通知，請新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記 （即使您使用不含 Engagement ADM）：

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

請確定您有下列權限中的 hello 您`AndroidManifest.xml`(之前 hello`</application>`標記)。

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>授與 Engagement OAuth 認證
在 Engagement 入口網站中提交您的 OAuth 認證 (用戶端識別碼和用戶端密碼)。

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM 用戶端程式庫]:https://developer.amazon.com/sdk/adm/setup.html
[整合 ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[此程序]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
