---
title: "aaaStorSimple 虛擬陣列 web UI 管理 |Microsoft 文件"
description: "描述如何 tooperform 基本裝置系統管理工作透過 hello StorSimple Virtual Array web UI。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>使用您的 StorSimple Virtual Array hello Web UI tooadminister
![安裝程序流程](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>概觀
這篇文章中的 hello 教學課程適用於 toohello Microsoft Azure StorSimple Virtual Array （也稱為 hello StorSimple 內部部署虛擬裝置） 執行 2016 年 3 月公開上市 (GA) 版本。 本文說明某些 hello 複雜工作流程及管理工作可以在 hello StorSimple Virtual Array 執行。 您可以管理 hello StorSimple Virtual Array 使用 hello StorSimple Manager 服務 UI （參考的 tooas hello 入口網站 UI） 和 hello hello 裝置的本機 web UI。 本文著重在 hello 工作，您可以使用執行 hello web UI。

這篇文章包含下列教學課程的 hello:

* 取得 hello 服務資料加密金鑰
* 疑難排解 Web UI 安裝程式錯誤
* 產生記錄檔封裝
* 關閉或重新啟動您的裝置

## <a name="get-hello-service-data-encryption-key"></a>取得 hello 服務資料加密金鑰
當您以 hello StorSimple Manager 服務註冊第一個裝置時，會產生服務資料加密金鑰。 這個索引鍵是所需要的 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple Manager 服務。

如果您有錯置的服務資料加密金鑰，需要 tooretrieve，執行 hello 下列步驟在 hello 本機 web UI hello 裝置註冊服務。

#### <a name="tooget-hello-service-data-encryption-key"></a>tooget hello 服務資料加密金鑰
1. 連接 toohello 本機 web UI。 跳過**組態** > **雲端設定**。
2. 在 hello hello 頁面底部，按一下**Get 的服務資料加密金鑰**。 金鑰將會顯示。 複製並儲存此金鑰。
   
    ![取得服務資料加密金鑰 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>疑難排解 Web UI 安裝程式錯誤
在某些情況下當您設定 hello 裝置透過 hello 本機 web UI，您可能會遇到錯誤。 toodiagnose 和疑難排解這類錯誤，您可以執行 hello 診斷測試。

#### <a name="toorun-hello-diagnostic-tests"></a>toorun hello 診斷測試
1. 在本機 web UI hello，移過**疑難排解** > **診斷測試**。
   
    ![執行診斷 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. 在 hello hello 頁面底部，按一下**執行診斷測試**。 這會起始測試 toodiagnose 任何可能與您的網路、 裝置、 web proxy、 時間或雲端設定的問題。 系統會通知您該 hello 裝置正在執行測試。
3. Hello 測試都已完成之後，將會顯示 hello 結果。 hello 下列範例顯示 hello 診斷測試結果。 請注意，hello web proxy 設定未設定此裝置，因此，無法執行 hello web proxy 測試。 所有 hello 其他測試網路設定，DNS 伺服器，以及時間設定成功。
   
    ![執行診斷 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>產生記錄檔封裝
記錄檔套件包含所有 hello 相關記錄，有助於協助 Microsoft 支援服務，任何裝置的問題進行疑難排解。 在此版本中，可以透過 hello 本機 web UI 產生記錄檔套件。

#### <a name="toogenerate-hello-log-package"></a>toogenerate hello 記錄封裝
1. 在本機 web UI hello，移過**疑難排解** > **系統記錄檔**。
   
    ![產生記錄檔封裝 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. 在 hello hello 頁面底部，按一下**建立記錄檔套件**。 將建立 hello 系統記錄檔的封裝。 這需要幾分鐘的時間。
   
    ![產生記錄檔封裝 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    已成功建立 hello 封裝，並 tooindicate hello 時間和日期建立 hello 封裝時，將會更新 hello 頁面之後，系統會通知您。
   
    ![產生記錄檔封裝 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. 按一下 [下載記錄檔封裝] 。 壓縮的封裝將會下載到您的系統上。
   
    ![產生記錄檔封裝 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. 您可以解壓縮 hello 下載記錄檔的封裝，並檢視 hello 系統記錄檔。

## <a name="shut-down-and-restart-your-device"></a>關閉並重新啟動您的裝置
您可以關閉或重新啟動虛擬裝置 hello 本機 web UI。 我們建議，再重新啟動、 hello 主機上讓 hello 磁碟區或共用離線再 hello 裝置。 這樣可以讓資料損毀的可能性降至最低。 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut 向您的虛擬裝置
1. 在本機 web UI hello，移過**維護** > **電源設定**。
2. 在 hello hello 頁面底部，按一下**關機**。
   
    ![裝置關閉 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. 會出現警告，指出關機的 hello 裝置將會中斷已在進行中，進入停機狀態造成任何 IO。 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)。
   
    ![裝置關閉警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    系統會通知您已起始 hello 關閉。
   
    ![已開始關閉裝置](./media/storsimple-ova-web-ui-admin/image38.png)
   
    hello 裝置會立即關閉。 如果您想 toostart 您的裝置，您需要 toodo，透過 hello HYPER-V 管理員。

#### <a name="toorestart-your-virtual-device"></a>toorestart 虛擬裝置
1. 在本機 web UI hello，移過**維護** > **電源設定**。
2. 在 hello hello 頁面底部，按一下**重新啟動**。
   
    ![裝置重新啟動](./media/storsimple-ova-web-ui-admin/image36.png)
3. 會出現警告，指出該重新啟動的 hello 裝置將會中斷已在進行中，導致停機所有 IOs。 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-ova-web-ui-admin/image3.png)。
   
    ![重新啟動警告](./media/storsimple-ova-web-ui-admin/image37.png)
   
    系統會通知您已起始 hello 重新啟動。
   
    ![已起始重新啟動](./media/storsimple-ova-web-ui-admin/image39.png)
   
    在進行 hello 重新啟動時，您將會遺失 hello 連接 toohello UI。 您可以透過定期重新整理 hello UI 監視 hello 重新啟動。 或者，您可以監視透過 HYPER-V 管理員 hello hello 裝置重新啟動狀態。

## <a name="next-steps"></a>後續步驟
了解如何太[使用 hello StorSimple Manager 服務 toomanage 裝置](storsimple-virtual-array-manager-service-administration.md)。

