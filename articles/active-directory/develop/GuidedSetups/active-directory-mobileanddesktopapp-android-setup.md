---
title: "aaaAzure AD v2 Android 快速入門-安裝 |Microsoft 文件"
description: "Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API，或呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>設定專案

> 改為偏好 toodownload 這個範例的 Android Studio 專案嗎？ [下載專案](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。


### <a name="create-a-new-project"></a>建立新專案 
1.  開啟 Android Studio，移至：`File` > `New` > `New Project`
2.  為您的應用程式命名並按一下 `Next`
3.  請確定 tooselect *API 21 或更新版本 (Android 5.0)*按一下`Next`
4.  保留 `Empty Activity`，按一下 `Next`，然後按一下 `Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>加入 hello Microsoft 驗證程式庫 (MSAL) tooyour 專案
1.  在 Android Studio 中，移至：`Gradle Scripts` > `build.gradle (Module: app)`
2.  複製和貼上 hello 下列程式碼底下`Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>關於此套件

上述的 hello 套件會安裝 hello Microsoft 驗證程式庫 (MSAL)。 MSAL 處理取得，快取和重新整理使用者使用的語彙基元 tooaccess 受 Azure Active Directory v2 端點的 Api。
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>建立您應用程式的 UI

1.  開啟：`activity_main.xml` (在 `res` > `layout` 底下)
2.  變更從 hello 活動版面配置`android.support.constraint.ConstraintLayout`或其他太`LinearLayout`
3.  新增`android:orientation="vertical"`屬性太`LinearLayout`節點
4.  複製和貼上 hello 下列程式碼到 hello`LinearLayout`節點，取代 hello 目前內容：

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

