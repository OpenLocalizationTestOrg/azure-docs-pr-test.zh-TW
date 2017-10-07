---
title: "Azure AD Connect 同步︰處理 userCertificate 屬性所造成的 LargeObject 錯誤 | Microsoft Docs"
description: "本主題提供 hello 補救步驟 LargeObject userCertificate 屬性所造成的錯誤。"
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Azure AD Connect 同步︰處理 userCertificate 屬性所造成的 LargeObject 錯誤 | Microsoft Docs

Azure AD 會強制執行的最大限制**15**憑證上 hello 值**userCertificate**屬性。 Azure AD 傳回的 Azure AD Connect 匯出具有超過 15 個值 tooAzure AD 物件，如果**LargeObject**錯誤訊息：

>*「 hello 佈建的物件是太大。修剪 hello 屬性值，這個物件的數目。hello 作業將會重試 hello 中下一個同步處理循環...」*

hello LargeObject 錯誤可能是其他 AD 屬性所造成。 tooconfirm 確實因 hello userCertificate 屬性，您需要針對 hello 物件在內部部署 AD，或在 hello tooverify[同步處理服務管理員 Metaverse 搜尋](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch)。

tooobtain hello 物件清單中您的租用戶 LargeObject 錯誤，使用其中一個 hello 下列方法：

 * 如果您的租用戶啟用 Azure AD Connect Health 進行同步時，您可以參考 toohello[同步處理錯誤報告](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview)提供。
 
 * hello 通知電子郵件。 目錄同步作業錯誤，便會傳送一次同步處理循環的 hello 結尾有 hello LargeObject 發生錯誤的物件清單。 
 * hello[同步處理服務管理員作業 索引標籤](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations)顯示 hello LargeObject 發生錯誤的物件清單，如果您按一下 hello 最新的匯出 tooAzure AD 作業。
 
