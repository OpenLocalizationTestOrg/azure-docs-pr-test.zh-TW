---
title: "aaaIntroduction tooAzure 儲存體 |Microsoft 文件"
description: "Azure 儲存體，hello 雲端中 Microsoft 的線上資料存放區的概觀。 了解如何 toouse hello 在應用程式中的最佳可用的雲端儲存體解決方案。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>簡介 tooMicrosoft Azure 儲存體

## <a name="overview"></a>概觀
Azure 儲存體是 hello 雲端儲存體解決方案，依賴持續性、 可用性和延展性 toomeet hello 需求的客戶的現代應用程式。 透過閱讀此文件，開發人員、IT 專業人員，以及商業決策人員可以了解關於：

* 何謂 Azure 儲存體，以及可以如何在雲端、行動、伺服器和桌面應用程式中加以充分運用
* 您可以儲存的資料種類與 hello Azure 儲存體服務： blob （物件） 的資料、 NoSQL 資料表資料、 訊息排入佇列，與檔案共用。
* 如何管理 Azure 儲存體存取 tooyour 資料
* 如何透過備援和複寫來保持 Azure 儲存體資料的永久性
* 其中 toogo 下一步 toobuild 應用程式的第一個 Azure 儲存體

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

如需使用 Azure 儲存體的工具、程式庫及其他資源的詳細資訊，請參閱下方的 [後續步驟](#next-steps) 。

## <a name="what-is-azure-storage"></a>何謂 Azure 儲存體？
雲端運算針對資料需要可擴充、可持久和高可用性儲存體的應用程式，提供了全新案例 - 這也是 Microsoft 開發 Azure 儲存體的真正原因。 在加法 toomaking 它讓開發人員 toobuild 大規模的應用程式 toosupport 新案例，Azure 儲存體也提供 hello 儲存體基礎的 Azure 虛擬機器，進一步的建築 tooits 強固性。

讓您可以儲存並處理數百個 tb 的科學、 財務分析和媒體應用程式所需的資料 toosupport hello 巨量資料案例，是可大幅擴充，azure 儲存體。 或者您可以儲存 hello 少量資料所需的小型企業網站。 只要是落在您的需求，您只針對付費 hello 打算儲存的資料。 Azure 儲存體目前儲存了數十兆的獨特客戶物件，且平均每秒處理上百萬個要求。

Azure 儲存體是彈性，連結，您可以設計針對大的整體客群的應用程式和視需要調整這些應用程式層都根據 hello 提供儲存資料的數量，以及 hello 對它發出的要求數目。 您只需在使用時，針對所使用資料進行付費即可。

Azure 儲存體使用自動分割系統，可自動根據流量負載平衡您的資料。 這表示，為您的應用程式成長 hello 需求，Azure 儲存體自動配置 hello 適當的資源 toomeet 它們。

Hello world，從任何類型的應用程式中的任何位置存取 azure 儲存體是是否正在執行 hello 雲端 hello 桌面、 內部部署伺服器，或行動或平板電腦裝置。 Hello 應用程式其中 hello 裝置上儲存資料的子集，但會將它與一組完整的 hello 雲端中儲存的資料同步處理行動裝置的情況下，您可以使用 Azure 儲存體。

為了方便開發，Azure 儲存體支援使用各種作業系統 (包括 Windows 和 Linux) 和多種程式設計語言 (包括 .NET、Java、Node.js、Python、Ruby、PHP 和 C++ 及行動程式設計語言) 的用戶端。 Azure 儲存體也會公開透過簡單的 REST Api，也就是可用 tooany 能夠傳送和接收資料透過 HTTP/HTTPS 的用戶端的資料資源。

Azure Premium 儲存體對於 Azure 虛擬機器上執行的 I/O 密集工作負載提供高效能、低延遲磁碟支援。 與 Azure 高階儲存體，您可以附加多個永續性資料磁碟 tooa 虛擬機器，並設定它們 toomeet 效能需求。 各個資料磁碟都有 Azure Premium 儲存體的 SSD 磁碟做為備援，充分達到最大的 I/O 效能。 如需詳細資訊，請參閱 [Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md) 。

## <a name="introducing-hello-azure-storage-services"></a>介紹 hello Azure 儲存體服務
Azure 儲存體提供下列四項服務的 hello: Blob 儲存體，資料表儲存體、 佇列儲存體和檔案儲存體。

* 「Blob 儲存體」可儲存非結構化物件資料。 Blob 可以是任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也會參照的 tooas 物件儲存體。
* 「表格儲存體」可儲存結構化資料集。 資料表儲存體是 NoSQL 索引鍵屬性的資料存放區，可快速開發和快速存取 toolarge 數量的資料。
* 「佇列儲存體」可為工作流程處理及雲端服務元件間的通訊，提供可靠的訊息服務。
* 檔案存放裝置提供共用存放裝置使用 hello 標準 SMB 通訊協定的舊版應用程式。 Azure 虛擬機器和雲端服務可以透過掛接共用，應用程式元件之間共用檔案資料，並在內部部署應用程式可以存取透過 hello 檔案服務 REST API 的共用中的檔案資料。

Azure 儲存體帳戶是安全的帳戶，可讓您存取 Azure 儲存體中的 tooservices。 儲存體帳戶提供儲存體資源 hello 唯一命名空間。 hello 圖顯示 hello 儲存體帳戶中的 hello Azure 儲存體資源之間的關聯性：

![Azure 儲存體資源](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob 儲存體
Blob 儲存體具有大量非結構化的物件資料 toostore hello 雲端中的使用者，提供符合成本效益且可擴充的方案。 您可以使用 Blob 儲存體 toostore 內容，例如：

* 文件
* 社交資料 (例如照片、視訊、音樂和部落格)
* 檔案、電腦、資料庫和裝置的備份
* Web 應用程式的影像和文字
* 雲端應用程式的組態資料
* 巨量資料 (例如記錄和其他大型資料集)

每個 Blob 會組織成一個容器。 容器也會提供實用的方式 tooassign 安全性原則 toogroups 的物件。 儲存體帳戶可以包含任何數目的容器，以及容器可以包含任何數目的 blob，向上 toohello 500 TB 容量限制的 hello 儲存體帳戶。

Blob 儲存體提供三種類型的 Blob，包括區塊 Blob、附加 Blob 及分頁 Blob (磁碟)。

* 區塊 Blob 已針對串流和儲存雲端物件進行最佳化，是儲存文件、媒體檔案、備份等的不錯選擇。
* 附加 blob 類似 tooblock blob，但適合用於附加作業。 附加 blob 可以只是藉由加入新的區塊 toohello 結尾更新。 附加 blob 是不錯的選擇，例如記錄、 需要新的資料寫入只 toohello 結尾 hello blob toobe 案例。
* 分頁 blob 適用於代表 IaaS 磁碟，支援隨機寫入，以及可能是 up too1 TB 的大小。 Azure 虛擬機器網路連結的 IaaS 磁碟是以頁面 Blob 方式儲存的 VHD。

對於網路條件約束而進行上傳或下載資料 tooBlob 儲存體上提出 hello 傳輸的資料集非常大，您可以寄送磁碟機 tooMicrosoft tooimport 或匯出資料直接從 hello 資料中心。 請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)。

## <a name="table-storage"></a>表格儲存體

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

新式應用程式通常會要求以超越前幾代軟體需求的延伸性和彈性儲存資料。 資料表儲存體提供高可用性、 可大幅擴充的儲存體，讓您的應用程式可以自動調整 toomeet 使用者需求。 表格儲存體屬於 Microsoft 的 NoSQL 索引鍵屬性儲存，它的無結構描述設計讓它有別於傳統的關聯式資料庫。 Schemaless 資料存放區中，很容易 tooadapt 資料做為 hello 需要的應用程式 evolve。 資料表儲存體是簡單 toouse，因此開發人員可以快速建立應用程式。 存取 toodata 非常快速且符合成本效益的所有種類的應用程式。  相較於類似資料量的傳統 SQL，資料表儲存體通常可大幅降低成本。

表格儲存體屬於索引鍵屬性儲存，代表資料表中的每個值會與具型別的屬性名稱一起儲存。 hello 屬性名稱可以用於篩選和指定選取準則。 一組屬性及其值就構成一個實體。 由於 schemaless 資料表儲存體，在兩個實體 hello 相同資料表可以包含不同集合的屬性，而這些屬性可以屬於不同的類型。

您可以使用資料表儲存體 toostore 彈性的資料集，例如 web 應用程式、 通訊錄，裝置資訊和任何其他類型的中繼資料服務所需的使用者資料。  您可以將任意數目的實體儲存在資料表中，而且儲存體帳戶包含任何數量的資料表，向上 toohello hello 儲存體帳戶的容量限制。

如同 Blob 和佇列，開發人員可以管理並存取資料表儲存體使用標準的 REST 通訊協定，但是資料表儲存體也支援子集 hello OData 通訊協定，以簡化進階的查詢功能，並啟用 JSON 和 AtomPub (XML 為基礎)格式。

現今的以網際網路為基礎的應用程式對於類似資料表儲存體的 NoSQL 資料庫會提供常用的替代 tootraditional 關聯式資料庫。

## <a name="queue-storage"></a>佇列儲存體
設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。 佇列儲存體提供可靠的傳訊解決方案的應用程式元件之間的非同步通訊，不論它們是在 hello 雲端中，hello 桌面、 內部部署伺服器，或行動裝置。 佇列儲存體也支援管理非同步工作並建置處理工作流程。

儲存體帳戶可包含任意數目的佇列。 佇列可以包含任意數目的訊息，向上 toohello hello 儲存體帳戶的容量限制。 個別訊息可能是 up too64 KB 的大小。

## <a name="file-storage"></a>檔案儲存體
hello Azure 檔案服務可讓您可以使用 hello 標準伺服器訊息區塊 (SMB) 通訊協定來存取的高可用性的網路檔案共用上的 tooset。 Hello 表示多個 Vm 可以共用相同的檔案具有讀取和寫入權限。 您也可以讀取 hello 檔案使用 hello REST 介面或 hello 儲存體用戶端程式庫。

區分 Azure 檔案儲存體從公司檔案共用上的一件事是您可以從任何地方存取 hello 檔案中使用的 URL，指向 toohello 檔案，並且包含共用的存取簽章 (SAS) token 的 hello world。 您可以產生 SAS 權杖。它們允許特定存取 tooa 私人資產一段特定時間。

檔案共用可以用於許多常見案例：

* 許多內部部署應用程式會使用檔案共用。 這項功能可讓您更輕鬆 toomigrate 共用資料 tooAzure 這些應用程式。 如果您裝載 hello 檔案共用 toohello 相同磁碟機代號，hello 內部應用程式會使用，hello 屬於您存取 hello 檔案共用的應用程式應該使用最少，如果有的話，變更。

* 組態檔可以儲存在檔案共用上並從多個 VM 進行存取。 工具和公用程式使用多個群組中的開發人員可以儲存在檔案共用，確保所有人都可以找到它們，和他們使用 hello 相同版本。

* 診斷記錄檔、 度量和損毀傾印是只有三個範例的資料可以寫入 tooa 檔案共用和處理或稍後分析。

在這個階段，Active Directory 為基礎的驗證和存取控制清單 (Acl) 不支援，但會在未來的 hello 中一些時間。 hello 儲存體帳戶認證是使用的 tooprovide 驗證存取 toohello 檔案共用。 這表示具有 hello 共用裝載的任何人都會有完整讀取/寫入存取 toohello 共用。

## <a name="access-tooblob-table-queue-and-file-resources"></a>存取 tooBlob、 資料表、 佇列和檔案資源
根據預設，只有 hello 儲存體帳戶擁有者可以存取 hello 儲存體帳戶中的資源。 如 hello 資料的安全性，對您帳戶中的資源所提出的每個要求都必須經過驗證。 驗證會仰賴共用金鑰模型。 Blob 也可以設定的 toosupport 匿名驗證。

建立儲存體帳戶時所指派的兩組存取金鑰可用於驗證。 必須要有兩個金鑰可確保您的應用程式維持可用，當您定期重新產生金鑰 hello 常見的安全性金鑰管理作法。

如果您需要 tooallow 控制使用者存取 tooyour 存放裝置資源，您可以建立共用的存取簽章。 共用的存取簽章 (SAS) 是可附加的 tooa URL 可讓委派存取 tooa 儲存體資源語彙基元。 擁有 hello 語彙基元的任何人都可以存取它所指 toowith hello 權限，它會指定 hello 資源，hello 段時間，它是有效。 從 2015-04-05 版開始，Azure 儲存體支援兩種共用存取簽章：服務 SAS 與帳戶 SAS。

hello 服務 SAS 委派存取 tooa 資源中其中一個 hello 存放服務： hello Blob、 佇列、 資料表或檔案服務。

SA 帳戶會將委派存取 tooresources 一或多個 hello 儲存體服務中。 您可以委派未提供與服務 SAS 存取 tooservice 層級作業。 您也可以委派存取 tooread、 寫入和刪除 blob 容器、 資料表、 佇列和服務的 SAS 不允許的檔案共用上的作業。

最後，您可以指定容器及其 Blob 或特定的 Blob 是否可供公用存取。 當您將容器或 Blob 指定為公用時，任何人都可以進行匿名讀取；不需要驗證。  公用容器和 Blob 對於公開資源 (例如網站上所託管的媒體和文件) 而言非常有用。  針對整體客群 toodecrease 網路延遲，您可以快取以 hello Azure CDN 的網站所使用的 blob 資料。

如需共用存取簽章的詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。 請參閱[管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)和[hello Azure 儲存體服務驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)如安全存取 tooyour 儲存體帳戶的詳細資訊。

## <a name="replication-for-durability-and-high-availability"></a>持久性和高可用性的複寫
儲存體帳戶一定是您在 Microsoft Azure 中的 hello 資料複寫 tooensure 耐久性與高可用性。 您的資料，請在 hello 相同資料中心內或 tooa 第二個資料中心，依據您選擇的複寫選項的複寫複本。 複寫會保護資料，並保留您的應用程式執行時間的暫時性硬體故障的 hello 事件中。 如果您的資料複寫 tooa 第二個資料中心，也可以保護的資料，避免發生災難性失敗 hello 主要位置。

複寫可確保您的儲存體帳戶符合 hello[服務等級協定 (SLA) 的儲存體](https://azure.microsoft.com/support/legal/sla/storage/)即使在 hello 字體的失敗。 如需 Azure 儲存體的 hello SLA 保證持久性和可用性，請參閱。

當您建立儲存體帳戶時，您可以選取其中一個 hello 下列複寫選項：

* **本地備援儲存體 (LRS)。** 本地備援儲存體可維護三個資料複本。 LRS 會在單一區域的單一資料中心內複寫三次。 LRS 避免資料受到一般硬體故障，但不是能從單一資料中心的 hello 失敗。

    使用 LRS 可享有折扣費率。 如需最高的持久性，建議您採用異地備援儲存體，如下所述。
* **區域備援儲存體 (ZRS)。** 區域備援儲存體可維護三個資料複本。 ZRS 複寫三次到兩個 toothree 設備，可能在單一區域或跨兩個區域，持久性比 LRS 更高。 ZRS 可確保資料在單一地區內的持續性。

    ZRS 提供高於 LRS 等級的持久性；不過，如需最高的持久性，建議您採用地理區域備援儲存體，如下所述。

  > [!NOTE]
  > ZRS 目前僅適用於區塊 blob，且僅 2014年 2 月 14 日版以上版本提供支援。
  >
  > 一旦您已建立儲存體帳戶，並選取 ZRS，您無法將它轉換 toouse tooany 其他類型的複寫，反之亦然。
  >
  >
* **異地備援儲存體 (GRS)**。 GRS 可維護六個資料複本。 使用 GRS 時，您的資料會在 hello 主要區域中，複寫三次，並在 hello 主要區域，提供 hello 最高持久性層級哩的次要區域數百也複寫三次。 在 hello 事件中的 hello 主要區域故障，Azure 儲存體將會容錯移轉 toohello 次要區域。 GRS 可確保兩個不同區域中的資料持續性。

    如需主要和次要配對的相關資訊 (依區域)，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。
* **讀取權限異地備援儲存體 (RA-GRS)**。 讀取權限的地理備援儲存體複寫您資料 tooa 次要地理位置，並提供在 hello 次要位置的讀取權限 tooyour 資料中。 讀取權限的地理備援儲存體可讓您 tooaccess 從主要 hello 或 hello 次要位置，在一個位置變得無法使用的 hello 事件資料。 讀取權限的地理備援儲存體是預設儲存體帳戶的 hello 預設選項，當您建立它。

  > [!IMPORTANT]
  > 您可以變更您的資料複寫方式建立儲存體帳戶後，除非建立 hello 帳戶時，指定 ZRS。 不過請注意，您可能會造成的額外的單次資料傳輸成本如果您從 LRS tooGRS 或 RA-GRS 切換。
  >
  >

如需儲存體複寫選項相關的其他詳細資料，請參閱 [Azure 儲存體複寫](storage-redundancy.md) 。

如需儲存體帳戶複寫的價格資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/)。 如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services) 。

