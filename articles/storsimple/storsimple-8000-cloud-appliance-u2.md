---
title: "aaaStorSimple 雲端設備更新 3 |Microsoft 文件"
description: "了解 toocreate，部署及管理 Microsoft Azure 虛擬網路中的 StorSimple 雲端應用裝置的方式。 （適用於 tooStorSimple Update 3 及更新版本）。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>部署和管理 Azure 中的 StorSimple 雲端設備 (Update 3 和更新版本)

## <a name="overview"></a>概觀

hello StorSimple 8000 系列雲端應用裝置是隨附於 Microsoft Azure StorSimple 方案的額外功能。 hello StorSimple 雲端應用裝置會在 Microsoft Azure 虛擬網路中，在虛擬機器上執行，您可以使用它向上 tooback 和複製資料從您的主機。

本文描述 hello 逐步程序 toodeploy，並管理在 Azure StorSimple 雲端應用裝置。 閱讀本文之後，您將能夠：

* 了解如何 hello 雲端應用裝置與 hello 實體裝置。
* 應能 toocreate，且設定 hello 雲端應用裝置。
* 連接 toohello 雲端應用裝置。
* 了解如何以 hello toowork 雲端應用裝置。

此教學課程適用於 tooall hello StorSimple 雲端應用程式執行 Update 3 及更新版本。

#### <a name="cloud-appliance-model-comparison"></a>雲端設備模型比較

hello StorSimple 雲端應用裝置中有兩個模型，標準的 8010 （之前稱為 hello 1100） 」 與 「 進階 8020 （Update 2 中引進）。 下表中的 hello 顯示 hello 兩個模型的比較。

