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
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>如何 toouse hello 適用於 Android 的 Azure 行動應用程式 SDK

本指南也說明如何 toouse hello Android 用戶端 SDK 行動應用程式 tooimplement 常見案例，例如：

* 查詢資料 (插入、更新和刪除)。
* 驗證。
* 處理錯誤。
* 自訂 hello 用戶端。

此指南著重於 hello 用戶端的 Android SDK。  toolearn 深入了解 hello 行動應用程式的伺服器端 Sdk，請參閱[搭配.NET 後端 SDK] [ 10]或[toouse 如何 hello Node.js 後端 SDK] [ 11].

## <a name="reference-documentation"></a>參考文件

您可以找到 hello [Javadocs API 參考][ 12] hello GitHub 上的 Android 用戶端程式庫。

## <a name="supported-platforms"></a>支援的平台

hello Azure 行動應用程式 SDK for Android 支援應用程式開發介面層級 19-24 (透過 Nougat KitKat) 電話和平板電腦的表單係數。  驗證，特別是，利用常用的 web 架構方法 toogather 認證。  伺服器流程驗證不適用於小型外形規格的裝置，例如手錶。

## <a name="setup-and-prerequisites"></a>設定和必要條件

完整的 hello[行動應用程式快速入門](app-service-mobile-android-get-started.md)教學課程。  此工作可確保您已符合開發 Azure Mobile Apps 的所有必要條件。  快速入門 hello 也可協助您設定您的帳戶，並建立第一個行動裝置應用程式後端。

如果您決定不 toocomplete hello 快速入門教學課程，請完成下列工作的 hello:

