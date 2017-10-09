---
title: "aaaStorSimple 本機固定磁碟區常見問題集 |Microsoft 文件"
description: "提供的答案 toofrequently 詢問有關 StorSimple 問題在本機固定磁碟區。"
services: storsimple
documentationcenter: NA
author: manuaery
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/26/2017
ms.author: manuaery
ms.openlocfilehash: a3a6557ca15e7e1947b45dcfd005640103c09591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-locally-pinned-volumes-frequently-asked-questions-faq"></a>StorSimple 本機固定磁碟區︰常見問題集 (FAQ)
## <a name="overview"></a>概觀
hello 如下的問題和解答，當您建立本機固定的 StorSimple 磁碟區時，您可能必須將轉換分層磁碟區 tooa 固定在本機磁碟區 （反之亦然），或備份及還原本機固定磁碟區。

問題和答案分成下列類別目錄的 hello

* 建立本機固定磁碟區
* 備份本機固定磁碟區
* 轉換的階層式磁碟區 tooa 固定在本機磁碟區
* 還原本機固定磁碟區
* 容錯移轉本機固定磁碟區

## <a name="questions-about-creating-a-locally-pinned-volume"></a>有關建立本機固定磁碟區的問題
**問：** Hello 我可以在 hello 8000 系列的裝置建立本機固定磁碟區的大小上限為何？

**A**在裝置上執行 StorSimple 8000 系列 Update 3.0，您可以佈建本機固定磁碟區總 too8.5 TB 或向上 too200 TB hello 8100 裝置上的階層式磁碟區。 您可以在較大 8600 裝置 hello，佈建本機固定磁碟區總 too22.5 TB 或分層的磁碟區總 too500 TB。

**問：** 我最近剛升級我 8100 裝置 tooUpdate 3.0 和 hello 可用的大小上限時 toocreate 本機固定磁碟區，為只有 6 TB 和不 8.5 TB。 為什麼我無法建立 8.5 TB 的磁碟區？

**A**如果您的裝置正在執行更新 3.0，您可以佈建本機固定磁碟區總 too8.5 TB 或分層的磁碟區上 too200 TB 向上 hello 8100 裝置。 如果您的裝置已有分層磁碟區，hello 空間可供建立本機固定磁碟區將會按比例低於此最大限制。 比方說，如果大約 106 TB 分層磁碟區的已佈建 8100 裝置上 （這是一半 hello 階層容量），則會跟著降低的 too4 TB （hello hello 8100 裝置，您可以建立的本機磁碟區的大小上限。大致一半 hello 最多在本機固定磁碟區容量）。

由於某些 hello 裝置上的本機空間是使用的 toohost hello 工作組的階層式磁碟區，就會降低 hello 建立本機固定磁碟區的可用空間，如果 hello 裝置具有分層磁碟區。 相反地，建立本機固定磁碟區按比例減少 hello 階層式磁碟區的可用空間。 hello 下表摘要說明 hello 可用分層式的容量 hello 8100 和 8600 裝置上，建立本機固定磁碟區時。

#### <a name="update-30"></a>Update 3.0 
| 本機固定磁碟區佈建的容量 | 佈建階層式磁碟區-8100 的可用容量 toobe | 佈建階層式磁碟區-8600 的可用容量 toobe |
| --- | --- | --- |
| 0 |200 TB |500 TB |
| 1 TB |176.5 TB |477.8 TB |
| 4 TB |105.9 TB |411.1 TB |
| 8.5 TB |0 TB |311.1 TB |
| 10 TB |NA |277.8 TB |
| 15 TB |NA |166.7 TB |
| 22.5 TB |NA |0 TB |

**問：** 為什麼建立本機固定磁碟區是長時間執行的作業？

**答：** 已密集佈建本機固定磁碟區。 toocreate 空間 hello hello 裝置的本機層、 某些資料，從現有的階層式磁碟區可能會在 hello 佈建程序期間推送 toohello 雲端。 因為這取決於 hello hello 磁碟區正在佈建 hello 您裝置和 hello 可用的頻寬 toohello 雲端上的現有資料大小 hello 花費的時間 toocreate 本機磁碟區可能是幾個小時。

**問：** 多久花費 toocreate 本機固定磁碟區？

