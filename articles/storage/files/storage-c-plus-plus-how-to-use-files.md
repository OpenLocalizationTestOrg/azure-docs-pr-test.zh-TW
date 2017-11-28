---
title: "使用 C++ 開發 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何開發使用 Azure 檔案儲存體來儲存檔案資料的 C++ 應用程式和服務。"
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 86c3714327074f5576e535f67a0a2a8e761ffb46
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="cb6e1-103">使用 C++ 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="cb6e1-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="cb6e1-104">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="cb6e1-104">About this tutorial</span></span>

<span data-ttu-id="cb6e1-105">在本教學課程中，您將學習如何對 Azure 檔案儲存體執行基本作業。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-105">In this tutorial, you'll learn how to perform basic operations on Azure File storage.</span></span> <span data-ttu-id="cb6e1-106">透過以 C++ 撰寫的範例，您將學習如何建立共用和目錄、上傳、列出及刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-106">Through samples written in C++, you'll learn how to create shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="cb6e1-107">如果您是 Azure 檔案儲存體的新手，閱讀下列各節中的概念，對於了解範例很有幫助。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-107">If you are new to Azure File storage , going through the concepts in the sections that follow will be helpful in understanding the samples.</span></span>


* <span data-ttu-id="cb6e1-108">建立及刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="cb6e1-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="cb6e1-109">建立及刪除目錄</span><span class="sxs-lookup"><span data-stu-id="cb6e1-109">Create and delete directories</span></span>
* <span data-ttu-id="cb6e1-110">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="cb6e1-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="cb6e1-111">上傳、下載及刪除檔案</span><span class="sxs-lookup"><span data-stu-id="cb6e1-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="cb6e1-112">設定 Azure 檔案共用的配額 (大小上限)</span><span class="sxs-lookup"><span data-stu-id="cb6e1-112">Set the quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="cb6e1-113">為使用共用上所定義之共用存取原則的檔案建立共用存取簽章 (SAS 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>

> [!Note]  
> <span data-ttu-id="cb6e1-114">由於 Azure 檔案儲存體可透過 SMB 存取，因此便可使用標準 C++ I/O 類別和函式撰寫簡單的應用程式以存取 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-114">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard C++ I/O classes and functions.</span></span> <span data-ttu-id="cb6e1-115">本文將說明如何撰寫使用 Azure 儲存體 C++ SDK 的應用程式，它會使用 [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) 與 Azure 檔案儲存體通訊。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-115">This article will describe how to write applications that use the Azure Storage C++ SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="cb6e1-116">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="cb6e1-116">Create a C++ application</span></span>
<span data-ttu-id="cb6e1-117">若要建置範例，您必須安裝適用於 C++ 的 Azure 儲存體用戶端程式庫 2.4.0。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-117">To build the samples, you will need to install the Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="cb6e1-118">您也應該建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="cb6e1-119">若要安裝適用於 C++ 的 Azure 儲存體用戶端 2.4.0，您可以使用下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="cb6e1-119">To install the Azure Storage Client 2.4.0 for C++, you can use one of the following methods:</span></span>

* <span data-ttu-id="cb6e1-120">**Linux：** 遵循 [Azure Storage Client Library for C++ 讀我檔案](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 頁面中提供的指示進行。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-120">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="cb6e1-121">**Windows：**在 Visual Studio 中，按一下 [工具]&gt;[NuGet 套件管理員]&gt;[套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="cb6e1-122">在 [NuGet 套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 中輸入下列命令，然後按下 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-122">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="cb6e1-123">設定您的應用程式以使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="cb6e1-123">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="cb6e1-124">在您要操作 Azure 檔案儲存體的 C++ 來源檔案頂端，新增下列 include 陳述式：</span><span class="sxs-lookup"><span data-stu-id="cb6e1-124">Add the following include statements to the top of the C++ source file where you want to manipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="cb6e1-125">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="cb6e1-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="cb6e1-126">若要使用檔案儲存體，您必須連接到您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-126">To use File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="cb6e1-127">第一個步驟是設定連接字串，我們將用它來連線至您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-127">The first step would be to configure a connection string, which we'll use to connect to your storage account.</span></span> <span data-ttu-id="cb6e1-128">讓我們定義靜態變數以便進行。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-128">Let's define a static variable to do that.</span></span>

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="cb6e1-129">連接到 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cb6e1-129">Connecting to an Azure storage account</span></span>
<span data-ttu-id="cb6e1-130">您可以使用 **cloud_storage_account** 類別來代表儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-130">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="cb6e1-131">若要從儲存體連接字串擷取儲存體帳戶資訊，您可以使用 **parse** 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-131">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="cb6e1-132">建立 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="cb6e1-132">Create an Azure File share</span></span>
<span data-ttu-id="cb6e1-133">Azure 檔案儲存體中的所有檔案和目錄都位於名為 [共用] 的容器中。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="cb6e1-134">您的儲存體帳戶可以有帳戶容量允許數量的共用。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="cb6e1-135">若要取得共用及其內容的存取權，您必須使用 Azure 檔案儲存體用戶端。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-135">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```cpp
// Create the Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="cb6e1-136">使用 Azure 檔案儲存體用戶端，您可以取得共用的參考。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-136">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="cb6e1-137">若要建立共用，請使用 **cloud_file_share** 物件的 **create_if_not_exists** 方法。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-137">To create the share, use the **create_if_not_exists** method of the **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="cb6e1-138">目前，**共用**會將參考保留至名為 **my-sample-share** 的共用。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-138">At this point, **share** holds a reference to a share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="cb6e1-139">刪除 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="cb6e1-139">Delete an Azure File share</span></span>
<span data-ttu-id="cb6e1-140">刪除共用可以藉由在 cloud_file_share 物件上呼叫 **delete_if_exists** 方法來完成。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-140">Deleting a share is done by calling the **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="cb6e1-141">以下是執行該作業的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="cb6e1-142">建立目錄</span><span class="sxs-lookup"><span data-stu-id="cb6e1-142">Create a directory</span></span>
<span data-ttu-id="cb6e1-143">您可以組織儲存體，方法是將檔案放在子目錄中，而不是將所有檔案都放在根目錄中。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-143">You can organize storage by putting files inside subdirectories instead of having all of them in the root directory.</span></span> <span data-ttu-id="cb6e1-144">Azure 檔案儲存體可讓您建立您的帳戶允許數量的目錄。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-144">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="cb6e1-145">下列程式碼會在根目錄底下建立名為 **my-sample-directory** 的目錄，以及名為 **my-sample-subdirectory** 的子目錄。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-145">The code below will create a directory named **my-sample-directory** under the root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="cb6e1-146">刪除目錄</span><span class="sxs-lookup"><span data-stu-id="cb6e1-146">Delete a directory</span></span>
<span data-ttu-id="cb6e1-147">刪除目錄是一項簡單的工作，不過請注意您無法刪除仍然包含檔案或其他目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="cb6e1-148">列舉 Azure 檔案共用的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="cb6e1-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="cb6e1-149">取得共用內檔案和目錄的清單很容易，只要在 **cloud_file_directory** 參考上呼叫 **list_files_and_directories** 即可。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="cb6e1-150">若要存取傳回的 **list_file_and_directory_item** 中豐富的屬性和方法，您必須呼叫 **list_file_and_directory_item.as_file** 方法來取得 **cloud_file** 物件，或呼叫 **list_file_and_directory_item.as_directory** 方法來取得 **cloud_file_directory** 物件。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-150">To access the rich set of properties and methods for a returned **list_file_and_directory_item**, you must call the **list_file_and_directory_item.as_file** method to get a **cloud_file** object, or the **list_file_and_directory_item.as_directory** method to get a **cloud_file_directory** object.</span></span>

<span data-ttu-id="cb6e1-151">下列程式碼示範如何擷取和輸出共用之根目錄中每個項目的 URI。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-151">The following code demonstrates how to retrieve and output the URI of each item in the root directory of the share.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="cb6e1-152">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="cb6e1-152">Upload a file</span></span>
<span data-ttu-id="cb6e1-153">Azure 檔案共用至少包含根目錄，檔案可以放置其中。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-153">At the very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="cb6e1-154">在本節中，您將學習如何從本機儲存體將檔案上傳至共用的根目錄。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-154">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="cb6e1-155">上傳檔案的第一個步驟是取得檔案所在之目錄的參考。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-155">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="cb6e1-156">您可以藉由呼叫共用物件的 **get_root_directory_reference** 方法來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-156">You do this by calling the **get_root_directory_reference** method of the share object.</span></span>

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="cb6e1-157">現在您具有共用之根目錄的參考，您可以對其上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-157">Now that you have a reference to the root directory of the share, you can upload a file onto it.</span></span> <span data-ttu-id="cb6e1-158">此範例會從檔案、文字和串流進行上傳。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="cb6e1-159">下載檔案</span><span class="sxs-lookup"><span data-stu-id="cb6e1-159">Download a file</span></span>
<span data-ttu-id="cb6e1-160">若要下載檔案，請先擷取檔案參考，然後呼叫 **download_to_stream** 方法將檔案內容傳輸到您可接著保留在本機檔案的串流物件。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-160">To download files, first retrieve a file reference and then call the **download_to_stream** method to transfer the file contents to a stream object, which you can then persist to a local file.</span></span> <span data-ttu-id="cb6e1-161">或者，您可以使用 **download_to_file** 方法，將檔案內容下載到本機檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-161">Alternatively, you can use the **download_to_file** method to download the contents of a file to a local file.</span></span> <span data-ttu-id="cb6e1-162">您可以使用 **download_text** 方法，將檔案內容當成文字字串下載。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-162">You can use the **download_text** method to download the contents of a file as a text string.</span></span>

<span data-ttu-id="cb6e1-163">下列範例使用 **download_to_stream** 和 **download_text** 方法，示範如何下載前幾節中所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-163">The following example uses the **download_to_stream** and **download_text** methods to demonstrate downloading the files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="cb6e1-164">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="cb6e1-164">Delete a file</span></span>
<span data-ttu-id="cb6e1-165">另一個常見的 Azure 檔案儲存體作業是刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="cb6e1-166">下列程式碼會刪除名為 my-sample-file-3 且儲存在根目錄底下的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-166">The following code deletes a file named my-sample-file-3 stored under the root directory.</span></span>

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="cb6e1-167">設定 Azure 檔案共用的配額 (大小上限)</span><span class="sxs-lookup"><span data-stu-id="cb6e1-167">Set the quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="cb6e1-168">您可以設定檔案共用的配額 (或大小上限)，以 GB 為單位。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-168">You can set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="cb6e1-169">您也可以檢查有多少資料目前儲存在共用上。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-169">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="cb6e1-170">藉由設定共用的配額，您可以限制儲存在共用上的檔案大小總計。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-170">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="cb6e1-171">如果共用上的檔案大小總計超過共用上設定的配額，則用戶端將無法增加現有檔案的大小或建立新的檔案 (除非這些檔案為空白)。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-171">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="cb6e1-172">下列範例示範如何檢查共用的目前使用狀況，以及如何設定共用的配額。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-172">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="cb6e1-173">產生檔案或檔案共用的共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cb6e1-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="cb6e1-174">您可以為檔案共用或個別檔案產生共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="cb6e1-175">您也可以在檔案共用上建立共用存取原則，以管理共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-175">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="cb6e1-176">建議您建立共用存取原則，因為如果必須洩漏 SAS，它提供了一種撤銷 SAS 的方式。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-176">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="cb6e1-177">下列範例會在共用上建立共用存取原則，然後使用該原則為共用中檔案上的 SAS 提供條件約束。</span><span class="sxs-lookup"><span data-stu-id="cb6e1-177">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="cb6e1-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb6e1-178">Next steps</span></span>
<span data-ttu-id="cb6e1-179">如需深入了解 Azure 儲存體，請探索這些資源：</span><span class="sxs-lookup"><span data-stu-id="cb6e1-179">To learn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="cb6e1-180">Storage Client Library for C++</span><span class="sxs-lookup"><span data-stu-id="cb6e1-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="cb6e1-181">[Azure 儲存體檔案服務的 C++ 範例] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="cb6e1-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="cb6e1-182">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="cb6e1-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="cb6e1-183">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="cb6e1-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)