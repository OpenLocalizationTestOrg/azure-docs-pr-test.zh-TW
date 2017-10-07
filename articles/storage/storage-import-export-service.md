---
title: "從 blob 儲存體 aaaUsing Azure 匯入/匯出 tootransfer 資料 tooand |Microsoft 文件"
description: "了解如何 toocreate 匯入和匯出 hello 傳輸資料 tooand 從 blob 儲存體的 Azure 入口網站中的工作。"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 84471d736d2433ffee9f49fbef91856d3dd56bb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>使用 hello Microsoft Azure 匯入/匯出服務 tootransfer 資料 tooblob 存放裝置
hello Azure 匯入/匯出服務可讓您 toosecurely 傳輸大量資料 tooAzure blob 儲存體傳送的硬碟機 tooan Azure 資料中心。 您也可以使用這項服務 tootransfer 資料從 Azure blob 儲存體 toohard 磁碟機上和出貨 tooyour 在內部部署站台。 這個服務是適合您想要 tootransfer 數 tb 資料 tooor 從 Azure，但上傳或下載 hello 網路上是不可行，因為 toolimited 頻寬或高的網路成本。

hello 服務需要的硬碟機應 BitLocker 加密的資料的 hello 安全性。 hello 服務支援這兩個 hello 傳統和 Azure 資源管理員儲存體帳戶 （標準，也很酷層） 出現在所有的公用 Azure 的 hello 區域。 您必須提供指定的本文中稍後的 hello 支援位置的硬碟機 tooone。

在本文中，您進一步了解 hello Azure 匯入/匯出服務和 tooship 來複製資料 tooand 從 Azure Blob 儲存體的磁碟機。

## <a name="when-should-i-use-hello-azure-importexport-service"></a>何時應該使用 hello Azure 匯入/匯出服務？
請考慮使用 Azure 匯入/匯出服務上傳或下載資料透過 hello 網路太慢，或取得額外的網路頻寬成本增高時。

您可以使用此服務的案例，例如︰

* 移轉資料 toohello 雲端： 快速移動大量資料 tooAzure 和成本效益。
* 內容發佈： 快速傳送資料 tooyour 客戶站台。
* 備份： 在 Azure blob 儲存體需要您在內部部署資料 toostore 的備份。
* 資料復原： 復原大量的資料儲存在 blob 儲存體，並傳遞 tooyour 在內部部署位置。

## <a name="prerequisites"></a>必要條件
本節列出 hello 必要條件需要的 toouse 這項服務。 請先仔細檢閱，再運送您的磁碟機。

### <a name="storage-account"></a>儲存體帳戶
您必須擁有現有的 Azure 訂用帳戶和一個或多個儲存體帳戶 toouse hello 匯入/匯出服務。 每個工作可能會使用的 tootransfer 資料 tooor 從一個儲存體帳戶。 換句話說，單一匯入/匯出作業不能跨越多個儲存體帳戶。 如需建立新的儲存體帳戶資訊，請參閱[如何 tooCreate 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)。

### <a name="blob-types"></a>Blob 類型
您也可以使用 Azure 匯入/匯出服務 toocopy 資料**區塊**blob 或**頁面**blob。 相反地，您只能使用此服務從 Azure 儲存體匯出**區塊** Blob、**分頁** Blob 或**附加** Blob。

### <a name="job"></a>作業
匯入匯出從 Blob 儲存體 tooor toobegin hello 過程中的，您先建立作業。 此工作可以是「匯入工作」或「匯出工作」：

* 當您想要您的 Azure 儲存體帳戶中有內部 tooblobs tootransfer 資料時，請建立匯入工作。
* 建立匯出工作時要 tootransfer 資料目前儲存為您儲存體帳戶 toohard 的磁碟機中的 blob 隨附 tooyou.s 的建立作業時，通知 hello 匯入/匯出服務，您將運送一或多硬碟磁碟機 tooan Azure資料中心。

* 若為匯入工作，您將運送含有資料的硬碟。
* 若為匯出工作，您將運送空的硬碟。
* 您可以送出每個作業 too10 硬碟磁碟機上。

您可以建立的匯入或匯出工作使用 hello Azure 入口網站或 hello [Azure 儲存體匯入/匯出 REST API](/rest/api/storageimportexport)。

### <a name="waimportexport-tool"></a>WAImportExport 工具
建立 hello 第一個步驟**匯入**作業是 tooprepare 您將運送匯入的磁碟機。 tooprepare 您的磁碟機，必須先連接 tooa 本機伺服器與 hello 本機伺服器上執行的 hello WAImportExport 工具。 此 WAImportExport 工具有助於進行複製資料的 toohello 磁碟機、 hello hello BitLocker 磁碟機上的資料加密及產生 hello 磁碟機日誌檔案。

hello 日誌檔案會儲存您的工作與磁碟機，例如磁碟機序號和儲存體帳戶名稱的基本資訊。 這個日誌檔不會儲存在 hello 磁碟機上。 建立匯入工作期間，會使用它。 建立工作的逐步解說詳細資料會在本文中稍後提供。

