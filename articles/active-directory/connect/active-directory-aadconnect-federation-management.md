---
title: "aaaActive Directory Federation Services 管理和使用 Azure AD Connect 自訂 |Microsoft 文件"
description: "使用 Azure AD Connect 進行 AD FS 管理，以及使用 Azure AD Connect 和 PowerShell 的使用者 AD FS 登入經驗的自訂。"
keywords: "AD FS, ADFS, AD FS 管理, AAD Connect, 連線, 登入, AD FS 自訂, 修復信任, O365, 同盟, 信賴憑證者"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>使用 Azure AD Connect 管理和自訂 Active Directory Federation Services
本文說明如何 toomanage 和自訂 Active Directory Federation Services (AD FS)，藉由使用 Azure Active Directory (Azure AD) 連線。 它也包含其他常見的 AD FS 工作，您可能需要 toodo 完成 AD FS 伺服器陣列組態。

| 主題 | 涵蓋內容 |
|:--- |:--- |
| **管理 AD FS** | |
| [修復 hello 信任](#repairthetrust) |如何 toorepair hello 同盟信任與 Office 365。 |
| [使用替代登入識別碼與 Azure AD 建立同盟關係](#alternateid) | 使用替代登入識別碼設定同盟  |
| [新增 AD FS 伺服器](#addadfsserver) |如何 tooexpand AD FS 伺服器與其他的 AD FS 伺服器陣列。 |
| [新增 AD FS Web 應用程式 Proxy 伺服器](#addwapserver) |如何 tooexpand AD FS 伺服器陣列與其他 Web 應用程式 Proxy (WAP) 伺服器。 |
| [新增同盟網域](#addfeddomain) |如何 tooadd 同盟網域。 |
| [Hello SSL 憑證更新](active-directory-aadconnectfed-ssl-update.md)| 如何 tooupdate hello SSL 憑證的 AD FS 伺服器陣列。 |
| **自訂 AD FS** | |
| [新增自訂公司標誌或圖例](#customlogo) |如何 toocustomize AD FS 登入頁面上的公司標誌與插圖。 |
| [新增登入說明](#addsignindescription) |如何 tooadd 登入頁面描述。 |
| [修改 AD FS 宣告規則](#modclaims) |如何 toomodify AD FS 宣告各種同盟案例。 |

## <a name="manage-ad-fs"></a>管理 AD FS
您可以使用 hello Azure AD Connect 精靈，而需要最少使用者介入的 Azure AD Connect 中執行各種不同的 AD FS 相關工作。 安裝 Azure AD Connect 執行 hello 精靈完成之後，您可以執行 hello 精靈一次 tooperform 其他工作。

## 修復 hello 信任<a name=repairthetrust></a>
您可以使用 Azure AD Connect toocheck hello 的目前健全狀況 hello AD FS 與 Azure AD 信任，並採取適當動作 toorepair hello 信任。 請遵循這些步驟 toorepair 您的 Azure AD 與 AD FS 信任。

1. 選取**修復 AAD 與 ADFS 信任**hello 清單中的其他工作。
   ![](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. 在 hello**連接 tooAzure AD**頁面上，提供 Azure AD 全域管理員認證，然後按一下**下一步**。
   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. 在 hello**遠端存取認證**頁面上，輸入 hello 認證 hello 網域系統管理員。

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    在按 [下一步] 之後，Azure AD Connect 會檢查憑證健康情況並顯示任何問題。

    ![憑證的狀態](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    hello**準備 tooconfigure**頁面顯示 hello 的動作清單將會執行 toorepair hello 信任。

    ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. 按一下**安裝**toorepair hello 信任。

> [!NOTE]
> Azure AD Connect 只可以對自我簽署的憑證進行修復或採取動作。 Azure AD Connect 無法修復第三方憑證。

## 使用替代識別碼與 Azure AD 建立同盟關係<a name=alternateid></a>
建議的 hello 內部部署使用者主體 Name(UPN) 和 hello 雲端使用者主體名稱會保留 hello 相同。 如果 hello 內部部署 UPN 會使用非路由傳送的網域 （例如。 Contoso.local) 無法變更或到期 toolocal 應用程式相依性，我們建議您設定替代的登入識別碼。 替代的登入識別碼，可讓您 tooconfigure 登入體驗，使用者可以使用登入其 UPN，例如 mail 以外的屬性。 hello 選項使用者主體名稱在 Azure AD Connect 的預設值 toohello Active Directory 中的 userPrincipalName 屬性。 如果您選擇任何其他屬性來作為使用者主體名稱，而且您使用 AD FS 來建立同盟，則 Azure AD Connect 會就替代登入識別碼對 AD FS 進行設定。 選擇不同屬性來作為使用者主體名稱的範例如下所示︰

![替代識別碼屬性的選擇](media/active-directory-aadconnect-federation-management/attributeselection.png)

AD FS 替代登入識別碼的設定作業包含兩個主要步驟︰
1. **設定 hello 正確的發行宣告集**: hello 發行宣告規則，在 hello Azure AD 信賴憑證者的合作對象信任是修改的 toouse hello 選取 UserPrincipalName 屬性，如 hello 替代 hello 使用者識別碼。
2. **啟用 hello AD FS 組態中的替代登入識別碼**: hello AD FS 設定會更新，讓 AD FS 可以查閱 hello 替代識別碼 hello 適當樹系中的使用者 此設定支援 Windows Server 2012 R2 (含 KB2919355) 或更新版本上的 AD FS。 如果 hello AD FS 伺服器 2012 R2，hello hello 存在的 Azure AD Connect 檢查需要 KB。 如果 hello 無法偵測 KB，將會顯示警告之後完成組態，如下所示：

    ![2012 R2 上缺少 KB 的警告](media/active-directory-aadconnect-federation-management/kbwarning.png)

    發生遺漏 KB，toorectify hello 組態安裝所需的 hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) ，然後修復 hello 信任使用[修復 AAD 與 AD FS 信任](#repairthetrust)。

> [!NOTE]
> 如需有關 alternateID 和步驟 toomanually 設定，請閱讀[設定替代的登入識別碼](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## 新增 AD FS 伺服器 <a name=addadfsserver></a>

> [!NOTE]
> tooadd AD FS 伺服器，Azure AD Connect 需要 hello PFX 憑證。 因此，您可以執行這項作業，只有當您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列中。

1. 選取 [部署其他同盟伺服器]，然後按 [下一步]。

   ![其他同盟伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. 在 hello**連接 tooAzure AD**頁面上，輸入 Azure AD 全域管理員認證，然後按一下**下一步**。

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. 提供 hello 網域系統管理員認證。

   ![網域系統管理員認證](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect 會要求您使用 Azure AD Connect 設定新的 AD FS 伺服器陣列時所提供的 hello PFX 檔案的 hello 密碼。 按一下**輸入密碼**tooprovide hello hello PFX 檔案密碼。

   ![憑證密碼](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. 在 hello **AD FS 伺服器**頁面上，輸入 hello 伺服器名稱或 IP 位址 toobe 加入 toohello AD FS 伺服器陣列。

   ![AD FS 伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. 按一下**下一步**，並瀏覽 hello 最終**設定**頁面。 Azure AD Connect 已完成將加入 hello 伺服器 toohello AD FS 伺服器陣列之後，您會獲得 hello 選項 tooverify hello 連線。

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![安裝完成](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## 新增 AD FS WAP 伺服器 <a name=addwapserver></a>

> [!NOTE]
> tooadd WAP 伺服器，Azure AD Connect 需要 hello PFX 憑證。 因此，您只可以執行這項作業，如果您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列。

1. 選取**部署 Web 應用程式 Proxy**從 hello 可用工作的清單。

   ![部署 Web 應用程式 Proxy](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. 提供 hello Azure 全域管理員認證。

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. 在 hello**指定 SSL 憑證**頁面上，您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列時所提供的 hello PFX 檔案提供 hello 密碼。
   ![憑證密碼](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. 新增 hello 伺服器 toobe 加入做為 WAP 伺服器。 Hello WAP 伺服器可能不是聯結的 toohello 網域，因為 hello 精靈即會詢問要新增的系統管理認證 toohello 伺服器。

   ![管理伺服器認證](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. 在 hello **Proxy 信任認證**頁面上，提供系統管理認證 tooconfigure hello proxy 信任及存取 hello 主要伺服器 hello AD FS 伺服器陣列中的。

   ![Proxy 信任憑證](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. 在 [hello**準備 tooconfigure** ] 頁面上，hello 精靈會顯示 hello 將執行的動作清單。

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. 按一下**安裝**toofinish hello 組態。 Hello 設定完成之後，hello 精靈 」 提供 hello 選項 tooverify hello 連線 toohello 伺服器。 按一下**確認**toocheck 連線。

   ![安裝完成](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## 新增同盟網域 <a name=addfeddomain></a>

它是簡單 tooadd 網域 toobe 同盟與 Azure AD 使用 Azure AD Connect。 Azure AD Connect 新增 hello 同盟網域，並修改 hello 宣告規則 toocorrectly 反映 hello 簽發者，如果您有多個網域與 Azure AD 建立同盟。

1. tooadd 同盟網域，選取 hello 工作**新增其他 Azure AD 網域**。

   ![其他 Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. 在 hello hello 精靈的下一個頁面上，提供 Azure AD 中的 hello 全域系統管理員認證。

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. 在 hello**遠端存取認證**頁面上，提供 hello 網域系統管理員認證。

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. 在 hello 下一個頁面上，hello 精靈會提供您可以建立與您在內部部署目錄同盟的 Azure AD 網域的清單。 Hello 清單中選擇 hello 網域。

   ![Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    選擇 hello 網域之後，請 hello 精靈會提供您與 hello 精靈的進一步動作的適當資訊將會接受並 hello hello 設定的影響。 在某些情況下，如果您選取的網域，不尚未驗證在 Azure AD 中 hello 精靈為您提供資訊 toohelp 會確認 hello 網域。 請參閱[加入您的自訂網域名稱 tooAzure Active Directory](../active-directory-add-domain.md)如需詳細資訊。

5. 按一下 [下一步] 。 hello**準備 tooconfigure**頁面會顯示 hello Azure AD Connect 會執行的動作清單。 按一下**安裝**toofinish hello 組態。

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> 使用者從 hello 加入之前，會先無法 toologin tooAzure AD 同盟的網域必須進行同步處理。

## <a name="ad-fs-customization"></a>AD FS 自訂
hello 下列各節提供有關一些 hello 常見工作的詳細資料，當您自訂 AD FS 登入頁面上，您可能必須 tooperform。

## 新增自訂公司標誌或圖例 <a name=customlogo></a>
會顯示在 hello hello 公司 toochange hello 標誌**登入**頁面上，使用下列 Windows PowerShell cmdlet 和語法的 hello。

> [!NOTE]
> hello 建議維度 hello 標誌為 260 x 35 @ 96 dpi，檔案大小不超過 10 KB。

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> hello *TargetName*參數是必要項。 釋放與 AD FS 的 hello 預設佈景主題是名為 Default。

## 新增登入說明 <a name=addsignindescription></a>
登入頁面描述 toohello tooadd**登入頁面**，使用下列 Windows PowerShell cmdlet 和語法的 hello。

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## 修改 AD FS 宣告規則 <a name=modclaims></a>
AD FS 支援豐富的宣告語言，您可以使用 toocreate 自訂宣告規則。 如需詳細資訊，請參閱[hello hello 宣告規則語言的角色](https://technet.microsoft.com/library/dd807118.aspx)。

hello 下列章節說明如何撰寫自訂規則，在某些情況下讓 tooAzure AD 和 AD FS 同盟產生關聯。

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>條件式出現在 hello 屬性中的值上的固定 ID
Azure AD Connect 可讓您指定做為來源錨點的物件時進行同步處理 tooAzure AD 屬性 toobe。 如果 hello 自訂屬性中的 hello 值不是空的您可能想 tooissue 不可變的識別碼宣告。

例如，您可能會選取**ms-ds-consistencyguid**為 hello 來源錨點和問題的 hello 屬性**ImmutableID**為**ms-ds-consistencyguid**中案例的 hello屬性有對它的值。 如果沒有針對 hello 屬性值，發出**objectGuid**為 hello 不可變的識別碼。 Hello 之後 > 一節中所述，您可以建構 hello 自訂宣告規則集。

**規則 1：查詢屬性**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

這項規則，在您要查詢的 hello 值**ms-ds-consistencyguid**和**objectGuid** hello 從 Active Directory 的使用者。 Hello 存放區名稱 tooan 適當的存放區中變更名稱 AD FS 部署。 也 hello 宣告型別 tooa 適當的宣告類型變更為您的同盟，為所定義的**objectGuid**和**ms-ds-consistencyguid**。

此外，藉由使用**新增**而非**問題**，避免加入 hello 實體的連出問題，並可以使用 hello 值作為中間值。 您將發行更新版本的規則中的 hello 宣告之後您建立哪些值 toouse hello 不可變的識別碼。

**規則 2： 檢查 ms-ds-consistencyguid 存在 hello 使用者**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

此規則會定義稱為暫存旗標**idflag**太設定**useguid**如果沒有任何**ms-ds-consistencyguid** hello 使用者填入。 這背後的 hello 邏輯是 hello 事實 AD FS 不允許空的宣告。 因此當您新增宣告 http://contoso.com/ws/2016/02/identity/claims/objectguid 和 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid 規則 1 」 中，您得到**msdsconsistencyguid**宣告才hello 使用者會填入 hello 值。 如果未填入，AD FS 會看到它將具有空值，並因此立即捨棄。 所有物件都會有 **objectGuid**，因此執行規則 1 之後，宣告一律會在該處。

**規則 3：發出 ms-ds-consistencyguid 為固定 ID (如果有的話)**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

這是隱含的 **存在** 檢查。 如果 hello hello 宣告值存在，然後發出，做為不可變的 hello 識別碼。 hello 上一個範例使用 hello **nameidentifier**宣告。 您必須 toochange 此 toohello 適當的宣告類型 hello 不可變的識別碼在您的環境中。

**規則 4：發出 objectGuid 做為固定 ID，如果未出現 ms-ds-consistencyGuid**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

在這項規則，只會檢查 hello 暫存旗標**idflag**。 您可以決定是否要根據 tooissue hello 宣告於它的值。

> [!NOTE]
> 這些規則 hello 順序十分重要。

### <a name="sso-with-a-subdomain-upn"></a>使用子網域 UPN 的 SSO
您可以加入多個網域 toobe 中所述，使用 Azure AD Connect，同盟[加入新的同盟的網域](active-directory-aadconnect-federation-management.md#addfeddomain)。 您必須修改 hello 使用者主要名稱 (UPN) 宣告，讓 hello 簽發者 ID 對應 toohello 根網域和不 hello 子網域，因為 hello 同盟的根網域也涵蓋 hello 子系。

根據預設，hello 會簽發者識別碼設定為宣告規則：

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![預設簽發者識別碼宣告](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

hello 預設規則只會採用 hello UPN 尾碼，並會在 hello 簽發者 ID 宣告中。 比方說，John 是 sub.contoso.com 中的使用者，而 contoso.com 與 Azure AD 同盟。 John 進入john@sub.contoso.com為 hello 時 tooAzure AD 在登入的使用者名稱。 hello 預設簽發者 ID 宣告規則中 AD FS 中 hello 下列方式處理它：

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**宣告值：**http://sub.contoso.com/adfs/services/trust/

toohave 唯一 hello 根網域中 hello 簽發者宣告值，變更 hello 宣告規則 toomatch hello 下列：

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>後續步驟
深入了解 [使用者登入選項](active-directory-aadconnect-user-signin.md)。
