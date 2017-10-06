---
title: "DPM 工作負載 tooAzure 傳統入口網站註冊 aaaBack |Microsoft 文件"
description: "DPM 伺服器使用 hello Azure 備份服務簡介 toobacking"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, Data Protection Manager, DPM 備份"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>準備註冊與 DPM 工作負載 tooAzure tooback
> [!div class="op_single_selector"]
> * [Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 備份伺服器 (傳統)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (傳統)](backup-azure-dpm-introduction-classic.md)
>
>

本文章提供簡介 toousing Microsoft Azure 備份 tooprotect System Center Data Protection Manager (DPM) 伺服器和工作負載。 在閱讀本文後，您將了解：

* Azure DPM 伺服器備份的運作方式
* hello 必要條件 tooachieve smooth 備份體驗
* hello 發生一般錯誤以及如何與它們 toodeal
* 支援的案例

System Center DPM 會備份檔案和應用程式資料。 可以儲存在磁帶上，在磁碟上，或備份至 Microsoft Azure 備份 tooAzure tooDPM 所備份的資料。 DPM 與 Azure 備份的互動方式如下：

* **DPM 部署為實體伺服器或內部部署虛擬機器**— 如果 DPM 部署為實體伺服器或內部部署 HYPER-V 虛擬機器，您可以將組成資料 tooan Azure 備份保存庫此外 toodisk 並磁帶備份。
* **DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。 如果 DPM 部署為 Azure 虛擬機器您可以備份資料 tooAzure 磁碟附加 toohello DPM Azure 虛擬機器，或您可以將 hello 資料儲存區卸載備份 tooan Azure 備份保存庫。

## <a name="why-backup-your-dpm-servers"></a>為何要備份 DPM 伺服器？
使用 Azure 備份來備份 DPM 伺服器 hello 商業優勢包括：

* 在內部部署 DPM 部署，您可以使用 Azure 備份做為替代 toolong 詞彙部署 tootape。
* 若是在 Azure 中的 DPM 部署，Azure Backup 可讓您 toooffload 存放裝置與 hello Azure 磁碟，您 tooscale 向上藉由將較舊的資料儲存在 Azure 備份，在磁碟上的新資料。

## <a name="how-does-dpm-server-backup-work"></a>DPM 伺服器備份的運作方式
新的虛擬機器，需要 hello 資料的時間點快照集的第一個 tooback。 hello Azure 備份服務會起始 hello 備份作業在 hello 排定的時間，而且觸發程序 hello 備用分機號碼 tootake 快照集。 hello 備用分機號碼座標與 hello 客體 VSS 服務 tooachieve 一致性，並叫用的 hello Azure 儲存體服務的 hello blob 快照 API，一旦達到一致性。 這是完成 tooget hello 磁碟 hello 虛擬機器的一致快照集，而不需要 tooshut 向下。

已擷取 hello 快照之後，hello Azure 備份服務 toohello 備份保存庫會傳送 hello 資料。 hello 服務會負責找出並傳送只有 hello 從 hello hello 備份儲存體和網路進行有效率的最後一個備份已變更的區塊。 Hello 資料傳輸完成時，會移除 hello 快照集並建立復原點。 Hello Azure 傳統入口網站中可以看到此復原點。

> [!NOTE]
> Linux 虛擬機器只能進行檔案一致性的備份。
>
>

## <a name="prerequisites"></a>必要條件
準備 Azure Backup tooback DPM 資料備份，如下所示：

1. **建立備份保存庫**。 如果您尚未建立備份保存庫中您訂用帳戶，請參閱 hello Azure 入口網站的版本，這篇文章-[準備與 DPM 工作負載 tooAzure 向上 tooback](backup-azure-dpm-introduction.md)。

  > [!IMPORTANT]
  > 從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
  > 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
  >- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
  >- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
  >

2. **下載保存庫認證**— 在 Azure Backup 上, 傳您建立 toohello 保存庫的 hello 管理憑證。
3. **安裝 hello Azure 備份代理程式並註冊 hello 伺服器**— 從 Azure Backup，在每一部 DPM 伺服器上安裝 hello 代理程式和 hello 備份保存庫中註冊 hello DPM 伺服器。

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>需求 (和限制)
* DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。 它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。
* 如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。 這是必要的才能安裝 hello Azure Backup Agent。
* hello DPM 伺服器應該使用 Windows PowerShell 和.Net Framework 4.5 安裝。
* DPM 可以備份大部分的工作負載 tooAzure 備份。 如需完整清單，支援功能的請參閱 hello Azure Backup 支援以下項目。
* Azure 備份中儲存的資料無法復原使用 hello 「 複製 tootape 」 選項。
* 您需要 Azure 帳戶啟用 hello Azure Backup 功能。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。
* 使用 Azure Backup 必須安裝在您想 tooback hello 伺服器 hello Azure Backup Agent toobe。 每一部伺服器必須至少 10%的 hello 正在備份，可做為本機可用儲存體的 hello 資料大小。 例如，備份 100 GB 的資料所需要的最小值為 10 GB 的可用空間 hello 臨時位置。 雖然 hello 最小值為 10%，建議使用 15%的可用本機儲存空間 toobe hello 快取位置使用。
* 資料會儲存在 hello Azure 保存庫儲存體中。 您可以備份 tooan Azure 備份保存庫的資料沒有限制 toohello 數量但 hello 大小的資料來源 （例如虛擬機器或資料庫） 不應該超過 54,400 GB。

這些檔案類型支援 tooAzure 備份：

* 加密 (僅限完整備份)
* 壓縮 (支援增量備份)
* 疏鬆 (支援增量備份)
* 壓縮和疏鬆 (視為疏鬆來處理)

下列為不支援的類型：

* 不支援區分大小寫的檔案系統上的伺服器。
* 硬式連結 (略過)
* 重新分析點 (略過)
* 加密和壓縮 (略過)
* 加密和疏鬆 (略過)
* 壓縮資料流
* 疏鬆資料流

> [!NOTE]
> 從 System Center 2012 DPM with SP1 開始，在您可以備份使用 Microsoft Azure 備份的 DPM tooAzure 所保護的工作負載。
>
>
