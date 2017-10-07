---
title: "aaaIdentity 同步處理和重複項目屬性的恢復功能 |Microsoft 文件"
description: "新的 UPN 或 ProxyAddress 衝突 toohandle 物件在使用 Azure AD Connect 目錄同步作業期間如何行為。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>身分識別同步處理和重複屬性恢復功能
「重複屬性恢復功能」是 Azure Active Directory 中的一項功能，可在執行 Microsoft 的其中一個同步處理工具時，用來消除 **UserPrincipalName** 和 **ProxyAddress** 衝突所造成的不便。

所有之間這兩個屬性都是唯一通常需要的 toobe**使用者**，**群組**，或**連絡人**給定的 Azure Active Directory 租用戶中的物件。

> [!NOTE]
> 只有使用者可以擁有 UPN。
> 
> 

hello 新行為，這項功能可讓 hello 雲端部份 hello 同步管線中，因此它是無從驗證，包括 Azure AD Connect、 DirSync 和 MIM + 連接器任何 Microsoft 同步處理產品相關的用戶端。 hello 泛型的詞彙 「 同步處理用戶端 」 用於此文件 toorepresent 這些產品的任何一個。

## <a name="current-behavior"></a>目前的行為
如果沒有嘗試 tooprovision UPN 或 ProxyAddress 值違反了這個唯一性條件約束新的物件，Azure Active Directory 會封鎖來自建立該物件。 同樣地，如果更新物件時具有非唯一的 UPN 或 ProxyAddress，hello 更新將會失敗。 佈建嘗試或更新的 hello hello 同步用戶端時每個匯出循環中，會重試，並繼續 toofail，hello 衝突解決之前。 在每次嘗試時產生錯誤報表電子郵件和 hello 同步用戶端會將錯誤記錄。

## <a name="behavior-with-duplicate-attribute-resiliency"></a>重複屬性恢復功能的行為
而不完全失敗 tooprovision 或更新且重複的屬性，Azure Active Directory 「 隔離 」 hello 重複的屬性會違反 hello 唯一性條件約束的物件。 如果這是必要的佈建，例如 UserPrincipalName 屬性 hello 服務指派的預留位置值。 這些暫存值 hello 格式  
“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”。  
如果 hello 屬性不是必要的如**ProxyAddress**，Azure Active Directory 只要隔離 hello 衝突的屬性，並繼續處理 hello 物件建立或更新。

在隔離 hello 屬性，hello 衝突的相關資訊會在 hello 使用相同的錯誤報表電子郵件傳送 hello 舊的行為。 不過，此資訊只會出現在 hello 錯誤報告一次，hello 隔離發生失敗時，它不會繼續 toobe 未來記錄電子郵件。 此外，因為此物件的 hello 匯出成功，hello 同步用戶端不會記錄錯誤並不重試 hello 建立 / 更新作業，在後續同步處理循環時。

此行為的新屬性已被的 toosupport 加入 toohello 使用者、 群組和連絡人物件類別：  
**DirSyncProvisioningErrors**

這是使用的 toostore hello 衝突的屬性會違反 hello 唯一性條件約束應該將它們加入通常在多重值的屬性。 執行有重複的屬性衝突已經解決，且會自動從隔離區移除有問題的 hello 屬性每個小時 toolook 的 Azure Active Directory 中已啟用背景計時器工作。

### <a name="enabling-duplicate-attribute-resiliency"></a>啟用重複屬性恢復功能
重複的屬性恢復功能會在所有的 Azure Active Directory 租用戶之間 hello 新的預設行為。 它會預設啟用的同步處理 hello 於 2016 年 8 月 22 日，或更新版本的第一次的所有租用戶上。 啟用同步處理先前 toothis 日期的租用戶會有已啟用批次中的 hello 功能。 本次首度發行的 2016 年 9 月開始，會傳送電子郵件通知 tooeach 租用戶的技術通知接觸 hello hello 功能會啟用時的特定日期。

> [!NOTE]
> 一旦開啟「重複屬性恢復功能」，即無法予以停用。

如果您的租用戶啟用 hello 功能 toocheck，您可以下載 hello hello Azure Active Directory PowerShell 模組最新版本，執行：

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> 它已為您的租用戶之前，無法再使用 Set-msoldirsyncfeature cmdlet tooproactively 啟用 hello 重複屬性恢復功能。 toobe 無法 tootest hello 功能，您將需要 toocreate 新的 Azure Active Directory 租用戶。

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>識別具有 DirSyncProvisioningErrors 的物件
這些錯誤，因為 tooduplicate 屬性衝突，Azure Active Directory PowerShell 和 Office 365 系統管理入口網站 hello tooidentify 物件有目前兩種方法。 有計劃 tooextend tooadditional 入口網站基礎 hello 未來中的報告。

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Hello 本主題中的 PowerShell cmdlet，hello 下列條件為真：

* 下列指令程式的 hello 都區分大小寫。
* hello **– ErrorCategory PropertyConflict**必須永遠包含在內。 目前沒有任何其他類型**ErrorCategory**，但可能會在 hello 未來擴充。

首先，執行 **Connect-MsolService** 並輸入租用戶系統管理員的認證。

然後，使用下列 cmdlet 和運算子 tooview 錯誤以不同方式的 hello:

