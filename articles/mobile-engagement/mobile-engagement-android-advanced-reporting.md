---
title: "aaaAdvanced 報告 Azure Mobile Engagement Android SDK 選項"
description: "描述如何 toodo 進階報告 toocapture 分析 Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Android 上使用 Engagement 的進階報告
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

本主題說明 Android 應用程式中的其他報告案例。 您可以套用這些選項的 toohello 應用程式建立 hello[入門](mobile-engagement-android-get-started.md)教學課程。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

您已完成的 hello 教學課程刻意直接和簡單，但屬於進階的選項，您可以選擇。

## <a name="modifying-your-activity-classes"></a>修改 `Activity` 類別
在 hello[快速入門教學課程](mobile-engagement-android-get-started.md)，只 toodo 已 toomake 您`*Activity`子類別繼承自 hello 對應`Engagement*Activity`類別。 例如，如果您的舊版活動延伸 `ListActivity`，可以將它延伸 `EngagementListActivity`。

> [!IMPORTANT]
> 當使用`EngagementListActivity`或`EngagementExpandableListActivity`，請確定任何呼叫太`requestWindowFeature(...);`太進行 hello 呼叫之前`super.onCreate(...);`，否則會發生損毀。
> 
> 

您可以在 hello 找到這些類別`src`資料夾，並可以將其複製到您的專案。 hello 類別中也會有 hello **JavaDoc**。

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>替代方法：手動呼叫 `startActivity()` 和 `endActivity()`
如果您無法或不想 toooverload 您`Activity`類別，您可以改為開始和結束您的活動藉由呼叫 hello`EngagementAgent`的直接的方法。

> [!IMPORTANT]
> hello Android SDK 從未呼叫 hello`endActivity()`方法，即使關閉 hello 應用程式 （在 Android 上，應用程式會永遠不會關閉）。 因此，它是*高*建議 toocall hello `startActivity()` hello 中的方法`onResume`回呼的*所有*程式活動與 hello `endActivity()` hello 中的方法`onPause()`回呼的*所有*程式活動。 這是 hello 唯一方式 toobe 確定不會遺漏工作階段。 如果工作階段外洩，hello Engagement 服務永遠不會中斷 hello Engagement 後端 （因為 hello 服務仍會保持連接，只要工作階段已暫止）。
> 
> 

下列是一個範例：

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

這個範例是類似 toohello`EngagementActivity`類別與變種，提供其原始程式碼中 hello`src`資料夾。

## <a name="using-applicationoncreate"></a>使用 Application.onCreate()
您將放置在任何程式碼`Application.onCreate()`和其他應用程式中執行所有應用程式的程序，包括 hello Engagement 服務回呼。 它可能會不必要的副作用，例如不必要的記憶體配置和 hello Engagement 的處理序中的執行緒或重複廣播接收器或服務。

如果您覆寫`Application.onCreate()`，我們建議您加入下列程式碼片段在 hello 開頭的 hello 您`Application.onCreate()`函式：

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

您可以 hello 相同的動作，如`Application.onTerminate()`， `Application.onLowMemory()`，和`Application.onConfigurationChanged(...)`。

您也可以擴充`EngagementApplication`而不是擴充`Application`: hello 回呼`Application.onCreate()`程序的核取並呼叫沒有 hello`Application.onApplicationProcessCreate()`僅 hello 目前處理序是否不 hello 一個裝載 hello Engagement 服務，hello 適用相同的規則hello 其他回呼。

## <a name="tags-in-hello-androidmanifestxml-file"></a>Hello AndroidManifest.xml 檔中的標記
在 hello AndroidManifest.xml 檔中的 hello 服務標記，hello`android:label`屬性可讓您的行動服務的 hello toochoose hello 名稱出現 tooend 使用者在他們的電話號碼 hello 」 執行的服務 」 畫面中。 我們建議將此屬性設定太`"<Your application name>Service"`(例如， `"AcmeFunGameService"`)。

指定 hello`android:process`屬性可確保該 hello Engagement 服務執行其自己的處理程序 （在相同的處理序當做您的應用程式會讓您的主要/UI 執行緒可能較不回應 hello 執行 Engagement）。

## <a name="building-with-proguard"></a>使用 ProGuard 建置
如果您建立使用 ProGuard 應用程式套件，您需要 tookeep 某些類別。 您可以使用下列組態程式碼片段的 hello:

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
