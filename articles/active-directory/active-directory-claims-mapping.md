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
ms.openlocfilehash: 78dbbe085fca26ad529c6262ba852f3c06ace404
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Azure Active Directory 中的宣告對應 (公開預覽)

>[!NOTE]
>這項功能會取代目前透過入口網站提供的[宣告自訂](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization)。 如果您在相同的應用程式中除了使用本文詳述的 Graph/PowerShell 方法外，還使用入口網站來自訂宣告，則針對該應用程式所核發的權杖將會忽略入口網站中的設定。
透過本文詳述的方法所進行的設定將不會反映在入口網站中。

租用戶系統管理員會使用這項功能，以針對其租用戶的特定應用程式自訂權杖中所發出的宣告。 您可以使用宣告對應原則來進行下列作業：

- 選取要在權杖中包含哪些宣告。
- 建立尚未存在的宣告類型。
- 選擇或變更特定宣告中所發出的資料來源。

>[!NOTE]
>這項功能目前為公開預覽版。 您應做好將任何變更還原或移除的準備。 公用預覽版期間功能可用於任何 Azure Active Directory (Azure AD) 訂用帳戶。 不過，當功能正式推出時，功能的某些層面可能需要 Azure Active Directory Premium 訂用帳戶。

## <a name="claims-mapping-policy-type"></a>宣告對應原則類型
在 Azure AD 中，**原則**物件代表個別應用程式或組織中的所有應用程式上強制執行的一組規則。 每個類型的原則都具有包含一組屬性的獨特結構，這些屬性會接著套用至它們已被指派的物件。

宣告對應原則是一種**原則**物件，會修改針對特定應用程式所核發之權杖所發出的宣告。

## <a name="claim-sets"></a>宣告集
某些宣告集會定義其在權杖中的使用方式和時機。

### <a name="core-claim-set"></a>核心宣告集
核心宣告集中的宣告會出現在每個權杖中，不論其原則為何。 系統會將這些宣告視為受限制宣告，您無法加以修改。

### <a name="basic-claim-set"></a>基本宣告集
基本宣告集包含預設會針對權杖所發出的宣告 (除了核心宣告集以外)。 使用宣告對應原則即可省略或修改這些宣告。

### <a name="restricted-claim-set"></a>受限制的宣告集
無法使用原則來修改的受限制宣告。 您無法變更資料來源，而且在產生這些宣告時不會套用任何轉換。

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
使用宣告對應原則屬性，即可控制要發出哪些宣告，以及要從哪個來源取得資料。 如果未設定任何原則，系統所發出的權杖就會包含核心宣告集、基本宣告集，以及應用程式選擇要收到的任何選擇性宣告。

### <a name="include-basic-claim-set"></a>包含基本宣告集

**字串：**IncludeBasicClaimSet

**資料類型：**布林值 (True 或 False)

**摘要：**此屬性會決定是否在此原則所影響到的權杖中包含基本宣告集。 

- 如果設為 True，此原則所影響到的權杖中就會發出基本宣告集。 
- 如果設為 False，權杖中將不會包含基本宣告集的宣告，除非相同原則的宣告結構描述屬性中個別新增了這些宣告。

>[!NOTE] 
>核心宣告集中的宣告會出現在每個權杖中，不論此屬性的設定為何。 

### <a name="claims-schema"></a>宣告結構描述

**字串：**ClaimsSchema

**資料類型：**具有一或多個宣告結構描述項目的 JSON blob

**摘要：**此屬性會定義除了基本宣告集和核心宣告集以外，原則所影響到的權杖中還會有哪些宣告。
此屬性中所定義的每個宣告結構描述項目必須有某些資訊。 您必須指定資料來自何處 (**值**或**來源/識別碼組**)，以及資料是以哪種宣告形式來發出 (**宣告類型**)。

### <a name="claim-schema-entry-elements"></a>宣告結構描述項目的元素

**值：**值元素會定義靜態值來作為宣告中發出的資料。

**來源/識別碼組：**來源和識別碼元素會定義宣告中的資料來自何處。 

來源元素必須設為下列其中一個值： 


- 「使用者」：宣告中的資料是使用者物件上的屬性。 
- 「應用程式」：宣告中的資料是應用程式 (用戶端) 服務主體上的屬性。 
- 「資源」：宣告中的資料是資源服務主體上的屬性。
- 「對象」：宣告中的資料是作為權杖對象之服務主體 (用戶端或資源服務主體) 上的屬性。
- 「公司」：宣告中的資料是資源租用戶之公司物件上的屬性。
- 「轉換」：宣告中的資料來自宣告轉換 (請參閱本文稍後的＜宣告轉換＞一節)。 

