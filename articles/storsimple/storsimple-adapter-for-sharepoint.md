---
title: "aaaInstall StorSimple Adapter for SharePoint |Microsoft 文件"
description: "描述如何 tooinstall 及設定或移除 hello StorSimple Adapter for SharePoint 伺服器陣列中的 SharePoint。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>安裝和設定 hello StorSimple Adapter for SharePoint
## <a name="overview"></a>概觀
hello StorSimple Adapter for SharePoint 是一種元件，可讓您提供 Microsoft Azure StorSimple 彈性儲存和資料保護 tooSharePoint 伺服器陣列。 您可以使用從 hello SQL Server 內容資料庫 toohello Microsoft Azure StorSimple 混合式雲端儲存體裝置 hello 配接器 toomove 二進位大型物件 (BLOB) 內容。

hello StorSimple Adapter for SharePoint 的函式做為遠端 BLOB 儲存 (RBS) 提供者和使用 hello SQL Server 遠端 BLOB 儲存體功能 toostore 非結構化的 SharePoint 內容 （以 hello Blob 形式），並受到 StorSimple 裝置的檔案伺服器上。

> [!NOTE]
> hello StorSimple Adapter for SharePoint 支援 SharePoint Server 2010 遠端 BLOB 儲存 (RBS)。 它不支援 SharePoint Server 2010 外部 BLOB 儲存體 (EBS)。


* toodownload hello StorSimple Adapter for SharePoint，跳過[StorSimple Adapter for SharePoint] [ 1] hello Microsoft Download Center 中。
* 如需規劃 RBS 和 RBS 限制的詳細資訊，請移至太[決定在 SharePoint 2013 中的 RBS toouse] [ 2]或[規劃 RBS (SharePoint Server 2010)] [3].

