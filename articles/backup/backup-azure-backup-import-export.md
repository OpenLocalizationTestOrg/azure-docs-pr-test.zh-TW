---
title: "備份-離線備份，或初始植入使用 aaaAzure hello Azure 匯入/匯出服務 |Microsoft 文件"
description: "了解如何 Azure Backup 可讓您使用 hello Azure 匯入/匯出服務的 hello 網路 toosend 資料。 本文說明 hello 離線植入 hello 初始備份資料的使用 hello Azure 匯入匯出服務。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>在 Azure 備份中離線備份工作流程
Azure 備份有數個內建的效率 hello 期間初始完整備份資料 tooAzure 節省網路和儲存體成本。 初始完整備份通常會傳輸大量資料，而且需要更多的網路頻寬比較時，傳輸只 hello 差異/增量 toosubsequent 備份。 Azure 備份的壓縮 hello 初始備份。 Hello 離線植入程序，透過 Azure 備份可以使用磁碟 tooupload hello 壓縮初始備份資料離線 tooAzure。  

hello 離線植入的 Azure 備份的程序緊密整合以 hello [Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)，可讓您 tootransfer 資料 tooAzure 使用磁碟。 如果您有 tb (TBs) 需要 toobe 透過高延遲及低頻寬網路傳送的初始備份資料，您可以使用一或多個硬碟 tooan Azure 資料中心上的 hello 離線植入工作流程 tooship hello 初始備份複本。 本文章會提供完成此工作流程的 hello 步驟的概觀。

## <a name="overview"></a>概觀
使用 hello 離線植入功能的 Azure 備份和 Azure 匯入/匯出，它是簡單 tooupload hello 資料離線 tooAzure 使用磁碟。 而不是透過 hello 網路傳送 hello 初始完整複本，hello 備份資料會寫入 tooa*預備位置*。 Hello 複本 toohello 暫存位置使用 hello Azure 匯入/匯出工具來完成之後，此資料會寫入 tooone 或更多的 SATA 磁碟機，請根據 hello 資料量而定。 這些磁碟機是最終已出貨的 toohello 最接近的 Azure 資料中心。

