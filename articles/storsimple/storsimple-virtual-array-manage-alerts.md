---
title: "aaaView 及管理 Microsoft Azure StorSimple Virtual Array 警示 |Microsoft 文件"
description: "描述 StorSimple Virtual Array 警示條件和嚴重性，以及如何 toouse hello StorSimple Manager 服務 toomanage 警示。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Hello StorSimple Virtual Array 的使用 StorSimple 裝置管理員 toomanage 警示

## <a name="overview"></a>概觀

hello StorSimple 裝置 Manager 服務中的 hello 警示功能提供您 tooreview 一種方式，並清除警示相關的 tooStorSimple 虛擬陣列，即時的方式。 您可以使用 hello 警示上 hello**服務摘要**刀鋒視窗 toocentrally 監視您的 StorSimple 虛擬陣列的 hello 健全狀況問題和 hello 整體的 Microsoft Azure StorSimple 解決方案。

本教學課程說明如何 tooconfigure 警示通知，常見的警示條件，警示的嚴重性層級，以及如何 tooview 及追蹤的警示。 此外，它會包括警示快速參考資料表，可讓您 tooquickly 找出特定的警示，並適當地回應。

![警示頁面](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>設定警示設定

您可以選擇是否要讓 toobe 收到 hello 警示的條件，您的 StorSimple 虛擬陣列的每個電子郵件通知。 此外，您可以識別其他警示通知收件者電子郵件地址輸入 hello**其他電子郵件收件者** 方塊中，並以分號分隔。

> [!NOTE]
> 您可以對每一個虛擬陣列輸入最多 20 個電子郵件地址。


啟用虛擬陣列的電子郵件通知後，hello 通知清單的成員會收到電子郵件訊息，每次發生嚴重的警示時。 會將傳送 hello 訊息 *storsimple-alerts-noreply@mail.windowsazure.com*  ，並將說明 hello 警示條件。 收件者可以按一下**Unsubscribe** tooremove 本身從 hello 電子郵件通知清單。

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable 警示的電子郵件通知

1. 服務和 hello 移 tooyour StorSimple 裝置管理員**管理**區段中選取，然後按一下 **裝置**。 從顯示的裝置 hello 清單，請選取，然後按一下您的裝置。
   
    ![警示設定](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. 這會開啟 hello**設定**刀鋒視窗。 在 hello**裝置設定**區段中，選取**一般**。 這會開啟 hello**一般設定**刀鋒視窗。
   
    ![警示通知組態](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. 在 hello**一般設定**刀鋒視窗中，跳過**警示設定**區段和 hello 下列設定：
   
   1. 在 hello**啟用電子郵件通知**欄位中，選取**是**。
   2. 在 hello**電子郵件服務系統管理員**欄位中，選取**是**如果您想 toohave hello 服務系統管理員，而且所有的共同管理員收到 hello 警示通知。
   3. 在 hello**其他電子郵件收件者**欄位中，輸入 hello 的所有其他收件者應該會收到 hello 警示通知的電子郵件地址。 輸入名稱，格式為 hello  *someone@somewhere.com* 。使用分號 tooseparate hello 電子郵件地址。 您可以對每一個虛擬裝置設定最多 20 個電子郵件地址。
      
       ![警示通知組態](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. 按一下 toosend 測試電子郵件通知，**傳送測試電子郵件**。 hello StorSimple 裝置管理員服務將會顯示狀態訊息轉送 hello 測試通知。
      
       ![已傳送警示測試通知電子郵件](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > 如果 hello 測試通知無法傳送訊息，hello StorSimple 裝置管理員服務將會顯示適當的訊息。 按一下**確定**，稍候幾分鐘，然後再試 toosend 測試通知訊息。
      > 
      > 
   5. 在 hello hello 頁面底部，按一下**儲存**toosave 您的設定。 系統提示您進行確認時，按一下 [是] 。
      
      ![已傳送警示測試通知電子郵件](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>常見的警示狀況

您的 StorSimple Virtual Array 回應 tooa 各種情況中，會產生警示。 hello 如下 hello 最常見的警示條件類型：

* **連線問題** – 當傳送資料有困難時會發生這些警示。 通訊可能會發生問題的資料 tooand 傳輸期間從 hello Azure 儲存體帳戶或到期 toolack hello 虛擬裝置與 hello StorSimple 裝置管理員服務之間的連線。 通訊問題是一些 hello 最複雜 toofix 因為有太多失敗點。 您應該一律先網路連線和網際網路存取可用之前先確認 toomore 上繼續進行進階疑難排解。 如需連接埠和防火牆設定的資訊，請太[StorSimple Virtual Array 系統需求](storsimple-ova-system-requirements.md)。 疑難排解說明，請跳過[hello Test-connection cmdlet 與疑難排解](storsimple-troubleshoot-deployment.md)。
* **效能問題** – 當系統未以最佳方式運作時，例如負荷過重，就會造成這些警示。

此外，您可能會看到警示相關的 toosecurity、 更新或工作失敗。

## <a name="alert-severity-levels"></a>警示嚴重性層級

警示有不同的嚴重性層級，視 hello 的 hello 影響而定，警示的情況下會有並 hello 回應 toohello 警示需要。 hello 嚴重性層級為：

* **重大**– 此警示會回應 tooa 條件影響 hello 成功的效能，您的系統中。 動作是必要的 tooensure hello StorSimple 服務沒有被中斷。
* **警告** – 此狀況如果不解決，可能會演變成重大狀況。 您應該調查 hello 狀況並採取任何必要動作 tooclear hello 問題。
* **資訊** – 此警示包含適用於追蹤和管理系統的資訊。

## <a name="view-and-track-alerts"></a>檢視和追蹤警示

hello StorSimple 裝置管理員服務摘要 刀鋒視窗可提供您快速概覽 hello 您虛擬裝置，排列依據嚴重性等級的警示數目。

![警示儀表板](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

按一下 hello 嚴重性層級 tooopen hello**警示**刀鋒視窗。 hello 結果包含只 hello 符合該嚴重性層級的警示。

![警示報表範圍 tooalert 類型](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

按一下 hello 清單 tooget 的其他詳細資料 hello 警示，包括 hello 上次報告 hello 警示，hello 次數 hello 裝置上的 hello 警示和 hello 建議的動作 tooresolve hello 警示中的警示。

![警示清單和詳細資料](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

如果您需要 toosend hello 資訊 tooMicrosoft 支援，您可以複製 hello 警示詳細資料 tooa 文字檔案。 您有遵循 hello 建議，並解決 hello 警示狀況的內部之後，您應清除 hello hello 清單中的警示。 從 [hello] 清單中選取 hello 警示，然後按一下**清除**。 tooclear 多個警示，選取每個警示，按一下任何資料行除了 hello**警示**資料行，然後再按一下**清除**全部選取之後 hello 警示 toobe 清除。

當您按一下**清除**、 就 hello 機會 tooprovide 註解 hello 警示和 hello 步驟，花費了 tooresolve hello 問題。 

![警示註解](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

如果以新資訊觸發其他事件 hello 系統將會清除某些事件。 

## <a name="sort-and-review-alerts"></a>排序和檢閱警示

hello**警示**刀鋒視窗可以顯示 too250 的警示。 如果您已超過此數目的警示，並非所有的警示會顯示 hello 預設檢視中。 您可以結合下列欄位會顯示哪些警示的 toocustomize hello:

* **狀態** – 您可以顯示 [作用中] 或 [已清除] 警示。 作用中警示仍會觸發系統時已清除的警示已被手動清除由系統管理員，或以程式設計方式清除因為 hello 系統以新資訊更新 hello 警示條件。
* **嚴重性** – 您可以顯示所有嚴重性層級 (重大、警告、資訊) 的警示，或只顯示特定嚴重性的警示，例如只有重大警示。
* **來源**– 您可以顯示所有來源的警示，或限制 hello 警示 toothose 來自 hello 服務或一個或所有 hello 虛擬裝置。
* **時間範圍**– 藉由指定 hello**從**和**至**日期和時間戳記，您可以查看警示 hello 您感興趣的時間週期期間。

## <a name="alerts-quick-reference"></a>警示快速參考

hello 下表列出一些您可能遇到的問題，以及其他資訊和建議可用 hello StorSimple 警示。 StorSimple Virtual Array 警示可分成下列類別目錄的 hello 的其中一個：

* [雲端連線能力警示](#cloud-connectivity-alerts)
* [組態警示](#configuration-alerts)
* [作業失敗警示](#job-failure-alerts)
* [效能警示](#performance-alerts)
* [安全性警示](#security-alerts)
* [更新警示](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>雲端連線能力警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 裝置 *<device name>* 是未連接 toohello 雲端。 |hello 名為裝置無法連線 toohello 雲端。 |無法連線 toohello 雲端。 這可能是因 tooone hello 以下的：<ul><li>可能有 hello 網路設定，您的裝置上的問題。</li><li>可能有問題 hello 儲存體帳戶認證。</li></ul>如需有關疑難排解連線問題的詳細資訊，請移至 toohello[本機 web UI](storsimple-ova-web-ui-admin.md)的 hello 裝置。 |

### <a name="configuration-alerts"></a>組態警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 不支援的內部部署虛擬裝置組態。 |效能變慢。 |hello 目前的組態可能會導致效能降低。 確定您的伺服器符合 hello 最低設定需求。 如需詳細資訊，請移至太[StorSimple 虛擬陣列需求](storsimple-ova-system-requirements.md)。 |
| <裝置名稱> 上的佈建磁碟空間即將用盡。 |磁碟空間警告。 |佈建磁碟空間偏低。 toofree 佔用空間，建議您移動工作負載 tooanother 磁碟區或共用或刪除資料。 |

### <a name="job-failure-alerts"></a>作業失敗警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 無法完成 <裝置名稱> 的備份。 |備份作業失敗。 |無法建立備份。 請考慮 hello 下列其中一種：<ul><li>連線問題會導致 hello 備份作業無法成功地完成。 確定沒有連線問題。 如需有關疑難排解連線問題的詳細資訊，請移至 toohello[本機 web UI](storsimple-ova-web-ui-admin.md)虛擬裝置。</li><li>您已達到 hello 可用的存放裝置限制。 toofree 佔用空間，請考慮刪除任何不再需要的備份。</li></ul> 解決 hello 問題、 清除 hello 警示和重試 hello 作業。 |
| 無法完成 <裝置名稱> 的複製。 |複製作業失敗。 |無法建立複製。 請考慮 hello 下列其中一種：<ul><li>您的備份清單可能無效。 重新整理 hello 清單 tooverify 時仍然有效。</li><li>連線問題可能防止 hello 複製操作無法順利完成。 確定沒有連線問題。</li><li>您已達到 hello 可用的存放裝置限制。 toofree 佔用空間，請考慮刪除任何不再需要的備份。</li></ul>解決 hello 問題、 清除 hello 警示和重試 hello 作業。 |

### <a name="performance-alerts"></a>效能警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 您遇到資料傳輸的非預期延遲 |慢速資料傳輸。 |當您超出儲存體服務的 hello 延展性目標時，就會發生節流處理錯誤。 hello 儲存體服務會執行此 tooensure 的任何單一用戶端或租用戶可以在 hello 費用的其他人使用 hello 服務。 如需有關如何疑難排解您的 Azure 儲存體帳戶的詳細資訊，請移太[監視、 診斷和疑難排解 Microsoft Azure 儲存體](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)。 |
| <裝置名稱> 上的本機保留磁碟空間即將用盡。 |回應時間變慢。 |hello 的 10%的總佈建的大小 <*裝置名稱*> 會保留在 hello 本機裝置和您正在不足 hello 保留空間。 hello 工作負載 <*裝置名稱*> 會產生較高的變換，或您的速率可能最近移轉大量資料。 這可能會導致效能降低。 請考慮的其中一個 hello 動作 tooresolve 下列這樣：<ul><li>增加 hello 雲端頻寬 toothis 裝置。</li><li>請減少或移動工作負載 tooanother 磁碟區或共用。</li></ul> |

### <a name="security-alerts"></a>安全性警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| <裝置名稱> 的密碼即將於 <數字> 天後到期。 |密碼警告。 |您的密碼即將於 <數字> 天後到期。 請考慮變更您的密碼。 如需詳細資訊，請移至太[變更 hello StorSimple Virtual Array 裝置系統管理員密碼](storsimple-virtual-array-change-device-admin-password.md)。 |

### <a name="update-alerts"></a>更新警示

| 警示文字 | 事件 | 詳細資訊 / 建議的動作 |
|:--- |:--- |:--- |
| 您的裝置有新的更新可用。 |可用的更新 toohello StorSimple Virtual Array。 |您可以安裝新的更新從 hello**維護**頁面。 |
| 無法掃描 <裝置名稱> 有無新的更新。 |更新失敗。 |安裝新的更新時發生錯誤。 您可以手動安裝 hello 更新。 如果 hello 問題持續發生，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)。 |

## <a name="next-steps"></a>後續步驟

* [深入了解 hello StorSimple Virtual Array](storsimple-ova-overview.md)。

