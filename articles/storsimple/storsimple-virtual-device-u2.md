---
title: "aaaStorSimple 虛擬裝置 Update 2 |Microsoft 文件"
description: "了解 toocreate，部署及管理 Microsoft Azure 虛擬網路中的 StorSimple 虛擬裝置的方式。 （適用於 tooStorSimple Update 2）。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>部署和管理 Azure 中的 StorSimple 虛擬裝置
## <a name="overview"></a>概觀
hello StorSimple 8000 系列的虛擬裝置是隨附於 Microsoft Azure StorSimple 方案的額外功能。 hello StorSimple 虛擬裝置會在 Microsoft Azure 虛擬網路中，在虛擬機器上執行，您可以使用它向上 tooback 和複製資料從您的主機。 這個教學課程描述如何 toodeploy 和管理 Azure 中的虛擬裝置，以及為適用 tooall hello 執行軟體版本更新 2 和較低的虛擬裝置。

#### <a name="virtual-device-model-comparison"></a>虛擬裝置模型比較
hello StorSimple 虛擬裝置已使用在兩個模型中，標準的 8010 （之前稱為 hello 1100） 」 與 「 進階 8020 （Update 2 中引進）。 Hello 兩個模型的比較是下面製成資料表。

| 裝置型號 | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **最大容量** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 核心、7 GB 記憶體) |Standard_DS3 (4 核心、14 GB 記憶體) |
| **版本相容性** |執行 Update 2 之前或更新版本的版本 |執行 Update 2 或更新版本的版本 |
| **區域可用性** |所有 Azure 區域 |支援進階儲存體和 DS3 Azure VM 的所有 Azure 區域<br></br> 使用[這份清單](https://azure.microsoft.com/en-us/regions/services)toosee 如果兩個*虛擬機器 > DS 系列*和*存放裝置 > 磁碟儲存體*都是在您的區域。 |
| **儲存體類型** |將 Azure 標準儲存體使用於本機磁碟<br></br> 了解如何太[建立標準儲存體帳戶](../storage/common/storage-create-storage-account.md) |將 Azure 進階儲存體使用於本機磁碟<sup>2</sup> <br></br>了解如何太[建立高階儲存體帳戶](../storage/common/storage-premium-storage.md) |
| **工作負載指引** |從備份的檔案的項目層級擷取 |雲端開發和測試案例、低延遲、較高效能工作負載 <br></br>災害復原的次要裝置 |

<sup>1</sup> *稱為 hello 1100*。

<sup>2</sup> *兩者 hello 8010 並用 8020 Azure 標準儲存體的 hello 雲端層。 hello 差異僅存在於內 hello 裝置 hello 本機層*。

本文說明 hello 部署 StorSimple 虛擬裝置在 Azure 中的逐步程序。 閱讀本文之後，您將能夠：

* 了解如何 hello 虛擬裝置與 hello 實體裝置。
* 應能 toocreate，且設定 hello 虛擬裝置。
* 連接 toohello 虛擬裝置。
* 深入了解如何 toowork hello 虛擬裝置。

本教學課程適用於 tooall hello StorSimple 虛擬裝置執行 Update 2 與更新版本。

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Hello 虛擬裝置不同於 hello 實體裝置的方式
hello StorSimple 虛擬裝置是軟體形式的 StorSimple，在 Microsoft Azure 虛擬機器中的單一節點上執行。 hello 虛擬裝置支援災害復原案例實體裝置就無法使用，以及適用於從備份項目層級擷取用於在內部部署災害復原和雲端開發人員和測試案例。

#### <a name="differences-from-hello-physical-device"></a>與 hello 實體裝置的差異
hello 下表顯示 hello StorSimple 虛擬裝置與 hello StorSimple 實體裝置之間的一些主要差異。

|  | 實體裝置 | 虛擬裝置 |
| --- | --- | --- |
| **位置** |位於 hello 資料中心。 |在 Azure 中執行。 |
| **網路介面** |有六個網路介面：DATA 0 到 DATA 5。 |只有一個網路介面：DATA 0。 |
| **註冊** |註冊期間 hello 組態步驟。 |註冊是個別的工作。 |
| **服務資料加密金鑰** |重新產生 hello 實體裝置上，然後以 hello 新的金鑰更新 hello 虛擬裝置。 |無法重新產生從 hello 虛擬裝置。 |

## <a name="prerequisites-for-hello-virtual-device"></a>Hello 虛擬裝置的必要條件
hello 下列各節說明 hello StorSimple 虛擬裝置的組態先決條件。 先前 toodeploying 虛擬裝置，檢閱 hello[使用虛擬裝置的安全性考量](storsimple-security.md#storsimple-virtual-device-security)。

#### <a name="azure-requirements"></a>Azure 需求
佈建 hello 虛擬裝置之前，您需要下列 Azure 環境中的準備 toomake hello:

* Hello 虛擬裝置，請[在 Azure 中設定虛擬網路](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 如果使用進階儲存體，您必須在支援進階儲存體的 Azure 區域中建立虛擬網路。 hello Premium 儲存體區域是區域對應 toohello 資料列*磁碟儲存體*hello 清單中[依地區的 Azure 服務](https://azure.microsoft.com/en-us/regions/services)。
* 它是 Azure 所提供，而不是指定您自己的 DNS 伺服器名稱的建議 toouse hello 預設 DNS 伺服器。 如果您的 DNS 伺服器名稱無效或 hello DNS 伺服器不能 tooresolve IP 位址正確，hello 建立 hello 虛擬裝置將會失敗。
* 點對站及站對站都是選用的，但並非必要。 如有需要，您可以針對更進階的案例設定這些選項。
* 您可以建立[Azure 虛擬機器](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)（主機伺服器） 可以使用 hello hello 虛擬裝置所公開的磁碟區的 hello 虛擬網路中。 這些伺服器必須符合下列需求的 hello:                             

  * 是已安裝 iSCSI 啟動器軟體的 Windows 或 Linux VM。
  * 執行在 hello 與 hello 虛擬裝置相同虛擬網路。
  * 可以透過 hello 內部 IP 位址的 hello 虛擬裝置 hello 虛擬裝置無法 tooconnect toohello iSCSI 目標。
* 請確定您已設定支援 iSCSI 和雲端流量 hello 上相同虛擬網路。

#### <a name="storsimple-requirements"></a>StorSimple 需求
請更新 tooyour Azure StorSimple 服務之後，您建立虛擬裝置前的 hello:

* 新增[存取控制記錄](storsimple-manage-acrs.md)hello 將要 toobe 虛擬裝置的主機伺服器的 Vm。
* 使用[儲存體帳戶](storsimple-manage-storage-accounts.md#add-a-storage-account)在 hello 與 hello 虛擬裝置相同的區域。 若儲存體帳戶位於不同區域，可能導致效能不佳。 您可以與 hello 虛擬裝置搭配使用的標準或高階儲存體帳戶。 更多有關如何 toocreate[標準儲存體帳戶](../storage/common/storage-create-storage-account.md)或[高階儲存體帳戶](../storage/common/storage-premium-storage.md)
* 用於建立虛擬裝置 hello 用於您的資料從其他儲存體帳戶。 使用相同的儲存體帳戶可能會導致效能不佳的 hello。

請確定您擁有 hello 下列資訊，才能開始：

* 您的 Azure 傳統入口網站帳戶具有存取認證。
* 從您的實體裝置 hello 服務資料加密金鑰的複本。

## <a name="create-and-configure-hello-virtual-device"></a>建立及設定 hello 虛擬裝置
在之前執行這些程序，請確定您已符合 hello [hello 虛擬裝置的必要條件](#prerequisites-for-the-virtual-device)。

您建立虛擬網路、 設定 StorSimple Manager 服務，並在實體 StorSimple 裝置向 hello 服務之後，您可以使用下列步驟 toocreate hello，並設定 StorSimple 虛擬裝置。

### <a name="step-1-create-a-virtual-device"></a>步驟 1：建立虛擬裝置
執行下列步驟 toocreate hello StorSimple 虛擬裝置 hello。

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

如果 hello 建立 hello 虛擬裝置失敗，在此步驟中，您可能沒有連線 toohello 網際網路。 如需詳細資訊，請移至太[疑難排解網際網路連線失敗](#troubleshoot-internet-connectivity-errors)時建立虛擬裝置。

### <a name="step-2-configure-and-register-hello-virtual-device"></a>步驟 2： 設定和註冊 hello 虛擬裝置
然後再開始此程序，請確定您已擁有 hello 服務資料加密金鑰的副本。 hello 服務資料加密金鑰時所建立您設定第一個 StorSimple 裝置，且已指示 toosave 它在安全的位置。 如果您沒有 hello 服務資料加密金鑰的複本，您必須連絡 Microsoft 支援服務尋求協助。

執行下列步驟 tooconfigure hello 和註冊 StorSimple 虛擬裝置。

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>步驟 3: （選擇性） 修改 hello 裝置組態設定
hello 下列小節說明如果您想要 toouse CHAP 時，StorSimple Snapshot Manager，或變更 hello 裝置系統管理員密碼 hello StorSimple 虛擬裝置所需的 hello 裝置組態設定。

#### <a name="configure-hello-chap-initiator"></a>設定 hello CHAP 起始端
這個參數會包含虛擬裝置 （目標） 預期從嘗試 tooaccess hello 磁碟區的 hello 啟動器 （伺服器） 的 hello 認證。 hello 起始端將會提供 CHAP 使用者名稱和 CHAP 密碼 tooidentify 本身 tooyour 裝置在這個驗證過程。 如需詳細步驟，請移太[為您的裝置設定 CHAP](storsimple-configure-chap.md#unidirectional-or-one-way-authentication)。

#### <a name="configure-hello-chap-target"></a>設定 hello CHAP 目標
這個參數會包含具有 CHAP 功能的起始端要求相互或雙向驗證時，會使用您的虛擬裝置的 hello 認證。 虛擬裝置會使用反向 CHAP 使用者名稱和反向 CHAP 密碼 tooidentify 本身 toohello 啟動器在此驗證程序。 請注意，CHAP 目標設定為全域設定。 當套用這些時，所有 hello 磁碟區連接的 toohello 存放虛擬裝置會都使用 CHAP 驗證。 如需詳細步驟，請移太[為您的裝置設定 CHAP](storsimple-configure-chap.md#bidirectional-or-mutual-authentication)。

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>設定 hello StorSimple Snapshot Manager 密碼
StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。

> [!NOTE]
> Hello 虛擬裝置，您的 Windows 主機的 Azure 虛擬機器。
>
>

當 hello StorSimple Snapshot Manager 中設定裝置，您將會提示您 tooprovide hello StorSimple 裝置 IP 位址和密碼 tooauthenticate 存放裝置。 如需詳細步驟，請移太[設定 StorSimple Snapshot Manager 密碼](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)。

#### <a name="change-hello-device-administrator-password"></a>變更 hello 裝置系統管理員密碼
當您使用 hello Windows PowerShell 介面 tooaccess hello 虛擬裝置，您將會需要的 tooenter 裝置系統管理員密碼。 如 hello 資料的安全性，您會需要的 toochange 此密碼，才能 hello 虛擬裝置可供使用。 如需詳細步驟，請移太[設定裝置系統管理員密碼](storsimple-change-passwords.md#change-the-device-administrator-password)。

## <a name="connect-remotely-toohello-virtual-device"></a>從遠端連線 toohello 虛擬裝置
預設不啟用遠端存取 tooyour 虛擬裝置透過 hello Windows PowerShell 介面。 您首先，需要 tooenable hello 虛擬裝置上的啟用遠端管理，然後啟用它將會使用的 tooaccess hello 用戶端上您虛擬裝置。

hello 兩步驟程序 tooconnect 遠端詳述如下。

### <a name="step-1-configure-remote-management"></a>步驟 1：設定遠端管理
執行下列步驟 tooconfigure 遠端管理您的 StorSimple 虛擬裝置 hello。

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>步驟 2： 從遠端存取 hello 虛擬裝置
啟用遠端管理在 hello StorSimple 裝置設定 頁面之後，您可以使用 Windows PowerShell 遠端執行功能 tooconnect toohello 虛擬裝置 hello 內的另一部虛擬機器從相同虛擬網路。例如，您可以從 hello 主機 VM，您設定並使用 tooconnect iSCSI 連線。 在大多數部署中，您都應已開啟公用端點 tooaccess 主機可用於存取 hello 虛擬裝置的 VM。

> [!WARNING]
> **為了加強安全性，我們強烈建議使用 HTTPS 連線 toohello 端點時，您已完成 PowerShell 遠端工作階段後，再刪除 hello 端點。**
>
>

您應該依照 hello 程序[遠端連線 tooyour StorSimple 裝置](storsimple-remote-connect.md)tooset 註冊虛擬裝置的遠端處理功能。

## <a name="connect-directly-toohello-virtual-device"></a>直接連接 toohello 虛擬裝置
您也可以連接直接 toohello 虛擬裝置。 如果您想要 tooconnect 直接 toohello 從 hello 虛擬網路或外部的 hello Microsoft Azure 環境之外的另一部電腦的虛擬裝置，您需要 toocreate hello 遵循程序中所述的其他端點。

執行下列步驟 toocreate 公用端點 hello 虛擬裝置上的 hello。

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

我們建議您從連接 hello 內的另一部虛擬機器相同虛擬網路，因為這種作法將虛擬網路上的公用端點的 hello 數目降到最低。 當您使用這個方法時，您只要透過遠端桌面工作階段連接 toohello 虛擬機器，並如同本機網路上的任何其他 Windows 用戶端，然後設定用於該虛擬機器。 因為將會已知 hello 連接埠不需要 tooappend hello 公用連接埠號碼。

## <a name="work-with-hello-storsimple-virtual-device"></a>與 hello StorSimple 虛擬裝置搭配使用
現在您已建立和設定 hello StorSimple 虛擬裝置，您就準備好 toostart 加以使用。 您可以使用磁碟區容器、 磁碟區以及備份原則上的虛擬裝置就如同實體 StorSimple 裝置。hello 唯一的差別是您需要 toomake 確定從您的裝置清單中選取 hello 虛擬裝置。 請參閱太[使用 hello StorSimple Manager 服務 toomanage 虛擬裝置](storsimple-manager-service-administration.md)hello hello 虛擬裝置的各種管理工作的逐步程序。

hello 下列各節將討論一些與 hello 虛擬裝置搭配使用時，您將會遇到的 hello 差異。

### <a name="maintain-a-storsimple-virtual-device"></a>維護 StorSimple 虛擬裝置
因為它是一個純軟體裝置，維護 hello 虛擬裝置時，最少比較 toomaintenance hello 實體裝置。 您有下列選項的 hello:

* **軟體更新**– 您可以檢視上次更新 hello 軟體，以及任何更新狀態訊息的 hello 日期。 您可以使用 hello**掃描更新**按鈕在 hello 底部 hello 頁面 tooperform 手動掃描如果您想 toocheck 新的更新。 如果更新可用，請按一下**安裝更新**tooinstall。 因為沒有在 hello 虛擬裝置上的單一介面，這表示會有服務略為中斷套用更新的時間。 hello 虛擬裝置將會關閉並重新啟動 （如果有必要） tooapply 任何已發行的更新。 如逐步程序，請移至太[更新您的裝置](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal)。
* **支援封裝**– 您可以建立並上傳支援套件 toohelp Microsoft 支援服務疑難排解您的虛擬裝置的問題。 如逐步程序，請移至太[建立及管理支援封裝](storsimple-create-manage-support-package.md)。

### <a name="storage-accounts-for-a-virtual-device"></a>虛擬裝置的儲存體帳戶
儲存體帳戶所建立的 hello StorSimple Manager 服務、 虛擬裝置 hello，和 hello 實體裝置。 當您建立儲存體帳戶時，我們建議您使用的地區識別碼 hello 易記名稱 toohelp 中的確定該 hello 地區都是一致的所有 hello 系統元件。 是虛擬裝置，請務必所有元件是中的 hello hello 相同區域 tooprevent 效能問題。

如逐步程序，請移至太[加入儲存體帳戶](storsimple-manage-storage-accounts.md#add-a-storage-account)。

### <a name="deactivate-a-storsimple-virtual-device"></a>停用 StorSimple 虛擬裝置
停用虛擬裝置會刪除 hello VM 建立時已佈建的 hello 資源。 Hello 虛擬裝置停用之後，它不能還原 tooits 先前的狀態。 您停用 hello 虛擬裝置之前，請確定 toostop 或刪除用戶端和依賴它的主機。

停用虛擬裝置會導致下列動作的 hello:

* 移除 hello 虛擬裝置。
* hello OS 磁碟和資料磁碟建立 hello 虛擬裝置會移除。
* 保留 hello 裝載服務和佈建期間建立的虛擬網路。 如果您不使用它們，就應該手動加以刪除。
* 建立 hello 虛擬裝置的雲端快照集會保留。

如逐步程序，請移至太[停用及刪除您的 StorSimple 裝置](storsimple-deactivate-and-delete-device.md)。

只要 hello 虛擬裝置會顯示為停用在 hello StorSimple Manager 服務頁面上，您可以從 hello 上的裝置清單刪除 hello 虛擬裝置**裝置**頁面。

### <a name="start-stop-and-restart-a-virtual-device"></a>啟動、停止和重新啟動虛擬裝置
不同於 StorSimple 實體裝置 hello，沒有任何電源開啟或關閉 StorSimple 虛擬裝置上的按鈕 toopush 電源。 不過，可能有的一些情況需要 toostop，而重新啟動 hello 虛擬裝置。 例如，有些更新可能會重新啟動 VM 會與該 hello toofinish hello 更新程序。 hello 您 toostart、 停止及重新啟動虛擬裝置的最簡單的方式為 toouse hello 虛擬機器管理主控台。

當您查看 hello 管理主控台時，hello 虛擬裝置的狀態是**執行**因為在建立後，依預設已啟動。 您隨時都能啟動、停止及重新啟動虛擬機器。

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>重設 toofactory 預設值
如果您決定，您只想 toostart 透過您的虛擬裝置，只需要停用及刪除它並再建立新。 就像您的實體裝置重設時，新的虛擬裝置並不會安裝; 任何更新因此，請確定 toocheck 後才能使用它的更新。

## <a name="fail-over-toohello-virtual-device"></a>容錯移轉 toohello 虛擬裝置
災害復原 (DR) 是其中一個 hello hello 的 StorSimple 虛擬裝置所針對的主要案例。 在此案例中，hello 實體 StorSimple 裝置，或整個資料中心可能無法使用。 幸運的是，您可以使用虛擬裝置 toorestore 作業在替代位置。 在 DR 期間，hello 來源裝置 hello 磁碟區容器會變更擁有權，並會傳送的 toohello 虛擬裝置。 hello DR 的必要條件是，已建立並設定 hello 虛擬裝置、 hello 磁碟區容器內的所有 hello 磁碟區都要都離線，和 hello 磁碟區容器具有相關聯的雲端快照集。

> [!NOTE]
> * 使用虛擬裝置做時 hello 次要裝置 dr，請注意，hello 8010 具有 30TB，標準儲存體 8020 具有 64 TB 的進階儲存體。 hello 高容量 8020 虛擬裝置可能是更適合 DR 案例。
> * 您無法容錯移轉或再製，從執行的裝置更新 2 tooa 裝置執行更新前 1 軟體。 您可以不過容錯移轉執行 Update 2 tooa 裝置執行 Update 1 （1.1 或 1.2） 的裝置
>
>

如逐步程序，請移至太[容錯移轉 tooa 虛擬裝置](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device)。

## <a name="shut-down-or-delete-hello-virtual-device"></a>關閉或刪除 hello 虛擬裝置
如果您之前設定並使用 StorSimple 虛擬裝置但現在想 toostop 持計算費用，其用途，您可以關閉 hello 虛擬裝置。 正在關閉 hello 虛擬裝置並不會刪除其作業系統或儲存體中的資料磁碟。 它會停止費用持您的訂用帳戶，但儲存體費用 hello OS 和資料磁碟將會繼續。

如果您刪除或關閉 hello 虛擬裝置時，它會顯示為**離線**hello 裝置 hello StorSimple Manager 服務頁面上。 您可以選擇 toodeactivate 或刪除 hello 裝置，如果您也想 toodelete hello hello 虛擬裝置所建立的備份。 如需詳細資訊，請參閱 [停用及刪除 StorSimple 裝置](storsimple-deactivate-and-delete-device.md)。

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>針對網際網路連線錯誤進行疑難排解
Hello 建立期間虛擬裝置，如果沒有任何連線 toohello 網際網路，hello 建立步驟將會失敗。 tootroubleshoot hello 失敗是否因網際網路連線，執行下列步驟在 hello Azure 傳統入口網站中的 hello:

1. 在 Azure 中建立 Windows server 2012 虛擬機器。 此虛擬機器應該使用相同的儲存體帳戶、 VNet 和子網路所使用的虛擬裝置 hello。 如果您已經有現有的 Windows Server 主機，在 Azure 中使用 hello 相同的儲存體帳戶、 Vnet 和子網路，您也可以使用它 tootroubleshoot hello 網際網路連線。
2. 遠端登入 hello hello 前面步驟中建立的虛擬機器。
3. 開啟命令視窗 hello 虛擬機器內 (Win + R，然後輸入`cmd`)。
4. 執行下列 cmd 在 hello 提示字元中的 hello。

    `nslookup windows.net`
5. 如果`nslookup`失敗，則網際網路連線失敗導致 hello 虛擬裝置無法註冊 toohello StorSimple Manager 服務。
6. 變更所需的 hello tooyour hello 虛擬裝置的虛擬網路 tooensure 是無法 tooaccess 例如"windows.net 「 Azure 站台。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello StorSimple Manager 服務 toomanage 虛擬裝置](storsimple-manager-service-administration.md)。
* 了解如何太[StorSimple 磁碟區從備份組還原](storsimple-restore-from-backup-set.md)。