如需 Azure 儲存體持久性的架構詳細資訊，請參閱 [SOSP 文件：Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。

## <a name="transferring-data-tooand-from-azure-storage"></a>從 Azure 儲存體傳輸資料 tooand
您可以使用 hello AzCopy 命令列公用程式 toocopy blob、 檔案和資料表資料儲存體帳戶中或跨儲存體帳戶。 請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)如需詳細資訊。

AzCopy 之上 hello [Azure 資料移動文件庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)，這是目前可供預覽。

hello Azure 匯入/匯出服務會提供方式 tooimport blob 資料，或從透過郵寄 toohello Azure 資料中心的硬碟磁碟儲存體帳戶匯出 blob 資料。 如需 hello 匯入/匯出服務的詳細資訊，請參閱[使用 hello Microsoft Azure 匯入/匯出服務 tooTransfer 資料 tooBlob 儲存體](storage-import-export-service.md)。

## <a name="pricing"></a>價格
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>儲存體 API、程式庫和工具
任何可提出 HTTP/HTTPS 要求的語言皆可存取 Azure 儲存體資源。 另外，Azure 儲存體還提供了幾種熱門語言的程式設計程式庫。 這些程式庫可透過處理詳細資料 (例如同步和非同步叫用、進行批次作業、例外狀況管理、自動重試、運作方式等等) 來簡化使用 Azure 儲存體的許多項目。 程式庫目前可提供下列語言的 hello，而且平台，使用與其他人 hello 管線：