如果來源是轉換，則 **TransformationID** 元素也必須包含在這個宣告定義中。

識別碼元素可識別宣告的值是由來源上的哪個屬性所提供。 下表列出每個來源值的有效識別碼值。

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

**TransformationID：**只有在來源元素設定為「轉換」時，才必須提供 TransformationID 元素。

- 此元素必須符合 **ClaimsTransformation** 屬性 (會定義如何產生此宣告的資料) 中轉換項目的識別碼元素。

**宣告類型：****JwtClaimType** 和 **SamlClaimType** 元素會定義此宣告結構描述項目是參考哪個宣告。

- JwtClaimType 必須包含要在 JWT 中發出的宣告名稱。
- SamlClaimType 必須包含要在 SAML 權杖中發出的宣告 URI。

>[!NOTE]
>受限制宣告集裡面所含宣告的名稱和 URI 不能用於宣告類型元素。 如需詳細資訊，請參閱本文稍後的＜例外狀況和限制＞一節。

### <a name="claims-transformation"></a>宣告轉換

**字串：**ClaimsTransformation

**資料類型：**具有一或多個轉換項目的 JSON blob 

**摘要：**使用此屬性可對來源資料套用常見的轉換，以便為宣告結構描述中指定的宣告產生輸出資料。

**識別碼：**使用識別碼元素可在 TransformationID 宣告結構描述項目中參考此轉換項目。 對於這項原則內的每個轉換項目，此值都必須是唯一的。

**TransformationMethod：**TransformationMethod 元素可識別該執行哪個作業才能為宣告產生資料。

根據您所選擇的方法，系統預期會有一組輸入和輸出。 您可以使用 **InputClaims**、**InputParameters** 和 **OutputClaims** 元素來定義這些輸入和輸出。

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>表 4：轉換方法和預期的輸入和輸出
|TransformationMethod|預期的輸入|預期的輸出|說明|
|-----|-----|-----|-----|
|Join|string1、string2、分隔符號|outputClaim|可在輸入字串之間使用分隔符號來聯結這些字串。 例如：string1:"foo@bar.com" , string2:"sandbox" , separator:"." 會導致 outputClaim:"foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|擷取電子郵件地址的本機部分。 例如：mail:"foo@bar.com" 會導致 outputClaim:"foo"。 如果沒有 @ 符號，則原始輸入字串會以現狀傳回。|

**InputClaims：**使用 InputClaims 元素可從宣告結構描述項目將資料傳遞至轉換。 它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。

- **ClaimTypeReferenceId** 會與宣告結構描述項目的識別碼元素聯結以尋找適當的輸入宣告。 
- **TransformationClaimType** 則可用來為此輸入指定唯一的名稱。 此名稱必須符合轉換方法的其中一個預期輸入。

**InputParameters：**使用 InputParameters 元素可對轉換傳遞常數值。 它有兩個屬性：**值**和**識別碼**。

- **值**是要傳遞的實際常數值。
- **識別碼**則可用來為此輸入指定唯一的名稱。 此名稱必須符合轉換方法的其中一個預期輸入。

**OutputClaims：**使用 OutputClaims 元素可保留轉換所產生的資料，並將資料繫結到宣告結構描述項目。 它有兩個屬性：**ClaimTypeReferenceId** 和 **TransformationClaimType**。

- **ClaimTypeReferenceId** 會與宣告結構描述項目的識別碼聯結以尋找適當的輸出宣告。
- **TransformationClaimType** 則可用來為此輸出指定唯一的名稱。 此名稱必須符合轉換方法的其中一個預期輸出。

### <a name="exceptions-and-restrictions"></a>例外狀況和限制

**SAML NameID 和 UPN：**您用來取得 NameID 和 UPN 值的來源屬性以及所允許的宣告轉換會受到限制。

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
|Join|所聯結的尾碼必須是資源租用戶的已驗證網域。|

### <a name="custom-signing-key"></a>自訂簽署金鑰
您必須對服務主體物件指派自訂簽署金鑰，宣告對應原則才會生效。 所有已核發並受到該原則影響的權杖皆會使用此金鑰來簽署。 您必須將應用程式設定為接受使用此金鑰所簽署的權杖。 這可確保系統確認宣告對應原則的建立者已修改權杖。 這項確認可防止應用程式使用惡意執行者所建立的宣告對應原則。

