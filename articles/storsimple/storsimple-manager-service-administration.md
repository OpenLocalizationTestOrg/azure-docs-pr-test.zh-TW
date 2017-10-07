---
title: "aaaStorSimple 管理員服務管理 |Microsoft 文件"
description: "了解如何使用您的 StorSimple 裝置 hello StorSimple Manager 服務中的 toomanage hello Azure 傳統入口網站。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister
## <a name="overview"></a>概觀
本文說明 hello StorSimple Manager 服務介面，包括如何 tooconnect tooit hello 各種可用的選項，以及連結時，可以透過此 UI 執行的 toohello 特定工作流程。 本指南是適用 tooboth;hello StorSimple 實體與 hello 虛擬裝置。

閱讀本文知後，您將了解：

* 連接 tooStorSimple 管理員服務
* 瀏覽 hello StorSimple Manager UI
* 管理您的 StorSimple 裝置透過 hello StorSimple Manager 服務

## <a name="connect-toostorsimple-manager-service"></a>連接 tooStorSimple 管理員服務
hello StorSimple Manager 服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。 您使用管理中心的 Microsoft Azure 傳統入口網站，並在瀏覽器 toomanage 執行這些裝置。 tooconnect toohello StorSimple Manager 服務，請勿 hello 遵循。

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello 服務
1. 瀏覽過[https://manage.windowsazure.com/](https://manage.windowsazure.com/)。
2. 使用您的 Microsoft 帳戶認證，登入 toohello Microsoft Azure 傳統入口網站 （位於 hello 的右上方 hello 窗格）。
3. 捲動左導覽窗格 tooaccess hello StorSimple Manager 服務的 hello。

## <a name="navigate-storsimple-manager-service-ui"></a>瀏覽 StorSimple Manager 服務 UI
hello UI 會顯示 hello 下表中的 hello StorSimple Manager 服務導覽階層。

* **StorSimple Manager**登陸頁面會帶您 toohello UI 服務層級頁面適用 tooall 裝置服務內。
* **裝置**頁面會帶您 toohello 裝置層級 UI 頁面適用 tooa 特定裝置。
* **磁碟區容器**頁面會讓您顯示所有與裝置相關聯的 hello 磁碟區的 [toohello 磁碟區] 頁面。

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>StorSimple Manager 服務瀏覽階層
| 登陸頁面 | 服務層級頁面 | 裝置層級頁面 | 裝置層級頁面 |
| --- | --- | --- | --- |
| StorSimple Manager 服務 |服務儀表板 |裝置儀表板 | |
| 裝置 → |監視 | | |
| 備份類別目錄 |磁碟區容器 → |磁碟區 | |
| 設定 (服務) |備份原則 | | |
| 作業 |設定 (裝置) | | |
| Alerts |維護 | | |

![提供的影片](./media/storsimple-manager-service-administration/Video_icon.png) **提供的影片**

按一下 toowatch hello StorSimple Manager 服務使用者介面引導您的視訊[這裡](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/)。

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>使用 StorSimple Manager 服務管理 StorSimple 裝置
hello 下表顯示之所有 hello 常見管理工作和複雜工作流程可以在 hello StorSimple Manager 服務 UI 內執行的摘要。 這些工作被組織根據 hello UI 頁面啟動它們。

如需有關每個工作流程的詳細資訊，請按一下 hello hello 資料表中的適當程序。

#### <a name="storsimple-manager-workflows"></a>StorSimple Manager 工作流程
| 如果您希望 toodo 如此... | 移至 toothis UI 頁面... | 使用此程序。 |
| --- | --- | --- |
| 建立服務</br>刪除服務</br>取得服務註冊金鑰</br>重新產生服務註冊金鑰 |StorSimple Manager 服務 |[部署 StorSimple Manager 服務](storsimple-manage-service.md) |
| 變更 hello 服務資料加密金鑰</br>檢視 hello 作業記錄檔 |StorSimple Manager 服務 → 儀表板 |[使用 hello StorSimple Manager 服務儀表板](storsimple-service-dashboard.md) |
| 停用裝置</br>刪除裝置 |StorSimple Manager 服務 → 裝置 |[停用或刪除裝置](storsimple-deactivate-and-delete-device.md) |
| 了解災害復原和裝置容錯移轉</br>容錯移轉 tooa 實體裝置</br>容錯移轉 tooa 虛擬裝置</br>業務持續性災害復原 (BCDR) |StorSimple Manager 服務 → 裝置 |[StorSimple 裝置的容錯移轉與災害復原](storsimple-device-failover-disaster-recovery.md) |
| 列出磁碟區備份</br>選取備份組</br>刪除備份組 |StorSimple Manager 服務 → 備份目錄 |[管理備份](storsimple-manage-backup-catalog.md) |
| 複製磁碟區 |StorSimple Manager 服務 → 備份目錄 |[複製磁碟區](storsimple-clone-volume.md) |
| 還原備份組 |StorSimple Manager 服務 → 備份目錄 |[還原備份組](storsimple-restore-from-backup-set.md) |
| 有關儲存體帳戶</br>新增儲存體帳戶</br>編輯儲存體帳戶</br>刪除儲存體帳戶</br>儲存體帳戶的金鑰輪替 |StorSimple Manager 服務 → 設定 |[管理儲存體帳戶](storsimple-manage-storage-accounts.md) |
| 關於頻寬範本</br>新增頻寬範本</br>編輯頻寬範本</br>刪除頻寬範本</br>使用預設頻寬範本</br>建立在指定時間啟動的全天頻寬範本 |StorSimple Manager 服務 → 設定 |[管理頻寬範本](storsimple-manage-bandwidth-templates.md) |
| 關於存取控制記錄</br>建立存取控制記錄</br>編輯存取控制記錄</br>刪除存取控制記錄 |StorSimple Manager 服務 → 設定 |[管理存取控制記錄](storsimple-manage-acrs.md) |
| 檢視工作詳細資料</br>取消工作 |StorSimple Manager 服務 → 工作 |[管理工作](storsimple-manage-jobs.md) |
| 接收警示通知</br>管理警示</br>檢閱警示 |StorSimple Manager 服務 → 警示 |[檢視和管理 StorSimple 警示](storsimple-manage-alerts.md) |
| 檢視連接的啟動器</br>尋找裝置序號 hello</br>尋找 hello 目標 IQN |StorSimple Manager 服務 → 裝置 → 儀表板 |[使用 hello StorSimple 裝置儀表板](storsimple-device-dashboard.md) |
| 建立監視圖表 |StorSimple Manager 服務 → 裝置 → 監視器 |[監視您的 StorSimple 裝置](storsimple-monitor-device.md) |
| 新增磁碟區容器</br>修改磁碟區容器</br>刪除磁碟區容器 |StorSimple Manager 服務 → 裝置 → 磁碟區容器 |[管理磁碟區容器](storsimple-manage-volume-containers.md) |
| 新增磁碟區</br>修改磁碟區</br>使磁碟區離線</br>刪除磁碟區</br>監視磁碟區 |StorSimple Manager 服務 → 裝置 → 磁碟區容器 → 磁碟區 |[管理磁碟區](storsimple-manage-volumes.md) |
| 修改裝置設定</br>修改時間設定</br>修改 DNS.md 設定</br>設定網路介面 |StorSimple Manager 服務 → 裝置 → 設定 |[修改 StorSimple 裝置的裝置組態](storsimple-modify-device-config.md) |
| 檢視 Web Proxy 設定 |StorSimple Manager 服務 → 裝置 → 設定 |[設定裝置的 Web Proxy](storsimple-configure-web-proxy.md) |
| 修改裝置系統管理員密碼</br>修改 StorSimple Snapshot Manager 密碼 |StorSimple Manager 服務 → 裝置 → 設定 |[變更 StorSimple 密碼](storsimple-change-passwords.md) |
| 設定遠端管理 |StorSimple Manager 服務 → 裝置 → 設定 |[從遠端連線 tooyour StorSimple 裝置](storsimple-remote-connect.md) |
| 設定警示設定 |StorSimple Manager 服務 → 裝置 → 設定 |[檢視和管理 StorSimple 警示](storsimple-manage-alerts.md) |
| 為 StorSimple 裝置設定 CHAP |StorSimple Manager 服務 → 裝置 → 設定 |[為 StorSimple 裝置設定 CHAP](storsimple-configure-chap.md) |
| 新增備份原則</br>新增或修改排程</br>刪除備份原則</br>進行手動備份</br>使用多個磁碟區和排程建立自訂備份原則 |StorSimple Manager 服務 → 裝置 → 備份原則 |[管理備份原則](storsimple-manage-backup-policies.md) |
| 停止裝置控制器</br>重新啟動裝置控制器</br>關閉裝置控制器</br>重設您的裝置 toofactory 預設值</br>(上述項目僅適用於內部部署裝置) |StorSimple Manager 服務 → 裝置 → 維護 |[管理 StorSimple 裝置控制器](storsimple-manage-device-controller.md) |
| 了解 StorSimple 硬體元件</br>監視硬體狀態</br>(上述項目僅適用於內部部署裝置) |StorSimple Manager 服務 → 裝置 → 維護 |[監視硬體元件](storsimple-monitor-hardware-status.md) |
| 建立支援封裝 |StorSimple Manager 服務 → 裝置 → 維護 |[建立及管理支援封裝](storsimple-create-manage-support-package.md) |
| 安裝軟體更新 |StorSimple Manager 服務 → 裝置 → 維護 |[更新您的裝置](storsimple-update-device.md) |

## <a name="next-steps"></a>後續步驟
如果您遇到任何問題，與您的 StorSimple 裝置 hello 日常作業，或與硬體元件，請參閱：

* [可運作裝置的疑難排解](storsimple-troubleshoot-operational-device.md)
* [使用 StorSimple 監視 LED 指示燈](storsimple-monitoring-indicators.md)

如果您不能解決 hello 問題，而且需要 toocreate 服務要求，請參閱太[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)。