1. [檢視全部](#see-all)
2. [依屬性類型](#by-property-type)
3. [依衝突的值](#by-conflicting-value)
4. [使用字串搜尋](#using-a-string-search)
5. [排序](#sorted)
6. [以有限的數量或全部](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>檢視全部
一旦連接之後，toosee 一般佈建錯誤 hello 租用戶中的屬性清單執行：

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

這會產生類似 hello 下列結果：  
 ![Get MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>依屬性類型
依屬性類型的 toosee 錯誤新增 hello **-PropertyName**旗標以 hello **UserPrincipalName**或**ProxyAddresses**引數：

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

或

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>依衝突的值
toosee 錯誤相關 tooa 特定屬性新增 hello **-PropertyValue**旗標 (**-PropertyName**加入這個旗標時必須一併使用):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>使用字串搜尋
toodo 廣泛的字串搜尋使用 hello **-SearchString**旗標。 這適用於獨立從所有旗標，但 hello 的例外是上述 hello **-ErrorCategory PropertyConflict**，永遠是必要項：

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>以有限的數量或全部
1. **MaxResults <Int>** 可以是使用 toolimit hello 查詢 tooa 特定數目的值。
2. **所有**可以是使用的 tooensure 大量錯誤存在的 hello 案例中擷取所有結果。

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Office 365 系統管理入口網站
您可以在 hello Office 365 系統管理中心檢視目錄同步作業錯誤。 hello hello Office 365 入口網站只會顯示在報表**使用者**發生這些錯誤的物件。 並不會顯示「群組」和「連絡人」之間的衝突相關資訊。

![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "作用中使用者")

如需如何 tooview 目錄同步作業錯誤的 hello Office 365 admin center 指示，請參閱[識別 Office 365 中的目錄同步作業錯誤](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)。

### <a name="identity-synchronization-error-report"></a>身分識別同步處理錯誤報告
當具有重複的屬性發生衝突的物件會處理與通知包含在這個新行為 hello 標準識別身分同步處理錯誤報告的電子郵件，會傳送 hello 租用戶的 toohello 通知技術連絡人。 不過，此行為有一項重大變更。 在過去 hello，重複的屬性發生衝突的相關資訊會包含在每個後續的錯誤報告之前 hello 衝突已解決。 使用這個新的行為，指定衝突的 hello 錯誤通知未只能出現一次-次 hello hello 衝突的屬性會被隔離。

哪些 hello 電子郵件通知看起來像 ProxyAddress 衝突的範例如下：  
    ![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")  

## <a name="resolving-conflicts"></a>解決衝突
疑難排解這些錯誤的策略與解決策略不應該從 hello hello 過去中的重複屬性錯誤處理的方式不同。 hello 唯一的差異是，透過在 hello 服務端 tooautomatically hello 租用戶的 hello 計時器工作掃掠加入 hello 屬性問題 toohello 適當物件中一旦 hello 衝突的解決。

hello 下列文件概述各種疑難排解和解決方式：[重複或無效的屬性會讓 Office 365 中的目錄同步作業](https://support.microsoft.com/kb/2647098)。

## <a name="known-issues"></a>已知問題
沒有任何已知問題會導致資料遺失或服務降級。 其中幾個美觀，其他人會導致標準 「*前的恢復功能*"重複的屬性而不是隔離 hello 衝突的屬性，而另一個會擲回的錯誤 toobe 會造成特定錯誤 toorequire 額外的手動 v-table 修正。

**核心行為︰**

1. 具有特定的屬性設定的物件相對於的 toohello 重複屬性被隔離繼續 tooreceive 匯出錯誤。  
   例如：
   
    a. 新使用者會在 AD 中以 UPN 為 **Joe@contoso.com**、ProxyAddress 為 **smtp:Joe@contoso.com** 的方式建立
   
    b. hello 這個物件屬性發生衝突與現有的群組，其中是 ProxyAddress  **SMTP:Joe@contoso.com** 。
   
    c. 在匯出時**ProxyAddress 衝突**而不需要隔離 hello 衝突的屬性會擲回錯誤。 hello 作業是在每個後續同步處理循環中，重試，因為它可能已啟用 hello 恢復功能之前。
2. 如果在建立兩個群組會在內部以 hello 相同 SMTP 位址，一個失敗 tooprovision hello 第一次嘗試重複的標準**ProxyAddress**錯誤。 不過，hello 重複的值是適當隔離時 hello 下一個同步處理循環。

**Office 入口網站報告**：

1. UPN 衝突集合中的兩個物件的 hello 詳細的錯誤訊息是 hello 相同。 這表示它們都已變更 / 隔離 UPN，當事實上只有其中一個變更了資料。
2. hello UPN 衝突的詳細的錯誤訊息會顯示 hello 錯誤 displayName 的使用者已變更/隔離其 UPN。 例如：
   
    a. **User A** 會先與 **UPN = User@contoso.com** 同步。
   
    b. **使用者 B**嘗試的 toobe 同步處理與接**UPN = User@contoso.com** 。
   
    c. **使用者 B 的**UPN 變更太**User1234@contoso.onmicrosoft.com** 和 **User@contoso.com** 太加入**DirSyncProvisioningErrors**。
   
    d. hello 錯誤訊息，取得**使用者 B**應該指出**使用者 A**已經有 **User@contoso.com**  UPN，但它示**使用者 B**自己顯示名稱。

**身分識別同步處理錯誤報告**：

hello 連結*步驟 tooresolve 此問題*不正確：  
    ![作用中使用者](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "作用中使用者")  

它應該太點[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency)。

## <a name="see-also"></a>另請參閱
* [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
* [在 Office 365 中識別目錄同步處理錯誤](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

