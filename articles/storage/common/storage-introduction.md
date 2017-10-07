---
title: "aaaIntroduction tooAzure 儲存體 |Microsoft 文件"
description: "簡介 tooAzure 儲存體，Microsoft 的 hello 雲端中的資料存放區。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>簡介 tooMicrosoft Azure 儲存體

Microsoft Azure 儲存體是 Microsoft 管理的雲端服務，可提供高度可用、安全、持久、可擴充和備援的儲存體。 Microsoft 會為您進行維護和處理重大問題。 

Azure 儲存體包含三項資料服務：Blob 儲存體、檔案儲存體和佇列儲存體。 Blob 儲存體支援標準和進階儲存體，使用 hello 最快的效能可能只 Ssd 的進階儲存體。 另一個功能是很棒的存放裝置，可讓您 toostorage 大量的較低的成本很少存取的資料。

在本文中，您會了解 hello 下列：
* hello Azure 儲存體服務
* hello 類型的儲存體帳戶
* 存取您的 blob、佇列和檔案
* 加密
* 複寫 
* 將資料傳入或傳出儲存體
* hello 許多儲存體用戶端程式庫使用。 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>介紹 hello Azure 儲存體服務

toouse 任何 hello 服務提供 Azure 儲存體-Blob 儲存體、 檔案儲存體和佇列儲存體--您先建立儲存體帳戶，再從該儲存體帳戶中的特定服務的資料傳輸。 

## <a name="blob-storage"></a>Blob 儲存體

Blob 基本上類似您在電腦 (或平板電腦、行動裝置等) 上儲存的檔案。 它們可以是圖片、Microsoft Excel 檔案、HTML 檔案、虛擬硬碟 (VHD)、巨量資料 (例如記錄、資料庫備份) - 幾乎涵蓋任何項目。 Blob 會儲存在容器中，也就是類似 toofolders。 

之後將檔案儲存在 Blob 儲存體，您可以存取從任何地方這些中使用 Url 的 hello world，hello REST 介面，或其中一個 hello Azure SDK 儲存體用戶端程式庫。 儲存體用戶端程式庫提供多種語言，包括 Node.js、Java、PHP、Ruby、Python 和 .NET。 

Blob 有三種類型：區塊 Blob、附加 Blob 和分頁 Blob (用於 VHD 檔案)。

* 區塊 blob 會使用的 toohold 一般檔案出 tooabout 4.7 TB。 
* 頁面 blob 是使用的 toohold 向上 too8 TB 大小的隨機存取檔案。 這些用來備份 Vm 的 hello VHD 檔案。
* 附加 blob 的區塊，就像 hello 區塊 blob，組成，但會針對最佳化附加作業。 這些用於等記錄資訊 toohello 相同 blob 的多個 Vm。

對於網路條件約束而進行上傳或下載資料 tooBlob 儲存體上提出 hello 傳輸的資料集非常大，您可以寄送的硬碟機 tooMicrosoft tooimport 一組或匯出資料直接從 hello 資料中心。 請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)。

## <a name="file-storage"></a>檔案儲存體

hello Azure 檔案服務可讓您可以使用 hello 標準伺服器訊息區塊 (SMB) 通訊協定來存取的高可用性的網路檔案共用上的 tooset。 Hello 表示多個 Vm 可以共用相同的檔案具有讀取和寫入權限。 您也可以讀取 hello 檔案使用 hello REST 介面或 hello 儲存體用戶端程式庫。 

區分 Azure 檔案儲存體從公司檔案共用上的一件事是您可以從任何地方存取 hello 檔案中使用的 URL，指向 toohello 檔案，並且包含共用的存取簽章 (SAS) token 的 hello world。 您可以產生 SAS 權杖。它們允許特定存取 tooa 私人資產一段特定時間。 

檔案共用可以用於許多常見案例： 

* 許多內部部署應用程式會使用檔案共用。 這項功能可讓您更輕鬆 toomigrate 共用資料 tooAzure 這些應用程式。 如果您裝載 hello 檔案共用 toohello 相同磁碟機代號，hello 內部應用程式會使用，hello 屬於您存取 hello 檔案共用的應用程式應該使用最少，如果有的話，變更。

