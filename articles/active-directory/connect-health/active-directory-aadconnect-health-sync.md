---
title: "與同步處理的 Azure AD Connect Health aaaUsing |Microsoft 文件"
description: "這是將討論如何 toomonitor Azure AD Connect 同步處理的 hello Azure AD Connect Health 頁面。"
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>使用 Azure AD Connect Health 監視 Azure AD Connect 同步處理
下列文件的 hello 是特定 toomonitoring Azure AD Connect （同步） 與 Azure AD Connect Health。  如需使用 Azure AD Connect Health 來監視 AD FS 的詳細資訊，請參閱 [在 AD FS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)。 此外，如需使用 Azure AD Connect Health 來監視 Active Directory 網域服務的詳細資訊，請參閱 [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>適用於同步處理的 Azure AD Connect Health 警示
同步處理區段 hello Azure AD Connect Health 警示會提供 hello 的作用中警示清單。 每個警示都包含相關資訊、 解決步驟和連結 toorelated 文件。 藉由選取作用中或已解決的警示，您會看到新的刀鋒視窗的詳細資訊，請為 tooresolve hello 警示及連結 tooadditional 文件，您可以採取的步驟。 您也可以在 hello 過去已解決的警示檢視歷程記錄資料。

只要選取的警示的其他資訊以及步驟會提供您可以採取 tooresolve hello 警示和連結 tooadditional 文件。

![Azure AD Connect 同步處理錯誤](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>有限的警示評估
如果 Azure AD Connect 不使用 hello 預設組態 （例如，如果屬性篩選從 hello 預設組態 tooa 自訂組態變更），然後 hello Azure AD Connect Health 代理程式將不會上傳 hello 錯誤事件相關的 tooAzureAD Connect。

這會由 hello 服務限制 hello 評估的警示。 您會看到將橫幅指出此情況下您的服務的 hello Azure 入口網站中。

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

您可以透過按一下 [設定]，並允許 Azure AD Connect Health 代理程式 tooupload 所有的錯誤記錄檔來變更這個設定。

![適用於同步處理的 Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>同步處理深入了解
需要系統管理員頻繁地 tooknow hello toosync 變更 tooAzure AD 和變更正在進行中的 hello 數量所花費的時間。 這項功能提供簡單的方式 toovisualize 此使用圖形下方的 hello:   

* 同步處理作業的延遲
* 物件變更趨勢

### <a name="sync-latency"></a>同步處理延遲
這項功能提供的圖形化趨勢 hello 同步處理作業 （匯入、 匯出、 等等） 的連接器的延遲。  這可提供快速並輕鬆 toounderstand 不僅 hello 可能需要進一步調查的 hello 延遲，您的作業 （如果有發生變更的大型集合，此項會較大），但方式 toodetect 異常的延遲。

![同步處理延遲](./media/active-directory-aadconnect-health-sync/synclatency02.png)

根據預設，會顯示只有 hello 的 hello Azure AD 連接器 hello 'Export' 作業的延遲。  toosee hello 連接器上的多個作業或 tooview 作業，從其他連接器，以滑鼠右鍵按一下在 hello 圖上，選取 編輯圖表或 hello 」 編輯延遲圖表 」 按鈕上按一下，然後選擇 hello 特定作業和連接器。

### <a name="sync-object-changes"></a>同步處理物件的變更
這項功能提供的圖形化 hello 數的變更，會在評估並匯出 tooAzure AD 趨勢。  今天，嘗試 toogather hello 同步處理記錄檔的這項資訊是很困難。  hello 圖表可讓您，不但更簡單的方式監視 hello 數目會在您的環境中進行的變更，但 hello 失敗所發生的視覺化檢視。

![同步處理延遲](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>物件層級同步處理錯誤報告 (預覽)
在 Windows Server AD 與 Azure AD 之間使用 Azure AD Connect 同步處理身分識別資料時，針對可能發生的同步處理錯誤，這項功能提供相關的報告。

* hello 報表涵蓋 hello 同步用戶端所記錄的錯誤 (Azure AD Connect 1.1.281.0 版或更高版本)
* Hello 上次同步處理作業 hello 同步處理引擎中包含 hello 發生的錯誤。 （「 匯出 」 上 hello Azure AD 連接器。）
* Azure AD Connect Health 代理程式進行同步必須 hello 報表 tooinclude hello 最新資料的傳出連線所需的 toohello 結束點。
* hello 報表是**更新之後每隔 30 分鐘**使用 hello 資料上傳由 Azure AD Connect Health 代理程式進行同步。它提供下列重要功能的 hello

  * 錯誤分類
  * 依各類別之錯誤列出物件
  * 所有 hello hello 錯誤，在某個位置的相關資料
  * 並排比較的物件，因為 tooa 衝突錯誤
  * Hello 錯誤報表下載為 CSV，（即將推出）

### <a name="categorization-of-errors"></a>錯誤分類
hello 報表來分類 hello 現有同步處理中的錯誤 hello 下列類別：

| 類別 | 說明 |
| --- | --- |
| 重複的屬性 |當 Azure AD Connect 嘗試在 Azure AD 中以一或多個重複的屬性值建立或更新物件時發生錯誤，這些屬性在租用戶中必須是唯一的，例如 proxyAddresses、UserPrincipalName。 |
| 資料不符 |Hello 軟比對失敗會導致同步處理錯誤的 toomatch 物件時的錯誤。 |
| 資料驗證失敗 |錯誤，因為 tooinvalid 資料，例如在重要的屬性，例如 UserPrincipalName，不支援的字元格式化之前寫入在 Azure AD 中驗證失敗的錯誤。 |
| 大型屬性 |當一或多個屬性都是大於 hello 錯誤允許大小、 長度或計數。 |
| 其他 |所有其他錯誤無法容納的 hello 上方類別目錄。 根據意見，此類別將會進一步分成子類別。 |

![同步處理錯誤報告摘要](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![同步處理錯誤報告類別](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>依各類別之錯誤列出物件
鑽研至每個類別會提供物件都有 hello 錯誤類別目錄中的 hello 的清單。
![同步處理錯誤報告清單](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>錯誤詳細資料
下列資料位於 hello 詳細檢視每個錯誤

* 識別項的 hello *AD 物件*涉及
* 識別項的 hello *Azure AD 物件*涉及 （視情況）
* 錯誤描述以及 toofix
* 相關文章

![同步處理錯誤報告詳細資料](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Hello 錯誤報表下載為 CSV
藉由選取 hello 「 匯出 」 按鈕，您可以下載所有 hello 錯誤相關的所有 hello 詳細資料的 CSV 檔案。

## <a name="related-links"></a>相關連結
* [針對同步處理期間的錯誤進行疑難排解](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [重複屬性恢復功能](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health 代理程式安裝](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health 操作](active-directory-aadconnect-health-operations.md)
* [使用 Azure AD Connect Health 來搭配 AD FS](active-directory-aadconnect-health-adfs.md)
* [在 AD DS 使用 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health 常見問題集](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health 版本歷程記錄](active-directory-aadconnect-health-version-history.md)