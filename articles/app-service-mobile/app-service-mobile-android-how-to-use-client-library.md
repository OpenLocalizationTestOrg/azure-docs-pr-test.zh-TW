---
title: "如何使用 Android 版 Azure Mobile Apps SDK | Microsoft Docs"
description: "如何使用 Android 版 Azure Mobile Apps SDK"
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="2ee35-103">如何使用 Android 版 Azure Mobile Apps SDK</span><span class="sxs-lookup"><span data-stu-id="2ee35-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="2ee35-104">本指南說明如何使用適用於 Mobile Apps 的 Android 用戶端 SDK 來實作常見案例，例如：</span><span class="sxs-lookup"><span data-stu-id="2ee35-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="2ee35-105">查詢資料 (插入、更新和刪除)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="2ee35-106">驗證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-106">Authentication.</span></span>
* <span data-ttu-id="2ee35-107">處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="2ee35-107">Handling errors.</span></span>
* <span data-ttu-id="2ee35-108">自訂用戶端。</span><span class="sxs-lookup"><span data-stu-id="2ee35-108">Customizing the client.</span></span>

<span data-ttu-id="2ee35-109">本指南著重於用戶端 Android SDK。</span><span class="sxs-lookup"><span data-stu-id="2ee35-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="2ee35-110">若要深入了解 Mobile Apps 的伺服器端 SDK，請參閱[使用 .NET 後端 SDK][10]或[如何使用 Node.js 後端 SDK][11]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="2ee35-111">參考文件</span><span class="sxs-lookup"><span data-stu-id="2ee35-111">Reference Documentation</span></span>

<span data-ttu-id="2ee35-112">您可以在 GitHub 找到 Android 用戶端程式庫的 [Javadocs API 參考][12]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="2ee35-113">支援的平台</span><span class="sxs-lookup"><span data-stu-id="2ee35-113">Supported Platforms</span></span>

<span data-ttu-id="2ee35-114">Android 版 Azure Mobile Apps SDK 支援 API 層級 19 至 24 (KitKat 至 Nougat) 的手機和平板電腦外形規格。</span><span class="sxs-lookup"><span data-stu-id="2ee35-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="2ee35-115">特別是驗證，會使用常用的 web 架構方法來收集認證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="2ee35-116">伺服器流程驗證不適用於小型外形規格的裝置，例如手錶。</span><span class="sxs-lookup"><span data-stu-id="2ee35-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="2ee35-117">設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="2ee35-117">Setup and Prerequisites</span></span>

