---
title: "搭配 Blob 儲存體 (Java) 的內部部署應用程式 | Microsoft Docs"
description: "了解如何建立可將影像上傳至 Azure，然後在瀏覽器中顯示此影像的主控台應用程式。 程式碼範例以 Java 撰寫。"
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="f15b3-104">搭配 Blob 儲存體的內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="f15b3-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="f15b3-105">Overview</span><span class="sxs-lookup"><span data-stu-id="f15b3-105">Overview</span></span>
<span data-ttu-id="f15b3-106">下列範例說明如何使用 Azure 儲存體，在 Azure 中儲存影像。</span><span class="sxs-lookup"><span data-stu-id="f15b3-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="f15b3-107">本文中的程式碼適用於主控台應用程式，可將影像上傳至 Azure，然後建立可在瀏覽器中顯示此影像的 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f15b3-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f15b3-108">Prerequisites</span></span>
* <span data-ttu-id="f15b3-109">已安裝 Java Developer Kit (JDK) 1.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f15b3-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="f15b3-110">已安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="f15b3-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="f15b3-111">已安裝 Azure Libraries for Java 的 JAR 和任何適用的相依性 JAR，且位於 Java 編輯器所使用的組建路徑中。</span><span class="sxs-lookup"><span data-stu-id="f15b3-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="f15b3-112">如需安裝 Azure Libraries for Java 的詳細資訊，請參閱 [下載 Azure SDK for Java](../java-download-azure-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="f15b3-113">已設定 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f15b3-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="f15b3-114">本文中的程式碼將會使用此儲存體帳戶的帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="f15b3-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="f15b3-115">如需建立儲存體帳戶的詳細資訊，請參閱[如何建立儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)，如需擷取帳戶金鑰的詳細資訊，請參閱[如何檢視並複製儲存體存取金鑰](storage-create-storage-account.md#view-and-copy-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="f15b3-116">您已建立一個已命名並儲存於路徑 c:\\myimages\\image1.jpg 中的本機映像檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="f15b3-117">或者，修改範例中的 **FileInputStream** 建構函式以使用其他影像路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="f15b3-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="f15b3-118">使用 Azure Blob 儲存體上傳檔案</span><span class="sxs-lookup"><span data-stu-id="f15b3-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="f15b3-119">以下為逐步程序。</span><span class="sxs-lookup"><span data-stu-id="f15b3-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="f15b3-120">如果您希望跳過此程序，也能在本文後續內容中看到完整的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f15b3-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="f15b3-121">透過包含匯入 Azure 核心儲存體類別、Azure Blob 用戶端類別、Java IO 類別和 **URISyntaxException** 類別來開始程式碼。</span><span class="sxs-lookup"><span data-stu-id="f15b3-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="f15b3-122">宣告名為 **StorageSample** 的類別，並加上左括號 **{**。</span><span class="sxs-lookup"><span data-stu-id="f15b3-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="f15b3-123">在 **StorageSample** 類別中，宣告將包含預設端點通訊協定、儲存體帳戶名稱和儲存體存取金鑰 (如您 Azure 儲存體帳戶中所指定) 的字串變數。</span><span class="sxs-lookup"><span data-stu-id="f15b3-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="f15b3-124">分別以您自己的帳戶名稱和帳戶金鑰取代預留位置值 **your\_account\_name** 和 **your\_account\_key**。</span><span class="sxs-lookup"><span data-stu-id="f15b3-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="f15b3-125">將您的宣告加入 **main** 中，包括 **try** 區塊，以及加上必要的左括號 **{**。</span><span class="sxs-lookup"><span data-stu-id="f15b3-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="f15b3-126">宣告下列類型的變數 (以下說明乃是針對他們在此範例中的用途)：</span><span class="sxs-lookup"><span data-stu-id="f15b3-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="f15b3-127">**CloudStorageAccount**：可用來以 Azure 儲存體帳戶名稱和金鑰初始化帳戶物件，並可用來建立 Blob 用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="f15b3-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="f15b3-128">**CloudBlobClient**：可用來存取 Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="f15b3-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="f15b3-129">**CloudBlobContainer**：可用來建立 Blob 容器、列出容器中的 Blob，和刪除容器。</span><span class="sxs-lookup"><span data-stu-id="f15b3-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="f15b3-130">**CloudBlockBlob**：可用來將本機影像檔案上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="f15b3-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="f15b3-131">對 **account** 變數指定值。</span><span class="sxs-lookup"><span data-stu-id="f15b3-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="f15b3-132">對 **serviceClient** 變數指定值。</span><span class="sxs-lookup"><span data-stu-id="f15b3-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="f15b3-133">對 **container** 變數指定值。</span><span class="sxs-lookup"><span data-stu-id="f15b3-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="f15b3-134">我們將取得名為 **gettingstarted**的容器參照。</span><span class="sxs-lookup"><span data-stu-id="f15b3-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="f15b3-135">// 建立容器。</span><span class="sxs-lookup"><span data-stu-id="f15b3-135">Create the container.</span></span> <span data-ttu-id="f15b3-136">如果容器不存在，此方法將會建立容器 (並傳回 **true**)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="f15b3-137">如果容器存在，則會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="f15b3-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="f15b3-138">**createIfNotExists** 的替代方式是 **create** 方法 (如果容器已存在，將傳回錯誤訊息)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="f15b3-139">設定容器的匿名存取。</span><span class="sxs-lookup"><span data-stu-id="f15b3-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="f15b3-140">取得區塊 Blob 的參照，此參照將可代表 Azure 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="f15b3-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="f15b3-141">使用 **File** 建構函式，來取得在本機建立且即將上傳之檔案的參照。</span><span class="sxs-lookup"><span data-stu-id="f15b3-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="f15b3-142">執行此程式碼之前，請確定您已建立此檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="f15b3-143">透過呼叫 **CloudBlockBlob.upload** 方法來上傳本機檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="f15b3-144">**CloudBlockBlob.upload** 方法的第一個參數是 **FileInputStream** 物件，代表將上傳至 Azure 儲存體的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="f15b3-145">第二個參數是檔案的大小 (位元組)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="f15b3-146">呼叫名為 **MakeHTMLPage** 的協助程式函數來製作基本的 HTML 頁面，此頁面將包含 **&lt;image&gt;** 元素，且來源設定為目前位於您 Azure 儲存體帳戶中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="f15b3-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="f15b3-147">我們將在本文後面討論 **MakeHTMLPage** 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f15b3-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="f15b3-148">列印關於已建立之 HTML 頁面的狀態訊息和相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f15b3-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="f15b3-149">透過插入右括號 **}** 來結束 **try** 區塊</span><span class="sxs-lookup"><span data-stu-id="f15b3-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="f15b3-150">處理下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="f15b3-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="f15b3-151">**FileNotFoundException**：**FileInputStream** 或 **FileOutputStream** 建構函式可能擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f15b3-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="f15b3-152">**StorageException**：Azure 用戶端儲存體程式庫可能擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f15b3-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="f15b3-153">**URISyntaxException**：**ListBlobItem.getUri** 方法可能擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f15b3-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="f15b3-154">**Exception**：一般例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f15b3-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="f15b3-155">透過插入右括號 **}** 來結束 **main**</span><span class="sxs-lookup"><span data-stu-id="f15b3-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="f15b3-156">建立名為 **MakeHTMLPage** 的方法，藉此建立基本的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="f15b3-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="f15b3-157">此方法包含參數類型 **CloudBlobContainer**，可用來逐一取得已上傳的 Blob 清單。</span><span class="sxs-lookup"><span data-stu-id="f15b3-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="f15b3-158">此方法將擲回例外狀況類型 **FileNotFoundException** (**FileOutputStream** 建構函式可能擲回的例外狀況) 和 **URISyntaxException** (**ListBlobItem.getUri** 方法可能擲回的例外狀況)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="f15b3-159">加上左括號 **{**。</span><span class="sxs-lookup"><span data-stu-id="f15b3-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="f15b3-160">建立名為 **index.html**的本機檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="f15b3-161">寫入本機檔案，加入 **&lt;html&gt;**、**&lt;header&gt;** 和 **&lt;body&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="f15b3-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="f15b3-162">逐一取得已上傳的 Blob 清單。</span><span class="sxs-lookup"><span data-stu-id="f15b3-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="f15b3-163">在 HTML 頁面中，為每個 Blob 建立一個 **&lt;img&gt;** 元素，並將其 **src** 屬性傳送至 Azure 儲存體帳戶中之 Blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="f15b3-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="f15b3-164">雖然您在此範例中僅新增一張影像，如果您要新增多張，此程式碼需要重複列舉全部影像。</span><span class="sxs-lookup"><span data-stu-id="f15b3-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="f15b3-165">為了方便起見，此範例假設每個已上傳的 Blob 是一張影像。</span><span class="sxs-lookup"><span data-stu-id="f15b3-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="f15b3-166">如果您已更新除了影像以外的 Blob，或分頁 Blob 而非區塊 Blob，則請視需要調整程式碼。</span><span class="sxs-lookup"><span data-stu-id="f15b3-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="f15b3-167">結束 **&lt;body&gt;** 元素和 **&lt;html&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="f15b3-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="f15b3-168">關閉本機檔案。</span><span class="sxs-lookup"><span data-stu-id="f15b3-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="f15b3-169">透過插入右括號 **}** 來結束 **MakeHTMLPage**</span><span class="sxs-lookup"><span data-stu-id="f15b3-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="f15b3-170">透過插入右括號 **}** 來結束 **StorageSample**</span><span class="sxs-lookup"><span data-stu-id="f15b3-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="f15b3-171">下列是此範例的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="f15b3-171">The following is the complete code for this example.</span></span> <span data-ttu-id="f15b3-172">請記得修改預留位置值 **your\_account\_name** 和 **your\_account\_key**，以便分別使用您的帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="f15b3-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="f15b3-173">除了將本機影像檔案上傳至 Azure 儲存體以外，此範例程式碼還會建立本機檔案 namedindex.html，您可在瀏覽器中開啟此檔案以查看已上傳影像。</span><span class="sxs-lookup"><span data-stu-id="f15b3-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="f15b3-174">因為此程式碼包含您的帳戶名稱和帳戶金鑰，請確定您的來源程式碼安全無虞。</span><span class="sxs-lookup"><span data-stu-id="f15b3-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="f15b3-175">刪除容器</span><span class="sxs-lookup"><span data-stu-id="f15b3-175">To delete a container</span></span>
<span data-ttu-id="f15b3-176">由於您需支付儲存體的費用，因此，在您完成體驗此範例之後，您可能會想要刪除 **gettingstarted** 容器。</span><span class="sxs-lookup"><span data-stu-id="f15b3-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="f15b3-177">若要刪除容器，請使用 **CloudBlobContainer.delete** 方法。</span><span class="sxs-lookup"><span data-stu-id="f15b3-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="f15b3-178">若要呼叫 **CloudBlobContainer.delete** 方法，初始化 **CloudStorageAccount**、**ClodBlobClient** 及 **CloudBlobContainer** 物件的程序與為 **createIfNotExist** 方法所顯示的程序相同。</span><span class="sxs-lookup"><span data-stu-id="f15b3-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="f15b3-179">下列是刪除名為 **gettingstarted**之容器的完整範例。</span><span class="sxs-lookup"><span data-stu-id="f15b3-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="f15b3-180">如需其他 Blob 儲存體類別和方法的概觀，請參閱 [如何使用 Java 的 Blob 儲存體](storage-java-how-to-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f15b3-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f15b3-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f15b3-181">Next steps</span></span>
<span data-ttu-id="f15b3-182">請遵循下列連結以深入了解更複雜的儲存體工作。</span><span class="sxs-lookup"><span data-stu-id="f15b3-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="f15b3-183">Azure Storage SDK for Java</span><span class="sxs-lookup"><span data-stu-id="f15b3-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="f15b3-184">Azure 儲存體用戶端 SDK 參考</span><span class="sxs-lookup"><span data-stu-id="f15b3-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="f15b3-185">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="f15b3-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="f15b3-186">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="f15b3-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

