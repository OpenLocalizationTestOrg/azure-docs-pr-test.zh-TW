---
title: "將 DPM 工作負載備份至 Azure 傳統入口網站 | Microsoft Docs"
description: "使用 Azure 備份服務來備份 DPM 伺服器的簡介"
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
ms.openlocfilehash: a9a516cfdfaf4b95c4f0121a66e90f6e71206e9f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="preparing-to-back-up-workloads-to-azure-with-dpm"></a>準備使用 DPM 將工作負載備份到 Azure
> [!div class="op_single_selector"]
> * [Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 備份伺服器 (傳統)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (傳統)](backup-azure-dpm-introduction-classic.md)
>
>

本文簡介如何使用 Microsoft Azure 備份來保護 System Center Data Protection Manager (DPM) 伺服器和工作負載。 在閱讀本文後，您將了解：

* Azure DPM 伺服器備份的運作方式
* 使備份流暢的必要條件
* 遇到的一般錯誤以及如何排除
* 支援的案例

System Center DPM 會備份檔案和應用程式資料。 備份到 DPM 的資料可以儲存在磁帶、磁碟上，或使用 Microsoft Azure 備份來備份到 Azure。 DPM 與 Azure 備份的互動方式如下：

* **DPM 部署為實體伺服器或內部部署虛擬機器** — 如果 DPM 部署為實體伺服器或內部部署 HYPER-V 虛擬機器，除了備份到磁碟和磁帶上，您還可以將資料備份到 Azure 備份保存庫。
* **DPM 部署為 Azure 虛擬機器** — 從 System Center 2012 R2 Update 3 開始，DPM 可以部署為 Azure 虛擬機器。 如果 DPM 部署為 Azure 虛擬機器，您可以將資料備份到連接至 DPM Azure 虛擬機器的 Azure 磁碟，或者您也可以將資料備份到 Azure 備份保存庫以卸載資料儲存體。

## <a name="why-backup-your-dpm-servers"></a>為何要備份 DPM 伺服器？
使用 Azure 備份來備份 DPM 伺服器的商業利益包括：

* 在內部部署 DPM 部署中，您可以使用 Azure 備份來替代長期的磁帶部署。
* 在 Azure 的 DPM 部署中，Azure 備份可讓您卸載 Azure 磁碟中的儲存體，進而透過將較舊的資料儲存在 Azure 備份上而將較新的資料儲存在磁碟上來進行擴充。

## <a name="how-does-dpm-server-backup-work"></a>DPM 伺服器備份的運作方式
若要備份虛擬機器，首先需要資料的時間點快照集。 Azure 備份服務在排定的時間初始備份作業，並觸發備份延伸模組以建立快照集。 備份延伸模組與客體的 VSS 服務進行協調以達到一致性，達到一致性後將叫用 Azure 儲存體服務的 blob 快照集 API。 這可以讓虛擬機器不需關機即可獲取一致性的磁碟快照集。

在擷取快照集之後，Azure 備份服務會將資料傳送到備份保存庫。 服務會負責識別上次備份後有所變更的區塊並只傳送這些區塊，讓備份儲存體和網路更有效率。 資料傳送完畢時將移除快照集，並建立復原點。 Azure 傳統入口網站中可以查看此復原點。

> [!NOTE]
> Linux 虛擬機器只能進行檔案一致性的備份。
>
>

## <a name="prerequisites"></a>必要條件
如下所示讓 Azure 備份做好備份 DPM 資料的準備：

1. **建立備份保存庫**。 如果您尚未在訂用帳戶中建立備份保存庫，請參閱[準備使用 DPM 將工作負載備份至 Azure](backup-azure-dpm-introduction.md) 這篇文章的 Azure 入口網站版本。

  > [!IMPORTANT]
  > 從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。
  > 您現在可以將備份保存庫升級至復原服務保存庫。 如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。 Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。<br/> 在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。 **在 2017 年 11 月 1 日以前**：
  >- 所有其餘的備份保存庫都會自動升級至復原服務保存庫。
  >- 您將無法在傳統入口網站中存取您的備份資料。 相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。
  >

2. **下載保存庫認證** — 在 Azure 備份中，將您建立的管理憑證上傳到保存庫。
3. **安裝 Azure 備份代理程式並註冊伺服器** — 從 Azure 備份，在每一部 DPM 伺服器上安裝代理程式，並在備份保存庫中註冊 DPM 伺服器。

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>需求 (和限制)
* DPM 可以做為實體伺服器或 System Center 2012 SP1 或 System Center 2012 R2 上安裝的 HYPER-V 虛擬機器來執行。 它也可以做為 System Center 2012 R2 (至少含 DPM 2012 R2 更新彙總套件 3) 上執行的 Azure 虛擬機器，或 System Center 2012 R2 (至少含更新彙總套件 5) 上執行之 VMWare 中的 Windows 虛擬機器來執行。
* 如果您使用 System Center 2012 SP1 來執行 DPM，則應該安裝 System Center Data Protection Manager SP1 的更新彙總套件 2。 要有此軟體才能安裝 Azure 備份代理程式。
* DPM 伺服器應該已安裝 Windows PowerShell 和 .Net Framework 4.5。
* DPM 可以將大部分的工作負載備份至 Azure 備份。 如需所支援項目的完整清單，請參閱下面的 Azure 備份支援項目。
* 使用 [複製到磁帶] 選項無法復原 Azure 備份中儲存的資料。
* 您需要已啟用 Azure 備份功能的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 請閱讀 [Azure 備份定價](https://azure.microsoft.com/pricing/details/backup/)。
* 要使用 Azure 備份，就必須在您想要備份的伺服器上安裝 Azure 備份代理程式。 每個伺服器必須至少具有所要備份之資料大小的 10 % 做為本機可用儲存空間。 例如，備份 100GB 的資料時，在臨時位置中至少需要 10 GB 的可用空間。 雖然最小值是 10%，但是建議使用 15% 的可用本機儲存空間來做為快取位置。
* 資料會儲存在 Azure 保存庫儲存體中。 可以備份至 Azure 備份保存庫的資料數量沒有限制，但是資料來源 (例如虛擬機器或資料庫) 的大小不應超過 54400 GB。

下列檔案類型可支援備份至 Azure：

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
> 從 System Center 2012 DPM SP1 開始，您可以使用 Microsoft Azure 備份將受到 DPM 保護的工作負載備份至 Azure。
>
>