## <a name="mitigation-options"></a>緩和選項
Hello LargeObject 錯誤解決之前，相同的物件不可以是其他屬性變更 toohello 匯出 tooAzure AD。 tooresolve hello 錯誤，您可以考慮下列選項的 hello:

 * 升級 Azure AD Connect toobuild 1.1.524.0 或之後。 在 Azure AD Connect 會建置 1.1.524.0，hello 現成的同步處理規則已更新的 toonot 匯出屬性 userCertificate 和 userSMIMECertificate hello 屬性有超過 15 的值。 如需詳細資訊，如何 tooupgrade Azure AD Connect，請參閱 tooarticle [Azure AD Connect： 從先前版本 toohello 最新升級](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version)。

 * 實作**輸出同步處理規則**中匯出的 Azure AD Connect **null 值，而非 hello 實際值的物件具有超過 15 個憑證值**。 此選項，很適合，如果您不需要任何 hello 憑證值匯出 toobe tooAzure AD 物件超過 15 的值。 如需詳細資訊，如何 tooimplement 此同步處理規則，toonext 區段，請參閱[userCertificate 屬性的實作同步處理規則 toolimit 匯出](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute)。

 * Hello 上的憑證值的減少 hello 內部部署 AD 物件 (15 個或更少） 藉由移除不再由您的組織使用的值。 這是適用在 hello 屬性膨脹的起因是過期或未使用的憑證。 您可以使用 hello [PowerShell 指令碼可以使用這裡](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f)toohelp 尋找備份，並刪除過期的憑證，在您內部部署 AD。 在刪除之前 hello 憑證，建議您在組織中驗證與 hello 公開金鑰--基礎結構系統管理員。

 * 設定 Azure AD Connect tooexclude hello userCertificate 屬性從正在匯出 tooAzure AD。 一般情況下，我們不建議這個選項因為 hello 屬性可能會使用 Microsoft Online Services tooenable 特定案例。 特別是：
    * hello 使用者物件上的 hello userCertificate 屬性是由 Exchange Online 與 Outlook 用戶端用於訊息簽署和加密。 toolearn 進一步了解這項功能，請參閱 tooarticle [S/MIME 訊息簽署和加密](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx)。

    * 使用 Azure AD tooallow Windows 10 在內部部署已加入網域裝置 tooconnect tooAzure AD hello 電腦物件上的 hello userCertificate 屬性。 toolearn 進一步了解這項功能，請參閱 tooarticle[連接已加入網域裝置 tooAzure AD 以進行 Windows 10 體驗](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy)。

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>實作同步處理規則 toolimit 匯出 userCertificate 屬性
tooresolve hello LargeObject 錯誤 hello userCertificate 屬性所造成，您可以實作的輸出同步處理規則中匯出的 Azure AD Connect **null 值，而非 hello 實際值的物件具有超過 15 個憑證值**. 本章節描述 hello 步驟需要的 tooimplement hello 同步處理規則**使用者**物件。 hello 步驟可能會調整為**連絡人**和**電腦**物件。

> [!IMPORTANT]
> 匯出 null 值中移除值之前已成功匯出 tooAzure AD 憑證。

hello 步驟可以摘要如下：

1. 停用同步排程器，並確認沒有任何同步處理在進行中。
3. 尋找現有輸出同步處理規則 hello userCertificate 屬性。
4. 建立所需的 hello 輸出同步處理規則。
5. 請確認現有的物件，LargeObject 錯誤 hello 新同步處理規則。
6. 適用於 hello 新同步處理規則 tooremaining 物件 LargeObject 錯誤。
7. 請確認沒有任何未預期的變更，等候 toobe 匯出 tooAzure AD。
8. 匯出 hello 變更 tooAzure AD。
9. 重新啟用同步排程器。

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>步驟 1. 停用同步排程器，並確認沒有任何同步處理在進行中
請確定沒有同步處理 hello 中間的實作新的同步處理時，會發生非預期的規則 tooavoid 變更正在執行匯出 tooAzure AD。 toodisable hello 內建的同步處理排程器：
1. Hello Azure AD Connect 的伺服器上啟動 PowerShell 工作階段。

2. 執行 Cmdlet 以停用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> hello 前面的步驟都只與 hello 內建的排程器的 Azure AD Connect 的適用 toonewer 版本 (1.1.xxx.x)。 如果您使用舊版 (1.0.xxx.x) 的 Azure AD Connect 使用 Windows 工作排程器，或您正在使用您自己自訂的排程器 （不常見） tootrigger 定期同步處理，則需要 toodisable 它們據以。

3. 啟動 hello**同步處理服務管理員**移 tooSTART → 所同步處理服務。

4. 移 toohello**作業**索引標籤上，並確認其狀態是沒有作業*「 進行中 」。*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>步驟 2. 尋找現有輸出同步處理規則 hello userCertificate 屬性
應該要有現有的同步處理規則已啟用和設定的使用者物件 tooAzure AD tooexport userCertificate 屬性。 找出此同步處理規則 toofind 其**優先順序**和**範圍篩選器**組態：

1. 啟動 hello**同步處理規則編輯器**移 tooSTART → 所同步處理規則編輯器。

2. 設定下列值的 hello hello 搜尋篩選器：

    | 屬性 | 值 |
    | --- | --- |
    | 方向 |**輸出** |
    | MV 物件類型 |**人員** |
    | 連接器 |Azure AD 連接器的名稱 |
    | 連接器物件類型 |**user** |
    | MV 屬性 |**userCertificate** |

3. 如果您的使用者物件使用 OOB （的全新） 同步處理規則 tooAzure AD 連接器 tooexport userCertficiate 屬性，您應該會回到 hello *"Out tooAAD – 使用者 ExchangeOnline"*規則。
4. 記下 hello**優先順序**此同步處理規則的值。
5. 選取 hello 同步處理規則，然後按一下**編輯**。
6. 在 hello *」 編輯保留規則確認 」*快顯對話方塊中，按一下**否**。 （也請別擔心，我們不會 toomake 任何變更 toothis 同步處理規則）。
7. 在 hello 編輯畫面上，選取 hello**範圍篩選** 索引標籤。
8. 記下 hello 範圍設定篩選器設定。 如果您使用 hello OOB 同步處理規則，只應該有**一個範圍的篩選群組包含兩個子句**，包括：

    | 屬性 | 運算子 | 值 |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | User |
    | cloudMastered | NOTEQUAL | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>步驟 3. 建立所需的 hello 輸出同步處理規則
hello 新同步處理規則必須有 hello 相同**範圍篩選器**和**優先順序**比 hello 現有的同步處理規則。 這可確保該 hello 新的同步處理規則適用於的 toohello 相同的物件設定為 hello 現有的同步處理規則，並覆寫 hello 現有同步處理規則 hello userCertificate 屬性。 toocreate hello 同步處理規則：
1. 在 hello 同步處理規則編輯器中，按一下 hello**加入新規則** 按鈕。
2. 在 hello**描述索引標籤**，提供下列組態的 hello:

    | 屬性 | 值 | 詳細資料 |
    | --- | --- | --- |
    | 名稱 | 提供名稱 | 例如， *「 出 tooAAD – 自訂覆寫的 userCertificate 」* |
    | 說明 | 提供描述 | 例如，「如果 userCertificate 屬性有 15 個以上的值，匯出 NULL」。 |
    | 連線系統 | *選取 hello Azure AD Connector* |
    | 連線系統物件類型 | **user** | |
    | Metaverse 物件類型 | **person** | |
    | 連結類型 | **Join** | |
    | 優先順序 | 選擇 1-99 之間的數字 | hello 數字選擇必須不使用任何現有的同步處理規則，而且具有較低的值 (因此，較高優先順序) 比 hello 現有的同步處理規則。 |

3. 移 toohello**範圍篩選**索引標籤上，並實作使用相同範圍篩選 hello 現有同步處理規則的 hello。
4. 略過 hello**聯結規則** 索引標籤。
5. 移 toohello**轉換**tooadd 新轉換使用下列組態索引標籤上：

    | 屬性 | 值 |
    | --- | --- |
    | 流程類型 |**運算式** |
    | 目標屬性 |**userCertificate** |
    | 來源屬性 |*下列運算式使用 hello*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. 按一下 hello**新增**按鈕 toocreate hello 同步處理規則。

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>步驟 4. 驗證現有的物件，LargeObject 錯誤 hello 新同步處理規則
這是 hello 同步處理的 tooverify 建立規則是否正常運作，LargeObject 錯誤現有的 AD 物件然後再套用 tooother 物件：
1. 移 toohello**作業**hello 同步處理服務管理員中的索引標籤。
2. 選取 hello 最新的匯出 tooAzure AD 作業，然後按一下其中一個 hello LargeObject 錯誤物件。
3.  在 [hello 連接器空間物件屬性快顯畫面上，按一下 hello**預覽**] 按鈕。
4. 在 hello 預覽快顯畫面上，選取 **完整同步處理**按一下**認可預覽**。
5. 關閉 hello 預覽畫面與 hello 連接器空間物件屬性畫面。
6. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。
7. 以滑鼠右鍵按一下 hello **Azure AD**連接器並選取**執行...**
8. 在 hello 執行連接器快顯視窗中，選取 **匯出**步驟，然後按一下**確定**。
9. 等候匯出 tooAzure AD toocomplete，並確認此特定物件上沒有任何詳細的 LargeObject 錯誤。

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>步驟 5。 套用 hello 新同步處理規則 tooremaining 物件 LargeObject 錯誤
一旦加入 hello 同步處理規則，您會需要 toorun hello AD 連接器完整同步處理步驟：
1. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。
2. 以滑鼠右鍵按一下 hello **AD**連接器並選取**執行...**
3. 在 hello 執行連接器快顯視窗中，選取 **完整同步處理**步驟，然後按一下**確定**。
4. 等候 hello 完整同步處理步驟 toocomplete。
5. 重複上述步驟 hello hello 剩餘 AD 連接器，如果您有多個 AD 連接器。 通常，如果您有多個內部部署目錄，則需要多個連接器。

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>步驟 6. 請確認沒有任何未預期的變更，等候 toobe 匯出 tooAzure AD
1. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。
2. 以滑鼠右鍵按一下 hello **Azure AD**連接器並選取**搜尋連接器空間**。
3. 在 hello 搜尋連接器空間快顯視窗：
    1. 將範圍設定為太**暫止匯出**。
    2. 將 3 個核取方塊全部勾選，包括 [新增]、[修改] 和 [刪除]。
    3. 按一下**搜尋**按鈕 tooreturn 所有物件與變更正在等候 toobe 匯出 tooAzure AD。
    4. 請確認沒有任何非預期的變更。 hello 物件上，按兩下 tooexamine hello 變更之特定的物件。

### <a name="step-7-export-hello-changes-tooazure-ad"></a>步驟 7. 匯出的 hello 變更 tooAzure AD
tooexport hello 變更 tooAzure AD:
1. 移 toohello**連接器**hello 同步處理服務管理員中的索引標籤。
2. 以滑鼠右鍵按一下 hello **Azure AD**連接器並選取**執行...**
4. 在 hello 執行連接器快顯視窗中，選取 **匯出**步驟，然後按一下**確定**。
5. 等候匯出 tooAzure AD toocomplete，並確認沒有任何多個 LargeObject 錯誤。

### <a name="step-8-re-enable-sync-scheduler"></a>步驟 8。 重新啟用同步排程器
Hello 問題解決後，重新啟用裝置 hello 內建的同步處理排程器：
1. 啟動 PowerShell 工作階段。
2. 執行 Cmdlet 以重新啟用排定的同步處理︰`Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> hello 前面的步驟都只與 hello 內建的排程器的 Azure AD Connect 的適用 toonewer 版本 (1.1.xxx.x)。 如果您使用舊版 (1.0.xxx.x) 的 Azure AD Connect 使用 Windows 工作排程器，或您正在使用您自己自訂的排程器 （不常見） tootrigger 定期同步處理，則需要 toodisable 它們據以。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