**答：** 由於本機固定磁碟區會以佈建，某些現有的資料，從分層磁碟區可能會被 toohello 雲端期間 hello 佈建程序。 因此，多因素，包括 hello hello 磁碟區的大小，取決於本機固定磁碟區的 hello 所花費時間 toocreate hello 裝置上的資料，而且 hello 可用的頻寬。 沒有磁碟區的全新安裝裝置，hello 時間 toocreate 本機固定磁碟區是約 10 分鐘每 tb 的資料。 不過，建立本機磁碟區可能需要數小時，根據上述說明正在使用中的裝置上的 hello 因素。

**問：** 我想 toocreate 本機固定磁碟區。 是否有任何我需要留意 toobe 的最佳作法？

**答：** 需要資料一直位於本機保證，而且是機密 toocloud 延遲的工作負載適用的本機固定磁碟區。 同時考慮到任何工作負載的本機磁碟區的使用方式，請留意下列 hello:

* 本機固定磁碟區會以佈建，並建立本機磁碟區會影響 hello 階層式磁碟區的可用空間。 因此，我們建議您一開始使用較小的磁碟區，並隨著您的儲存體需求增加來相應增加。
* 本機磁碟區的佈建是長時間執行的作業可能會牽涉到將分層磁碟區 toohello 雲端推入現有的資料。 因此，您可能會遇到這些磁碟區的效能降低。
* 佈建本機磁碟區是耗時的作業。 hello 所涉及的實際時間取決於多個因素： hello 的 hello 正在佈建的磁碟區，您的裝置，並可用的頻寬上的資料大小。 如果您未備份您現有的磁碟區 toohello 雲端、 建立磁碟區則速度較慢。 我們建議您在佈建本機磁碟區之前，製作現有磁碟區的雲端快照。
* 您可以轉換現有的階層式磁碟區 toolocally 固定磁碟區，這項轉換牽涉到佈建的 hello 造成本機固定磁碟區 （在加法 toobringing 關閉階層式資料，如果有的話，從 hello 雲端) 中的 hello 裝置上的空間。 這同樣是取決於上述因素的長時間執行作業。 我們建議將 hello 程序將會更慢，如果現有的磁碟區不會備份備份您現有的磁碟區之前 tooconversion。 您的裝置也可能在此程序中遇到效能降低。