* 組態檔可以儲存在檔案共用上並從多個 VM 進行存取。 工具和公用程式使用多個群組中的開發人員可以儲存在檔案共用，確保所有人都可以找到它們，和他們使用 hello 相同版本。

* 診斷記錄檔、 度量和損毀傾印是只有三個範例的資料可以寫入 tooa 檔案共用和處理或稍後分析。

在這個階段，Active Directory 為基礎的驗證和存取控制清單 (Acl) 不支援，但會在未來的 hello 中一些時間。 hello 儲存體帳戶認證是使用的 tooprovide 驗證存取 toohello 檔案共用。 這表示具有 hello 共用裝載的任何人都會有完整讀取/寫入存取 toohello 共用。

## <a name="queue-storage"></a>佇列儲存體

hello Azure 佇列服務是使用的 toostore 並擷取訊息。 佇列訊息可以是 too64 KB 的大小，up，佇列可以包含數百萬個訊息。 佇列是以非同步方式處理訊息 toobe 通常使用的 toostore 清單。 

例如，假設您想客戶 toobe 無法 tooupload 圖片，而且您想 toocreate 縮圖的每張圖片。 您可以讓您上傳 hello 圖片時等候您 toocreate hello 縮圖的客戶。 另外也可以 toouse 佇列。 當 hello 客戶完成他的上傳時，寫入訊息 toohello 佇列。 然後有 Azure 函式從 hello 佇列擷取 hello 訊息，並建立 hello 縮圖。 Hello 組件，這項處理可以調整個別提供您更多控制微調您的使用量時。

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>表格儲存體
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
標準 Azure 表格儲存體現在屬於 Cosmos DB。 Azure 表格儲存體也有進階資料表，可提供輸送量最佳化的資料表、全域發佈，以及自動次要索引。 toolearn 詳細並再試一次出 hello 新 premium 體驗，請簽出[Azure Cosmos DB： 表格 API](https://aka.ms/premiumtables)。

## <a name="disk-storage"></a>磁碟儲存體

hello Azure 儲存體團隊也擁有的磁碟，包括所有 hello managed 和 unmanaged 的磁碟功能可供虛擬機器。 如需有關這些功能的詳細資訊，請參閱 hello[計算服務文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。

## <a name="types-of-storage-accounts"></a>儲存體帳戶類型 

下表顯示 hello 各種類型的儲存體帳戶，以及與每個可用的物件。

|**儲存體帳戶的類型**|**一般用途：標準**|**一般用途：進階**|**Blob 儲存體、經常性存取和非經常性存取層**|
|-----|-----|-----|-----|
|**支援的服務**| Blob、檔案、佇列服務 | Blob 服務 | Blob 服務|
|**支援的 Blob 類型**|區塊 Blob、分頁 Blob 及附加 Blob | 分頁 Blob | 區塊 Blob 和附加 Blob|

### <a name="general-purpose-storage-accounts"></a>一般用途的儲存體帳戶

一般用途的儲存體帳戶有兩種。 

#### <a name="standard-storage"></a>標準儲存體 

hello 最常使用的儲存體帳戶是標準儲存體帳戶，可用於所有類型的資料。 標準儲存體帳戶使用磁性媒體 toostore 資料。

#### <a name="premium-storage"></a>進階儲存體

進階儲存體可為分頁 blob 提供高效能儲存體，主要用於 VHD 檔案。 進階儲存體帳戶使用 SSD toostore 資料。 Microsoft 建議對所有 VM 使用進階儲存體。

### <a name="blob-storage-accounts"></a>Blob 儲存體帳戶

專門儲存體帳戶用於 toostore 區塊 blob，而且附加 blob hello Blob 儲存體帳戶。 您無法將分頁 blob 儲存在這些帳戶中，因此無法儲存 VHD 檔案。 這些帳戶可讓您存取層 tooHot tooset 或 Cool;hello 層可以隨時變更。 

hello 作用的存取層使用，針對經常存取的檔案-支付較高的成本，如存放裝置，但 hello 成本存取 hello blob 是低很多。 對儲存在 hello 酷炫的存取層中的 blob，支付較高的成本，用於存取 hello blob 但 hello 儲存體的成本更低。

## <a name="accessing-your-blobs-files-and-queues"></a>存取您的 blob、檔案和佇列

每個儲存體帳戶都有兩種驗證金鑰，任一種金鑰均可用於任何作業。 有兩個索引鍵，因此您可以換 hello 偶爾金鑰 tooenhance 安全性。 就非常重要，這些機碼保持安全狀態因為持有者，以及 hello 帳戶名稱，允許無限制的存取 tooall 資料 hello 儲存體帳戶中。 

本節查看兩個方式 toosecure hello 儲存體帳戶，以及其資料。 如需保護您資料的儲存體帳戶的詳細資訊，請參閱 hello [Azure 儲存體安全性指南 》](storage-security-guide.md)。

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Toostorage 帳戶使用 Azure AD 保護的存取

其中一種方式 toosecure 存取 tooyour 存放的資料是控制存取 toohello 儲存體帳戶金鑰。 使用資源管理員角色型存取控制 (RBAC)，您可以指派角色 toousers、 群組或應用程式。 這些角色會繫結 tooa 組特定的允許或不允許的動作。 使用 RBAC toogrant 存取 tooa 儲存體帳戶只會處理該儲存體帳戶，例如變更 hello 存取層的 hello 管理作業。 您無法使用 RBAC toogrant 存取 toodata 物件與特定的容器或檔案共用。 不過，您可以使用 RBAC toogrant 存取 toohello 儲存體帳戶金鑰 」，接著可以使用的 tooread hello 資料物件。 

### <a name="securing-access-using-shared-access-signatures"></a>使用共用存取簽章保護存取權 

您可以使用共用的存取簽章和預存存取原則 toosecure 資料物件。 共用的存取簽章 (SAS) 是字串，包含可能是安全性權杖附加 toohello URI toodelegate 存取 toospecific 儲存物件和 toospecify 條件約束，例如權限和存取 hello 日期/時間範圍，可讓您的資產。 這項功能有廣泛的功能。 如需詳細資訊，請參閱太[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。

### <a name="public-access-tooblobs"></a>公用存取 tooblobs

hello Blob 服務可讓您 tooprovide 公用存取 tooa 容器和其 blob 或特定的 blob。 當您將容器或 Blob 指定為公用時，任何人都可以進行匿名讀取；不需要驗證。 舉例來說，當您會想 toodo 這是當您有使用影像、 視訊或從 Blob 儲存體的文件的網站。 如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>加密

有幾個基本類型的加密 hello 儲存體服務。 

### <a name="encryption-at-rest"></a>待用加密 

您可以在任一 hello 檔案服務 （預覽） 上啟用儲存體服務加密 (SSE) 或 hello Azure 儲存體帳戶的 Blob 服務。 如果啟用，就會加密寫入 toohello 特定服務的所有資料寫入之前。 當您讀取 hello 資料時，會先解密，傳回之前。 

### <a name="client-side-encryption"></a>用戶端加密

hello 儲存體用戶端程式庫有的方法可以呼叫 tooprogrammatically 再將它傳送嗨網路跨 hello 用戶端 tooAzure 從加密資料。 它會以加密方式儲存，這表示待用時也會加密。 讀取回 hello 資料時，會解密 hello 資訊在收到之後。 

### <a name="encryption-in-transit-with-azure-file-shares"></a>透過 Azure 檔案共用進行傳輸時加密

如需共用存取簽章的詳細資訊，請參閱 [使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md) 。 請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)和[hello Azure 儲存體服務驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)如安全存取 tooyour 儲存體帳戶的詳細資訊。

如需有關如何保護您的儲存體帳戶和加密的詳細資訊，請參閱 hello [Azure 儲存體安全性指南 》](storage-security-guide.md)。

## <a name="replication"></a>複寫

在您的資料是持久的順序 tooensure，Azure 儲存體具有 hello 能力 tookeep （和管理） 資料的多個複本。 這稱為複寫，有時候稱為備援。 當您設定儲存體帳戶時，您可選取複寫類型。 在大部分情況下，可以在 hello 儲存體帳戶設定之後修改此設定。 

所有儲存體帳戶都有**本機備援儲存體 (LRS)**。 這表示您資料的三個複本都受 hello 資料中心內的 Azure 儲存體指定 hello 儲存體帳戶已設定時。 當變更都會認可的 tooone 複製、 hello 其他兩個複本會更新後再傳回成功。 這表示 hello 三個複本都保持同步。此外，hello 三個複本位於不同的容錯網域和升級網域，這表示您的資料可用，即使保存您資料的儲存體節點失敗或更新時所建立的離線 toobe。 

**本地備援儲存體 (LRS)**

如上所述，使用 LRS，您在單一資料中心內有三個資料複本。 這個方法會處理 hello 問題的資料變成無法使用，如果儲存體節點失敗或被更新，離線 toobe，但不是 hello 變得無法使用整個資料中心的大小寫。

**區域備援儲存體 (ZRS)**

區域備援儲存體 (ZRS) 維護 hello 三個區域的資料複本，以及另一組的三份資料。 hello 的三個複本的第二個集合會以非同步方式複寫跨越一或兩個區域內的資料中心。 請注意，ZRS 僅適用於一般用途的儲存體帳戶中的區塊 Blob。 此外，一旦您已建立儲存體帳戶，並選取 ZRS，您無法將它轉換 toouse tooany 其他類型的複寫，反之亦然。

ZRS 帳戶可提供比 LRS 更高的持久性，但 ZRS 帳戶並沒有計量或記錄功能。 

**異地備援儲存體 (GRS)**

地理備援儲存體 (GRS) 維護 hello 三個區域的資料複本主要區域中加上另一組次要區域數百甚遠 hello 主要區域中資料的三個複本。 在 hello 事件中的 hello 主要區域故障，Azure 儲存體將容錯移轉 toohello 次要區域。 

**讀取權限異地備援儲存體 (RA-GRS)** 

讀取權限的地理備援儲存體是與 GRS 完全相同，不同之處在於您 hello 次要位置中取得讀取權限 toohello 資料。 如果 hello 主要資料中心變成暫時無法使用，您可以繼續 tooread hello 資料從 hello 次要位置。 這很有幫助。 例如，您可能會變更為唯讀模式，並指出 toohello 次要複本的 web 應用程式允許某些存取，即使沒有更新。 

> [!IMPORTANT]
> 您可以變更您的資料複寫方式建立儲存體帳戶後，除非建立 hello 帳戶時，指定 ZRS。 不過請注意，您可能會造成的額外的單次資料傳輸成本如果您從 LRS tooGRS 或 RA-GRS 切換。
>

如需有關複寫的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。

嚴重損壞修復資訊，請參閱[如果 Azure 儲存體中斷，就會發生何種 toodo](storage-disaster-recovery-guidance.md)。

如需如何 tooleverage RA-GRS 儲存體 tooensure 高可用性，請參閱[設計高可用的應用程式使用 RA-GRS](storage-designing-ha-apps-with-ragrs.md)。

## <a name="transferring-data-tooand-from-azure-storage"></a>從 Azure 儲存體傳輸資料 tooand

儲存體帳戶中或跨儲存體帳戶，您可以使用 hello AzCopy 命令列公用程式 toocopy blob 和檔案資料。 Hello 下列其中一種文件的說明，請參閱：

* [使用適用於 Windows 的 AzCopy 傳輸資料](storage-use-azcopy.md)
* [使用適用於 Linux 的 AzCopy 傳輸資料](storage-use-azcopy-linux.md)

AzCopy 之上 hello [Azure 資料移動文件庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)，這是目前可供預覽。

hello Azure 匯入/匯出服務可使用的 tooimport 或匯出大量的 blob 資料 tooor 從儲存體帳戶。 您準備從 hello 硬碟 hello 資料郵件多個硬碟 tooan Azure 資料中心，將傳送的位置和傳送嗨硬碟回 tooyou。 如需 hello 匯入/匯出服務的詳細資訊，請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](../storage-import-export-service.md)。

## <a name="pricing"></a>價格

如需 Azure 儲存體定價的詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage/blobs/)。

