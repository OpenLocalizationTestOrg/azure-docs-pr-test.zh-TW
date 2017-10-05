---
title: "預覽 Azure 匯入/匯出作業的磁碟機使用量 - v1 | Microsoft Docs"
description: "了解如何預覽您已針對 Azure 匯入/匯出服務中的匯出作業選取的 blob 清單。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 6ec74ae0b0931f3fed99a43f4f7e58f9d425b138
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="a420e-103">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="a420e-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="a420e-104">建立匯出作業之前，您必須先選擇一組要匯出的 blob。</span><span class="sxs-lookup"><span data-stu-id="a420e-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="a420e-105">Microsoft Azure 匯入/匯出服務可讓您使用一份 blob 路徑或 blob 前置詞清單來代表您已選取的 blob。</span><span class="sxs-lookup"><span data-stu-id="a420e-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="a420e-106">接著，必須判斷您需要傳送多少個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a420e-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="a420e-107">匯入/匯出工具提供的 `PreviewExport` 命令可根據您要使用的磁碟機大小，預覽所選取 Blob 的磁碟機使用量。</span><span class="sxs-lookup"><span data-stu-id="a420e-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="a420e-108">命令列參數</span><span class="sxs-lookup"><span data-stu-id="a420e-108">Command-line parameters</span></span>

<span data-ttu-id="a420e-109">使用匯入/匯出工具的 `PreviewExport` 命令時，您可以使用下列參數。</span><span class="sxs-lookup"><span data-stu-id="a420e-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="a420e-110">命令列參數</span><span class="sxs-lookup"><span data-stu-id="a420e-110">Command-line parameter</span></span>|<span data-ttu-id="a420e-111">說明</span><span class="sxs-lookup"><span data-stu-id="a420e-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="a420e-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="a420e-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="a420e-113">選用。</span><span class="sxs-lookup"><span data-stu-id="a420e-113">Optional.</span></span> <span data-ttu-id="a420e-114">記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="a420e-114">The log directory.</span></span> <span data-ttu-id="a420e-115">詳細資訊記錄檔會寫入至這個目錄。</span><span class="sxs-lookup"><span data-stu-id="a420e-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="a420e-116">如未指定記錄檔目錄，則會使用目前的目錄做為記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="a420e-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="a420e-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="a420e-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="a420e-118">必要。</span><span class="sxs-lookup"><span data-stu-id="a420e-118">Required.</span></span> <span data-ttu-id="a420e-119">匯出作業的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a420e-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="a420e-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="a420e-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="a420e-121">如果未指定 (且只有在未指定) 容器 SAS 時，才是必要參數。</span><span class="sxs-lookup"><span data-stu-id="a420e-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="a420e-122">匯出作業之儲存體帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="a420e-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="a420e-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="a420e-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="a420e-124">如果未指定 (且只有在未指定) 儲存體帳戶金鑰時，才是必要參數。</span><span class="sxs-lookup"><span data-stu-id="a420e-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="a420e-125">容器 SAS，可供列出要在匯出作業中匯出的 blob。</span><span class="sxs-lookup"><span data-stu-id="a420e-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="a420e-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="a420e-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="a420e-127">必要。</span><span class="sxs-lookup"><span data-stu-id="a420e-127">Required.</span></span> <span data-ttu-id="a420e-128">XML 檔案的路徑，此檔案包含要匯出的 Blob 的Blob 路徑清單或 Blob 路徑前置詞。</span><span class="sxs-lookup"><span data-stu-id="a420e-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="a420e-129">匯入/匯出服務 REST API 的 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 作業中 `BlobListBlobPath` 元素中所使用的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="a420e-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="a420e-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="a420e-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="a420e-131">必要。</span><span class="sxs-lookup"><span data-stu-id="a420e-131">Required.</span></span> <span data-ttu-id="a420e-132">要用於匯出作業的磁碟機大小，例如 500GB、1.5TB。</span><span class="sxs-lookup"><span data-stu-id="a420e-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="a420e-133">命令列範例</span><span class="sxs-lookup"><span data-stu-id="a420e-133">Command-line example</span></span>

<span data-ttu-id="a420e-134">下列範例示範 `PreviewExport` 命令：</span><span class="sxs-lookup"><span data-stu-id="a420e-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="a420e-135">匯出 blob 清單檔案可能包含 blob 名稱和 blob 前置詞，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="a420e-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="a420e-136">Azure 匯入/匯出工具會列出所有要匯出的 blob 並計算如何將它們封裝到指定大小的磁碟機，並考量任何必要的額外負荷，然後估計保留 blob 和磁碟機使用量資訊所需的磁碟機數目。</span><span class="sxs-lookup"><span data-stu-id="a420e-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="a420e-137">以下輸出範例，以中省略資訊記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="a420e-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="a420e-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a420e-138">Next steps</span></span>

* [<span data-ttu-id="a420e-139">Azure 匯入/匯出工具參考</span><span class="sxs-lookup"><span data-stu-id="a420e-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
