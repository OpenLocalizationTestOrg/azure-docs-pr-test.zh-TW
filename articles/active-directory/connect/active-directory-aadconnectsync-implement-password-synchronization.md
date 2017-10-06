---
title: "搭配 Azure AD Connect 同步化 aaaImplement 密碼同步化 |Microsoft 文件"
description: "提供有關的資訊，密碼同步化的運作方式以及 tooset 組成。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>使用 Azure AD Connect 同步處理實作密碼同步處理
本文章提供您需要 toosynchronize 您的使用者密碼從內部部署 Active Directory 執行個體 tooa 雲端型 Azure Active Directory (Azure AD) 執行個體的資訊。

## <a name="what-is-password-synchronization"></a>什麼是密碼同步處理
hello 機率封鎖的從 tooa 忘記的密碼到期完成工作相關 toohello 數目的不同的密碼，您需要 tooremember。 hello 需要 tooremember，hello 高 hello 機率 tooforget 其中一個更多的密碼。 問題和密碼重設和其他密碼相關的問題有關的呼叫 hello 最多的技術支援資源。

密碼同步處理是一項功能使用 toosynchronize 使用者密碼從內部部署 Active Directory 執行個體 tooa 以雲端為基礎的 Azure AD 執行個體。
使用此功能 toosign tooAzure AD 服務，例如 Office 365、 Microsoft Intune、 CRM Online 和 Azure Active Directory 網域服務 (Azure AD DS) 中。 您登入 toohello 服務使用 hello toosign 用於 tooyour 相同的密碼在內部部署 Active Directory 執行個體。

