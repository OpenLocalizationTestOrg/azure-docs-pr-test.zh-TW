---
title: "Azure AD Connect 同步：在 Azure AD Connect 同步中進行組態變更 | Microsoft Docs"
description: "逐步解說如何 toomake 變更 toohello 設定在 Azure AD Connect 同步處理。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Azure AD Connect 同步： 如何變更 toohello toomake 預設組態
本主題的 hello 目的是 toowalk 您透過 toomake 如何變更 toohello 預設組態，在 Azure AD Connect 同步處理。其中提供一些常見案例的步驟。 這項知識，您應該能夠 toomake 一些簡單的變更 tooyour 擁有自己的商務規則為基礎的組態。

## <a name="synchronization-rules-editor"></a>同步處理規則編輯器
hello 同步處理規則編輯器是使用的 toosee 和變更 hello 預設組態。 您可以在 hello 開始 功能表底下 hello **Azure AD Connect**群組。  
![內含同步處理規則編輯器的開始功能表](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

當您開啟它時，您會看到 hello 預設鶈蜪規則。

![同步處理規則編輯器](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>在 hello 編輯器中巡覽
hello 下拉式清單頂端 hello hello 編輯器可讓您 tooquickly 尋找特定的規則。 例如，如果您想 hello 屬性 proxyAddresses 隨附的其中 toosee hello 規則時，會變更 hello 下拉式清單 toohello 下列：  
![SRE 篩選](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
tooreset 篩選和載入全新的組態，請按**F5** hello 鍵盤上。

有按鈕 toohello 右上方，**加入新規則**。 這個按鈕會使用的 toocreate 您自己自訂的規則。

Hello 底部中，您會有作用的按鈕上選取的同步處理規則。 [編輯] 和 [刪除] 會如您預期般執行。 **匯出**產生的 PowerShell 指令碼重新建立 hello 同步處理規則。 此程序可讓您 toomove 從一個伺服器 tooanother 的同步處理規則。

## <a name="create-your-first-custom-rule"></a>建立您的第一個自訂規則
hello 最常見的變更是變更 toohello 屬性流程。 來源目錄中的 hello 資料可能無法如 Azure AD 所示。 在本節中的 hello 範例，您想確定 hello 指定名稱的使用者一律會處於 toomake**適當的大小寫**。

### <a name="disable-hello-scheduler"></a>停用 hello 排程器
hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)預設會每隔 30 分鐘執行。 您想 toomake 確定無法啟動時要進行變更，以及疑難排解您的新規則。 tootemporarily 停用 hello 排程器，啟動 PowerShell 並執行`Set-ADSyncScheduler -SyncCycleEnabled $false`

![停用 hello 排程器](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>建立 hello 規則
1. 按一下 [新增規則] 。
2. 在 hello**描述**頁面上，輸入 hello 下列：  
   ![輸入規則篩選](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * 名稱： 授與 hello 規則的描述性名稱。
   * 描述： 適用於某些釐清，讓其他人可以了解哪些 hello 規則。
   * 連線系統： 位於 hello 系統 hello 物件。 在此情況下，選取 hello Active Directory 連接器。
   * 已連線的系統/Metaverse 物件類型︰分別選取 [使用者] 和 [人員]。
   * 連結類型： 變更此值太**聯結**。
   * 優先順序： 提供在 hello 系統中是唯一的值。 較低的數值表示優先順序較高。
   * 標籤︰保留空白。 只有 Microsoft 提供的現成可用規則應該在此方塊中填入值。
3. 在 hello**範圍篩選**頁面上，輸入**givenName ISNOTNULL**。  
   ![輸入規則範圍篩選器](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   此區段是哪些物件 hello 規則應該套用至使用的 toodefine。 如果空白，hello 規則將會套用 tooall 使用者物件。 但會包括會議室、服務帳戶，以及其他非人員的使用者物件。
4. 在 hello**聯結規則**，保持空白。
5. 在 hello**轉換**頁面上，也變更 hello FlowType**運算式**。 選取 hello 目標屬性**givenName**，在來源輸入`PCase([givenName])`。
   ![輸入規則轉換](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   hello 同步處理引擎會同時在 hello 函式名稱與 hello hello 屬性名稱區分大小寫。 如果您輸入錯誤，當您將加入 hello 規則看到警告。 hello 編輯器可讓您 toosave，並繼續進行，因此，您必須 tooreopen hello 規則與正確的 hello 規則。
6. 按一下**新增**toosave hello 規則。

新的自訂規則應該顯示以 hello 其他同步 hello 系統中的規則。

### <a name="verify-hello-change"></a>確認 hello 變更
這個新的變更，您會想 toomake 確定它正常運作，而且不會擲回任何錯誤。 根據 hello 您擁有的物件數目，有兩個不同的方式 toodo 此步驟。

1. 在所有物件上執行完整同步處理
2. 在單一物件上執行預覽和完整同步處理

啟動**同步處理服務**從 hello [開始] 功能表。 本節中的 hello 步驟都位於這項工具。

1. **所有物件的完整同步處理**  
   選取**連接器**hello 頂端。 識別 hello 連接器，您所做的變更 tooin hello 前一節，在此情況下 hello Active Directory 網域服務，並加以選取。 從 [動作] 中選取 [執行]，然後選取 [完整同步處理] 和 [確定]。
   ![完整同步處理](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   hello 物件現在會 hello metaverse 中更新。 現在，您會想 toolook hello hello metaverse 中的物件。
2. **單一物件的預覽和完整同步處理**  
   選取**連接器**hello 頂端。 識別 hello 連接器，您所做的變更 tooin hello 前一節，在此情況下 hello Active Directory 網域服務，並加以選取。 選取 [搜尋連接器空間] 。 使用範圍 toofind 想要 toouse tootest hello 變更的物件。 選取 hello 物件，然後按一下 **預覽**。 在 hello 新畫面上，選取 **認可預覽**。  
   ![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   hello 變更已認可的 toohello metaverse。

**查看 hello metaverse 中的 hello 物件**  
您現在想的 toopick 少數範例物件 toomake 確定 hello 預期值和套用該 hello 規則。 選取**Metaverse 搜尋**從 hello。 新增任何篩選，您必須 toofind hello 相關物件。 Hello 搜尋結果中，從開啟的物件。 查看 hello 屬性值，並也確認在 hello**同步處理規則**hello 如預期般套用規則的資料行。  
![Metaverse 搜尋](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>啟用 hello 排程器
如果一切如預期般，您可以再次啟用 hello 排程器。 從 PowerShell，執行 `Set-ADSyncScheduler -SyncCycleEnabled $true`。

## <a name="other-common-attribute-flow-changes"></a>其他常見屬性流程變更
hello 上一節所述 toomake 如何變更 tooan 屬性流程。 本節提供了一些其他的範例。 hello 步驟縮寫 toocreate hello 同步處理規則的方式，但是您可以在 hello 上一節中找到 hello 完整步驟。

### <a name="use-another-attribute-than-hello-default"></a>使用其他比 hello 預設屬性
Fabrikam，沒有其中 hello 本機字母用於名字、 姓氏和顯示名稱的樹系。 hello 拉丁字元表示法，這些屬性可以找到 hello 延伸模組屬性中。 在 Azure AD 中建立 hello 全域通訊清單時，Office 365 hello 的組織想要改為使用這些屬性 toobe。

使用預設設定時，將物件從本機樹系 hello 看起來像這樣：  
![屬性流程 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

toocreate 其他屬性，流量的規則 hello 遵循：

* 啟動**同步處理規則編輯器**從 hello [開始] 功能表。
* 與**輸入**仍然選取的 toohello hello 按鈕上按一下滑鼠左鍵，**加入新規則**。
* 為 hello 規則提供名稱和描述。 選取 hello 在內部部署 Active Directory 和 hello 相關的物件類型。 在 [連結類型] 中，選取 [聯結]。 為優先順序挑選一個其他規則還沒使用的數字。 hello 鶈蜪規則的開頭 100，因此在此範例中，就可以使用 hello 值 50。
  ![屬性流程 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* 將領域保留空白 （也就是應該套用 tooall hello 樹系中的使用者物件）。
* 保留 聯結規則空白 （也就，可讓任何聯結 hello 鶈蜪規則控制代碼）。
* 在轉換、 建立 hello 下列流程：  
  ![屬性流程 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* 按一下**新增**toosave hello 規則。
* 跳過**同步處理服務管理員**。 在**連接器**，選取 hello 的連接器我們加入 hello 規則的位置。 依序選取 [執行] 和 [完整同步處理]。 完整同步處理重新計算使用 hello 目前規則的所有物件。

以下是相同的物件與此自訂規則的 hello 的 hello 結果：  
![屬性流程 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>屬性的長度
字串屬性可索引的預設集 toobe 並使用 hello 最大長度為 448 個字元。 如果您正在使用可能包含多個字串屬性，然後在 hello 屬性流程中進行確定 tooinclude hello 下列：  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>變更 hello userPrincipalSuffix
Active Directory 中的 hello userPrincipalName 屬性永遠不知道 hello 使用者，且可能不適合 hello 登入識別碼。 hello Azure AD Connect 同步作業安裝精靈允許挑選不同的屬性，例如郵件。 但在某些情況下 hello 必須計算屬性。 例如，Contoso 的 hello 公司有兩個 Azure AD 目錄，一個用於生產環境，另一個用於測試。 他們想 hello 使用者在其測試租用戶 toouse 另一個後的置詞 hello 登入識別碼。  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

在此運算式中，接受所有項目第一次方的 hello @-sign (Word) 和具有固定的字串串連。

### <a name="convert-a-multi-value-tooa-single-value"></a>將多重值 tooa 單一值的轉換
雖然看起來單一 Active Directory 使用者和電腦中的值，Active Directory 中的某些屬性是多重值 hello 結構描述中。 例如，hello 描述屬性。  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

在此運算式以防 hello 屬性有值，需要 hello 屬性中的 hello 第一個項目 (Item) 移除開頭和尾端空白 (Trim)，然後再保留 hello 前 448 個字元 （左） hello 字串中。

### <a name="do-not-flow-an-attribute"></a>請勿傳送屬性
如需有關本章節的 hello 案例的背景，請參閱[控制 hello 屬性流程程序](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process)。

有兩種 toonot 流程屬性。 hello 第一次是 hello 安裝精靈 中，並可讓您太[移除選取的屬性](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering)。 此選項適用於您永遠不會同步處理之前的 hello 屬性。 不過，如果您已經啟動 toosynchronize 這個屬性，稍後又將它移除這項功能，然後 hello 同步處理引擎會停止管理 hello 屬性，而且 hello 現有的值也會保留在 Azure AD。

如果您想 tooremove hello 屬性值，請確定它不會在未來的 hello 流動時，您需要改為建立自訂規則。

Fabrikam，我們知道的某些屬性我們同步 toohello 雲端的 hello 不應該有。 我們想要 toomake 確定這些屬性會從 Azure AD 中移除。  
![不正確的擴充屬性](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* 建立新的輸入同步處理規則，並填入 hello 描述![描述](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* 建立類型的屬性流程**運算式**與 hello 來源**AuthoritativeNull**。 常值的 hello **AuthoritativeNull**指出 hello 值應空白 hello MV 中，即使較低的優先順序同步處理規則會嘗試 toopopulate hello 值。
  ![擴充屬性的轉換](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* 儲存 hello 的同步處理規則。 啟動**同步處理服務**、 尋找 hello 連接器，請選擇**執行**，和**完整同步處理**。 此步驟會重新計算所有屬性流程。
* 請確認該 hello 適合變更即將 toobe 匯出搜尋 hello 連接器空間。
  ![分段刪除](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>使用 PowerShell 建立規則
使用 hello 同步處理規則編輯器會正常運作時，您只需要少數變更 toomake。 如果您需要 toomake 許多變更，則 PowerShell 可能會更好的選項。 某些進階功能只有 PowerShell 才提供。

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>取得 hello PowerShell 指令碼的預設規則
toosee hello hello 同步處理中建立的預設規則、 選取 hello 規則的 PowerShell 指令碼規則編輯器，然後按一下**匯出**。 這個動作可讓您 hello PowerShell 指令碼該建立的 hello 規則。

### <a name="advanced-precedence"></a>進階優先順序
hello 現成的同步處理規則的優先順序值為 100 開頭。 如果您有多個樹系，而且需要 toomake 許多自訂變更，然後 99 的同步處理規則可能不太夠。

您可以指示 hello hello 鶈蜪規則之前插入的其他規則的同步處理引擎。 tooget 這種行為，請遵循下列步驟：

1. 標記 hello 第一個現成的同步處理規則 (此規則為 hello**中從 AD 使用者將聯結**) 在 hello 同步處理規則編輯器，再選取**匯出**。 複製 hello SR 識別碼值。  
![變更前的 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. 建立 hello 新同步處理規則。 您可以使用 hello 同步處理規則編輯器 toocreate 它。 匯出 hello 規則 tooa PowerShell 指令碼。
3. 在 hello 屬性**PrecedenceBefore**，插入 hello 鶈蜪規則 hello 識別碼值。 設定 hello**優先順序**太**0**。 請確定 hello 識別碼屬性都是唯一而且不會重複使用另一項規則中的 GUID。 同時確定該 hello **ImmutableTag**屬性未設定; 這個屬性只應設定的預設規則。 儲存 hello PowerShell 指令碼並執行它。 100 hello 優先順序值指派給您的自訂規則，而所有其他預設的規則就會遞增 hello 結果。  
![變更後的 PowerShell](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

您可以有許多自訂同步處理規則使用相同的 hello **PrecedenceBefore**時所需的值。


## <a name="enable-synchronization-of-preferreddatalocation"></a>啟用 PreferredDataLocation 的同步處理
Azure AD Connect 可支援同步處理的 hello **PreferredDataLocation**屬性**使用者**1.1.524.0 版本和之後的物件。 更具體地說，我們已導入下列變更︰

* hello hello 物件類型的結構描述**使用者**hello 在 Azure AD Connector 延伸 tooinclude PreferredDataLocation 屬性，這是字串類型的單一值。

* hello hello 物件類型的結構描述**人員**在 hello Metaverse 延伸 tooinclude PreferredDataLocation 屬性，這是字串類型的單一值。

根據預設，hello PreferredDataLocation 屬性不是啟用同步處理，因為在內部部署 Active Directory 中沒有對應的 PreferredDataLocation 屬性。 您必須手動啟用同步處理。

> [!IMPORTANT]
> 目前，Azure AD 可讓已同步處理使用者物件和雲端使用者物件 toobe 直接使用 Azure AD PowerShell 來設定上的 hello PreferredDataLocation 屬性。 一旦您啟用了 hello PreferredDataLocation 屬性的同步處理，您必須停止使用 Azure AD PowerShell tooconfigure hello 屬性上**同步處理使用者物件**為 Azure AD Connect 會覆寫根據在內部部署 Active Directory 中的 hello 來源屬性值。

> [!IMPORTANT]
> 在 1 2017 年 9 月，Azure AD 就不再允許 hello PreferredDataLocation 屬性上**同步處理使用者物件**toobe 直接使用 Azure AD PowerShell 來設定。 tooconfigure PreferredLocation 屬性上的同步處理使用者物件，您必須使用 Azure AD Connect 只。

在啟用之前 hello PreferredDataLocation 屬性的同步處理，您必須：

 * 首先，決定用來當做 hello 來源屬性的內部部署 Active Directory 屬性 toobe。 此屬性的類型必須是**字串**，且具備**單一值**。

 * 如果您先前已設定 hello PreferredDataLocation 屬性上現有的同步處理，使用 Azure AD PowerShell 的 Azure AD 使用者物件，您必須**backport** hello 屬性值 toohello 對應使用者物件在內部部署 Active Directory。
 
    > [!IMPORTANT]
    > 如果您不要使用 backport hello 屬性值 toohello 對應使用者物件在內部部署 Active Directory 中的，Azure AD Connect 的 hello PreferredDataLocation 屬性同步處理時的 Azure AD 中將會移除 hello 現有屬性值啟用。

 * 建議您設定 hello 來源屬性上至少有幾個內部部署 AD 使用者物件，它可以用來驗證稍後。
 
hello hello PreferredDataLocation 屬性的步驟 tooenable 同步處理可以摘要如下：

1. 停用同步排程器，並確認沒有任何同步處理在進行中

2. 新增 hello 來源屬性 toohello 內部部署 AD 連接器結構描述

3. 新增 PreferredDataLocation toohello Azure AD Connector 結構描述

4. 從內部部署 Active Directory 中建立輸入同步處理規則 tooflow hello 屬性值

5. 建立輸出同步處理規則 tooflow hello 屬性值 tooAzure AD

6. 執行完整的同步處理週期

7. 啟用同步排程器

> [!NOTE]
> hello 本節其餘部分涵蓋這些詳細資料中的步驟。 Azure AD 部署單一樹系拓撲時或無自訂同步處理規則的 hello 內容將描述這些。 如果您有多樹系拓撲時，自訂同步處理規則設定，或已在臨時伺服器，您需要據此 tooadjust hello 步驟。

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>步驟 1：停用同步排程器，並確認沒有任何同步處理在進行中
請確定沒有同步處理的更新同步處理的 hello 中間時，會發生非預期的規則 tooavoid 變更正在執行匯出 tooAzure AD。 toodisable hello 內建的同步處理排程器：

 1. Hello Azure AD Connect 的伺服器上啟動 PowerShell 工作階段。

 2. 執行 Cmdlet 以停用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. 啟動 hello**同步處理服務管理員**移 tooSTART → 所同步處理服務。
 
 4. 移 toohello**作業**索引標籤上，並確認其狀態是沒有作業*「 進行中 」。*

![同步處理服務管理員 - 確認沒有進行中的作業](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>步驟 2： 新增 hello 來源屬性 toohello 內部部署 AD 連接器結構描述
並非所有的 AD 屬性會匯入至 hello 內部部署 AD 連接器空間。 tooadd hello 來源 toohello 的屬性清單 hello 匯入的屬性：

 1. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。
 
 2. 以滑鼠右鍵按一下 hello**在內部部署 AD 連接器**選取**屬性**。
 
 3. 在 [hello 快顯對話方塊中，移 toohello**選取屬性**] 索引標籤。
 
 4. 請確定 hello 屬性清單中，核取 hello 來源屬性。
 
 5. 按一下**確定**toosave。

![新增來源屬性 tooon 內部部署 AD 連接器結構描述](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>步驟 3： 加入 PreferredDataLocation toohello Azure AD Connector 結構描述
根據預設，hello PreferredDataLocation 屬性不會匯入 hello Azure AD Connect 的空間。 tooadd hello PreferredDataLocation 屬性 toohello 清單匯入的屬性：

 1. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。

 2. 以滑鼠右鍵按一下 hello **Azure AD Connector**選取**屬性**。

 3. 在 [hello 快顯對話方塊中，移 toohello**選取屬性**] 索引標籤。

 4. 請確定 hello PreferredDataLocation 屬性已簽入 hello 屬性清單。

 5. 按一下**確定**toosave。

![新增來源屬性 tooAzure AD 連接器結構描述](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>步驟 4： 從內部部署 Active Directory 中建立輸入同步處理規則 tooflow hello 屬性值
允許從內部部署 Active Directory toohello Metaverse hello 來源屬性 hello 屬性值 tooflow hello 輸入同步處理規則：

1. 啟動 hello**同步處理規則編輯器**移 tooSTART → 所同步處理規則編輯器。

2. 集 hello 搜尋篩選器**方向**toobe**輸入**。

3. 按一下**加入新規則**按鈕 toocreate 新的輸入規則。

4. 在 hello**描述**索引標籤上，提供下列組態的 hello:
 
    | 屬性 | 值 | 詳細資料 |
    | --- | --- | --- |
    | 名稱 | 提供名稱 | 例如，「In from AD – User PreferredDataLocation」 |
    | 說明 | 提供描述 |  |
    | 連線系統 | *挑選 hello 內部部署 AD 連接器* |  |
    | 連線系統物件類型 | **使用者** |  |
    | Metaverse 物件類型 | **人員** |  |
    | 連結類型 | **Join** |  |
    | 優先順序 | 選擇 1 - 99 之間的數字 | 1 - 99 已保留供自訂同步處理規則使用。 請勿挑選已由其他同步處理規則使用的值。 |

5. 移 toohello**範圍篩選**索引標籤和加入**以 hello 子句之後的單一範圍篩選群組**:
 
    | 屬性 | 運算子 | 值 |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | 使用者\_ | 
 
    範圍篩選器會決定此輸入同步處理規則要套用至哪個內部部署 AD 物件。 在此範例中，我們會使用做為相同的範圍篩選器的 hello *」 在 from AD – 使用者一般"* OOB 同步處理規則，可以防止 hello 同步處理規則套用 tooUser 透過 Azure AD 使用者回寫所建立的物件功能。 您可能需要根據 Azure AD Connect 部署 tooyour tootweak hello 範圍篩選。

6. 移 toohello**轉換索引標籤**並實作 hello 下列轉換規則：
 
    | 流程類型 | 目標屬性 | 來源 | 套用一次 | 合併類型 |
    | --- | --- | --- | --- | --- |
    | 直接 | PreferredDataLocation | 挑選 hello 來源屬性 | 未核取 | 更新 |

7. 按一下**新增**toocreate hello 輸入的規則。

![建立輸入同步處理規則](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>步驟 5： 建立輸出同步處理規則 tooflow hello 屬性值 tooAzure AD
hello 輸出同步處理規則允許 hello Metaverse toohello PreferredDataLocation 屬性從 Azure AD 中的 hello 屬性值 tooflow:

1. 移 toohello**同步處理規則**編輯器。

2. 集 hello 搜尋篩選器**方向**toobe**輸出**。

3. 按一下 [新增規則] 按鈕。

4. 在 hello**描述**索引標籤上，提供下列組態的 hello:

    | 屬性 | 值 | 詳細資料 |
    | --- | --- | --- |
    | 名稱 | 提供名稱 | 例如，「 出 tooAAD – 使用者 PreferredDataLocation" |
    | 說明 | 提供描述 |
    | 連線系統 | *選取 hello AAD 連接器* |
    | 連線系統物件類型 | User ||
    | Metaverse 物件類型 | **人員** ||
    | 連結類型 | **Join** ||
    | 優先順序 | 選擇 1 - 99 之間的數字 | 1 - 99 已保留供自訂同步處理規則使用。 請勿挑選已由其他同步處理規則使用的值。 |

5. 移 toohello**範圍篩選**索引標籤和加入**單一範圍篩選群組與兩個子句**:
 
    | 屬性 | 運算子 | 值 |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | User |
    | cloudMastered | NOTEQUAL | True |

    範圍篩選器會決定此輸出同步處理規則要套用至哪個 Azure AD 物件。 在此範例中，我們使用 hello 相同的範圍篩選器，「 出 tooAD – 使用者身分識別 」 從 OOB 同步處理規則。 它會防止 hello 同步處理規則要套用的 tooUser 物件未從內部部署 Active Directory 同步處理。 您可能需要根據 Azure AD Connect 部署 tooyour tootweak hello 範圍篩選。
    
6. 移 toohello**轉換**索引標籤上，並實作 hello 下列轉換規則：

    | 流程類型 | 目標屬性 | 來源 | 套用一次 | 合併類型 |
    | --- | --- | --- | --- | --- |
    | 直接 | PreferredDataLocation | PreferredDataLocation | 未核取 | 更新 |

7. 關閉**新增**toocreate hello 輸出規則。

![建立輸出同步處理規則](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>步驟 6：執行完整的同步處理週期
一般情況下，完整的同步處理循環是必要，因為我們加入了新的屬性 tooboth hello AD 和 Azure AD Connector 結構描述，並導入了自訂同步處理規則。 建議您之前匯出 tooAzure AD，驗證 hello 變更。 您可以使用下列步驟 tooverify hello 變更時以手動方式執行 hello 步驟組成完整的同步處理循環的 hello。 

1. 執行**完整匯入**步驟 hello**在內部部署 AD 連接器**:

   1. 移 toohello**作業**hello 同步處理服務管理員中的索引標籤。

   2. 以滑鼠右鍵按一下 hello**在內部部署 AD 連接器**選取**執行...**

   3. 在 hello 快顯對話方塊中，選取 **完整匯入**按一下**確定**。
    
   4. 等候作業 toocomplete。

    > [!NOTE]
    > 您可以在略過完整匯入 hello 內部部署 AD 連接器如果 hello 來源屬性已包含在 hello 匯入的屬性清單中。 換句話說，您不需要 toomake 期間的任何變更[步驟 2： 新增 hello 來源屬性 toohello 內部部署 AD 連接器架構](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema)。

2. 執行**完整匯入**步驟 hello **Azure AD Connector**:

   1. 以滑鼠右鍵按一下 hello **Azure AD Connector**選取**執行...**

   2. 在 hello 快顯對話方塊中，選取 **完整匯入**按一下**確定**。
   
   3. 等候作業 toocomplete。

3. 請確認現有的使用者物件上的 hello 同步處理規則變更：

hello 來源屬性從內部部署 Active Directory 與 Azure AD 從 PreferredDataLocation 已匯入 hello 各自的連接器空間。 完整同步處理步驟之前，建議您不要**預覽**上現有的使用者物件中 hello 內部部署 AD 連接器空間。 您挑選的 hello 物件應該填入 hello 來源屬性。 成功**預覽**以 hello PreferredDataLocation hello Metaverse 中填入是 hello 同步處理規則的設定正確的良好指標。 如需有關資訊 toodo**預覽**，請參閱 toosection[驗證 hello 變更](#verify-the-change)。

4. 執行**完整同步處理**步驟 hello**在內部部署 AD 連接器**:

   1. 以滑鼠右鍵按一下 hello**在內部部署 AD 連接器**選取**執行...**
  
   2. 在 hello 快顯對話方塊中，選取**完整同步處理**按一下**確定**。
   
   3. 等候作業 toocomplete。

5. 確認**暫停匯出**tooAzure AD:

   1. 以滑鼠右鍵按一下 hello **Azure AD Connector**選取**搜尋連接器空間**。

   2. 在 hello 搜尋連接器空間快顯對話方塊：

      1. 設定**範圍**太**暫止匯出**。
      
      2. 將 3 個核取方塊全部勾選，包括 [新增]、[修改] 和 [刪除]。
      
      3. 按一下 hello**搜尋**按鈕 tooget hello 清單具有變更 toobe 匯出的物件。 tooexamine hello 變更之特定物件，連按兩下 hello 物件。
      
      4. 請確認預期 hello 變更。

6. 執行**匯出**步驟 hello **Azure AD Connector**
      
   1. 以滑鼠右鍵按一下 hello **Azure AD Connector**選取**執行...**
   
   2. 在 hello 執行連接器快顯對話方塊中，選取 **匯出**按一下**確定**。
   
   3. 等候匯出 tooAzure AD toocomplete。

> [!NOTE]
> 您可能會注意到 hello 步驟不包含 hello 完整同步處理步驟和 hello Azure AD Connector 的 「 匯出 」 步驟。 因為從內部部署 Active Directory tooAzure AD 只傳送 hello 屬性值，則不需要 hello 步驟。

### <a name="step-7-re-enable-sync-scheduler"></a>步驟 7：重新啟用同步排程器
重新啟用 hello 內建的同步處理排程器：

1. 啟動 PowerShell 工作階段。

2. 執行 Cmdlet 以重新啟用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>後續步驟
* 深入了解 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。
* 如需詳細資訊中的 hello 運算式語言[了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)。

**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