### <a name="cross-tenant-scenarios"></a>跨租用戶案例
宣告對應原則不適用於來賓使用者。 如果有來賓使用者嘗試使用指派給應用程式服務主體的宣告對應原則來存取應用程式，系統就會核發預設權杖 (原則沒有任何效果)。

## <a name="claims-mapping-policy-assignment"></a>宣告對應原則指派
宣告對應原則只能指派給服務主體物件。

### <a name="example-claims-mapping-policies"></a>宣告對應原則範例

在 Azure AD 中，當您可以為特定的服務主體自訂權杖中所發出的宣告時，許多案例便可能實現。 在本節中，我們將逐步解說一些常見案例，以協助您掌握如何使用宣告對應原則類型。

#### <a name="prerequisites"></a>必要條件
在下列範例中，您會為服務主體建立、更新、連結和刪除原則。 如果您是 Azure AD 的新手，我們建議您先深入了解如何取得 Azure AD 租用戶，然後再利用這些範例繼續進行。 

若要開始使用，請執行下列步驟：


1. 下載最新的 [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)。
2.  執行 Connect 命令以登入您的 Azure AD 管理帳戶。 您每次啟動新的工作階段時執行此命令。
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  若要查看在組織中建立的所有原則，請執行下列命令。 建議您在進行完下列案例中的大部分作業之後執行此命令，以確認原則是否如預期般地建立。
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-to-omit-the-basic-claims-from-tokens-issued-to-a-service-principal"></a>範例：建立並指派原則，以在核發給服務主體的權杖中省略基本宣告。
在此範例中，您將會建立原則，以從核發給連結之服務主體的權杖中移除基本宣告集。


1. 建立宣告對應原則。 這個連結至特定服務主體的原則會從權杖中移除基本宣告。
    1. 若要建立原則，請執行此命令： 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. 若要查看您的新原則並取得原則的 ObjectId，請執行下列命令：
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  將原則指派給服務主體。 您也需要取得服務主體的 ObjectId。 
    1.  若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。 或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。
    2.  當您有服務主體的 ObjectId 時，執行下列命令︰  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-to-include-the-employeeid-and-tenantcountry-as-claims-in-tokens-issued-to-a-service-principal"></a>範例：建立並指派原則，以在核發給服務主體的權杖中納入 EmployeeID 和 TenantCountry 來作為宣告。
在此範例中，您將會建立原則，以在核發給連結之服務主體的權杖中新增 EmployeeID 和 TenantCountry。 在 SAML 權杖和 JWT 中，系統會以名稱宣告類型來發出 EmployeeID。 在 SAML 權杖和 JWT 中，系統會以國家/地區宣告類型來發出 TenantCountry。 在此範例中，我們會繼續在權杖中納入基本宣告集。

1. 建立宣告對應原則。 這個連結至特定服務主體的原則會在權杖中新增 EmployeeID 和 TenantCountry 宣告。
    1. 若要建立原則，請執行此命令：  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. 若要查看您的新原則並取得原則的 ObjectId，請執行下列命令：
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  將原則指派給服務主體。 您也需要取得服務主體的 ObjectId。 
    1.  若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。 或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。
    2.  當您有服務主體的 ObjectId 時，執行下列命令︰  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-to-a-service-principal"></a>範例：建立並指派原則，以在核發給服務主體的權杖中使用宣告轉換。
在此範例中，您將會建立原則，以對核發給連結之服務主體的 JWT 發出自訂宣告「JoinedData」。 這個宣告會包含藉由聯結資料 (儲存於使用者物件上的 extensionattribute1 屬性中) 與「.sandbox」所建立的值。 在此範例中，我們會在權杖中排除基本宣告集。


1. 建立宣告對應原則。 這個連結至特定服務主體的原則會在權杖中新增 EmployeeID 和 TenantCountry 宣告。
    1. 若要建立原則，請執行此命令： 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. 若要查看您的新原則並取得原則的 ObjectId，請執行下列命令： 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  將原則指派給服務主體。 您也需要取得服務主體的 ObjectId。 
    1.  若要查看您組織的所有服務主體，您可以查詢 Microsoft Graph。 或者，在 Azure AD Graph 總管，登入您的 Azure AD 帳戶。
    2.  當您有服務主體的 ObjectId 時，執行下列命令︰ 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
