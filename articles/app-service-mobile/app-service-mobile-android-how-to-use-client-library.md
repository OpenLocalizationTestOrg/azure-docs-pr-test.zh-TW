---
title: "aaaHow toouse hello Android 的 Azure 行動應用程式 SDK |Microsoft 文件"
description: "如何 toouse hello 適用於 Android 的 Azure 行動應用程式 SDK"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="45b21-103">如何 toouse hello 適用於 Android 的 Azure 行動應用程式 SDK</span><span class="sxs-lookup"><span data-stu-id="45b21-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="45b21-104">本指南也說明如何 toouse hello Android 用戶端 SDK 行動應用程式 tooimplement 常見案例，例如：</span><span class="sxs-lookup"><span data-stu-id="45b21-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="45b21-105">查詢資料 (插入、更新和刪除)。</span><span class="sxs-lookup"><span data-stu-id="45b21-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="45b21-106">驗證。</span><span class="sxs-lookup"><span data-stu-id="45b21-106">Authentication.</span></span>
* <span data-ttu-id="45b21-107">處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="45b21-107">Handling errors.</span></span>
* <span data-ttu-id="45b21-108">自訂 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="45b21-108">Customizing hello client.</span></span>

<span data-ttu-id="45b21-109">此指南著重於 hello 用戶端的 Android SDK。</span><span class="sxs-lookup"><span data-stu-id="45b21-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="45b21-110">toolearn 深入了解 hello 行動應用程式的伺服器端 Sdk，請參閱[搭配.NET 後端 SDK] [ 10]或[toouse 如何 hello Node.js 後端 SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="45b21-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="45b21-111">參考文件</span><span class="sxs-lookup"><span data-stu-id="45b21-111">Reference Documentation</span></span>

<span data-ttu-id="45b21-112">您可以找到 hello [Javadocs API 參考][ 12] hello GitHub 上的 Android 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="45b21-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="45b21-113">支援的平台</span><span class="sxs-lookup"><span data-stu-id="45b21-113">Supported Platforms</span></span>

<span data-ttu-id="45b21-114">hello Azure 行動應用程式 SDK for Android 支援應用程式開發介面層級 19-24 (透過 Nougat KitKat) 電話和平板電腦的表單係數。</span><span class="sxs-lookup"><span data-stu-id="45b21-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="45b21-115">驗證，特別是，利用常用的 web 架構方法 toogather 認證。</span><span class="sxs-lookup"><span data-stu-id="45b21-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="45b21-116">伺服器流程驗證不適用於小型外形規格的裝置，例如手錶。</span><span class="sxs-lookup"><span data-stu-id="45b21-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="45b21-117">設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="45b21-117">Setup and Prerequisites</span></span>

