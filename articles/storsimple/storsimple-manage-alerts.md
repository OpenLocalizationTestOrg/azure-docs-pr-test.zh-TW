---
title: "aaaView 及管理 StorSimple 警示 |Microsoft 文件"
description: "描述 StorSimple 警示的條件和嚴重性、 如何 tooconfigure 警示通知，以及如何 toouse hello StorSimple Manager 服務 toomanage 警示。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bee49253-9ac7-4131-95f6-6bf0e72b8438
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: anbacker
ms.openlocfilehash: d322c88b565606538a3acb61ff939ec1fbe2f3cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-alerts"></a>使用 hello StorSimple Manager 服務 tooview 及管理 StorSimple 警示
## <a name="overview"></a>概觀
hello**警示**hello StorSimple Manager 服務中的索引標籤的方式為您提供 tooreview 和清除 StorSimple 裝置相關警示即時的方式。 從這個索引標籤中，您可以集中監視 hello 的 StorSimple 裝置的健全狀況問題和 hello 整體的 Microsoft Azure StorSimple 解決方案。

本教學課程描述常見的警示條件、 警示的嚴重性層級，以及如何 tooconfigure 警示通知。 此外，它會包括警示快速參考資料表，可讓您 tooquickly 找出特定的警示，並適當地回應。

![警示頁面](./media/storsimple-manage-alerts/HCS_AlertsPage.png)

## <a name="common-alert-conditions"></a>常見的警示狀況
您的 StorSimple 裝置回應 tooa 各種情況中，會產生警示。 hello 如下 hello 最常見的警示條件類型：

* **硬體問題**– 這些警示會告知您有關 hello 健康情況的硬體。 它們讓您知道是否需要升級韌體、網路介面是否有問題，或您的其中一個資料磁碟機是否有問題。
* **連線問題** – 當傳送資料有困難時會發生這些警示。 通訊可能會發生問題的資料 tooand 傳輸期間從 hello Azure 儲存體帳戶或到期 toolack hello 裝置與 hello StorSimple Manager 服務之間的連線。 通訊問題是一些 hello 最複雜 toofix 因為有太多失敗點。 您應該一律先網路連線和網際網路存取可用之前先確認 toomore 上繼續進行進階疑難排解。 疑難排解說明，請跳過[hello Test-connection cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md)。
* **效能問題** – 當系統未以最佳方式運作時，例如負荷過重，就會造成這些警示。

此外，您可能會看到警示相關的 toosecurity、 更新或工作失敗。

## <a name="alert-severity-levels"></a>警示嚴重性層級
警示有不同的嚴重性層級，視 hello 的 hello 影響而定，警示的情況下會有並 hello 回應 toohello 警示需要。 hello 嚴重性層級為：

* **重大**– 此警示會回應 tooa 條件影響 hello 成功的效能，您的系統中。 動作是必要的 tooensure hello StorSimple 服務沒有被中斷。
* **警告** – 此狀況如果不解決，可能會演變成重大狀況。 您應該調查 hello 狀況並採取任何必要動作 tooclear hello 問題。
* **資訊** – 此警示包含適用於追蹤和管理系統的資訊。

## <a name="configure-alert-settings"></a>設定警示設定
您可以選擇是否要讓 toobe 收到警示的條件，每個您 StorSimple 裝置的電子郵件通知。 此外，您可以識別其他警示通知收件者電子郵件地址輸入 hello**其他電子郵件收件者** 方塊中，並以分號分隔。

> [!NOTE]
> 您可以對每一裝置輸入最多 20 個電子郵件地址。
> 
> 

啟用裝置的電子郵件通知後，hello 通知清單的成員會收到電子郵件訊息，每次發生嚴重的警示時。 會將傳送 hello 訊息 *storsimple-alerts-noreply@mail.windowsazure.com*  ，並將說明 hello 警示條件。 收件者可以按一下**Unsubscribe** tooremove 本身從 hello 電子郵件通知清單。

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>tooenable 之裝置的警示的電子郵件通知
1. 跳過**裝置** > **設定**hello 裝置。
2. 在下**警示設定**，hello 下列設定：
   
   1. 在 hello**傳送電子郵件通知**欄位中，選取**是**。
   2. 在 hello**電子郵件服務系統管理員**欄位中，選取**是**如果您想 toohave hello 服務系統管理員，而且所有的共同管理員收到 hello 警示通知。
   3. 在 hello**其他電子郵件收件者**欄位中，輸入 hello 的所有其他收件者應該會收到 hello 警示通知的電子郵件地址。 輸入名稱，格式為 hello  *someone@somewhere.com* 。使用分號 tooseparate hello 電子郵件地址。 您可以對每一裝置設定最多 20 個電子郵件地址。 
      
       ![警示通知設定](./media/storsimple-manage-alerts/AlertNotify.png)
