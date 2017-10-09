---
title: "裝置管理員服務管理 aaaStorSimple |Microsoft 文件"
description: "了解如何使用您的 StorSimple 裝置 hello StorSimple 裝置管理員中的服務 toomanage hello Azure 入口網站。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: alkohli
ms.openlocfilehash: d73dc32bd39b2c832d5c4a5edda32a2e7f55a503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-device"></a>使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister

## <a name="overview"></a>概觀

本文說明 hello StorSimple 裝置管理員服務介面，包括如何 tooconnect tooit hello 各種可用的選項，以及連結時，可以透過此 UI 執行的 toohello 特定工作流程。 本指南是適用 tooboth;hello StorSimple 實體裝置和 hello 雲端應用裝置。

閱讀本文知後，您將了解：

* 連線 tooStorSimple 裝置管理員服務
* 管理您的 StorSimple 裝置透過 hello StorSimple 裝置管理員服務

## <a name="connect-toostorsimple-device-manager-service"></a>連線 tooStorSimple 裝置管理員服務

hello StorSimple 裝置管理員服務在 Microsoft Azure 中執行，並連接 toomultiple StorSimple 裝置。 您使用管理中心的 Microsoft Azure 入口網站，在瀏覽器 toomanage 執行這些裝置。 tooconnect toohello StorSimple 裝置管理員服務，請勿 hello 遵循。

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello 服務
1. 瀏覽過[https://portal.azure.com/](https://portal.azure.com/)。
2. 使用您的 Microsoft 帳戶認證，登入 toohello Microsoft Azure 入口網站 （位於 hello 的右上方 hello 窗格）。
3. 捲動左導覽窗格 tooaccess hello StorSimple 裝置管理員服務的 hello。


## <a name="administer-storsimple-device-using-storsimple-device-manager-service"></a>使用 StorSimple 裝置管理員服務管理 StorSimple 裝置

hello 下表顯示之所有 hello 常見管理工作和複雜工作流程可以在 hello StorSimple 裝置管理員服務 UI 內執行的摘要。 這些工作被組織根據 hello UI 刀鋒視窗啟動它們。

如需有關每個工作流程的詳細資訊，請按一下 hello hello 資料表中的適當程序。

#### <a name="storsimple-device-manager-workflows"></a>StorSimple 裝置管理員工作流程

| 如果您希望 toodo 如此... | 使用此程序。 |
| --- | --- |
| 建立服務</br>刪除服務</br>取得服務註冊金鑰</br>重新產生服務註冊金鑰 |[部署 StorSimple 裝置管理員服務](storsimple-8000-manage-service.md) |
| 檢視 hello 活動記錄檔 |[使用摘要的 hello StorSimple 裝置管理員服務](storsimple-8000-service-dashboard.md) |
| 變更 hello 服務資料加密金鑰</br>檢視 hello 作業記錄檔 |[使用 hello StorSimple 裝置管理員服務儀表板](storsimple-8000-service-dashboard.md) |
| 停用裝置</br>刪除裝置 |[停用或刪除裝置](storsimple-8000-deactivate-and-delete-device.md) |
| 了解災害復原和裝置容錯移轉</br>容錯移轉 tooa 實體裝置</br>容錯移轉 tooa 虛擬裝置</br>業務持續性災害復原 (BCDR) |[StorSimple 裝置的容錯移轉與災害復原](storsimple-8000-device-failover-disaster-recovery.md) |
| 列出磁碟區備份</br>選取備份組</br>刪除備份組 |[管理備份](storsimple-8000-manage-backup-catalog.md) |
| 複製磁碟區 |[複製磁碟區](storsimple-8000-clone-volume-u2.md) |
| 還原備份組 |[還原備份組](storsimple-8000-restore-from-backup-set-u2.md) |
| 有關儲存體帳戶</br>新增儲存體帳戶</br>編輯儲存體帳戶</br>刪除儲存體帳戶</br>替換儲存體帳戶的金鑰 |[管理儲存體帳戶](storsimple-8000-manage-storage-accounts.md) |
| 關於頻寬範本</br>新增頻寬範本</br>編輯頻寬範本</br>刪除頻寬範本</br>使用預設頻寬範本</br>建立在指定時間啟動的全天頻寬範本 |[管理頻寬範本](storsimple-8000-manage-bandwidth-templates.md) |
| 關於存取控制記錄</br>建立存取控制記錄</br>編輯存取控制記錄</br>刪除存取控制記錄 |[管理存取控制記錄](storsimple-8000-manage-acrs.md) |
| 檢視工作詳細資料</br>取消工作 |[管理工作](storsimple-8000-manage-jobs-u2.md) |
| 接收警示通知</br>管理警示</br>檢閱警示 |[檢視和管理 StorSimple 警示](storsimple-8000-manage-alerts.md) |
| 建立監視圖表 |[監視您的 StorSimple 裝置](storsimple-monitor-device.md) |
| 新增磁碟區容器</br>修改磁碟區容器</br>刪除磁碟區容器 |[管理磁碟區容器](storsimple-8000-manage-volume-containers.md) |
| 新增磁碟區</br>修改磁碟區</br>使磁碟區離線</br>刪除磁碟區</br>監視磁碟區 |[管理磁碟區](storsimple-8000-manage-volumes-u2.md) |
| 修改裝置設定</br>修改時間設定</br>修改 DNS.md 設定</br>設定網路介面 |[修改 StorSimple 裝置的裝置組態](storsimple-8000-modify-device-config.md) |
| 檢視 Web Proxy 設定 |[設定裝置的 Web Proxy](storsimple-8000-configure-web-proxy.md) |
| 修改裝置系統管理員密碼</br>修改 StorSimple Snapshot Manager 密碼 |[變更 StorSimple 密碼](storsimple-8000-change-passwords.md) |
| 設定遠端管理 |[從遠端連線 tooyour StorSimple 裝置](storsimple-8000-remote-connect.md) |
| 設定警示設定 |[檢視和管理 StorSimple 警示](storsimple-8000-manage-alerts.md) |
| 為 StorSimple 裝置設定 CHAP |[為 StorSimple 裝置設定 CHAP](storsimple-configure-chap.md) |
| 新增備份原則</br>新增或修改排程</br>刪除備份原則</br>進行手動備份</br>建立具有多個磁碟區和排程的自訂備份原則 |[管理備份原則](storsimple-8000-manage-backup-policies-u2.md) |
| 停止裝置控制器</br>重新啟動裝置控制器</br>關閉裝置控制器</br>重設您的裝置 toofactory 預設值</br>(上述項目僅適用於內部部署裝置) |[管理 StorSimple 裝置控制器](storsimple-8000-manage-device-controller.md) |
| 了解 StorSimple 硬體元件</br>監視硬體狀態</br>(上述項目僅適用於內部部署裝置) |[監視硬體元件](storsimple-8000-monitor-hardware-status.md) |
| 建立支援封裝 |[建立及管理支援封裝](storsimple-8000-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple) |
| 安裝軟體更新 |[更新您的裝置](storsimple-update-device.md) |

## <a name="next-steps"></a>後續步驟

如果您遇到任何問題，與您的 StorSimple 裝置 hello 日常作業，或與硬體元件，請參閱：

* [使用 hello 診斷工具進行疑難排解](storsimple-8000-diagnostics.md)
* [使用 StorSimple 監視 LED 指示燈](storsimple-monitoring-indicators.md)

如果您不能解決 hello 問題，而且需要 toocreate 服務要求，請參閱太[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)。

