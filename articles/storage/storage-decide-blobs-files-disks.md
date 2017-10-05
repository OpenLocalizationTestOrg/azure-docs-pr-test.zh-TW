---
title: "決定何時使用 Azure Blob、Azure 檔案或 Azure 資料磁碟"
description: "深入了解在 Azure 中儲存和存取資料的不同方法，協助您決定使用哪種技術。"
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
ms.openlocfilehash: e282a8a7bec1cb6e48110e7c9859a3a19ab8a11e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deciding-when-to-use-azure-blobs-azure-files-or-azure-data-disks"></a>決定何時使用 Azure Blob、Azure 檔案或 Azure 資料磁碟

Microsoft Azure 在 Azure 儲存體中提供數種功能，用以在雲端儲存和存取資料。 此文章涵蓋 Azure 檔案、Blob 和資料磁碟，並設計來協助從這些功能中選擇想要的功能。

## <a name="scenarios"></a>案例

下表對檔案、Blob 和資料磁碟進行比較，並顯示適用於各項的範例案例。

| 功能 | 描述  | 使用時機 |
|--------------|-------------|-------------|
| **Azure 檔案** | 提供 SMB 介面、用戶端程式庫和 [REST 介面](/rest/api/storageservices/file-service-rest-api)，允許從任何位置存取儲存的檔案。 | 您想要將應用程式「隨即轉移」到雲端，該應用程式已使用原生檔案系統 API 來在它與在 Azure 中執行的其他應用程式之間共用資料。<br/><br/>您想要儲存需要從許多虛擬機器存取的開發和偵錯工具。 |
| **Azure Blob** | 提供用戶端程式庫和 [REST 介面](/rest/api/storageservices/blob-service-rest-api)，允許在區塊 Blob 中大規模地儲存及存取非結構化資料 。 | 您想要應用程式支援串流及隨機存取案例。<br/><br/>您想要能夠從任何位置存取應用程式資料。 |
| **Azure 資料磁碟** | 提供用戶端程式庫和 [REST 介面](/rest/api/compute/virtualmachines/virtualmachines-create-or-update)，允許持續從連結的虛擬硬碟儲存和存取資料。 | 您想要隨即轉移使用原生檔案系統 API 讀取及寫入資料至永續性磁碟的應用程式。<br/><br/>您想要儲存不需要從連結磁碟的虛擬機器之外存取的資料。 |

## <a name="comparison-files-and-blobs"></a>比較：檔案和 Blob

下表對 Azure 檔案和 Azure Blob 進行比較。  
  
||||  
|-|-|-|  
|**屬性**|**Azure Blob**|**Azure 檔案**|  
|持久性選項|LRS、ZRS、GRS (和 RA-GRS，以便獲得更高的可用性)|LRS、GRS|  
|協助工具|REST API|REST API<br /><br /> SMB 2.1 和 SMB 3.0 (標準檔案系統 API)|  
|連線能力|REST API -- 全球|REST API - 全球<br /><br /> SMB 2.1 -- 區域內<br /><br /> SMB 3.0 -- 全球|  
|端點|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|目錄|一般命名空間|真實目錄物件|  
|名稱區分大小寫|區分大小寫|不區分大小寫，但保留大小寫|  
|容量|最大 500 TB 的容器|5 TB 檔案共用|  
|輸送量|每個區塊 Blob 最大每秒 60 MB|每個共用最大每秒 60 MB|  
|物件大小|最大 200 GB/區塊 Blob|最大 1TB/檔案|  
|計費的容量|根據寫入的位元組|根據檔案大小|  
|用戶端程式庫|多種語言|多種語言|  
  
## <a name="comparison-files-and-data-disks"></a>比較：檔案和資料磁碟

Azure 檔案可補強 Azure 資料磁碟。 資料磁碟一次只能連結到一部 Azure 虛擬機器。 資料磁碟是固定格式的 VHD，它在 Azure 儲存體中儲存為分頁 Blob，並由虛擬機器用來儲存持久資料。 Azure 檔案中的檔案共用可透過與存取本機磁碟 (使用原生檔案系統 API) 一樣的方式存取，並可跨許多部虛擬機器共用。  
 
下表對 Azure 檔案和 Azure 資料磁碟進行比較。  
 
||||  
|-|-|-|  
|**屬性**|**Azure 資料磁碟**|**Azure 檔案**|  
|範圍|單一虛擬機器專用|跨多部虛擬機器的共用存取|  
|快照與複製|是|否|  
|組態|在啟動虛擬機器時連線|在虛擬機器啟動之後連線|  
|驗證|內建|使用 net use 設定|  
|清除|自動|手動|  
|使用 REST 存取|無法存取 VHD 內的檔案|可以存取儲存在共用中的檔案|  
|大小上限|1 TB 磁碟|5 TB 檔案共用和 1 TB 共用內的檔案|  
|最大 8KB IOps|500 IOps|1000 IOps|  
|輸送量|每個磁碟最大每秒 60 MB|每個檔案共用最大每秒 60 MB|  

## <a name="next-steps"></a>後續步驟

決定如何儲存及存取資料時，您也應考慮牽涉的成本。 如需詳細資訊，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。
  
某些 SMB 功能並不適用於雲端。 如需詳細資訊，請參閱 [Azure 檔案服務不支援的功能](/rest/api/storageservices/features-not-supported-by-the-azure-file-service)。
  
如需有關資料磁碟的詳細資訊，請參閱[管理磁碟及映像](storage-about-disks-and-vhds-linux.md)和[如何將資料磁碟連結到 Windows 虛擬機器](../virtual-machines/windows/classic/attach-disk.md)。