---
title: "物件，為 not synchronizing tooAzure AD aaaTroubleshoot |Microsoft 文件 '"
description: "疑難排解物件為 not synchronizing tooAzure AD 的原因。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>疑難排解為 not synchronizing tooAzure AD 物件

如果物件未以預期 tooAzure AD 進行同步處理，它可能會因為幾個原因。 如果您收到錯誤電子郵件從 Azure AD，或者您看見 Azure AD Connect Health hello 時發生錯誤，然後讀取[疑難排解匯出錯誤](active-directory-aadconnect-troubleshoot-sync-errors.md)改為。 但如果您正在疑難排解 hello 物件不在 Azure AD 中的問題，然後本主題是您。 本主題描述 toofind 錯誤 hello Azure AD Connect 的內部部署元件中的同步處理。

toofind hello 錯誤，您將在一些不同的位置中順序的 hello toolook:

1. hello[作業記錄](#operations)以找出 hello 同步處理引擎所識別匯入和同步處理期間的錯誤。
2. hello[連接器空間](#connector-space-object-properties)尋找遺失的物件和同步處理錯誤。
3. hello [metaverse](#metaverse-object-properties)尋找資料相關的問題。

請先啟動 [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)，再開始進行這些步驟。

## <a name="operations"></a>作業
hello hello 同步處理服務管理員中的作業 索引標籤是您應該啟動您疑難排解的位置。 hello 作業 索引標籤會顯示 hello hello 最新的作業結果。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

hello 上半部會顯示所有執行長期的順序。 根據預設，hello 作業記錄會保留資訊 hello 過去七天，但是可以變更此設定，以 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)。 您想 toolook 任何不會顯示成功狀態的執行。 您可以變更 hello hello 標頭，即可排序。

hello**狀態**資料行是 hello 最重要的資訊並顯示 hello 執行最嚴重的問題。 以下是依照優先順序 tooinvestigate hello 最常見狀態的簡短摘要 (其中 * 表示幾個可能的錯誤字串)。

| 狀態 | 註解 |
| --- | --- |
| stopped-* |執行 hello 無法完成。 例如，如果 hello 遠端系統已關閉，且無法聯繫。 |
| stopped-error-limit |有 5,000 個以上的錯誤。 hello 執行自動已停止，因為 toohello 大量的錯誤。 |
| completed-\*-errors |hello 執行已完成，但有錯誤 (少於 5000)，應予調查。 |
| completed-\*-warnings |hello 執行完成，但某些資料不是處於 hello 預期狀態。 如果您遇到錯誤，則此訊息通常只是一個徵狀。 在您解決錯誤之前，不應該調查警告。 |
| 成功 |沒有問題。 |

當您選取一個資料列時，hello 底部更新 tooshow hello 詳細資料，執行。 toohello 最左側的 hello 底部，您可能必須清單指出**步驟 #**。 如果您的樹系中有多個網域，而每個網域都以一個步驟來代表，則只會顯示此清單。 hello 網域名稱可以找到 hello 標題底下**分割**。 在下**同步處理統計資料**，您可以找到 hello 數的變更，已處理的詳細資訊。 您可以按一下 hello 連結 tooget hello 變更物件的清單。 如果您有物件發生錯誤，這些會顯示於 [同步處理錯誤] 下方。

### <a name="troubleshoot-errors-in-operations-tab"></a>疑難排解 [作業] 索引標籤中的錯誤
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
當您遇到錯誤時，這兩個錯誤與 hello 錯誤本身中的 hello 物件會提供更多資訊的連結。

Hello 錯誤字串，即可開始 (**同步處理規則-錯誤-函式的觸發**hello 圖片中)。 您會先看到 hello 物件的概觀。 toosee hello 實際的錯誤，按一下 [hello] 按鈕**堆疊追蹤**。 這個追蹤會提供偵錯 hello 錯誤層級資訊。

您可以以滑鼠右鍵按一下 hello**呼叫堆疊資訊**方塊中，選擇**選取所有**，和**複製**。 您可以複製 hello 堆疊並查看您最愛的編輯器，例如 [記事本] 中的 hello 錯誤。

* 如果 hello 錯誤是從**SyncRulesEngine**，則第一次 hello 物件上有一份所有屬性的 hello 呼叫堆疊資訊。 向下捲動直到您看到 hello 標題**InnerException = >**。  
  ![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  hello 列之後顯示 hello 錯誤。 在上面的 hello 圖片，hello 錯誤是從建立的自訂同步處理規則 Fabrikam。

如果 hello 錯誤本身不會提供足夠的資訊，則時間 toolook 在 hello 資料本身。 您可以按一下 hello 與 hello 物件識別項的連結，繼續疑難排解 hello[連接器空間匯入的物件](#cs-import)。

## <a name="connector-space-object-properties"></a>連接器空間物件屬性
如果您沒有在 hello 中找到的任何錯誤[作業](#operations)索引標籤，那麼 hello 下一個步驟是從 Active Directory、 toohello metaverse 和 tooAzure AD toofollow hello 連接器空間物件。 在這個路徑中，您應該尋找 hello 問題所在。

### <a name="search-for-an-object-in-hello-cs"></a>Hello CS 中的物件搜尋

在**同步處理服務管理員**，按一下 **連接器**，選取 hello Active Directory 連接器，和**搜尋連接器空間**。

在**範圍**，選取**RDN** （當您想在 hello CN 屬性 toosearch） 或**DN 或錨點**（當您想 toosearch hello distinguishedName 屬性上的）。 輸入值，然後按一下 [搜尋]。  
![連接器空間搜尋](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

如果找不到 hello 物件想要則它可能已篩選與[網域型篩選](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)或[組織單位型篩選](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)。 讀取 hello[設定篩選](active-directory-aadconnectsync-configure-filtering.md)hello 篩選的主題 tooverify 會如預期完成設定。

另一個實用的搜尋中為 tooselect hello Azure AD 連接器，**範圍**選取**擱置匯入**，並選取 hello**新增**核取方塊。 此搜尋會提供您 Azure AD 中無法與內部部署物件建立關聯的所有已同步處理物件。  
![連接器空間搜尋孤立物件](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
這些物件是由另一個同步引擎所建立，或是由具有不同篩選組態的同步引擎所建立。 此檢視是一個由不再受管理的「孤立」物件所組成的清單。 您應該檢閱這份清單，並考慮移除這些物件正在使用 hello [Azure AD PowerShell](http://aka.ms/aadposh) cmdlet。

### <a name="cs-import"></a>CS 匯入
當您開啟的 cs 物件時，有數個索引標籤是 hello 頂端。 hello**匯入**索引標籤會顯示 hello 分段匯入後的資料。  
![CS 物件](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
hello**舊值**顯示目前儲存在 連接與 hello**新值**功能已從 hello 來源系統接收，且尚未套用。 如果 hello 物件上沒有錯誤，都不會處理變更。

**錯誤**  
![CS 物件](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
hello**同步處理錯誤** 索引標籤才會顯示 hello 物件發生問題。 如需詳細資訊，請參閱[針對同步處理錯誤進行疑難排解 (英文)](#troubleshoot-errors-in-operations-tab)。

### <a name="cs-lineage"></a>CS 歷程
hello 歷程索引標籤會顯示 hello 連接器空間物件的相關的 toohello metaverse 物件的方式。 您可以看到 hello 連接器上一次匯入的已變更時，hello 連接的系統，以及套用規則 toopopulate 資料在 hello metaverse。  
![CS 歷程](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
在 hello**動作**資料行中，您可以看到有一個**輸入**hello 動作的同步處理規則**佈建**。 指出只要此連接器空間物件存在於，hello metaverse 物件維持。 如果同步處理規則 hello 清單會改為顯示方向的同步處理規則**輸出**和**佈建**，它會指出當 hello metaverse 物件被刪除時，就會刪除此物件。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
您也可以在 hello 看到**PasswordSync** hello 傳入的連接器空間中的資料行可能造成變更 toohello 密碼，因為一個同步處理規則有 hello 值**True**。 此密碼，然後會傳送 hello 輸出規則透過 tooAzure AD。

Hello 歷程 索引標籤，您可以按一下以取得 toohello metaverse [Metaverse 物件屬性](#mv-attributes)。

在所有索引標籤的 hello 底部有兩個按鈕：**預覽**和**記錄**。

### <a name="preview"></a>預覽
hello 預覽頁面是使用的 toosynchronize 一個單一物件。 如果您正在疑難排解的一些自訂的同步處理規則，而且想 toosee hello 影響變更的單一物件，就會很有用。 您可以在 [完整同步處理] 和 [差異同步處理] 之間做選擇。您也可以選取之間**產生預覽**，只會 hello 變更保留在記憶體中，和**認可預覽**，其更新 hello metaverse，而且所有階段都變更 tootarget 連接器空間。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
您可以檢查 hello 物件和哪一項規則套用特定的屬性流程。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>記錄檔
hello 記錄頁面是使用的 toosee hello 密碼同步處理狀態和歷程記錄。 如需詳細資訊，請參閱[針對密碼同步處理進行疑難排解 (英文)](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)。

## <a name="metaverse-object-properties"></a>Metaverse 物件屬性
它是從 hello 來源 Active Directory 搜尋通常最好 toostart[連接器空間](#connector-space)。 不過，您也可以開始從 hello metaverse 搜尋。

### <a name="search-for-an-object-in-hello-mv"></a>Hello MV 中的物件搜尋
在 [Synchronization Service Manager] 中，按一下 [Metaverse 搜尋]。 建立查詢，您會知道找到 hello 使用者。 您可以搜尋通用的屬性，例如 accountName (sAMAccountName) 和 userPrincipalName。 如需詳細資訊，請參閱 [Metaverse 搜尋](active-directory-aadconnectsync-service-manager-ui-mvsearch.md)。
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

在 hello**搜尋結果**視窗中，按一下 hello 物件。

如果您找不到 hello 物件，然後它尚未到達 hello metaverse。 繼續 hello Active Directory 中的 hello 物件 toosearch[連接器空間](#connector-space-object-properties)。 可能封鎖了未來 toohello metaverse 中的 hello 物件的同步處理發生錯誤，或可能套用的篩選。

### <a name="mv-attributes"></a>MV 屬性
Hello 屬性索引標籤上，您可以查看 hello 值，而哪些連接器貢獻它。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

如果物件未進行同步處理，然後查看 hello 下列 hello metaverse 中的屬性：
- Hello 屬性**cloudFiltered**存在並設太**true**嗎？ 如果是，則它已經篩選 toohello 步驟中的，根據[屬性型篩選](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering)。
- Hello 屬性**sourceAnchor**存在嗎？ 如果不存在，您是否擁有帳戶資源樹系拓撲？ 如果物件識別為連結信箱 (hello 屬性**msExchRecipientTypeDetails** hello 值 2)，然後 hello 與啟用的 Active Directory 帳戶的樹系提供 hello sourceAnchor。 請確定已匯入並正確地同步處理 hello 主要帳戶。 hello 主帳戶必須列在 hello[連接器](#mv-connectors)hello 物件。

### <a name="mv-connectors"></a>MV 連接器
hello 連接器 索引標籤會顯示有 hello 物件的表示法的所有連接器空間。  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
您應該要有連至下列各項的連接器：

- 每個 Active Directory 樹系 hello 使用者都會在。 這項呈現可以包括 foreignSecurityPrincipals 和 Contact 物件。
- Azure AD 中的連接器。

如果您遺漏 hello 連接器 tooAzure AD，然後讀取[MV 屬性](#MV-attributes)tooverify hello 準則所佈建 tooAzure AD。

此索引標籤也可讓您 toonavigate toohello[連接器空間物件](#connector-space-object-properties)。 請選取一個資料列，然後按一下 [屬性]。

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
