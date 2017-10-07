---
title: "aaaIntroduction tooAzure 檔案儲存體 |Microsoft 文件"
description: "Azure 檔案儲存體的概觀，此服務可讓您 toocreate 和使用網路檔案共用中 hello 使用 hello 業界標準的 Microsoft 雲端。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>簡介 tooAzure 檔案存放裝置
Azure 檔案儲存體提供網路檔案共用使用 hello 業界標準的 hello 雲端[伺服器訊息區塊 (SMB) 通訊協定](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)和[Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx)。 用戶端 (例如 Windows、macOS、Linux 的內部部署) 或 Azure 虛擬機器可同時掛接 Azure 檔案共用。 一般用途儲存體帳戶可讓您存取 tooAzure 檔案儲存體和其他服務，例如 Blob、 Azure 虛擬機器磁碟，在單一帳戶之下的佇列。



## <a name="videos"></a>影片
| 介紹 Azure 檔案儲存體 (27 分鐘) | Azure 檔案儲存體教學課程 (5 分鐘)  |
|-|-|
| [![Screencap 的 hello 簡介 Azure 檔案儲存體視訊-按一下 tooplay ！](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Hello Azure 檔案儲存體教學課程-Screencap 按一下 tooplay ！](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Azure 檔案儲存體為何很實用
Azure 檔案儲存體可讓您 tooreplace Windows Server、 Linux 或 NAS 型檔案伺服器裝載於內部，或在 hello 雲端與雲端無作業系統的檔案共用。 這有下列優點 hello:

* **共用存取**。 Azure 檔案共用支援 hello 業界標準的 SMB 通訊協定，這表示您可以順暢地取代您的內部檔案共用 Azure 檔案共用而不需擔心應用程式相容性。 無法 tooshare 檔案系統在多部電腦，應用程式/執行個體是使用 Azure 檔案儲存體的應用程式，需要 shareability 更大的優點。 
* **受到完整管理**。 Azure 檔案共用可以建立不含 hello 需要 toomanage 硬體或作業系統。 這表示您沒有 toodeal 修補 hello 伺服器 OS 重大安全性升級或替換故障硬碟。
* **指令碼和工具**。 PowerShell cmdlet 和 Azure CLI 可以使用的 toocreate、 裝載和管理儲存體的檔案共用做 hello 管理的 Azure 應用程式的一部分。您可以建立及管理 Azure 檔案共用使用 Azure 入口網站和 Azure 儲存體總管。 
* **復原功能**。 Azure 檔案儲存體已經根據 hello toobe 永遠可使用的總接地。 Azure 檔案以取代在內部部署的檔案共用儲存體，表示您不再需要 toowake 向上 toodeal 本機電源中斷或網路問題。 
* **熟悉的可程式性**。 在 Azure 中執行的應用程式可以存取透過檔案 hello 共用中的資料[系統 I/O Api](https://msdn.microsoft.com/library/system.io.file.aspx)。 開發人員因此可以利用其現有的程式碼和技術 toomigrate 現有應用程式。 此外 tooSystem IO Api，您可以使用[Azure 儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/dn261237.aspx)或 hello [Azure 儲存體的 REST API](/rest/api/storageservices/file-service-rest-api)。

Azure 檔案共用可以用來：

* **取代內部部署檔案伺服器**：  
    Azure 檔案儲存體可以是傳統的內部部署檔案伺服器或 NAS 裝置上使用的 toocompletely 取代檔案共用。 熱門作業系統，例如 Windows、 macOS 和 Linux 座落 hello 世界中，可以輕鬆地掛接 Azure 檔案共用。

* **「原形移轉」應用程式**：  
    Azure 檔案儲存體可輕鬆太 「 提起和 shift 」 的應用程式 toohello 雲端使用內部部署檔案的檔案就會共用 tooshare hello 應用程式的各部分之間的資料。 發生這種情況，每個 VM 的 toomake 連接 toohello 檔案共用，然後可讀取並寫入檔案，就像它會根據內部檔案共用。

* **簡化雲端開發**：  
    Azure 檔案儲存體可以用於許多不同的方式 toosimplify 新雲端開發專案。
    * **共用的應用程式設定**：  
        分散式應用程式的常見模式為 toohave 組態檔，在集中位置，從許多不同的 Vm 進行存取。 這些組態檔現在可以儲存在 Azure 檔案共用中，並由所有應用程式執行個體進行存取。 這些設定也可以透過 hello REST 介面，可讓世界各地存取 toohello 組態檔來管理。

    * **診斷共用**：  
        Azure 檔案共用也可以使用的 toosave 診斷檔案，例如記錄、 度量和損毀傾印。 具有這些可用的透過 SMB 的 hello 和 REST 介面可讓應用程式 toobuild 或利用各種不同的分析工具，以處理及分析 hello 診斷資料。

    * **開發/測試/偵錯**：  
        當開發人員或系統管理員使用 hello 雲端中的 Vm 上時，它們通常需要一組工具或公用程式。 在每台他們所需的虛擬機器上安裝與散佈這些公用程式相當費時。 使用 Azure 檔案儲存體，開發人員或系統管理員可以儲存最愛的工具在檔案共用，可以輕鬆地連接的 toofrom 任何虛擬機器。
        
## <a name="how-does-it-work"></a>運作方式
管理 Azure 檔案共用會比管理檔案共用內部部署簡單許多。 hello 下列圖表說明 hello Azure 檔案儲存體管理建構：

![檔案結構](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **儲存體帳戶**： 所有存取的 tooAzure 是儲存體透過儲存體帳戶。 如需關於儲存體帳戶容量的詳細資訊，請參閱＜Azure 儲存體延展性和效能目標＞(英文)。
* **共用**：檔案儲存體共用是 Azure 中的 SMB 檔案共用。 所有的目錄和檔案必須在上層共用中建立。 帳戶可以包含無限的數目的共用，並共用可以存放無限的數量的 toohello 5TB 的總容量 hello 檔案共用上的檔案。
* **目錄**：選擇性的目錄階層。
* **檔案**: hello 共用中的檔案。 檔案可能是 up too1 TB 的大小。
* **URL 格式**： 可以使用下列 URL 格式的 hello 檔案來定址：  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>後續步驟
* [建立 Azure 檔案共用](storage-file-how-to-create-file-share.md)
* [連線並在 Windows 上掛接](storage-file-how-to-use-files-windows.md)
* [連線並在 Linux 上掛接](storage-how-to-use-files-linux.md)
* [連線並在 macOS 上掛接](storage-file-how-to-use-files-mac.md)
* [常見問題集](storage-files-faq.md)
* [疑難排解](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>概念性文章和影片
* [Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Azure 檔案儲存體的工具支援
* [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md)
* [如何 toouse AzCopy 與 Microsoft Azure 儲存體](storage-use-azcopy.md)
* [使用 Azure CLI hello 與 Azure 儲存體](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>部落格文章
* [Azure 檔案儲存體現已公開推出](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure 檔案儲存體內部](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 檔案服務簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [移轉資料 tooAzure 檔案](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>參考
* [Storage Client Library for .NET 參考資料](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [檔案服務 REST API 參考](http://msdn.microsoft.com/library/azure/dn167006.aspx)
