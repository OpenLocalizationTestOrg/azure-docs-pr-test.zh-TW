---
title: "Azure 檔案儲存體相關常見問題的 aaaFrequently |Microsoft 文件"
description: "尋找 toofrequently Azure 檔案儲存體相關常見問題的答案。"
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
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: d8a94fdc77e928dbc6996e1e635cd3527e0c67d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>關於 Azure 檔案儲存體的常見問題集

## <a name="general"></a>一般
* **問：什麼是 Azure 檔案儲存體？**  
   
    Azure 檔案儲存體是 Azure 中的分散式檔案系統。 它提供可讓使用者 toomount hello 存放裝置為原生支援 Azure 虛擬機器或在內部部署電腦上共用的 SMB 通訊協定介面。

* **問：Azure 檔案儲存體為何很實用？**  
   
    Azure 檔案儲存體可跨多部 VM 和平台存取共用資料。 請參閱太[為什麼 Azure 檔案儲存是很有用](storage-files-introduction.md#why-azure-file-storage-is-useful)。

* **問：何時應該使用 Azure 檔案、Azure Blob 或 Azure 磁碟？**  
   
    Microsoft Azure 提供數種方式 hello 雲端 toostore 及存取資料。  
   
    Azure 檔案儲存體-提供 SMB 介面、 用戶端程式庫和 REST 介面，允許從任何位置輕鬆地存取 toostored 檔案。  
   
    Azure Blob-提供用戶端程式庫和 REST 介面，可讓非結構化的資料 toobe 存放及存取大規模區塊 blob 中。  
   
    Azure 資料磁碟-提供用戶端程式庫和 REST 介面，可讓資料 toobe 持續儲存和存取從連接的虛擬硬碟。  
   
    進一步了解上[制定時 toouse Azure Blob、 Azure 或 Azure 資料磁碟](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)

* **問：如何開始使用 Azure 檔案儲存體？**  
   
    您可以從建立 Azure 檔案共用開始。 您可以建立使用 Azure 入口網站、 hello Azure 儲存體 PowerShell cmdlet、 hello Azure 儲存體用戶端程式庫或 hello Azure 儲存體的 REST API 的 Azure 檔案共用。在本教學課程中，您將學習：

    * [了解如何 toocreate Azure 檔案共用使用 hello 入口網站](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [了解如何 toocreate Azure 檔案共用使用 Powershell](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [了解如何 toocreate Azure 檔案共用使用 CLI](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **問：Azure 檔案儲存體支援何種複寫？**  
   
    Azure 檔案儲存體目前只支援 LRS 或 GRS。 我們計劃 toosupport RA-GRS，但尚無時間表 tooshare。

## <a name="security-authentication-and-access-control"></a>安全性、驗證和存取控制

* **問：什麼是 Azure 檔案儲存體中的不同方式 tooaccess 檔案？**
    
    您可以使用 SMB 3.0 通訊協定在本機電腦上掛接 hello 檔案共用，或使用的工具，例如[存放裝置總管](http://storageexplorer.com/)tooaccess 檔案在檔案共用。 從您的應用程式，您可以使用儲存體用戶端程式庫、 REST Api 或 Powershell tooaccess Azure 檔案中的檔案共用。

* **問：如何提供使用 web 瀏覽器存取 tooa 特定檔案？**
    
    使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。 比方說，您可以產生具有唯讀存取 tooa 特定檔案的語彙基元，特定的一段時間。 擁有此 url 的任何人可以直接從任何網頁瀏覽器存取 hello 檔案，而它有效。 從儲存體總管之類的 UI 就能輕鬆產生 SAS 金鑰。

* **問：它是可能 toospecify 唯讀或唯寫的資料夾權限內 hello 共用嗎？**
    
    如果裝載 hello 透過 SMB 的檔案共用，您不需要此層級的權限控制。 不過，您可以達到此目的建立共用的存取簽章 (SAS) 透過 hello REST API 或用戶端程式庫。  

* **問：如何啟用 Azure 檔案儲存體的伺服器端加密？**

    Azure 檔案儲存體的[伺服器端加密](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)在所有區域和公用與國內雲端公開上市。 您可以使用 [Azure 入口網站](https://portal.azure.com/)、[Microsoft Azure 儲存體資源提供者 API](/rest/api/storagerp/storageaccounts)、[Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 或 [Azure CLI](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)，為 Azure 檔案儲存體啟用 SSE。
    
    啟用 SSE 上 Azure 檔案儲存體之後, 將會自動加密任何新資料寫入 toohello 檔案儲存在該儲存體帳戶。 這項功能適用於所有新的資料寫入 tooexisting 或新的共用中的現有或新的儲存體帳戶。 此用此功能不會額外收費。 進一步了解上[如何在 Azure 檔案儲存體 tooenable SSE](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)。

* **問：Azure 檔案儲存體是否支援 Active Directory 型驗證？**
   
    我們目前不支援 AD 式驗證或 ACL，但在我們的功能要求清單中卻有它。 現在，hello Azure 儲存體帳戶金鑰是使用的 tooprovide 驗證 toohello 檔案共用。 我們提供透過 hello REST API 或 hello 用戶端程式庫中使用共用的存取簽章 (SAS) 因應措施。 使用 SAS 時，您可以產生在一段時間內都是有效的具有特定權限的權杖。 例如，您可以產生語彙基元具有唯讀存取 tooa 提供與 10 分鐘過期的檔案。 擁有這個語彙基元有效時的任何人都有唯讀存取 toothat 檔案的 10 分鐘。
   
    透過 hello REST API 或用戶端程式庫只支援 SAS。 當您掛接 hello 透過 hello SMB 通訊協定的檔案共用時，您無法使用 SAS toodelegate 存取 tooits 內容。 
    
* **問：什麼是 Azure 檔案儲存體支援 hello 資料相容性原則？**

   Azure 檔案儲存體執行最上層的其他儲存體服務在 Azure 儲存體和適用於 hello hello 相同的儲存體架構相同的資料相容性原則。 Azure 儲存體資料相容性的詳細資訊，您可以下載並參照太[Microsoft Azure 資料保護文件](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)。

## <a name="on-premises-access"></a>內部部署存取

* **我有 toouse Azure ExpressRoute tooconnect tooAzure 檔案存放裝置從內部部署 VM 的 Q.Do 嗎？**
   
    否。 如果您不需要 ExpressRoute，您仍可存取 hello 檔案共用從內部部署，只要您有連接埠 445 （TCP 輸出） 開放網際網路存取。 不過，您可以搭配使用 ExpressRoute 與 Azure 檔案儲存體 (如果需要)。

* **問：如何在本機電腦上掛接 Azure 檔案共用？** 
    
    您可以掛接 hello 透過 hello SMB 通訊協定的檔案共用，只要已開啟連接埠 445 （TCP 輸出），而且您的用戶端支援 hello SMB 3.0 通訊協定 （例如，您使用 Windows 10 或 Windows Server 2012）。 請使用本機 ISP 提供者 toounblock hello 連接埠。 在 hello 過渡版，您可以檢視您使用的檔案[存放裝置總管](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)。


## <a name="billing-and-pricing"></a>計費和定價
* **問：沒有外部 toohello 訂用帳戶計費的頻寬 hello Azure VM 與檔案共用計數之間的網路流量？**
   
    如果 hello 檔案共用和 VM 在 hello 相同 Azure 地區，hello 兩者間傳輸是免費的。 如果它們是在不同的區域，hello 它們之間的流量將支付外部頻寬。

## <a name="backup"></a>備份

* **問：如何備份我的 Azure 檔案共用？**
    
    您可以使用 AzCopy、RoboCopy，或是可備份已掛接檔案共用的協力廠商備份工具。 我們預期未來; 接近 hello toohave hello 能力 tootake 的快照集檔案共用您將會無法 toouse 此功能 toobackup Azure 檔案共用。

## <a name="performance"></a>效能

* **問：什麼是 Azure 檔案儲存體的 hello 規模限制？**
    如需 Azure 檔案儲存體延展性和效能目標的資訊，請參閱 [Azure 儲存體延展性和效能目標](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files)。

* **問：嘗試 toounzip 檔案到 Azure 檔案儲存體時，我效能而變慢。我該怎麼辦？**
    
    tootransfer 大量的檔案到 Azure 檔案儲存體，我們建議為這些工具都已最佳化的網路傳輸使用 AzCopy （Windows、 Linux/Unix 的預覽） 或 Azure Powershell。

* **問：修補程式已被釋放 toofix 緩慢效能問題，Azure 檔案儲存體？**
    
    hello 客戶從 Windows 8.1 或 Windows Server 2012 R2 來存取 Azure 檔案儲存體時，hello Windows 小組最近已發行的修補程式 toofix 效能降低的問題。 如需詳細資訊，請簽出 hello 相關知識庫文章[降低效能，當您從 Windows 8.1 或 Server 2012 R2 中存取 Azure 檔案儲存體](https://support.microsoft.com/kb/3114025)。

## <a name="features-and-interoperability-with-other-services"></a>與其他服務的功能互通性
* **問：是 「 檔案共用見證"hello 的其中一個容錯移轉叢集的 Azure 檔案儲存體的使用案例？**
   
    目前不受支援。

* **問：有 hello REST API 中的重新命名作業嗎？**
   
    目前沒有。

* **問：可以有巢狀共用，換句話說，共用下的共用嗎？**
    
    否。 hello 檔案共用是 hello 虛擬驅動程式，您可以掛接，因此不支援巢狀的共用。

* **問：搭配 IBM MQ 使用 Azure 檔案儲存體**
    
    設定 Azure 檔案儲存體服務時，IBM 已發行的文件 tooguide IBM MQ 客戶。 如需詳細資訊，請簽出[如何 toosetup IBM MQ 多重執行個體使用 Microsoft Azure 檔案服務的佇列管理員](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)。


## <a name="troubleshooting"></a>疑難排解
* **問：如何針對 Azure 檔案儲存體錯誤進行疑難排解？**
    
    您可以使用參照太[Azure 檔案儲存體疑難排解文章](storage-troubleshoot-windows-file-connection-problems.md)的端對端疑難排解指引。 


## <a name="see-also"></a>另請參閱
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

### <a name="conceptual-articles-and-videos"></a>概念性文章和影片
* [Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [如何 toouse Linux 的 Azure 檔案儲存體](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>檔案儲存體的工具支援
* [如何 toouse AzCopy 與 Microsoft Azure 儲存體](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [使用 Azure CLI hello 與 Azure 儲存體](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [針對 Azure 檔案儲存體的問題進行疑難排解](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>部落格文章
* [Azure 檔案儲存體現已公開推出](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure 檔案儲存體內部](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 檔案服務簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [移轉資料 tooAzure 檔案存放裝置](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>參考
* [Storage Client Library for .NET 參考資料](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [檔案服務 REST API 參考](http://msdn.microsoft.com/library/azure/dn167006.aspx)
