---
title: "aaaDeciding 時 toouse Azure Blob、 Azure 或 Azure 資料磁碟"
description: "了解 hello 不同的方式 toostore 及存取資料在 Azure toohelp 決定哪些技術 toouse。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: cd43abde43daf33dd7c43aa2696a9c8d5cd19612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>決定當 toouse Azure Blob、 Azure 檔案或 Azure 資料磁碟

Microsoft Azure 提供數種功能，在 Azure 儲存體來儲存和存取您 hello 雲端中的資料。 本文章涵蓋 Azure 檔案、 Blob 和資料磁碟，並為您選擇這些功能的設計的 toohelp。

## <a name="scenarios"></a>案例

hello 下表比較檔案、 Blob 和資料磁碟，並顯示適用於每個範例案例。

| 功能 | 說明 | 當 toouse |
|--------------|-------------|-------------|
| **Azure 檔案** | 提供 SMB 介面，用戶端程式庫，和[REST 介面](/rest/api/storageservices/file-service-rest-api)toostored 檔案允許從任何地方存取。 | 您想太 「 提起和 shift 」 應用程式 toohello 雲端已經使用 hello 原生檔案系統 Api tooshare 之間的資料並在 Azure 中執行其他應用程式。<br/><br/>您想 toostore 開發和偵錯工具需要 toobe 從多個虛擬機器存取。 |
| **Azure Blob** | 提供用戶端程式庫和[REST 介面](/rest/api/storageservices/blob-service-rest-api)，可讓非結構化的資料太儲存或存取大規模區塊 blob 中。 | 您想要您的應用程式 toosupport 串流和隨機存取案例。<br/><br/>您想從任何地方 toobe 無法 tooaccess 應用程式資料。 |
| **Azure 資料磁碟** | 提供用戶端程式庫和[REST 介面](/rest/api/compute/virtualmachines/virtualmachines-create-or-update)，可讓資料 toobe 持續儲存和存取從連接的虛擬硬碟。 | 您希望 toolift，和應用程式，使用原生檔案系統 Api tooread 和寫入資料 toopersistent 磁碟。<br/><br/>您不需要從外部 hello 虛擬機器 toowhich hello 磁碟存取的 toobe toostore 資料會附加。 |

## <a name="comparison-files-and-blobs"></a>比較：檔案和 Blob

hello 下表比較 Azure 檔案和 Azure Blob。  
  
||||  
|-|-|-|  
|**屬性**|**Azure Blob**|**Azure 檔案**|  
|持久性選項|LRS、ZRS、GRS (和 RA-GRS，以便獲得更高的可用性)|LRS、GRS|  
|協助工具|REST API|REST API<br /><br /> SMB 2.1 和 SMB 3.0 (標準檔案系統 API)|  
|連線能力|REST API -- 全球|REST API - 全球<br /><br /> SMB 2.1 -- 區域內<br /><br /> SMB 3.0 -- 全球|  
|端點|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|目錄|一般命名空間|真實目錄物件|  
|名稱區分大小寫|區分大小寫|不區分大小寫，但保留大小寫|  
|容量|向上 too500 500TB 的容器|5 TB 檔案共用|  
|Throughput|向上 too60 MB/s 每個區塊 blob|向上 too60 MB/s 每個共用|  
|物件大小|向上 too200 GB/區塊 blob|Too1TB/檔案|  
|計費的容量|根據寫入的位元組|根據檔案大小|  
|用戶端程式庫|多種語言|多種語言|  
  
## <a name="comparison-files-and-data-disks"></a>比較：檔案和資料磁碟

Azure 檔案可補強 Azure 資料磁碟。 資料磁碟一次只能附加的 tooone Azure 虛擬機器。 資料磁碟 hello 虛擬機器 toostore 持久資料所使用，且都儲存為分頁 blob 在 Azure 儲存體，固定格式 Vhd。 可以存取 Azure 檔案中的檔案共用中 hello 相同方式與 hello 本機磁碟存取 （透過使用原生檔案系統 Api），並可以橫跨多個虛擬機器。  
 
hello 下表比較 Azure 檔案和 Azure 資料磁碟。  
 
||||  
|-|-|-|  
|**屬性**|**Azure 資料磁碟**|**Azure 檔案**|  
|Scope|獨佔 tooa 單一虛擬機器|跨多部虛擬機器的共用存取|  
|快照與複製|是|否|  
|組態|在啟動 hello 虛擬機器的連線|連接 hello 虛擬機器啟動之後|  
|驗證|內建|使用 net use 設定|  
|清除|自動|手動|  
|使用 REST 存取|無法存取檔案內 hello VHD|可以存取儲存在共用中的檔案|  
|大小上限|1 TB 磁碟|5 TB 檔案共用和 1 TB 共用內的檔案|  
|最大 8KB IOps|500 IOps|1000 IOps|  
|Throughput|Too60 MB/s 每個磁碟設定|向上 too60 MB/s 每個檔案共用|  

## <a name="next-steps"></a>後續步驟

當制定有關如何儲存和存取您的資料，您也應該考慮 hello 成本相關。 如需詳細資訊，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。
  
某些 SMB 功能不適用 toohello 雲端。 如需詳細資訊，請參閱[不支援的 hello Azure 檔案服務功能](/rest/api/storageservices/features-not-supported-by-the-azure-file-service)。
  
如需有關資料磁碟的詳細資訊，請參閱[管理磁碟及映像](../../virtual-machines/windows/about-disks-and-vhds.md)和[如何 tooAttach Windows 虛擬機器的資料磁碟 tooa](../../virtual-machines/windows/classic/attach-disk.md)。
