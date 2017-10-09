---
title: "Azure 匯入/匯出匯出工作-v1 aaaPreviewing 磁碟機使用量 |Microsoft 文件"
description: "了解如何 toopreview hello 清單的 blob 您選取用於匯出工作 hello Azure 匯入/匯出服務中。"
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
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="daf4b-103">預覽匯出作業的磁碟機使用量</span><span class="sxs-lookup"><span data-stu-id="daf4b-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="daf4b-104">建立匯出工作之前，您會需要的 toochoose blob toobe 一組匯出。</span><span class="sxs-lookup"><span data-stu-id="daf4b-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="daf4b-105">hello Microsoft Azure 匯入/匯出服務可讓您 toouse 一份 blob 路徑或 blob 前置詞 toorepresent hello blob，您已選取。</span><span class="sxs-lookup"><span data-stu-id="daf4b-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="daf4b-106">接下來，您需要 toodetermine 多少磁碟機需要 toosend。</span><span class="sxs-lookup"><span data-stu-id="daf4b-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="daf4b-107">hello 匯入/匯出工具提供 hello`PreviewExport`選取命令 toopreview 磁碟機使用量。 hello blob 時，根據 hello hello 磁碟機大小要 toouse。</span><span class="sxs-lookup"><span data-stu-id="daf4b-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="daf4b-108">命令列參數</span><span class="sxs-lookup"><span data-stu-id="daf4b-108">Command-line parameters</span></span>

<span data-ttu-id="daf4b-109">您可以使用下列參數，當使用 hello hello `PreviewExport` hello 匯入/匯出工具的命令。</span><span class="sxs-lookup"><span data-stu-id="daf4b-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="daf4b-110">命令列參數</span><span class="sxs-lookup"><span data-stu-id="daf4b-110">Command-line parameter</span></span>|<span data-ttu-id="daf4b-111">說明</span><span class="sxs-lookup"><span data-stu-id="daf4b-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="daf4b-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="daf4b-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="daf4b-113">選用。</span><span class="sxs-lookup"><span data-stu-id="daf4b-113">Optional.</span></span> <span data-ttu-id="daf4b-114">hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="daf4b-114">hello log directory.</span></span> <span data-ttu-id="daf4b-115">詳細資訊記錄檔會寫入 toothis 目錄。</span><span class="sxs-lookup"><span data-stu-id="daf4b-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="daf4b-116">如果未不指定任何記錄檔目錄，則 hello 目前的目錄會用作 hello 記錄檔目錄。</span><span class="sxs-lookup"><span data-stu-id="daf4b-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="daf4b-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="daf4b-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="daf4b-118">必要。</span><span class="sxs-lookup"><span data-stu-id="daf4b-118">Required.</span></span> <span data-ttu-id="daf4b-119">hello 名稱 hello hello 儲存體帳戶匯出工作。</span><span class="sxs-lookup"><span data-stu-id="daf4b-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="daf4b-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="daf4b-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="daf4b-121">如果未指定 (且只有在未指定) 容器 SAS 時，才是必要參數。</span><span class="sxs-lookup"><span data-stu-id="daf4b-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="daf4b-122">hello hello hello 的儲存體帳戶的帳戶金鑰匯出工作。</span><span class="sxs-lookup"><span data-stu-id="daf4b-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="daf4b-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="daf4b-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="daf4b-124">如果未指定 (且只有在未指定) 儲存體帳戶金鑰時，才是必要參數。</span><span class="sxs-lookup"><span data-stu-id="daf4b-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="daf4b-125">用於列出 hello blob toobe hello 容器 SAS 匯出 hello 匯出工作。</span><span class="sxs-lookup"><span data-stu-id="daf4b-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="daf4b-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="daf4b-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="daf4b-127">必要。</span><span class="sxs-lookup"><span data-stu-id="daf4b-127">Required.</span></span> <span data-ttu-id="daf4b-128">路徑 toohello XML 檔案包含清單的 blob 路徑或 blob 路徑前置詞 hello blob toobe 匯出。</span><span class="sxs-lookup"><span data-stu-id="daf4b-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="daf4b-129">hello 檔案格式用於 hello `BlobListBlobPath` hello 中的項目[Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 匯入/匯出服務 REST API 的作業。</span><span class="sxs-lookup"><span data-stu-id="daf4b-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="daf4b-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="daf4b-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="daf4b-131">必要。</span><span class="sxs-lookup"><span data-stu-id="daf4b-131">Required.</span></span> <span data-ttu-id="daf4b-132">hello 大小為匯出工作，如磁碟機 toouse*例如*，500GB、 1.5 t B。</span><span class="sxs-lookup"><span data-stu-id="daf4b-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="daf4b-133">命令列範例</span><span class="sxs-lookup"><span data-stu-id="daf4b-133">Command-line example</span></span>

<span data-ttu-id="daf4b-134">hello 下列範例會示範 hello`PreviewExport`命令：</span><span class="sxs-lookup"><span data-stu-id="daf4b-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="daf4b-135">hello 匯出 blob 清單檔案可能包含 blob 名稱和 blob 前置詞，如下所示：</span><span class="sxs-lookup"><span data-stu-id="daf4b-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="daf4b-136">hello Azure 匯入/匯出工具會列出所有匯出的 blob toobe 和計算的 toopack hello 的磁碟機到指定大小，而不顧及任何必要的額外負荷，接著評估 hello 的磁碟機數目所需 toohold hello blob 和磁碟機使用情形資訊。</span><span class="sxs-lookup"><span data-stu-id="daf4b-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="daf4b-137">Hello 輸出，以省略資訊的記錄檔的範例如下：</span><span class="sxs-lookup"><span data-stu-id="daf4b-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="daf4b-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="daf4b-138">Next steps</span></span>

* [<span data-ttu-id="daf4b-139">Azure 匯入/匯出工具參考</span><span class="sxs-lookup"><span data-stu-id="daf4b-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