3. toosend 測試電子郵件通知，按一下 hello 箭號圖示下一步太**傳送測試電子郵件**。 hello StorSimple Manager 服務將會顯示狀態訊息轉送 hello 測試通知。 
4. Hello 下列訊息出現時，按一下**確定**。 
   
    ![已傳送警示測試通知電子郵件](./media/storsimple-manage-alerts/HCS_AlertNotificationConfig3.png)
   
   > [!NOTE]
   > 如果 hello 無法傳送測試通知訊息，hello StorSimple Manager 服務將會顯示適當的訊息。 按一下**確定**，稍候幾分鐘，然後再試 toosend 測試通知訊息。 
   > 
   > 

## <a name="view-and-track-alerts"></a>檢視和追蹤警示
hello StorSimple Manager 服務儀表板為您提供快速概覽 hello 根據嚴重性層級來排列您的裝置上的警示數目。

![警示儀表板](./media/storsimple-manage-alerts/admin_alerts_dashboard.png)

按一下 hello 嚴重性層級開啟 hello**警示** 索引標籤 hello 結果包含只 hello 符合該嚴重性層級的警示。

![警示報表範圍 tooalert 類型](./media/storsimple-manage-alerts/admin_alerts_scoped.png)

按一下 [hello] 清單中的警示您提供其他詳細資料來 hello 警示、 包括 hello 最後一個時間 hello 報告警示、 hello 次數 hello 裝置等 hello hello 警示的建議動作 tooresolve hello 警示。 如果是硬體警示，則也會識別 hello 硬體元件。

![硬體警示範例](./media/storsimple-manage-alerts/admin_alerts_hardware.png)

如果您需要 toosend hello 資訊 tooMicrosoft 支援，您可以複製 hello 警示詳細資料 tooa 文字檔案。 您有遵循 hello 建議，並解決 hello 警示狀況的內部之後，您應清除從 hello 裝置 hello 警示中 hello 選取 hello 警示**警示** 索引標籤，然後按一下**清除**. tooclear 多個警示，選取每個警示，按一下任何資料行除了 hello**警示**資料行，然後再按一下**清除**全部選取之後 hello 警示 toobe 清除。 請注意當 hello 問題已解決或 hello 系統以新資訊更新 hello 警示時，會自動清除部分警示。

當您按一下**清除**、 就 hello 機會 tooprovide 註解 hello 警示和 hello 步驟，花費了 tooresolve hello 問題。 如果以新資訊觸發其他事件 hello 系統將會清除某些事件。 在此情況下，您會看到下列訊息的 hello。

