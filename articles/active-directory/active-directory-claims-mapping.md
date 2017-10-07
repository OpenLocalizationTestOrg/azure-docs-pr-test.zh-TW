---
title: "Azure Active Directory 中的宣告對應 (公開預覽) | Microsoft Docs"
description: "此頁面說明 Azure Active Directory 宣告對應。"
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Azure Active Directory 中的宣告對應 (公開預覽)

>[!NOTE]
>這項功能會取代並取代 hello[宣告自訂](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization)目前提供透過 hello 入口網站。 如果您要自訂使用 hello 入口網站的宣告此外 toohello 圖形/PowerShell 方法本文中詳述 hello 上相同的應用程式、 針對該應用程式將會忽略 hello 入口網站中的 hello 組態所簽發的權杖。
透過這份文件中詳述的 hello 方法所做的組態將不會反映在 hello 入口網站中。

這項功能會使用其租用戶中特定應用程式的權杖中發出的租用戶系統管理員 」 toocustomize hello 宣告。 您可以使用宣告對應原則來進行下列作業：

- 選取要在權杖中包含哪些宣告。
- 建立尚未存在的宣告類型。
- 選擇或變更 hello 發出特定的宣告中的資料來源。

>[!NOTE]
>這項功能目前為公開預覽版。 準備 toorevert 或移除任何變更。 公開預覽期間的任何 Azure Active Directory (Azure AD) 訂用帳戶中使用 hello 功能。 不過，hello 功能正式推出時，某些層面 hello 功能可能需要 Azure Active Directory premium 訂用帳戶。

## <a name="claims-mapping-policy-type"></a>宣告對應原則類型
在 Azure AD 中，**原則**物件代表個別應用程式或組織中的所有應用程式上強制執行的一組規則。 每種原則有唯一的結構，以一組相關的屬性，然後套用 tooobjects toowhich 會指派給他們。

宣告對應原則是一種**原則**修改 hello 的物件宣告在特定應用程式簽發的權杖中發出。

## <a name="claim-sets"></a>宣告集
某些宣告集會定義其在權杖中的使用方式和時機。

### <a name="core-claim-set"></a>核心宣告集
所宣告的宣告 hello 核心組會在每個權杖，不論原則。 系統會將這些宣告視為受限制宣告，您無法加以修改。

### <a name="basic-claim-set"></a>基本宣告集
hello 基本的宣告集包含 hello 宣告，所發出的權杖 （在加法 toohello 核心宣告集） 的預設值。 可省略這些宣告，或修改使用 hello 宣告對應原則。

