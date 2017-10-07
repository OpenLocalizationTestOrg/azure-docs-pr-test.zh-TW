---
title: "Azure AD Connect：針對同步處理期間的錯誤進行疑難排解 | Microsoft Docs"
description: "說明如何使用 Azure AD Connect 同步處理期間發生 tootroubleshoot 錯誤。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>針對同步處理期間的錯誤進行疑難排解
識別資料同步處理從 Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD) 時，就可能發生錯誤。 本文提供不同類型的同步錯誤，一些 hello 會導致這些錯誤和潛在的方式 toofix hello 錯誤的可能案例的概觀。 本文章包含 hello 常見的錯誤類型，並不一定會涵蓋所有的 hello 可能的錯誤。

 本文章假設 hello 讀者已熟悉 hello 基礎[設計概念的 Azure AD 與 Azure AD Connect](active-directory-aadconnect-design-concepts.md)。

Hello 最新版本的 Azure AD Connect\(年 8 月 2016年或更新版本\)的同步處理錯誤報表位於 hello [Azure 入口網站](https://aka.ms/aadconnecthealth)做為 Azure AD Connect Health 進行同步的一部分。

從 2016 年 9 月 1 日開始[Azure Active Directory 重複屬性復原](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)會啟用功能，依預設，所有的 hello*新*Azure Active Directory 租用戶。 這項功能將會自動啟用現有的租用戶 hello 未來幾個月。

Azure AD Connect 執行作業的 3 種從 hello 目錄則保持同步： 匯入、 同步處理及匯出。 錯誤可以在所有 hello 作業中進行。 本文主要著重在錯誤期間匯出 tooAzure AD。

## <a name="errors-during-export-tooazure-ad"></a>匯出 tooAzure AD 期間發生的錯誤
下列章節說明不同類型的同步處理期間 hello 匯出作業 tooAzure AD 使用可以發生的錯誤 hello Azure AD 連接器。 此連接器，可識別的 hello 名稱格式"contoso。*onmicrosoft.com*"。
匯出 tooAzure AD 期間發生的錯誤指出該 hello 作業\(新增、 更新、 刪除等\)由 Azure AD Connect 所嘗試的\(同步處理引擎\)在 Azure Active Directory 失敗。

![匯出錯誤概觀](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>資料不符錯誤
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>說明
* 當 Azure AD Connect\(同步處理引擎\)指示 Azure Active Directory tooadd 或更新物件，Azure AD 相符項目 hello 連入的物件使用 hello **sourceAnchor**屬性 toohello **immutableId** Azure AD 中物件的屬性。 此種比對稱為**完全比對**。
* 當 Azure AD**找不到**符合 hello 之任何物件**immutableId**屬性以 hello **sourceAnchor** hello 連入物件，然後才提供的屬性新物件，則會回到 toouse hello ProxyAddresses 和 UserPrincipalName 屬性 toofind 相符項目。 此種比對稱為**大致比對**。 hello 軟相符項目是設計的 toomatch hello 新的物件同步處理期間新增/更新代表 hello 與已經存在於 Azure AD （也就源自 Azure AD） 中的物件在內部部署的相同實體 （使用者、 群組）。
* **InvalidSoftMatch**就會發生錯誤時 hello 硬碟的相符項目找不到任何相符物件**AND**彈性比對尋找相符的物件，但該物件具有不同值的*immutableId*非 hello 連入物件*SourceAnchor*，建議的 hello 符合物件與另一個物件從內部部署 Active Directory 同步處理。

換句話說，為了讓 hello 軟相符 toowork，軟體與 hello 物件 toobe 應該沒有任何值 hello *immutableId*。 如果任何物件具有*immutableId*值組失敗 hello 硬符合，但滿足 hello 軟比對準則，hello 作業會產生 InvalidSoftMatch 同步處理錯誤。

結構描述不允許 toohave hello hello 遵循的相同值的兩個或多個物件的 azure Active Directory 屬性。 \(這不是詳盡的清單。\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> [Azure AD 屬性重複屬性復原](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)功能也回復為 Azure Active Directory hello 預設行為。  這將會處理重複 ProxyAddresses 和 UserPrincipalName 屬性存在於內部部署 AD hello 方式中，進行 Azure AD 更有彈性的方式減少 hello 看到 Azure AD Connect （以及其他同步處理用戶端） 的同步處理錯誤的數目環境。 這項功能不會修正 hello 重複錯誤。 因此 hello 資料仍然需要 toobe 固定。 但是，它可讓 Azure AD 中佈建由於 tooduplicated 值阻止新物件佈建。 這也會減少 hello 同步處理傳回的錯誤數目 toohello 同步處理用戶端。
> 如果您的租用戶啟用這項功能，不會看到 hello InvalidSoftMatch 同步處理錯誤期間的新物件佈建看到。
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>InvalidSoftMatch 的範例案例
1. Hello ProxyAddresses 屬性的相同值存在於內部部署 Active Directory 與兩個或多個物件。 只有一個會在 Azure AD 中佈建。
2. 以相同的 userPrincipalName 值存在於內部部署 Active Directory 的 hello 兩個或多個物件。 只有一個會在 Azure AD 中佈建。
3. 物件已加入 hello 在內部部署 Active Directory 以 hello 相同 Azure Active Directory 中現有物件的 ProxyAddresses 屬性的值。 加入在內部部署的 hello 物件未取得 Azure Active Directory 中佈建。
4. 物件已加入在內部部署 Active Directory 以 hello 相同的 Azure Active Directory 中帳戶的 userPrincipalName 屬性的值。 hello 物件未取得 Azure Active Directory 中佈建。
5. 同步處理的帳戶已從樹系 A tooForest b 的 Azure AD Connect （同步處理引擎） 已使用移動 ObjectGUID 屬性 toocompute hello SourceAnchor。 Hello 樹系移動之後, hello hello SourceAnchor 值是不同的。 在 Azure AD 中失敗 toosync 與 hello 現有物件 hello （來自樹系 B) 的新物件。
6. 同步處理的物件從內部部署 Active Directory 意外刪除了和建立新的物件已在 Active Directory 中的 hello 相同實體 （例如使用者），但不會刪除 Azure Active Directory 中的 hello 帳戶。 hello 新帳戶失敗 toosync 與 hello 現有 Azure AD 物件。
7. Azure AD Connect 解除安裝後再重新安裝。 Hello 重新安裝期間，不同的屬性已被選為 hello SourceAnchor。 所有先前已同步的 hello 物件停止 InvalidSoftMatch 錯誤與同步處理。

#### <a name="example-case"></a>範例案例︰
1. **Bob Smith** 是 Azure Active Directory 中已從 *contoso.com* 的內部部署 Active Directory 同步處理的使用者
2. Bob Smith 的 **UserPrincipalName** 已設定為 **bobs@contoso.com**。
3. **「 abcdefghijklmnopqrstuv = ="**為 hello **SourceAnchor**計算方式是使用 Bob Smith 的 Azure AD Connect **objectGUID**在內部部署 Active Directory 中，亦即 hello **immutableId** Bob smith，Azure Active Directory 中。
4. Bob 也有下列值 hello **proxyAddresses**屬性：
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. 新的使用者， **Bob Taylor**，會在內部部署 Active Directory 加入 toohello。
6. Bob Taylor 的 **UserPrincipalName** 已設為 **bobt@contoso.com**。
7. **「 abcdefghijkl0123456789 = =""**為 hello **sourceAnchor**計算方式是使用 Bob Taylor 的 Azure AD Connect **objectGUID**從內部部署 Active Directory。 Bob Taylor 物件尚未同步 tooAzure Active Directory。
8. Bob taylor 了解有 hello 遵循 hello proxyAddresses 屬性的值
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. 同步處理期間，Azure AD Connect 會辨識 hello 新增 Bob taylor 了解在內部部署 Active Directory，並要求 Azure AD toomake hello 相同的變更。
10. Azure AD 會先執行完全比對。 也就是說，它會在其中搜尋是否有任何物件，但 hello immutableId 等於太"abcdefghijkl0123456789 = ="。 完全比對會失敗，因為 Azure AD 中沒有其他物件具有該 immutableId。
11. Azure AD 會嘗試比對 toosoft Bob taylor 了解。 也就是說，它會在其中搜尋是否有任何物件，但 proxyAddresses 等於 toohello 三個值，包括smtp:bob@contoso.com
12. Azure AD 會尋找 Bob Smith 物件 toomatch hello 軟比對準則。 但此物件具有 hello immutableId 值 ="abcdefghijklmnopqrstuv = ="。 這表示此物件已從內部部署 Active Directory 中的另一個物件同步處理。 因此，Azure AD 無法大致比對這些物件，並會導致 **InvalidSoftMatch** 同步處理錯誤。

#### <a name="how-toofix-invalidsoftmatch-error"></a>如何 toofix InvalidSoftMatch 錯誤
hello hello InvalidSoftMatch 錯誤最常見原因是兩個物件具有不同的 SourceAnchor \(immutableId\)有相同的值為 hello ProxyAddresses 及/或 UserPrincipalName 屬性，這些屬性 hello 期間所使用的 helloAzure AD 上的軟體比對程序。 在訂單 toofix hello 無效的彈性比對

1. 識別重複的 hello proxyAddresses、 userPrincipalName 或 hello 錯誤造成其他屬性值。 也會識別這兩個\(或多個\)hello 衝突中涉及的物件。 hello 所產生的報表[Azure AD Connect Health 進行同步](https://aka.ms/aadchsyncerrors)可協助您識別 hello 兩個物件。
2. 識別哪些物件應該繼續 toohave hello 重複值，以及哪些物件不應該。
3. 從 hello 物件不應該有該值，移除重複的 hello 值。 請注意，您應該進行變更 hello hello 物件源自其中的目錄中的 hello。 在某些情況下，您可能需要 toodelete 的其中一個衝突的 hello 物件。
4. 如果您進行變更 hello 在內部部署 AD 中的 hello，可讓 Azure AD Connect 同步處理 hello 變更。

請注意，在 Azure AD Connect Health 進行同步的同步處理錯誤報表會更新每隔 30 分鐘包括 hello hello 最新的同步處理嘗試的錯誤。

> [!NOTE]
> ImmutableId，根據定義，不應該變更 hello hello 物件存留期間。 如果未使用的 hello 案例，請注意，從清單上方的 hello 設定 Azure AD Connect，您最後可能會在 Azure AD Connect 其中計算 hello SourceAnchor hello AD 物件代表 hello 同一個實體的不同值的情況下 (相同的使用者 /群組/連絡人等） 具有您想 toocontinue 使用現有 Azure AD 物件。
>
>

#### <a name="related-articles"></a>相關文章
* [重複或無效的屬性會防止 Office 365 進行目錄同步作業](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>說明
當 Azure AD 會嘗試 toosoft 比對兩個物件時，您就可以確定兩個不同物件"物件類型 」 （例如使用者、 群組、 連絡人等） 具有相同值 hello 屬性使用 tooperform hello 彈性比對的 hello。 在 Azure AD 中不允許重複的這些屬性，如 hello 作業會導致 「 ObjectTypeMismatch 」 同步處理錯誤。

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>ObjectTypeMismatch 錯誤的示範案例
* 在 Office 365 中建立擁有郵件功能的安全性群組。 系統管理員，加入新的使用者或連絡人在內部部署上 AD （未同步處理尚未 tooAzure AD） 以 hello 相同的 hello Office 365 hello ProxyAddresses 屬性的值分組。

#### <a name="example-case"></a>範例案例
1. 管理 Office 365 中建立新郵件功能的安全性群組，hello 稅部門，並提供做為電子郵件地址tax@contoso.com。這會指派 hello 值是此群組的 hello ProxyAddresses 屬性**smtp:tax@contoso.com**
2. 新使用者加入 Contoso.com，而且在 hello proxyAddress 做為內部部署的 hello 使用者建立帳戶**smtp:tax@contoso.com**
3. Azure AD Connect 會同步 hello 新的使用者帳戶，它會收到 hello"ObjectTypeMismatch 」 錯誤。

#### <a name="how-toofix-objecttypemismatch-error"></a>如何 toofix ObjectTypeMismatch 錯誤
hello hello ObjectTypeMismatch 錯誤最常見原因是類型的兩個不同 （使用者、 群組、 連絡人等） 的物件有的 hello hello ProxyAddresses 屬性相同的值。 在 toofix hello ObjectTypeMismatch 順序：

1. 識別重複的 hello proxyAddresses （或其他屬性） 值的造成 hello 錯誤。 也會識別這兩個\(或多個\)hello 衝突中涉及的物件。 hello 所產生的報表[Azure AD Connect Health 進行同步](https://aka.ms/aadchsyncerrors)可協助您識別 hello 兩個物件。
2. 識別哪些物件應該繼續 toohave hello 重複值，以及哪些物件不應該。
3. 從 hello 物件不應該有該值，移除重複的 hello 值。 請注意，您應該進行變更 hello hello 物件源自其中的目錄中的 hello。 在某些情況下，您可能需要 toodelete 的其中一個衝突的 hello 物件。
4. 如果您進行變更 hello 在內部部署 AD 中的 hello，可讓 Azure AD Connect 同步處理 hello 變更。 在 Azure AD Connect Health 進行同步的同步處理錯誤報表取得每隔 30 分鐘更新，並包含 hello hello 最新的同步處理嘗試的錯誤。

## <a name="duplicate-attributes"></a>重複的屬性
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>說明
結構描述不允許 toohave hello hello 遵循的相同值的兩個或多個物件的 azure Active Directory 屬性。 這是在 Azure AD 中的每個物件會強制的 toohave 這些屬性的指定執行個體的唯一值。

* ProxyAddresses
* UserPrincipalName

如果 Azure AD Connect 嘗試 tooadd 新物件或更新現有物件具有值的上述屬性已指派 tooanother 物件在 Azure Active Directory 中的 hello，hello 操作就會導致 hello"AttributeValueMustBeUnique"同步錯誤。

#### <a name="possible-scenarios"></a>可能的案例︰
1. 重複的值是指派的 tooan 已同步處理的物件，可與同步處理的另一個物件衝突。

#### <a name="example-case"></a>範例案例︰
1. **Bob Smith** 是 Azure Active Directory 中已從 contoso.com 的內部部署 Active Directory 同步處理的使用者
2. Bob Smith 的內部部署 **UserPrincipalName** 已設定為 **bobs@contoso.com**。
3. Bob 也有下列值 hello **proxyAddresses**屬性：
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. 新的使用者， **Bob Taylor**，會在內部部署 Active Directory 加入 toohello。
5. Bob Taylor 的 **UserPrincipalName** 已設為 **bobt@contoso.com**。
6. **Bob Taylor**具有下列值 hello hello **ProxyAddresses**屬性 i。 smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. Bob Taylor 物件已成功與 Azure AD 同步處理。
8. 系統管理員決定 tooupdate Bob Taylor 的**ProxyAddresses**屬性以 hello 下列值： 我。 **smtp:bob@contoso.com**
9. Azure AD 將會嘗試 tooupdate Bob taylor 了解的物件值，上述的 hello 與 Azure AD 中，但該作業將會失敗為 ProxyAddresses 值已指派 tooBob Smith，因而導致"AttributeValueMustBeUnique 」 錯誤。

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>如何 toofix AttributeValueMustBeUnique 錯誤
hello hello AttributeValueMustBeUnique 錯誤最常見原因是兩個物件具有不同的 SourceAnchor \(immutableId\)擁有的 hello 相同的 hello ProxyAddresses 及/或 UserPrincipalName 屬性的值。 在訂單 toofix AttributeValueMustBeUnique 錯誤

1. 識別重複的 hello proxyAddresses、 userPrincipalName 或 hello 錯誤造成其他屬性值。 也會識別這兩個\(或多個\)hello 衝突中涉及的物件。 hello 所產生的報表[Azure AD Connect Health 進行同步](https://aka.ms/aadchsyncerrors)可協助您識別 hello 兩個物件。
2. 識別哪些物件應該繼續 toohave hello 重複值，以及哪些物件不應該。
3. 從 hello 物件不應該有該值，移除重複的 hello 值。 請注意，您應該進行變更 hello hello 物件源自其中的目錄中的 hello。 在某些情況下，您可能需要 toodelete 的其中一個衝突的 hello 物件。
4. 如果您進行變更 hello 在內部部署 AD 中的 hello，可讓 Azure AD Connect 同步處理 hello 變更 hello 錯誤 tooget 固定的。

#### <a name="related-articles"></a>相關文章
-[重複或無效的屬性會防止 Office 365 進行目錄同步作業](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>資料驗證失敗
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>說明
Azure Active Directory 會強制執行各種限制允許 hello 目錄中寫入該資料 toobe 之前 hello 資料本身。 這是使用者取得 hello 最佳可能的體驗使用 hello 應用程式相依於此資料時的 tooensure。

#### <a name="scenarios"></a>案例
a. hello UserPrincipalName 屬性值具有無效/不支援的字元。
b. hello UserPrincipalName 屬性未依照 hello 必要的格式。

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>如何 toofix IdentityDataValidationFailed 錯誤
a. 請確定該 hello userPrincipalName 屬性已支援的字元和所需的格式。

#### <a name="related-articles"></a>相關文章
* [準備 tooprovision 使用者可透過目錄同步處理 tooOffice 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>說明
這是特定的情況會導致**"FederatedDomainChangeError"** hello 尾碼的使用者的 UserPrincipalName 變更從一個同盟的網域 tooanother 同盟網域時，同步處理錯誤。

#### <a name="scenarios"></a>案例
針對同步處理的使用者，從一個同盟的網域 tooanother 同盟網域在內部部署變更 hello UserPrincipalName 後置詞。 例如， *UserPrincipalName = bob@contoso.com* 已變更過*UserPrincipalName = bob@fabrikam.com* 。

#### <a name="example"></a>範例
1. Bob Smith，Contoso.com，帳戶加入為新使用者在 Active Directory 中以 hello UserPrincipalNamebob@contoso.com
2. Bob 移動 tooa 不同的區域稱為 Fabrikam.com 和他 UserPrincipalName Contoso.com 的變更toobob@fabrikam.com
3. Contoso.com 和 fabrikam.com 網域都是使用 Azure Active Directory 的同盟網域。
4. Bob 的 userPrincipalName 並不會更新，而導致發生 "FederatedDomainChangeError" 同步處理錯誤。

#### <a name="how-toofix"></a>如何 toofix
如果使用者的 UserPrincipalName 尾碼已更新從 bob @**contoso.com** toobob @**fabrikam.com**，其中同時**contoso.com**和**fabrikam.com**是**同盟網域**，然後依照這些步驟 toofix hello 同步錯誤

1. 從 Azure AD 中更新 hello 使用者的 UserPrincipalName bob@contoso.com toobob@contoso.onmicrosoft.com。您可以使用下列 PowerShell 命令以 hello Azure AD PowerShell 模組的 hello:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. 允許 hello 下一個同步處理循環 tooattempt 同步處理。 此時間同步處理將會成功，而且也會更新 hello UserPrincipalName 的 Bobtoobob@fabrikam.com如預期般。

#### <a name="related-articles"></a>相關文章
* [變更未同步處理 hello Azure Active Directory 同步作業工具之後變更 hello 的使用者帳戶 toouse 不同的同盟網域 UPN](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>說明
當屬性超過允許的大小限制、 長度限制或 Azure Active Directory 結構描述所設定的計數限制 hello 時，hello 同步處理作業會產生 hello **LargeObject**或**ExceededAllowedLength**同步錯誤。 通常會發生此錯誤的下列屬性的 hello

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>可能的案例
1. Bob userCertificate 屬性儲存太多指派憑證 tooBob。 這些可能包含已過期的舊版憑證。 hello 嚴格限制為 15 的憑證。 如需有關如何使用 userCertificate toohandle LargeObject 錯誤屬性，請參閱 tooarticle [userCertificate 屬性所造成的處理 LargeObject 錯誤](active-directory-aadconnectsync-largeobjecterror-usercertificate.md)。
2. Bob userSMIMECertificate 屬性儲存太多指派憑證 tooBob。 這些可能包含已過期的舊版憑證。 hello 嚴格限制為 15 的憑證。
3. Bob thumbnailPhoto 在 Active Directory 中設定是在 Azure AD 中同步處理的 toobe 太大。
4. 自動母體擴展期間的 Active Directory 中的 hello ProxyAddresses 屬性，物件會有太多 ProxyAddresses 指派。

### <a name="how-toofix"></a>如何 toofix
1. 請讓 hello 錯誤該 hello 屬性 hello 允許的限制內。

## <a name="related-links"></a>相關連結
* [在 Active Directory 管理中心找出 Active Directory 物件](https://technet.microsoft.com/library/dd560661.aspx)
* [如何使用 Azure Active Directory PowerShell 物件 tooquery Azure Active Directory](https://msdn.microsoft.com/library/azure/jj151815.aspx)
