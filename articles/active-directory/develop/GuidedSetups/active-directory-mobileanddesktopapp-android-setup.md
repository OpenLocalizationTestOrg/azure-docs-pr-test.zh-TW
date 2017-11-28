---
title: "Azure AD v2 Android 快速入門 - 設定 | Microsoft Docs"
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
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="33783-103">設定專案</span><span class="sxs-lookup"><span data-stu-id="33783-103">Set up your project</span></span>

> <span data-ttu-id="33783-104">想要改為下載此範例的 Android Studio 專案嗎？</span><span class="sxs-lookup"><span data-stu-id="33783-104">Prefer to download this sample's Android Studio project instead?</span></span> <span data-ttu-id="33783-105">[下載專案](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) 並跳至[設定步驟](#create-an-application-express)，以在執行之前先設定程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="33783-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="33783-106">建立新專案</span><span class="sxs-lookup"><span data-stu-id="33783-106">Create a new project</span></span> 
1.  <span data-ttu-id="33783-107">開啟 Android Studio，移至：`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="33783-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="33783-108">為您的應用程式命名並按一下 `Next`</span><span class="sxs-lookup"><span data-stu-id="33783-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="33783-109">確定已選取 [API 21 or newer (Android 5.0) (API 21 或更新版本 (Android 5.0))] 並按一下 `Next`</span><span class="sxs-lookup"><span data-stu-id="33783-109">Make sure to select *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="33783-110">保留 `Empty Activity`，按一下 `Next`，然後按一下 `Finish`</span><span class="sxs-lookup"><span data-stu-id="33783-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="33783-111">將 Microsoft Authentication Library (MSAL) 新增至您的專案</span><span class="sxs-lookup"><span data-stu-id="33783-111">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1.  <span data-ttu-id="33783-112">在 Android Studio 中，移至：`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="33783-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="33783-113">複製下列程式碼並貼到 `Dependencies` 底下：</span><span class="sxs-lookup"><span data-stu-id="33783-113">Copy and paste the following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="33783-114">關於此套件</span><span class="sxs-lookup"><span data-stu-id="33783-114">About this package</span></span>

<span data-ttu-id="33783-115">上面的套件會安裝 Microsoft Authentication Library (MSAL)。</span><span class="sxs-lookup"><span data-stu-id="33783-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="33783-116">MSAL 會處理使用者權杖的取得、快取及重新整理作業，這些權杖是用來存取受 Azure Active Directory v2 端點保護的 API。</span><span class="sxs-lookup"><span data-stu-id="33783-116">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="33783-117">建立您應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="33783-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="33783-118">開啟：`activity_main.xml` (在 `res` > `layout` 底下)</span><span class="sxs-lookup"><span data-stu-id="33783-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="33783-119">將活動配置從 `android.support.constraint.ConstraintLayout` 或其他配置變更為 `LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="33783-119">Change the activity layout from `android.support.constraint.ConstraintLayout` or other to `LinearLayout`</span></span>
3.  <span data-ttu-id="33783-120">將 `android:orientation="vertical"` 屬性新增至 `LinearLayout` 節點</span><span class="sxs-lookup"><span data-stu-id="33783-120">Add `android:orientation="vertical"` property to `LinearLayout` node</span></span>
4.  <span data-ttu-id="33783-121">複製下列程式碼並貼到 `LinearLayout` 節點中，取代目前的內容：</span><span class="sxs-lookup"><span data-stu-id="33783-121">Copy and paste the following code into the `LinearLayout` node, replacing the current content:</span></span>

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