### <a name="restricted-claim-set"></a>受限制的宣告集
無法使用原則來修改的受限制宣告。 無法變更 hello 資料來源，並產生這些宣告時，會套用任何轉換。

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>表 1：JSON Web 權杖 (JWT) 的受限制宣告集
|宣告類型 (名稱)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|assertion|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|副本|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|code|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|電子郵件|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|password|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|資源|
|角色|
|角色|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|username|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>表 2：安全性聲明標記語言 (SAML) 的受限制宣告集
|宣告類型 (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>宣告對應原則屬性
使用對應的宣告會發出，因此 hello 資料來自何處，原則 toocontrol 宣告 hello 屬性。 如果沒有原則設定，hello 系統簽發權杖包含 hello 核心宣告集，hello 基本宣告集，並選擇 tooreceive hello 應用程式的任何選擇性宣告。

### <a name="include-basic-claim-set"></a>包含基本宣告集

**字串：**IncludeBasicClaimSet

**資料類型：**布林值 (True 或 False)

**摘要：**此屬性決定 hello 基本的宣告集合是否包含在這個原則影響的語彙基元。 

- 如果組 tooTrue，hello 基本的宣告集中的所有宣告會發出權杖的 hello 原則影響。 
- 如果組 tooFalse，hello 基本的宣告集中的宣告不在 hello 語彙基元，除非它們個別加入 hello hello 宣告結構描述屬性中相同原則。

>[!NOTE] 
>設定會在每個權杖，不論這個屬性設定為宣告 hello 核心宣告。 

### <a name="claims-schema"></a>宣告結構描述

**字串：**ClaimsSchema

**資料類型：**具有一或多個宣告結構描述項目的 JSON blob

**摘要：**此屬性會定義哪些宣告會出現在 hello 原則影響的 hello 語彙基元，此外 toohello 基本宣告集和 hello 核心宣告集。
此屬性中所定義的每個宣告結構描述項目必須有某些資訊。 您必須指定 hello 資料來自何處 (**值**或**來源/識別碼組**)，以及哪個宣告 hello 資料就會發出為 (**宣告的型別**)。

### <a name="claim-schema-entry-elements"></a>宣告結構描述項目的元素

**值：** hello 值項目定義為靜態值為 hello 資料 toobe hello 宣告中所發出。

**來源/識別碼組：** hello 來源和項目指定 ID 定義 hello 宣告中的 hello 資料來自何處。 

hello 來源項目必須設定 tooone hello 以下的： 


- 「 使用者 」: hello hello 資料宣告是 hello 使用者物件上的屬性。 
- 「 應用程式 」: hello hello 資料宣告是 hello 應用程式 （用戶端） 的服務主體上的屬性。 
- 「 資源 」: hello hello 資料宣告是 hello 資源服務主體上的屬性。
- "audience": hello hello 宣告中的資料是 hello 是 hello 對象的 hello 語彙基元 （任一 hello 用戶端或資源服務主體） 的服務主體上的屬性。
- 「 公司 」: hello hello 資料宣告是 hello 資源租用戶的公司物件上的屬性。
- 「 轉換 」: hello hello 資料宣告從宣告轉換 （請參閱本文稍後的 hello"宣告轉換 」 一節）。 

如果 hello 來源是轉換，hello **TransformationID**元素必須包含在這個宣告定義。

hello ID 項目識別哪個 hello 來源上的屬性提供 hello 宣告 hello 值。 hello 下表列出每個值的來源有效的識別碼 hello 的值。

#### <a name="table-3-valid-id-values-per-source"></a>表 3：每個來源的有效識別碼值
|來源|ID|說明|
|-----|-----|-----|
|User|surname|姓氏|
|User|givenname|名字|
|User|displayname|顯示名稱|
|User|objectid|ObjectID|
|User|mail|電子郵件地址|
|User|userprincipalname|使用者主體名稱|
|User|department|department|
|User|onpremisessamaccountname|內部部署的 Sam 帳戶名稱|
|User|netbiosname|NetBios 名稱|
|User|dnsdomainname|Dns 網域名稱|
|User|onpremisesecurityidentifier|內部部署的安全性識別碼|
|User|companyname|組織名稱|
|User|streetaddress|街道地址|
|User|postalcode|郵遞區號|
|User|preferredlanguange|慣用語言|
|User|onpremisesuserprincipalname|內部部署的 UPN|
|User|mailNickname|郵件暱稱|
|User|extensionattribute1|擴充屬性 1|
|User|extensionattribute2|擴充屬性 2|
|User|extensionattribute3|擴充屬性 3|
|User|extensionattribute4|擴充屬性 4|
|User|extensionattribute5|擴充屬性 5|
|User|extensionattribute6|擴充屬性 6|
|User|extensionattribute7|擴充屬性 7|
|User|extensionattribute8|擴充屬性 8|
|User|extensionattribute9|擴充屬性 9|
|User|extensionattribute10|擴充屬性 10|
|User|extensionattribute11|擴充屬性 11|
|User|extensionattribute12|擴充屬性 12|
|User|extensionattribute13|擴充屬性 13|
|User|extensionattribute14|擴充屬性 14|
|User|extensionattribute15|擴充屬性 15|
|User|othermail|其他郵件|
|User|country|國家 (地區)|
|User|city|City|
|User|state|State|
|User|jobtitle|職稱|
|User|employeeid|員工識別碼|
|User|facsimiletelephonenumber|傳真電話號碼|
|application, resource, audience|displayname|顯示名稱|
|application, resource, audience|objected|ObjectID|
|application, resource, audience|tags|服務主體標籤|
|公司|tenantcountry|租用戶的國家/地區|

**TransformationID:** hello TransformationID 元素必須提供來源項目時，才 hello 設定得 「 轉換 」。

- 此項目必須符合在 hello hello 轉換項目的 hello ID 元素**ClaimsTransformation**屬性，定義如何產生此宣告的 hello 資料。

**宣告類型：** hello **JwtClaimType**和**SamlClaimType**元素會定義哪個宣告此宣告的結構描述項目參考。

- hello JwtClaimType 必須包含發出的 Jwt hello 宣告 toobe hello 名稱。
- hello SamlClaimType 必須包含 URI 的 hello 宣告 toobe SAML 權杖中發出的 hello。

>[!NOTE]
>名稱與 Uri 中 hello 的宣告受限制的宣告集不能用於為 hello 宣告型別項目。 如需詳細資訊，請參閱本文稍後 hello < 例外狀況和限制 > 一節。

### <a name="claims-transformation"></a>宣告轉換

**字串：**ClaimsTransformation

**資料類型：**具有一或多個轉換項目的 JSON blob 

**摘要：**使用這個屬性 tooapply 一般轉換 toosource 資料、 toogenerate hello 輸出資料的宣告中指定 hello 宣告結構描述。

**ID:**使用 hello ID 項目 tooreference 此轉換中的項目 hello TransformationID 宣告結構描述項目。 對於這項原則內的每個轉換項目，此值都必須是唯一的。

**TransformationMethod:** hello TransformationMethod 元素會識別哪一個作業已執行的 toogenerate hello hello 宣告的資料。

根據選擇的 hello 方法，必須輸入和輸出的一組。 這些定義使用 hello **InputClaims**，**這**和**OutputClaims**項目。

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>表 4：轉換方法和預期的輸入和輸出
|TransformationMethod|預期的輸入|預期的輸出|說明|
|-----|-----|-----|-----|
|Join|string1、string2、分隔符號|outputClaim|可在輸入字串之間使用分隔符號來聯結這些字串。 例如：string1:"foo@bar.com" , string2:"sandbox" , separator:"." 會導致 outputClaim:"foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|擷取 hello 的電子郵件地址的本機部份。 例如：mail:"foo@bar.com" 會導致 outputClaim:"foo"。 如果不是 @ 符號是存在，則現狀傳回 hello 原始輸入的字串。|

**InputClaims:**使用宣告架構項目 tooa 轉換 InputClaims 元素 toopass hello 的資料。 它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。

- **ClaimTypeReferenceId**聯結與 hello 宣告結構描述項目 toofind hello 適當輸入宣告的 ID 項目。 
- **TransformationClaimType**是使用的 toogive 唯一名稱 toothis 輸入。 此名稱必須符合預期的 hello 輸入 hello 轉換方法的其中一種。

**在這：**使用這項目 toopass 常數值 tooa 轉換。 它有兩個屬性：**值**和**識別碼**。

- **值**hello 實際的常數值 toobe 傳遞。
- **識別碼**是使用的 toogive 唯一名稱 toothis 輸入。 此名稱必須符合預期的 hello 輸入 hello 轉換方法的其中一種。

**OutputClaims:**使用產生的轉換，OutputClaims 元素 toohold hello 資料，並將它連接 tooa 宣告結構描述項目。 它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。

- **ClaimTypeReferenceId**與 hello 識別碼 hello 宣告結構描述項目 toofind hello 適當的輸出宣告的聯結。
- **TransformationClaimType**是使用的 toogive 的唯一名稱 toothis 輸出。 這個名稱必須符合預期的 hello 輸出 hello 轉換方法的其中一個。

### <a name="exceptions-and-restrictions"></a>例外狀況和限制

**SAML NameID 和 UPN:** hello 屬性來源 hello NameID 和 UPN 值與 hello 宣告的允許，轉換會受到限制。

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>表 5：允許作為 SAML NameID 資料來源的屬性
|來源|ID|說明|
|-----|-----|-----|
|User|mail|電子郵件地址|
|User|userprincipalname|使用者主體名稱|
|User|onpremisessamaccountname|內部部署的 Sam 帳戶名稱|
|User|employeeid|員工識別碼|
|User|extensionattribute1|擴充屬性 1|
|User|extensionattribute2|擴充屬性 2|
|User|extensionattribute3|擴充屬性 3|
|User|extensionattribute4|擴充屬性 4|
|User|extensionattribute5|擴充屬性 5|
|User|extensionattribute6|擴充屬性 6|
|User|extensionattribute7|擴充屬性 7|
|User|extensionattribute8|擴充屬性 8|
|User|extensionattribute9|擴充屬性 9|
|User|extensionattribute10|擴充屬性 10|
|User|extensionattribute11|擴充屬性 11|
|User|extensionattribute12|擴充屬性 12|
|User|extensionattribute13|擴充屬性 13|
|User|extensionattribute14|擴充屬性 14|
|User|extensionattribute15|擴充屬性 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>表 6：允許 SAML NameID 使用的轉換方法
|TransformationMethod|限制|
| ----- | ----- |
|ExtractMailPrefix|None|
|Join|要聯結的 hello 尾碼必須 hello 資源的租用戶的已驗證的網域。|

### <a name="custom-signing-key"></a>自訂簽署金鑰
宣告對應原則 tootake 效果 toohello 服務主體物件必須指派自訂的簽署金鑰。 所有簽發的權杖，受到 hello 原則會使用此金鑰簽署。 應用程式必須使用此金鑰進行簽署的設定的 tooaccept 語彙基元。 這可確保通知的語彙基元已被修改的 hello hello 建立者的宣告對應的原則。 這項確認可防止應用程式使用惡意執行者所建立的宣告對應原則。

### <a name="cross-tenant-scenarios"></a>跨租用戶案例
宣告對應原則不會套用 tooguest 使用者。 如果有 guest 使用者嘗試 tooaccess 應用程式與宣告對應原則指派 tooits 服務主體時，發出 hello 預設的語彙基元 （hello 原則沒有任何影響）。

## <a name="claims-mapping-policy-assignment"></a>宣告對應原則指派
宣告對應原則只能指派 tooservice principal 物件。

### <a name="example-claims-mapping-policies"></a>宣告對應原則範例

在 Azure AD 中，當您可以為特定的服務主體自訂權杖中所發出的宣告時，許多案例便可能實現。 在本節中，我們逐步解說，可協助您掌握 toouse hello 如何宣告對應原則類型可為一些常見案例。

#### <a name="prerequisites"></a>必要條件
Hello 遵循範例，在您建立、 更新連結，並刪除服務主體原則。 如果您是新 tooAzure AD，我們建議您了解 tooget 的 Azure AD 租用戶才能繼續進行這些範例。 

tooget 啟動，請勿 hello 下列步驟：


1. 下載最新的 hello [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)。
2.  執行 hello 連接命令 toosign tooyour Azure AD 系統管理員帳戶。 您每次啟動新的工作階段時執行此命令。
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee 命令已建立您的組織，執行下列的 hello 中的所有原則。 我們建議您執行此命令，在 hello 的大部分作業後，下列案例中，預期 toocheck 作為正在建立您的原則。
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>範例： 建立及指派原則 tooomit hello 基本的宣告簽發的權杖 tooa 服務主體。
在此範例中，您建立的原則移除發行的權杖 toolinked hello 基本的宣告集，服務主體。


1. 建立宣告對應原則。 此原則，連結的 toospecific 服務主體，會移除語彙基元中的 hello 基本的宣告集。
    1. toocreate hello 原則，執行下列命令： 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令：
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  指派 hello 原則 tooyour 服務主體。 您也需要 tooget hello 您的服務主體的 ObjectId。 
    1.  toosee 貴組織的所有服務主體中，您可以查詢 Graph。 或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。
    2.  當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>範例： 建立及指派原則 tooinclude hello EmployeeID 和 TenantCountry 權杖中的宣告發出 tooa 服務主體。
在此範例中，您建立原則，將 hello EmployeeID 和 TenantCountry tootokens 發出 toolinked 服務主體。 為 SAML 權杖和 Jwt 中的 hello 名稱宣告類型，就會發出 hello EmployeeID。 以宣告方式 hello 國家 （地區） 在 SAML 權杖和 Jwt 的型別，就會發出 hello TenantCountry。 在此範例中，我們將繼續 tooinclude hello 基本宣告 hello 語彙基元中設定。

1. 建立宣告對應原則。 此原則，連結的 toospecific 服務主體加入 hello EmployeeID 和 TenantCountry 宣告 tootokens。
    1. toocreate hello 原則，執行下列命令：  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令：
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  指派 hello 原則 tooyour 服務主體。 您也需要 tooget hello 您的服務主體的 ObjectId。 
    1.  toosee 貴組織的所有服務主體中，您可以查詢 Graph。 或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。
    2.  當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>範例： 建立及發行的權杖 tooa 服務主體中使用宣告轉換原則指派。
在此範例中，您建立原則，它會發出 tooJWTs 發出 toolinked 服務主體的自訂宣告"JoinedData"。 這個宣告包含聯結 hello 資料儲存在 「.sandbox"hello 使用者物件上的 hello extensionattribute1 屬性中建立的值。 在此範例中，我們會排除 hello 基本 hello 語彙基元中設定的宣告。


1. 建立宣告對應原則。 此原則，連結的 toospecific 服務主體加入 hello EmployeeID 和 TenantCountry 宣告 tootokens。
    1. toocreate hello 原則，執行下列命令： 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee 您新的原則和 tooget hello 原則 ObjectId，執行 hello，下列命令： 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  指派 hello 原則 tooyour 服務主體。 您也需要 tooget hello 您的服務主體的 ObjectId。 
    1.  toosee 貴組織的所有服務主體中，您可以查詢 Graph。 或者，在 Azure AD Graph 總管 中，登入 tooyour Azure AD 帳戶。
    2.  當您擁有 hello ObjectId 的下列命令您服務主體時，執行 hello: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