## <a name="storage-apis-libraries-and-tools"></a>儲存體 API、程式庫和工具
任何可提出 HTTP/HTTPS 要求的語言皆可存取 Azure 儲存體資源。 另外，Azure 儲存體還提供了幾種熱門語言的程式設計程式庫。 這些程式庫可透過處理詳細資料 (例如同步和非同步叫用、進行批次作業、例外狀況管理、自動重試、運作方式等等) 來簡化使用 Azure 儲存體的許多項目。 程式庫目前可提供下列語言的 hello，而且平台，使用與其他人 hello 管線：

### <a name="azure-storage-data-services"></a>Azure 儲存體資料服務
* [儲存體服務 REST API](/rest/api/storageservices/)
* [適用於 .NET 的儲存體用戶端程式庫](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [適用於 Java/Android 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/java/)
* [適用於 Node.js 的儲存體用戶端程式庫](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [適用於 PHP 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/php/)
* [適用於 Python 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/python/)
* [適用於 Ruby 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/ruby/)
* [適用於 PowerShell 的儲存體 Cmdlet](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [適用於 CLI 2.0 的儲存體命令](/cli/azure/storage)

## <a name="next-steps"></a>後續步驟

* [深入了解 Blob 儲存體](../blobs/storage-blobs-introduction.md)
* [深入了解檔案儲存體](../storage-files-introduction.md)
* [深入了解佇列儲存體](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>針對系統管理員
* [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md)
* [使用 Azure CLI 搭配 Azure 儲存體](../storage-azure-cli.md)

### <a name="for-net-developers"></a>針對 .NET 開發人員
* [以 .NET 開始使用 Azure Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)
* [以 .NET 開始使用 Azure 表格儲存體](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [以 .NET 開始使用 Azure 佇列儲存體](../storage-dotnet-how-to-use-queues.md)
* [在 Windows 上開始使用 Azure 檔案儲存體](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>針對 Java/Android 開發人員
* [如何從 Java 的 Blob 儲存體 toouse](../blobs/storage-java-how-to-use-blob-storage.md)
* [如何從 Java 資料表儲存體 toouse](../../cosmos-db/table-storage-how-to-use-java.md)
* [如何從 Java 佇列儲存體 toouse](../storage-java-how-to-use-queue-storage.md)
* [如何從 Java 檔案儲存體 toouse](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>針對 Node.js 開發人員
* [如何 toouse Node.js 從 Blob 儲存體](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [如何 toouse 從 Node.js 的資料表儲存體](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [如何 toouse 從 Node.js 佇列儲存體](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>針對 PHP 開發人員
* [如何 toouse 來自 PHP 的 Blob 儲存體](../blobs/storage-php-how-to-use-blobs.md)
* [如何 toouse 來自 PHP 的資料表儲存體](../../cosmos-db/table-storage-how-to-use-php.md)
* [如何 toouse 來自 PHP 的佇列儲存體](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>針對 Ruby 開發人員
* [如何 toouse Ruby 從 Blob 儲存體](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [如何 toouse Ruby 從資料表儲存體](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [如何 toouse Ruby 從佇列儲存體](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>針對 Python 開發人員
* [如何 toouse 來自 Python 的 Blob 儲存體](../blobs/storage-python-how-to-use-blob-storage.md)
* [如何 toouse 來自 Python 的資料表儲存體](../../cosmos-db/table-storage-how-to-use-python.md)
* [如何 toouse 來自 Python 的佇列儲存體](../storage-python-how-to-use-queue-storage.md)   
* [如何 toouse 來自 Python 的檔案存放裝置](../storage-python-how-to-use-file-storage.md) 
-->