![清除警示訊息](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>排序和檢閱警示
您可能會發現警示的更有效率 toorun 報表，讓您可以檢閱和清除群組中。 此外，hello**警示** 索引標籤可以顯示 too250 的警示。 如果您已超過此數目的警示，並非所有的警示會顯示 hello 預設檢視中。 您可以結合下列欄位會顯示哪些警示的 toocustomize hello:

* **狀態** – 您可以顯示 [作用中] 或 [已清除] 警示。 作用中警示仍會觸發系統時已清除的警示已被手動清除由系統管理員，或以程式設計方式清除因為 hello 系統以新資訊更新 hello 警示條件。
* **嚴重性** – 您可以顯示所有嚴重性層級 (重大、警告、資訊) 的警示，或只顯示特定嚴重性的警示，例如只有重大警示。
* **來源**– 您可以顯示所有來源的警示，或限制來自 hello 服務或一個或所有的 hello 裝置 hello 警示 toothose。
* **時間範圍**– 藉由指定 hello**從**和**至**日期和時間戳記，您可以查看警示 hello 您感興趣的時間週期期間。

## <a name="alerts-quick-reference"></a>警示快速參考
hello 下表列出一些您可能遇到的問題，以及其他資訊和建議可用 hello Microsoft Azure StorSimple 警示。 StorSimple 裝置警示分為下列類別目錄的 hello:

* [雲端連線能力警示](#cloud-connectivity-alerts)
* [叢集警示](#cluster-alerts)
* [災害復原警示](#disaster-recovery-alerts)
* [硬體警示](#hardware-alerts)
* [作業失敗警示](#job-failure-alerts)
* [固定在本機的磁碟區警示](#locally-pinned-volume-alerts)
* [網路警示](#networking-alerts)
* [效能警示](#performance-alerts)
* [安全性警示](#security-alerts)
* [支援封裝警示](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>雲端連線能力警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 連線太 <*雲端認證名稱*> 無法建立。 |無法連線 toohello 儲存體帳戶。 |您的裝置似乎有連線問題。 請執行 hello `Test-HcsmConnection` cmdlet 從 hello Windows PowerShell Interface for StorSimple，在您的裝置 tooidentify 並修正 hello 問題。 如果 hello 設定正確無誤，hello 問題可能是 hello hello 的 hello 警示的儲存體帳戶認證。 在此情況下，使用 hello `Test-HcsStorageAccountCredential` cmdlet toodetermine 是否有可以解決的問題。<ul><li>檢查網路設定。</li><li>檢查您的儲存體帳戶認證。</li></ul> |
| 我們未收到活動訊號來自您的裝置 hello 上次 <*數目*> 分鐘。 |無法連線 toodevice。 |您的裝置似乎有連線問題。 請使用 hello `Test-HcsmConnection` cmdlet 從 hello Windows PowerShell Interface for StorSimple，在您的裝置 tooidentify，並修正 hello 問題，或連絡網路系統管理員。 |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>雲端連線失敗時的 StorSimple 行為
若雲端連線失敗時，在生產環境中執行的 StorSimple 裝置會發生什麼情況？

如果雲端連線失敗 StorSimple 實際裝置上，然後根據您的裝置 hello 狀態 hello 可能會發生下列： 

* **Hello 您的裝置上的本機資料**： 段時間，會有任何中斷和讀取作業將繼續 toobe 提供服務。 不過，當 hello 未完成的 Io 數目會增加並超過限制時，hello 讀取無法啟動 toofail。 
  
    根據您的裝置上 hello 的資料量，hello 寫入也仍 hello toooccur hello 中斷後的第一個幾個小時 hello 雲端連線中。 hello 寫入將會再變慢及最終啟動 toofail 如果 hello 雲端連線中斷幾小時。 （toobe 推入 toohello 雲端資料的 hello 裝置上沒有暫存儲存位置。 傳送嗨資料時，這個區域會排清。 如果連線失敗，此儲存體區域中的資料將不會發送 toohello 雲端，且 IO 將會失敗。）   
* **Hello 雲端中的 hello 資料**： 對於大部分雲端連線錯誤，則會傳回錯誤。 一旦還原 hello 連線之後，就會繼續 hello IOs hello 使用者線上具有 toobring hello 磁碟區沒有。 在罕見情況下，使用者介入的情況下可能會需要的 toobring 後 hello 從磁碟區上線 hello Azure 傳統入口網站。 
* **正在進行中的雲端快照集**: hello 作業會重試幾次 4-5 小時內，而且如果未還原 hello 連線，將會失敗 hello 雲端快照。

### <a name="cluster-alerts"></a>叢集警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 裝置容錯移轉太 <*裝置名稱*>。 |裝置處於維護模式。 |裝置容錯移轉由於 tooentering 或現有的維護模式。 這很正常，不需要採取任何動作。 已認可此警示之後，請從 hello 警示頁面中清除。 |
| 裝置容錯移轉太 <*裝置名稱*>。 |剛更新裝置的韌體或軟體。 |發生叢集容錯移轉，因為 tooan 更新。 這很正常，不需要採取任何動作。 已認可此警示之後，請從 hello 警示頁面中清除。 |
| 裝置容錯移轉太 <*裝置名稱*>。 |控制器已關閉或重新啟動。 |裝置容錯移轉，因為 hello 作用中控制器關機或重新啟動系統管理員。 不需要採取任何動作。 已認可此警示之後，請從 hello 警示頁面中清除。 |
| 裝置容錯移轉太 <*裝置名稱*>。 |規劃的容錯移轉。 |確認這是規劃的容錯移轉。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。 |
| 裝置容錯移轉太 <*裝置名稱*>。 |未計劃的容錯移轉。 |StorSimple 建置 tooautomatically 復原，從非計劃的容錯移轉。 如果您看到大量的這些警示，請連絡 Microsoft 支援服務。 |
| 裝置容錯移轉太 <*裝置名稱*>。 |其他/未知的原因。 |如果您看到大量的這些警示，請連絡 Microsoft 支援服務。 Hello 問題解決後，請清除此警示從 hello 警示 頁面。 |
| 重大裝置服務會回報故障狀態。 |資料路徑服務失敗。 |連絡 Microsoft 支援服務尋求協助。 |
| 網路介面 <DATA #> 的虛擬 IP 位址會回報故障狀態。 |其他/未知的原因。 |有時候暫時性狀況可能會導致這些警示。 如果這是 hello 案例，然後此警示將會自動清除一段時間後。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |
| 網路介面 <DATA #> 的虛擬 IP 位址會回報故障狀態。 |介面名稱： <*資料 #*> IP 位址<IP address>無法上線，因為 hello 網路上偵測到重複的 IP 位址。 |確保 hello 重複的 IP 位址已從 hello 網路移除或重新設定 hello 介面使用不同的 IP 位址。 |

### <a name="disaster-recovery-alerts"></a>災害復原警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 復原作業無法還原所有的這項服務的 hello 設定。 部分裝置的裝置設定資料處於不一致的狀態。 |災害復原之後偵測到資料不一致。 |與 hello 裝置上不同步 hello 服務上的加密的資料。 授權裝置 hello <*裝置名稱*> 從 StorSimple Manager toostart hello 同步處理程序。 使用 hello Windows PowerShell Interface for StorSimple toorun hello`Restore-HcsmEncryptedServiceData`裝置上 <*裝置名稱*> cmdlet，cmdlet toorestore hello 安全性設定檔時提供為輸入的 toothis hello 舊密碼。 然後執行 hello `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet tooupdate hello 服務資料加密金鑰。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。 |

### <a name="hardware-alerts"></a>硬體警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 硬體元件 <元件識別碼> 報告狀態為 <狀態>。 | |有時候暫時性狀況可能會導致這些警示。 如果是的話，一段時間之後會自動清除這個警示。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |
| 被動控制器不正常。 |hello 被動 （次要） 控制器無法運作。 |您的裝置正常運作，但其中一個控制器不正常。 請嘗試重新啟動該控制器。 如果未解決 hello 問題，請連絡 Microsoft 支援服務。 |
| 偵測到即將發生的磁碟機失敗。 | 偵測到即將發生的磁碟機失敗。 |我們偵測到即將發生的磁碟機故障影響 hello 硬體元件 ' 中位置的磁碟機 <*位置識別碼*>，機箱 <*機箱識別碼*>'。 請考慮替換您的磁碟機。 <br> 開始 hello 更換磁碟之前，請檢閱下列資訊的 hello。<br><br>如果您的裝置有一部以上失敗的磁碟，永遠不要移除一部以上的 SSD 或 HDD。 這樣做可能會導致資料遺失。<br><br>請確定您將更換 SSD 放置在先前包含 SSD 的插槽中。 hello 也適用於 HDD。<br><br>位置編號從 0 too11。 插槽 2 中的故障的磁碟對應 tooa 插槽 3 的 hello 裝置 （從 hello 左上角） 中的故障的磁碟。<br><br>如需更換磁碟的詳細資訊，請移 toohttps://go.microsoft.com/fwlink/?linkid=838653。 如果問題仍存在，請透過 https://go.microsoft.com/fwlink/?linkid=838654 連絡 Microsoft 支援服務。 |

### <a name="job-failure-alerts"></a>作業失敗警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 備份 <來源磁碟區群組識別碼> 失敗。 |備份工作失敗。 |連線問題會導致 hello 備份作業無法成功地完成。 如果沒有任何連線問題，您可能已達到 hello 的備份數目上限。 刪除任何不再需要然後重試 hello 作業的備份。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。 |
| 複製 <*來源備份的項目 Id*> 太 <*目的地磁碟區序號*> 失敗。 |複製工作失敗。 |Hello 備份的重新整理 hello 備份清單 tooverify 為仍然有效。 如果 hello 備份是有效的很可能在雲端連線問題，導致 hello 複製操作無法順利完成。 如果沒有任何連線問題，您可能已達到 hello 儲存體限制。 刪除任何不再需要然後重試 hello 作業的備份。 在您採取適當的動作 tooresolve hello 問題之後，清除此警示從 hello 警示 頁面。 |
| 還原 <來源備份項目識別碼> 失敗。 |還原工作失敗。 |Hello 備份的重新整理 hello 備份清單 tooverify 為仍然有效。 如果 hello 備份是有效的很可能在雲端連線問題，導致 hello 還原作業無法成功地完成。 如果沒有任何連線問題，您可能已達到 hello 儲存體限制。 刪除任何不再需要然後重試 hello 作業的備份。 在您採取適當的動作 tooresolve hello 問題之後，清除此警示從 hello 警示 頁面。 |

### <a name="locally-pinned-volume-alerts"></a>固定在本機的磁碟區警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 建立本機磁碟區 <磁碟區名稱> 失敗。 |hello 磁碟區建立工作已失敗。 <*錯誤訊息對應 toohello 失敗錯誤碼*>。 |連線問題可能防止 hello 空間建立作業無法成功地完成。 本機固定磁碟區以佈建，並建立空間的 hello 程序牽涉到儲存階層式磁碟區 toohello 雲端。 如果沒有任何連線問題，您可能已耗盡 hello hello 裝置上的本機空間。 判斷空間上是否有 hello 裝置後再重試此作業。 |
| 擴充本機磁碟區 <磁碟區名稱> 失敗。 |hello 大量修改工作已失敗太 <*錯誤訊息對應 toohello 失敗錯誤碼*>。 |連線問題可能防止 hello 磁碟區延伸作業無法成功地完成。 本機固定磁碟區會以佈建及延伸現有空間的 hello 的 hello 程序牽涉到儲存階層式磁碟區 toohello 雲端。 如果沒有任何連線問題，您可能已耗盡 hello hello 裝置上的本機空間。 判斷空間上是否有 hello 裝置後再重試此作業。 |
| 轉換磁碟區 <磁碟區名稱> 失敗。 |hello 磁碟區轉換工作 tooconvert hello 磁碟區類型從本機固定 tootiered 失敗。 |無法完成從固定在本機的型別 tootiered hello 磁碟區的轉換。 請確認沒有任何連線問題，導致 hello 作業無法順利完成。 為了疑難排解連接問題太移[hello Test-hcsmconnection cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet)。<br>現在已被 hello 原始固定在本機磁碟區標示為分層磁碟區，因為某些 hello hello 固定在本機磁碟區的資料有 hello 轉換期間溢出 toohello 雲端。 hello 結果分層磁碟區仍佔用未來的本機磁碟區無法回收 hello 裝置上的本機空間。<br>請解決任何連線問題，清除 hello 警示並轉換成此磁碟區後 toohello 原始本機固定磁碟區類型 tooensure hello 的所有資料都都可以提供在本機上一次。 |
| 轉換磁碟區 <磁碟區名稱> 失敗。 |hello 磁碟區轉換工作 tooconvert hello 磁碟區類型從分層式 toolocally 釘選失敗。 |無法完成 hello 磁碟區的分層式的 toolocally 釘選的型別轉換。 請確認沒有任何連線問題，導致 hello 作業無法順利完成。 為了疑難排解連接問題太移[hello Test-hcsmconnection cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet)。<br>hello 原始分層磁碟區現在標示為本機固定磁碟區 hello 轉換程序的一部分進行 toohave 資料位於 hello 雲端 hello 以佈建 hello 裝置，此磁碟區上的空間時可以不會再回收以進行未來的本機磁碟區。<br>解決任何連線問題、 清除 hello 警示和轉換此磁碟區後 toohello 原始分層磁碟區類型 tooensure 本機以 hello 裝置上佈建，可以回收空間。 |
| 接近 <磁碟區群組名稱> 的本機快照的本機空間使用量 |Hello 備份原則的本機快照可能即將耗盡空間並會失效的 tooavoid 主機寫入失敗。 |頻繁的本機快照與 hello 與此備份原則群組關聯的磁碟區中的高資料變換率導致本機空間快速耗盡 hello 裝置 toobe 上。 刪除任何不再需要的本機快照。 此外，更新較不頻繁的本機快照集，此備份原則 tootake 您本機快照排程，並確保會定期取得雲端快照。 如果不會採用這些動作，這些快照的本機空間可能即將耗盡 hello 系統會自動刪除它們 tooensure 主機寫入持續 toobe 順利處理。 |
| <磁碟區群組名稱> 的本機快照已經無效。 |hello 的本機快照 <*磁碟區群組名稱*> 失效，被刪除，因為它們已超過 hello hello 裝置上的本機空間。 |這不在未來的 hello 重複發生，請檢閱此備份原則的 hello 本機快照排程，並刪除不再需要的所有本機快照 tooensure。 頻繁的本機快照與 hello 與此備份原則群組關聯的磁碟區中的高資料變換率可能會導致本機空間快速耗盡 hello 裝置 toobe 上。 |
| 還原 <來源備份項目識別碼> 失敗。 |hello 還原工作已失敗。 |如果您有固定在本機或在本機固定和階層式磁碟區，此備份原則，hello 備份的重新整理 hello 備份清單 tooverify 中混用是否仍然有效。 如果 hello 備份是有效的很可能在雲端連線問題，導致 hello 還原作業無法成功地完成。 在本機 hello 釘選為屬於此快照集的群組不包含所有資料下載的 toohello 裝置，而且，如果您有混合的階層式和本機固定磁碟區，此快照集 」 群組中，它們不會彼此同步已還原的磁碟區。 toosuccessfully 完成 hello 還原作業，在此群組離線，hello 主機上建立 hello 磁碟區，然後重試 hello 還原作業。 請注意 hello 期間所執行的任何修改 toohello 磁碟區資料還原程序將會遺失。 |

### <a name="networking-alerts"></a>網路警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 無法啟動 StorSimple 服務。 |資料路徑錯誤 |如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |
| 偵測到 'Data0' 的 IP 位址重複。 | |hello 系統偵測到 IP 位址 '10.0.0.1' 的衝突。 hello hello 裝置上的網路資源 'Data0'  *<device1>* 處於離線狀態。 確定此網路中的其他任何實體並未使用此 IP 位址。 tootroubleshoot 網路問題、 跳過[hello Get-netadapter cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet)。 請連絡網路系統管理員協助解決此問題。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |
| 'Data0' 的 IPv4 (或 IPv6) 位址已離線。 | |hello 網路資源 'Data0' 使用 IP 位址 '10.0.0.1'。 和首碼長度 '22' hello 裝置上 *<device1>* 處於離線狀態。 請確定該連接此介面的 hello 交換器連接埠 toowhich 可正常運作。 tootroubleshoot 網路問題、 跳過[hello Get-netadapter cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet)。 |

### <a name="performance-alerts"></a>效能警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| hello 裝置負載超過 <*閾值*>。 |比預期的回應時間慢。 |您的裝置報告使用率處於輸入/輸出負荷過重的情況。 這會導致您的裝置 toonot 工作達到其應有的效能。 檢閱您附加 toohello 裝置，並判斷是否有任何無法 tooanother 裝置或不再需要移動的 hello 工作負載。<br>toounderstand hello 目前狀態，請移過[使用 hello StorSimple Manager 服務 toomonitor 您的裝置](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>安全性警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| Microsoft 支援服務工作階段已開始。 |協力廠商已存取支援工作階段。 |請確認已授權此存取。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。 |
| <項目> 密碼將在 <時間長度> 後過期。 |密碼即將過期。 |請在密碼過期之前變更密碼。 |
| <項目識別碼> 遺漏安全性組態資訊。 | |hello 與此磁碟區容器相關聯的磁碟區不能使用的 tooreplicate 您的 StorSimple 組態。 tooensure 資料已安全地儲存，我們建議您刪除 hello 磁碟區容器及 hello 磁碟區容器相關聯的任何磁碟區。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。 |
| 嘗試登入 <項目 ID> 失敗 <數字> 次。 |多次嘗試登入失敗。 |您的裝置可能遭受攻擊，或授權的使用者正在嘗試 tooconnect 不正確的密碼。<ul><li>請連絡授權的使用者，並確認這些嘗試來自合法來源。 如果您繼續 toosee 大量的登入嘗試失敗，請考慮停用遠端管理並連絡網路系統管理員。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。</li><li>確認您的快照集管理員執行個體設定 hello 正確的密碼。 採取適當的動作之後，請清除此警示從 hello 警示 頁面。</li></ul>如需詳細資訊，請移至太[變更過期的裝置密碼](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password)。 |
| 變更 hello 服務資料加密金鑰時發生一個或多個失敗。 | |沒有變更 hello 服務資料加密金鑰時發生錯誤。 在您解決 hello 錯誤條件後，執行 hello `Invoke-HcsmServiceDataEncryptionKeyChange` hello Windows PowerShell Interface for StorSimple 在裝置 tooupdate hello 服務上的指令程式。 如果此問題持續發生， 請連絡 Microsoft 支援服務。 解決 hello 問題之後，請清除此警示從 hello 警示 頁面。 |

### <a name="support-package-alerts"></a>支援封裝警示
| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 建立支援封裝失敗。 |StorSimple 無法產生 hello 封裝。 |重試此作業。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 解決 hello 問題之後，清除此警示從 hello 警示 頁面。 |

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 錯誤和疑難排解可運作的裝置](storsimple-troubleshoot-operational-device.md)。

