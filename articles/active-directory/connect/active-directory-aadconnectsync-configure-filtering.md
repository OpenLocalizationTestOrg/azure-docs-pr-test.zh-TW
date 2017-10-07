---
title: "Azure AD Connect 同步：設定篩選 | Microsoft Docs"
description: "說明如何在 Azure AD Connect 同步處理篩選 tooconfigure。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect 同步處理：設定篩選
使用篩選功能可讓您控制內部部署目錄中的哪些物件應該出現在 Azure Active Directory 中。 hello 預設組態會 hello 設定樹系中的所有網域中的所有物件。 一般情況下，這是建議的組態 hello。 完整的全域通訊清單對於使用 Exchange Online 和商務用 Skype 等 Office 365 工作負載的使用者來說十分方便，因為如此一來，他們就可以傳送電子郵件和呼叫每個人。 Hello 預設組態，他們必須使用相同的經驗，他們必須在內部部署 Exchange 或 Lync 實作 hello。

在某些情況下不過，您需要進行一些變更 toohello 預設設定。 這裡有一些範例：

* 您計劃 toouse hello[多 Azure AD 目錄拓撲](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant)。 然後，您需要 tooapply 篩選 toocontrol 哪個物件處於已同步處理的 tooa 特定 Azure AD 目錄。
* 您要執行 Azure 或 Office 365 試驗，因此只想要使用 Azure AD 中的部分使用者。 在 hello 小型試驗，就不重要 toohave 完整的全域通訊清單 toodemonstrate hello 功能。
* Azure AD 中有很多您不需要的服務帳戶和其他非個人帳戶。
* 為了符合法規，您不能刪除任何內部部署的使用者帳戶。 你只能停用它們。 但在 Azure AD 中，您只想使用中帳戶 toobe 存在。

本文件涵蓋如何 tooconfigure hello 不同篩選方法。

> [!IMPORTANT]
> Microsoft 不支援修改或操作正式記載的 hello 動作之外的 Azure AD Connect 同步處理。 任何這些動作都可能會導致 Azure AD Connect 同步處理的不一致或不受支援狀態。如此一來，Microsoft 無法提供這類部署的技術支援人員。

## <a name="basics-and-important-notes"></a>基本概念和重要事項
在 Azure AD Connect 同步處理中，您隨時都能啟用篩選功能。 如果您使用預設設定的目錄同步作業啟動，然後設定 篩選時，會被篩選掉的 hello 物件不再同步的 tooAzure AD。 因為這項變更，系統會在 Azure AD 中，刪除 Azure AD 中先前已同步處理但接著篩選出的所有物件。

開始進行的變更 toofiltering 之前，請確定您[停用排程的工作的 hello](#disable-scheduled-task)讓您不小心不要匯出您還沒有尚未確認 toobe 正確的變更。

因為篩選可以移除在 hello 的許多物件相同的時間，您想要確定新的篩選器都正確無誤，然後再開始匯出任何 toomake 變更 tooAzure AD。 在您完成 hello 組態步驟之後，我們強烈建議您遵循 hello[驗證步驟](#apply-and-verify-changes)您匯出，並讓變更 tooAzure AD 之前。

您無法刪除許多物件不小心 hello tooprotect 功能 」[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)」 預設為開啟。 如果您刪除到期的許多物件 toofiltering (依預設 500)，您需要在此發行項 tooallow hello toofollow hello 步驟刪除 toogo 透過 tooAzure AD。

如果您使用組建 2015 年 11 月之前 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250))、 進行變更 tooa 篩選組態，並使用密碼同步處理，則您需要 tootrigger 完整同步處理所有密碼之後您已經完成 hello 設定。 如需如何 tootrigger 密碼完整同步處理步驟，請參閱[觸發完整同步處理所有密碼](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords)。 如果您要建置 1.0.9125 或更新版本中，然後 hello regular**完整同步處理**動作也會計算是否應該同步處理密碼，以及是否不再需要這個額外步驟。

如果**使用者**而意外刪除物件在 Azure AD 中由於篩選錯誤，您可以重新建立 hello 使用者物件在 Azure AD 中移除篩選組態。 然後您可以再次同步處理您的目錄。 這個動作會從 hello 資源回收筒還原 hello 使用者，在 Azure AD 中。 不過，您無法取消刪除其他物件類型。 例如，如果您不小心刪除安全性群組，而它是使用的 tooACL 資源，hello 群組和其 Acl 無法復原。