* [建立行動裝置應用程式後端][ 13] toouse 與 Android 應用程式。
* 在 Android Studio 中，[更新 hello Gradle 組建檔案](#gradle-build)。
* [啟用網際網路權限](#enable-internet)。

### <a name="gradle-build"></a>更新 hello Gradle 組建檔案

變更以下兩個 build.gradle  檔案：

1. 加入這個程式碼 toohello*專案*層級**build.gradle**檔案置於 hello *buildscript*標記：

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. 加入這個程式碼 toohello*模組應用程式*層級**build.gradle**檔案置於 hello*相依性*標記：

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    目前 hello 最新版本為 3.3.0。 hello 支援的版本會列出[上 bintray][14]。

### <a name="enable-internet"></a>啟用網際網路權限

tooaccess Azure，您的應用程式必須啟用 hello 網際網路權限。 如果尚未啟用，加入下列一行程式碼 tooyour hello **AndroidManifest.xml**檔案：

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>建立用戶端連線

Azure 行動應用程式提供四個函式 tooyour 行動應用程式：

* Azure Mobile Apps Service 的「資料存取」和「離線同步處理」。
* 呼叫以 hello Azure 行動應用程式伺服器 SDK 所撰寫的自訂 Api。
* Azure App Service 驗證和授權的「驗證」。
* 通知中樞的「推播通知註冊」。

這些函式首先會要求您建立 `MobileServiceClient` 物件。  您的行動用戶端內只應該建立一個 `MobileServiceClient` 物件 (亦即，它應該是單一子句模式)。  toocreate`MobileServiceClient`物件：

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

hello`<MobileAppUrl>`是字串，或是指向 tooyour 行動後端 URL 物件。  如果您使用 Azure App Service toohost 行動後端，請確定您使用安全的 hello `https://` hello URL 的版本。

hello 用戶端也需要存取 toohello 活動或內容-hello `this` hello 範例中的參數。  hello MobileServiceClient 建構應該會在 hello 內`onCreate()`方法中 hello 參考活動的 hello`AndroidManifest.xml`檔案。

最佳做法是，您應該將伺服器通訊擷取到它自己的 (單一模式) 類別。  在此情況下，您應該傳遞 hello 活動內 hello 建構函式 tooappropriately hello 服務設定。  例如：

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

您現在可以呼叫`AzureServiceAdapter.Initialize(this);`在 hello`onCreate()`主要活動的方法。  需要存取 toohello 用戶端的其他方法使用`AzureServiceAdapter.getInstance();`tooobtain 參考 toohello service 配接器。

## <a name="data-operations"></a>資料作業

hello Azure 行動應用程式 SDK 的 hello 核心是 tooprovide 存取 toodata hello 行動裝置應用程式後端儲存在 SQL Azure。  您可以使用強型別類型 (建議選項) 或不具類型的查詢 (不建議) 來存取此資料。  hello 大量本節說明如何使用強型別的類別。

### <a name="define-client-data-classes"></a>定義用戶端資料類別

tooaccess SQL Azure 資料表資料，定義對應 toohello 資料表 hello 行動裝置應用程式後端中的用戶端資料類別。 本主題中的範例假設名為的資料表**MyDataTable**，其中包含下列資料行的 hello:

* id
* text
* 完成

hello 對應的型別的用戶端物件位於檔案呼叫**MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

針對您新增的每個欄位，新增 getter 和 setter 方法。  如果您的 SQL Azure 資料表包含多個資料行，您將加入 hello 對應欄位 toothis 類別。  例如，如果 hello DTO （資料傳輸物件） 具有整數優先順序資料行，則您可能會加入這個欄位，以及其 getter 和 setter 方法：

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

如何 toocreate 其他資料表中您的行動應用程式後端，請參閱的 toolearn[如何： 定義資料表控制器][ 15] （.NET 後端） 或[使用動態結構描述定義資料表][ 16] （Node.js 後端）。

Azure 行動應用程式後端資料表定義五個特殊欄位，其中四個為可用 tooclients:

* `String id`: hello hello 記錄的全域唯一識別碼。  最佳做法，請 hello 識別碼 hello 字串表示法[UUID] [ 17]物件。
* `DateTimeOffset updatedAt`: hello 的 hello 上次更新日期/時間。  hello updatedAt 欄位由 hello 伺服器設定，且不能設定您的用戶端程式碼。
* `DateTimeOffset createdAt`: hello 日期/時間建立該 hello 物件。  hello createdAt 欄位由 hello 伺服器設定，且不能設定您的用戶端程式碼。
* `byte[] version`： 通常表示為字串，hello 版本也會設定 hello 伺服器。
* `boolean deleted`： 表示 hello 記錄已刪除但未清除尚未。  請勿使用 `deleted` 作為您類別中的屬性。

hello`id`是必填欄位。  hello`updatedAt`欄位和`version`欄位可用來離線同步處理 (如增量同步處理和衝突解決方式分別)。  hello`createdAt`欄位是參考欄位，而不是由 hello 用戶端。  hello 名稱是"跨線上"hello 屬性名稱，且不是可調整。  不過，您可以建立您的物件與 hello 之間的對應 」 跨網路 」 名稱使用 hello [gson] [ 3]程式庫。  例如：

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

### <a name="create-a-table-reference"></a>建立資料表參考

tooaccess 資料表時，第一次建立[MobileServiceTable] [ 8]物件呼叫 hello **getTable**方法上 hello [MobileServiceClient][9].  此方法有兩個多載：

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

在下列程式碼中，hello **m**是參考 tooyour MobileServiceClient 物件。  hello 第一個多載會使用其中 hello 類別名稱和 hello 資料表名稱是 hello 相同，而且會 hello 其中一個用於 hello 快速入門：

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

hello 第二個多載時，會使用 hello 資料表名稱是 hello 類別名稱不同： hello 第一個參數是 hello 資料表名稱。

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>查詢後端資料表

首先，取得資料表參考。  在 hello 資料表參考，然後執行查詢。  查詢是以下的任何組合︰

* `.where()` [篩選子句](#filtering)。
* `.orderBy()` [排序子句](#sorting)。
* `.select()` [欄位選取子句](#selection)。
* [分頁結果](#paging)的 `.skip()` 和 `.top()`。

hello 子句必須呈現在 hello 上述順序。

### <a name="filter"></a> 篩選結果

hello 一般形式是查詢的：

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

hello 上述範例會傳回所有結果 （向上 toohello hello 伺服器所設定的最大頁面大小）。  hello `.execute()` hello 後端上執行 hello 查詢的方法。  hello 查詢是轉換的 tooan [OData v3] [ 19]之前傳輸 toohello 行動應用程式後端的查詢。  在收到，hello 行動應用程式後端會將 hello 查詢轉換成 SQL 陳述式之前執行 hello SQL Azure 執行個體上。  網路活動需要一些時間，因為 hello`.execute()`方法會傳回[ `ListenableFuture<E>` ] [ 18]。

### <a name="filtering"></a>篩選傳回的資料

hello 查詢執行之後傳回所有項目從 hello **ToDoItem**資料表**完成**等於**false**。

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** hello 參考 toohello 行動服務資料表我們先前所建立。

定義篩選條件使用 hello**其中**hello 資料表參考上的方法呼叫。 hello**其中**方法後面**欄位**方法，然後指定 hello 邏輯述詞的方法。 可能的述詞方法包括 **eq** (等於)、**ne** (不等於)、**gt** (大於)、**ge** (大於或等於)、**lt** (小於)、**le** (小於或等於)。 這些方法可讓您比較數字和字串 toospecific 值欄位。

您可以依日期進行篩選。 hello 下列方法可讓您比較 hello 整個日期欄位或 hello 日期部分：**年**，**月份**，**天**，**小時**， **分鐘**，和**第二個**。 hello 下列範例會將篩選條件的項目其*到期日*等於 2013年。

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

hello 下列方法支援更複雜的篩選字串欄位： **startsWith**， **endsWith**， **concat**， **subString**， **indexOf**，**取代**， **toLower**， **toUpper**，**修剪**，和**長度**。 下列範例會篩選的資料表資料列，其中 hello hello*文字*資料行開頭為"PRI0。 」

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

數字欄位支援下列運算子方法的 hello:**新增**， **sub**， **mul**， **div**， **mod**， **floor**， **ceiling**，和**捨入**。 下列範例會篩選的資料表資料列，其中 hello hello**持續時間**是偶數。

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

您可以結合述詞與下列邏輯方法：**and**、**or** 和 **not**。 hello 下列範例會結合兩個 hello 前面範例。

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

群組和巢狀邏輯運算子︰

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

如需詳細討論和篩選的範例，請參閱[瀏覽的 hello Android 用戶端查詢模型的 hello 豐富][20]。

### <a name="sorting"></a>排序傳回的資料

hello 下列程式碼的所有項目從資料表傳回的**ToDoItems**排序按遞增 hello*文字*欄位。 *mToDoTable*是 hello 參考 toohello 後端的資料表，您先前建立：

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

hello 第一個參數的 hello **orderBy**方法是在哪個 toosort hello 欄位的字串相等 toohello 名稱。 hello 第二個參數使用 hello **QueryOrder**列舉 toospecify 是否 toosort 遞增或遞減。  如果要篩選使用 hello***其中***方法、 hello***其中***必須叫用方法之前 hello ***orderBy***方法。

### <a name="selection"></a>選取特定資料行

hello 下列程式碼說明 tooreturn 所有的資料表中的項目**ToDoItems**，但只會顯示 hello**完成**和**文字**欄位。 **mToDoTable**是 hello 參考 toohello 後端的資料表，我們在先前所建立。

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

hello 參數 toohello 選取函式是您想 tooreturn hello 資料表的資料行 hello 字串名稱。  hello**選取**方法需要等 toofollow 方法**其中**和**orderBy**。 而其後可以跟隨 **skip** 和 **top** 之類的分頁方法。

### <a name="paging"></a>以分頁方式傳回資料

資料**一律**以分頁方式傳回。  hello 傳回記錄的數目上限是由 hello 伺服器設定。  如果 hello 用戶端要求更多記錄，hello 伺服器就會傳回 hello 的記錄數目上限。  根據預設，hello hello 伺服器上的最大頁面大小是 50 筆記錄。

hello 第一個範例顯示如何 tooselect hello 從資料表的前五個項目。 hello 查詢傳回的資料表中的 hello 項目**ToDoItems**。 **mToDoTable**是 hello 參考 toohello 後端的資料表，您先前建立：

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

以下是查詢，便可略過 hello 前五個項目，然後傳回 hello 下一步的五個：

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

如果您想 tooget 所有記錄資料表中，實作程式碼 tooiterate 所有頁面上：

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

使用此方法的所有記錄的要求會建立兩個要求 toohello 行動應用程式後端的最小值。

> [!TIP]
> 選擇的 hello 正確的頁面大小為而發生 hello 要求的記憶體使用量、 頻寬使用量和延遲完全收到 hello 資料之間的平衡。  hello 預設 （50 筆記錄） 是適用於所有裝置。  如果您以獨佔方式在較大的記憶體裝置上運作，增加 too500 組成。  我們無法接受的延遲和大量記憶體的問題中發現該 hello 頁面大小增加超過 500 筆記錄的結果。

### <a name="chaining"></a>作法：串連查詢方法

可以串連 hello 方法用於查詢後端的資料表。 方法可讓您 tooselect 特定資料行的排序和分頁的已篩選資料列鏈結的查詢。 您可以建立複雜的邏輯篩選器。  每個查詢方法都會傳回 Query 物件。 tooend hello 系列的方法和實際執行的 hello 查詢中，呼叫 hello**執行**方法。 例如：

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

hello 鏈結的查詢的方法都必須排序，如下所示：

1. 篩選 (**where**) 方法。
2. 排序 (**orderBy**) 方法。
3. 選取 (**select**) 方法。
4. 分頁 (**skip** 和 **top**) 方法。

## <a name="binding"></a>繫結資料 toohello 使用者介面

資料繫結牽涉到三項要件：

* hello 資料來源
* hello 螢幕的配置
* hello 配接器，繫結 hello 兩個在一起。

在我們的範例程式碼，傳回 hello 資料從 hello 行動應用程式的 SQL Azure 資料表**ToDoItem**到陣列。 此活動是常見的資料應用模式。  資料庫查詢通常會傳回 hello 清單或陣列中的用戶端取得的資料列集合。 在此範例中，hello 陣列會是 hello 資料來源。  hello 程式碼會指定定義 hello 裝置出現的 hello 資料 hello 檢視畫面配置。  hello 兩個繫結以及配接器，它在這段程式碼中的 hello 延伸**ArrayAdapter&lt;ToDoItem&gt;** 類別。

#### <a name="layout"></a>定義 hello 版面配置

hello 版面配置是由數個 XML 程式碼片段定義。 指定現有的版面配置，下列程式碼的 hello 代表 hello **ListView**我們想 toopopulate 我們的伺服器資料。

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

在上述程式碼的 hello，hello *listitem*屬性指定的個別資料列的 hello 配置 hello 識別碼 hello 清單中。 此程式碼指定核取方塊和相關聯的文字，並取得具現化一次的 hello 清單中的每個項目。 這種配置不會顯示 hello**識別碼**欄位，以及更複雜的配置會顯示 hello 中指定的其他欄位。 此程式碼是在 hello **row_list_to_do.xml**檔案。

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

#### <a name="adapter"></a>定義 hello 配接器
因為我們檢視 hello 資料來源是陣列**ToDoItem**，我們子類別我們配接器從**ArrayAdapter&lt;ToDoItem&gt;** 類別。 這個子類別會產生一份檢視的每個**ToDoItem**使用 hello **row_list_to_do**版面配置。  在我們的程式碼中，我們會定義 hello 遵循 hello 的延伸模組類別**ArrayAdapter&lt;E&gt;** 類別：

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

覆寫 hello 配接器**getView**方法。 例如：

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

我們在「活動」中建立此類別的執行個體，如下所示：

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

hello 第二個參數 toohello ToDoItemAdapter 建構函式會參考 toohello 版面配置。 我們現在可以執行個體化 hello **ListView**並指派 hello 配接器 toohello **ListView**。

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>使用 hello 配接器 tooBind toohello UI

現在您已經準備就緒 toouse 資料繫結。 hello 下列程式碼顯示以 hello 資料表和填滿 tooget 項目如何 hello 本機介面卡以 hello 傳回項目。

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

呼叫 hello 配接器在任何時間修改 hello **ToDoItem**資料表。 修改是對個別記錄逐一執行的，因此您會處理單一資料列，而不是集合。 當您插入項目時，呼叫 hello**新增**方法 hello 配接器，則刪除時，呼叫 hello**移除**方法。

您可以在 hello 找到完整的範例[Android 快速入門專案][21]。

## <a name="inserting"></a>將資料插入 hello 後端

具現化執行個體的 hello *ToDoItem*類別，並設定其屬性。

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

然後使用**insert** tooinsert 物件：

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

hello 傳回實體的相符項目插入至 hello 後端的資料表、 包含的 hello 識別碼和任何其他值的 hello 資料 (例如 hello `createdAt`， `updatedAt`，和`version`欄位) 上 hello 後端設定。

Mobile Apps 資料表需要名為 **識別碼**的主索引鍵資料行。此資料行必須是字串。 hello hello ID 資料行的預設值是 GUID。  您可以提供其他的唯一值，例如電子郵件地址或使用者名稱。 當字串 ID 值未提供插入的記錄時，hello 後端會產生新的 GUID。

字串 ID 值會提供下列優點 hello:

* 可以產生識別碼，而不需要進行往返 toohello 資料庫。
* 更容易 toomerge 來自不同資料表或資料庫的記錄。
* 識別碼值與應用程式邏輯的整合更理想。

若要支援離線同步處理，則 **需要** 字串識別碼值。  一旦儲存 hello 後端資料庫中，您無法變更 Id。

## <a name="updating"></a>將行動裝置應用程式中的資料更新

tooupdate 資料在資料表中，將新物件 toohello hello **update （)**方法。

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

在此範例中，*項目*hello 一個參考 tooa 資料列*ToDoItem*有了一些變更 tooit 的資料表。  hello 資料列以 hello 相同**識別碼**會更新。

## <a name="deleting"></a>將行動裝置應用程式中的資料刪除

hello，下列程式碼顯示如何藉由指定資料表的資料 toodelete hello 資料物件。

```java
mToDoTable
    .delete(item);
```

您也可以刪除項目，藉由指定 hello**識別碼**hello 列 toodelete 欄位。

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>依識別碼查閱特定項目

尋找具有特定的項目**識別碼**欄位以 hello **Lookup**方法：

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>作法：使用不具類型的資料

hello 不具類型的程式設計模型可讓您完全控制 JSON 序列化。  有一些常見的案例，您可能希望 toouse 不具類型的程式設計模型。 例如，如果您的後端資料表包含許多資料行，而且您只需要 tooreference hello 資料行的子集。  hello 具類型的模型需要的 toodefine hello 的所有資料行定義中的資料類別中的 hello 行動應用程式後端。  大部分的應用程式開發介面呼叫，以存取資料的 hello 如下 toohello 輸入程式設計的呼叫。 hello 主要差異在於，hello 不具類型的模型中您可以叫用方法上 hello **MobileServiceJsonTable**物件，而不是 hello **MobileServiceTable**物件。

### <a name="json_instance"></a>建立不具型別的資料表執行個體

類似 toohello 具類型的模型，您一開始會取得資料表參考，但它是在此情況下**MobileServicesJsonTable**物件。 取得呼叫 hello hello 參考**getTable** hello 用戶端的執行個體上的方法：

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

一旦您建立執行個體的 hello **MobileServiceJsonTable**，它具有幾乎 hello hello 具類型的程式撰寫模型做為可用的相同 API。 在某些情況下，hello 方法會採用不具類型的參數，而不是具類型的參數。

### <a name="json_insert"></a>插入不具型別的資料表中
hello 下列程式碼會示範如何 toodo 插入。 hello 第一個步驟是 toocreate [JsonObject][1]，屬於 hello [gson] [ 3]程式庫。

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

然後，使用**insert** hello 資料表 tooinsert hello 不具型別的的物件。

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

如果您需要 tooget hello 識別碼 hello 插入物件，使用 hello **getAsJsonPrimitive()**方法。

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>在不具型別的資料表中進行刪除
hello 下列程式碼會示範如何 toodelete 執行個體，在此情況下，hello 相同的執行個體**JsonObject**中 hello 之前建立*插入*範例。 hello 程式碼為 hello hello 與輸入案例中，但 hello 方法具有不同的簽章，因為它會參考**JsonObject**。

```java
mToDoTable
    .delete(insertedItem);
```

您也可以直接使用 ID 來刪除執行個體：

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>從不具型別的資料表傳回所有資料列
hello 下列程式碼會示範如何 tooretrieve 整個資料表。 因為您使用 JSON 資料表，您可以選擇性地擷取只有部分 hello 資料表的資料行。

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

hello 組相同的篩選、 篩選和分頁可用於 hello 具型別模型的方法可供 hello 不具類型的模型。

## <a name="offline-sync"></a>實作離線同步處理

hello Azure 行動應用程式用戶端 SDK 也會實作離線的資料同步處理本機使用 SQLite 資料庫 toostore hello 伺服器資料的複本。  離線的資料表上執行的作業不需要行動裝置的連線能力 toowork。  離線同步處理有助於彈性且更複雜的邏輯解決衝突的 hello 費用的效能。  hello Azure 行動應用程式用戶端 SDK 實作 hello 下列功能：

* 增量同步處理︰只會下載更新和新的記錄，可節省頻寬和記憶體耗用量。
* 開放式並行存取： 作業會假設 toosucceed。  衝突解決會延遲，直到 hello 伺服器上執行更新。
* 衝突解決方式： hello SDK 偵測到衝突的變更已在 hello 伺服器，並提供勾點 tooalert hello 使用者。
* 虛刪除： 已刪除的記錄會標示為已刪除，讓其他裝置 tooupdate 其離線快取的。

### <a name="initialize-offline-sync"></a>將離線同步處理初始化

每個離線的資料表必須定義在 hello 離線快取，才能使用。  一般而言，資料表定義是在 hello 用戶端 hello 建立後立即完成：

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

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>取得參考 toohello 離線快取表格

如需線上資料表，請使用 `.getTable()`。  如需離線資料表，請使用 `.getSyncTable()`：

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

所有 hello 可用方法的平均工作 （包括篩選、 排序、 分頁、 將資料插入、 更新資料，和刪除資料） 的線上資料表在線上或離線的資料表。

### <a name="synchronize-hello-local-offline-cache"></a>同步處理 hello 本機離線快取

同步處理是您的應用程式的 hello 控制項內。  以下是同步處理方法的範例︰

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

如果有提供查詢名稱 toohello`.pull(query, queryname)`方法，則增量同步處理是使用的 tooreturn 只記錄已建立或最後一次順利完成的 hello 提取之後變更。

### <a name="handle-conflicts-during-offline-synchronization"></a>處理離線同步處理期間的衝突

如果在 `.push()` 作業期間發生衝突，就會擲回 `MobileServiceConflictException`。   hello 伺服器所發行的項目內嵌在 hello 例外狀況，而且可以藉由擷取`.getItem()`hello 例外狀況。  調整 hello 推入，由下列項目 hello MobileServiceSyncContext 物件上呼叫 hello:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

在您希望的位置，有標示為所有衝突之後, 再呼叫`.push()`再次 tooresolve 所有 hello 衝突。

## <a name="custom-api"></a>呼叫自訂 API

自訂 API 可讓您 toodefine 自訂端點來公開伺服器功能並不對應 tooan 插入、 更新、 刪除或讀取作業。 透過使用自訂 API，您可以進一步控制訊息，包括讀取與設定 HTTP 訊息標頭，並定義除了 JSON 以外的訊息內文格式。

從 Android 用戶端，您可以呼叫 hello **invokeApi**方法 toocall hello 自訂 API 端點。 hello 下列範例示範如何 toocall API 端點命名**completeAll**，它會傳回名為的集合類別**MarkAllResult**。

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

hello **invokeApi** hello 用戶端，傳送 POST 要求 toohello 新的自訂 API 上呼叫方法。 hello hello 自訂 API 所傳回的結果會顯示在訊息對話方塊中中,，為任何錯誤。 其他版本的**invokeApi**可讓您選擇性地傳送 hello 要求主體中的物件，指定 hello HTTP 方法，並傳送 hello 要求與查詢參數。 也會提供不具型別的版本 **invokeApi** 。

## <a name="authentication"></a>新增驗證 tooyour 應用程式

詳細的教學課程已說明如何 tooadd 這些功能。

App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶、Twitter 以及 Azure Active Directory) 來 [驗證應用程式使用者](app-service-mobile-android-get-started-users.md)。 您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。 您也可以使用 hello 身分識別通過驗證的使用者 tooimplement 授權規則的後端中。

支援兩個驗證流程：**伺服器**流程和**用戶端**流程。 hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 身分識別提供者 web 介面。  沒有其他 Sdk 是必要的 tooimplement 伺服器流程驗證。 伺服器流程驗證不會提供深層整合 hello 行動裝置，且只建議證明的情況。

因為它是倚賴 hello 身分識別提供者所提供的 Sdk hello 用戶端流程能裝置特定功能，例如單一登入的整合更加深入。  例如，您可以將 hello Facebook SDK 整合行動應用程式。  hello 行動用戶端交換到 hello Facebook 應用程式，並確認您登入前交換後 tooyour 行動裝置應用程式。

四個步驟是在您的應用程式的必要的 tooenable 驗證：

* 對識別提供者註冊應用程式以進行驗證。
* 設定 App Service 後端。
* 限制只在 hello 應用程式服務後端的資料表權限 tooauthenticated 使用者存取。
* 加入驗證程式碼 tooyour 應用程式。

您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。 您也可以使用 hello 的已驗證的使用者 toomodify SID 的要求。  如需詳細資訊，請檢閱[開始使用驗證]和 hello 伺服器 SDK 如何文件。

### <a name="caching"></a>驗證︰伺服器流程

hello 下列程式碼會啟動使用 hello Google 提供者伺服器流程登入程序。  因為 hello hello Google 提供者的安全性需求，則需要其他組態：

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

此外，新增下列方法 toohello 主要活動類別的 hello:

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

hello`GOOGLE_LOGIN_REQUEST_CODE`定義您的 main 中活動用於 hello`login()`方法內 hello`onActivityResult()`方法。  您可以選擇任何唯一的數字，只要 hello 使用相同的號碼 hello 內`login()`方法和 hello`onActivityResult()`方法。  如果您的服務配接器 （如稍早所示） 到抽象 hello 用戶端程式碼，您應該 hello service 配接器上呼叫 hello 適當的方法。

您也需 customtabs tooconfigure hello 專案。  先指定重新導向 URL。  新增下列程式碼片段太 hello`AndroidManifest.xml`:

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

新增 hello **redirectUriScheme** toohello`build.gradle`應用程式的檔案：

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

最後，會加入`com.android.support:customtabs:23.0.1`toohello 依存性清單中 hello`build.gradle`檔案：

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

取得 hello 識別碼 hello 登入的使用者從**MobileServiceUser**使用 hello **getUserId**方法。 如需 toouse 未來 toocall 如何 hello 非同步登入應用程式開發介面的範例，請參閱[開始使用驗證]。

> [!WARNING]
> hello 提及的 URL 配置是區分大小寫。  確認所有出現的 `{url_scheme_of_you_app}` 大小寫相符。

### <a name="caching"></a>快取驗證權杖

快取驗證權杖會要求您 toostore hello 使用者識別碼和 hello 裝置本機上的驗證 token。 hello 下次 hello 應用程式啟動時，您檢查 hello 快取，和如果這些值都存在，則可以略過 hello 程序中的記錄檔，並解除凍結 hello 用戶端使用此資料。 不過這項資料是區分大小寫，而且應該儲存以防 hello 電話遭竊，安全的加密。  您可以看到 toocache 驗證中的語彙基元的完整範例[快取驗證權杖 區段][7]。

當您嘗試 toouse 過期的權杖時，您會收到*401 未經授權的*回應。 您可以使用篩選器處理驗證錯誤。  篩選條件攔截要求 toohello 應用程式服務後端。 hello 篩選程式碼測試 401 回應 hello、 觸發程序 hello 登入程序，然後會繼續產生 hello 401 hello 要求。

### <a name="refresh"></a>使用重新整理權杖

傳回的 Azure 應用程式服務驗證和授權的 hello token 具有一小時已定義的存留時間。  在這段期間之後, 您必須重新驗證 hello 使用者。  如果您是使用長時間執行的語彙基元，您收到透過用戶端流程驗證，則您可以重新驗證與 Azure 應用程式服務驗證並授權使用 hello 相同的語彙基元。  所產生的另一個 Azure App Service 權杖會含有新的存留期。

您也可以註冊 hello 提供者 toouse 重新整理語彙基元。  重新整理權杖並非一律可用。  需要進行其他設定：

* 如**Azure Active Directory**，設定 hello Azure Active Directory 應用程式的用戶端密碼。  設定 Azure Active Directory 驗證時，請指定 hello Azure App Service 中的 hello 用戶端密碼。  呼叫 `.login()` 時，傳遞 `response_type=code id_token` 作為參數︰

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* 如**Google**，傳遞 hello`access_type=offline`做為參數：

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* 如**Microsoft 帳戶**，選取 hello`wl.offline_access`範圍。

toorefresh 語彙基元，呼叫`.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

最佳作法是建立的篩選條件會偵測 hello 伺服器 401 回應，並嘗試 toorefresh hello 使用者 token。

## <a name="log-in-with-client-flow-authentication"></a>使用用戶端流程驗證登入

hello 登入用戶端流量驗證的一般程序如下所示：

* 以您設定伺服器流程驗證的相同方式設定 Azure App Service 驗證與授權。
* 整合 hello 驗證提供者 SDK 驗證 tooproduce 存取權杖。
* 呼叫 hello`.login()`方法，如下所示：

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

取代 hello`onSuccess()`方法的任何程式碼您希望 toouse 成功登入。  hello`{provider}`字串是有效的提供者： **aad** (Azure Active Directory)， **facebook**， **google**， **microsoftaccount**，或**twitter**。  如果您實作自訂驗證，您可以也使用 hello 自訂驗證提供者的標記。

### <a name="adal"></a>驗證使用者以 hello Active Directory 驗證程式庫 (ADAL)

您可以使用 hello Active Directory 驗證程式庫 (ADAL) toosign 使用者將使用 Azure Active Directory 應用程式。 使用用戶端流量登入通常是最好的 toousing hello`loginAsync()`方法，因為它提供更原生的 UX 操作，並允許其他自訂。

1. 設定下列 hello AAD 登入您的行動裝置應用程式後端[tooconfigure Active Directory 登入服務的應用程式如何][ 22]教學課程。 請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。
2. 藉由修改下列定義您 build.gradle 檔案 tooinclude hello 安裝 ADAL:

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

1. 加入下列程式碼 tooyour 應用程式，進行下列取代 hello hello:

* 取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。 hello 格式應該是 https://login.microsoftonline.com/contoso.onmicrosoft.com。
* 取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。 您可以從 hello 取得 hello 用戶端識別碼**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。
* 取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。
* 取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。 此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。

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

## <a name="filters"></a>調整 hello 用戶端伺服器通訊

hello 用戶端連接通常是使用 hello 基礎 HTTP hello Android SDK 所提供的程式庫的基本 HTTP 連接。  有幾個原因為何，您會想 toochange 的：

* 您希望 toouse 替代 HTTP 程式庫 tooadjust 逾時。
* 您希望 tooprovide 進度列。
* 您希望 tooadd 自訂標頭 toosupport API 管理功能。
* 您希望 toointercept 失敗的回應，以便您可以實作重新驗證。
* 您希望 toolog 後端要求 tooan 分析服務。

### <a name="using-an-alternate-http-library"></a>使用替代的 HTTP 程式庫

呼叫 hello`.setAndroidHttpClientFactory()`之後立即建立用戶端參考的方法。  例如，tooset hello 連接逾時 too60 秒數 （而不是 hello 預設值 10 秒）：

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

### <a name="implement-a-progress-filter"></a>實作進度篩選條件

您可以藉由實作 `ServiceFilter` 來實作每個要求的攔截。  例如，下列 hello 更新預先建立的進度列：

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

您可以附加此篩選器 toohello 用戶端，如下所示：

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>自訂要求標頭

使用下列 hello`ServiceFilter`和附加 hello 中的 hello 篩選 hello 與相同的方式`ProgressFilter`:

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

### <a name="conversions"></a>設定自動序列化

您可以指定使用 hello 套用 tooevery 資料行的轉換策略[gson] [ 3]應用程式開發介面。 hello Android 用戶端程式庫會使用[gson] [ 3] hello 幕後 tooserialize Java 物件 tooJSON 資料 tooAzure App Service 傳送嗨資料之前。  hello 下列程式碼使用 hello **setFieldNamingStrategy()**方法 tooset hello 策略。 這個範例會刪除 hello 初始字元 ("m")，並接著小寫 hello 下一個字元，每個欄位名稱。 比方說，它會將「mId」變成「id」。  實作轉換策略 tooreduce hello 需要`SerializedName()`大部分欄位上的註解。

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

建立使用 hello 的行動用戶端參考之前，必須執行此程式碼**MobileServiceClient**。

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
