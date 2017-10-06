---
title: "aaaOn 內部部署應用程式使用 blob 儲存體 (Java) |Microsoft 文件"
description: "了解如何 toocreate 主控台應用程式上傳映像 tooAzure，然後按一下 顯示 hello 瀏覽器中的映像。 程式碼範例以 Java 撰寫。"
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="fb729-104">搭配 Blob 儲存體的內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="fb729-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="fb729-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fb729-105">Overview</span></span>
<span data-ttu-id="fb729-106">hello 下列範例示範您如何使用 Azure 儲存體來儲存在 Azure 中的映像。</span><span class="sxs-lookup"><span data-stu-id="fb729-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="fb729-107">這篇文章中的 hello 程式碼是為主控台應用程式，上傳映像 tooAzure，然後建立的 HTML 檔案，在您的瀏覽器中顯示 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="fb729-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb729-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb729-108">Prerequisites</span></span>
* <span data-ttu-id="fb729-109">已安裝 Java Developer Kit (JDK) 1.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fb729-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="fb729-110">hello Azure SDK 會安裝。</span><span class="sxs-lookup"><span data-stu-id="fb729-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="fb729-111">hello hello Azure libraries for Java JAR 和任何適用的相依性 （每瓶），會安裝，且位於 hello Java 編譯器所使用的組建路徑。</span><span class="sxs-lookup"><span data-stu-id="fb729-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="fb729-112">如需安裝 hello Azure Libraries for Java 的資訊，請參閱[下載 hello Azure SDK for Java](../java-download-azure-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="fb729-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="fb729-113">已設定 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb729-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="fb729-114">hello 帳戶名稱和帳戶金鑰 hello 儲存體帳戶將供 hello 本文中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb729-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="fb729-115">請參閱[如何 tooCreate 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)如需建立儲存體帳戶資訊和[檢視與複製的儲存體存取金鑰](storage-create-storage-account.md#view-and-copy-storage-access-keys)如需擷取 hello 帳戶金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="fb729-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="fb729-116">您已建立名為本機映像檔案儲存在 hello path c:\\myimages\\image1.jpg。</span><span class="sxs-lookup"><span data-stu-id="fb729-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="fb729-117">此外，修改**FileInputStream** hello 範例 toouse 不同的影像路徑和檔案名稱中建構函式。</span><span class="sxs-lookup"><span data-stu-id="fb729-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="fb729-118">toouse Azure blob 儲存體 tooupload 檔案</span><span class="sxs-lookup"><span data-stu-id="fb729-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="fb729-119">以下為逐步程序。</span><span class="sxs-lookup"><span data-stu-id="fb729-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="fb729-120">如果您想要繼續 tooskip，hello 整個程式碼會在本文稍後。</span><span class="sxs-lookup"><span data-stu-id="fb729-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="fb729-121">開始 hello 程式碼，藉由匯入的 hello Azure 核心儲存類別、 hello Azure blob 的用戶端類別，hello Java IO 類別和 hello **URISyntaxException**類別。</span><span class="sxs-lookup"><span data-stu-id="fb729-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="fb729-122">宣告類別，名為**StorageSample**，並包含 hello 左括號**{**。</span><span class="sxs-lookup"><span data-stu-id="fb729-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="fb729-123">在 hello **StorageSample**類別中，宣告會包含 hello 預設端點的通訊協定，您的儲存體帳戶名稱和儲存體存取金鑰，Azure 儲存體帳戶中所指定的字串變數。</span><span class="sxs-lookup"><span data-stu-id="fb729-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="fb729-124">取代 hello 預留位置值**您\_帳戶\_名稱**和**您\_帳戶\_金鑰**使用您自己的帳戶名稱和帳戶金鑰分別。</span><span class="sxs-lookup"><span data-stu-id="fb729-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="fb729-125">為您宣告中，加入**主要**，包括**再試一次**區塊，並包含 hello 必要左括弧， **{**。</span><span class="sxs-lookup"><span data-stu-id="fb729-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="fb729-126">宣告變數的 hello 下列型別 (描述是在此範例中的使用方式的 hello):</span><span class="sxs-lookup"><span data-stu-id="fb729-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="fb729-127">**CloudStorageAccount**： 使用的 tooinitialize hello 帳戶與您的 Azure 儲存體帳戶名稱和金鑰，toocreate 物件 blob 用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="fb729-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="fb729-128">**CloudBlobClient**： 使用 tooaccess hello blob 服務。</span><span class="sxs-lookup"><span data-stu-id="fb729-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="fb729-129">**CloudBlobContainer**： 使用的 toocreate blob 容器、 列出 hello 容器和刪除 hello 容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="fb729-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="fb729-130">**CloudBlockBlob**： 使用的 tooupload 本機映像檔案 toothe 容器。</span><span class="sxs-lookup"><span data-stu-id="fb729-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="fb729-131">指派值 toohello**帳戶**變數。</span><span class="sxs-lookup"><span data-stu-id="fb729-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="fb729-132">指派值 toohello **serviceClient**變數。</span><span class="sxs-lookup"><span data-stu-id="fb729-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="fb729-133">指派值 toohello**容器**變數。</span><span class="sxs-lookup"><span data-stu-id="fb729-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="fb729-134">我們會取得名為參考 tooa 容器**gettingstarted**。</span><span class="sxs-lookup"><span data-stu-id="fb729-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="fb729-135">建立 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="fb729-135">Create hello container.</span></span> <span data-ttu-id="fb729-136">如果不存在，這個方法會建立 hello 容器 (和傳回**true**)。</span><span class="sxs-lookup"><span data-stu-id="fb729-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="fb729-137">如果存在 hello 容器，它會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="fb729-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="fb729-138">替代太**createIfNotExists**為 hello**建立**方法 （如果 hello 容器已經存在，則會傳回錯誤）。</span><span class="sxs-lookup"><span data-stu-id="fb729-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="fb729-139">設定 hello 容器的匿名存取。</span><span class="sxs-lookup"><span data-stu-id="fb729-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="fb729-140">取得代表 Azure 儲存體中的 hello blob 參考 toohello 區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="fb729-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="fb729-141">使用 hello**檔案**建構函式 tooget 參照 toohello 在本機建立的檔案，您將上傳。</span><span class="sxs-lookup"><span data-stu-id="fb729-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="fb729-142">請確定您已執行 hello 程式碼之前先建立這個檔案。</span><span class="sxs-lookup"><span data-stu-id="fb729-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="fb729-143">透過呼叫 toohello hello 本機檔案上傳**CloudBlockBlob.upload**方法。</span><span class="sxs-lookup"><span data-stu-id="fb729-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="fb729-144">hello 第一個參數 toohello **CloudBlockBlob.upload**方法**FileInputStream**物件，代表 hello 本機檔案可上傳 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fb729-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="fb729-145">hello 第二個參數是 hello 大小，以位元組為單位 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="fb729-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="fb729-146">呼叫 helper 函式，名為**MakeHTMLPage**，toomake 基本 HTML 頁面，其中包含**&lt;映像&gt;** hello 來源組 toohello blob，現在已在 Azure 中的項目儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb729-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="fb729-147">hello 碼**MakeHTMLPage**將在本文稍後討論。</span><span class="sxs-lookup"><span data-stu-id="fb729-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="fb729-148">列印時的狀態訊息和 hello 建立 HTML 網頁的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fb729-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="fb729-149">關閉 hello**再試一次**區塊插入右括弧： **}**</span><span class="sxs-lookup"><span data-stu-id="fb729-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="fb729-150">處理 hello 下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="fb729-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="fb729-151">**FileNotFoundException**： 可能會擲回 hello **FileInputStream**或**FileOutputStream**建構函式。</span><span class="sxs-lookup"><span data-stu-id="fb729-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="fb729-152">**StorageException**: hello Azure 用戶端儲存體程式庫所擲回。</span><span class="sxs-lookup"><span data-stu-id="fb729-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="fb729-153">**URISyntaxException**： 可能會擲回 hello **ListBlobItem.getUri**方法。</span><span class="sxs-lookup"><span data-stu-id="fb729-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="fb729-154">**Exception**：一般例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="fb729-154">**Exception**: Generic exception handling.</span></span>

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="fb729-155">透過插入右括號 **}** 來結束 **main**</span><span class="sxs-lookup"><span data-stu-id="fb729-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="fb729-156">建立名為方法**MakeHTMLPage** toocreate 基本 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="fb729-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="fb729-157">這個方法有一個參數類型**CloudBlobContainer**，這將會使用的 tooiterate 透過 hello 已上傳的 blob 清單。</span><span class="sxs-lookup"><span data-stu-id="fb729-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="fb729-158">這個方法會擲回例外狀況型別的**FileNotFoundException**，這可能會擲回的 hello **FileOutputStream**建構函式，和**URISyntaxException**，如此可能擲回的 hello **ListBlobItem.getUri**方法。</span><span class="sxs-lookup"><span data-stu-id="fb729-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="fb729-159">加上左括號 **{**。</span><span class="sxs-lookup"><span data-stu-id="fb729-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="fb729-160">建立名為 **index.html**的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="fb729-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="fb729-161">寫入 toohello 本機檔案，加入在 hello  **&lt;html&gt;**， **&lt;標頭&gt;**，和**&lt;主體&gt;**項目。</span><span class="sxs-lookup"><span data-stu-id="fb729-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="fb729-162">逐一查看 hello 已上傳的 blob 清單。</span><span class="sxs-lookup"><span data-stu-id="fb729-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="fb729-163">每個 blob，hello HTML 頁面中建立 **&lt;img&gt;** 具有項目，其**src**傳送給 hello hello blob URI，存在於您的 Azure 儲存體帳戶中的屬性。</span><span class="sxs-lookup"><span data-stu-id="fb729-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="fb729-164">雖然您在此範例中僅新增一張影像，如果您要新增多張，此程式碼需要重複列舉全部影像。</span><span class="sxs-lookup"><span data-stu-id="fb729-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="fb729-165">為了方便起見，此範例假設每個已上傳的 Blob 是一張影像。</span><span class="sxs-lookup"><span data-stu-id="fb729-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="fb729-166">如果您已更新映像以外的 blob 或分頁 blob，而不是區塊 blob，調整 hello 程式碼所需。</span><span class="sxs-lookup"><span data-stu-id="fb729-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="fb729-167">關閉 hello **&lt;主體&gt;**元素與 hello  **&lt;html&gt;** 項目。</span><span class="sxs-lookup"><span data-stu-id="fb729-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="fb729-168">關閉 hello 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="fb729-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="fb729-169">透過插入右括號 **}** 來結束 **MakeHTMLPage**</span><span class="sxs-lookup"><span data-stu-id="fb729-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="fb729-170">透過插入右括號 **}** 來結束 **StorageSample**</span><span class="sxs-lookup"><span data-stu-id="fb729-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="fb729-171">hello 以下是 hello 這個範例的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb729-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="fb729-172">請記住 toomodify hello 預留位置值**您\_帳戶\_名稱**和**您\_帳戶\_金鑰**toouse 您的帳戶名稱和帳戶索引鍵，分別。</span><span class="sxs-lookup"><span data-stu-id="fb729-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="fb729-173">在加法 toouploading 您本機的映像檔案 tooAzure 存放裝置 hello 範例程式碼會建立本機檔案 namedindex.html，您可以開啟瀏覽器 toosee 中上傳的影像。</span><span class="sxs-lookup"><span data-stu-id="fb729-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="fb729-174">由於 hello 程式碼包含您的帳戶名稱和帳戶金鑰，確定您的程式碼是安全。</span><span class="sxs-lookup"><span data-stu-id="fb729-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="fb729-175">toodelete 容器</span><span class="sxs-lookup"><span data-stu-id="fb729-175">toodelete a container</span></span>
<span data-ttu-id="fb729-176">因為您將支付儲存體，您可能需要 toodelete **gettingstarted**容器完成後的實驗順利進行此範例。</span><span class="sxs-lookup"><span data-stu-id="fb729-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="fb729-177">toodelete 容器，使用 hello **CloudBlobContainer.delete**方法。</span><span class="sxs-lookup"><span data-stu-id="fb729-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="fb729-178">toocall hello **CloudBlobContainer.delete**方法、 hello 程序初始化**CloudStorageAccount**， **ClodBlobClient**，和**CloudBlobContainer**物件是 hello 與顯示相同**createIfNotExist**方法。</span><span class="sxs-lookup"><span data-stu-id="fb729-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="fb729-179">hello 以下是刪除 hello 命名容器的完整範例**gettingstarted**。</span><span class="sxs-lookup"><span data-stu-id="fb729-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

<span data-ttu-id="fb729-180">如需其他 blob 儲存體類別和方法的概觀，請參閱[如何從 Java 的 Blob 儲存體 toouse](storage-java-how-to-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="fb729-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb729-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb729-181">Next steps</span></span>
<span data-ttu-id="fb729-182">請遵循這些連結 toolearn 深入了解更複雜的儲存體工作。</span><span class="sxs-lookup"><span data-stu-id="fb729-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="fb729-183">Azure Storage SDK for Java</span><span class="sxs-lookup"><span data-stu-id="fb729-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="fb729-184">Azure 儲存體用戶端 SDK 參考</span><span class="sxs-lookup"><span data-stu-id="fb729-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="fb729-185">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="fb729-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="fb729-186">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="fb729-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