<span data-ttu-id="45b21-118">完整的 hello[行動應用程式快速入門](app-service-mobile-android-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="45b21-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="45b21-119">此工作可確保您已符合開發 Azure Mobile Apps 的所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="45b21-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="45b21-120">快速入門 hello 也可協助您設定您的帳戶，並建立第一個行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="45b21-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="45b21-121">如果您決定不 toocomplete hello 快速入門教學課程，請完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="45b21-122">[建立行動裝置應用程式後端][ 13] toouse 與 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="45b21-123">在 Android Studio 中，[更新 hello Gradle 組建檔案](#gradle-build)。</span><span class="sxs-lookup"><span data-stu-id="45b21-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="45b21-124">[啟用網際網路權限](#enable-internet)。</span><span class="sxs-lookup"><span data-stu-id="45b21-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="45b21-125"><a name="gradle-build"></a>更新 hello Gradle 組建檔案</span><span class="sxs-lookup"><span data-stu-id="45b21-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="45b21-126">變更以下兩個 build.gradle  檔案：</span><span class="sxs-lookup"><span data-stu-id="45b21-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="45b21-127">加入這個程式碼 toohello*專案*層級**build.gradle**檔案置於 hello *buildscript*標記：</span><span class="sxs-lookup"><span data-stu-id="45b21-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="45b21-128">加入這個程式碼 toohello*模組應用程式*層級**build.gradle**檔案置於 hello*相依性*標記：</span><span class="sxs-lookup"><span data-stu-id="45b21-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="45b21-129">目前 hello 最新版本為 3.3.0。</span><span class="sxs-lookup"><span data-stu-id="45b21-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="45b21-130">hello 支援的版本會列出[上 bintray][14]。</span><span class="sxs-lookup"><span data-stu-id="45b21-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="45b21-131"><a name="enable-internet"></a>啟用網際網路權限</span><span class="sxs-lookup"><span data-stu-id="45b21-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="45b21-132">tooaccess Azure，您的應用程式必須啟用 hello 網際網路權限。</span><span class="sxs-lookup"><span data-stu-id="45b21-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="45b21-133">如果尚未啟用，加入下列一行程式碼 tooyour hello **AndroidManifest.xml**檔案：</span><span class="sxs-lookup"><span data-stu-id="45b21-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="45b21-134">建立用戶端連線</span><span class="sxs-lookup"><span data-stu-id="45b21-134">Create a Client Connection</span></span>

<span data-ttu-id="45b21-135">Azure 行動應用程式提供四個函式 tooyour 行動應用程式：</span><span class="sxs-lookup"><span data-stu-id="45b21-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="45b21-136">Azure Mobile Apps Service 的「資料存取」和「離線同步處理」。</span><span class="sxs-lookup"><span data-stu-id="45b21-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="45b21-137">呼叫以 hello Azure 行動應用程式伺服器 SDK 所撰寫的自訂 Api。</span><span class="sxs-lookup"><span data-stu-id="45b21-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="45b21-138">Azure App Service 驗證和授權的「驗證」。</span><span class="sxs-lookup"><span data-stu-id="45b21-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="45b21-139">通知中樞的「推播通知註冊」。</span><span class="sxs-lookup"><span data-stu-id="45b21-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="45b21-140">這些函式首先會要求您建立 `MobileServiceClient` 物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="45b21-141">您的行動用戶端內只應該建立一個 `MobileServiceClient` 物件 (亦即，它應該是單一子句模式)。</span><span class="sxs-lookup"><span data-stu-id="45b21-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="45b21-142">toocreate`MobileServiceClient`物件：</span><span class="sxs-lookup"><span data-stu-id="45b21-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="45b21-143">hello`<MobileAppUrl>`是字串，或是指向 tooyour 行動後端 URL 物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="45b21-144">如果您使用 Azure App Service toohost 行動後端，請確定您使用安全的 hello `https://` hello URL 的版本。</span><span class="sxs-lookup"><span data-stu-id="45b21-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="45b21-145">hello 用戶端也需要存取 toohello 活動或內容-hello `this` hello 範例中的參數。</span><span class="sxs-lookup"><span data-stu-id="45b21-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="45b21-146">hello MobileServiceClient 建構應該會在 hello 內`onCreate()`方法中 hello 參考活動的 hello`AndroidManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="45b21-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="45b21-147">最佳做法是，您應該將伺服器通訊擷取到它自己的 (單一模式) 類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="45b21-148">在此情況下，您應該傳遞 hello 活動內 hello 建構函式 tooappropriately hello 服務設定。</span><span class="sxs-lookup"><span data-stu-id="45b21-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="45b21-149">例如：</span><span class="sxs-lookup"><span data-stu-id="45b21-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="45b21-150">您現在可以呼叫`AzureServiceAdapter.Initialize(this);`在 hello`onCreate()`主要活動的方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="45b21-151">需要存取 toohello 用戶端的其他方法使用`AzureServiceAdapter.getInstance();`tooobtain 參考 toohello service 配接器。</span><span class="sxs-lookup"><span data-stu-id="45b21-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="45b21-152">資料作業</span><span class="sxs-lookup"><span data-stu-id="45b21-152">Data Operations</span></span>

<span data-ttu-id="45b21-153">hello Azure 行動應用程式 SDK 的 hello 核心是 tooprovide 存取 toodata hello 行動裝置應用程式後端儲存在 SQL Azure。</span><span class="sxs-lookup"><span data-stu-id="45b21-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="45b21-154">您可以使用強型別類型 (建議選項) 或不具類型的查詢 (不建議) 來存取此資料。</span><span class="sxs-lookup"><span data-stu-id="45b21-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="45b21-155">hello 大量本節說明如何使用強型別的類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="45b21-156">定義用戶端資料類別</span><span class="sxs-lookup"><span data-stu-id="45b21-156">Define client data classes</span></span>

<span data-ttu-id="45b21-157">tooaccess SQL Azure 資料表資料，定義對應 toohello 資料表 hello 行動裝置應用程式後端中的用戶端資料類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="45b21-158">本主題中的範例假設名為的資料表**MyDataTable**，其中包含下列資料行的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="45b21-159">id</span><span class="sxs-lookup"><span data-stu-id="45b21-159">id</span></span>
* <span data-ttu-id="45b21-160">text</span><span class="sxs-lookup"><span data-stu-id="45b21-160">text</span></span>
* <span data-ttu-id="45b21-161">完成</span><span class="sxs-lookup"><span data-stu-id="45b21-161">complete</span></span>

<span data-ttu-id="45b21-162">hello 對應的型別的用戶端物件位於檔案呼叫**MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="45b21-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="45b21-163">針對您新增的每個欄位，新增 getter 和 setter 方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="45b21-164">如果您的 SQL Azure 資料表包含多個資料行，您將加入 hello 對應欄位 toothis 類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="45b21-165">例如，如果 hello DTO （資料傳輸物件） 具有整數優先順序資料行，則您可能會加入這個欄位，以及其 getter 和 setter 方法：</span><span class="sxs-lookup"><span data-stu-id="45b21-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="45b21-166">如何 toocreate 其他資料表中您的行動應用程式後端，請參閱的 toolearn[如何： 定義資料表控制器][ 15] （.NET 後端） 或[使用動態結構描述定義資料表][ 16] （Node.js 後端）。</span><span class="sxs-lookup"><span data-stu-id="45b21-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="45b21-167">Azure 行動應用程式後端資料表定義五個特殊欄位，其中四個為可用 tooclients:</span><span class="sxs-lookup"><span data-stu-id="45b21-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="45b21-168">`String id`: hello hello 記錄的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="45b21-169">最佳做法，請 hello 識別碼 hello 字串表示法[UUID] [ 17]物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="45b21-170">`DateTimeOffset updatedAt`: hello 的 hello 上次更新日期/時間。</span><span class="sxs-lookup"><span data-stu-id="45b21-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="45b21-171">hello updatedAt 欄位由 hello 伺服器設定，且不能設定您的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="45b21-172">`DateTimeOffset createdAt`: hello 日期/時間建立該 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="45b21-173">hello createdAt 欄位由 hello 伺服器設定，且不能設定您的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="45b21-174">`byte[] version`： 通常表示為字串，hello 版本也會設定 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="45b21-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="45b21-175">`boolean deleted`： 表示 hello 記錄已刪除但未清除尚未。</span><span class="sxs-lookup"><span data-stu-id="45b21-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="45b21-176">請勿使用 `deleted` 作為您類別中的屬性。</span><span class="sxs-lookup"><span data-stu-id="45b21-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="45b21-177">hello`id`是必填欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-177">hello `id` field is required.</span></span>  <span data-ttu-id="45b21-178">hello`updatedAt`欄位和`version`欄位可用來離線同步處理 (如增量同步處理和衝突解決方式分別)。</span><span class="sxs-lookup"><span data-stu-id="45b21-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="45b21-179">hello`createdAt`欄位是參考欄位，而不是由 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="45b21-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="45b21-180">hello 名稱是"跨線上"hello 屬性名稱，且不是可調整。</span><span class="sxs-lookup"><span data-stu-id="45b21-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="45b21-181">不過，您可以建立您的物件與 hello 之間的對應 」 跨網路 」 名稱使用 hello [gson] [ 3]程式庫。</span><span class="sxs-lookup"><span data-stu-id="45b21-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="45b21-182">例如：</span><span class="sxs-lookup"><span data-stu-id="45b21-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="45b21-183">建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="45b21-183">Create a Table Reference</span></span>

<span data-ttu-id="45b21-184">tooaccess 資料表時，第一次建立[MobileServiceTable] [ 8]物件呼叫 hello **getTable**方法上 hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="45b21-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="45b21-185">此方法有兩個多載：</span><span class="sxs-lookup"><span data-stu-id="45b21-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="45b21-186">在下列程式碼中，hello **m**是參考 tooyour MobileServiceClient 物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="45b21-187">hello 第一個多載會使用其中 hello 類別名稱和 hello 資料表名稱是 hello 相同，而且會 hello 其中一個用於 hello 快速入門：</span><span class="sxs-lookup"><span data-stu-id="45b21-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="45b21-188">hello 第二個多載時，會使用 hello 資料表名稱是 hello 類別名稱不同： hello 第一個參數是 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="45b21-189"><a name="query"></a>查詢後端資料表</span><span class="sxs-lookup"><span data-stu-id="45b21-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="45b21-190">首先，取得資料表參考。</span><span class="sxs-lookup"><span data-stu-id="45b21-190">First, obtain a table reference.</span></span>  <span data-ttu-id="45b21-191">在 hello 資料表參考，然後執行查詢。</span><span class="sxs-lookup"><span data-stu-id="45b21-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="45b21-192">查詢是以下的任何組合︰</span><span class="sxs-lookup"><span data-stu-id="45b21-192">A query is any combination of:</span></span>

* <span data-ttu-id="45b21-193">`.where()` [篩選子句](#filtering)。</span><span class="sxs-lookup"><span data-stu-id="45b21-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="45b21-194">`.orderBy()` [排序子句](#sorting)。</span><span class="sxs-lookup"><span data-stu-id="45b21-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="45b21-195">`.select()` [欄位選取子句](#selection)。</span><span class="sxs-lookup"><span data-stu-id="45b21-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="45b21-196">[分頁結果](#paging)的 `.skip()` 和 `.top()`。</span><span class="sxs-lookup"><span data-stu-id="45b21-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="45b21-197">hello 子句必須呈現在 hello 上述順序。</span><span class="sxs-lookup"><span data-stu-id="45b21-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="45b21-198"><a name="filter"></a> 篩選結果</span><span class="sxs-lookup"><span data-stu-id="45b21-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="45b21-199">hello 一般形式是查詢的：</span><span class="sxs-lookup"><span data-stu-id="45b21-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="45b21-200">hello 上述範例會傳回所有結果 （向上 toohello hello 伺服器所設定的最大頁面大小）。</span><span class="sxs-lookup"><span data-stu-id="45b21-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="45b21-201">hello `.execute()` hello 後端上執行 hello 查詢的方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="45b21-202">hello 查詢是轉換的 tooan [OData v3] [ 19]之前傳輸 toohello 行動應用程式後端的查詢。</span><span class="sxs-lookup"><span data-stu-id="45b21-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="45b21-203">在收到，hello 行動應用程式後端會將 hello 查詢轉換成 SQL 陳述式之前執行 hello SQL Azure 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="45b21-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="45b21-204">網路活動需要一些時間，因為 hello`.execute()`方法會傳回[ `ListenableFuture<E>` ] [ 18]。</span><span class="sxs-lookup"><span data-stu-id="45b21-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="45b21-205"><a name="filtering"></a>篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="45b21-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="45b21-206">hello 查詢執行之後傳回所有項目從 hello **ToDoItem**資料表**完成**等於**false**。</span><span class="sxs-lookup"><span data-stu-id="45b21-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="45b21-207">**mToDoTable** hello 參考 toohello 行動服務資料表我們先前所建立。</span><span class="sxs-lookup"><span data-stu-id="45b21-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="45b21-208">定義篩選條件使用 hello**其中**hello 資料表參考上的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="45b21-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="45b21-209">hello**其中**方法後面**欄位**方法，然後指定 hello 邏輯述詞的方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="45b21-210">可能的述詞方法包括 **eq** (等於)、**ne** (不等於)、**gt** (大於)、**ge** (大於或等於)、**lt** (小於)、**le** (小於或等於)。</span><span class="sxs-lookup"><span data-stu-id="45b21-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="45b21-211">這些方法可讓您比較數字和字串 toospecific 值欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="45b21-212">您可以依日期進行篩選。</span><span class="sxs-lookup"><span data-stu-id="45b21-212">You can filter on dates.</span></span> <span data-ttu-id="45b21-213">hello 下列方法可讓您比較 hello 整個日期欄位或 hello 日期部分：**年**，**月份**，**天**，**小時**， **分鐘**，和**第二個**。</span><span class="sxs-lookup"><span data-stu-id="45b21-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="45b21-214">hello 下列範例會將篩選條件的項目其*到期日*等於 2013年。</span><span class="sxs-lookup"><span data-stu-id="45b21-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="45b21-215">hello 下列方法支援更複雜的篩選字串欄位： **startsWith**， **endsWith**， **concat**， **subString**， **indexOf**，**取代**， **toLower**， **toUpper**，**修剪**，和**長度**。</span><span class="sxs-lookup"><span data-stu-id="45b21-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="45b21-216">下列範例會篩選的資料表資料列，其中 hello hello*文字*資料行開頭為"PRI0。 」</span><span class="sxs-lookup"><span data-stu-id="45b21-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="45b21-217">數字欄位支援下列運算子方法的 hello:**新增**， **sub**， **mul**， **div**， **mod**， **floor**， **ceiling**，和**捨入**。</span><span class="sxs-lookup"><span data-stu-id="45b21-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="45b21-218">下列範例會篩選的資料表資料列，其中 hello hello**持續時間**是偶數。</span><span class="sxs-lookup"><span data-stu-id="45b21-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="45b21-219">您可以結合述詞與下列邏輯方法：**and**、**or** 和 **not**。</span><span class="sxs-lookup"><span data-stu-id="45b21-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="45b21-220">hello 下列範例會結合兩個 hello 前面範例。</span><span class="sxs-lookup"><span data-stu-id="45b21-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="45b21-221">群組和巢狀邏輯運算子︰</span><span class="sxs-lookup"><span data-stu-id="45b21-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="45b21-222">如需詳細討論和篩選的範例，請參閱[瀏覽的 hello Android 用戶端查詢模型的 hello 豐富][20]。</span><span class="sxs-lookup"><span data-stu-id="45b21-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="45b21-223"><a name="sorting"></a>排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="45b21-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="45b21-224">hello 下列程式碼的所有項目從資料表傳回的**ToDoItems**排序按遞增 hello*文字*欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="45b21-225">*mToDoTable*是 hello 參考 toohello 後端的資料表，您先前建立：</span><span class="sxs-lookup"><span data-stu-id="45b21-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="45b21-226">hello 第一個參數的 hello **orderBy**方法是在哪個 toosort hello 欄位的字串相等 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="45b21-227">hello 第二個參數使用 hello **QueryOrder**列舉 toospecify 是否 toosort 遞增或遞減。</span><span class="sxs-lookup"><span data-stu-id="45b21-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="45b21-228">如果要篩選使用 hello***其中***方法、 hello***其中***必須叫用方法之前 hello ***orderBy***方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="45b21-229"><a name="selection"></a>選取特定資料行</span><span class="sxs-lookup"><span data-stu-id="45b21-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="45b21-230">hello 下列程式碼說明 tooreturn 所有的資料表中的項目**ToDoItems**，但只會顯示 hello**完成**和**文字**欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="45b21-231">**mToDoTable**是 hello 參考 toohello 後端的資料表，我們在先前所建立。</span><span class="sxs-lookup"><span data-stu-id="45b21-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="45b21-232">hello 參數 toohello 選取函式是您想 tooreturn hello 資料表的資料行 hello 字串名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="45b21-233">hello**選取**方法需要等 toofollow 方法**其中**和**orderBy**。</span><span class="sxs-lookup"><span data-stu-id="45b21-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="45b21-234">而其後可以跟隨 **skip** 和 **top** 之類的分頁方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="45b21-235"><a name="paging"></a>以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="45b21-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="45b21-236">資料**一律**以分頁方式傳回。</span><span class="sxs-lookup"><span data-stu-id="45b21-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="45b21-237">hello 傳回記錄的數目上限是由 hello 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="45b21-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="45b21-238">如果 hello 用戶端要求更多記錄，hello 伺服器就會傳回 hello 的記錄數目上限。</span><span class="sxs-lookup"><span data-stu-id="45b21-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="45b21-239">根據預設，hello hello 伺服器上的最大頁面大小是 50 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="45b21-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="45b21-240">hello 第一個範例顯示如何 tooselect hello 從資料表的前五個項目。</span><span class="sxs-lookup"><span data-stu-id="45b21-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="45b21-241">hello 查詢傳回的資料表中的 hello 項目**ToDoItems**。</span><span class="sxs-lookup"><span data-stu-id="45b21-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="45b21-242">**mToDoTable**是 hello 參考 toohello 後端的資料表，您先前建立：</span><span class="sxs-lookup"><span data-stu-id="45b21-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="45b21-243">以下是查詢，便可略過 hello 前五個項目，然後傳回 hello 下一步的五個：</span><span class="sxs-lookup"><span data-stu-id="45b21-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="45b21-244">如果您想 tooget 所有記錄資料表中，實作程式碼 tooiterate 所有頁面上：</span><span class="sxs-lookup"><span data-stu-id="45b21-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="45b21-245">使用此方法的所有記錄的要求會建立兩個要求 toohello 行動應用程式後端的最小值。</span><span class="sxs-lookup"><span data-stu-id="45b21-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="45b21-246">選擇的 hello 正確的頁面大小為而發生 hello 要求的記憶體使用量、 頻寬使用量和延遲完全收到 hello 資料之間的平衡。</span><span class="sxs-lookup"><span data-stu-id="45b21-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="45b21-247">hello 預設 （50 筆記錄） 是適用於所有裝置。</span><span class="sxs-lookup"><span data-stu-id="45b21-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="45b21-248">如果您以獨佔方式在較大的記憶體裝置上運作，增加 too500 組成。</span><span class="sxs-lookup"><span data-stu-id="45b21-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="45b21-249">我們無法接受的延遲和大量記憶體的問題中發現該 hello 頁面大小增加超過 500 筆記錄的結果。</span><span class="sxs-lookup"><span data-stu-id="45b21-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="45b21-250"><a name="chaining"></a>作法：串連查詢方法</span><span class="sxs-lookup"><span data-stu-id="45b21-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="45b21-251">可以串連 hello 方法用於查詢後端的資料表。</span><span class="sxs-lookup"><span data-stu-id="45b21-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="45b21-252">方法可讓您 tooselect 特定資料行的排序和分頁的已篩選資料列鏈結的查詢。</span><span class="sxs-lookup"><span data-stu-id="45b21-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="45b21-253">您可以建立複雜的邏輯篩選器。</span><span class="sxs-lookup"><span data-stu-id="45b21-253">You can create complex logical filters.</span></span>  <span data-ttu-id="45b21-254">每個查詢方法都會傳回 Query 物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-254">Each query method returns a Query object.</span></span> <span data-ttu-id="45b21-255">tooend hello 系列的方法和實際執行的 hello 查詢中，呼叫 hello**執行**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="45b21-256">例如：</span><span class="sxs-lookup"><span data-stu-id="45b21-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="45b21-257">hello 鏈結的查詢的方法都必須排序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b21-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="45b21-258">篩選 (**where**) 方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="45b21-259">排序 (**orderBy**) 方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="45b21-260">選取 (**select**) 方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="45b21-261">分頁 (**skip** 和 **top**) 方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="45b21-262"><a name="binding"></a>繫結資料 toohello 使用者介面</span><span class="sxs-lookup"><span data-stu-id="45b21-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="45b21-263">資料繫結牽涉到三項要件：</span><span class="sxs-lookup"><span data-stu-id="45b21-263">Data binding involves three components:</span></span>

* <span data-ttu-id="45b21-264">hello 資料來源</span><span class="sxs-lookup"><span data-stu-id="45b21-264">hello data source</span></span>
* <span data-ttu-id="45b21-265">hello 螢幕的配置</span><span class="sxs-lookup"><span data-stu-id="45b21-265">hello screen layout</span></span>
* <span data-ttu-id="45b21-266">hello 配接器，繫結 hello 兩個在一起。</span><span class="sxs-lookup"><span data-stu-id="45b21-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="45b21-267">在我們的範例程式碼，傳回 hello 資料從 hello 行動應用程式的 SQL Azure 資料表**ToDoItem**到陣列。</span><span class="sxs-lookup"><span data-stu-id="45b21-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="45b21-268">此活動是常見的資料應用模式。</span><span class="sxs-lookup"><span data-stu-id="45b21-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="45b21-269">資料庫查詢通常會傳回 hello 清單或陣列中的用戶端取得的資料列集合。</span><span class="sxs-lookup"><span data-stu-id="45b21-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="45b21-270">在此範例中，hello 陣列會是 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="45b21-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="45b21-271">hello 程式碼會指定定義 hello 裝置出現的 hello 資料 hello 檢視畫面配置。</span><span class="sxs-lookup"><span data-stu-id="45b21-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="45b21-272">hello 兩個繫結以及配接器，它在這段程式碼中的 hello 延伸**ArrayAdapter&lt;ToDoItem&gt;** 類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="45b21-273"><a name="layout"></a>定義 hello 版面配置</span><span class="sxs-lookup"><span data-stu-id="45b21-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="45b21-274">hello 版面配置是由數個 XML 程式碼片段定義。</span><span class="sxs-lookup"><span data-stu-id="45b21-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="45b21-275">指定現有的版面配置，下列程式碼的 hello 代表 hello **ListView**我們想 toopopulate 我們的伺服器資料。</span><span class="sxs-lookup"><span data-stu-id="45b21-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="45b21-276">在上述程式碼的 hello，hello *listitem*屬性指定的個別資料列的 hello 配置 hello 識別碼 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="45b21-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="45b21-277">此程式碼指定核取方塊和相關聯的文字，並取得具現化一次的 hello 清單中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="45b21-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="45b21-278">這種配置不會顯示 hello**識別碼**欄位，以及更複雜的配置會顯示 hello 中指定的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="45b21-279">此程式碼是在 hello **row_list_to_do.xml**檔案。</span><span class="sxs-lookup"><span data-stu-id="45b21-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="45b21-280"><a name="adapter"></a>定義 hello 配接器</span><span class="sxs-lookup"><span data-stu-id="45b21-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="45b21-281">因為我們檢視 hello 資料來源是陣列**ToDoItem**，我們子類別我們配接器從**ArrayAdapter&lt;ToDoItem&gt;** 類別。</span><span class="sxs-lookup"><span data-stu-id="45b21-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="45b21-282">這個子類別會產生一份檢視的每個**ToDoItem**使用 hello **row_list_to_do**版面配置。</span><span class="sxs-lookup"><span data-stu-id="45b21-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="45b21-283">在我們的程式碼中，我們會定義 hello 遵循 hello 的延伸模組類別**ArrayAdapter&lt;E&gt;** 類別：</span><span class="sxs-lookup"><span data-stu-id="45b21-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="45b21-284">覆寫 hello 配接器**getView**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="45b21-285">例如：</span><span class="sxs-lookup"><span data-stu-id="45b21-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="45b21-286">我們在「活動」中建立此類別的執行個體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b21-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="45b21-287">hello 第二個參數 toohello ToDoItemAdapter 建構函式會參考 toohello 版面配置。</span><span class="sxs-lookup"><span data-stu-id="45b21-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="45b21-288">我們現在可以執行個體化 hello **ListView**並指派 hello 配接器 toohello **ListView**。</span><span class="sxs-lookup"><span data-stu-id="45b21-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="45b21-289"><a name="use-adapter"></a>使用 hello 配接器 tooBind toohello UI</span><span class="sxs-lookup"><span data-stu-id="45b21-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="45b21-290">現在您已經準備就緒 toouse 資料繫結。</span><span class="sxs-lookup"><span data-stu-id="45b21-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="45b21-291">hello 下列程式碼顯示以 hello 資料表和填滿 tooget 項目如何 hello 本機介面卡以 hello 傳回項目。</span><span class="sxs-lookup"><span data-stu-id="45b21-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="45b21-292">呼叫 hello 配接器在任何時間修改 hello **ToDoItem**資料表。</span><span class="sxs-lookup"><span data-stu-id="45b21-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="45b21-293">修改是對個別記錄逐一執行的，因此您會處理單一資料列，而不是集合。</span><span class="sxs-lookup"><span data-stu-id="45b21-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="45b21-294">當您插入項目時，呼叫 hello**新增**方法 hello 配接器，則刪除時，呼叫 hello**移除**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="45b21-295">您可以在 hello 找到完整的範例[Android 快速入門專案][21]。</span><span class="sxs-lookup"><span data-stu-id="45b21-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="45b21-296"><a name="inserting"></a>將資料插入 hello 後端</span><span class="sxs-lookup"><span data-stu-id="45b21-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="45b21-297">具現化執行個體的 hello *ToDoItem*類別，並設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="45b21-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="45b21-298">然後使用**insert** tooinsert 物件：</span><span class="sxs-lookup"><span data-stu-id="45b21-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="45b21-299">hello 傳回實體的相符項目插入至 hello 後端的資料表、 包含的 hello 識別碼和任何其他值的 hello 資料 (例如 hello `createdAt`， `updatedAt`，和`version`欄位) 上 hello 後端設定。</span><span class="sxs-lookup"><span data-stu-id="45b21-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="45b21-300">Mobile Apps 資料表需要名為 **識別碼**的主索引鍵資料行。此資料行必須是字串。</span><span class="sxs-lookup"><span data-stu-id="45b21-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="45b21-301">hello hello ID 資料行的預設值是 GUID。</span><span class="sxs-lookup"><span data-stu-id="45b21-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="45b21-302">您可以提供其他的唯一值，例如電子郵件地址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="45b21-303">當字串 ID 值未提供插入的記錄時，hello 後端會產生新的 GUID。</span><span class="sxs-lookup"><span data-stu-id="45b21-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="45b21-304">字串 ID 值會提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="45b21-305">可以產生識別碼，而不需要進行往返 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="45b21-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="45b21-306">更容易 toomerge 來自不同資料表或資料庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="45b21-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="45b21-307">識別碼值與應用程式邏輯的整合更理想。</span><span class="sxs-lookup"><span data-stu-id="45b21-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="45b21-308">若要支援離線同步處理，則 **需要** 字串識別碼值。</span><span class="sxs-lookup"><span data-stu-id="45b21-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="45b21-309">一旦儲存 hello 後端資料庫中，您無法變更 Id。</span><span class="sxs-lookup"><span data-stu-id="45b21-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="45b21-310"><a name="updating"></a>將行動裝置應用程式中的資料更新</span><span class="sxs-lookup"><span data-stu-id="45b21-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="45b21-311">tooupdate 資料在資料表中，將新物件 toohello hello **update （)**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="45b21-312">在此範例中，*項目*hello 一個參考 tooa 資料列*ToDoItem*有了一些變更 tooit 的資料表。</span><span class="sxs-lookup"><span data-stu-id="45b21-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="45b21-313">hello 資料列以 hello 相同**識別碼**會更新。</span><span class="sxs-lookup"><span data-stu-id="45b21-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="45b21-314"><a name="deleting"></a>將行動裝置應用程式中的資料刪除</span><span class="sxs-lookup"><span data-stu-id="45b21-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="45b21-315">hello，下列程式碼顯示如何藉由指定資料表的資料 toodelete hello 資料物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="45b21-316">您也可以刪除項目，藉由指定 hello**識別碼**hello 列 toodelete 欄位。</span><span class="sxs-lookup"><span data-stu-id="45b21-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="45b21-317"><a name="lookup"></a>依識別碼查閱特定項目</span><span class="sxs-lookup"><span data-stu-id="45b21-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="45b21-318">尋找具有特定的項目**識別碼**欄位以 hello **Lookup**方法：</span><span class="sxs-lookup"><span data-stu-id="45b21-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="45b21-319"><a name="untyped"></a>作法：使用不具類型的資料</span><span class="sxs-lookup"><span data-stu-id="45b21-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="45b21-320">hello 不具類型的程式設計模型可讓您完全控制 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="45b21-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="45b21-321">有一些常見的案例，您可能希望 toouse 不具類型的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="45b21-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="45b21-322">例如，如果您的後端資料表包含許多資料行，而且您只需要 tooreference hello 資料行的子集。</span><span class="sxs-lookup"><span data-stu-id="45b21-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="45b21-323">hello 具類型的模型需要的 toodefine hello 的所有資料行定義中的資料類別中的 hello 行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="45b21-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="45b21-324">大部分的應用程式開發介面呼叫，以存取資料的 hello 如下 toohello 輸入程式設計的呼叫。</span><span class="sxs-lookup"><span data-stu-id="45b21-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="45b21-325">hello 主要差異在於，hello 不具類型的模型中您可以叫用方法上 hello **MobileServiceJsonTable**物件，而不是 hello **MobileServiceTable**物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="45b21-326"><a name="json_instance"></a>建立不具型別的資料表執行個體</span><span class="sxs-lookup"><span data-stu-id="45b21-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="45b21-327">類似 toohello 具類型的模型，您一開始會取得資料表參考，但它是在此情況下**MobileServicesJsonTable**物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="45b21-328">取得呼叫 hello hello 參考**getTable** hello 用戶端的執行個體上的方法：</span><span class="sxs-lookup"><span data-stu-id="45b21-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="45b21-329">一旦您建立執行個體的 hello **MobileServiceJsonTable**，它具有幾乎 hello hello 具類型的程式撰寫模型做為可用的相同 API。</span><span class="sxs-lookup"><span data-stu-id="45b21-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="45b21-330">在某些情況下，hello 方法會採用不具類型的參數，而不是具類型的參數。</span><span class="sxs-lookup"><span data-stu-id="45b21-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="45b21-331"><a name="json_insert"></a>插入不具型別的資料表中</span><span class="sxs-lookup"><span data-stu-id="45b21-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="45b21-332">hello 下列程式碼會示範如何 toodo 插入。</span><span class="sxs-lookup"><span data-stu-id="45b21-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="45b21-333">hello 第一個步驟是 toocreate [JsonObject][1]，屬於 hello [gson] [ 3]程式庫。</span><span class="sxs-lookup"><span data-stu-id="45b21-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="45b21-334">然後，使用**insert** hello 資料表 tooinsert hello 不具型別的的物件。</span><span class="sxs-lookup"><span data-stu-id="45b21-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="45b21-335">如果您需要 tooget hello 識別碼 hello 插入物件，使用 hello **getAsJsonPrimitive()**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="45b21-336"><a name="json_delete"></a>在不具型別的資料表中進行刪除</span><span class="sxs-lookup"><span data-stu-id="45b21-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="45b21-337">hello 下列程式碼會示範如何 toodelete 執行個體，在此情況下，hello 相同的執行個體**JsonObject**中 hello 之前建立*插入*範例。</span><span class="sxs-lookup"><span data-stu-id="45b21-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="45b21-338">hello 程式碼為 hello hello 與輸入案例中，但 hello 方法具有不同的簽章，因為它會參考**JsonObject**。</span><span class="sxs-lookup"><span data-stu-id="45b21-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="45b21-339">您也可以直接使用 ID 來刪除執行個體：</span><span class="sxs-lookup"><span data-stu-id="45b21-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="45b21-340"><a name="json_get"></a>從不具型別的資料表傳回所有資料列</span><span class="sxs-lookup"><span data-stu-id="45b21-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="45b21-341">hello 下列程式碼會示範如何 tooretrieve 整個資料表。</span><span class="sxs-lookup"><span data-stu-id="45b21-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="45b21-342">因為您使用 JSON 資料表，您可以選擇性地擷取只有部分 hello 資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="45b21-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="45b21-343">hello 組相同的篩選、 篩選和分頁可用於 hello 具型別模型的方法可供 hello 不具類型的模型。</span><span class="sxs-lookup"><span data-stu-id="45b21-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="45b21-344"><a name="offline-sync"></a>實作離線同步處理</span><span class="sxs-lookup"><span data-stu-id="45b21-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="45b21-345">hello Azure 行動應用程式用戶端 SDK 也會實作離線的資料同步處理本機使用 SQLite 資料庫 toostore hello 伺服器資料的複本。</span><span class="sxs-lookup"><span data-stu-id="45b21-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="45b21-346">離線的資料表上執行的作業不需要行動裝置的連線能力 toowork。</span><span class="sxs-lookup"><span data-stu-id="45b21-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="45b21-347">離線同步處理有助於彈性且更複雜的邏輯解決衝突的 hello 費用的效能。</span><span class="sxs-lookup"><span data-stu-id="45b21-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="45b21-348">hello Azure 行動應用程式用戶端 SDK 實作 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="45b21-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="45b21-349">增量同步處理︰只會下載更新和新的記錄，可節省頻寬和記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="45b21-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="45b21-350">開放式並行存取： 作業會假設 toosucceed。</span><span class="sxs-lookup"><span data-stu-id="45b21-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="45b21-351">衝突解決會延遲，直到 hello 伺服器上執行更新。</span><span class="sxs-lookup"><span data-stu-id="45b21-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="45b21-352">衝突解決方式： hello SDK 偵測到衝突的變更已在 hello 伺服器，並提供勾點 tooalert hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="45b21-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="45b21-353">虛刪除： 已刪除的記錄會標示為已刪除，讓其他裝置 tooupdate 其離線快取的。</span><span class="sxs-lookup"><span data-stu-id="45b21-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="45b21-354">將離線同步處理初始化</span><span class="sxs-lookup"><span data-stu-id="45b21-354">Initialize Offline Sync</span></span>

<span data-ttu-id="45b21-355">每個離線的資料表必須定義在 hello 離線快取，才能使用。</span><span class="sxs-lookup"><span data-stu-id="45b21-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="45b21-356">一般而言，資料表定義是在 hello 用戶端 hello 建立後立即完成：</span><span class="sxs-lookup"><span data-stu-id="45b21-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="45b21-357">取得參考 toohello 離線快取表格</span><span class="sxs-lookup"><span data-stu-id="45b21-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="45b21-358">如需線上資料表，請使用 `.getTable()`。</span><span class="sxs-lookup"><span data-stu-id="45b21-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="45b21-359">如需離線資料表，請使用 `.getSyncTable()`：</span><span class="sxs-lookup"><span data-stu-id="45b21-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="45b21-360">所有 hello 可用方法的平均工作 （包括篩選、 排序、 分頁、 將資料插入、 更新資料，和刪除資料） 的線上資料表在線上或離線的資料表。</span><span class="sxs-lookup"><span data-stu-id="45b21-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="45b21-361">同步處理 hello 本機離線快取</span><span class="sxs-lookup"><span data-stu-id="45b21-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="45b21-362">同步處理是您的應用程式的 hello 控制項內。</span><span class="sxs-lookup"><span data-stu-id="45b21-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="45b21-363">以下是同步處理方法的範例︰</span><span class="sxs-lookup"><span data-stu-id="45b21-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="45b21-364">如果有提供查詢名稱 toohello`.pull(query, queryname)`方法，則增量同步處理是使用的 tooreturn 只記錄已建立或最後一次順利完成的 hello 提取之後變更。</span><span class="sxs-lookup"><span data-stu-id="45b21-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="45b21-365">處理離線同步處理期間的衝突</span><span class="sxs-lookup"><span data-stu-id="45b21-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="45b21-366">如果在 `.push()` 作業期間發生衝突，就會擲回 `MobileServiceConflictException`。</span><span class="sxs-lookup"><span data-stu-id="45b21-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="45b21-367">hello 伺服器所發行的項目內嵌在 hello 例外狀況，而且可以藉由擷取`.getItem()`hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="45b21-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="45b21-368">調整 hello 推入，由下列項目 hello MobileServiceSyncContext 物件上呼叫 hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="45b21-369">在您希望的位置，有標示為所有衝突之後, 再呼叫`.push()`再次 tooresolve 所有 hello 衝突。</span><span class="sxs-lookup"><span data-stu-id="45b21-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="45b21-370"><a name="custom-api"></a>呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="45b21-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="45b21-371">自訂 API 可讓您 toodefine 自訂端點來公開伺服器功能並不對應 tooan 插入、 更新、 刪除或讀取作業。</span><span class="sxs-lookup"><span data-stu-id="45b21-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="45b21-372">透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。</span><span class="sxs-lookup"><span data-stu-id="45b21-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="45b21-373">從 Android 用戶端，您可以呼叫 hello **invokeApi**方法 toocall hello 自訂 API 端點。</span><span class="sxs-lookup"><span data-stu-id="45b21-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="45b21-374">hello 下列範例示範如何 toocall API 端點命名**completeAll**，它會傳回名為的集合類別**MarkAllResult**。</span><span class="sxs-lookup"><span data-stu-id="45b21-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="45b21-375">hello **invokeApi** hello 用戶端，傳送 POST 要求 toohello 新的自訂 API 上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="45b21-376">hello hello 自訂 API 所傳回的結果會顯示在訊息對話方塊中中,，為任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="45b21-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="45b21-377">其他版本的**invokeApi**可讓您選擇性地傳送 hello 要求主體中的物件，指定 hello HTTP 方法，並傳送 hello 要求與查詢參數。</span><span class="sxs-lookup"><span data-stu-id="45b21-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="45b21-378">也會提供不具型別的版本 **invokeApi** 。</span><span class="sxs-lookup"><span data-stu-id="45b21-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="45b21-379"><a name="authentication"></a>新增驗證 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="45b21-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="45b21-380">詳細的教學課程已說明如何 tooadd 這些功能。</span><span class="sxs-lookup"><span data-stu-id="45b21-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="45b21-381">App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory) 來 [驗證應用程式使用者](app-service-mobile-android-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="45b21-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="45b21-382">您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="45b21-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="45b21-383">您也可以使用 hello 身分識別通過驗證的使用者 tooimplement 授權規則的後端中。</span><span class="sxs-lookup"><span data-stu-id="45b21-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="45b21-384">支援兩個驗證流程：**伺服器**流程和**用戶端**流程。</span><span class="sxs-lookup"><span data-stu-id="45b21-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="45b21-385">hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 身分識別提供者 web 介面。</span><span class="sxs-lookup"><span data-stu-id="45b21-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="45b21-386">沒有其他 Sdk 是必要的 tooimplement 伺服器流程驗證。</span><span class="sxs-lookup"><span data-stu-id="45b21-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="45b21-387">伺服器流程驗證不會提供深層整合 hello 行動裝置，且只建議證明的情況。</span><span class="sxs-lookup"><span data-stu-id="45b21-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="45b21-388">因為它是倚賴 hello 身分識別提供者所提供的 Sdk hello 用戶端流程能裝置特定功能，例如單一登入的整合更加深入。</span><span class="sxs-lookup"><span data-stu-id="45b21-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="45b21-389">例如，您可以將 hello Facebook SDK 整合行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="45b21-390">hello 行動用戶端交換到 hello Facebook 應用程式，並確認您登入前交換後 tooyour 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="45b21-391">四個步驟是在您的應用程式的必要的 tooenable 驗證：</span><span class="sxs-lookup"><span data-stu-id="45b21-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="45b21-392">對識別提供者註冊應用程式以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="45b21-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="45b21-393">設定 App Service 後端。</span><span class="sxs-lookup"><span data-stu-id="45b21-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="45b21-394">限制只在 hello 應用程式服務後端的資料表權限 tooauthenticated 使用者存取。</span><span class="sxs-lookup"><span data-stu-id="45b21-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="45b21-395">加入驗證程式碼 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="45b21-396">您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="45b21-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="45b21-397">您也可以使用 hello 的已驗證的使用者 toomodify SID 的要求。</span><span class="sxs-lookup"><span data-stu-id="45b21-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="45b21-398">如需詳細資訊，請檢閱[開始使用驗證]和 hello 伺服器 SDK 如何文件。</span><span class="sxs-lookup"><span data-stu-id="45b21-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="45b21-399"><a name="caching"></a>驗證︰伺服器流程</span><span class="sxs-lookup"><span data-stu-id="45b21-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="45b21-400">hello 下列程式碼會啟動使用 hello Google 提供者伺服器流程登入程序。</span><span class="sxs-lookup"><span data-stu-id="45b21-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="45b21-401">因為 hello hello Google 提供者的安全性需求，則需要其他組態：</span><span class="sxs-lookup"><span data-stu-id="45b21-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="45b21-402">此外，新增下列方法 toohello 主要活動類別的 hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="45b21-403">hello`GOOGLE_LOGIN_REQUEST_CODE`定義您的 main 中活動用於 hello`login()`方法內 hello`onActivityResult()`方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="45b21-404">您可以選擇任何唯一的數字，只要 hello 使用相同的號碼 hello 內`login()`方法和 hello`onActivityResult()`方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="45b21-405">如果您的服務配接器 （如稍早所示） 到抽象 hello 用戶端程式碼，您應該 hello service 配接器上呼叫 hello 適當的方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="45b21-406">您也需 customtabs tooconfigure hello 專案。</span><span class="sxs-lookup"><span data-stu-id="45b21-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="45b21-407">先指定重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="45b21-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="45b21-408">新增下列程式碼片段太 hello`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="45b21-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="45b21-409">新增 hello **redirectUriScheme** toohello`build.gradle`應用程式的檔案：</span><span class="sxs-lookup"><span data-stu-id="45b21-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="45b21-410">最後，會加入`com.android.support:customtabs:23.0.1`toohello 依存性清單中 hello`build.gradle`檔案：</span><span class="sxs-lookup"><span data-stu-id="45b21-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="45b21-411">取得 hello 識別碼 hello 登入的使用者從**MobileServiceUser**使用 hello **getUserId**方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="45b21-412">如需 toouse 未來 toocall 如何 hello 非同步登入應用程式開發介面的範例，請參閱[開始使用驗證]。</span><span class="sxs-lookup"><span data-stu-id="45b21-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="45b21-413">hello 提及的 URL 配置是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="45b21-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="45b21-414">確認所有出現的 `{url_scheme_of_you_app}` 大小寫相符。</span><span class="sxs-lookup"><span data-stu-id="45b21-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="45b21-415"><a name="caching"></a>快取驗證權杖</span><span class="sxs-lookup"><span data-stu-id="45b21-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="45b21-416">快取驗證權杖會要求您 toostore hello 使用者識別碼和 hello 裝置本機上的驗證 token。</span><span class="sxs-lookup"><span data-stu-id="45b21-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="45b21-417">hello 下次 hello 應用程式啟動時，您檢查 hello 快取，和如果這些值都存在，則可以略過 hello 程序中的記錄檔，並解除凍結 hello 用戶端使用此資料。</span><span class="sxs-lookup"><span data-stu-id="45b21-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="45b21-418">不過這項資料是區分大小寫，而且應該儲存以防 hello 電話遭竊，安全的加密。</span><span class="sxs-lookup"><span data-stu-id="45b21-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="45b21-419">您可以看到 toocache 驗證中的語彙基元的完整範例[快取驗證權杖 區段][7]。</span><span class="sxs-lookup"><span data-stu-id="45b21-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="45b21-420">當您嘗試 toouse 過期的權杖時，您會收到*401 未經授權的*回應。</span><span class="sxs-lookup"><span data-stu-id="45b21-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="45b21-421">您可以使用篩選器處理驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="45b21-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="45b21-422">篩選條件攔截要求 toohello 應用程式服務後端。</span><span class="sxs-lookup"><span data-stu-id="45b21-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="45b21-423">hello 篩選程式碼測試 401 回應 hello、 觸發程序 hello 登入程序，然後會繼續產生 hello 401 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="45b21-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="45b21-424"><a name="refresh"></a>使用重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="45b21-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="45b21-425">傳回的 Azure 應用程式服務驗證和授權的 hello token 具有一小時已定義的存留時間。</span><span class="sxs-lookup"><span data-stu-id="45b21-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="45b21-426">在這段期間之後, 您必須重新驗證 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="45b21-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="45b21-427">如果您是使用長時間執行的語彙基元，您收到透過用戶端流程驗證，則您可以重新驗證與 Azure 應用程式服務驗證並授權使用 hello 相同的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="45b21-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="45b21-428">所產生的另一個 Azure App Service 權杖會含有新的存留期。</span><span class="sxs-lookup"><span data-stu-id="45b21-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="45b21-429">您也可以註冊 hello 提供者 toouse 重新整理語彙基元。</span><span class="sxs-lookup"><span data-stu-id="45b21-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="45b21-430">重新整理權杖並非一律可用。</span><span class="sxs-lookup"><span data-stu-id="45b21-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="45b21-431">需要進行其他設定：</span><span class="sxs-lookup"><span data-stu-id="45b21-431">Additional configuration is required:</span></span>

* <span data-ttu-id="45b21-432">如**Azure Active Directory**，設定 hello Azure Active Directory 應用程式的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="45b21-433">設定 Azure Active Directory 驗證時，請指定 hello Azure App Service 中的 hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="45b21-434">呼叫 `.login()` 時，傳遞 `response_type=code id_token` 作為參數︰</span><span class="sxs-lookup"><span data-stu-id="45b21-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="45b21-435">如**Google**，傳遞 hello`access_type=offline`做為參數：</span><span class="sxs-lookup"><span data-stu-id="45b21-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="45b21-436">如**Microsoft 帳戶**，選取 hello`wl.offline_access`範圍。</span><span class="sxs-lookup"><span data-stu-id="45b21-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="45b21-437">toorefresh 語彙基元，呼叫`.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="45b21-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="45b21-438">最佳作法是建立的篩選條件會偵測 hello 伺服器 401 回應，並嘗試 toorefresh hello 使用者 token。</span><span class="sxs-lookup"><span data-stu-id="45b21-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="45b21-439">使用用戶端流程驗證登入</span><span class="sxs-lookup"><span data-stu-id="45b21-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="45b21-440">hello 登入用戶端流量驗證的一般程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b21-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="45b21-441">以您設定伺服器流程驗證的相同方式設定 Azure App Service 驗證與授權。</span><span class="sxs-lookup"><span data-stu-id="45b21-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="45b21-442">整合 hello 驗證提供者 SDK 驗證 tooproduce 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="45b21-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="45b21-443">呼叫 hello`.login()`方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b21-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="45b21-444">取代 hello`onSuccess()`方法的任何程式碼您希望 toouse 成功登入。</span><span class="sxs-lookup"><span data-stu-id="45b21-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="45b21-445">hello`{provider}`字串是有效的提供者： **aad** (Azure Active Directory)， **facebook**， **google**， **microsoftaccount**，或**twitter**。</span><span class="sxs-lookup"><span data-stu-id="45b21-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="45b21-446">如果您實作自訂驗證，您可以也使用 hello 自訂驗證提供者的標記。</span><span class="sxs-lookup"><span data-stu-id="45b21-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="45b21-447"><a name="adal"></a>驗證使用者以 hello Active Directory 驗證程式庫 (ADAL)</span><span class="sxs-lookup"><span data-stu-id="45b21-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="45b21-448">您可以使用 hello Active Directory 驗證程式庫 (ADAL) toosign 使用者將使用 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="45b21-449">使用用戶端流量登入通常是最好的 toousing hello`loginAsync()`方法，因為它提供更原生的 UX 操作，並允許其他自訂。</span><span class="sxs-lookup"><span data-stu-id="45b21-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="45b21-450">設定下列 hello AAD 登入您的行動裝置應用程式後端[tooconfigure Active Directory 登入服務的應用程式如何][ 22]教學課程。</span><span class="sxs-lookup"><span data-stu-id="45b21-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="45b21-451">請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="45b21-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="45b21-452">藉由修改下列定義您 build.gradle 檔案 tooinclude hello 安裝 ADAL:</span><span class="sxs-lookup"><span data-stu-id="45b21-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="45b21-453">加入下列程式碼 tooyour 應用程式，進行下列取代 hello hello:</span><span class="sxs-lookup"><span data-stu-id="45b21-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="45b21-454">取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="45b21-455">hello 格式應該是 https://login.microsoftonline.com/contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="45b21-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="45b21-456">取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="45b21-457">您可以從 hello 取得 hello 用戶端識別碼**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="45b21-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="45b21-458">取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="45b21-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="45b21-459">取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。</span><span class="sxs-lookup"><span data-stu-id="45b21-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="45b21-460">此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。</span><span class="sxs-lookup"><span data-stu-id="45b21-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="45b21-461"><a name="filters"></a>調整 hello 用戶端伺服器通訊</span><span class="sxs-lookup"><span data-stu-id="45b21-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="45b21-462">hello 用戶端連接通常是使用 hello 基礎 HTTP hello Android SDK 所提供的程式庫的基本 HTTP 連接。</span><span class="sxs-lookup"><span data-stu-id="45b21-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="45b21-463">有幾個原因為何，您會想 toochange 的：</span><span class="sxs-lookup"><span data-stu-id="45b21-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="45b21-464">您希望 toouse 替代 HTTP 程式庫 tooadjust 逾時。</span><span class="sxs-lookup"><span data-stu-id="45b21-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="45b21-465">您希望 tooprovide 進度列。</span><span class="sxs-lookup"><span data-stu-id="45b21-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="45b21-466">您希望 tooadd 自訂標頭 toosupport API 管理功能。</span><span class="sxs-lookup"><span data-stu-id="45b21-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="45b21-467">您希望 toointercept 失敗的回應，以便您可以實作重新驗證。</span><span class="sxs-lookup"><span data-stu-id="45b21-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="45b21-468">您希望 toolog 後端要求 tooan 分析服務。</span><span class="sxs-lookup"><span data-stu-id="45b21-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="45b21-469">使用替代的 HTTP 程式庫</span><span class="sxs-lookup"><span data-stu-id="45b21-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="45b21-470">呼叫 hello`.setAndroidHttpClientFactory()`之後立即建立用戶端參考的方法。</span><span class="sxs-lookup"><span data-stu-id="45b21-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="45b21-471">例如，tooset hello 連接逾時 too60 秒數 （而不是 hello 預設值 10 秒）：</span><span class="sxs-lookup"><span data-stu-id="45b21-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="45b21-472">實作進度篩選條件</span><span class="sxs-lookup"><span data-stu-id="45b21-472">Implement a Progress Filter</span></span>

<span data-ttu-id="45b21-473">您可以藉由實作 `ServiceFilter` 來實作每個要求的攔截。</span><span class="sxs-lookup"><span data-stu-id="45b21-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="45b21-474">例如，下列 hello 更新預先建立的進度列：</span><span class="sxs-lookup"><span data-stu-id="45b21-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="45b21-475">您可以附加此篩選器 toohello 用戶端，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45b21-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="45b21-476">自訂要求標頭</span><span class="sxs-lookup"><span data-stu-id="45b21-476">Customize Request Headers</span></span>

<span data-ttu-id="45b21-477">使用下列 hello`ServiceFilter`和附加 hello 中的 hello 篩選 hello 與相同的方式`ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="45b21-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="45b21-478"><a name="conversions"></a>設定自動序列化</span><span class="sxs-lookup"><span data-stu-id="45b21-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="45b21-479">您可以指定使用 hello 套用 tooevery 資料行的轉換策略[gson] [ 3]應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="45b21-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="45b21-480">hello Android 用戶端程式庫會使用[gson] [ 3] hello 幕後 tooserialize Java 物件 tooJSON 資料 tooAzure App Service 傳送嗨資料之前。</span><span class="sxs-lookup"><span data-stu-id="45b21-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="45b21-481">hello 下列程式碼使用 hello **setFieldNamingStrategy()**方法 tooset hello 策略。</span><span class="sxs-lookup"><span data-stu-id="45b21-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="45b21-482">這個範例會刪除 hello 初始字元 ("m")，並接著小寫 hello 下一個字元，每個欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="45b21-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="45b21-483">比方說，它會將「mId」變成「id」。</span><span class="sxs-lookup"><span data-stu-id="45b21-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="45b21-484">實作轉換策略 tooreduce hello 需要`SerializedName()`大部分欄位上的註解。</span><span class="sxs-lookup"><span data-stu-id="45b21-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="45b21-485">建立使用 hello 的行動用戶端參考之前，必須執行此程式碼**MobileServiceClient**。</span><span class="sxs-lookup"><span data-stu-id="45b21-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[開始使用驗證]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
