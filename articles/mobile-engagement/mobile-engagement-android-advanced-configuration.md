---
title: "Azure Mobile Engagement Android SDK 的 aaaAdvanced 組態"
description: "說明進階組態選項包括 hello，Android 的 Azure Mobile Engagement Android SDK 資訊清單的 hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Azure Mobile Engagement Android SDK 的進階組態
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

此程序描述如何 tooconfigure Azure Mobile Engagement Android 應用程式的各種組態選項。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>權限需求
有些選項需要所有的參考和內嵌在 hello 特定功能中的以下所列的特定權限。 加入這些權限 toohello AndroidManifest.xml 專案的之前或之後 hello`<application>`標記。

hello 權限的程式碼需要 toolook 如下 hello，填寫 hello hello 表的適當權限。

    <uses-permission android:name="android.permission.[specific permission]"/>


| 權限 | 使用時機 |
| --- | --- |
| 網際網路 |必要。 針對基本報告 |
| ACCESS_NETWORK_STATE |必要。 針對基本報告 |
| RECEIVE_BOOT_COMPLETED |必要。 裝置重新開機後 hello 通知中心 tooshow |
| WAKE_LOCK |建議使用。 啟用「在使用 WiFi 或螢幕關閉時收集統計資料」 |
| VIBRATE |選用。 在收到通知後啟用震動 |
| DOWNLOAD_WITHOUT_NOTIFICATION |選用。 啟用「Android 重點通知」 |
| WRITE_EXTERNAL_STORAGE |選用。 啟用「Android 重點通知」 |
| ACCESS_COARSE_LOCATION |選用。 啟用「即時位置報告」 |
| ACCESS_FINE_LOCATION |選用。 啟用「GPS 式即時位置報告」 |

從 Android M 開始，[某些權限是在執行階段管理](mobile-engagement-android-location-reporting.md#android-m-permissions)。

如果您已經在使用``ACCESS_FINE_LOCATION``，則不需要 tooalso 使用``ACCESS_COARSE_LOCATION``。

## <a name="android-manifest-configuration-options"></a>Android 資訊清單組態選項
### <a name="crash-report"></a>當機報告
toodisable 當機報告，加入此程式碼之間 hello`<application>`和`</application>`標記：

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>高載閾值
根據預設，hello Engagement 服務報表會即時記錄。 如果經常改變應用程式報表記錄，它是較佳的 toobuffer hello 記錄檔和 tooreport 一次在固定時間基底 （稱為 「 高載模式 」）。 toodo，因此請加入這個程式碼之間 hello`<application>`和`</application>`標記：

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

高載模式稍微增加 hello 電池壽命，但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。 高載閾值不能超過 30000 (30 秒)。

### <a name="session-timeout"></a>工作階段逾時
 您可以按 hello 結束活動**首頁**或**回**索引鍵，透過閒置的 設定 hello 電話或跳到其他應用程式。 根據預設，工作階段結束十秒 hello 其最後一個活動結尾之後。 這可避免工作階段分隔每個階段 hello 使用者結束，並傳回 toohello 應用程式快速，可以發生時 hello 使用者收取映像，檢查通知等等。您可能想 toomodify 這個參數。 toodo，因此請加入這個程式碼之間 hello`<application>`和`</application>`標記：

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>停用記錄報告
### <a name="using-a-method-call"></a>使用方法呼叫
如果您想 Engagement toostop 傳送記錄檔，您可以呼叫：

    EngagementAgent.getInstance(context).setEnabled(false);

這個呼叫是持續性的：它使用共用的喜好設定檔案。

如果參與作用中時呼叫此函式，可能需要一分鐘的 hello 服務 toostop。 不過，它將不會啟動所有 hello hello 服務下次您啟動 hello 應用程式。

您可以啟用記錄 reporting 再次呼叫相同函式與 hello `true`。

### <a name="integration-in-your-own-preferenceactivity"></a>在您自己的 `PreferenceActivity`
如不呼叫此函數，您也可以在現有的 `PreferenceActivity` 中直接整合此設定。

您可以設定您的喜好設定檔案 （由 hello 所需的模式） 的 Engagement toouse hello`AndroidManifest.xml`檔案搭配`application meta-data`:

* hello`engagement:agent:settings:name`金鑰是使用的 toodefine hello hello 共用的喜好設定檔案名稱。
* hello`engagement:agent:settings:mode`金鑰是使用的 toodefine hello 模式 hello 共用的喜好設定檔案。 使用 hello 相同模式做為您`PreferenceActivity`。 必須傳遞 hello 模式，表示為數字： 如果您在程式碼中使用常數旗標的組合，請檢查 hello 總計值。

Engagement 一律會使用 hello`engagement:key`內 hello 喜好設定檔案，以便管理這項設定，則為 true 的索引鍵。

下列範例中的 hello`AndroidManifest.xml`顯示 hello 預設值：

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

接著您可以將新增`CheckBoxPreference`中您的喜好設定配置，例如 hello 下列其中一個：

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
