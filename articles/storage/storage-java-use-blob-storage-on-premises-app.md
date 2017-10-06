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
# <a name="on-premises-application-with-blob-storage"></a>搭配 Blob 儲存體的內部部署應用程式
## <a name="overview"></a>概觀
hello 下列範例示範您如何使用 Azure 儲存體來儲存在 Azure 中的映像。 這篇文章中的 hello 程式碼是為主控台應用程式，上傳映像 tooAzure，然後建立的 HTML 檔案，在您的瀏覽器中顯示 hello 映像。

## <a name="prerequisites"></a>必要條件
* 已安裝 Java Developer Kit (JDK) 1.6 版或更新版本。
* hello Azure SDK 會安裝。
* hello hello Azure libraries for Java JAR 和任何適用的相依性 （每瓶），會安裝，且位於 hello Java 編譯器所使用的組建路徑。 如需安裝 hello Azure Libraries for Java 的資訊，請參閱[下載 hello Azure SDK for Java](../java-download-azure-sdk.md)。
* 已設定 Azure 儲存體帳戶。 hello 帳戶名稱和帳戶金鑰 hello 儲存體帳戶將供 hello 本文中的程式碼。 請參閱[如何 tooCreate 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)如需建立儲存體帳戶資訊和[檢視與複製的儲存體存取金鑰](storage-create-storage-account.md#view-and-copy-storage-access-keys)如需擷取 hello 帳戶金鑰資訊。
* 您已建立名為本機映像檔案儲存在 hello path c:\\myimages\\image1.jpg。 此外，修改**FileInputStream** hello 範例 toouse 不同的影像路徑和檔案名稱中建構函式。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>toouse Azure blob 儲存體 tooupload 檔案
以下為逐步程序。 如果您想要繼續 tooskip，hello 整個程式碼會在本文稍後。

開始 hello 程式碼，藉由匯入的 hello Azure 核心儲存類別、 hello Azure blob 的用戶端類別，hello Java IO 類別和 hello **URISyntaxException**類別。

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

宣告類別，名為**StorageSample**，並包含 hello 左括號**{**。

```java
public class StorageSample {
```

在 hello **StorageSample**類別中，宣告會包含 hello 預設端點的通訊協定，您的儲存體帳戶名稱和儲存體存取金鑰，Azure 儲存體帳戶中所指定的字串變數。 取代 hello 預留位置值**您\_帳戶\_名稱**和**您\_帳戶\_金鑰**使用您自己的帳戶名稱和帳戶金鑰分別。

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

為您宣告中，加入**主要**，包括**再試一次**區塊，並包含 hello 必要左括弧， **{**。

```java
    public static void main(String[] args)
    {
        try
        {
```

宣告變數的 hello 下列型別 (描述是在此範例中的使用方式的 hello):

* **CloudStorageAccount**： 使用的 tooinitialize hello 帳戶與您的 Azure 儲存體帳戶名稱和金鑰，toocreate 物件 blob 用戶端物件。
* **CloudBlobClient**： 使用 tooaccess hello blob 服務。
* **CloudBlobContainer**： 使用的 toocreate blob 容器、 列出 hello 容器和刪除 hello 容器中的 blob。
* **CloudBlockBlob**： 使用的 tooupload 本機映像檔案 toothe 容器。

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

指派值 toohello**帳戶**變數。

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

指派值 toohello **serviceClient**變數。

```java
serviceClient = account.createCloudBlobClient();
```

指派值 toohello**容器**變數。 我們會取得名為參考 tooa 容器**gettingstarted**。

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

建立 hello 容器。 如果不存在，這個方法會建立 hello 容器 (和傳回**true**)。 如果存在 hello 容器，它會傳回**false**。 替代太**createIfNotExists**為 hello**建立**方法 （如果 hello 容器已經存在，則會傳回錯誤）。

```java
container.createIfNotExists();
```

設定 hello 容器的匿名存取。

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

取得代表 Azure 儲存體中的 hello blob 參考 toohello 區塊 blob。

```java
blob = container.getBlockBlobReference("image1.jpg");
```

使用 hello**檔案**建構函式 tooget 參照 toohello 在本機建立的檔案，您將上傳。 請確定您已執行 hello 程式碼之前先建立這個檔案。

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

透過呼叫 toohello hello 本機檔案上傳**CloudBlockBlob.upload**方法。 hello 第一個參數 toohello **CloudBlockBlob.upload**方法**FileInputStream**物件，代表 hello 本機檔案可上傳 tooAzure 儲存體。 hello 第二個參數是 hello 大小，以位元組為單位 hello 檔案。

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

呼叫 helper 函式，名為**MakeHTMLPage**，toomake 基本 HTML 頁面，其中包含**&lt;映像&gt;** hello 來源組 toohello blob，現在已在 Azure 中的項目儲存體帳戶。 hello 碼**MakeHTMLPage**將在本文稍後討論。

```java
MakeHTMLPage(container);
```

列印時的狀態訊息和 hello 建立 HTML 網頁的相關資訊。

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

關閉 hello**再試一次**區塊插入右括弧： **}**

處理 hello 下列例外狀況：

* **FileNotFoundException**： 可能會擲回 hello **FileInputStream**或**FileOutputStream**建構函式。
* **StorageException**: hello Azure 用戶端儲存體程式庫所擲回。
* **URISyntaxException**： 可能會擲回 hello **ListBlobItem.getUri**方法。
* **Exception**：一般例外狀況處理。

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

透過插入右括號 **}** 來結束 **main**

建立名為方法**MakeHTMLPage** toocreate 基本 HTML 頁面。 這個方法有一個參數類型**CloudBlobContainer**，這將會使用的 tooiterate 透過 hello 已上傳的 blob 清單。 這個方法會擲回例外狀況型別的**FileNotFoundException**，這可能會擲回的 hello **FileOutputStream**建構函式，和**URISyntaxException**，如此可能擲回的 hello **ListBlobItem.getUri**方法。 加上左括號 **{**。

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

建立名為 **index.html**的本機檔案。

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

寫入 toohello 本機檔案，加入在 hello  **&lt;html&gt;**， **&lt;標頭&gt;**，和**&lt;主體&gt;**項目。

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

逐一查看 hello 已上傳的 blob 清單。 每個 blob，hello HTML 頁面中建立 **&lt;img&gt;** 具有項目，其**src**傳送給 hello hello blob URI，存在於您的 Azure 儲存體帳戶中的屬性。
雖然您在此範例中僅新增一張影像，如果您要新增多張，此程式碼需要重複列舉全部影像。

為了方便起見，此範例假設每個已上傳的 Blob 是一張影像。 如果您已更新映像以外的 blob 或分頁 blob，而不是區塊 blob，調整 hello 程式碼所需。

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

關閉 hello **&lt;主體&gt;**元素與 hello  **&lt;html&gt;** 項目。

```java
stream.println("</body>");
stream.println("</html>");
```

關閉 hello 本機檔案。

```java
stream.close();
```

透過插入右括號 **}** 來結束 **MakeHTMLPage**

透過插入右括號 **}** 來結束 **StorageSample**

