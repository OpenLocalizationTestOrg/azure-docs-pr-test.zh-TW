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
## <a name="set-up-your-project"></a><span data-ttu-id="5e1c9-103">設定專案</span><span class="sxs-lookup"><span data-stu-id="5e1c9-103">Set up your project</span></span>

> <span data-ttu-id="5e1c9-104">改為偏好 toodownload 這個範例的 Android Studio 專案嗎？</span><span class="sxs-lookup"><span data-stu-id="5e1c9-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="5e1c9-105">[下載專案](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。</span><span class="sxs-lookup"><span data-stu-id="5e1c9-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="5e1c9-106">建立新專案</span><span class="sxs-lookup"><span data-stu-id="5e1c9-106">Create a new project</span></span> 
1.  <span data-ttu-id="5e1c9-107">開啟 Android Studio，移至：`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="5e1c9-108">為您的應用程式命名並按一下 `Next`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="5e1c9-109">請確定 tooselect *API 21 或更新版本 (Android 5.0)*按一下`Next`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="5e1c9-110">保留 `Empty Activity`，按一下 `Next`，然後按一下 `Finish`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="5e1c9-111">加入 hello Microsoft 驗證程式庫 (MSAL) tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="5e1c9-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="5e1c9-112">在 Android Studio 中，移至：`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="5e1c9-113">複製和貼上 hello 下列程式碼底下`Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="5e1c9-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="5e1c9-114">關於此套件</span><span class="sxs-lookup"><span data-stu-id="5e1c9-114">About this package</span></span>

<span data-ttu-id="5e1c9-115">上述的 hello 套件會安裝 hello Microsoft 驗證程式庫 (MSAL)。</span><span class="sxs-lookup"><span data-stu-id="5e1c9-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="5e1c9-116">MSAL 處理取得，快取和重新整理使用者使用的語彙基元 tooaccess 受 Azure Active Directory v2 端點的 Api。</span><span class="sxs-lookup"><span data-stu-id="5e1c9-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="5e1c9-117">建立您應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="5e1c9-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="5e1c9-118">開啟：`activity_main.xml` (在 `res` > `layout` 底下)</span><span class="sxs-lookup"><span data-stu-id="5e1c9-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="5e1c9-119">變更從 hello 活動版面配置`android.support.constraint.ConstraintLayout`或其他太`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="5e1c9-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="5e1c9-120">新增`android:orientation="vertical"`屬性太`LinearLayout`節點</span><span class="sxs-lookup"><span data-stu-id="5e1c9-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="5e1c9-121">複製和貼上 hello 下列程式碼到 hello`LinearLayout`節點，取代 hello 目前內容：</span><span class="sxs-lookup"><span data-stu-id="5e1c9-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

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