hello [2016 年 8 月更新的 Azure 備份 （和更新版本）](http://go.microsoft.com/fwlink/?LinkID=229525)包含 hello *Azure 磁碟準備工具*，名為 AzureOfflineBackupDiskPrep 的：

* 可協助您準備 Azure 匯入您的磁碟機使用 hello Azure 匯入/匯出工具。
* 會自動建立 hello Azure 匯入/匯出服務的 Azure 匯入工作上 hello [Azure 傳統入口網站](https://manage.windowsazure.com)為相對於 toocreating hello 相同手動與舊版本的 Azure 備份。

Hello 備份資料 tooAzure hello 上的傳完成之後，Azure Backup 複製 hello 備份資料 toohello 備份保存庫，並排定 hello 增量備份。

> [!NOTE]
> toouse hello Azure 磁碟準備工具，請確定您已安裝 hello 2016 年 8 月更新的 Azure 備份 （或更新版本），並執行 hello 工作流程與它的所有 hello 步驟。 如果您使用較舊版本的 Azure 備份，您可以利用 hello Azure 匯入/匯出工具所述，本文章稍後的章節中準備 hello SATA 磁碟機。
>
>

## <a name="prerequisites"></a>必要條件
* [熟悉 hello Azure 匯入/匯出工作流程](../storage/common/storage-import-export-service.md)。
* 之前起始 hello 工作流程時，請務必 hello 下列：
  * 已建立 Azure 備份保存庫。
  * 已下載保存庫認證。
  * hello Azure 備份代理程式已安裝 Windows Server/Windows 用戶端或 System Center Data Protection Manager 伺服器上與 hello 電腦向 hello Azure 備份保存庫。
* [下載 Azure 發行檔案設定 hello](https://manage.windowsazure.com/publishsettings) hello 從中您計劃 tooback 組成資料的電腦上。
* 準備暫存位置，可能是網路共用或 hello 電腦上的其他磁碟機。 預備位置的 hello 是暫時的儲存體，並暫時在此工作流程期間使用。 請確定該 hello 預備位置有足夠的磁碟空間 toohold 初始複本。 例如，如果您嘗試 tooback 500 GB 的檔案伺服器，請確定該 hello 臨時區域至少 500 GB。 (較少量用到期 toocompression。)
* 確定您使用的是支援的磁碟機。 只有 2.5 英吋 SSD 或 2.5 或 3.5 吋 SATA II/III 內部硬碟機支援 hello 匯入/匯出服務搭配使用。 您可以使用向上 too10 TB 的硬碟機。 檢查 hello [Azure 匯入/匯出服務文件](../storage/common/storage-import-export-service.md#hard-disk-drives)hello hello 服務支援的磁碟機的最新的集。
* 啟用 BitLocker 連接 hello 電腦 toowhich hello SATA 磁碟機的寫入器。
* [下載 hello Azure 匯入/匯出工具](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409)toohello 電腦 toowhich hello SATA 磁碟機寫入器已連線。 如果您已下載並安裝 hello 2016 年 8 月更新的 Azure 備份 （或更新版本），就不需要此步驟。

## <a name="workflow"></a>工作流程
本節中的 hello 資訊可協助您完成 hello 離線備份工作流程，以便您的資料可以傳遞 tooan Azure 資料中心，並上傳 tooAzure 儲存體。 如果您有關於 hello 匯入服務或任何方面的 hello 程序的問題，請參閱 hello[匯入服務概觀](../storage/common/storage-import-export-service.md)先前參考的文件。

### <a name="initiate-offline-backup"></a>起始離線備份
1. 當您將備份排程時，您會看到下列畫面 （Windows Server、 Windows 用戶端或 System Center Data Protection Manager） 中的 hello。

    ![匯入畫面](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    以下是在 System Center Data Protection Manager hello 對應螢幕： <br/>
    ![DPM 匯入畫面](./media/backup-azure-backup-import-export/dpmoffline.png)

    hello 輸入 hello 描述如下所示：

    * **預備位置**: hello 暫存位置 toowhich hello 初始備份複本會寫入。 這可能是在網路共用或本機電腦上。 如果 hello 複製電腦與來源電腦不同，我們建議您指定預備位置的 hello hello 完整網路路徑。
    * **Azure 匯入工作名稱**: hello 藉由 Azure 匯入服務和 Azure 備份追蹤 hello 傳輸傳送的資料磁碟 tooAzure 唯一的名稱。
    * **Azure 發佈設定**：包含訂用帳戶設定檔相關資訊的 XML 檔案。 檔案中也包含與訂用帳戶相關聯的安全認證。 您可以[hello 檔案下載](https://manage.windowsazure.com/publishsettings)。 提供 hello 本機路徑 toohello 發行設定檔。
    * **Azure 訂用帳戶 ID**: hello hello 您計劃 tooinitiate hello Azure 匯入作業的訂用帳戶的 Azure 訂用帳戶 ID。 如果您有多個 Azure 訂用帳戶，使用您想與 hello 匯入工作 tooassociate hello 訂閱 hello 識別碼。
    * **Azure 儲存體帳戶**: hello hello 傳統類型儲存體帳戶提供與 hello Azure 匯入工作相關聯的 Azure 訂用帳戶。
    * **Azure 儲存體容器**: hello hello 這項作業的資料匯入的 Azure 儲存體帳戶中的 hello 目的地儲存體 blob 名稱。

    > [!NOTE]
    > 如果您已註冊伺服器 tooan hello 從 Azure 復原服務保存庫[Azure 入口網站](https://portal.azure.com)用於您的備份或不在雲端方案提供者 (CSP) 的訂用帳戶，您仍然可以建立傳統類型的儲存體帳戶從 helloAzure 入口網站並將它用於 hello 離線備份工作流程。
    >
    >

     儲存這項資訊，因為您需要 tooenter 再次在下列步驟。 只有 hello*預備位置*時需要使用 hello Azure 磁碟準備工具 tooprepare hello 磁碟。    
2. 完成 hello 工作流程，然後選取 **立即備份**hello Azure Backup 管理主控台 tooinitiate hello 離線備份複本中。 hello 初始備份寫入 toohello 臨時區域，做為此步驟的一部分。

    ![立即備份](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello 對應工作流程中 System Center Data Protection Manager，以滑鼠右鍵按一下 hello**保護群組**，然後選擇 hello**建立復原點**選項。 然後您可以選擇 hello**線上保護**選項。

    ![DPM 立即備份](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Hello 作業完成之後，hello 預備位置將是用於磁碟準備就緒 toobe。

    ![備份進度](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>準備 SATA 磁碟機，並使用 hello Azure 磁碟準備工具建立 Azure 匯入工作
hello Azure 磁碟準備工具是可用的 hello 復原服務代理程式的安裝目錄中 (2016 年 8 月更新和更新版本) hello 下列路徑中。

   *\Microsoft* *Azure* *Recovery* *Services* *Agent\Utils\*

1. 前往 toohello 目錄，並複製 hello **AzureOfflineBackupDiskPrep**備妥的磁碟機 toobe 掛接於哪一個 hello 目錄 tooa 複製電腦。 請確定 hello 與考慮 toohello 複製電腦的下列：

    * hello 複製電腦可存取暫存位置 hello 離線植入的工作流程使用相同網路中 hello 提供路徑的 hello hello**起始離線備份**工作流程。
    * Hello 電腦上啟用 BitLocker。
    * hello 電腦可以存取 hello Azure 入口網站。

    如有必要，hello 複製電腦可以 hello 與 hello 來源電腦相同。
2. 以 hello Azure 磁碟準備工具目錄為 hello 目前目錄中，開啟提升權限的命令提示字元，hello 複製電腦上，然後執行下列命令的 hello:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | 參數 | 說明 |
    | --- | --- |
    | s:&lt;*預備位置路徑*&gt; |已使用 tooprovide hello 路徑 toohello 預備 hello 中輸入的位置的必要輸入**起始離線備份**工作流程。 |
    | p:&lt;*路徑 tooPublishSettingsFile*&gt; |選擇性的輸入使用 tooprovide hello 路徑 toohello **Azure 發佈設定**hello 中輸入的檔案**起始離線備份**工作流程。 |

    > [!NOTE]
    > hello&lt;路徑 tooPublishSettingFile&gt;值時，強制 hello 複製電腦與來源電腦是不相同。
    >
    >

    當您執行 hello 命令時，hello 工具會要求 hello hello Azure 匯入作業的對應，需要準備 toobe toohello 磁碟機的選取範圍。 如果只以提供暫存位置的 hello 單一匯入作業相關聯，您會看到像 hello 的螢幕。

    ![Azure 磁碟準備工具的輸入](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. 輸入 hello 磁碟機代號而不需 hello 尾端的 hello 掛接的磁碟，傳輸 tooAzure 需 tooprepare 冒號。 提供 hello 格式化 hello 磁碟機，當系統提示您的確認。

    hello 工具就會開始 tooprepare hello 磁碟 hello 備份資料。 您可能需要其他 tooattach 磁碟 hello 工具提示 hello 提供磁碟沒有足夠的空間供 hello 備份資料時。 <br/>

    在成功執行 hello 工具 hello 最後，您所提供的一或多個磁碟備妥要建立傳送 tooAzure。 此外，匯入工作 hello 名稱與您在提供 hello**起始離線備份**hello Azure 傳統入口網站上建立工作流程。 最後，hello 工具會顯示 hello 送貨地址 toohello 其中 hello 磁碟都必須隨附 toobe 的 Azure 資料中心，及 hello 連結 toolocate hello hello Azure 傳統入口網站上的匯入作業。

    ![Azure 磁碟準備完成](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. 出貨 hello 磁碟 toohello 位址提供該 hello 工具，並保留 hello 追蹤號碼，供日後參考。<br/>

5. 當您移 toohello 連結顯示該 hello 工具，您會看到您在 hello 中指定的 hello Azure 儲存體帳戶**起始離線備份**工作流程。 這裡您會看到新建立的 hello 匯入工作上 hello**匯入/匯出**hello 儲存體帳戶 索引標籤。

    ![建立的匯入作業](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. 按一下**出貨資訊**底部 hello hello 頁面 tooupdate 連絡人詳細資料中 hello 遵循畫面所示。 Microsoft 會使用此資訊 tooship，hello 匯入作業之後您磁碟回復 tooyou 完成。

    ![連絡資訊](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. 輸入 hello 傳送 hello 下一個畫面上的 詳細資料。 提供 hello**遞送承運業者**和**追蹤號碼**對應 toohello 磁碟出貨 toohello Azure 資料中心的詳細資料。

    ![寄送資訊](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>完整的 hello 工作流程
Hello 匯入作業完成之後，初始備份資料是儲存體帳戶中所提供。 hello 復原服務代理程式，然後複製 hello 內容的 hello 資料從這個帳戶 toohello 備份保存庫或復原服務保存庫，適用者為準。 Hello 下一個排程的備份時間，hello Azure 備份代理程式會透過 hello 初始備份複本，執行 hello 增量備份。

> [!NOTE]
> hello 下列各節套用 toousers 的較早版本的 Azure 備份不具備存取 toohello Azure 磁碟準備工具。
>
>

### <a name="prepare-a-sata-drive"></a>準備 SATA 磁碟機
1. 下載 hello [Microsoft Azure 匯入/匯出工具](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409)toohello 複製電腦。 確定可從您計劃 toorun hello 下的一組命令 hello 電腦存取該 hello 預備位置。 如有必要，hello 複製電腦可以 hello 與 hello 來源電腦相同。

2. 解壓縮 hello WAImportExport.zip 檔。 執行 hello WAImportExport 工具格式化 hello SATA 磁碟機、 寫入 hello 備份資料 toohello SATA 磁碟機，並進行加密。 執行下列命令的 hello 之前，請確定 hello 電腦上已啟用 BitLocker。 <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > 如果您已安裝 hello 2016 年 8 月更新的 Azure 備份 （或更新版本），請確定該 hello 預備您輸入的位置是 hello 與另一個在 hello hello 相同**立即備份**畫面上，並包含 AIB 和基底 Blob 的檔案。
    >
    >

| 參數 | 說明 |
| --- | --- |
| /j:<*JournalFile*> |hello 路徑 toohello 日誌檔。 每個磁碟機必須只有一個日誌檔案。 hello 日誌檔不得 hello 目標磁碟機上。 hello 日誌檔的副檔名是.jrn，並建立做為執行此命令的一部分。 |
| /id:<*SessionId*> |hello 工作階段 ID 識別一個複製工作階段。 它是使用的 tooensure 中斷的複製工作階段的精確的復原。 會在複製工作階段中複製的檔案儲存在名為 hello hello 目標磁碟機上的工作階段識別碼之後的目錄。 |
| /sk:<*StorageAccountKey*> |匯入 hello hello 儲存體帳戶 toowhich hello 資料的帳戶金鑰。 hello 與它相同備份原則/保護群組建立過程中輸入 toobe hello 主要需求。 |
| /BlobType |hello 的 blob 類型。 已指定 **PageBlob** 時，此工作流程才會成功。 這不是 hello 預設選項，而且應該在這個命令中所述。 |
| /t:<*TargetDriveLetter*> |hello 沒有 hello 尾端 hello 目前複製工作階段的冒號 hello 目標硬碟機的磁碟機代號。 |
| /format |hello 選項 tooformat hello 磁碟機。 指定此參數，當 hello 磁碟機需要 toobe 格式化;否則請省略它。 Hello 工具格式化 hello 磁碟機之前，它會提示確認 hello 主控台。 toosuppress hello 確認，請指定 hello /silentmode 參數。 |
| /encrypt |hello 選項 tooencrypt hello 磁碟機。 Hello 磁碟機未加密的 BitLocker 和需求 toobe hello 工具來加密時，請指定此參數。 Hello 磁碟機已使用 BitLocker 加密，如果省略這個參數，指定 hello /bk 參數，並提供 hello 現有 BitLocker 金鑰。 如果您指定 hello /format 參數時，您也必須指定 hello/加密參數。 |
| /srcdir:<*SourceDirectory*> |包含檔案 toobe hello 來源目錄複製 toohello 目標磁碟機。 確認該 hello 指定的目錄名稱都有完整而非相對路徑。 |
| /dstdir:<*DestinationBlobVirtualDirectory*> |hello 路徑 toohello 目的地虛擬目錄在 Azure 儲存體帳戶。 當您指定 hello 目的地虛擬目錄或 blob 是確定 toouse 有效的容器名稱。 請記住容器名稱必須是小寫。  此容器的名稱應該是您輸入在建立備份原則/保護群組的其中一個 hello。 |

> [!NOTE]
> 日誌檔擷取 hello 整個 hello 工作流程資訊的 hello WAImportExport 資料夾中建立。 Hello Azure 入口網站中建立匯入工作時，您會需要此檔案。
>
>

  ![PowerShell 輸出](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立匯入工作
1. 移 tooyour 儲存體帳戶中 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **匯入/匯出**，然後**建立匯入工作**hello 工作窗格中。

    ![Hello Azure 入口網站中的匯入/匯出 索引標籤](./media/backup-azure-backup-import-export/azureportal.png)

2. 在 hello 精靈的步驟 1，表示您已經備妥您的磁碟機，而且您擁有 hello 可用的磁碟機日誌檔案。

3. 在步驟 2 中的 hello 精靈，提供 hello 人員負責這個匯入工作的連絡資訊。

4. 在步驟 3 中上, 傳您取得 hello 前一節中的 hello 磁碟機日誌檔案。

5. 在步驟 4 中，輸入您在建立備份原則/保護群組時輸入的 hello 匯入工作的描述性名稱。 您輸入的 hello 名稱可包含小寫字母、 數字、 連字號和底線，必須以字母開頭，而且不能包含空格。 您可以選擇正在進行中之後，便會完成您的作業是使用的 tootrack hello 名稱。

6. 接下來，從 hello 清單中選取的資料中心區域。 hello 資料中心地區指出 hello 資料中心和地址 toowhich 您撽拶嫋您的封裝。

    ![選取資料中心區域](./media/backup-azure-backup-import-export/dc.png)

7. 在步驟 5 中，從 hello] 清單中，選取 [貨運公司，並輸入您的承運業者帳戶號碼。 Microsoft 會使用此帳戶 tooship 您的磁碟機備份 tooyou 匯入工作完成之後。

8. 出貨 hello 磁碟，然後輸入 hello 追蹤 hello 出貨編號 tootrack hello 狀態。 Hello 資料中心內到達 hello 磁碟之後，就複製 toohello 儲存體帳戶，而且 hello 狀態會更新。

    ![已完成的狀態](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>完整的 hello 工作流程
Hello 初始備份資料提供儲存體帳戶中 hello Microsoft Azure 復原服務代理程式從這個帳戶 toohello 備份保存庫或復原服務保存庫複製 hello 資料的 hello 內容之後，適用者為準。 Hello 下一個排程中備份的時間，hello Azure 備份代理程式會透過 hello 初始備份複本，執行 hello 增量備份。

## <a name="next-steps"></a>後續步驟
* Hello Azure 匯入/匯出工作流程上的任何問題，請參閱太[使用 hello Microsoft Azure 匯入/匯出服務 tootransfer 資料 tooBlob 儲存](../storage/common/storage-import-export-service.md)。
* Toohello 離線備份 區段的 hello Azure Backup，請參閱[常見問題集](backup-azure-backup-faq.md)hello 工作流程相關的任何問題。