<span data-ttu-id="2ee35-118">完成 [Mobile Apps 快速入門](app-service-mobile-android-get-started.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="2ee35-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="2ee35-119">此工作可確保您已符合開發 Azure Mobile Apps 的所有必要條件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="2ee35-120">快速入門也可協助您設定帳戶，並建立您的第一個行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="2ee35-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="2ee35-121">如果您決定不要完成快速入門教學課程，請完成下列工作︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="2ee35-122">[建立行動應用程式後端][13]以搭配 Android 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="2ee35-123">在 Android Studio 中， [更新 Gradle 組建檔案](#gradle-build)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="2ee35-124">[啟用網際網路權限](#enable-internet)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="2ee35-125"><a name="gradle-build"></a>更新 Gradle 組建檔案</span><span class="sxs-lookup"><span data-stu-id="2ee35-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="2ee35-126">變更以下兩個 build.gradle  檔案：</span><span class="sxs-lookup"><span data-stu-id="2ee35-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="2ee35-127">將此程式碼新增至 *buildscript* 標籤內的*專案*層級 **build.gradle** 檔案：</span><span class="sxs-lookup"><span data-stu-id="2ee35-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="2ee35-128">將此程式碼新增至 *dependencies* 標籤內的*模組應用程式*層級 **build.gradle** 檔案：</span><span class="sxs-lookup"><span data-stu-id="2ee35-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="2ee35-129">目前最新版為 3.3.0。</span><span class="sxs-lookup"><span data-stu-id="2ee35-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="2ee35-130">支援的版本列在 [Bintray 上][14]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="2ee35-131"><a name="enable-internet"></a>啟用網際網路權限</span><span class="sxs-lookup"><span data-stu-id="2ee35-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="2ee35-132">若要存取 Azure，您的應用程式必須啟用網際網路權限。</span><span class="sxs-lookup"><span data-stu-id="2ee35-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="2ee35-133">如果尚未啟用，請將下列這一行程式碼加入至 AndroidManifest.xml  檔案：</span><span class="sxs-lookup"><span data-stu-id="2ee35-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="2ee35-134">建立用戶端連線</span><span class="sxs-lookup"><span data-stu-id="2ee35-134">Create a Client Connection</span></span>

<span data-ttu-id="2ee35-135">Azure Mobile Apps 為您的行動應用程式提供四個函式︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="2ee35-136">Azure Mobile Apps Service 的「資料存取」和「離線同步處理」。</span><span class="sxs-lookup"><span data-stu-id="2ee35-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="2ee35-137">以 Azure Mobile Apps Server SDK 撰寫的「呼叫自訂 API」。</span><span class="sxs-lookup"><span data-stu-id="2ee35-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="2ee35-138">Azure App Service 驗證和授權的「驗證」。</span><span class="sxs-lookup"><span data-stu-id="2ee35-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="2ee35-139">通知中樞的「推播通知註冊」。</span><span class="sxs-lookup"><span data-stu-id="2ee35-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="2ee35-140">這些函式首先會要求您建立 `MobileServiceClient` 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="2ee35-141">您的行動用戶端內只應該建立一個 `MobileServiceClient` 物件 (亦即，它應該是單一子句模式)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="2ee35-142">若要建立 `MobileServiceClient` 物件︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="2ee35-143">`<MobileAppUrl>` 是字串，或是指向您行動後端的 URL 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="2ee35-144">如果您是使用 Azure App Service 來裝載您的行動後端，請確定您使用安全 `https://` 版本的 URL。</span><span class="sxs-lookup"><span data-stu-id="2ee35-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="2ee35-145">用戶端也需要存取活動或內容 - 本範例中為 `this` 參數。</span><span class="sxs-lookup"><span data-stu-id="2ee35-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="2ee35-146">MobileServiceClient 建構應該發生在 `AndroidManifest.xml` 檔案中所參考的 `onCreate()` 活動方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="2ee35-147">最佳做法是，您應該將伺服器通訊擷取到它自己的 (單一模式) 類別。</span><span class="sxs-lookup"><span data-stu-id="2ee35-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="2ee35-148">在此情況下，您應該傳遞建構函式內的活動，以適當地設定服務。</span><span class="sxs-lookup"><span data-stu-id="2ee35-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="2ee35-149">例如：</span><span class="sxs-lookup"><span data-stu-id="2ee35-149">For example:</span></span>

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

<span data-ttu-id="2ee35-150">您現在可以呼叫主要活動 `onCreate()` 方法中的 `AzureServiceAdapter.Initialize(this);`。</span><span class="sxs-lookup"><span data-stu-id="2ee35-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="2ee35-151">需要存取用戶端的其他任何方法會使用 `AzureServiceAdapter.getInstance();`，來取得服務配接器的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="2ee35-152">資料作業</span><span class="sxs-lookup"><span data-stu-id="2ee35-152">Data Operations</span></span>

<span data-ttu-id="2ee35-153">Azure Mobile Apps SDK 的核心，是提供對行動裝置應用程式後端上的 SQL Azure 內所儲存資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="2ee35-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="2ee35-154">您可以使用強型別類型 (建議選項) 或不具類型的查詢 (不建議) 來存取此資料。</span><span class="sxs-lookup"><span data-stu-id="2ee35-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="2ee35-155">本章節大部分都在討論使用強型別類型。</span><span class="sxs-lookup"><span data-stu-id="2ee35-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="2ee35-156">定義用戶端資料類別</span><span class="sxs-lookup"><span data-stu-id="2ee35-156">Define client data classes</span></span>

<span data-ttu-id="2ee35-157">若要存取 SQL Azure 資料表的資料，請定義對應至行動應用程式後端中資料表的用戶端資料類別。</span><span class="sxs-lookup"><span data-stu-id="2ee35-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="2ee35-158">本主題中的範例採用名為 MyDataTable 的資料表，其中包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="2ee35-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="2ee35-159">id</span><span class="sxs-lookup"><span data-stu-id="2ee35-159">id</span></span>
* <span data-ttu-id="2ee35-160">text</span><span class="sxs-lookup"><span data-stu-id="2ee35-160">text</span></span>
* <span data-ttu-id="2ee35-161">完成</span><span class="sxs-lookup"><span data-stu-id="2ee35-161">complete</span></span>

<span data-ttu-id="2ee35-162">對應型別的用戶端物件位於名為 MyDataTable.java 的檔案中：</span><span class="sxs-lookup"><span data-stu-id="2ee35-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="2ee35-163">針對您新增的每個欄位，新增 getter 和 setter 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="2ee35-164">如果您的 SQL Azure 資料表包含多個資料行，您會將對應的欄位新增至此類別。</span><span class="sxs-lookup"><span data-stu-id="2ee35-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="2ee35-165">例如，如果 DTO (資料傳輸物件) 有整數 Priority 資料行，則您可能會新增此欄位，以及其 getter 和 setter 方法：</span><span class="sxs-lookup"><span data-stu-id="2ee35-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="2ee35-166">若要了解如何在您的 Mobile Apps 後端建立其他資料表，請參閱[做法：定義資料表控制器][15] (.NET 後端) 或[使用動態結構描述定義資料表][16] (Node.js 後端)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="2ee35-167">Azure Mobile Apps 後端資料表定義了五個特殊欄位，其中四個可供用戶端使用︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="2ee35-168">`String id`︰記錄的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="2ee35-169">最佳做法是，使識別碼成為 [UUID][17] 物件的字串表示法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="2ee35-170">`DateTimeOffset updatedAt`︰上次更新的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="2ee35-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="2ee35-171">UpdatedAt 欄位由伺服器設定，且不得由用戶端程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="2ee35-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="2ee35-172">`DateTimeOffset createdAt`：建立物件的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="2ee35-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="2ee35-173">CreatedAt 欄位由伺服器設定，且不得由用戶端程式碼設定。</span><span class="sxs-lookup"><span data-stu-id="2ee35-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="2ee35-174">`byte[] version`︰通常會以字串表示，版本也是由伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="2ee35-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="2ee35-175">`boolean deleted`︰表示記錄已刪除，但尚未清除。</span><span class="sxs-lookup"><span data-stu-id="2ee35-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="2ee35-176">請勿使用 `deleted` 作為您類別中的屬性。</span><span class="sxs-lookup"><span data-stu-id="2ee35-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="2ee35-177">`id` 是必填欄位。</span><span class="sxs-lookup"><span data-stu-id="2ee35-177">The `id` field is required.</span></span>  <span data-ttu-id="2ee35-178">`updatedAt` 欄位和 `version` 欄位是用於離線同步處理 (分別適用於增量同步處理和衝突解決)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="2ee35-179">`createdAt` 欄位是參考欄位，且用戶端不可使用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="2ee35-180">名稱為屬性的 "across-the-wire" 名稱，且不可調整。</span><span class="sxs-lookup"><span data-stu-id="2ee35-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="2ee35-181">不過，您可以使用 [gson][3] 程式庫，建立物件與 "across-the-wire" 名稱之間的對應。</span><span class="sxs-lookup"><span data-stu-id="2ee35-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="2ee35-182">例如：</span><span class="sxs-lookup"><span data-stu-id="2ee35-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="2ee35-183">建立資料表參考</span><span class="sxs-lookup"><span data-stu-id="2ee35-183">Create a Table Reference</span></span>

<span data-ttu-id="2ee35-184">若要存取資料表，請先在 [MobileServiceClient][9] 上呼叫 **getTable** 方法，以建立 [MobileServiceTable][8] 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="2ee35-185">此方法有兩個多載：</span><span class="sxs-lookup"><span data-stu-id="2ee35-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="2ee35-186">在下列程式碼中， **mClient** 是您的 MobileServiceClient 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="2ee35-187">第一個多載會在類別名稱與資料表名稱相同的情況下使用，而且會使用於 Quickstart：</span><span class="sxs-lookup"><span data-stu-id="2ee35-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="2ee35-188">第二個多載會在資料表名稱與類型名稱不同時使用：第一個參數為資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="2ee35-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="2ee35-189"><a name="query"></a>查詢後端資料表</span><span class="sxs-lookup"><span data-stu-id="2ee35-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="2ee35-190">首先，取得資料表參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-190">First, obtain a table reference.</span></span>  <span data-ttu-id="2ee35-191">然後針對資料表參考執行查詢。</span><span class="sxs-lookup"><span data-stu-id="2ee35-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="2ee35-192">查詢是以下的任何組合︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-192">A query is any combination of:</span></span>

* <span data-ttu-id="2ee35-193">`.where()` [篩選子句](#filtering)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="2ee35-194">`.orderBy()` [排序子句](#sorting)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="2ee35-195">`.select()` [欄位選取子句](#selection)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="2ee35-196">[分頁結果](#paging)的 `.skip()` 和 `.top()`。</span><span class="sxs-lookup"><span data-stu-id="2ee35-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="2ee35-197">子句必須依上述順序呈現。</span><span class="sxs-lookup"><span data-stu-id="2ee35-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="2ee35-198"><a name="filter"></a> 篩選結果</span><span class="sxs-lookup"><span data-stu-id="2ee35-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="2ee35-199">查詢的一般格式如下︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="2ee35-200">上述範例會傳回所有結果 (最多為伺服器所設定的最大頁面大小)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="2ee35-201">`.execute()` 方法會在後端執行查詢。</span><span class="sxs-lookup"><span data-stu-id="2ee35-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="2ee35-202">傳送至 Mobile Apps 後端之前，查詢會轉換成 [OData v3][19] 查詢。</span><span class="sxs-lookup"><span data-stu-id="2ee35-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="2ee35-203">在收到時，Mobile Apps 後端在 SQL Azure 執行個體上執行查詢之前，會將查詢轉換成 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="2ee35-204">由於網路活動耗費時間，`.execute()` 方法會傳回 [`ListenableFuture<E>`][18]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="2ee35-205"><a name="filtering"></a>篩選傳回的資料</span><span class="sxs-lookup"><span data-stu-id="2ee35-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="2ee35-206">下列查詢執行會從 **complete** 等於 **false** 的 **ToDoItem** 資料表傳回所有項目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-207">**mToDoTable** 是我們先前建立的行動服務資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="2ee35-208">在資料表參考上使用 **where** 方法呼叫定義篩選器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="2ee35-209">在 **where** 方法之後，依序是 **field** 方法以及指定邏輯述詞的方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="2ee35-210">可能的述詞方法包括 **eq** (等於)、**ne** (不等於)、**gt** (大於)、**ge** (大於或等於)、**lt** (小於)、**le** (小於或等於)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="2ee35-211">這些方法可讓您比較數字和字串欄位與特定值。</span><span class="sxs-lookup"><span data-stu-id="2ee35-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="2ee35-212">您可以依日期進行篩選。</span><span class="sxs-lookup"><span data-stu-id="2ee35-212">You can filter on dates.</span></span> <span data-ttu-id="2ee35-213">下列方法可讓您比較整個日期欄位或比較日期的某些部分：**year**、**month**、**day**、**hour**、**minute** 和 **second**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="2ee35-214">下列範例會為 *到期日* 為 2013 年的項目新增篩選器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-215">下列方法在字串欄位上支援複雜的篩選器：**startsWith**、**endsWith**、**concat**、**subString**、**indexOf**、**replace**、**toLower**、**toUpper**、**trim** 和 **length**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="2ee35-216">下列範例會對「text」  資料行的開頭為 "PRI0" 的資料表資料列進行篩選。</span><span class="sxs-lookup"><span data-stu-id="2ee35-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="2ee35-217">數字欄位支援下列運算子方法：**add**、**sub**、**mul**、**div**、**mod**、**floor**、**ceiling** 和 **round**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="2ee35-218">下列範例會對 **duration** 為偶數的資料表資料列進行篩選。</span><span class="sxs-lookup"><span data-stu-id="2ee35-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-219">您可以結合述詞與下列邏輯方法：**and**、**or** 和 **not**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="2ee35-220">下列範例會結合上述的兩個範例。</span><span class="sxs-lookup"><span data-stu-id="2ee35-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="2ee35-221">群組和巢狀邏輯運算子︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="2ee35-222">如需篩選的詳細討論與範例，請參閱[探索功能豐富的 Android 用戶端查詢模型][20]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="2ee35-223"><a name="sorting"></a>排序傳回的資料</span><span class="sxs-lookup"><span data-stu-id="2ee35-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="2ee35-224">下列程式碼會從 **ToDoItems** 資料表傳回依 *text* 欄位遞增排序的所有項目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="2ee35-225">*mToDoTable* 是您先前建立的後端資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-226">**orderBy** 方法的第一個參數是一個字串，代表作為排序依據的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="2ee35-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="2ee35-227">第二個參數會使用 **QueryOrder** 列舉，指定要進行遞增還是遞減排序。</span><span class="sxs-lookup"><span data-stu-id="2ee35-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="2ee35-228">如果您使用 ***where*** 方法進行篩選，***where*** 方法必須要在 ***orderBy*** 方法之前叫用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="2ee35-229"><a name="selection"></a>選取特定資料行</span><span class="sxs-lookup"><span data-stu-id="2ee35-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="2ee35-230">下列程式碼將說明如何傳回 **ToDoItems** 資料表中的所有項目，但僅顯示 **complete** 和 **text** 欄位。</span><span class="sxs-lookup"><span data-stu-id="2ee35-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="2ee35-231">**mToDoTable** 是我們先前建立的後端資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="2ee35-232">select 函數的參數是您要傳回之資料表資料行的字串名稱。</span><span class="sxs-lookup"><span data-stu-id="2ee35-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="2ee35-233">**select** 方法必須跟隨在 **where** 和 **orderBy** 等方法之後。</span><span class="sxs-lookup"><span data-stu-id="2ee35-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="2ee35-234">而其後可以跟隨 **skip** 和 **top** 之類的分頁方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="2ee35-235"><a name="paging"></a>以分頁方式傳回資料</span><span class="sxs-lookup"><span data-stu-id="2ee35-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="2ee35-236">資料**一律**以分頁方式傳回。</span><span class="sxs-lookup"><span data-stu-id="2ee35-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="2ee35-237">傳回的記錄數目上限是由伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="2ee35-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="2ee35-238">如果用戶端要求更多記錄，伺服器就會傳回最大記錄數目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="2ee35-239">根據預設，伺服器上的最大頁面大小為 50 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="2ee35-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="2ee35-240">第一個範例將說明如何從資料表中選取前五個項目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="2ee35-241">查詢會傳回 **ToDoItems**資料表中的項目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="2ee35-242">**mToDoTable** 是您先前建立的後端資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-243">以下是略過前五個項目，而傳回後續五個項目的查詢：</span><span class="sxs-lookup"><span data-stu-id="2ee35-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="2ee35-244">如果您想要取得資料表中的所有記錄，請實作程式碼來逐一查看所有頁面︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="2ee35-245">使用此方法要求所有記錄，會向 Mobile Apps 後端建立最少兩個要求。</span><span class="sxs-lookup"><span data-stu-id="2ee35-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="2ee35-246">選擇正確的頁面大小是在要求過程中的記憶體使用量、頻寬使用量和完全接收資料的延遲時間之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="2ee35-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="2ee35-247">預設值 (50 筆記錄) 適用於所有裝置。</span><span class="sxs-lookup"><span data-stu-id="2ee35-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="2ee35-248">如果您在較大記憶體裝置上獨立操作，則最多增加至 500。</span><span class="sxs-lookup"><span data-stu-id="2ee35-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="2ee35-249">我們發現，將頁面大小增加至超過 500 筆記錄，會導致無法接受的延遲和大量記憶體問題。</span><span class="sxs-lookup"><span data-stu-id="2ee35-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="2ee35-250"><a name="chaining"></a>作法：串連查詢方法</span><span class="sxs-lookup"><span data-stu-id="2ee35-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="2ee35-251">用來查詢後端資料表的方法是可以串連的。</span><span class="sxs-lookup"><span data-stu-id="2ee35-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="2ee35-252">鏈結查詢方法可讓您從排序和分頁的篩選資料列中選取特定資料行。</span><span class="sxs-lookup"><span data-stu-id="2ee35-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="2ee35-253">您可以建立複雜的邏輯篩選器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-253">You can create complex logical filters.</span></span>  <span data-ttu-id="2ee35-254">每個查詢方法都會傳回 Query 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-254">Each query method returns a Query object.</span></span> <span data-ttu-id="2ee35-255">若要結束這一系列的方法並實際執行查詢，請呼叫 **execute** 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="2ee35-256">例如：</span><span class="sxs-lookup"><span data-stu-id="2ee35-256">For example:</span></span>

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

<span data-ttu-id="2ee35-257">鏈結的查詢方法必須依下列順序︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="2ee35-258">篩選 (**where**) 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="2ee35-259">排序 (**orderBy**) 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="2ee35-260">選取 (**select**) 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="2ee35-261">分頁 (**skip** 和 **top**) 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="2ee35-262"><a name="binding"></a>將資料繫結到使用者介面</span><span class="sxs-lookup"><span data-stu-id="2ee35-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="2ee35-263">資料繫結牽涉到三項要件：</span><span class="sxs-lookup"><span data-stu-id="2ee35-263">Data binding involves three components:</span></span>

* <span data-ttu-id="2ee35-264">資料來源</span><span class="sxs-lookup"><span data-stu-id="2ee35-264">The data source</span></span>
* <span data-ttu-id="2ee35-265">畫面配置</span><span class="sxs-lookup"><span data-stu-id="2ee35-265">The screen layout</span></span>
* <span data-ttu-id="2ee35-266">將這兩個項目連結在一起的配接器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="2ee35-267">在範例程式碼中，我們會將 Mobile Apps SQL Azure 資料表 **ToDoItem** 中的資料傳回陣列中。</span><span class="sxs-lookup"><span data-stu-id="2ee35-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="2ee35-268">此活動是常見的資料應用模式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="2ee35-269">資料庫查詢通常會傳回用戶端在清單或陣列中取得的資料列集合。</span><span class="sxs-lookup"><span data-stu-id="2ee35-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="2ee35-270">在此範例中，陣列是資料來源。</span><span class="sxs-lookup"><span data-stu-id="2ee35-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="2ee35-271">程式碼會指定一個畫面配置，以定義裝置上出現的資料檢視。</span><span class="sxs-lookup"><span data-stu-id="2ee35-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="2ee35-272">這兩個項目會透過配接器繫結在一起；在此程式碼中，配接器會是 **ArrayAdapter&lt;ToDoItem&gt;** 類別的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="2ee35-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="2ee35-273"><a name="layout"></a>定義配置</span><span class="sxs-lookup"><span data-stu-id="2ee35-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="2ee35-274">配置可使用數個 XML 程式碼片段來定義。</span><span class="sxs-lookup"><span data-stu-id="2ee35-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="2ee35-275">在現有配置下，下列程式碼會顯示我們要以伺服器資料填入的 **ListView** 。</span><span class="sxs-lookup"><span data-stu-id="2ee35-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="2ee35-276">在上述程式碼中，「listitem」  屬性會指定清單中個別資料列的配置識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="2ee35-277">此程式碼會指定核取方塊及其相關文字，並對清單中的每個項目具現化一次。</span><span class="sxs-lookup"><span data-stu-id="2ee35-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="2ee35-278">此配置不會顯示 **id** 欄位，而更複雜的配置將會指定顯示畫面中的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="2ee35-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="2ee35-279">此程式碼位於 **row_list_to_do.xml** 檔案中。</span><span class="sxs-lookup"><span data-stu-id="2ee35-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="2ee35-280"><a name="adapter"></a>定義配接器</span><span class="sxs-lookup"><span data-stu-id="2ee35-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="2ee35-281">由於我們的檢視資料來源是 **ToDoItem** 的陣列，因此我們將配接器設為 **ArrayAdapter&lt;ToDoItem&gt;** 類別的子類別。</span><span class="sxs-lookup"><span data-stu-id="2ee35-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="2ee35-282">這個子類別會為每個使用 **row_list_to_do** 配置的 **ToDoItem** 產生一個檢視。</span><span class="sxs-lookup"><span data-stu-id="2ee35-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="2ee35-283">我們在程式碼中定義了下列類別，這是 **ArrayAdapter&lt;E&gt;** 類別的擴充功能：</span><span class="sxs-lookup"><span data-stu-id="2ee35-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="2ee35-284">覆寫配接器的 **getView** 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="2ee35-285">例如：</span><span class="sxs-lookup"><span data-stu-id="2ee35-285">For example:</span></span>

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

<span data-ttu-id="2ee35-286">我們在「活動」中建立此類別的執行個體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ee35-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="2ee35-287">ToDoItemAdapter 建構函式的第二個參數是配置的參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="2ee35-288">我們現在可以具現化 **ListView**，並對 **ListView** 指派配接器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="2ee35-289"><a name="use-adapter"></a>使用配接器來繫結至 UI</span><span class="sxs-lookup"><span data-stu-id="2ee35-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="2ee35-290">您現在已可使用資料繫結。</span><span class="sxs-lookup"><span data-stu-id="2ee35-290">You are now ready to use data binding.</span></span> <span data-ttu-id="2ee35-291">下列程式碼說明如何取得資料表中的項目，並以傳回的項目填入本機配接器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="2ee35-292">請在每次修改 **ToDoItem** 資料表時呼叫配接器。</span><span class="sxs-lookup"><span data-stu-id="2ee35-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="2ee35-293">修改是對個別記錄逐一執行的，因此您會處理單一資料列，而不是集合。</span><span class="sxs-lookup"><span data-stu-id="2ee35-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="2ee35-294">在插入項目時，請對配接器呼叫 **add** 方法，刪除時則呼叫 **remove** 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="2ee35-295">您可以在 [Android 快速入門專案][21]中找到完整的範例。</span><span class="sxs-lookup"><span data-stu-id="2ee35-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="2ee35-296"><a name="inserting"></a>將資料插入後端</span><span class="sxs-lookup"><span data-stu-id="2ee35-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="2ee35-297">將「ToDoItem」  類別的執行個體具現化，並設定其屬性。</span><span class="sxs-lookup"><span data-stu-id="2ee35-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="2ee35-298">然後使用 **insert()** 插入物件︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="2ee35-299">傳回的實體會符合插入後端資料表的資料，包括識別碼和後端上設定的任何其他值 (例如 `createdAt`、`updatedAt` 和 `version` 欄位)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="2ee35-300">Mobile Apps 資料表需要名為 **識別碼**的主索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="2ee35-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="2ee35-301">此資料行必須是字串。</span><span class="sxs-lookup"><span data-stu-id="2ee35-301">This column must be a string.</span></span> <span data-ttu-id="2ee35-302">識別碼資料行的預設值是 GUID。</span><span class="sxs-lookup"><span data-stu-id="2ee35-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="2ee35-303">您可以提供其他的唯一值，例如電子郵件地址或使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2ee35-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="2ee35-304">未針對插入的記錄提供字串識別碼值時，後端會產生新的 GUID。</span><span class="sxs-lookup"><span data-stu-id="2ee35-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="2ee35-305">字串識別碼值提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="2ee35-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="2ee35-306">不需要往返存取資料庫就能產生識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="2ee35-307">輕鬆合併不同資料表或資料庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="2ee35-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="2ee35-308">識別碼值與應用程式邏輯的整合更理想。</span><span class="sxs-lookup"><span data-stu-id="2ee35-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="2ee35-309">若要支援離線同步處理，則 **需要** 字串識別碼值。</span><span class="sxs-lookup"><span data-stu-id="2ee35-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="2ee35-310">一旦識別碼儲存在後端資料庫中，您就無法將它變更。</span><span class="sxs-lookup"><span data-stu-id="2ee35-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="2ee35-311"><a name="updating"></a>將行動裝置應用程式中的資料更新</span><span class="sxs-lookup"><span data-stu-id="2ee35-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="2ee35-312">若要更新資料表中的資料，請將新物件傳遞至 **update()** 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="2ee35-313">在此範例中，*item* 是 *ToDoItem* 資料表中某個資料列的參考，其中已有一些變更。</span><span class="sxs-lookup"><span data-stu-id="2ee35-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="2ee35-314">具有相同 **識別碼** 的資料列已更新。</span><span class="sxs-lookup"><span data-stu-id="2ee35-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="2ee35-315"><a name="deleting"></a>將行動裝置應用程式中的資料刪除</span><span class="sxs-lookup"><span data-stu-id="2ee35-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="2ee35-316">下列程式碼說明如何藉由指定資料物件來刪除資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="2ee35-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="2ee35-317">您也可以藉由指定要刪除的資料列的 **id** 欄位來刪除項目。</span><span class="sxs-lookup"><span data-stu-id="2ee35-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="2ee35-318"><a name="lookup"></a>依識別碼查閱特定項目</span><span class="sxs-lookup"><span data-stu-id="2ee35-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="2ee35-319">以 **lookUp()** 方法查閱具有特定**識別碼**欄位的項目：</span><span class="sxs-lookup"><span data-stu-id="2ee35-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="2ee35-320"><a name="untyped"></a>作法：使用不具類型的資料</span><span class="sxs-lookup"><span data-stu-id="2ee35-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="2ee35-321">不具型別的程式設計模型可讓您精確掌控 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="2ee35-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="2ee35-322">在某些常見情況下，您可能會想使用不具型別的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="2ee35-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="2ee35-323">例如，如果您的後端資料表包含許多資料行，但您只需要參考其中幾個資料行時。</span><span class="sxs-lookup"><span data-stu-id="2ee35-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="2ee35-324">使用具型別的模型時，您必須在資料類別中將 Mobile Apps 後端所定義的所有資料行進行定義。</span><span class="sxs-lookup"><span data-stu-id="2ee35-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="2ee35-325">用來存取資料的 API 呼叫大多會與型別程式設計呼叫相類似。</span><span class="sxs-lookup"><span data-stu-id="2ee35-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="2ee35-326">主要的差別在於，在不具型別的模型中，您會叫用 **MobileServiceJsonTable** 物件的方法，而不是 **MobileServiceTable** 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="2ee35-327"><a name="json_instance"></a>建立不具型別的資料表執行個體</span><span class="sxs-lookup"><span data-stu-id="2ee35-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="2ee35-328">和型別模型一樣，首先您必須取得資料表參考，但在此案例中這會是 **MobileServicesJsonTable** 物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="2ee35-329">在用戶端的執行個體上呼叫 **getTable** 方法以取得參考：</span><span class="sxs-lookup"><span data-stu-id="2ee35-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="2ee35-330">在您建立 **MobileServiceJsonTable**的執行個體後，它就幾乎具有和型別程式設計模型所能使用的一樣的 API。</span><span class="sxs-lookup"><span data-stu-id="2ee35-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="2ee35-331">在某些情況下，這些方法會採用不具型別的參數，而非具型別的參數。</span><span class="sxs-lookup"><span data-stu-id="2ee35-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="2ee35-332"><a name="json_insert"></a>插入不具型別的資料表中</span><span class="sxs-lookup"><span data-stu-id="2ee35-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="2ee35-333">下列程式碼將說明如何執行插入。</span><span class="sxs-lookup"><span data-stu-id="2ee35-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="2ee35-334">第一個步驟是建立屬於 [gson][3] 程式庫的 [JsonObject][1]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="2ee35-335">然後，使用 **insert()** 在資料表中插入不具型別的物件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="2ee35-336">如果您需要取得所插入之物件的識別碼，請使用 **getAsJsonPrimitive()** 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="2ee35-337"><a name="json_delete"></a>在不具型別的資料表中進行刪除</span><span class="sxs-lookup"><span data-stu-id="2ee35-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="2ee35-338">下列程式碼將說明如何刪除執行個體 (在此案例中，即為在前述 **插入** 範例中建立的同一個 *JsonObject* 執行個體)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="2ee35-339">程式碼與典型案例相同，但方法具有不同的簽章，因為它會參考 **JsonObject**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="2ee35-340">您也可以直接使用 ID 來刪除執行個體：</span><span class="sxs-lookup"><span data-stu-id="2ee35-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="2ee35-341"><a name="json_get"></a>從不具型別的資料表傳回所有資料列</span><span class="sxs-lookup"><span data-stu-id="2ee35-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="2ee35-342">下列程式碼將說明如何擷取整個資料表。</span><span class="sxs-lookup"><span data-stu-id="2ee35-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="2ee35-343">由於您使用 JSON 資料表，因此可以選擇性地只擷取資料表的某些資料行。</span><span class="sxs-lookup"><span data-stu-id="2ee35-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="2ee35-344">具型別的模型可使用的同一組篩選、篩選和分頁方法，可供不具型別的模型使用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="2ee35-345"><a name="offline-sync"></a>實作離線同步處理</span><span class="sxs-lookup"><span data-stu-id="2ee35-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="2ee35-346">Azure Mobile Apps 用戶端 SDK 也會使用 SQL Database 在本機儲存伺服器資料的副本，來實作離線資料同步處理。</span><span class="sxs-lookup"><span data-stu-id="2ee35-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="2ee35-347">離線資料表上執行的作業不需要行動連線能力。</span><span class="sxs-lookup"><span data-stu-id="2ee35-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="2ee35-348">離線同步處理可協助復原能力和效能，但代價是更複雜的衝突解決邏輯。</span><span class="sxs-lookup"><span data-stu-id="2ee35-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="2ee35-349">Mobile Apps 用戶端 SDK 會實作下列功能︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="2ee35-350">增量同步處理︰只會下載更新和新的記錄，可節省頻寬和記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="2ee35-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="2ee35-351">開放式並行存取︰作業會假設為成功。</span><span class="sxs-lookup"><span data-stu-id="2ee35-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="2ee35-352">會延後衝突解決，直到伺服器上執行更新為止。</span><span class="sxs-lookup"><span data-stu-id="2ee35-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="2ee35-353">衝突解決︰SDK 會偵測到伺服器上已進行的衝突變更，並提供攔截程序來警示使用者。</span><span class="sxs-lookup"><span data-stu-id="2ee35-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="2ee35-354">虛刪除︰已刪除的記錄會標示為已刪除，使其他裝置可更新其離線快取。</span><span class="sxs-lookup"><span data-stu-id="2ee35-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="2ee35-355">將離線同步處理初始化</span><span class="sxs-lookup"><span data-stu-id="2ee35-355">Initialize Offline Sync</span></span>

<span data-ttu-id="2ee35-356">必須在離線快取中定義每個離線資料表之後才能使用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="2ee35-357">一般而言，用戶端建立後，會立即完成資料表定義︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="2ee35-358">取得離線快取資料表的參考</span><span class="sxs-lookup"><span data-stu-id="2ee35-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="2ee35-359">如需線上資料表，請使用 `.getTable()`。</span><span class="sxs-lookup"><span data-stu-id="2ee35-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="2ee35-360">如需離線資料表，請使用 `.getSyncTable()`：</span><span class="sxs-lookup"><span data-stu-id="2ee35-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="2ee35-361">可供線上資料表 (包括篩選、排序、分頁、插入資料、更新資料和刪除資料) 使用的所有方法，在線上或離線資料表上都可正常運作。</span><span class="sxs-lookup"><span data-stu-id="2ee35-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="2ee35-362">同步處理本機離線快取</span><span class="sxs-lookup"><span data-stu-id="2ee35-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="2ee35-363">可在您的應用程式內控制同步處理。</span><span class="sxs-lookup"><span data-stu-id="2ee35-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="2ee35-364">以下是同步處理方法的範例︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="2ee35-365">如果將查詢名稱提供給 `.pull(query, queryname)` 方法，則使用增量同步處理所傳回的記錄，只有自上次成功完成提取後所建立或變更的記錄。</span><span class="sxs-lookup"><span data-stu-id="2ee35-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="2ee35-366">處理離線同步處理期間的衝突</span><span class="sxs-lookup"><span data-stu-id="2ee35-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="2ee35-367">如果在 `.push()` 作業期間發生衝突，就會擲回 `MobileServiceConflictException`。</span><span class="sxs-lookup"><span data-stu-id="2ee35-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="2ee35-368">伺服器所發行的項目內嵌於例外狀況，而且可以由 `.getItem()` 例外狀況進行擷取。</span><span class="sxs-lookup"><span data-stu-id="2ee35-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="2ee35-369">在 MobileServiceSyncContext 物件上呼叫下列項目來調整推送︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="2ee35-370">一旦所有衝突都如您想要的方式標記後，再次呼叫 `.push()` 來解決所有衝突。</span><span class="sxs-lookup"><span data-stu-id="2ee35-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="2ee35-371"><a name="custom-api"></a>呼叫自訂 API</span><span class="sxs-lookup"><span data-stu-id="2ee35-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="2ee35-372">自訂 API 可讓您定義自訂端點，並用來公開無法對應插入、更新、刪除或讀取等操作的伺服器功能。</span><span class="sxs-lookup"><span data-stu-id="2ee35-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="2ee35-373">透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="2ee35-374">從 Android 用戶端呼叫 **invokeApi** 方法，以呼叫自訂 API 端點。</span><span class="sxs-lookup"><span data-stu-id="2ee35-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="2ee35-375">下列範例示範如何呼叫名為 **completeAll** 的 API 端點，它會傳回名為 **MarkAllResult** 的集合類別。</span><span class="sxs-lookup"><span data-stu-id="2ee35-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="2ee35-376">**invokeApi** 方法是在用戶端上呼叫，可將 POST 要求傳送給新的自訂 API。</span><span class="sxs-lookup"><span data-stu-id="2ee35-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="2ee35-377">如有任何錯誤，自訂 API 傳回的結果會顯示在訊息對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="2ee35-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="2ee35-378">其他版本的 **invokeApi** 可讓您選擇性地在要求主體中傳送物件、指定 HTTP 方法，並隨著要求一起傳送查詢參數。</span><span class="sxs-lookup"><span data-stu-id="2ee35-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="2ee35-379">也會提供不具型別的版本 **invokeApi** 。</span><span class="sxs-lookup"><span data-stu-id="2ee35-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="2ee35-380"><a name="authentication"></a>在您的應用程式中新增驗證</span><span class="sxs-lookup"><span data-stu-id="2ee35-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="2ee35-381">教學課程已詳細說明如何新增這些功能。</span><span class="sxs-lookup"><span data-stu-id="2ee35-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="2ee35-382">App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory) 來 [驗證應用程式使用者](app-service-mobile-android-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="2ee35-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="2ee35-383">您可以在資料表上設定權限，以限制僅有通過驗證使用者可以存取特定操作。</span><span class="sxs-lookup"><span data-stu-id="2ee35-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="2ee35-384">您也可以使用經驗證使用者的身分識別，以在後端實作授權規則。</span><span class="sxs-lookup"><span data-stu-id="2ee35-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="2ee35-385">支援兩個驗證流程：**伺服器**流程和**用戶端**流程。</span><span class="sxs-lookup"><span data-stu-id="2ee35-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="2ee35-386">由於伺服器流程採用識別提供者的 Web 介面，因此所提供的驗證體驗也最為簡單。</span><span class="sxs-lookup"><span data-stu-id="2ee35-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="2ee35-387">不需要其他 SDK 就能實作伺服器流程驗證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="2ee35-388">伺服器流程驗證不會與行動裝置密切整合，因此只建議用於概念證明案例。</span><span class="sxs-lookup"><span data-stu-id="2ee35-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="2ee35-389">用戶端流程依賴識別提供者提供的 SDK，因此可以與裝置特有的功能深入整合，例如單一登入。</span><span class="sxs-lookup"><span data-stu-id="2ee35-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="2ee35-390">例如，您可以將 Facebook SDK 整合到行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="2ee35-391">行動用戶端會切換到 Facebook 應用程式，並確認您已登入再切換回行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="2ee35-392">要在您的應用程式中啟用驗證，必須執行四個步驟：</span><span class="sxs-lookup"><span data-stu-id="2ee35-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="2ee35-393">對識別提供者註冊應用程式以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="2ee35-394">設定 App Service 後端。</span><span class="sxs-lookup"><span data-stu-id="2ee35-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="2ee35-395">限制只有 App Service 後端上經驗證的使用者會具有資料表權限。</span><span class="sxs-lookup"><span data-stu-id="2ee35-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="2ee35-396">將驗證碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-396">Add authentication code to your app.</span></span>

<span data-ttu-id="2ee35-397">您可以在資料表上設定權限，以限制僅有通過驗證使用者可以存取特定操作。</span><span class="sxs-lookup"><span data-stu-id="2ee35-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="2ee35-398">您也可以使用已驗證的使用者 SID 來修改要求。</span><span class="sxs-lookup"><span data-stu-id="2ee35-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="2ee35-399">如需詳細資訊，請檢閱 [開始使用驗證] 和伺服器 SDK 做法文件。</span><span class="sxs-lookup"><span data-stu-id="2ee35-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="2ee35-400"><a name="caching"></a>驗證︰伺服器流程</span><span class="sxs-lookup"><span data-stu-id="2ee35-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="2ee35-401">下列程式碼會使用 Google 提供者來啟動伺服器流程登入程序。</span><span class="sxs-lookup"><span data-stu-id="2ee35-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="2ee35-402">由於 Google 提供者的安全性需求，需要其他設定︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="2ee35-403">此外，將下列方法新增至主要活動類別︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="2ee35-404">在您主要活動中定義的 `GOOGLE_LOGIN_REQUEST_CODE` 會用於 `login()` 方法，以及 `onActivityResult()` 方法內。</span><span class="sxs-lookup"><span data-stu-id="2ee35-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="2ee35-405">只要 `login()` 方法和 `onActivityResult()` 方法內都使用相同的數字，您就可以選擇任何唯一的數字。</span><span class="sxs-lookup"><span data-stu-id="2ee35-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="2ee35-406">如果您將用戶端程式碼服務擷取至服務配接器 (如先前所示)，應該在服務配接器上呼叫適當的方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="2ee35-407">您也需要設定 customtabs 的專案。</span><span class="sxs-lookup"><span data-stu-id="2ee35-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="2ee35-408">先指定重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="2ee35-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="2ee35-409">將下列程式碼片段新增至 `AndroidManifest.xml`：</span><span class="sxs-lookup"><span data-stu-id="2ee35-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="2ee35-410">將 **redirectUriScheme** 新增至應用程式的 `build.gradle` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="2ee35-411">最後，將 `com.android.support:customtabs:23.0.1` 新增至 `build.gradle` 檔案中的相依性清單︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="2ee35-412">使用 **getUserId** 方法從 **MobileServiceUser** 取得已登入使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="2ee35-413">如需如何使用 Futures 來呼叫非同步登入 API 的範例，請參閱 [開始使用驗證]。</span><span class="sxs-lookup"><span data-stu-id="2ee35-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="2ee35-414">所述的 URL 配置會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="2ee35-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="2ee35-415">確認所有出現的 `{url_scheme_of_you_app}` 大小寫相符。</span><span class="sxs-lookup"><span data-stu-id="2ee35-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="2ee35-416"><a name="caching"></a>快取驗證權杖</span><span class="sxs-lookup"><span data-stu-id="2ee35-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="2ee35-417">您必須將使用者 ID 和驗證語彙基元儲存在本機裝置上，才能快取驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="2ee35-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="2ee35-418">當應用程式下次啟動時，您只需確認這些值仍存在於快取中，即可略過登入程序，並使用這項資料還原用戶端。</span><span class="sxs-lookup"><span data-stu-id="2ee35-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="2ee35-419">但這項資料具有敏感性，因此應加密儲存，以確保在手機失竊的狀況下仍保有安全性。</span><span class="sxs-lookup"><span data-stu-id="2ee35-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="2ee35-420">您可以在[快取驗證權杖一節][7]中看到如何快取驗證權杖的完整範例。</span><span class="sxs-lookup"><span data-stu-id="2ee35-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="2ee35-421">當您嘗試使用到期的權杖時，您會收到「401 未授權」  的回應。</span><span class="sxs-lookup"><span data-stu-id="2ee35-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="2ee35-422">您可以使用篩選器處理驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="2ee35-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="2ee35-423">篩選器會攔截對 App Service 後端提出的要求。</span><span class="sxs-lookup"><span data-stu-id="2ee35-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="2ee35-424">篩選器程式碼會測試 401 的回應、觸發登入程序，然後繼續執行產生 401 的要求。</span><span class="sxs-lookup"><span data-stu-id="2ee35-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="2ee35-425"><a name="refresh"></a>使用重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="2ee35-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="2ee35-426">Azure App Service 驗證與授權傳回的權杖都有一小時的定義存留時間。</span><span class="sxs-lookup"><span data-stu-id="2ee35-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="2ee35-427">在這段期間之後，您必須重新驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="2ee35-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="2ee35-428">如果您使用的是透過用戶端流程驗證收到的長時間執行的權杖，您可以使用相同的權杖，透過 Azure App Service 驗證與授權進行重新驗證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="2ee35-429">所產生的另一個 Azure App Service 權杖會含有新的存留期。</span><span class="sxs-lookup"><span data-stu-id="2ee35-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="2ee35-430">您也可以註冊提供者來使用重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="2ee35-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="2ee35-431">重新整理權杖並非一律可用。</span><span class="sxs-lookup"><span data-stu-id="2ee35-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="2ee35-432">需要進行其他設定：</span><span class="sxs-lookup"><span data-stu-id="2ee35-432">Additional configuration is required:</span></span>

* <span data-ttu-id="2ee35-433">對於 **Azure Active Directory**，請設定 Azure Active Directory 應用程式的用戶端祕密。</span><span class="sxs-lookup"><span data-stu-id="2ee35-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="2ee35-434">設定 Azure Active Directory 驗證時，請在 Azure App Service 中指定用戶端祕密。</span><span class="sxs-lookup"><span data-stu-id="2ee35-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="2ee35-435">呼叫 `.login()` 時，傳遞 `response_type=code id_token` 作為參數︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="2ee35-436">若為 **Google**，請傳遞 `access_type=offline` 作為參數︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="2ee35-437">若為 **Microsoft 帳戶**，請選取 `wl.offline_access` 範圍。</span><span class="sxs-lookup"><span data-stu-id="2ee35-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="2ee35-438">若要重新整理權杖，請呼叫 `.refreshUser()`：</span><span class="sxs-lookup"><span data-stu-id="2ee35-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="2ee35-439">最佳做法是，建立篩選條件偵測來自伺服器的 401 回應，並嘗試重新整理使用者權杖。</span><span class="sxs-lookup"><span data-stu-id="2ee35-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="2ee35-440">使用用戶端流程驗證登入</span><span class="sxs-lookup"><span data-stu-id="2ee35-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="2ee35-441">使用用戶端流程驗證登入的一般程序如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="2ee35-442">以您設定伺服器流程驗證的相同方式設定 Azure App Service 驗證與授權。</span><span class="sxs-lookup"><span data-stu-id="2ee35-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="2ee35-443">將驗證提供者 SDK 進行整合以供驗證，來產生存取權杖。</span><span class="sxs-lookup"><span data-stu-id="2ee35-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="2ee35-444">呼叫 `.login()` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ee35-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="2ee35-445">將 `onSuccess()` 方法取代為您想要用於成功登入的任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="2ee35-446">`{provider}` 字串是有效的提供者︰**aad** (Azure Active Directory)、**facebook**、**google**、**microsoftaccount** 或 **twitter**。</span><span class="sxs-lookup"><span data-stu-id="2ee35-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="2ee35-447">如果您已實作自訂驗證，則也可以使用自訂驗證提供者的標記。</span><span class="sxs-lookup"><span data-stu-id="2ee35-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="2ee35-448"><a name="adal"></a>使用 Active Directory Authentication Library (ADAL) 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="2ee35-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="2ee35-449">您可以使用 Active Directory Authentication Library (ADAL)，利用 Azure Active Directory 將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ee35-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="2ee35-450">使用用戶端流程登入通常會比使用 `loginAsync()` 方法還適合，因為它提供更原生的 UX 風格，並允許其他自訂。</span><span class="sxs-lookup"><span data-stu-id="2ee35-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="2ee35-451">依照[如何設定 App Service 來進行 Active Directory 登入][22]教學課程的說明，設定您的行動應用程式後端來進行 AAD 登入。</span><span class="sxs-lookup"><span data-stu-id="2ee35-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="2ee35-452">請務必完成註冊原生用戶端應用程式的選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="2ee35-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="2ee35-453">安裝 ADAL，方法是修改您的 build.gradle 檔案以納入下列定義：</span><span class="sxs-lookup"><span data-stu-id="2ee35-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="2ee35-454">將下列程式碼新增至您的應用程式，進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="2ee35-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="2ee35-455">以您佈建應用程式的租用戶名稱取代 **INSERT-AUTHORITY-HERE** 。</span><span class="sxs-lookup"><span data-stu-id="2ee35-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="2ee35-456">格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="2ee35-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="2ee35-457">以您行動應用程式後端的用戶端識別碼取代 INSERT-RESOURCE-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="2ee35-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="2ee35-458">您可以從入口網站 [Azure Active Directory 設定] 底下的 [進階] 索引標籤取得用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ee35-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="2ee35-459">以您從原生用戶端應用程式中複製的用戶端識別碼取代 INSERT-CLIENT-ID-HERE  。</span><span class="sxs-lookup"><span data-stu-id="2ee35-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="2ee35-460">使用 HTTPS 配置，以您網站的 **/.auth/login/done** 端點取代 *INSERT-REDIRECT-URI-HERE* 。</span><span class="sxs-lookup"><span data-stu-id="2ee35-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="2ee35-461">此值應與 *https://contoso.azurewebsites.net/.auth/login/done* 類似。</span><span class="sxs-lookup"><span data-stu-id="2ee35-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="2ee35-462"><a name="filters"></a>調整用戶端與伺服器通訊</span><span class="sxs-lookup"><span data-stu-id="2ee35-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="2ee35-463">用戶端連線通常是使用隨 Android SDK 提供之基礎 HTTP 程式庫的基本 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="2ee35-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="2ee35-464">有幾個原因使您會想加以變更︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="2ee35-465">您想要使用替代的 HTTP 程式庫來調整逾時。</span><span class="sxs-lookup"><span data-stu-id="2ee35-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="2ee35-466">您想要提供進度列。</span><span class="sxs-lookup"><span data-stu-id="2ee35-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="2ee35-467">您想要新增自訂標頭，以支援 API 管理功能。</span><span class="sxs-lookup"><span data-stu-id="2ee35-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="2ee35-468">您想要攔截失敗的回應，以便您可以實作重新驗證。</span><span class="sxs-lookup"><span data-stu-id="2ee35-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="2ee35-469">您想要記錄分析服務的後端要求。</span><span class="sxs-lookup"><span data-stu-id="2ee35-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="2ee35-470">使用替代的 HTTP 程式庫</span><span class="sxs-lookup"><span data-stu-id="2ee35-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="2ee35-471">建立用戶端參考之後，立即呼叫 `.setAndroidHttpClientFactory()` 方法。</span><span class="sxs-lookup"><span data-stu-id="2ee35-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="2ee35-472">例如，若要將連線逾時設定為 60 秒 (而不是預設值 10 秒)︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="2ee35-473">實作進度篩選條件</span><span class="sxs-lookup"><span data-stu-id="2ee35-473">Implement a Progress Filter</span></span>

<span data-ttu-id="2ee35-474">您可以藉由實作 `ServiceFilter` 來實作每個要求的攔截。</span><span class="sxs-lookup"><span data-stu-id="2ee35-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="2ee35-475">例如，下列作業會更新預先建立的進度列︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="2ee35-476">您可以將此篩選條件附加至用戶端，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2ee35-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="2ee35-477">自訂要求標頭</span><span class="sxs-lookup"><span data-stu-id="2ee35-477">Customize Request Headers</span></span>

<span data-ttu-id="2ee35-478">使用下列 `ServiceFilter`，並使用與 `ProgressFilter` 相同的方式附加篩選條件：</span><span class="sxs-lookup"><span data-stu-id="2ee35-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="2ee35-479"><a name="conversions"></a>設定自動序列化</span><span class="sxs-lookup"><span data-stu-id="2ee35-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="2ee35-480">您可以使用 [gson][3] API 指定套用至每個資料行的轉換策略。</span><span class="sxs-lookup"><span data-stu-id="2ee35-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="2ee35-481">Android 用戶端程式庫會先在背景使用 [gson][3] 來將 Java 物件序列化為 JSON 資料，再將資料傳送至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="2ee35-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="2ee35-482">下列程式碼使用 **setFieldNamingStrategy()** 方法來設定策略。</span><span class="sxs-lookup"><span data-stu-id="2ee35-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="2ee35-483">此範例會刪除每個欄位名稱的起始字元 ("m")，然後將下一個字元轉換為小寫。</span><span class="sxs-lookup"><span data-stu-id="2ee35-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="2ee35-484">比方說，它會將「mId」變成「id」。</span><span class="sxs-lookup"><span data-stu-id="2ee35-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="2ee35-485">實作轉換策略，以減少大部分欄位上的 `SerializedName()` 註釋需要。</span><span class="sxs-lookup"><span data-stu-id="2ee35-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="2ee35-486">必須先執行此程式碼，才能使用 **MobileServiceClient** 來建立行動用戶端參考。</span><span class="sxs-lookup"><span data-stu-id="2ee35-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="2ee35-487">[開始使用驗證]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="2ee35-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