hello 本概觀的其餘部分將簡短描述 hello 角色 hello StorSimple Adapter for SharePoint 和 hello SharePoint 容量和效能限制，您應該留意才能安裝及設定 hello 配接器。 檢閱這項資訊之後，請跳過[StorSimple Adapter for SharePoint 安裝](#storsimple-adapter-for-sharepoint-installation)toobegin hello 配接器的設定。

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>StorSimple Adapter for SharePoint 優點
在 SharePoint 網站中，內容會在一個或多個內容資料庫中儲存為非結構化 BLOB 資料。 根據預設，這些資料庫裝載在執行中的 SQL Server 位於 hello SharePoint 伺服器陣列中的電腦。 BLOB 可能快速增大，耗用大量的內部部署儲存體。 基於這個理由，您可能想 toofind 另一個、 較不昂貴的存放裝置解決方案。 SQL Server 提供稱為遠端 Blob 儲存 (RBS) 可讓您將 BLOB 內容儲存在 hello 檔案系統中，hello SQL Server 資料庫外部的技術。 運用 RBS，Blob 可以位於 hello hello 執行 SQL Server 的電腦上的檔案系統或可以儲存在另一部伺服器電腦上的 hello 檔案系統中。

RBS 會要求您使用 RBS 提供者，例如 hello StorSimple Adapter for SharePoint，tooenable RBS 在 SharePoint 中。 hello StorSimple Adapter for SharePoint 搭配 RBS，讓您的 Blob tooa 伺服器 hello Microsoft Azure StorSimple 系統所備份的移動。 Microsoft Azure StorSimple 然後 hello BLOB 資料儲存在本機或 hello 雲端使用量為基礎。 極為活躍的 Blob （通常參照的 tooas 第 1 層或熱門資料） 在本機上。 較不活躍的資料和封存資料位於 hello 雲端中。 內容資料庫上啟用 RBS 之後，在 SharePoint 中建立任何新 BLOB 內容儲存 hello StorSimple 裝置上，而不是在 hello 內容資料庫。

hello Microsoft Azure StorSimple 實作 RBS 提供下列優點 hello:

* 移動 BLOB 內容 tooa 不同的伺服器，您可以減少 hello 可以改善 SQL Server 回應能力的 SQL Server 上的查詢負載。 
* Azure StorSimple 使用重複資料刪除和壓縮 tooreduce 資料大小。
* Azure StorSimple 提供資料保護 hello 表單的本機和雲端快照。 此外，如果您將 hello 資料庫本身放在 hello StorSimple 裝置上時，您可以備份 hello 內容資料庫和 Blob 一起損毀一致的方式。 （移動 hello 內容資料庫 toohello 裝置僅支援 hello StorSimple 8000 系列裝置。 這項功能不支援 hello 5000 或 7000 系列。）
* Azure StorSimple 包含災害復原功能，包括容錯移轉、檔案和磁碟區復原 (包括測試復原) 及快速還原資料。
* 您可以使用資料復原軟體，例如 Kroll Ontrack PowerControls，與 StorSimple 快照集 BLOB 資料 tooperform 的 SharePoint 內容的項目層級復原。 (此資料復原軟體需另外購買)。
* hello SharePoint 管理中心入口網站，可讓您 toomanage 整個 SharePoint 解決方案從中央位置插入 hello StorSimple Adapter for SharePoint。

移動 BLOB 內容 toohello 檔案系統，可以提供其他節省成本和優點。 例如，使用 RBS 可減少昂貴第 1 層儲存體的 hello 需要，因為此舉可縮小 hello 內容資料庫，RBS 可減少 hello hello SharePoint 伺服器陣列中所需的資料庫數目。 不過，其他因素，例如資料庫大小限制和非 RBS 內容的 hello 數量也會影響儲存需求。 如需 hello 成本和使用 RBS 的優點的詳細資訊，請參閱[規劃 RBS (SharePoint Foundation 2010)] [ 4]和[決定在 SharePoint 2013 中的 RBS toouse] [5].

### <a name="capacity-and-performance-limits"></a>容量和效能限制
您可以考慮在您的 SharePoint 方案中使用 RBS 之前，應該注意 hello 測試效能和容量限制的 SharePoint Server 2010 和 SharePoint Server 2013，以及這些限制與 tooacceptable 效能的相關。 如需詳細資訊，請參閱 [SharePoint 2013 的軟體界限及限制](https://technet.microsoft.com/library/cc262787.aspx)。

設定 RBS 之前，請檢閱下列 hello:

* 請確定該 hello 的大小總計 hello 內容 （內容資料庫中的 hello 大小） 再加上的任何相關外部化 Blob 的 hello 大小未超過 SharePoint 所支援的 hello RBS 大小限制。 這項限制為 200 GB。 
  
    **toomeasure 內容資料庫和 BLOB 的大小**
  
  1. Hello 中央系統管理 WFE 上執行此查詢。 啟動 SharePoint 管理命令介面中的 hello，然後輸入下列 Windows PowerShell 命令 tooget hello hello 內容資料庫大小的 hello:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      此步驟中取得 hello hello 內容資料庫大小 hello 磁碟上。
  2. 執行其中一個 hello hello SQL server 方塊上每個內容資料庫，在下列 SQL Management Studio 中的 SQL 查詢，並加入步驟 1 中取得的 hello 結果 toohello 數字。
     
     在 SharePoint 2013 內容資料庫中，輸入：
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     在 SharePoint 2010 內容資料庫中，輸入：
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     此步驟中取得 hello hello 已外部化的 Blob 大小。
* 我們建議您儲存所有的 BLOB 和資料庫內容從本機 hello StorSimple 裝置上。 hello StorSimple 裝置在雙節點叢集的高可用性。 將 hello 內容資料庫和 Blob 放 hello StorSimple 裝置上提供高可用性。
  
    使用傳統 SQL Server 移轉最佳作法 toomove hello 內容資料庫 toohello StorSimple 裝置。 只有在從 hello 資料庫的所有 BLOB 內容之後移動 hello 資料庫已透過 RBS 移的 toohello 檔案共用。 如果您選擇 toomove hello 內容資料庫 toohello StorSimple 裝置時，我們建議您在主要磁碟區的 hello 裝置上設定 hello 內容資料庫儲存體。
* 在 Microsoft Azure StorSimple，如果使用分層磁碟區，所以內容儲存在本機 hello StorSimple 裝置的 tooguarantee 將不會分層式的 tooMicrosoft Azure 雲端儲存體。 因此，建議您搭配 SharePoint RBS 使用 StorSimple 本機固定磁碟區。 這可確保所有 BLOB 內容會保留在本機 hello StorSimple 在裝置上，，而且不是移動的 tooMicrosoft Azure。
* 如果您沒有儲存 hello 內容資料庫 hello StorSimple 裝置上，使用傳統 SQL Server 高可用性最佳作法支援 RBS。 SQL Server 叢集支援 RBS，而 SQL Server 鏡像不支援 RBS。 

> [!WARNING]
> 如果您尚未啟用 RBS，我們不建議移 hello 內容資料庫 toohello StorSimple 裝置。 這是未經過測試的設定。

## <a name="storsimple-adapter-for-sharepoint-installation"></a>StorSimple Adapter for SharePoint 安裝
您可以安裝 hello StorSimple Adapter for SharePoint 之前，您必須設定 hello StorSimple 裝置，並確定 hello SharePoint 伺服器陣列和 SQL Server 具現化符合所有必要條件。 本教學課程將說明組態需求，以及安裝與升級 hello StorSimple Adapter for SharePoint 的程序。

## <a name="configure-prerequisites"></a>設定必要條件
您可以安裝 hello StorSimple Adapter for SharePoint 之前，請確定 hello StorSimple 裝置、 SharePoint 伺服器陣列和 SQL Server 具現化符合下列必要條件 hello。

### <a name="system-requirements"></a>系統需求
hello StorSimple Adapter for SharePoint 搭配 hello 下列硬體和軟體：

* 支援的作業系統 – Windows Server 2008 R2 SP1、Windows Server 2012 或 Windows Server 2012 R2
* 支援的 SharePoint 版本 – SharePoint Server 2010 或 SharePoint Server 2013
* 支援的 SQL Server 版本 – SQL Server 2008 Enterprise Edition、SQL Server 2008 R2 Enterprise Edition 或 SQL Server 2012 Enterprise Edition
* 支援的 StorSimple 裝置 – StorSimple 8000 系列、StorSimple 7000 系列或 StorSimple 5000 系列。

### <a name="storsimple-device-configuration-prerequisites"></a>StorSimple 裝置組態必要條件
hello StorSimple 裝置區塊裝置，因此需要可裝載 hello 資料的檔案伺服器。 我們建議您使用不同的伺服器，而不是現有的伺服器從 hello SharePoint 伺服器陣列。 此檔案伺服器必須是在 hello 相同的區域網路 (LAN) 為 hello SQL Server 電腦裝載 hello 內容資料庫。

> [!TIP]
> * 如果您設定 SharePoint 伺服器陣列的高可用性，您應該也部署 hello 檔案伺服器高可用性。
> * 如果您未在 hello StorSimple 裝置上儲存 hello 內容資料庫，請使用支援 RBS 的傳統高可用性最佳作法。 SQL Server 叢集支援 RBS，而 SQL Server 鏡像不支援 RBS。 


請確定您的 StorSimple 裝置設定正確，且該適當的磁碟區 toosupport SharePoint 部署已設定且可從 SQL Server 電腦存取。 跳過[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)如果您尚未部署和設定您的 StorSimple 裝置。 請注意 hello StorSimple 裝置; hello IP 位址您需要這些期間 StorSimple Adapter for SharePoint 安裝。

此外，請確定用於 BLOB 外部化該 hello 磁碟區 toobe 符合下列需求的 hello:

* hello 磁碟區必須格式化成 64 KB 配置單位大小。
* 您的 web 前端 (WFE) 和應用程式伺服器必須是透過通用命名慣例 (UNC) 路徑無法 tooaccess hello 磁碟區。
* hello SharePoint 伺服器陣列必須是已設定的 toowrite toohello 磁碟區。

> [!NOTE]
> 您安裝並設定 hello 配接器之後，所有 BLOB 外部化都都必須透過 hello StorSimple 裝置 （hello 裝置會呈現 hello 磁碟區 tooSQL 伺服器和管理 hello 儲存層）。 您無法使用任何其他目標進行 BLOB 外部化。


如果您計劃的 hello BLOB toouse StorSimple Snapshot Manager tootake 快照集，而且資料庫資料，是確定 tooinstall StorSimple Snapshot Manager hello 資料庫伺服器上的，好讓它可以使用 SQL 寫入器服務 tooimplement hello hello Windows 磁碟區陰影複製服務 (VSS)。

> [!IMPORTANT]
> StorSimple Snapshot Manager 不支援 hello SharePoint VSS 寫入器，因此無法取得 SharePoint 資料的應用程式一致快照集。 在 SharePoint 案例中，StorSimple Snapshot Manager 只提供當機時保持一致的備份。


## <a name="sharepoint-farm-configuration-prerequisites"></a>SharePoint 伺服器陣列組態必要條件
請確定您的 SharePoint 伺服器陣列已正確設定，如下：

* 請檢查您的 SharePoint 伺服器陣列處於狀況良好的狀態，以及 hello 下列：
* 所有 SharePoint WFE 和 hello 伺服陣列中註冊的應用程式伺服器正在執行，而且可以 ping 從 hello 伺服器，您將安裝 hello StorSimple Adapter for SharePoint。
* hello SharePoint 計時器服務 （SPTimerV3 或 SPTimerV4） 正在每部 WFE 伺服器和應用程式伺服器上執行。
* Hello SharePoint 計時器服務和 hello IIS 應用程式集區的 hello SharePoint 管理中心內的網站執行具有系統管理權限。
* 請確定已停用 Internet Explorer 增強式安全性內容 (IE ESC)。 請遵循這些步驟 toodisable IE ESC:
  
  1. 關閉 Internet Explorer 的所有執行個體。
  2. 啟動 hello 伺服器管理員。
  3. 在 hello 左窗格中，按一下 **本機伺服器**。
  4. Hello 在右窗格中下, 一步太**IE 增強式安全性設定**，按一下 **上**。
  5. 在 [系統管理員] 下，按一下 [關閉]。
  6. 按一下 [確定] 。

## <a name="remote-blob-storage-rbs-prerequisites"></a>遠端 BLOB 儲存 (RBS) 必要條件
請確定您使用支援的 SQL Server 版本。 只要 hello 下列版本都支援，而且要能 toouse RBS:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

可以在外部化 Blob，只有那些 hello StorSimple 裝置的磁碟區呈現 tooSQL 伺服器。 不支援在其他目標上進行 BLOB 外部化。

當您完成所有必要設定步驟時，前往 太[安裝 hello StorSimple Adapter for SharePoint](#install-the-storsimple-adapter-for-sharepoint)。

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>安裝 hello StorSimple Adapter for SharePoint
使用下列步驟 tooinstall hello StorSimple Adapter for SharePoint 的 hello。 如果您重新安裝 hello 軟體，請參閱[升級或重新安裝 hello StorSimple Adapter for SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint)。 hello hello 安裝所需的時間取決於您的 SharePoint 伺服器陣列中的 SharePoint 資料庫的 hello 總數。

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>設定 RBS
您安裝 hello StorSimple Adapter for SharePoint 之後，設定 RBS，hello 遵循程序中所述。

> [!TIP]
> hello StorSimple Adapter for SharePoint 會外掛到 hello SharePoint 管理中心 頁面，允許啟用或停用 hello SharePoint 伺服陣列中每個內容資料庫上的 RBS toobe。 不過，啟用或停用 RBS hello 內容資料庫上會導致 IIS 重設，且根據您伺服陣列組態，可以暫時中斷 hello 可用性的 hello SharePoint web 前端 (WFE)。 （例如 hello 使用前端負載平衡器、 hello 目前的伺服器工作負載等因素可以限制或去除此中斷作業）。tooprotect 使用者發生中斷，我們建議您啟用或停用 RBS，只在計劃性的維護視窗。


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>設定記憶體回收
從 SharePoint 網站刪除的物件，它們不會自動刪除從 hello RBS 存放區磁碟區。 相反地，非同步的背景維護程式刪除被遺棄的 Blob hello 檔案存放區中。 系統管理員可以定期排程這個程序 toorun 或在必要時啟動。

當您啟用 RBS 時，此維護程式 (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) 會自動安裝在所有 SharePoint WFE 伺服器和應用程式伺服器上。 hello 程式會安裝在下列位置的 hello:*開機磁碟機*: \Program Files\Microsoft SQL 遠端 Blob 儲存體 10.50\Maintainer\

如需設定和使用 hello 維護程式的詳細資訊，請參閱[SharePoint Server 2013 中的維護 RBS][8]。

> [!IMPORTANT]
> hello RBS 維護程式會耗用大量資源。 您應該排程它 toorun 只有在的 hello SharePoint 伺服器陣列上的輕量活動期間。


### <a name="delete-orphaned-blobs-immediately"></a>立即刪除被遺棄的 BLOB
若要立即 toodelete 被遺棄的 Blob，您可以使用下列指示的 hello。 請注意，這些指示如何作法是在 SharePoint 2013 環境中以 hello 下列元件的範例：

* hello 內容的資料庫名稱是 WSS_Content。
* hello SQL Server 名稱是 SHRPT13 SQL12\SHRPT13。
* hello web 應用程式名稱為 SharePoint – 80。

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>升級或重新安裝 hello StorSimple Adapter for SharePoint
使用下列程序 tooupgrade SharePoint 伺服器 hello，然後重新安裝 StorSimple Adapter for SharePoint 或 toosimply 升級或重新安裝現有的 SharePoint 伺服器陣列中的 hello 配接器。

> [!IMPORTANT]
> 檢閱下列資訊，然後再嘗試 tooupgrade hello SharePoint 軟體和 （或） 升級或重新安裝 hello StorSimple Adapter for SharePoint:
> 
> * 任何先前移 tooexternal 儲存體透過 RBS hello 重新安裝完成之前，將無法使用的檔案和 hello RBS 功能會啟用一次。 toolimit 使用者影響，執行任何升級或重新安裝已規劃的維護期間。
> * hello hello 升級/重新安裝所需的時間可能會不同，根據 hello SharePoint 資料庫總數 hello SharePoint 伺服器陣列中。
> * Hello 升級/重新安裝完成之後，您需要 tooenable RBS hello 內容資料庫。 如需詳細資訊，請參閱 [設定 RBS](#configure-rbs) 。
> * 如果您有非常大量的資料庫 （大於 200 個） 的 SharePoint 伺服器陣列設定 RBS，hello **SharePoint 管理中心內**頁面可能會逾時。如果發生此情況，請重新整理 hello 頁面。 這不會影響 hello 設定程序。


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>移除 StorSimple Adapter for SharePoint
下列程序的 hello 說明的 toomove hello Blob 回 toohello SQL Server 內容資料庫，然後再解除安裝 hello StorSimple Adapter for SharePoint 的方式。 

> [!IMPORTANT]
> 解除安裝 hello 配接器軟體之前，您尚未 toomove hello Blob 後 toohello 內容資料庫。


### <a name="before-you-begin"></a>開始之前
收集下列資訊，然後才能移 hello 資料回 toohello SQL Server 內容資料庫，並開始 hello 介面卡移除程序的 hello:

* 所有的 hello 資料庫已啟用 RBS 的 hello 名稱
* 設定 BLOB 存放區的 hello 的 hello UNC 路徑。

### <a name="move-hello-blobs-back-toohello-content-databases"></a>移動 hello Blob 後 toohello 內容資料庫
解除安裝 hello StorSimple Adapter for SharePoint 軟體之前，您必須將所有 hello Blob 外部化的後 toohello SQL Server 內容資料庫的移轉。 如果您嘗試使用 toouninstall hello StorSimple Adapter for SharePoint 移動所有 hello Blob 後 toohello 內容資料庫之前，您會看到下列警告訊息的 hello。

![警告訊息](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello Blob 後 toohello 內容資料庫
1. 下載每個外部化的 hello 物件。
2. 開啟 hello **SharePoint 管理中心內**頁面，然後瀏覽過**系統設定**。
3. 在 [Azure StorSimple] 下方，按一下 [設定 StorSimple Adapter]。
4. 在 hello**設定 StorSimple 介面卡**頁面上，按一下 hello**停用**每個您想要從外部 BLOB 儲存體 tooremove hello 內容資料庫下方的按鈕。 
5. 從 SharePoint 刪除 hello 物件並上傳一次。

或者，您可以使用 hello Microsoft` RBS Migrate()` SharePoint 隨附的 PowerShell cmdlet。 如需詳細資訊，請參閱 [將內容移入或移出 RBS](https://technet.microsoft.com/library/ff628255.aspx)。

移動 hello Blob 後 toohello 內容資料庫之後，請繼續 toohello 下一個步驟：[解除安裝 hello 配接器](#uninstall-the-adapter)。

### <a name="uninstall-hello-adapter"></a>解除安裝 hello 配接器
移動 hello Blob 後 toohello SQL Server 內容資料庫之後，使用下列選項 toouninstall hello StorSimple Adapter for SharePoint 的 hello 的其中一個。

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>toouse hello 安裝程式 toouninstall hello 配接器
1. 以系統管理員權限 toolog toohello web 前端 (WFE) 伺服器上使用的帳戶。
2. 按兩下 hello StorSimple Adapter for SharePoint 安裝程式。 hello 安裝精靈會啟動。
   
    ![安裝精靈](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. 按一下 [下一步] 。 hello 遵循頁面隨即出現。
   
    ![安裝精靈移除頁面](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. 按一下**移除**tooselect hello 移除程序。 hello 遵循頁面隨即出現。
   
    ![安裝精靈確認頁面](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. 按一下**移除**tooconfirm hello 移除。 hello 下列進度 頁面隨即出現。
   
    ![安裝精靈進度頁面](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Hello 移除完成時，會出現 hello 完成頁面。 按一下**完成**tooclose hello 安裝精靈。

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello 控制台 toouninstall hello 配接器
1. 開啟 hello 控制台，然後按一下**程式和功能**。
2. 選取 **StorSimple Adapter for SharePoint**，然後按一下解除安裝。

## <a name="next-steps"></a>後續步驟
[深入了解 StorSimple](storsimple-overview.md)。

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
