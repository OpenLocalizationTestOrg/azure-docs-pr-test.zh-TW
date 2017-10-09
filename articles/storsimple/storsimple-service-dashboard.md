---
title: "aaaStorSimple 管理員服務儀表板 |Microsoft 文件"
description: "描述 hello StorSimple Manager 服務儀表板，並說明如何 toouse 它讓 StorSimple 方案 toomonitor hello 健全狀況。"
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>使用 hello StorSimple Manager 服務儀表板
## <a name="overview"></a>概觀
hello StorSimple Manager 服務儀表板頁面會提供所有 hello 的裝置連線的 toohello StorSimple Manager 服務，反白顯示那些需要系統管理員注意的摘要檢視。 本教學課程介紹 hello 儀表板頁面、 說明 hello 儀表板的內容，以及函式，並說明您可以從這個頁面上執行的 hello 工作。

![服務儀表板](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

hello StorSimple Manager 服務儀表板會顯示下列資訊的 hello:

* 在 hello**圖表**區域中，您可以看到您的裝置 hello 相關度量圖表。 您可以檢視 hello 主要儲存體 （本機釘選或階層） 跨所有 hello 裝置，以及以 hello 給裝置使用的一段時間的雲端儲存體使用。 在 hello 右上角的 hello 圖表 toospecify 1 週、 1 個月、 3 個月或 1 年的時間刻度使用 hello 控制項。
* hello**使用量概觀**顯示 hello 佈建並供所有裝置上的所有裝置相對 toohello 可用總儲存體的主要儲存體。 **佈建**是指已備妥並配置供使用，而儲存體的 toohello 數量**用於**檢視 hello 啟動器連接的 toohello 裝置是指 toousage 的磁碟區。
* hello**警示**區域提供所有 hello 作用中警示的快照集上，依警示嚴重性分組的所有 hello 裝置。 按一下 hello 嚴重性層級開啟 hello**警示**頁面上，已設定領域的 tooshow 這些警示。 在 [hello**警示**] 頁面上，您可以按一下個別警示 tooview 詳細有關該警示，包括任何建議的動作。 如果 hello 問題已經解決，您也可以清除 hello 警示。
* hello**作業**區域會提供連接的所有裝置上最近工作的快照 tooyour 服務。 您可以在作業正在進行中，這些失敗 hello 過去 24 小時，使用 toolook 連結或的排程在 hello toorun 未來 24 小時內。
* hello**快速概覽**區域會提供實用資訊，例如服務狀態、 裝置連線的 toohello 服務、 hello 服務位置與 hello 服務相關聯的 hello 訂用帳戶的詳細資料的數目。 另外還有連結 toohello 作業記錄檔。 按一下 hello 連結 toosee 所有已完成的 StorSimple Manager 服務作業的清單。

您可以使用 hello StorSimple Manager 服務儀表板頁面 tooinitiate hello 下列工作：

* 檢視或重新產生 hello 服務註冊金鑰。
* 變更 hello 服務資料加密金鑰。
* 檢視 hello 作業記錄檔。

## <a name="view-or-regenerate-hello-service-registration-key"></a>檢視或重新產生 hello 服務註冊金鑰
hello 服務註冊金鑰是使用的 tooregister hello StorSimple Manager 服務，Microsoft Azure StorSimple 裝置，因此 hello 裝置會出現在 hello Azure 傳統入口網站，供進一步的管理動作。 hello 金鑰 hello 第一個裝置上建立並與您的裝置 hello 其他部分共用。

按一下**登錄機碼**（位於 hello hello 頁面底部） 開啟 hello**服務註冊金鑰**對話方塊中，您可以在其中一個複本 hello 目前服務註冊金鑰 toohello 剪貼簿或重新產生 hello 服務註冊金鑰。

重新產生 hello 金鑰不會影響先前已註冊的裝置： 它會影響只有 hello 後重新產生金鑰 hello 與 hello 服務註冊的裝置。

如需有關檢視和太產生 hello 服務註冊金鑰，請前往[Get hello 服務註冊金鑰](storsimple-manage-service.md#get-the-service-registration-key)。

## <a name="change-hello-service-data-encryption-key"></a>變更 hello 服務資料加密金鑰
服務資料加密金鑰是使用的 tooencrypt 客戶機密資料，例如從 StorSimple Manager 服務 toohello StorSimple 裝置傳送的儲存體帳戶認證。 您將需要 toochange 這些機碼定期如果您的 IT 組織具有 hello 存放裝置金鑰輪動原則。 hello 金鑰變更程序可能會稍有不同，視沒有單一裝置或多個 hello StorSimple Manager 服務所管理的裝置。

變更 hello 服務資料加密金鑰是 3 個步驟程序：

1. 使用 hello Azure 傳統入口網站，授權裝置 toochange hello 服務資料加密金鑰。
2. 使用 Windows PowerShell for StorSimple，起始 hello 服務資料加密金鑰變更。
3. 如果您有多個 StorSimple 裝置，更新其他裝置上 hello hello 服務資料加密金鑰。

hello 下列步驟描述 hello hello 服務資料加密金鑰變換程序。

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>檢視 hello 作業記錄檔
您可以按一下 hello hello 中可用的作業記錄連結，以檢視 hello 作業記錄**快速概覽**hello 儀表板的窗格。 這會帶您 toohello 管理服務 頁面上，您可以在此篩選，並查看 hello 記錄特定 tooyour StorSimple Manager 服務。

## <a name="next-steps"></a>後續步驟
* 了解如何太[StorSimple 裝置排解](storsimple-troubleshoot-operational-device.md)。
* 深入了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