hello 以下是 hello 這個範例的完整程式碼。 請記住 toomodify hello 預留位置值**您\_帳戶\_名稱**和**您\_帳戶\_金鑰**toouse 您的帳戶名稱和帳戶索引鍵，分別。

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

在加法 toouploading 您本機的映像檔案 tooAzure 存放裝置 hello 範例程式碼會建立本機檔案 namedindex.html，您可以開啟瀏覽器 toosee 中上傳的影像。

由於 hello 程式碼包含您的帳戶名稱和帳戶金鑰，確定您的程式碼是安全。

## <a name="toodelete-a-container"></a>toodelete 容器
因為您將支付儲存體，您可能需要 toodelete **gettingstarted**容器完成後的實驗順利進行此範例。 toodelete 容器，使用 hello **CloudBlobContainer.delete**方法。

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

toocall hello **CloudBlobContainer.delete**方法、 hello 程序初始化**CloudStorageAccount**， **ClodBlobClient**，和**CloudBlobContainer**物件是 hello 與顯示相同**createIfNotExist**方法。 hello 以下是刪除 hello 命名容器的完整範例**gettingstarted**。

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

如需其他 blob 儲存體類別和方法的概觀，請參閱[如何從 Java 的 Blob 儲存體 toouse](storage-java-how-to-use-blob-storage.md)。

## <a name="next-steps"></a>後續步驟
請遵循這些連結 toolearn 深入了解更複雜的儲存體工作。

* [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
* [Azure 儲存體用戶端 SDK 參考](http://dl.windowsazure.com/storage/javadoc/)
* [Azure 儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)