### <a name="azure-storage-data-services"></a>Azure 儲存體資料服務
* [儲存體服務 REST API](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [適用於 .NET、Windows Phone 和 Windows 執行階段的儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [適用於 Java/Android 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/java/)
* [適用於 Node.js 的儲存體用戶端程式庫](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [適用於 PHP 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/php/)
* [適用於 Ruby 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/ruby/)
* [適用於 Python 的儲存體用戶端程式庫](https://azure.microsoft.com/develop/python/)
* [PowerShell 1.0 的儲存體 Cmdlet](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Azure 儲存體管理服務
* [儲存體資源提供者 REST API 參考](/rest/api/storagerp/)
* [適用於 .NET 的儲存體資源提供者用戶端程式庫](/dotnet/api/microsoft.azure.management.storage)
* [適用於 PowerShell 1.0 的儲存體資源提供者 Cmdlet](/powershell/module/azure.storage)
* [儲存體服務管理 REST API (傳統)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Azure 儲存體資料移動服務
* [儲存體匯入/匯出服務 REST API](storage-import-export-service.md)
* [適用於 .NET 的儲存體資料移動 用戶端程式庫](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>工具和公用程式
* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* [Azure 儲存體用戶端工具](storage-explorers.md)
* [Azure SDK 及工具](https://azure.microsoft.com/tools/)
* [Azure 儲存體模擬器](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy 命令列公用程式](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>後續步驟
進一步了解 Azure 儲存體，toolearn 瀏覽這些資源：

### <a name="documentation"></a>文件
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)
* [建立儲存體帳戶](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>針對系統管理員
* [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md)
* [使用 Azure CLI 搭配 Azure 儲存體](storage-azure-cli.md)

### <a name="for-net-developers"></a>針對 .NET 開發人員
* [以 .NET 開始使用 Azure Blob 儲存體](storage-dotnet-how-to-use-blobs.md)
* [以 .NET 開始使用 Azure 表格儲存體](storage-dotnet-how-to-use-tables.md)
* [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md)
* [在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>針對 Java/Android 開發人員
* [如何從 Java 的 Blob 儲存體 toouse](storage-java-how-to-use-blob-storage.md)
* [如何從 Java 資料表儲存體 toouse](storage-java-how-to-use-table-storage.md)
* [如何從 Java 佇列儲存體 toouse](storage-java-how-to-use-queue-storage.md)
* [如何從 Java 檔案儲存體 toouse](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>針對 Node.js 開發人員
* [如何 toouse Node.js 從 Blob 儲存體](storage-nodejs-how-to-use-blob-storage.md)
* [如何 toouse 從 Node.js 的資料表儲存體](storage-nodejs-how-to-use-table-storage.md)
* [如何 toouse 從 Node.js 佇列儲存體](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>針對 PHP 開發人員
* [如何 toouse 來自 PHP 的 Blob 儲存體](storage-php-how-to-use-blobs.md)
* [如何 toouse 來自 PHP 的資料表儲存體](storage-php-how-to-use-table-storage.md)
* [如何 toouse 來自 PHP 的佇列儲存體](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>針對 Ruby 開發人員
* [如何 toouse Ruby 從 Blob 儲存體](storage-ruby-how-to-use-blob-storage.md)
* [如何 toouse Ruby 從資料表儲存體](storage-ruby-how-to-use-table-storage.md)
* [如何 toouse Ruby 從佇列儲存體](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>針對 Python 開發人員
* [如何 toouse 來自 Python 的 Blob 儲存體](storage-python-how-to-use-blob-storage.md)
* [如何 toouse 來自 Python 的資料表儲存體](storage-python-how-to-use-table-storage.md)
* [如何 toouse 來自 Python 的佇列儲存體](storage-python-how-to-use-queue-storage.md)
* [如何 toouse 來自 Python 的檔案存放裝置](storage-python-how-to-use-file-storage.md)