![何謂 Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

透過減少 hello 密碼數目，您的使用者需要 toomaintain toojust 其中一個。 密碼同步處理可協助您︰

* 改善使用者的 hello 產能。
* 降低技術支援成本。  

此外，如果您決定 toouse[與 Active Directory Federation Services (AD FS) 同盟](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)，萬一您的 AD FS 基礎結構失敗時，您可以選擇在設定密碼同步作業，以當作備份設定。

密碼同步處理是藉由 Azure AD Connect 同步處理延伸模組 toohello 目錄同步作業功能。toouse 密碼同步處理您的環境中，您要：

* 安裝 Azure AD Connect。  
* 設定內部部署 Active Directory 執行個體與 Azure Active Directory 執行個體之間的目錄同步作業。
* 啟用密碼同步處理。

如需詳細資訊，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

> [!NOTE]
> 如需針對 FIPS 和密碼同步處理所設定之 Azure Active Directory Domain Services 的詳細資訊，請參閱本文稍後的＜密碼同步處理和 FIPS＞。
>
>

## <a name="how-password-synchronization-works"></a>密碼同步處理如何運作
hello Active Directory 網域服務會將密碼儲存 hello 形式 hello 實際使用者密碼的雜湊值表示法。 雜湊值是單向數學函式的結果 (hello*雜湊演算法*)。 沒有密碼的單向函式 toohello 純文字版的 hello 方法 toorevert 的結果。 您無法使用密碼雜湊 toosign tooyour 在內部部署網路中。

您的密碼，Azure AD Connect 同步處理會擷取您的密碼雜湊，從 toosynchronize hello 在內部部署 Active Directory 執行個體。 套用額外的安全性處理 toohello 密碼雜湊之前同步處理 toohello Azure Active Directory 驗證服務。 密碼會以每個使用者為基礎，依照時間先後順序來進行同步處理。

hello 實際資料流程 hello 密碼同步處理程序是類似 toohello 同步處理的使用者資料，例如顯示名稱或電子郵件地址。 不過，密碼會同步處理頻率會比 hello 標準目錄同步處理期間，其他屬性。 hello 密碼同步處理程序執行每 2 分鐘。 您無法修改此程序的 hello 頻率。 當您同步處理密碼時，它會覆寫現有雲端密碼 hello。

hello 第一次啟用 hello 密碼同步功能，它會執行初始同步處理的 hello 的範圍內的所有使用者的密碼。 您無法明確地定義您想 toosynchronize 使用者密碼的子集。

當您變更在內部部署密碼時，hello 更新密碼會同步處理，通常會在幾分鐘的時間。
hello 密碼同步功能會自動重試失敗的同步處理嘗試。 如果嘗試 toosynchronize 密碼時發生錯誤，錯誤會記錄在事件檢視器中。

hello 同步處理密碼的 hello 使用者目前登入沒有任何影響。
當您登入 tooa 雲端服務時，就會發生同步處理的密碼變更立即不影響目前的雲端服務工作階段。 不過，當 hello 雲端服務會要求您 tooauthenticate 一次，您需要 tooprovide 新密碼。

第二個時間 tooauthenticate tooAzure AD，不論它們是否簽署 tootheir 公司網路中時，使用者必須輸入其公司認證。 這些模式可以最小化，不過，如果 hello 使用者在登入時 (KMSI) 核取方塊選取 hello 讓我保持登。 此選取動作會設定工作階段 Cookie 在短期間內略過驗證。 KMSI 行為可以啟用或停用 hello Azure AD 系統管理員。

> [!NOTE]
> 密碼同步處理才支援 Active Directory 中的 hello 物件類型使用者。 不支援 hello iNetOrgPerson 物件類型。

### <a name="detailed-description-of-how-password-synchronization-works"></a>密碼同步處理運作方式的詳細描述
hello 以下描述深入了解密碼同步處理 Active Directory 與 Azure AD 之間的運作方式。

![詳細的密碼流程](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. 每兩分鐘，hello AD 連線伺服器上的 hello 密碼同步處理代理程式要求儲存的密碼雜湊 （hello unicodePwd 屬性） 的 DC，以透過標準的 hello [MS DRSR](https://msdn.microsoft.com/library/cc228086.aspx)使用 toosynchronize 資料複寫通訊協定。之間的 Dc。 hello 服務帳戶必須具有複寫目錄變更 」 和 「 複寫目錄變更所有 AD （授與的預設安裝） 的權限 tooobtain hello 密碼雜湊。
2. 在傳送之前，hello DC hello MD4 密碼雜湊會使用加密的金鑰[MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hello RPC 工作階段金鑰和 salt 的雜湊。 接著會透過 RPC 傳送嗨結果 toohello 密碼同步處理代理程式。 hello DC 也會傳遞 hello salt toohello 同步代理程式利用 hello DC 複寫通訊協定，因此 hello 代理程式無法 toodecrypt hello 信封。
3.  Hello 密碼同步處理代理程式有 hello 加密的信封之後，就會使用[MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx)和 hello salt toogenerate 金鑰 toodecrypt hello 收到資料後 tooits 原始 MD4 格式。 沒有任何一點 hello 密碼同步處理代理程式沒有存取 toohello 純文字密碼。 hello MD5 使用密碼同步處理代理程式的主要是以 hello DC，複寫通訊協定相容性，它只會用於內部部署 hello DC 與 hello 密碼同步處理代理程式之間。
4.  hello 密碼同步處理代理程式第一個轉換 hello 雜湊 tooa 32 位元組十六進位字串，來展開 hello 16 位元組二進位密碼雜湊 too64 位元組，則此字串轉換成以 utf-16 編碼的二進位檔放回。
5.  hello 密碼同步處理代理程式會加入 salt，組成 10 位元組長度 salt，toohello 64 位元組的二進位 toofurther 保護 hello 原始雜湊。
6.  hello 密碼同步處理代理程式結合 hello MD4 雜湊和 salt，然後輸入 hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt)函式。 1000 個反覆運算的 hello [hmac-sha256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx)會使用索引鍵的雜湊演算法。 
7.  hello 密碼同步處理代理程式會採用 hello 產生 32 位元雜湊，串連這兩個 hello salt hello SHA256 反覆項目 tooit （適用於使用 Azure ad） 的數目再傳輸來自 Azure AD Connect tooAzure AD 透過 SSL 的 hello 字串。</br> 
8.  當使用者嘗試 toosign tooAzure AD 中的，並輸入其密碼、 hello 密碼透過 hello 執行相同的 MD4 + salt + PBKDF2 + hmac-sha256 程序。 如果 hello 產生雜湊符合儲存在 Azure AD 中的 hello 雜湊，hello 使用者已進入 hello 正確的密碼，並驗證。 

>[!Note] 
>hello 原始 MD4 雜湊不是傳輸的 tooAzure AD。 相反地，會傳送 hello hello 原始的 MD4 雜湊 SHA256 雜湊。 如此一來，取得儲存在 Azure AD 中的 hello 雜湊時，如果它不能在內部部署密碼的雜湊攻擊中。

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>密碼同步處理如何與 Azure Active Directory Domain Services 搭配運作
您也可以使用 hello 密碼同步處理功能 toosynchronize 在內部部署密碼太[Azure Active Directory 網域服務](../../active-directory-domain-services/active-directory-ds-overview.md)。 在此案例中，hello Azure Active Directory 網域服務執行個體會向使用者在 hello 雲端中的驗證您在內部部署 Active Directory 執行個體中所有 hello 方法。 此案例的 hello 體驗為在內部部署環境中類似的 toousing hello Active Directory 遷移工具 (ADMT)。

### <a name="security-considerations"></a>安全性考量
當同步處理密碼，hello 純文字密碼版本不是公開的 toohello 密碼同步功能、 tooAzure AD，或任何相關聯的 hello 服務。

使用者的驗證會針對 Azure AD 中，而不是反對 hello 組織自己的 Active Directory 執行個體。 如果您的組織有疑慮留下任何形式的密碼資料 hello 內部部署，您可以考慮該 hello SHA256 密碼資料儲存在 Azure AD-hello 事實的原始 MD4 雜湊 hello-雜湊是遠比什麼儲存在 Active Directory 安全。 此外，無法解密此 SHA256 雜湊，因為它無法被帶回 toohello 組織的 Active Directory 環境，呈現為有效的使用者密碼在傳遞的雜湊攻擊中。





### <a name="password-policy-considerations"></a>密碼原則考量
啟用密碼同步處理會影響兩種類型的密碼原則：

* 密碼複雜性原則
* 密碼到期原則

#### <a name="password-complexity-policy"></a>密碼複雜性原則  
啟用密碼同步處理時，在內部部署 Active Directory 執行個體中的 hello 密碼複雜性原則覆寫已同步處理使用者的 hello 雲端中的複雜性原則。 您可以使用所有 hello 有效密碼從您在內部部署 Active Directory 執行個體 tooaccess Azure AD 服務。

> [!NOTE]
> 直接在 hello 雲端中建立的使用者密碼仍主旨 toopassword 原則 hello 雲端中所定義。

#### <a name="password-expiration-policy"></a>密碼到期原則  
如果使用者在 hello 的密碼同步處理的範圍內，hello 雲端帳戶密碼設定得*永遠不過期*。

您可以繼續 toosign tooyour 雲端服務中，使用同步處理內部部署環境中已過期的密碼。 更新您的雲端密碼 hello 變更 hello 密碼 hello 在內部部署環境中的下一次。

#### <a name="account-expiration"></a>帳戶到期
如果您的組織使用 hello accountExpires 屬性做為使用者帳戶管理的一部分，請注意這個屬性不是已同步處理的 tooAzure AD。 如此一來，針對密碼同步處理設定之環境中到期的 Active Directory 帳戶在 Azure AD 仍然為作用中。 我們建議如果 hello 帳戶到期，工作流程動作應該觸發停用 hello 使用者的 Azure AD 帳戶的 PowerShell 指令碼。 相反地，當開啟 hello 帳戶時，hello Azure AD 執行個體應該會開啟。

### <a name="overwrite-synchronized-passwords"></a>覆寫已同步的密碼
系統管理員可以使用 Windows PowerShell 手動重設您的密碼。

在此情況下，hello 新密碼會覆寫已同步處理的密碼，並在 hello 雲端中定義的所有密碼原則都會套用的 toohello 新密碼。

如果您再次變更內部部署密碼，hello 新密碼會同步處理 toohello 雲端，而且它會覆寫 hello 手動更新密碼。

hello 同步處理密碼的 hello Azure 登入的使用者沒有任何影響。 您已登入 tooa 雲端服務時，就會發生同步處理的密碼變更立即不影響目前的雲端服務工作階段。 KMSI 擴充 hello 持續時間，這項差異。 當 hello 雲端服務會要求您 tooauthenticate 一次時，您需要 tooprovide 新密碼。

### <a name="additional-advantages"></a>其他優點

- 一般而言，密碼同步化是簡單 tooimplement 比 federation service。 它不需要任何額外的伺服器，並排除高可用性的同盟服務 tooauthenticate 使用者相依性。 
- 也可以加入 toofederation 中啟用密碼同步處理。 您可以將它作為同盟服務發生中斷時的後援服務。












## <a name="enable-password-synchronization"></a>啟用密碼同步處理
當您安裝 Azure AD Connect 使用 hello**快速設定**選項時，密碼同步化會自動啟用。 如需詳細資訊，請參閱[使用快速設定開始使用 Azure AD Connect](active-directory-aadconnect-get-started-express.md)。

如果您使用自訂設定，當您安裝 Azure AD Connect，密碼同步功能 hello 使用者登入頁面。 如需詳細資訊，請參閱[自訂 Azure AD Connect 安裝](active-directory-aadconnect-get-started-custom.md)。

![啟用密碼同步處理](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>密碼同步處理和 FIPS
如果您的伺服器已經鎖定，根據 tooFederal 資訊處理標準 (FIPS)，則會停用 MD5。

**密碼同步化的 tooenable MD5 執行 hello 下列步驟：**

1. 移 too%programfiles%\Azure AD Sync\Bin。
2. 開啟 miiserver.exe.config。
3. 請移至在 hello hello 檔案結尾處的 toohello configuration/runtime 節點。
4. 新增節點的後的 hello:`<enforceFIPSPolicy enabled="false"/>`
5. 儲存您的變更。

如需參考，此程式碼片段就是其大致樣貌︰

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

如需安全性和 FIPS 的詳細資訊，請參閱 [AAD 密碼同步、加密和 FIPS 合規性](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/)。

## <a name="troubleshoot-password-synchronization"></a>對密碼同步處理進行疑難排解
如果您在進行密碼同步處理時發生問題，請參閱[針對密碼同步處理進行疑難排解](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)。

## <a name="next-steps"></a>後續步驟
* [Azure AD Connect 同步處理：自訂同步處理選項](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
