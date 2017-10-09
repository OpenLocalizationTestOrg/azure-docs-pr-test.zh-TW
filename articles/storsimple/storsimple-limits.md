---
title: "aaaStorSimple 8000 系列系統限制 |Microsoft 文件"
description: "描述 StorSimple 8000 系列元件和連線的系統限制和建議大小。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f21862989f23f2fa4cf02c884cc0fc85c6cc2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>StorSimple 8000 系列的系統有何限制？
## <a name="overview"></a>概觀
StorSimple 提供您的資料中心的擴充性和彈性儲存體。 不過，當您規劃、部署及操作您的 StorSimple 方案時，有一些限制應該謹記在心。 hello 下表描述這些限制，並提供一些建議，讓您可利用您的 StorSimple 解決方案最取得 hello。

| 限制識別碼 | 限制 | 註解 |
| --- | --- | --- |
| 儲存體帳戶認證的數目上限 |64 | |
| 磁碟區容器的數目上限 |64 | |
| 磁碟區的數目上限 |255 | |
| 固定在本機的磁碟區的數目上線 |32 | |
| 每個頻寬範本之排程的數目上限 |168 |Hello 週 (24 * 7) 的每一天，每小時排程。 |
| 實體裝置上之分層磁碟區的大小上限 |64 TB (適用於 8100 和 8600) |8100 和 8600 為實體裝置。 |
| Azure 中的虛擬裝置上之分層磁碟區的大小上限 |30 TB (適用於 8010)  <br></br> 64 TB (適用於 8020) |8010 和 8020 為 Azure 中的虛擬裝置，分別使用了「標準儲存體」和「進階儲存體」。 |
| 實體裝置上之固定在本機的磁碟區的大小上限 |8.5 TB (適用於 8100) <br></br> 22.5 TB (適用於 8600) |8100 和 8600 為實體裝置。 |
| iSCSI 連線的數目上限 |512 | |
| 從起始端之 iSCSI 連線的數目上限 |512 | |
| 每個裝置的存取控制記錄的數目上限 |64 | |
| 每個備份原則的磁碟區數目上限 |20 | |
| 每個排程保留的備份數目上限 (備份原則中) |64 | |
| 每個備份原則的排程數目上限 |10 | |
| 每個磁碟區可以保留之任何類型快照集的數目上限 |256 |此數目包括本機快照和雲端快照。 |
| 可以在任何裝置中呈現的快照集數目上限 |10,000 | |
| 可以針對備份、還原或複製進行平行處理的磁碟區數目上限 |16 |<ul><li>如果有 16 個以上的磁碟區，當有可用的處理插槽時會依序處理它們。</li><li>Hello 作業完成之前，無法進行複製的新備份或還原的階層式磁碟區。 不過，對於本機的磁碟區，備份允許 hello 磁碟區上線後。</li></ul> |
| 分層磁碟區的還原和複製復原時間 |< 2 分鐘 |<ul><li>hello 磁碟區可在還原或複製作業，而不管 hello 磁碟區大小的 2 分鐘內。</li><li>hello 磁碟區效能一開始可能比正常，因為大部分的 hello 資料和中繼資料仍然位於 hello 定域機組中更慢。 為資料流，從 hello 雲端 toohello StorSimple 裝置可能會提高效能。</li><li>hello 總時間 toodownload 中繼資料取決於配置的磁碟區大小的 hello。 中繼資料自動帶入 hello 裝置 hello 背景以 hello 5 分鐘每 TB 的配置的磁碟區資料的速率。 此速率可能受到網際網路頻寬 toohello 雲端。</li><li>hello 還原或複製作業已完成 hello 裝置 hello 的所有中繼資料時。</li><li>無法執行備份作業，直到 hello 還原或複製作業全部完成。 |
| 固定在本機的磁碟區的還原復原時間 |< 2 分鐘 |<ul><li>hello 磁碟區是供 hello 還原作業，而不管 hello 磁碟區大小的 2 分鐘內。</li><li>hello 磁碟區效能一開始可能比正常，因為大部分的 hello 資料和中繼資料仍然位於 hello 定域機組中更慢。 為資料流，從 hello 雲端 toohello StorSimple 裝置可能會提高效能。</li><li>hello 總時間 toodownload 中繼資料取決於配置的磁碟區大小的 hello。 中繼資料自動帶入 hello 裝置 hello 背景以 hello 5 分鐘每 TB 的配置的磁碟區資料的速率。 此速率可能受到網際網路頻寬 toohello 雲端。</li><li>不同分層的磁碟區，本機固定磁碟區，於 hello 磁碟區資料也本機下載 hello 裝置上。 帶 hello 磁碟區的所有資料 toohello 裝置時，hello 還原作業已完成。</li><li>hello 還原作業可能會很長。 hello 總時間 toocomplete hello 還原將取決於 hello hello 佈建本機磁碟區，您的網際網路頻寬和 hello hello 裝置上的現有資料大小。 Hello 還原作業正在進行時允許 hello 固定在本機磁碟區上的備份作業。 |
| 雲端快照集的處理速率 |15 分鐘/TB |<ul><li>最小時間 toomake hello 雲端快照集準備可以上傳，每 TB 的備份中配置的磁碟區資料。 </li><li> 總計的雲端快照集時間計算方式是將這個時間 toohello 快照上傳時間，它會受到 hello 網際網路頻寬 toocloud。 |
| 最大用戶端讀取/寫入輸送量 （當由 hello SSD 層） * |920/720 MB/秒，使用單一 10 GbE 網路介面 |向上 too2x 具有 MPIO 和兩個網路介面。 |
| 最大用戶端讀取/寫入輸送量 （當由 hello HDD 層） * |120/250 MB/秒 | |
| （由提供從 hello 雲端層） 時，最大用戶端讀取/寫入輸送量 * Update 3 及更新版本 * * |分層磁碟區可達到 40/60 MB/s<br><br>磁碟區建立期間選取的封存選項在其中的分層磁碟區可達到 60/80 MB/s |讀取輸送量取決於用戶端產生和維護足夠的 I/O 佇列深度。 <br><br>完成的速度，取決於 hello 速度 hello 使用基礎儲存體帳戶。 |

&#42; 每個 I/O 類型的輸送量最大值的測量方式是使用 100% 讀取和 100% 寫入案例。 實際輸送量可能較低，取決於 I/O 混合和網路狀況。

&#42; &#42;效能數字之前 tooUpdate 3 可能較低。

## <a name="next-steps"></a>後續步驟
檢閱 hello [StorSimple 系統需求](storsimple-system-requirements.md)。 