詳細資訊太[建立本機固定磁碟區](storsimple-8000-manage-volumes-u2.md#add-a-volume)

**問：** 可以建立多個本機固定磁碟區在 hello 相同的時間？

**答：** 可以，但會循序處理所有固定在本機之磁碟區的建立和擴充作業。

本機固定磁碟區會以佈建，而且這需要建立 hello 裝置 （這可能會導致現有的資料，從分層磁碟區 toobe 推送 toohello 雲端 hello 佈建程序期間） 上的本機空間。 因此，如果佈建作業正在進行中，其他本機磁碟區建立作業就會排入佇列，直到該作業完成為止。

同樣地，如果正在擴充現有的本機磁碟區，或是正在轉換為分層磁碟區 tooa 本機固定磁碟區，然後 hello 建立新的本機固定磁碟區會進入佇列，直到 hello 先前的工作完成。 展開 hello 本機固定磁碟區的大小，牽涉到 hello 擴充 hello 現有本機的磁碟區的空間。 從階層式的 toolocally 固定磁碟區的轉換也牽涉到 hello 建立 hello 造成本機固定磁碟區的本機空間。 在這兩項作業中，建立或擴充本機空間都是長時間執行的作業。

您可以檢視這些作業在 hello**作業**刀鋒視窗中的 hello StorSimple 裝置管理員服務。 hello 主動處理的作業會持續更新 tooreflect hello 進度的佈建的空間。 hello 剩餘本機固定磁碟區的工作會標示為正在執行，但是其進度而停止，而且他們他們已排入佇列的 hello 順序中挑選。

**問：** 我刪除了本機固定磁碟區。 為什麼看 hello 回收空間會反映在 hello 可用空間當我嘗試 toocreate 新的磁碟區？

**答：** 如果您刪除本機固定磁碟區，可能不會立即更新 hello 空間供新磁碟區。 hello StorSimple 裝置管理員服務在約每小時更新 hello 可用的本機空間。 我們建議您等待一小時，然後再試 toocreate hello 新磁碟區。

**問：** Hello 雲端應用裝置上是否支援本機固定磁碟區？

**答：** Hello 雲端應用裝置 （8010 和 8020 裝置先前參考的 tooas hello StorSimple 虛擬裝置） 上不支援本機固定磁碟區。

**問：** 我可以使用 hello Azure PowerShell cmdlet toocreate 和管理本機固定磁碟區嗎？

**答：** 不可以，您無法透過 Azure PowerShell Cmdlet 建立固定在本機的磁碟區 (任何透過 Azure PowerShell 建立的磁碟區都是分層磁碟區)。 我們也建議您不要使用 hello Azure PowerShell cmdlet toomodify 任何屬性的本機固定磁碟區，它將 hello 修改 hello 磁碟區類型 tootiered 的不良的影響。

## <a name="questions-about-backing-up-a-locally-pinned-volume"></a>有關備份本機固定磁碟區的問題
**問：** 是否支援本機固定磁碟區的本機快照？

**答：** 是，您可以製作本機固定磁碟區的本機快照。 不過，我們強烈建議您定期備份您的本機固定磁碟區與您的資料保護的雲端快照集 tooensure hello 損毀的可能性。

請注意，本機固定磁碟區的本機快照集也可以出 toohello 雲端層，並不保證 toostay hello 的 hello 裝置的本機層中。

**問：** 是否有任何指導方針可管理本機固定磁碟區的本機快照？

**答：** 頻繁的本機快照與較高的 hello 本機固定磁碟區可能會導致本機空間快速耗盡 hello 裝置 toobe 上，並會導致資料從發送 toohello 雲端的階層式磁碟區中的資料變換率。 因此建議您降低本機快照集的 hello 數目。

**問：** 我收到警示指出本機固定磁碟區的本機快照可能失效。 何時會發生這種情形？

**答：** 頻繁的本機快照與較高的 hello 本機固定磁碟區可能會導致本機空間快速耗盡 hello 裝置 toobe 中的資料變換率。 如果 hello 本機層的 hello 裝置的使用率，擴充的雲端中斷可能會導致 hello 裝置填滿，並傳入寫入 toohello 磁碟區可能會導致失效的 hello 快照集 （如有 tooupdate hello 快照 toorefer 沒有空間。toohello 較舊的資料區塊的已覆寫）。 在這種情況下 hello toobe 提供，但 hello 本機快照可能無效，會繼續寫入 toohello 磁碟區。 沒有影響 tooyour 現有雲端快照。

hello 警示警告是，這種情況發生即可確保處理的 hello 相同及時藉由檢閱您的本機快照排程 tootake 較不頻繁的本機快照或刪除較舊的本機快照不再 toonotify必要項。

如果 hello 本機快照集失效，您會收到通知您，已經失效 hello hello 特定的備份原則的本機快照集失效的 hello 本機快照集的時間戳記的 hello 清單旁的資訊警示。 這些快照會自動刪除，您將不再能夠 tooview 中 hello**備份目錄**hello Azure 入口網站中的刀鋒視窗。

## <a name="questions-about-converting-a-tiered-volume-tooa-locally-pinned-volume"></a>關於轉換分層磁碟區 tooa 固定在本機磁碟區的問題
**問：** 我觀察 hello 裝置上的某些緩慢轉換的階層式磁碟區 tooa 固定在本機磁碟區時。 為什麼會發生這種情形？

**答：** hello 轉換程序包含兩個步驟：

1. 佈建的 hello 的 hello 裝置上的空間即將-到--轉換固定在本機磁碟區。
2. 從 hello 雲端 tooensure 本機下載任何階層式的資料的保證。

兩個步驟是長時間執行的 hello hello 磁碟區正在轉換 hello 裝置和可用的頻寬資料大小而定的作業。 某些資料，從現有的階層式磁碟區可能會溢出 toohello 雲端 hello 佈建程序的一部分，您的裝置可能會發生在這段期間的效能降低。 此外，hello 轉換程序可能會變慢如果：

* 現有的磁碟區尚未被備份 toohello 雲端;因此我們建議您備份您的磁碟區之前 tooinitiating 轉換。
* 頻寬節流原則已套用，這可能會受到限制 hello 可用的頻寬 toohello 雲端;因此，建議您有專用的 40 Mbps 或更多連接 toohello 雲端。
* hello 轉換程序可能需要數小時的時間到期，前文所; toohello 多因素因此，我們建議您執行這項作業在非尖峰時間或週末 tooavoid hello 結束取用者的影響。

詳細資訊太[分層磁碟區 tooa 固定在本機磁碟區轉換](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)

**問：** 可以取消 hello 磁碟區轉換作業嗎？

**答：** 否，您無法 hello 取消 hello 轉換作業一經啟動。 中所述 hello 前一個問題，請留意 hello 的潛在效能問題您可能會遇到在 hello 過程中，並遵循 hello 規劃轉換時，上面所列的最佳作法。

**問：** 如果 hello 轉換作業會失敗，怎樣 toomy 磁碟區？

**答：** 磁碟區轉換可能會 toocloud 連線問題而失敗。 hello 裝置最後可能會停止 hello 轉換程序之後一系列的不成功的嘗試 toobring 向 hello 雲端的階層式資料。 在此案例中，hello 磁碟區類型會繼續 toobe hello 來源磁碟區類型先前 tooconversion，和：

* 重大警示將會引發的 toonotify 您 hello 磁碟區轉換失敗。 更多有關[警示相關的 toolocally 固定磁碟區](storsimple-8000-manage-alerts.md#locally-pinned-volume-alerts)
* 如果您想要轉換的分層式的 tooa 固定在本機磁碟區，hello 磁碟區將會繼續 tooexhibit 屬性的階層式磁碟區，因為資料可能仍位於 hello 雲端。 我們建議您解決 hello 連線問題，然後再重試 hello 轉換作業。
* 同樣地，當轉換從本機固定 tooa 分層磁碟區失敗，雖然 hello 磁碟區將會標示為本機固定磁碟區，它將做為分層磁碟區 （因為資料可能已溢出 toohello 雲端）。 不過，它會繼續 hello 裝置 hello 本機層上的 toooccupy 空間。 此空間無法用於其他本機固定磁碟區。 我們建議您重試此作業 tooensure hello 磁碟區轉換已完成，而且可以回收 hello hello 裝置上的本機空間。

## <a name="questions-about-restoring-a-locally-pinned-volume"></a>有關還原本機固定磁碟區的問題
**問：** 是否會立即還原本機固定磁碟區？

**答：** 是，會立即還原本機固定磁碟區。 Hello hello 磁碟區的中繼資料資訊取自 hello 雲端 hello 還原作業的一部分，如 hello 磁碟區上線，並可供 hello 主機存取。 不過，本機保證 hello 磁碟區資料將不會存在，直到從 hello 雲端已下載所有的 hello 資料，而且您可能會遇到效能降低的這些磁碟區上 hello 還原 hello 持續時間內。

**問：** 多久花費 toorestore 本機固定磁碟區？

**答：** 本機固定磁碟區會立即還原，而且只要 hello 磁碟區中繼資料資訊會從 hello 雲端，同時在 hello 背景中下載 toobe hello 磁碟區資料仍繼續，請回到線上。 Hello 還原作業-hello 磁碟區資料--取得回 hello 本機保證此第二個部分是長時間執行的作業，且可能需要幾個小時一次進行本機所有 hello 資料 toobe。 hello 所花費時間 toocomplete hello 相同，取決於多個因素，例如 hello hello 正在還原的磁碟區的大小且 hello 可用的頻寬。 如果正在還原的 hello 原始磁碟區已遭刪除，額外的時間將會進入 toocreate hello 本機裝置上的空間 hello hello 還原作業的一部分。

**問：** 我需要的 toorestore 現有本機固定磁碟區 tooan 較舊的快照 （採取 hello 磁碟區已層）。 將為階層在此情況下會還原 hello 磁碟區嗎？

**答：** 否，hello 磁碟區將會還原為本機固定磁碟區。 雖然 hello 快照集時 hello 磁碟區階層式，還原現有的磁碟區時的日期 toohello 時間 StorSimple 一律會使用磁碟區的 hello 類型 hello 磁碟上目前存在。

**問：** 我不久，延伸我的本機固定磁碟區，但我現在需要 toorestore hello 資料 tooa 時間 hello 磁碟區的大小較小。 會還原重新調整 hello 目前的磁碟區，我必須 tooextend hello hello 磁碟區的大小一旦 hello 還原完成？

**答：** 是，hello 還原會重新調整 hello 磁碟區，且 hello 還原完成之後，您將需要 tooextend hello hello 磁碟區的大小。

**問：** 可以在還原期間變更磁碟區的 hello 的類型嗎？

**A.**否，您無法在還原期間變更 hello 磁碟區類型。

* 已刪除的磁碟區會還原為儲存在 hello 快照中的 hello 類型。
* 根據目前的類型，而不儲存在 hello 快照中的 hello 類型受限於還原現有的磁碟區 （請參閱 toohello 前兩個問題）。

**問：** 我需要 toorestore 我的本機固定磁碟區，但我時間快照中挑選正確的點。 可以取消 hello 目前的還原作業嗎？

**答：** 是，您可以取消進行中的還原作業。 hello hello 磁碟區狀態將會回復 toohello 狀態在 hello 還原 hello 開頭。 不過，任何 hello 還原正在進行中時，所做 toohello 磁碟區的寫入將會遺失。

**問：** 我已開始在其中一個本機固定磁碟區上進行還原作業，而目前在待處理項目目錄中看到我未重新建立的快照。 這有何用途？

**答：** 這是建立先前 toohello 還原作業和以防 hello 還原已遭取消或失敗，可用於復原的 hello 暫時快照集。 請勿刪除此快照集;它會自動予以刪除 hello 還原已完成。 如果還原作業僅有固定在本機的磁碟區或是混合了固定在本機的磁碟區與分層磁碟區，就可能就會發生此問題。 如果 hello 還原工作包含只有分層磁碟區，將不會發生這個問題。

**問：** 是否可以複製本機固定磁碟區？

**答：** 是，您可以這麼做。 不過，hello 固定在本機磁碟區將做為分層磁碟區複製，根據預設。 詳細資訊太[複製本機固定磁碟區](storsimple-8000-clone-volume-u2.md)

## <a name="questions-about-failing-over-a-locally-pinned-volume"></a>有關容錯移轉本機固定磁碟區的問題
**問：** 我需要 toofail 透過裝置 tooanother 實體裝置。 我的本機固定磁碟區將會容錯移轉為本機固定或階層式磁碟區？

**答：** hello 固定在本機磁碟區已容錯移轉為本機固定如果 hello 目標裝置正在執行 StorSimple 8000 系列 update 3 或更高版本。

[跨越版本的本機固定磁碟區容錯移轉和 DR](storsimple-8000-device-failover-disaster-recovery.md#device-failover-across-software-versions)

**問：** 本機固定磁碟區是否會在災害復原 (DR) 期間立即還原？

**答：** 是，在容錯移轉會立即還原本機固定磁碟區。 Hello hello 磁碟區的中繼資料資訊取自 hello 雲端 hello 容錯移轉作業的一部分，因為 hello 磁碟區上線 hello 目標裝置上，並供 hello 主機可以存取。 同時，hello 磁碟區資料仍 toodownload hello 背景，而且您可能會遇到這些磁碟區上的位置 hello hello 容錯移轉期間效能降低。

**問：** 我看到 hello 容錯移轉作業已完成，如何追蹤正在還原的本機固定磁碟區的 hello 進度 hello 目標裝置上嗎？

**答：** 在容錯移轉作業時，hello 容錯移轉工作標示為完成後 hello 容錯移轉設定中的所有 hello 磁碟區必須立即還原並上線 hello 目標裝置上。 這包括任何本機固定磁碟區可能會失敗。不過，本機保證的 hello 資料只能使用已下載所有 hello 資料 hello 磁碟區時。 您可以追蹤每個本機固定磁碟區已容錯移轉監視 hello 對應還原作業所建立 hello 容錯移轉的一部分處理。 這些個別的還原作業只會針對本機固定磁碟區建立。

**問：** 可以在容錯移轉期間變更磁碟區的 hello 的類型嗎？

**答：** 否，您無法在容錯移轉期間變更 hello 磁碟區類型。 如果您容錯透過 tooanother 實體裝置執行 StorSimple 8000 系列 update 3，hello 磁碟區已容錯移轉 hello hello 快照中儲存的磁碟區類型為基礎。

**問：** 可以容錯與本機固定磁碟區 toohello 雲端應用裝置磁碟區容器？

**答：** 是，您可以這麼做。 hello 固定在本機磁碟區的容錯移轉與分層磁碟區。 [跨越版本的本機固定磁碟區容錯移轉和 DR](storsimple-8000-device-failover-disaster-recovery.md#common-considerations-for-device-failover)