Azure AD Connect 只會刪除它一次被視為 toobe 範圍中的物件。 如果 Azure AD 中有物件是由另一個同步處理引擎所建立且不在範圍內，則新增篩選並不會移除這些物件。 例如，如果您開始在 Azure AD 中建立您的整個目錄的完整副本的 DirSync 伺服器，而且您安裝新的 Azure AD Connect 同步處理伺服器以平行方式從 hello 開頭啟用篩選條件時，Azure AD Connect 並不會移除額外的 hello以 DirSync 所建立的物件。

當您安裝或升級 Azure AD Connect tooa 較新版本時，會保留 hello 篩選組態。 其永遠 hello 組態的最佳作法 tooverify 不慎未變更後的第一次同步處理循環執行 hello 之前升級 tooa 較新版本。

如果您有多個樹系，則您必須套用篩選此主題 tooevery 樹系中所述設定的 hello (假設您想要 hello 相同所有組態)。

### <a name="disable-hello-scheduled-task"></a>停用 hello 排定的工作
toodisable hello 內建排程器觸發 un ciclo de sincronización 每隔 30 分鐘，請遵循下列步驟：

1. 移 tooa PowerShell 命令提示字元。
2. 執行`Set-ADSyncScheduler -SyncCycleEnabled $False`toodisable hello 排程器。
3. 變更 hello 會記載在本文中。
4. 執行`Set-ADSyncScheduler -SyncCycleEnabled $True`tooenable hello 排程器一次。

**如果您使用 1.1.105.0 之前的 Azure AD Connect 組建**  
toodisable hello 排程的工作的觸發程序 un ciclo de sincronización 每隔三小時，請遵循下列步驟：

