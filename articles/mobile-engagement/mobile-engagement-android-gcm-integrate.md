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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>如何 tooIntegrate GCM 與 Mobile Engagement
> [!IMPORTANT]
> 您必須遵循 hello tooIntegrate Engagement 在 Android 上再遵循本指南的文件中所述的 hello 整合程序。
> 
> 這份文件會很有用，只有當您已經整合的 hello 送達的模組和計劃 toopush Google Play 的裝置。 在您的應用程式，請先閱讀如何 toointegrate 觸達活動 tooIntegrate Engagement 觸達在 Android 上。
> 
> 

## <a name="introduction"></a>簡介
整合 GCM 可讓您的應用程式 toobe 推入。

GCM 裝載一律推入 toohello SDK 包含 hello `azme` hello 資料物件中的索引鍵。 因此，如果您在應用程式中因為其他目的使用 GCM，可以根據該金鑰篩選推送。

> [!IMPORTANT]
> 只有執行 Android 2.2 或更高版本，且已安裝 Google Play 並已啟用 Google 背景連線的裝置，才能使用 GCM 推播；不過，您仍可將這段程式碼安全地整合不支援 GCM 的裝置 (只使用對應方式)。
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>利用 API 金鑰建立 Google 雲端通訊專案
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>SDK 整合
### <a name="managing-device-registrations"></a>管理裝置註冊
每個裝置必須傳送註冊命令 toohello Google 伺服器，否則為也無法到達。

從 GCM 通知 （hello 裝置是自動解除登錄如果 hello 應用程式已解除安裝），也可以取消登錄裝置。

如果您不使用[Google 播放 SDK]或您不要已經傳送 hello 註冊意圖自行，您可以進行註冊 hello 裝置會自動為您的參與。

tooenable，新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記：

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>註冊識別碼 toohello Engagement 推送服務進行通訊，並且接收通知
中的 hello 裝置 toohello Engagement 推送順序 toocommunicate hello 註冊 id 服務和接收其通知，請新增下列 tooyour hello `AndroidManifest.xml` hello 內的檔案，`<application/>`標記 （即使您自行管理裝置註冊）：

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

請確定您有下列權限中的 hello 您`AndroidManifest.xml`(hello 之後`</application>`標記)。

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>授與 Mobile Engagement 存取 tooyour GCM API 金鑰
請遵循[本指南](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key)toogrant Mobile Engagement 存取 tooyour GCM API 金鑰。

[Google 播放 SDK]:https://developers.google.com/cloud-messaging/android/start
