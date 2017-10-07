---
title: "aaaWhat 是 StorSimple Snapshot Manager？ | Microsoft Docs"
description: "描述 hello StorSimple Snapshot Manager、 其結構，以及其功能。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>簡介 tooStorSimple Snapshot Manager

## <a name="overview"></a>概觀
StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，可簡化資料保護和備份管理 Microsoft Azure StorSimple 環境中。 使用 StorSimple Snapshot Manager 中，您可以管理在 hello 資料中心和 hello 雲端的 Microsoft Azure StorSimple 資料做為單一整合式儲存體解決方案，因而簡化備份程序，並降低成本。

本概觀介紹 hello StorSimple Snapshot Manager、 描述其功能，並說明其角色在 Microsoft Azure StorSimple。 

如需概觀 hello 整個 Microsoft Azure StorSimple 系統，包括 hello StorSimple 裝置，StorSimple Manager 服務、 StorSimple Snapshot Manager 和 StorSimple Adapter for SharePoint，請參閱[StorSimple 8000 系列： 混合式雲端儲存體解決方案](storsimple-overview.md)。 

> [!NOTE]
> * 您無法使用 StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple 虛擬陣列 （也稱為 StorSimple 內部部署虛擬裝置）。
> * 如果您計劃您的 StorSimple 裝置 tooinstall StorSimple Update 2，可確定 toodownload hello 最新版的 StorSimple Snapshot Manager，並將它安裝**安裝 StorSimple Update 2 之前**。 hello 最新版本的 StorSimple Snapshot Manager 的回溯相容性，以及適用於所有的 Microsoft Azure StorSimple 的發行版本。 如果您使用 hello 舊版的 StorSimple Snapshot Manager，您必須 tooupdate it （您不需要 toouninstall hello 先前版本再安裝新版本的 hello）。
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>StorSimple Snapshot Manager 用途和架構
StorSimple Snapshot Manager 提供中央管理主控台，您可以使用 toocreate 一致、 時間點備份複本的本機和雲端資料。 例如，您可以使用 hello 主控台：

* 設定、備份及刪除磁碟區。
* 設定磁碟區群組 tooensure 該備份資料是應用程式一致。
* 管理備份原則，以便在預先決定的排程上備份資料。
* 建立本機和雲端快照，可用於災害復原和儲存在 hello 雲端中。

StorSimple Snapshot Manager hello 提取 hello 註冊 hello hello 主機上的 VSS 提供者的應用程式的清單。 然後，toocreate 應用程式一致備份，它會檢查 hello 磁碟區應用程式所使用，並且建議磁碟區群組 tooconfigure。 StorSimple Snapshot Manager 會使用這些磁碟區群組 toogenerate 備份應用程式一致的。 （應用程式一致性是指所有相關的檔案和資料庫同步處理，且代表 hello hello 應用程式在特定時間點的時間，則為 true 的狀態。） 

StorSimple Snapshot Manager 備份採用增量快照，hello 所做的變更擷取自 hello 上次備份之後 hello 形式。 因此，備份所需的儲存體更少並可以快速建立和還原。 StorSimple Snapshot Manager 會使用 hello Windows 磁碟區陰影複製服務 (VSS) tooensure 快照集擷取應用程式一致的資料。 （如需詳細資訊，請移 toohello 整合與 Windows 磁碟區陰影複製服務 > 一節）。使用 StorSimple Snapshot Manager 時，您可以建立備份排程或視需要進行立即備份。 如果您需要 toorestore 資料從備份、 的 StorSimple Snapshot Manager 可讓您選取的本機目錄或雲端快照。 Azure StorSimple 只 hello 將資料還原所需的需求，以防止資料可用性延遲，在還原作業期間。）