1. 啟動**工作排程器**從 hello**啟動**功能表。
2. 直接在**工作排程器程式庫**，尋找名為 「 hello 任務**Azure AD Sync Scheduler**，按一下滑鼠右鍵，然後選取**停用**。  
   ![](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. 您現在可以進行組態變更，並從 hello 手動執行 hello 同步處理引擎**同步處理服務管理員**主控台。

完成篩選的所有變更之後，別忘了回 toocome 和**啟用**hello 工作一次。

## <a name="filtering-options"></a>篩選選項
您可以套用下列篩選組態類型 toohello 目錄同步作業工具的 hello:

* [**群組為基礎**](#group-based-filtering)： 單一的群組為基礎的篩選只能設定初始安裝上使用 hello 安裝精靈。
* [**網域型**](#domain-based-filtering)： 使用此選項，您可以選取哪些網域同步處理 tooAzure AD。 您也可以加入和從 hello 同步作業引擎組態移除網域，當您安裝 Azure AD Connect 同步處理之後，請變更 tooyour 在內部部署基礎結構。
* [**組織單位 (OU) – 基礎**](#organizational-unitbased-filtering)： 使用此選項，您可以選取哪些 Ou 同步 tooAzure AD。 此選項會套用在所選組織單位中的所有物件類型上。
* [**屬性為基礎**](#attribute-based-filtering)： 使用此選項，您可以篩選根據 hello 物件上的屬性值的物件。 您也可以讓不同物件類型透用不同篩選器。

您可以使用多個篩選選項 hello 在相同的時間。 例如，您可以使用組織單位型篩選 tooonly 包含一個 OU 中的物件。 在 hello 相同時間，您可以進一步使用屬性型篩選 toofilter hello 物件。 當您使用多個篩選的方法時，hello 篩選器會使用邏輯"AND"hello 篩選之間。

## <a name="domain-based-filtering"></a>網域型篩選
本章節提供您與 hello 步驟 tooconfigure 網域篩選。 如果您加入或移除網域樹系中，安裝 Azure AD Connect 之後，您也可以 tooupdate hello 篩選組態。

hello 慣用的方式 toochange 網域為基礎的篩選不執行 hello 安裝精靈，並將變更[網域和 OU 篩選](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)。 hello 安裝精靈會自動記錄在本主題的所有 hello 工作。

如果您因為某種原因無法 toorun hello 安裝精靈，您只應該遵循這些步驟。

網域型篩選組態包含下列步驟：

1. [選取 hello 網域](#select-domains-to-be-synchronized)想 tooinclude hello 同步處理。
2. 如需每個加入和移除網域，調整 hello[執行設定檔](#update-run-profiles)。
3. [套用並驗證變更](#apply-and-verify-changes)。

### <a name="select-hello-domains-toobe-synchronized"></a>選取 hello 網域 toobe 同步處理
tooset hello 網域篩選，請執行下列步驟 hello:

1. 登入執行 Azure AD Connect 同步處理所使用的帳戶成員的 hello toohello 伺服器**ADSyncAdmins**安全性群組。
2. 啟動**同步處理服務**從 hello**啟動**功能表。
3. 選取**連接器**，並在 hello**連接器**清單中，選取與 hello 類型 hello 連接器**Active Directory 網域服務**。 在 [動作] 中選取 [屬性]。  
   ![連接器屬性](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. 按一下 [設定目錄分割] 。
5. 在 hello**選取目錄分割**清單，選取，然後視需要取消選取網域。 確認已選取您想 toosynchronize 只有 hello 資料分割。  
   ![分割數](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   如果您已變更您的內部部署 Active Directory 基礎結構和加入或移除 hello 樹系的網域，然後按一下 hello**重新整理**按鈕 tooget 更新清單。 當您重新整理時，系統會要求您提供認證。 提供讀取權限 tooWindows Server Active Directory 中的任何認證。 不一定會在 [hello] 對話方塊中預先填入的 toobe hello 使用者。  
   ![需要重新整理](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. 當您完成時，關閉 hello**屬性**按一下**確定**。 如果您將網域移除 hello 樹系時，快顯訊息會顯示已移除網域，並將清除該組態。
7. 繼續 tooadjust hello[執行設定檔](#update-run-profiles)。

### <a name="update-hello-run-profiles"></a>更新執行的 hello 設定檔
如果您已更新網域篩選，您也需要 tooupdate hello 執行設定檔。

1. 在 hello**連接器**清單中，請確定已選取您在 hello 上一個步驟中變更連接器該 hello。 在 [動作] 中選取 [設定執行設定檔]。  
   ![連接器執行設定檔 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. 尋找並找出下列設定檔的 hello:
    * 完整匯入
    * 完整同步處理
    * 差異匯入
    * 差異同步處理
    * 匯出
3. 針對每個設定檔中，調整 hello**加入**和**移除**網域。
    1. 針對每個 hello 五個設定檔，請勿 hello 下列步驟針對每個**加入**網域：
        1. 選取執行 hello 設定檔，然後按一下**新步驟**。
        2. 在 hello**設定步驟** 頁面的 hello**類型**下拉式選單選取 hello 以 hello 身分 hello 設定檔的名稱相同的步驟類型設定。 然後按 [下一步] 。  
        ![連接器執行設定檔 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. 在 hello**連接器設定** 頁面的 hello**磁碟分割**下拉式功能表、 選取 hello 您已新增的 tooyour 網域篩選的 hello 網域名稱。  
        ![連接器執行設定檔 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. tooclose hello**設定執行設定檔**] 對話方塊中，按一下 [**完成**。
    2. 針對每個 hello 五個設定檔，請勿 hello 下列步驟針對每個**移除**網域：
        1. 選取執行 hello 設定檔。
        2. 如果 hello**值**的 hello**分割**屬性是 GUID，執行步驟並按一下選取的 hello**刪除步驟**。  
        ![連接器執行設定檔 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. 驗證您的變更。 應該會列出您想 toosynchronize 每個網域，做為每個執行設定檔的步驟。
4. tooclose hello**設定執行設定檔**] 對話方塊中，按一下 [**確定**。
5.  toocomplete hello 組態中，您需要 toorun**完整匯入**和**差異同步處理**。繼續閱讀 hello 區段[套用並驗證變更](#apply-and-verify-changes)。

## <a name="organizational-unitbased-filtering"></a>組織單位型篩選
hello 慣用的方式 toochange OU 為基礎的篩選不執行 hello 安裝精靈，並將變更[網域和 OU 篩選](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)。 hello 安裝精靈會自動記錄在本主題的所有 hello 工作。

如果您因為某種原因無法 toorun hello 安裝精靈，您只應該遵循這些步驟。

tooconfigure 組織單位型篩選，執行下列步驟 hello:

1. 登入執行 Azure AD Connect 同步處理所使用的帳戶成員的 hello toohello 伺服器**ADSyncAdmins**安全性群組。
2. 啟動**同步處理服務**從 hello**啟動**功能表。
3. 選取**連接器**，並在 hello**連接器**清單中，選取與 hello 類型 hello 連接器**Active Directory 網域服務**。 在 [動作] 中選取 [屬性]。  
   ![連接器屬性](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. 按一下**設定目錄分割**，選取您想 tooconfigure，然後再按一下 hello 網域**容器**。
5. 當系統提示您需要時提供讀取權限 tooyour 內部部署 Active Directory 的任何認證。 不一定會在 [hello] 對話方塊中預先填入的 toobe hello 使用者。
6. 在 hello**選取容器**對話方塊中，您不想 toosynchronize 與 hello 雲端目錄，然後再按一下清除 hello Ou**確定**。  
   ![Hello 選取容器 對話方塊中的 Ou](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * hello**電腦**為您的 Windows 10 電腦 toobe 已順利同步處理 tooAzure AD 應該選取的容器。 如果加入網域的電腦位於其他組織單位，請確定已選取這些電腦。
   * hello **ForeignSecurityPrincipals**應該選取容器，如果您有多個樹系信任。 此容器允許跨樹系安全性群組成員資格 toobe 解析。
   * hello **RegisteredDevices**應該選取 OU，如果您啟用 hello 裝置回寫功能。 如果您使用另一個回寫功能，例如群組回寫，請確定已選取這些位置。
   * 選取使用者、iNetOrgPersons、群組、連絡人和電腦所在位置的其他 OU。 在 hello 圖片中，所有這些 Ou 位於 hello ManagedObjects OU 中。
   * 如果您使用群組為基礎的篩選，hello hello 群組所在的 OU 必須包含。
   * 請注意，您可以設定是否為同步處理新 hello 篩選組態完成之後才加入的 Ou，或未同步處理。 請參閱 hello 下一節，如需詳細資訊。
7. 當您完成時，關閉 hello**屬性**按一下**確定**。
8. toocomplete hello 組態中，您需要 toorun**完整匯入**和**差異同步處理**。繼續閱讀 hello 區段[套用並驗證變更](#apply-and-verify-changes)。

### <a name="synchronize-new-ous"></a>同步處理新 OU
依預設，設定篩選之後，會同步處理建立的新 OU。 此狀態是以所選取的核取方塊表示。 您也可以取消選取某些子 OU。 tooget 這種行為，直到它變成白色藍色的核取記號 （其預設狀態），請按一下 [hello] 方塊。 然後取消選取任何的子 Ou，您不想 toosynchronize。

如果會同步處理所有的子 Ou，然後 hello 方塊是白色的藍色的核取記號。  
![所有方塊皆選取的 OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

如果某些子 Ou 已取消選取，hello 方塊是灰色的白色核取記號。  
![部分子 OU 未選取的 OU](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

使用此設定時，在 ManagedObjects 之下建立的新 OU 會同步處理。

hello Azure AD Connect 的安裝精靈一律會建立此設定。

### <a name="dont-synchronize-new-ous"></a>不要同步處理新 OU
您可以設定 hello 同步處理引擎 toonot hello 篩選組態完成後，同步處理新的 Ou。 此狀態會表示 hello 出現任何核取記號的實心灰色 hello 方塊的 UI 中。 tooget 這種行為，直到它變成白色沒有核取記號，請按一下 [hello] 方塊。 然後，選取 hello 的子 Ou 的 toosynchronize。

![含 hello 根未選取的 OU](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

使用此設定時，在 ManagedObjects 之下建立的新 OU 不會同步處理。

## <a name="attribute-based-filtering"></a>屬性型篩選
請確定您使用 hello 2015 年 11 月 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) 或更新的組建，這些步驟 toowork。

屬性為基礎的篩選是 hello 最有彈性的方式 toofilter 物件。 您可以使用 hello 冪[宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)toocontrol 幾乎各個層面物件時同步處理 tooAzure AD。

您可以套用[輸入](#inbound-filtering)從 Active Directory toohello metaverse，篩選和[輸出](#outbound-filtering)hello metaverse tooAzure AD 從篩選。 我們建議您套用輸入篩選，因為這是最簡單 toomaintain 的 hello。 您應該只使用輸出篩選，如果它需要從多個樹系 toojoin 物件 hello 評估才會發生。

### <a name="inbound-filtering"></a>輸入篩選
輸入篩選使用 hello 預設設定，其中將 tooAzure AD 物件必須 hello metaverse 屬性 cloudFiltered 未設定 tooa 值 toobe 同步處理。 如果這個屬性的值設定得**True**，然後 hello 物件未同步。 不應該太設定**False**，所設計。 toomake 確定其他規則有 hello 能力 toocontribute 值，這個屬性只應該 toohave hello 值**True**或**NULL** （不存在）。

在輸入篩選，您可以使用 hello 冪**範圍**toodetermine 物件 toosynchronize 或同步處理。 這是您在其中進行調整 toofit 您自己組織的需求。 hello 範圍模組有**群組**和**子句**toodetermine 在範圍內同步處理規則時。 「群組」會包含一個或多個「子句」。 多個子句之間會有邏輯 "AND"，而多個群組之間會有邏輯 "OR"。

讓我們看看以下範例：  
![範圍](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
這應該解讀為 **(department = IT) OR (department = Sales AND c = US)**。

在 hello 遵循範例和步驟，您使用 hello 使用者物件為例，但是您可以使用此所有物件類型。

在下列範例的 hello，hello 優先順序值開頭都是 50。 這可以是任何未使用的數字，但是應該小於 100。

#### <a name="negative-filtering-do-not-sync-these"></a>負面篩選：「不同步處理這些項目」
在下列範例的 hello，篩選出 （不同步處理） 的所有使用者其中**extensionAttribute15** hello 值**NoSync**。

1. 登入執行 Azure AD Connect 同步處理所使用的帳戶成員的 hello toohello 伺服器**ADSyncAdmins**安全性群組。
2. 啟動**同步處理規則編輯器**從 hello**啟動**功能表。
3. 確定已選取 輸入，然後按一下新增規則。
4. 指定 hello 規則的描述性名稱，例如"*中 from AD – User DoNotSyncFilter*"。 選取 hello 正確樹系中，選取**使用者**為 hello **CS 物件類型**，然後選取**人員**為 hello **MV 物件類型**。 在 [連結類型] 中，選取 [聯結]。 在 [優先順序] 中，輸入目前沒有被其他「同步化規則」使用的值 (例如 50)，然後按 [下一步]。  
   ![輸入 1 描述](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. 在 [範圍設定篩選] 中，按一下 [新增群組]，然後按一下 [新增子句]。 在 [屬性] 中，選取 [ExtensionAttribute15]。 請確定**運算子**設定得**相等**，然後輸入 hello 值**NoSync**在 hello**值**方塊。 按一下 [下一步] 。  
   ![輸入 2 範圍](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. 保留 hello**聯結**空的規則，然後按一下**下一步**。
7. 按一下**新增轉換**，選取 hello **FlowType**為**常數**，然後選取**cloudFiltered**為 hello **目標屬性**。 在 hello**來源**文字方塊中，輸入**True**。 按一下**新增**toosave hello 規則。  
   ![輸入 3 轉換](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. toocomplete hello 組態中，您需要 toorun**完整同步處理**。繼續閱讀 hello 區段[套用並驗證變更](#apply-and-verify-changes)。

#### <a name="positive-filtering-only-sync-these"></a>正面篩選：「只同步處理這些項目」
表示正進行篩選，可以更具有挑戰性，因為您也可以不是同步處理，例如會議室明顯 toobe tooconsider 物件。 您也是進行 toooverride hello 預設篩選 hello 鶈蜪規則中**中 from AD-User Join**。 當您建立自訂篩選時，請確定 toonot 包含重要的系統物件，複寫衝突物件、 特殊的信箱和 hello 服務帳戶的 Azure AD Connect。

hello 正數的篩選選項需要兩個同步處理規則。 您的物件 toosynchronize hello 正確的範圍內的情況下，需要一個規則 （或幾個）。 您也需要篩選出尚未被識別為應進行同步處理物件之所有物件的第二個全面涵蓋同步處理規則。

在下列範例的 hello，您只同步處理使用者物件，其中 hello 部門屬性都具有 hello 值**銷售**。

1. 登入執行 Azure AD Connect 同步處理所使用的帳戶成員的 hello toohello 伺服器**ADSyncAdmins**安全性群組。
2. 啟動**同步處理規則編輯器**從 hello**啟動**功能表。
3. 確定已選取 輸入，然後按一下新增規則。
4. 指定 hello 規則的描述性名稱，例如"*中 from AD – 使用者銷售同步*"。 選取 hello 正確樹系中，選取**使用者**為 hello **CS 物件類型**，然後選取**人員**為 hello **MV 物件類型**。 在 [連結類型] 中，選取 [聯結]。 在 [優先順序] 中，輸入目前沒有被其他「同步化規則」使用的值 (例如 51)，然後按 [下一步]。  
   ![輸入 4 描述](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. 在 [範圍設定篩選] 中，按一下 [新增群組]，然後按一下 [新增子句]。 在 [屬性] 中，選取 [部門]。 請確定運算子設定太**等於**，然後輸入 hello 值**銷售**在 hello**值**方塊。 按一下 [下一步] 。  
   ![輸入 5 範圍](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. 保留 hello**聯結**空的規則，然後按一下**下一步**。
7. 按一下**新增轉換**，選取**常數**為 hello **FlowType**，並選取 hello **cloudFiltered**為 hello **目標屬性**。 在 hello**來源**方塊中，輸入**False**。 按一下**新增**toosave hello 規則。  
   ![輸入 6 轉換](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   這是特殊案例，明確地設定 cloudFiltered 太**False**。
8. 我們現在有 toocreate hello 全面性的同步處理規則。 指定 hello 規則的描述性名稱，例如"*中 from AD – User Catch all 篩選*"。 選取 hello 正確樹系中，選取**使用者**為 hello **CS 物件類型**，然後選取**人員**為 hello **MV 物件類型**。 在 [連結類型] 中，選取 [聯結]。 在 [優先順序] 中，輸入目前沒有被其他「同步化規則」使用的值 (例如 99)。 您已選取 （較低優先順序） 高於 hello 上一次同步處理規則的優先順序值。 但是，您也留了一些空間，讓您可以新增多個篩選的同步處理規則稍後當您想同步處理其他部門 toostart 時。 按一下 [下一步] 。  
   ![輸入 7 描述](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. 將 [範圍設定篩選] 保留空白，然後按 [下一步]。 空白的篩選器指出該 hello 規則套用的 toobe tooall 物件。
10. 保留 hello**聯結**空的規則，然後按一下**下一步**。
11. 按一下**新增轉換**，選取**常數**為 hello **FlowType**，然後選取**cloudFiltered**為 hello **目標屬性**。 在 hello**來源**方塊中，輸入**True**。 按一下**新增**toosave hello 規則。  
    ![輸入 3 轉換](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. toocomplete hello 組態中，您需要 toorun**完整同步處理**。繼續閱讀 hello 區段[套用並驗證變更](#apply-and-verify-changes)。

如果需要您可以建立更多的 hello hello 同步處理中納入多個物件的第一種類型的規則。

### <a name="outbound-filtering"></a>輸出篩選
在某些情況下，它會篩選 hello 物件已經在 hello metaverse 中聯結時，才需要 toodo hello。 例如，可能需要 toolook hello mail 屬性從 hello 資源樹系，以及從 hello 帳戶樹系，如果物件應該同步處理的 toodetermine hello userPrincipalName 屬性。 在這些情況下，您可以建立 hello hello 輸出規則上的篩選。

在此範例中，您變更 hello 篩選，以便只有使用者具有其郵件與結尾的 userPrincipalName@contoso.com會同步處理：

1. 登入執行 Azure AD Connect 同步處理所使用的帳戶成員的 hello toohello 伺服器**ADSyncAdmins**安全性群組。
2. 啟動**同步處理規則編輯器**從 hello**啟動**功能表。
3. 在 [規則類型] 下方按一下 [輸出]。
4. 尋找名為 hello 規則**出 tooAAD – User Join**，然後按一下**編輯**。
5. 在 hello 快顯視窗，請回答**是**toocreate hello 規則的複本。
6. 在 hello**描述**頁面上，變更**優先順序**tooan 未使用的值，例如 50。
7. 按一下**範圍篩選**在 hello 左側的導覽，然後按一下 **Add 子句**。 在 [屬性] 中，選取 [郵件]。 在 [運算子] 中，選取 [ENDSWITH]。 在 值 中，輸入 **@contoso.com**，然後按一下新增子句。 在 [屬性] 中，選取 [userPrincipalName]。 在 [運算子] 中，選取 [ENDSWITH]。 在 [值] 中，輸入 **@contoso.com**。
8. 按一下 [儲存] 。
9. toocomplete hello 組態中，您需要 toorun**完整同步處理**。繼續閱讀 hello 區段[套用並驗證變更](#apply-and-verify-changes)。

## <a name="apply-and-verify-changes"></a>套用並驗證變更
進行組態變更之後，您必須套用 toohello hello 系統中已有的物件。 它也可能是應該處理的 hello 物件不是目前的 hello 同步處理引擎 (和 hello 同步處理引擎需要 tooread hello 來源系統再次 tooverify 其內容)。

如果您使用變更 hello 組態**網域**或**組織單位**篩選，則您需要 toodo**完整匯入**，後面接著**差異同步處理**。

如果您使用變更 hello 組態**屬性**篩選，則您需要 toodo**完整同步處理**。

下列步驟 hello:

1. 啟動**同步處理服務**從 hello**啟動**功能表。
2. 選取 [連接器]。 在 hello**連接器**清單中，選取您所做的設定變更之前的連接器 hello。 在 [動作] 中，選取 [執行]。  
   ![連接器執行](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. 在**執行設定檔**，選取在 hello 上一節所提到的 hello 作業。 如果您需要 toorun 兩個動作，執行第二個之後 hello hello 第一個已完成。 (hello**狀態**資料行是**閒置**hello 選取連接器。)

Hello 同步處理後，會匯出的分段的 toobe 所有變更。 您實際上會在 Azure AD 進行 hello 變更之前，您會想 tooverify 所有這些變更正確。

1. 啟動命令提示字元，然後移過`%Program Files%\Microsoft Azure AD Sync\bin`。
2. 執行 `csexport "Name of Connector" %temp%\export.xml /f:x`。  
   同步處理服務 」 hello hello 連接器名稱。 其名稱類似的 too"contoso.com – AAD"Azure ad。
3. 執行 `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`。
4. 現在您在 %temp% 中已經有名稱為 export.csv 的檔案，可在 Microsoft Excel 中加以檢查。 此檔案包含所有即將 toobe 匯出的 hello 變更。
5. 請 hello 必要的變更 toohello 資料或組態，以及執行這些步驟一次 （匯入、 同步處理及驗證） 直到 hello toobe 匯出相關的變更是您所預期。

當您感到滿意後時，將匯出 hello 變更 tooAzure AD。

1. 選取 [連接器]。 在 hello**連接器**清單中，選取 hello Azure AD 連接器。 在 [動作] 中，選取 [執行]。
2. 在 [執行設定檔] 中，選取 [匯出]。
3. 如果您的組態變更刪除許多物件，然後您看到錯誤在 hello 匯出 hello 數目超過設定的 hello 臨界值 （依預設 500） 時。 如果您看到此錯誤，則您需要 tootemporarily 停用 hello"[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)」 功能。

現在它會將時間 tooenable hello 排程器是一次。

1. 啟動**工作排程器**從 hello**啟動**功能表。
2. 直接在**工作排程器程式庫**，尋找名為 「 hello 任務**Azure AD Sync Scheduler**，按一下滑鼠右鍵，然後選取**啟用**。

## <a name="group-based-filtering"></a>群組型篩選
您可以設定群組為基礎的篩選 hello 第一次您使用安裝 Azure AD Connect[自訂安裝](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)。 它的主要是讓您想要只同步處理的物件 toobe 一小群試驗部署。 當您停用群組型篩選時，無法將它重新啟用。 它有*不支援*toouse 群組為基礎的自訂組態中的篩選。 它有只支援 tooconfigure 這項功能使用 hello 安裝精靈。 當您完成您的試驗時，然後使用其中一個 hello 其他篩選選項本主題中。 使用組織單位型篩選時搭配以群組為基礎的篩選，則必須包含 hello hello 群組及其成員的所在位置的 OU。

同步處理多個 AD 樹系時，您可藉由為每個 AD 連接器指定不同的群組，設定以群組為基礎的篩選。 如果您想 toosynchronize AD 樹系中的使用者和 hello 相同的使用者有一或多對應 FSP （外部安全性主體） 物件中其他 AD 樹系中，您必須確定該 hello 使用者物件和所有其相對應 FSP 物件會都在以群組為基礎篩選的範圍。 如果其中一個或多個 hello FSP 物件會排除群組為基礎的篩選，hello 使用者物件將無法同步處理的 tooAzure AD。

## <a name="next-steps"></a>後續步驟
- 深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。
- 深入了解[整合內部部署身分識別與 Azure AD](active-directory-aadconnect.md)。
