---
title: "Active Directory 複寫狀態，以及 Azure Log Analytics aaaMonitor |Microsoft 文件"
description: "定期 hello Active Directory 複寫狀態解決方案組件監視 Active Directory 環境的任何複寫失敗，並報告 hello 結果 OMS 儀表板上。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>使用 Log Analytics 監視 Active Directory 複寫狀態

![AD 複寫狀態符號](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory 是企業 IT 環境的重要元件。 tooensure 高可用性和高效能，每個網域控制站有它自己的 hello Active Directory 資料庫複本。 網域控制站複寫彼此順序 toopropagate 變更 hello 企業。 在此複寫程序中的失敗可導致各種問題 hello 企業。

定期 hello AD 複寫狀態解決方案組件監視 Active Directory 環境的任何複寫失敗，並報告 hello 結果 OMS 儀表板上。

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 方案。

* 您必須是評估 hello 網域 toobe 的成員的網域控制站上安裝代理程式。 或者，您必須在成員伺服器上安裝代理程式和設定 hello 代理程式 toosend AD 複寫資料 tooOMS。 如何 tooconnect Windows 電腦 tooOMS，請參閱的 toounderstand[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。 如果您的網域控制站已經是您想 tooconnect tooOMS 現有 System Center Operations Manager 環境的一部分，請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。
* 新增 hello OMS 工作區中使用 hello 程序中所述的 Active Directory 複寫狀態方案 tooyour [hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。  不需要進一步的組態。

## <a name="ad-replication-status-data-collection-details"></a>AD 複寫狀態資料收集詳細資料
hello 下表顯示資料收集方法，以及如何針對 AD 複寫狀態收集資料的其他詳細資料。

| 平台 | 直接代理程式 | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |每隔五天 |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>（選擇性） 啟用非網域控制站 toosend AD 資料 tooOMS
如果您不想 tooconnect 任何網域控制站直接 tooOMS，您可以使用其他 OMS 連線的電腦在您的網域 toocollect 資料 hello AD 複寫狀態方案組件，並讓它傳送嗨資料。

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>非網域控制站 toosend AD 資料 tooOMS tooenable
1. 請確認該 hello 電腦是您想使用 hello AD 複寫狀態解決方案 toomonitor hello 網域的成員。
2. [連接 hello Windows 電腦 tooOMS](log-analytics-windows-agents.md)或[連接使用您現有的 Operations Manager 環境 tooOMS](log-analytics-om-agents.md)，如果您尚未連接。
3. 該電腦上，設定下列登錄機碼的 hello:

   * 機碼：**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * 值：**IsTarget**
   * 數值資料︰**true**

   > [!NOTE]
   > 這些變更不會影響直到您重新啟動 hello Microsoft Monitoring Agent 服務 (HealthService.exe)。
   >
   >

## <a name="understanding-replication-errors"></a>了解複寫錯誤
一旦傳送 tooOMS AD 複寫狀態資料，您會看到下列影像指出您目前有多少複寫錯誤 hello OMS 儀表板上並排顯示類似 toohello。  
![AD 複寫狀態圖格](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**重要的複寫錯誤**錯誤會等於或高於 75%的 hello[標記存留時間](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx)為 Active Directory 樹系。

當您按一下 hello 磚時，您可以檢視 hello 錯誤的詳細資訊。
![AD 複寫狀態儀表板](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>目的地伺服器狀態和來源伺服器狀態
這些資料行會顯示 hello 狀態，目的地伺服器以及發生複寫錯誤的來源伺服器。 每個網域控制站名稱之後的 hello 數字表示該網域控制站上的複寫錯誤的 hello 數目。

目的地伺服器和來源伺服器 hello 錯誤會顯示，因為某些問題會更容易 tootroubleshoot 觀點 hello 來源伺服器和其他人 hello 目的地伺服器檢視方塊。

在此範例中，您可以看到多個目的地伺服器都面臨 hello 相同數目的錯誤，但有一部來源伺服器 (ADDC35) 多詳細的錯誤，所有 hello 比其他項目。 很可能導致 toofail toosend 資料 tooits 複寫協力電腦的 ADDC35 上沒有發生問題。 修正 hello 問題 ADDC35 上可能會解決許多 hello 目的地伺服器 區域中出現的 hello 錯誤。

### <a name="replication-error-types"></a>複寫錯誤類型
這個區域可讓您的整個企業內偵測到錯誤的 hello 類型的相關資訊。 每個錯誤有唯一的數字代碼和訊息，可協助您判斷 hello hello 錯誤根本原因。

hello 甜甜圈 hello 頂端讓您的瞭解其中錯誤會出現多個且較不常在您的環境。

它會示範多個網域控制站發生 hello 時相同的複寫錯誤。 在此情況下，您可能會無法 toodiscover 或識別一個網域控制站，方案然後重複它在其他網域控制站上受到 hello 相同錯誤。

### <a name="tombstone-lifetime"></a>標記存留期
hello 標記存留時間決定多久已刪除的物件，參考 tooas 標記，會保留在 hello Active Directory 資料庫。 已刪除的物件會傳遞 hello 標記存留時間，記憶體回收處理會自動移除它從 hello Active Directory 資料庫。

hello 預設標記存留期為 180 天的最新的 Windows 版本，但它是較舊的版本 60 天和它的 Active Directory 系統管理員可以明確地變更。

如果您有已接近或超過 hello 標記存留時間的複寫錯誤，很重要的 tooknow。 如果兩個網域控制站發生複寫錯誤的 hello 標記存留時間超過持續發生，是停用複寫之間的兩個網域控制站，即使固定的 hello 基礎複寫錯誤。

hello 標記存留時間區域，可協助您識別可能發生已停用的複寫的所在的位置。 每個錯誤中 hello**超過 100 %tsl**類別代表尚未複寫其來源和目的地伺服器之間的在最少 hello 樹系的 hello 標記存留時間的資料分割。

在此情況下，只需修正 hello 複寫錯誤將不太夠。 至少，您需要 toomanually 調查 tooidentify 並清除延遲物件，然後才能重新啟動複寫。 您甚至可能需要 toodecommission 網域控制站。

在加法 tooidentifying hello 標記存留時間，超過的保存任何複寫錯誤您也想 toopay 注意 tooany 錯誤落入 hello **50-75 %tsl**或**75 100 %tsl**類別目錄。

這些是會清楚地延遲、 不暫時性的因此它們可能需要您介入 tooresolve 的錯誤。 hello 好消息是，它們尚未到達 hello 標記存留時間。 如果您立即修正這些問題和*之前*到達 hello 標記存留時間，複寫可以重新啟動具有最少手動介入。

如前文所述，hello AD 複寫狀態解決方案的 hello 儀表板磚會顯示 hello 數目*重大*複寫錯誤，在您環境中，定義為超過 75%的標記存留時間 （包括錯誤錯誤會超過 100%的 TSL）。 盡可能 tookeep 0 這個數字。

> [!NOTE]
> 所有的 hello 標記存留期百分比計算根據您的 Active Directory 樹系的 hello 實際的標記存留時間，讓您可以信任這些百分比是正確的即使您擁有設定自訂的標記存留時間值。
>
>

### <a name="ad-replication-status-details"></a>AD 複寫狀態詳細資料
當您按一下其中一個 hello 清單中的任何項目時，您會看到資訊，請使用 記錄搜尋的其他詳細資料。 hello 結果是已篩選的 tooshow 只有 hello 錯誤 toothat 相關項目。 例如，如果您按一下第一個網域控制站 hello 底下所列**目的地伺服器狀態 (ADDC02)**，您會看到篩選 tooshow 錯誤與該列為 hello 目的地伺服器的網域控制站的搜尋結果：

![搜尋結果中的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

從這裡，您可以進一步篩選，修改 hello 的搜尋查詢，並以此類推。 如需使用記錄搜尋 hello 的詳細資訊，請參閱[記錄搜尋](log-analytics-log-searches.md)。

hello **HelpLink**欄位會顯示有關該特定錯誤的其他詳細資料與 TechNet 頁面 hello URL。 您可以複製並貼入您的瀏覽器視窗 toosee 資訊，疑難排解和修正 hello 錯誤相關的此連結。

您也可以按一下**匯出**tooexport hello 結果 tooExcel。 匯出 hello 資料可協助您以任何您想要的方式複寫錯誤資料視覺化。

![Excel 中匯出的 AD 複寫狀態錯誤](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>AD 複寫狀態常見問題集
**問︰多久更新一次 AD 複寫狀態資料？**
答： hello 資訊會更新每隔五天。

**問： 是否有這項資料更新頻率的方式 tooconfigure？**
答：目前沒有。

**問： 我需要 tooadd 所有我的網域控制站 toomy OMS 工作區中訂單 toosee 複寫狀態？**
答︰否，只需加入單一網域控制站。 如果您有多個網域控制站，您的 OMS 工作區中，所有這些資料會傳送 tooOMS。

**問： 我不想 tooadd 任何網域控制站 toomy OMS 工作區。仍然可以使用 hello AD 複寫狀態方案嗎？**
答： 會。 您可以設定的登錄金鑰 tooenable hello 值它。 請參閱[tooenable 非網域控制站 toosend AD 資料 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。

**問： hello 沒有 hello 資料收集的 hello 程序名稱為何？**
答︰AdvisorAssessment.exe

**問： 如何花費時間的資料收集的 toobe？**
答： 資料收集時間的 hello 的 Active Directory 環境的 hello 大小而定，但程序通常需要 15 分鐘內。

**問：收集的資料類型為何？**
答：複寫資訊是透過 LDAP 收集。

**問： 是否有方法 tooconfigure，資料收集時間？**
答：目前沒有。

**問： 哪些權限執行我需要 toocollect 資料嗎？**
答： 一般使用者權限 tooActive 目錄，已足夠。

## <a name="troubleshoot-data-collection-problems"></a>疑難排解資料收集問題
在訂單 toocollect 資料，hello AD 複寫狀態解決方案組件都需要至少一個網域控制站連線的 toobe tooyour OMS 工作區。 連接網域控制站後，會彈出訊息顯示**資料仍在收集中**。

如果您需要協助連接其中一個網域控制站，您可以檢視文件，網址[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。 或者，如果您的網域控制站已經連線的 tooan 現有 System Center Operations Manager 環境，您可以檢視文件，網址[連接 System Center Operations Manager tooLog 分析](log-analytics-om-agents.md)。

如果您不想 tooconnect 任何網域控制站直接 tooOMS 或 tooSCOM，請參閱[tooenable 非網域控制站 toosend AD 資料 tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms)。

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Active Directory 複寫狀態資料。