| 裝置型號 | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **最大容量** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 核心、7 GB 記憶體)| Standard_DS3 (4 核心、14 GB 記憶體)|
| **區域可用性** |所有 Azure 區域 |支援進階儲存體和 DS3 Azure VM 的 Azure 區域<br></br>使用[這份清單](https://azure.microsoft.com/regions/services/)toosee 如果兩個**虛擬機器 > DS 系列**和**存放裝置 > 磁碟儲存體**都是在您的區域。 |
| **儲存體類型** |將 Azure 標準儲存體使用於本機磁碟<br></br> 了解如何太[建立標準儲存體帳戶](../storage/common/storage-create-storage-account.md) |將 Azure 進階儲存體使用於本機磁碟<sup>2</sup> <br></br>了解如何太[建立高階儲存體帳戶](../storage/common/storage-premium-storage.md) |
| **工作負載指引** |從備份的檔案的項目層級擷取 |雲端開發和測試案例 <br></br>低延遲和更高的效能工作負載<br></br>災害復原的次要裝置 |

<sup>1</sup> *稱為 hello 1100*。

<sup>2</sup> *兩者 hello 8010 並用 8020 Azure 標準儲存體的 hello 雲端層。 hello 差異僅存在於內 hello 裝置 hello 本機層*。

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Hello 雲端應用裝置不同於 hello 實體裝置的方式

hello StorSimple 雲端應用裝置是軟體形式的 StorSimple，在 Microsoft Azure 虛擬機器中的單一節點上執行。 hello 雲端應用裝置支援災害復原案例是在不使用您的實體裝置。 hello 雲端應用裝置是適用於從備份、 在內部部署災害復原，以及雲端開發和測試案例的項目層級擷取。

#### <a name="differences-from-hello-physical-device"></a>與 hello 實體裝置的差異

hello 下表顯示 hello StorSimple 雲端應用裝置和 hello StorSimple 實體裝置之間的一些主要差異。

|  | 實體裝置 | 雲端設備 |
| --- | --- | --- |
| **位置** |位於 hello 資料中心。 |在 Azure 中執行。 |
| **網路介面** |有六個網路介面：DATA 0 到 DATA 5。 |只有一個網路介面：DATA 0。 |
| **註冊** |註冊期間 hello 初始設定步驟。 |註冊是個別的工作。 |
| **服務資料加密金鑰** |重新產生 hello 實體裝置上，然後以 hello 新的金鑰更新 hello 雲端應用裝置。 |無法重新產生從 hello 雲端應用裝置。 |
| **支援的磁碟區類型** |支援固定在本機和分層的磁碟區。 |只支援分層的磁碟區。 |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Hello 雲端應用裝置的必要條件

hello 下列各節說明您的 StorSimple 雲端應用裝置 hello 組態先決條件。 在部署雲端應用裝置之前，檢閱 hello 使用雲端應用裝置的安全性考量。

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Azure 需求

佈建 hello 雲端應用裝置之前，您需要下列 Azure 環境中的準備 toomake hello:

* 請確定您的資料中心已部署和執行 StorSimple 8000 系列實體裝置 (模型 8100 或 8600)。 註冊此裝置與 hello 相同 StorSimple 裝置管理員服務想 toocreate 的 StorSimple 雲端應用裝置。
* Hello 雲端應用裝置，[在 Azure 中設定虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。 如果使用進階儲存體，您必須在支援進階儲存體的 Azure 區域中建立虛擬網路。 hello Premium 儲存體區域是區域對應磁碟中的存放裝置 hello toohello 列[依地區的 Azure 服務清單](https://azure.microsoft.com/regions/services/)。
* 我們建議您使用 Azure 所提供，而不是指定您自己的 DNS 伺服器名稱的 hello 預設 DNS 伺服器。 如果您的 DNS 伺服器名稱無效或 hello DNS 伺服器不能 tooresolve IP 位址正確，hello 建立 hello 雲端應用裝置將會失敗。
* 點對站及站對站都是選用的，但並非必要。 如有需要，您可以針對更進階的案例設定這些選項。
* 您可以建立[Azure 虛擬機器](../virtual-machines/virtual-machines-windows-quick-create-portal.md)（主機伺服器） 可以使用 hello hello 雲端應用裝置所公開的磁碟區的 hello 虛擬網路中。 這些伺服器必須符合下列需求的 hello:

  * 是已安裝 iSCSI 啟動器軟體的 Windows 或 Linux VM。
  * 執行在 hello 與 hello 雲端應用裝置的相同虛擬網路。
  * 透過 hello 雲端應用裝置 hello 內部 IP 位址是 hello 雲端應用裝置能夠 tooconnect toohello iSCSI 目標。
  * 請確定您已設定支援 iSCSI 和雲端流量 hello 上相同虛擬網路。

#### <a name="storsimple-requirements"></a>StorSimple 需求

請更新 tooyour StorSimple 裝置管理員 」 服務之後才建立雲端應用裝置 hello:

* 新增[存取控制記錄](storsimple-8000-manage-acrs.md)為屬於您的雲端應用裝置進行 toobe hello 主機伺服器 hello Vm。
* 使用[儲存體帳戶](storsimple-8000-manage-storage-accounts.md#add-a-storage-account)在 hello 與 hello 雲端應用裝置相同的區域。 若儲存體帳戶位於不同區域，可能導致效能不佳。 您可以使用標準或高階儲存體帳戶與 hello 雲端應用裝置。 更多有關如何 toocreate[標準儲存體帳戶](../storage/common/storage-create-storage-account.md)或[高階儲存體帳戶](../storage/common/storage-premium-storage.md)
* 用於 hello 用於您的資料從雲端應用裝置建立不同的儲存體帳戶。 使用相同的儲存體帳戶可能會導致效能不佳的 hello。

請確定您擁有 hello 下列資訊，才能開始：

* 具有存取認證的 Azure 入口網站帳戶。
* 從您的實體裝置 hello 服務資料加密金鑰的副本註冊 toohello StorSimple 裝置管理員服務。

## <a name="create-and-configure-hello-cloud-appliance"></a>建立及設定 hello 雲端應用裝置

在之前執行這些程序，請確定您已符合 hello [hello 雲端應用裝置的必要條件](#prerequisites-for-the-cloud-appliance)。

執行下列步驟 toocreate StorSimple 雲端應用裝置 hello。

### <a name="step-1-create-a-cloud-appliance"></a>步驟 1：建立雲端設備

執行下列步驟 toocreate hello StorSimple 雲端應用裝置 hello。

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

如果 hello 雲端應用裝置 hello 建立失敗，在此步驟中，您可能沒有連線 toohello 網際網路。 如需詳細資訊，請移至太[疑難排解網際網路連線失敗](#troubleshoot-internet-connectivity-errors)建立雲端應用裝置時。

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>步驟 2： 設定和註冊 hello 雲端應用裝置

在開始此程序之前，請確定您已擁有 hello 服務資料加密金鑰的副本。 第一個 StorSimple 實體裝置向 hello StorSimple 裝置管理員服務時，會建立 hello 服務資料加密金鑰。 已指示 toosave 它在安全的位置。 如果您沒有 hello 服務資料加密金鑰的複本，您必須連絡 Microsoft 支援服務尋求協助。

執行下列步驟 tooconfigure hello，並註冊您的 StorSimple 雲端應用裝置。

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>步驟 3: （選擇性） 修改 hello 裝置組態設定

hello 下節說明 hello 裝置組態設定所需的 hello StorSimple 雲端應用裝置，如果您想 toouse CHAP 時，StorSimple Snapshot Manager，或變更 hello 裝置系統管理員密碼。

#### <a name="configure-hello-chap-initiator"></a>設定 hello CHAP 起始端

這個參數會包含您的雲端應用裝置 （目標） 預期從嘗試 tooaccess hello 磁碟區的 hello 啟動器 （伺服器） 的 hello 認證。 hello 啟動器提供 CHAP 使用者名稱和 CHAP 密碼 tooidentify 本身 tooyour 裝置在這個驗證過程。 如需詳細步驟，請移太[為您的裝置設定 CHAP](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication)。

#### <a name="configure-hello-chap-target"></a>設定 hello CHAP 目標

這個參數會包含具有 CHAP 功能的起始端要求相互或雙向驗證時，會使用您的雲端應用裝置的 hello 認證。 您的雲端應用裝置必須使用反向 CHAP 使用者名稱和反向 CHAP 密碼 tooidentify 本身 toohello 啟動器在此驗證程序。

> [!NOTE]
> CHAP 目標設定為全域設定。 當套用這些設定時，所有 hello 磁碟區都連接 toohello 雲端應用裝置使用 CHAP 驗證。

如需詳細步驟，請移太[為您的裝置設定 CHAP](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication)。

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>設定 hello StorSimple Snapshot Manager 密碼

StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。

> [!NOTE]
> Hello 雲端應用裝置，您的 Windows 主機會為 Azure 虛擬機器。

在 hello StorSimple Snapshot Manager 中設定裝置，系統會提示您 tooprovide hello StorSimple 裝置 IP 位址和密碼 tooauthenticate 存放裝置。 如需詳細步驟，請移太[設定 StorSimple Snapshot Manager 密碼](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password)。

#### <a name="change-hello-device-administrator-password"></a>變更 hello 裝置系統管理員密碼

當您使用 hello Windows PowerShell 介面 tooaccess hello 雲端應用裝置，您會需要的 tooenter 裝置系統管理員密碼。 Hello 資料的安全性，您必須變更此密碼才能使用 hello 雲端應用裝置。 如需詳細步驟，請移太[設定裝置系統管理員密碼](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password)。

## <a name="connect-remotely-toohello-cloud-appliance"></a>從遠端連線 toohello 雲端應用裝置

預設不啟用遠端存取 tooyour 雲端應用裝置，透過 hello Windows PowerShell 介面。 您必須先啟用 hello 雲端應用裝置上的啟用遠端管理，然後在 hello 上用戶端使用 tooaccess hello 雲端應用裝置。

hello 兩步驟程序描述如何 tooconnect 遠端 tooyour 雲端應用裝置。

### <a name="step-1-configure-remote-management"></a>步驟 1：設定遠端管理

執行下列步驟 tooconfigure 遠端管理您的 StorSimple 雲端應用裝置 hello。

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>步驟 2： 從遠端存取 hello 雲端應用裝置

啟用遠端管理 hello 雲端應用裝置上的之後，請使用 Windows PowerShell 遠端執行功能 tooconnect toohello 應用裝置 hello 內的另一部虛擬機器從相同虛擬網路。 例如，您可以從 hello 主機 VM，您設定並使用 tooconnect iSCSI 連線。 在大多數部署中，您會開啟公用端點 tooaccess 主機可用於存取 hello 雲端應用裝置的 VM。

> [!WARNING]
> **為了加強安全性，我們強烈建議使用 HTTPS 連線 toohello 端點時，您已完成 PowerShell 遠端工作階段後，再刪除 hello 端點。**

您必須依照 hello 程序[遠端連線 tooyour StorSimple 裝置](storsimple-8000-remote-connect.md)tooset 註冊您的雲端應用裝置的遠端處理功能。

## <a name="connect-directly-toohello-cloud-appliance"></a>直接連接 toohello 雲端應用裝置

您也可以連接直接 toohello 雲端應用裝置。 tooconnect 直接 toohello 雲端從另一部電腦以外的應用裝置 hello 虛擬網路或外部 hello Microsoft Azure 環境，您必須建立其他端點。

執行下列步驟 toocreate hello 雲端應用裝置上的公用端點的 hello。

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

我們建議您從連接 hello 內的另一部虛擬機器相同虛擬網路，因為這種作法將虛擬網路上的公用端點的 hello 數目降到最低。 在此情況下，透過遠端桌面工作階段連線 toohello 虛擬機器，然後再設定用於該虛擬機器，如同在本機網路上的任何其他 Windows 用戶端。 因為 hello 連接埠，就已經知道您不需要 tooappend hello 公用連接埠號碼。

## <a name="work-with-hello-storsimple-cloud-appliance"></a>使用 hello StorSimple 雲端應用裝置

現在您已建立和設定 hello StorSimple 雲端應用裝置，您就準備好 toostart 加以使用。 您可以使用雲端設備上的磁碟區容器、磁碟區及備份原則，如同實體 StorSimple 裝置上使用的一樣。 hello 唯一的差別是您需要 toomake 確定從您的裝置清單中選取 hello 雲端應用裝置。 請參閱太[使用 hello StorSimple 裝置管理員服務 toomanage 雲端應用裝置](storsimple-8000-manager-service-administration.md)hello hello 雲端應用裝置的各種管理工作的逐步程序。

hello 下列各節將討論一些您在使用 hello 雲端應用裝置時遇到的 hello 差異。

### <a name="maintain-a-storsimple-cloud-appliance"></a>維護 StorSimple 雲端設備

因為它是一個純軟體裝置，維護 hello 雲端應用裝置時，最少比較 toomaintenance hello 實體裝置。

您不能更新雲端設備。 使用軟體 toocreate 新的雲端應用裝置 hello 最新版本。


### <a name="storage-accounts-for-a-cloud-appliance"></a>雲端設備的儲存體帳戶

儲存體帳戶所建立的 hello StorSimple 裝置管理員服務、 hello 雲端應用裝置，以及 hello 實體裝置。 當您建立儲存體帳戶時，我們建議您在 hello 易記名稱中使用區域識別碼。 這有助於確保該 hello 地區都是一致的所有 hello 系統元件。 為雲端應用裝置，請務必所有 hello 元件都都在 hello 相同區域 tooprevent 效能問題。

如逐步程序，請移至太[加入儲存體帳戶](storsimple-8000-manage-storage-accounts.md#add-a-storage-account)。

### <a name="deactivate-a-storsimple-cloud-appliance"></a>停用 StorSimple 雲端設備

當您停用雲端應用裝置時，hello 動作會刪除 hello VM 和 hello 資源建立時已佈建。 Hello 雲端應用裝置已停用之後，它不能還原 tooits 先前的狀態。 您停用 hello 雲端應用裝置之前，請確定 toostop 或刪除用戶端和依賴它的主機。

停用雲端應用裝置會導致下列動作的 hello:

* hello 雲端應用裝置會移除。
* hello OS 磁碟和資料磁碟建立 hello 雲端應用裝置會移除。
* 保留 hello 裝載服務和佈建期間建立的虛擬網路。 如果您不使用它們，就應該手動加以刪除。
* 建立 hello 雲端應用裝置的雲端快照集會保留。

如逐步程序，請移至太[停用及刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。

只要 hello 雲端應用裝置會顯示為停用 hello StorSimple 裝置管理員服務刀鋒視窗上，您可以從 hello 上的裝置清單刪除 hello 雲端應用裝置**裝置**刀鋒視窗。

### <a name="start-stop-and-restart-a-cloud-appliance"></a>將雲端設備啟動、停止和重新啟動
不同於 StorSimple 實體裝置 hello，沒有任何電源開啟或關閉 StorSimple 雲端應用裝置上的按鈕 toopush 電源。 不過，可能有的一些情況需要 toostop，而重新啟動 hello 雲端應用裝置。

如您 toostart、 停止及重新啟動雲端應用裝置 hello 最簡單方式是透過 hello 虛擬機器服務刀鋒視窗。 移 hello 虛擬機器服務。 從 Vm 的 hello 清單，識別 hello VM 對應 tooyour 雲端應用裝置 （相同的名稱），然後按一下 hello VM 名稱。 當您查看您的虛擬機器刀鋒視窗時，hello 雲端應用裝置狀態會是**執行**因為在建立後，依預設已啟動。 您隨時都能啟動、停止及重新啟動虛擬機器。

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>重設 toofactory 預設值
如果您決定透過想 toostart，與您的雲端應用裝置，請停用和刪除它，然後建立一個新。

## <a name="fail-over-toohello-cloud-appliance"></a>容錯移轉 toohello 雲端應用裝置
災害復原 (DR) 是其中一個的 hello hello StorSimple 雲端應用裝置的主要案例針對設計。 在此案例中，hello 實體 StorSimple 裝置，或整個資料中心可能無法使用。 幸運的是，您可以使用雲端應用裝置 toorestore 作業在替代位置。 在 DR 期間，hello 來源裝置 hello 磁碟區容器會變更擁有權，並會傳送的 toohello 雲端應用裝置。

hello DR 的必要條件如下：

* hello 雲端應用裝置建立及設定。
* Hello 磁碟區容器內的所有 hello 磁碟區都會離線。
* hello 容錯移轉的磁碟區容器具有相關聯的雲端快照集。

> [!NOTE]
> * 當 DR 為 hello 次要裝置使用雲端應用裝置，請注意，hello 8010 具有 30TB，標準儲存體 8020 具有 64 TB，進階儲存體。 hello 高容量 8020 雲端應用裝置可能更適合 DR 案例。

如逐步程序，請移至太[容錯移轉 tooa 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。

## <a name="delete-hello-cloud-appliance"></a>刪除 hello 雲端應用裝置
如果您之前設定並使用 StorSimple 雲端應用裝置但現在想 toostop 持計算費用，其用途，您必須停止 hello 雲端應用裝置。 正在停止 hello 雲端應用裝置取消配置 hello VM。 這個動作將會停止您訂用帳戶上所產生的費用。 但是會繼續 hello 儲存體費用 hello OS 和資料磁碟。

所有 hello 的 toostop 費用，您必須刪除 hello 雲端應用裝置。 建立的 hello 雲端應用裝置 toodelete hello 備份，您可以停用或刪除 hello 裝置。 如需詳細資訊，請參閱 [停用及刪除 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>針對網際網路連線錯誤進行疑難排解
Hello 建立期間為雲端應用裝置，如果沒有任何連線 toohello 網際網路，hello 建立步驟會失敗。 tootroubleshoot 網際網路連線失敗，執行下列步驟在 hello Azure 入口網站中的 hello:

1. [在 Azure 中建立 Windows server 2012 虛擬機器](/articles/virtual-machines/windows/quick-create-portal.md)。 此虛擬機器應該使用 hello 相同儲存體帳戶、 VNet 和為您的雲端應用裝置所使用的子網路。 如果沒有現有 Windows Server 主機，在 Azure 中使用 hello 相同儲存體帳戶、 VNet、 和子網路，您也可以使用它 tootroubleshoot hello 網際網路連線。
2. 遠端登入 hello hello 前面步驟中建立的虛擬機器。
3. 開啟命令視窗 hello 虛擬機器內 (Win + R，然後輸入`cmd`)。
4. 執行下列 cmd 在 hello 提示字元中的 hello。

    `nslookup windows.net`
5. 如果`nslookup`失敗，則網際網路連線失敗導致無法登錄 toohello StorSimple 裝置管理員服務的 hello 雲端應用裝置。
6. 變更所需的 hello tooyour hello 雲端應用裝置的虛擬網路 tooensure 是無法 tooaccess Azure 站台例如_windows.net_。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello StorSimple 裝置管理員服務 toomanage 雲端應用裝置](storsimple-8000-manager-service-administration.md)。
* 了解如何太[StorSimple 磁碟區從備份組還原](storsimple-8000-restore-from-backup-set-u2.md)。