![StorSimple Snapshot Manager 架構](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**StorSimple Snapshot Manager 架構** 

## <a name="support-for-multiple-volume-types"></a>支援多個磁碟區類型
您可以使用 hello StorSimple Snapshot Manager tooconfigure 和備份下列類型的磁碟區的 hello: 

* **基本磁碟區** – 基本磁碟區是基本磁碟上的單一磁碟分割。 
* **簡單磁碟區** – 簡單磁碟區是動態磁碟區，其中包含來自單一動態磁碟的磁碟空間。 簡單磁碟區包含磁碟上的單一區域，或互相連結的多個區域 hello 同一個磁碟。 (簡單磁碟區只能在動態磁碟上建立。)簡單磁碟區不具有容錯功能。
* **動態磁碟區** – 動態磁碟區是動態磁碟上建立的磁碟區。 動態磁碟會使用磁碟區所包含的相關資訊的資料庫 tootrack 電腦中的動態磁碟上。 
* **含鏡像的動態磁碟區**– 含鏡像的動態磁碟區 hello RAID 1 架構為基礎。 使用 RAID 1 時，相同的資料會寫入兩個或多個磁碟，因而產生鏡像集。 可以處理讀取的要求的任何磁碟都包含 hello 要求資料。
* **叢集共用磁碟區**– 使用叢集共用磁碟區 (Csv)，在容錯移轉叢集中的多個節點可以同時讀取或寫入 toohello 同一個磁碟。 從一個節點 tooanother 節點容錯移轉可能會發生快，而不需要變更磁碟機擁有權或掛接、 卸載和移除磁碟區。 

> [!IMPORTANT]
> 請勿混用 Csv 和非 Csv hello 中相同的快照集。 不支援在快照中混用 CSV 和非 CSV。 
> 
> 

您可以使用 StorSimple Snapshot Manager toorestore 整個磁碟區群組或複製個別磁碟區和復原個別檔案。

* [磁碟區和磁碟區群組](#volumes-and-volume-groups) 
* [備份類型和備份原則](#backup-types-and-backup-policies) 

如需 StorSimple Snapshot Manager 功能的詳細資訊和如何 toouse 它們，請參閱[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。

## <a name="volumes-and-volume-groups"></a>磁碟區和磁碟區群組
使用 StorSimple Snapshot Manager 時，您可以建立磁碟區，然後將其設定為磁碟區群組。 

StorSimple Snapshot Manager 會使用磁碟區群組 toocreate 備份應用程式一致的。 應用程式一致性是指所有相關的檔案和資料庫同步處理，且呈現在特定時間點的應用程式，在時間 hello 真實狀態。 磁碟區群組 (也稱為是*一致性群組*) 形成 hello 基礎備份或還原作業。

磁碟區群組不是 hello 與磁碟區容器相同的。 磁碟區容器包含一個或多個共用雲端儲存體帳戶和其他屬性 (例如加密和頻寬耗用量) 的磁碟區。 單一磁碟區容器可包含 too256 精簡佈建 StorSimple 磁碟區。 如需磁碟區容器的詳細資訊，請移至太[管理磁碟區容器](storsimple-manage-volume-containers.md)。 磁碟區群組是您設定 toofacilitate 備份作業的磁碟區的集合。 如果您選取兩個磁碟區，隸屬 toodifferent 磁碟區容器、 將它們放在單一磁碟區群組，然後建立該磁碟區群組的備份原則，每個備份磁碟區將會在 hello 適當的磁碟區容器中，使用 hello 適當的儲存體帳戶。

> [!NOTE]
> 磁碟區群組中的所有磁碟區必須來自單一雲端服務提供者。
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>與 Windows 磁碟區陰影複製服務整合
StorSimple Snapshot Manager 會使用 hello Windows 磁碟區陰影複製服務 (VSS) toocapture 應用程式一致的資料。 VSS 藉由與 VSS 感知應用程式 toocoordinate hello 建立增量快照通訊促進應用程式一致性。 VSS 可確保 hello 應用程式暫時作用中狀態，或停止時，取得快照時。 

VSS hello StorSimple Snapshot Manager 實作適用於 SQL Server 和一般 NTFS 磁碟區。 hello 程序如下所示： 

1. 要求者，通常是資料管理和保護解決方案 (例如 StorSimple Snapshot Manager) 或備份應用程式，會叫用 VSS，並要求它 toogather hello 目標應用程式中的 hello 寫入器軟體的資訊。
2. VSS 連絡人 hello 寫入器元件 tooretrieve hello 資料的描述。 hello 寫入器會傳回備份 hello 資料 toobe hello 描述。 
3. VSS 指示 hello 寫入器 tooprepare hello 應用程式進行備份。 hello 寫入器更新交易記錄檔，並依此類推，藉由完成開啟的交易，準備進行備份的 hello 資料，然後通知 vss。
4. VSS 指示 hello 寫入器 tootemporarily 停止 hello 應用程式的資料會儲存並確定沒有資料會寫入 toohello 磁碟區 hello 陰影複製建立時。 這個步驟可確保資料一致性，而且所需時間不超過 60 秒。
5. VSS 指示 hello 提供者 toocreate hello 陰影複製。 提供者，它可以是軟體或硬體為基礎，來管理目前正在執行，並視需要建立它們的陰影複本 hello 磁碟區。 hello 提供者建立 hello 陰影複製，並在完成時通知 VSS。
6. VSS 連絡人 hello 寫入器 toonotify hello 應用程式表示 I/O 可繼續以及 tooconfirm I/O 已順利暫停期間陰影複製建立。 
7. VSS 如果 hello 複製成功，傳回 hello 複製的位置 toohello 要求者。 
8. 如果資料已寫入 hello 陰影複製建立時，hello 備份會不一致。 VSS 會刪除 hello 陰影複製，並通知 hello 要求者。 hello 要求者可以自動重複備份程序 hello 或通知 hello 管理員 tooretry 它在稍後。

下列圖例 hello，請參閱。

![VSS 程序](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Windows 磁碟區陰影複製服務程序** 

## <a name="backup-types-and-backup-policies"></a>備份類型和備份原則
使用 StorSimple Snapshot Manager 中，您可以備份資料，並將它儲存在本機和 hello 雲端中。 您可以立即使用 StorSimple Snapshot Manager tooback 資料或您可以使用備份原則 toocreate 排程自動進行備份。 備份原則也可讓您 toospecify 將保留快照集數目。 

### <a name="backup-types"></a>備份類型
您可以使用下列類型的備份 StorSimple Snapshot Manager toocreate hello:

* **本機快照**– 本機快照是儲存在 hello StorSimple 裝置的磁碟區資料的時間點副本。 一般而言，可以快速建立和還原這種類型的備份。 您可以如同使用本機備份複本一般使用本機快照。
* **雲端快照**– 雲端快照是儲存在 hello 雲端中的磁碟區資料的時間點複本。 雲端快照相當 tooa 快照式複寫不同的異地儲存系統上。 雲端快照在災害復原案例中特別有用。

### <a name="on-demand-and-scheduled-backups"></a>依需求和排程的備份
使用 StorSimple Snapshot Manager 中，您可以起始，立即建立單次備份 toobe，或者您可以使用備份原則 tooschedule 週期性備份作業。

備份原則是一組自動化規則，您可以使用 tooschedule 定期備份。 備份原則可讓您 toodefine hello 頻率和參數，以取得特定磁碟區群組的快照。 您可以使用原則 toospecify 開始和到期日期、 時間、 頻率和保留需求本機和雲端快照。 在定義原則之後會立即套用。 

您可以使用 StorSimple Snapshot Manager tooconfigure 或重新設定備份原則需要的時候。 

您設定 hello 下列每個您所建立的備份原則的資訊：

* **名稱**– 選取備份原則的 hello 的 hello 的唯一名稱。
* **型別**– hello 的備份原則，則為本機快照或雲端快照的類型。
* **磁碟區群組**– hello 磁碟區群組 toowhich hello 選取備份原則指派。
* **保留**– hello tooretain 備份複本數目。 如果您核取 hello**所有** 方塊中，所有的備份複本會保留 hello 的每個磁碟區的備份複本數目上限為止，在哪個點 hello 原則將會失敗並產生錯誤訊息。 或者，您可以指定數目的備份 tooretain （介於 1 到 64）。
* **日期**– hello hello 備份原則建立時的日期。

設定備份原則的相關資訊，請太[使用 StorSimple Snapshot Manager toocreate 與管理備份原則](storsimple-snapshot-manager-manage-backup-policies.md)。

### <a name="backup-job-monitoring-and-management"></a>監視和管理備份工作
您可以使用 hello StorSimple Snapshot Manager toomonitor 和管理即將進行、 排程，以及完成備份工作。 此外，StorSimple Snapshot Manager 提供 too64 完成備份的目錄。 您可以使用 hello 目錄 toofind 並還原磁碟區或個別檔案。 

如需監視備份作業的相關資訊，請移至太[使用 StorSimple Snapshot Manager tooview 及管理備份工作](storsimple-snapshot-manager-manage-backup-jobs.md)。

## <a name="next-steps"></a>後續步驟
* 深入了解[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 下載 [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220)。