hello WAImportExport 工具僅與 64 位元 Windows 作業系統相容。 請參閱 hello[作業系統](#operating-system)一節以取得支援的特定作業系統版本。

下載 hello 最新版 hello [WAImportExport 工具](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip)。 如需詳細資訊，需使用 hello WAImportExport 工具，請參閱 < hello[使用 hello WAImportExport 工具](storage-import-export-tool-how-to.md)。

>[!NOTE]
>**先前版本：**可以[下載 WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip)版的 hello 工具，並參閱太[WAImportExpot V1 使用量指南](storage-import-export-tool-how-to-v1.md)。 Hello 工具 WAImportExpot V1 版提供的支援**當資料已經預先寫入 toohello 磁碟準備磁碟**。 此外您將需要 toouse WAImportExpot V1 工具如果 hello 可用的唯一金鑰是 SAS 金鑰。

>

### <a name="hard-disk-drives"></a>硬碟
只有 2.5 英吋 SSD 或 2.5"或 3.5" SATA II 或 III 內部 HDD 支援 hello 匯入/匯出服務搭配使用。 單一匯入/匯出作業最多可以有 10 個 HDD/SSD，且每個個別 HDD/SSD 的大小不拘。 大量的磁碟機可以分散到多個工作，而且沒有可以建立工作的 hello 數目沒有限制。 

匯入作業將會處理上只有 hello 第一個資料磁碟區 hello 磁碟機上。 hello 資料磁碟區必須格式化為 NTFS。

> [!IMPORTANT]
> 此服務不支援隨附內建 USB 介面卡的外接式硬碟。 此外，您無法使用 hello 磁碟內的外部 HDD 的 hello 大小寫;請不要將外部 Hdd。
> 
> 

以下是一份外部 USB 介面卡使用 toocopy 資料 toointernal Hdd。 Anker 68UPSATAA-02BU Anker 68UPSHHDS-BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (6628 Series) Thermaltake BlacX Hot-Swap SATA External Hard Drive Docking Station (USB 2.0 & eSATA)

### <a name="encryption"></a>加密
必須使用 BitLocker 磁碟機加密來加密 hello hello 磁碟機上的資料。 此功能可保護傳輸中的資料。

匯入工作，都有兩種方式 tooperform hello 加密。 hello 第一種方法執行期間磁碟機準備 hello WAImportExport 工具時使用資料集的 CSV 檔案時 toospecify hello 選項。 hello 第二種方式是 tooenable 手動 hello 磁碟機上的 BitLocker 加密，並指定 hello driveset CSV 中的 hello 加密金鑰，在磁碟機準備期間執行 WAImportExport 工具命令列時發生。

匯出工作，您的資料複製的 toohello 磁碟機之後, 便可 hello 服務加密 hello 之前傳送它回復 tooyou 使用 BitLocker 的磁碟機。 會透過 Azure 入口網站 hello tooyou 提供 hello 加密金鑰。  

### <a name="operating-system"></a>作業系統
您可以使用下列 64 位元作業系統 tooprepare hello 硬碟使用 hello WAImportExport 工具之前傳送嗨磁碟機 tooAzure hello 的其中一個：

Windows 7 Enterprise、Windows 7 Ultimate、Windows 8 Pro、Windows 8 Enterprise、Windows 8.1 Pro、Windows 8.1 Enterprise、Windows 10<sup>1</sup>、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2。 所有這些作業系統都支援 BitLocker 磁碟機加密。

### <a name="locations"></a>位置
hello Azure 匯入/匯出服務支援從所有公用 Azure 儲存體帳戶複製資料 tooand。 您可以送出 hello 下列位置的硬碟機 tooone。 如果您的儲存體帳戶在這裡沒有指定，會提供替代的傳送位置，當您建立的公用 Azure 位置 hello 作業使用 hello Azure 入口網站或 hello 匯入/匯出 REST API。

支援的運送位置︰

* 美國東部
* 美國西部
* 美國東部 2
* 美國西部 2
* 美國中部
* 美國中北部
* 美國中南部
* 美國中西部
* 北歐
* 西歐
* 東亞
* 東南亞
* 澳洲東部
* 澳大利亞東南部
* 日本西部
* 日本東部
* 印度中部
* 印度南部
* 印度西部
* 加拿大中部
* 加拿大東部
* 巴西南部
* 韓國中部
* 美國政府維吉尼亞州
* 美國政府愛荷華州
* 美國 DoD 東部
* 美國國防部中央
* 中國東部
* 中國北部
* 英國南部

### <a name="shipping"></a>運送中
**傳送磁碟機 toohello 資料中心：**

當建立匯入或匯出工作，您會提供送貨地址的 hello 的其中一個支援的位置 tooship 您的磁碟機。 hello 送貨地址提供將取決於 hello 位置的儲存體帳戶，但它可能不是相同 hello 做為儲存體帳戶位置。

您可以使用像是 fedex 寄送、 DHL、 UPS 或 hello 美國郵遞服務 tooship 的承運業者寄送您的磁碟機 toohello 送貨地址。

**Hello 資料中心傳送磁碟機：**

建立匯入或匯出作業時，您必須提供傳回位址，如 Microsoft toouse 時傳送嗨磁碟機備份您的工作完成後即可。 請確定您提供有效的地址 tooavoid 延遲處理。

您可以使用您選擇的承運業者順序 tooforward 出貨 hello 硬碟中。 hello 貨運公司應該有適當的監督鏈的順序 toomaintain 鏈結中的追蹤。 您也必須提供有效的 fedex 寄送或 DHL 承運業者帳戶號碼 toobe Microsoft 用於 hello 磁碟機寄送回。 需要傳送 hello 美國和歐洲位置從磁碟機 fedex 寄送帳戶號碼。 從亞洲和澳洲位置送回磁碟機則需要 DHL 客戶編號。 您可以建立 [FedEx](http://www.fedex.com/us/oadr/) (適用於美國和歐洲) 或 [DHL](http://www.dhl.com/) (亞洲和澳洲) 貨運業者帳戶 (若沒有的話)。 如果您已經有貨運公司客戶編號，請確認它有效。

傳送您的封裝，您必須遵循在 hello 條款[Microsoft Azure 服務條款](https://azure.microsoft.com/support/legal/services-terms/)。

> [!IMPORTANT]
> 請注意您傳送的 hello 實體媒體，可能需要 toocross 國際框線。 您必須負責確保，您的實體媒體和資料匯入和/或根據 hello 適用法律匯出。 之前傳送嗨實體媒體，請洽詢 advisers tooverify 您的媒體和資料可以遵循和法令會識別已出貨的 toohello 資料中心。 這可協助達到 Microsoft 及時 tooensure。 比方說，任何會跨國際框線的封裝需要商業發票 toobe 附上 hello 封裝 （除了如果跨越歐盟內框線）。 您無法列印出 hello 商業發票從貨運公司網站的區域分布副本。 商業發票的範例為 [DHL 商業發票 (英文)](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) 和 [FedEx 商業發票 (英文)](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf)。 請確定 Microsoft hello 匯出工具為未被指示。
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Hello Azure 匯入/匯出服務如何運作？
您可以在內部部署站台與 Azure blob 儲存體使用 hello Azure 匯入/匯出服務建立工作，並傳送硬碟機 tooan Azure 資料中心之間傳輸資料。 您運送的每個硬碟都與單一作業相關聯。 每個工作都與單一儲存體帳戶相關聯。 檢閱 hello[先決條件 > 一節](#pre-requisites)仔細 toolearn 相關的此服務，例如支援 blob 類型、 磁碟類型、 位置和傳送的 hello 細節。

在本節中，我們將描述高的層級 hello 步驟，與匯入和匯出工作。 稍後 hello[快速入門 > 一節](#quick-start)，我們提供逐步指示 toocreate 匯入和匯出作業。

### <a name="inside-an-import-job"></a>匯入作業之內
概括而言，匯入工作牽涉到 hello 下列步驟：

* Hello 資料 toobe 匯入，然後 hello 您需要的磁碟機數目。
* 識別 hello 目的地 blob 位置中 Blob 儲存體的資料。
* 使用 WAImportExport 工具 toocopy hello 資料 tooone 或多個硬碟機，並使用 BitLocker 來加密認證。
* 在您使用 hello Azure 入口網站的目標儲存體帳戶中建立匯入工作或 hello 匯入/匯出 REST API。 如果使用 hello Azure 入口網站上, 傳 hello 磁碟機日誌檔案。
* 提供 hello 寄件地址和承運業者帳戶號碼 toobe 用於傳送嗨磁碟機後 tooyou。
* 出貨送貨地址提供在建立工作時硬碟機 toohello hello。
* 更新追蹤編號 hello 匯入工作詳細資料中的 hello 傳遞並送出 hello 匯入工作。
* 磁碟機是接收並處理 hello Azure 資料中心。
* 磁碟機寄使用承運業者帳戶 toohello 傳回地址 hello 匯入工作中提供。
  
    ![圖 1: 匯入工作流程](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>匯出作業之內
在高層級，匯出作業牽涉到 hello 下列步驟：

* 決定 hello 資料 toobe 匯出和 hello 您需要的磁碟機數目。
* 識別 hello 來源 blob 或 Blob 儲存體中的資料容器路徑。
* 在來源儲存體帳戶使用 hello Azure 入口網站中建立匯出工作或 hello 匯入/匯出 REST API。
* 指定 hello 來源 blob 或容器路徑 hello 中的資料匯出工作。
* 提供用於傳送嗨磁碟機後 tooyou toobe hello 傳回地址和承運業者帳戶號碼。
* 出貨送貨地址提供在建立工作時硬碟機 toohello hello。
* 更新追蹤編號 hello 匯出工作的詳細資料中的 hello 傳遞並送出 hello 匯出工作。
* hello 磁碟機是接收，並在 hello Azure 資料中心處理。
* hello 磁碟機加密使用 BitLocker。hello 索引鍵是可透過 hello Azure 入口網站。  
* hello 磁碟機寄使用承運業者帳戶 toohello 傳回地址 hello 匯入工作中提供。
  
    ![圖 2: 匯出工作流程](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>檢視您的工作和磁碟機狀態
您可以追蹤您匯入的 hello 狀態，或匯出工作從 hello Azure 入口網站。 按一下 hello**匯入/匯出** 索引標籤。您的工作清單會出現在 hello 頁面。

![檢視工作狀態](./media/storage-import-export-service/jobstate.png)

您會看到一個 hello 遵循根據您的磁碟機所在 hello 程序中的作業狀態。

| 工作狀態 | 說明 |
|:--- |:--- |
| 建立中 | 會建立一個作業之後，其狀態會設定 tooCreating。 Hello 作業在 hello 建立狀態時，hello 匯入/匯出服務會假設 hello 磁碟機尚未已出貨的 toohello 資料中心。 作業可能會維持在 hello 建立狀態 tootwo 週之後, 便會自動刪除 hello 服務所組成。 |
| 運送中 | 您寄送您的封裝之後，您應該更新 hello 追蹤 hello Azure 入口網站中的資訊。  這會變成"Shipping"hello 作業。 hello 作業會保留在 hello Shipping 狀態，如總 tootwo 週。 
| 已收到 | 所有磁碟都已都收到 hello 資料中心之後，hello 作業狀態將設 toohello 都接收。 |
| 傳輸中 | 至少一個磁碟機已開始處理，一旦 hello 工作狀態將 toohello 轉移。 請參閱 hello 磁碟機狀態下面章節，如需詳細資訊。 |
| 包裝中 | 所有磁碟機已完成處理之後，hello 作業將放在 hello 封裝狀態，直到 hello 磁碟機已出貨後 tooyou。 |
| Completed | 所有磁碟機已出貨後 toohello 客戶如果 hello 作業已完成不會發生錯誤之後再 hello 工作會設定 toohello 已完成狀態。 hello 作業將在 hello 已完成狀態中的 90 天後自動刪除。 |
| 關閉 | 如果已有任何錯誤 hello hello 作業處理期間，所有磁碟機已被已出貨後 toohello 客戶之後，再 hello 工作會設定 toohello 已關閉的狀態。 hello 作業將會自動在 90 天後在刪除 hello 已關閉狀態。 |

hello 下表描述 hello 生命週期，個別的磁碟機的過程中轉換匯入或匯出工作。 現在從 hello Azure 入口網站看見 hello 的作業中的每個磁碟機的目前狀態。
hello 下表說明每個工作中的每個磁碟機可能經歷的狀態。

| 磁碟機狀態 | 說明 |
|:--- |:--- |
| 已指定 | 匯入工作，從 hello Azure 入口網站建立 hello 作業時 hello 磁碟機的初始狀態會是 hello 指定狀態。 匯出工作，因為建立 hello 作業時，指定沒有磁碟機 hello 初始磁碟機狀態是 hello 已接收 」 狀態。 |
| 已收到 | 當 hello 匯入/匯出服務操作員已經處理 hello 磁碟機已收到從 hello 傳送公司匯入工作的 hello 磁碟機就會轉變 toohello 已接收 」 狀態。 匯出工作，hello 初始磁碟機狀態是 hello 已接收 」 狀態。 |
| 從未收到 | hello 磁碟機會移 toohello NeverReceived 狀態，當 hello 工作的包裹抵達但 hello 封裝不包含 hello 磁碟機。 如果已經兩週 hello 服務收到 hello 傳送的資訊，但 hello 封裝有尚未抵達 hello 資料中心，磁碟機也可以移動進入此狀態。 |
| 傳輸中 | Hello 服務開始 tootransfer hello 磁碟機 tooWindows Azure 儲存體的資料時，磁碟機會移 toohello 轉移狀態。 |
| Completed | Hello 服務已順利傳送所有的 hello 資料，且未發生錯誤時，磁碟機會移 toohello 已完成狀態。
| 已完成 (其他資訊) | 磁碟機會移 toohello CompletedMoreInfo 狀態時 hello 服務發生一些問題複製資料時從或 toohello 磁碟機。 hello 資訊可能包括錯誤、 警告或參考用訊息有關覆寫 blob。
| 已寄回 | hello 磁碟機會移 toohello ShippedBack 狀態，當已出貨從 hello 資料中心回 toohello 傳回位址。 |

此映像從 hello Azure 入口網站會顯示 hello 磁碟機狀態的範例作業：

![檢視磁碟機狀態](./media/storage-import-export-service/drivestate.png)

hello 以下表格說明 hello 磁碟機失敗狀態，以及所採取的每個狀態的 hello 動作。

| 磁碟機狀態 | Event | 解決方法/後續步驟 |
|:--- |:--- |:--- |
| 從未收到 | 已標示為 NeverReceived （因為它未收到 hello 作業的出貨的一部分） 到達另一個 「 出貨 」 中的磁碟機。 | hello 作業小組會移動 hello 磁碟機 toohello 已接收 」 狀態。 |
| N/A | 不屬於任何工作的磁碟機送達 hello 資料中心做為另一項工作的一部分。 | hello 磁碟機將會標示為額外的磁碟機，並將傳回 toohello 客戶 hello 與 hello 原始封裝相關聯的工作完成時。 |

### <a name="time-tooprocess-job"></a>時間 tooprocess 工作
hello tooprocess 匯入/匯出作業會根據不同的因素，例如傳送時間，作業類型而有所不同花費的時間類型的量與大小 hello 被複製資料和 hello 提供 hello 磁碟的大小。 hello 匯入/匯出服務沒有 SLA 但 hello 服務在收到 hello 磁碟之後會設法 toocomplete hello 複製 7 too10 天。 您可以更接近使用 hello REST API tootrack hello 工作進度。 列出工作的作業，它會指出複製進度 hello 沒有百分比完整的參數。 聯繫 toous，如果您需要估計 toocomplete 時間關鍵的匯入/匯出作業。

### <a name="pricing"></a>價格
**磁碟機處理費用**

在匯入或匯出工作當中，對於所處理的每個磁碟機會有一項磁碟機處理費用。 Hello 詳細資料請參閱 hello [Azure 匯入/匯出定價](https://azure.microsoft.com/pricing/details/storage-import-export/)。

**運送成本**

當您寄送磁碟機 tooAzure 時，您付費 hello 運送成本 toohello 出貨承運業者。 Microsoft 會傳回 hello 磁碟機 tooyou hello 送貨成本會負責您提供給作業的建立時間 hello toohello 承運業者帳戶。

**交易成本**

將資料匯入到 Blob 儲存體時，沒有交易成本。 從 blob 儲存體匯出資料時，才適用於 hello 標準輸出費用。 如需交易成本的更多詳細資料，請參閱 [資料傳輸價格](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>快速啟動
在本節中，我們將提供如何建立匯入和匯出作業的逐步指示。 請確定您符合所有 hello[先決條件](#pre-requisites)之前繼續進行後續步驟。

> [!IMPORTANT]
> hello 服務支援一個標準儲存體帳戶，每個匯入或匯出作業並不支援進階儲存體帳戶。 
> 
> 
## <a name="create-an-import-job"></a>建立匯入作業
傳送含有資料 toohello 指定的資料中心的一個或多個磁碟機從硬碟來建立匯入作業 toocopy 資料 tooyour Azure 儲存體帳戶。 hello 匯入工作要傳達有關硬碟機的詳細資料，資料 toobe 複製，目標儲存體帳戶，和出貨資訊 toohello Azure 匯入/匯出服務。 建立匯入工作是一個包含三步驟的程序。 首先，準備您的磁碟機使用 hello WAImportExport 工具。 第二，提交匯入工作使用 hello Azure 入口網站。 第三，出貨 hello 磁碟機 toohello 傳送期間作業建立和更新 hello 貨運資訊在您的工作詳細資料中提供的位址。   

### <a name="prepare-your-drives"></a>準備磁碟機
hello 第一個步驟匯入資料使用 hello Azure 匯入/匯出服務是 tooprepare 當您使用 hello WAImportExport 工具的磁碟機。 遵循下列 tooprepare hello 步驟是您的磁碟機。

1. 識別 hello 資料 toobe 匯入。 這可能是目錄和獨立 hello 本機伺服器上的檔案或網路共用。  
2. 決定您需要根據 hello 資料的總大小的磁碟機的 hello 數目。 取得所需的 hello 數目 2.5 英吋 SSD 或 2.5"或 3.5" SATA II 或 III 硬碟機。
3. 找出 hello 目標儲存體帳戶、 容器、 虛擬目錄和 blob。
4.  判斷 hello 目錄和/或獨立的檔案將會複製的 tooeach 硬碟機。
5.  建立 hello 資料集和 driveset 的 CSV 檔案。
    
    **資料集 CSV 檔案**
    
    以下是範例資料集 CSV 檔案範例︰
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    在上述範例中的 hello，100M_1.csv.txt 將名為"containername"hello 容器的複製的 toohello 根。 如果 hello 容器名稱"containername"不存在，將會建立一個。 所有檔案和資料夾下 50M_original 都會以遞迴方式複製 toocontainername。 將保留資料夾結構。

    深入了解[準備 hello 資料集中的 CSV 檔案](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file)。
    
    **請記住**： 根據預設，hello 資料將匯入為區塊 Blob。 您可以使用 hello BlobType 欄位值 tooimport 資料做為分頁 Blob。 例如，如果您要匯入將在 Azure VM 上掛接為磁碟的 VHD 檔案，必須將它們匯入為分頁 Blob。

    **磁碟機集 CSV 檔案**

    hello 值 hello driveset 旗標是為了讓 hello 工具 toocorrectly 對應的 CSV 檔案包含的磁碟 toowhich hello 磁碟機代號 hello 清單挑選準備磁碟 toobe hello 清單。 

    以下是 hello driveset CSV 檔案範例：
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    在上述範例中的 hello，假設已連接兩個磁碟，而且在建立基本的 NTFS 磁碟區與磁碟區代號 G:\ H:\。 hello 工具將會格式化，並加密的裝載 H:\，和將未格式化或加密 hello 磁碟裝載磁碟區 G:\ hello 磁碟。

    深入了解[準備 hello driveset CSV 檔案](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file)。

6.  使用 hello [WAImportExport 工具](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip)toocopy 資料 tooone 或多個硬碟。
7.  您可以指定"Encrypt"中 drivset CSV tooenable hello 的硬碟機上的 BitLocker 加密的加密欄位。 或者，您可能也啟用手動 hello 的硬碟機上的 BitLocker 加密"AlreadyEncrypted"並指定執行 hello 工具時提供 hello driveset CSV 中的 hello 索引鍵。

8. 完成磁碟準備之後，請勿修改 hello hello 硬碟機或 hello 日誌檔資料。

> [!IMPORTANT]
> 您準備的每個硬碟都會造成一個日誌檔案。 當您建立使用 hello Azure 入口網站的 hello 匯入工作時，您必須上傳 hello 磁碟機屬於該匯入工作的所有 hello 日誌的檔案。 沒有日誌檔案的磁碟機將不會被處理。
> 
>

以下 hello 命令與 hello 硬碟準備陳述式的範例使用 WAImportExport 工具。

WAImportExport 工具 hello PrepImport 命令先複製工作階段 toocopy 目錄及/或新的複製工作階段的檔案：

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**匯入範例 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

順序太**新增更多磁碟機**，一個可建立新的 driveset 檔案和執行 hello 命令，如下所示。 對於後續複製工作階段 toohello 不同磁碟機指定 InitialDriveset.csv 檔案中，指定新 driveset CSV 檔案，並提供它做為值 toohello 參數 」 AdditionalDriveSet"。 使用 hello**相同的日誌檔**名稱，並提供**新工作階段識別碼**。 hello AdditionalDriveset CSV 檔案格式是與 InitialDriveSet 格式相同。

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**匯入範例 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

在訂單 tooadd 其他資料 toohello 相同 driveset，可以針對後續複製工作階段 toocopy 其他檔案/目錄呼叫 WAImportExport 工具 PrepImport 命令： 後續複製工作階段 toohello 相同硬碟的磁碟機中指定的InitialDriveset.csv 檔案中，指定 hello**相同的日誌檔**名稱，並提供**新工作階段識別碼**; 沒有需要 tooprovide hello 儲存體帳戶金鑰。

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**匯入範例 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

查看使用中的 hello WAImportExport 工具的詳細[硬碟準備匯入](storage-import-export-tool-preparing-hard-drives-import.md)。

此外，請參閱 toohello[範例工作流程匯入工作 tooprepare 硬碟機](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)如需詳細的逐步指示。  

### <a name="create-hello-import-job"></a>建立 hello 匯入工作
1. 一旦您已經備妥您的磁碟機，請瀏覽 tooyour hello Azure 入口網站中的儲存體帳戶，以及檢視 hello 儀表板。 在 **[快速概覽]** 之下，按一下 **[建立匯入工作]**。 檢閱 hello 步驟，然後選取 [hello] 核取方塊 tooindicate 已經備妥您的磁碟機，而且您擁有 hello 可用的磁碟機日誌檔案。
2. 在步驟 1 中，提供負責這個匯入工作及有效的回覆地址的 hello 人員的連絡資訊。 如果您想 toosave hello 匯入工作的詳細資訊記錄檔資料，請檢查 hello 選項太**我 'waimportexport' blob 容器中的儲存 hello 詳細資訊記錄**。
3. 在步驟 2 中上, 傳您 hello 磁碟機準備步驟期間取得的 hello 磁碟機日誌檔案。 您必須為每個磁碟機，您已經備妥 tooupload 一個檔案。
   
   ![建立匯入工作 - 步驟 3](./media/storage-import-export-service/import-job-03.png)
4. 步驟 3 中，輸入 hello 匯入工作的描述性名稱。 請注意您所輸入的 hello 名稱可包含小寫字母、 數字、 連字號和底線，必須以字母開頭，而且不能包含空格。 您將使用您將 tootrack 選擇您的工作，都在進行中另一次，便會完成的 hello 名稱。
   
   接下來，從 hello 清單中選取您的資料中心區域。 hello 資料中心區域會顯示 hello 資料中心，並解決 toowhich 您撽拶嫋您的封裝。 請參閱下方的詳細資訊的 hello 常見問題集。
5. 在步驟 4 中，從 hello 清單中選取 貨運公司，並輸入您的承運業者帳戶號碼。 匯入工作完成之後，Microsoft 會使用此帳戶 tooship hello 磁碟機後 tooyou。
   
   如果您有追蹤號碼，從 hello 清單中選取您遞送承運業者並輸入您的追蹤號碼。
   
   如果您沒有數字，但選擇追蹤**我寄送包裹之後，我會提供這個匯入工作傳送資訊**，然後完成 hello 匯入程序。
6. tooenter 您的追蹤號碼之後已寄出您的封裝，傳回 toohello**匯入/匯出**hello Azure 入口網站中，儲存體帳戶頁面上，從 hello 清單中，選取您的工作，然後選擇 **出貨資訊**. 瀏覽 hello 精靈，並在步驟 2 中輸入您的追蹤號碼。
   
    如果沒有建立 hello 作業前 2 週更新 hello 追蹤號碼，hello 工作會過期。
   
    如果 hello 作業在 hello 建立、 傳送或轉移狀態，您也可以更新您承運業者帳戶號碼在步驟 2 中的 hello 精靈。 一旦 hello 工作處於 hello 包裝中 狀態，您無法更新您的承運業者帳戶號碼，該工作。
7. 您可以追蹤工作進度 hello 入口網站儀表板上。 請參閱 hello 前一節中的每個工作狀態表示由[檢視工作狀態](#viewing-your-job-status)。

## <a name="create-an-export-job"></a>建立匯出工作
建立匯出工作 toonotify hello 匯入/匯出服務，您將會傳送一個或多個空的磁碟機 toohello 資料中心，讓資料可以從您的儲存體帳戶 toohello 磁碟機中匯出並 hello 磁碟機然後出貨 tooyou。

### <a name="prepare-your-drives"></a>準備磁碟機
準備磁碟機以進行匯出工作時，建議進行下列預先檢查︰

1. 檢查 hello 號碼使用 hello WAImportExport 工具的 PreviewExport 命令所需的磁碟。 如需詳細資訊，請參閱 [Previewing Drive Usage for an Export Job (預覽匯出作業的磁碟機使用量)](https://msdn.microsoft.com/library/azure/dn722414.aspx)。 它可協助您預覽 hello blob，您所選取的磁碟機使用量，根據 hello hello 磁碟機大小要 toouse。
2. 請檢查您可以讀取/寫入 toohello 將運送 hello 匯出工作的硬碟機。

### <a name="create-hello-export-job"></a>建立 hello 匯出工作
1. toocreate 為匯出工作，瀏覽 tooyour hello Azure 入口網站中的儲存體帳戶，以及檢視 hello 儀表板。 在下**快速概覽**，按一下 **建立匯出工作**並繼續完成 hello 精靈。
2. 在步驟 2 中，提供這個匯出工作負責的 hello 人員的連絡資訊。 如果您想 toosave hello 匯出工作的詳細資訊記錄檔資料，請檢查 hello 選項太**我 'waimportexport' blob 容器中的儲存 hello 詳細資訊記錄**。
3. 步驟 3 中，指定您想 tooexport 從您的儲存體帳戶 tooyour 空白資料磁碟機或磁碟機的 blob。 您可以選擇 tooexport 所有 blob 資料 hello 儲存體帳戶中，或者您可以指定 blob 或 blob tooexport 的設定。
   
   toospecify blob tooexport，使用 hello **Equal To**選取器，並指定 hello 相對路徑 toohello blob 並 hello 容器名稱開頭。 使用*$root* toospecify hello 根容器。
   
   toospecify 所有 blob 開頭的前置詞使用 hello**開頭**選取器，並指定 hello 前置詞開頭是正斜線 '/'。 hello 前置詞可能會 hello hello 容器名稱、 hello 完整容器名稱，或 hello 完整容器名稱，後面接著 hello hello blob 名稱前置詞的前置詞。
   
   hello 下表顯示有效 blob 路徑的範例：
   
   | 選取器 | Blob 路徑 | 說明 |
   | --- | --- | --- |
   | 開頭為 |/ |將匯出的 hello 儲存體帳戶中的所有 blob |
   | 開頭為 |/$root/ |將匯出的 hello 根容器中的所有 blob |
   | 開頭為 |/book |匯出任何容器中以首碼 **book** |
   | 開頭為 |/music/ |匯出容器 **music** |
   | 開頭為 |/music/love |匯出容器 **music** 中以首碼 **love** 開頭的所有 Blob |
   | 太等於|$root/logo.bmp |匯出 blob **logo.bmp** hello 根容器中 |
   | 太等於|videos/story.mp4 |匯出容器 **videos** 中的 Blob **story.mp4** |
   
   您必須提供有效的格式中的 hello blob 路徑 tooavoid 錯誤在處理期間，此螢幕擷取畫面所示。
   
   ![建立匯出工作 - 步驟 3](./media/storage-import-export-service/export-job-03.png)
4. 在步驟 4 中，輸入 hello 匯出工作的描述性名稱。 您所輸入的 hello 名稱可包含小寫字母、 數字、 連字號和底線，必須以字母開頭，而且不能包含空格。
   
   hello 資料中心區域會顯示 hello 資料中心 toowhich 您撽拶嫋您的封裝。 請參閱下方的詳細資訊的 hello 常見問題集。
5. 在步驟 5 中，選取貨運公司 hello 清單中，並輸入您的承運業者帳戶號碼。 Microsoft 會使用此帳戶 tooship 匯出工作完成之後，您的磁碟機備份 tooyou。
   
   如果您有追蹤號碼，從 hello 清單中選取您遞送承運業者並輸入您的追蹤號碼。
   
   如果您沒有數字，但選擇追蹤**我寄送包裹之後，我會提供這個匯出工作的出貨資訊**，然後完成 hello 匯出程序。
6. tooenter 您的追蹤號碼之後已寄出您的封裝，傳回 toohello**匯入/匯出**hello Azure 入口網站中，儲存體帳戶頁面上，從 hello 清單中，選取您的工作，然後選擇 **出貨資訊**. 瀏覽 hello 精靈，並在步驟 2 中輸入您的追蹤號碼。
   
    如果沒有建立 hello 作業前 2 週更新 hello 追蹤號碼，hello 工作會過期。
   
    如果 hello 作業在 hello 建立、 傳送或轉移狀態，您也可以更新您承運業者帳戶號碼在步驟 2 中的 hello 精靈。 一旦 hello 工作處於 hello 包裝中 狀態，您無法更新您的承運業者帳戶號碼，該工作。
   
   > [!NOTE]
   > 如果匯出的 hello blob toobe 次複製 toohard 磁碟機的 hello 的使用中，Azure 匯入/匯出服務將採取 hello blob 和複製 hello 的快照集的快照集。
   > 
   > 
7. 您可以在 hello Azure 入口網站中的 hello 儀表板上追蹤工作進度。 請參閱每個作業的狀態表示 hello 前一節中的 「 檢視工作狀態 」。
8. 在收到 hello 磁碟機與您匯出的資料之後，您可以檢視和複製您的磁碟機的 hello 服務所產生的 hello BitLocker 金鑰。 瀏覽 tooyour hello Azure 入口網站中的儲存體帳戶，然後按一下 hello 匯入/匯出 索引標籤。從 hello 清單中，選取匯出工作，然後按一下 hello 檢視金鑰 按鈕。 hello BitLocker 金鑰會出現如下所示：
   
   ![檢視匯出工作的 BitLocker 金鑰](./media/storage-import-export-service/export-job-bitlocker-keys.png)

請因為它涵蓋了使用這項服務時，客戶遇到 hello 最常見的問題，移透過以下的 hello 常見問題集 > 一節。

## <a name="frequently-asked-questions"></a>常見問題集

**可以將複製使用 hello Azure 匯入/匯出服務的 Azure 檔案儲存體？**

否，hello Azure 匯入/匯出服務僅支援區塊 Blob 和分頁 Blob。 不支援其他所有儲存體類型，包括 Azure 檔案儲存體、表格儲存體和佇列儲存體。

**是可用的 CSP 訂閱 hello Azure 匯入/匯出服務？**

Azure 匯入/匯出服務確實支援 CSP 訂用帳戶。

**可以略過 hello 磁碟機準備步驟匯入工作，或可以準備磁碟機而不複製？**

任何您想要 tooship 匯入資料的磁碟機必須使用 hello Azure WAImportExport 工具備妥。 您必須使用 hello WAImportExport 工具 toocopy 資料 toohello 磁碟機。

**我需要 tooperform 任何磁碟準備時建立匯出工作？**

不需要，但建議先執行一些前置檢查。 檢查 hello 號碼使用 hello WAImportExport 工具的 PreviewExport 命令所需的磁碟。 如需詳細資訊，請參閱 [Previewing Drive Usage for an Export Job (預覽匯出作業的磁碟機使用量)](https://msdn.microsoft.com/library/azure/dn722414.aspx)。 它可協助您預覽 hello blob，您所選取的磁碟機使用量，根據 hello hello 磁碟機大小要 toouse。 也確認您可以從讀取和寫入 toohello 硬碟會隨附 hello 匯出工作。

**如果不小心傳送不符合 toohello HDD，會發生什麼情況支援需求？**

hello Azure 資料中心將會傳回不符合支援 toohello 需求 tooyou hello 磁碟機。 如果只有部分 hello hello 封裝中的磁碟機符合 hello 支援需求，將處理這些磁碟機，並會傳回不符合 hello 需求的 hello 磁碟機 tooyou。

**我可以取消工作嗎？**

您可以在工作狀態為 [建立中] 或 [運送中] 時取消工作。

**多久 hello Azure 入口網站中檢視已完成工作的狀態，hello？**

您可以檢視已完成工作的總 too90 天 hello 狀態。 已完成的作業會在 90 天後刪除。

**如果我想 tooimport 或匯出 10 個以上的磁碟機，我該怎麼辦？**

有一個匯入或匯出工作可以參考在 hello 匯入/匯出服務的單一工作只限於 10 個磁碟機。 如果您想 tooship 10 個以上的磁碟機，您可以建立多個工作。 相同的作業必須一起隨附於的 hello 與相關聯的磁碟機 hello 相同的封裝。
若資料容量跨越多個磁碟匯入工作，Microsoft 會提供指導與協助。 如需詳細資訊，請連絡 bulkimport@microsoft.com

**沒有 hello 服務格式 hello 磁碟機，再傳回它們嗎？**

否。 所有磁碟機都使用 BitLocker 加密。

**我可以為了匯入/匯出工作向 Microsoft 購買磁碟機嗎？**

否。 您將需要的 tooship 自己的磁碟機，同時匯入和匯出工作。

** 如何存取這個服務所匯入的資料**

使用獨立的工具呼叫儲存體總管或可透過 hello Azure 入口網站存取您的 Azure 儲存體帳戶的 hello 資料。 https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Hello 匯入作業完成後，將我的資料的外觀為何 hello 儲存體帳戶中？將保留我的目錄階層嗎？**

當準備匯入工作時硬碟機，hello 目的地被指定集中 CSV hello DstBlobPathOrPrefix 欄位。 這是在 hello hello 硬碟機的資料複製的儲存體帳戶 toowhich hello 目的地容器。 在此目的容器，從 hello 硬碟的資料夾來建立虛擬目錄並建立檔案的 blob。 

**Hello 磁碟機是否已存在於儲存體帳戶的檔案，將會 hello 服務覆寫現有的 blob 儲存體帳戶中？**

當您準備 hello 磁碟機，您可以指定 hello 目的地檔案應該覆寫還是略過使用資料集稱為 「 配置的 CSV 檔案中的 hello 欄位： < 命名 | 否-覆寫 | 覆寫 >。 根據預設，hello 服務將會重新命名 hello 新檔案，而不要覆寫現有的 blob。

**是 hello WAImportExport 工具與 32 位元作業系統相容？**
否。 hello WAImportExport 工具僅與 64 位元 Windows 作業系統相容。 請參閱 hello toohello 作業系統 > 一節[先決條件](#pre-requisites)如需支援的 OS 版本的完整清單。

**應該包含 hello 硬碟磁碟機以外的任何在我的套件嗎？**

僅限寄送硬碟機。 請勿加入電源線或 USB 纜線等項目。

**我是否必須 tooship 使用 fedex 寄送或 DHL 我的磁碟機？**

您可以寄送磁碟機 toohello 資料中心使用任何已知的承運業者，像是 fedex 寄送、 DHL、 UPS 或美國郵遞服務。 不過，傳送嗨磁碟機後 tooyou hello 資料中心，您必須提供 fedex 寄送帳戶號碼在 hello 美國與歐盟或在 hello 亞洲和澳洲地區 DHL 帳戶號碼。

**將我的磁碟機進行國際運送有任何限制嗎？**

請注意您傳送的 hello 實體媒體，可能需要 toocross 國際框線。 您必須負責確保，您的實體媒體和資料匯入和/或根據 hello 適用法律匯出。 之前傳送嗨實體媒體，請建議程式 tooverify 您的媒體和資料可以遵循和法令會識別已出貨的 toohello 資料中心。 這可協助達到 Microsoft 及時 tooensure。

**建立作業時，傳送地址的 hello 是我的儲存體帳戶位置不同的位置。我該怎麼辦？**

某些儲存體帳戶位置就是對應的 tooalternate 傳送位置。 先前使用的傳送位置也可以暫時對應的 tooalternate 位置。 請務必檢查 hello 傳送作業之前傳送您的磁碟機的建立過程中提供的位址。

**傳送我的磁碟機，hello 電信業者會要求 hello 資料中心連絡人地址和電話號碼。我該提供什麼？**

hello 電話號碼和 DC 提供位址做為建立工作的一部分。

**可以使用 hello Azure 匯入/匯出服務 toocopy PST 信箱及 SharePoint 資料 tooO365 嗎？**

請參閱太[匯入 PST 檔案或 SharePoint 資料 tooOffice 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx)。

**我可以使用 hello Azure 匯入/匯出服務 toocopy 我備份離線 toohello Azure 備份服務？**

請參閱太[Azure Backup 中的離線備份工作流程](../backup/backup-azure-backup-import-export.md)。

**Hello 最大數目的 HDD 中一次出是什麼？**

一個 「 出貨 」 可以是任意數目的 Hdd，建議您使用如果 hello 磁碟隸屬 toomultiple 作業太) 有 hello 磁碟標示著 hello 對應作業名稱。 以追蹤數字後置字元為-1，b） 更新 hello 作業-2 等等。
  
**Hello 最大的區塊 Blob 和分頁 Blob 大小支援磁碟匯入/匯出的是什麼？**

最大區塊 Blob 大小大約是 4.768 TB 或 5,000,000 MB。
最大分頁 Blob 大小為 1 TB。

**磁碟匯入/匯出是否支援 AES 256 加密？**

預設的 azure 匯入/匯出服務會使用 AES 128 bitlocker 加密來加密，不過可以手動使用 bitlocker 加密複製資料之前會增加的 tooAES 256。 

如果使用 [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip)，以下是命令範例
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
如果使用[WAImportExport 工具](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip)指定"AlreadyEncrypted 」，並提供 hello driveset CSV 中的 hello 索引鍵。
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>後續步驟

* [設定 hello WAImportExport 工具](storage-import-export-tool-how-to.md)
* [使用 hello AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)
* [Azure 匯入匯出 REST API 範例 (英文)](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

