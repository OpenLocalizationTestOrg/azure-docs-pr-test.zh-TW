---
title: "Azure AD Connect 所同步處理的屬性 | Microsoft Docs"
description: "列出 hello 屬性同步處理 tooAzure Active Directory。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Azure AD Connect 同步： 同步處理 tooAzure Active Directory 的屬性
本主題列出 Azure AD Connect 同步處理，即可同步處理的 hello 屬性。  
hello 屬性會依分組相關的 hello Azure AD 應用程式。

## <a name="attributes-toosynchronize"></a>屬性 toosynchronize
常見的問題是*什麼是 hello 清單的最小屬性 toosynchronize*。 hello 預設和建議的方法是 tookeep hello 預設屬性讓完整 GAL （全域通訊清單） 可用於建構中 hello 雲端和 tooget Office 365 的工作負載中的所有功能。 在某些情況下，有一些屬性，您的組織不想同步的 toohello 雲端因為這些屬性包含機密或 PII （個人識別資訊） 資料，如這個範例所示：  
![不正確的屬性](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

在此情況下，開始 hello 本主題中的屬性清單，識別可能包含機密或 PII 資料，而且無法同步處理的屬性。 接著，在安裝期間使用 [Azure AD 應用程式和屬性篩選](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering)將這些屬性取消選取。

> [!WARNING]
> 當取消選取屬性，應該小心，只能取消選取這些屬性絕對不可能 toosynchronize。 取消選取其他屬性可能對功能造成負面的影響。
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| 屬性名稱 | 使用者 | 註解 |
| --- |:---:| --- |
| accountEnabled |X |定義是否啟用帳戶。 |
| cn |X | |
| displayName |X | |
| objectSID |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| pwdLastSet |X |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| sourceAnchor |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| usageLocation |X |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |

## <a name="exchange-online"></a>Exchange Online
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| assistant |X |X | | |
| altRecipient |X | | |需要 Azure AD Connect 1.1.552.0 組建版本或更新版本。 |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| 說明 |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |群組目前未使用這個屬性。 |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |可用於 Azure AD Connect 1.1.524.0 版中 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Exchange Online 目前未使用這個屬性。 |
| msExchExtensionCustomAttribute2 |X |X |X |Exchange Online 目前未使用這個屬性。 |
| msExchExtensionCustomAttribute3 |X |X |X |Exchange Online 目前未使用這個屬性。 |
| msExchExtensionCustomAttribute4 |X |X |X |Exchange Online 目前未使用這個屬性。 |
| msExchExtensionCustomAttribute5 |X |X |X |Exchange Online 目前未使用這個屬性。 |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |衍生自 groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| 說明 |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |衍生自 groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| 說明 |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| securityEnabled | | |X |衍生自 groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| cn |X | |X |一般名稱或別名。 最常 hello 的前置詞 [mail] 值。 |
| displayName |X |X |X |字串，代表 hello 名稱通常顯示為 hello 易記名稱 （名字姓氏）。 |
| mail |X |X |X |電子郵件地址。 |
| member | | |X | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| proxyAddresses |X |X |X |機械屬性。 由 Azure AD 所使用。 包含 hello 使用者的所有次要電子郵件地址。 |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 |
| securityEnabled | | |X |衍生自 groupType。 |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |這個 UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |

## <a name="intune"></a>Intune
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| c |X |X | | |
| cn |X | |X | |
| 說明 |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| securityEnabled | | |X |衍生自 groupType |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |

## <a name="dynamics-crm"></a>Dynamics CRM
| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| 說明 |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| securityEnabled | | |X |衍生自 groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| title |X |X | | |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |

## <a name="3rd-party-applications"></a>協力廠商應用程式
此群組是一組屬性做為 hello 的一般工作負載或應用程式所需的基本屬性。 它可以用於另一節中未列出的工作負載或用於非 Microsoft 應用程式。 它會明確地使用 hello 下列：

* Yammer (使用的只有 User)
* [SharePoint 等資源所提供的混合式企業對企業 (B2B) 跨組織共同作業案例](http://go.microsoft.com/fwlink/?LinkId=747036)

此群組是一組屬性可用如果 hello Azure AD 目錄不是使用 toosupport Office 365、 Dynamics 或 Intune。 它包含一小組的核心屬性。

| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |定義是否啟用帳戶。 |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |機械屬性。 AD 使用者識別碼使用 toomaintain Azure 之間的同步處理 AD 和 AD。 |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |機械屬性。 使用的 tooknow 時 tooinvalidate 已發行的權杖。 供密碼同步處理和同盟使用。 |
| sn |X |X | | |
| sourceAnchor |X |X |X |機械屬性。 不可變的識別項 toomaintain ADDS 與 Azure AD 之間的關係。 |
| usageLocation |X | | |機械屬性。 hello 使用者的國家/地區。 用於授權指派。 |
| userPrincipalName |X | | |UPN 是使用者 hello hello 登入識別碼。 最常 hello 與 [mail] 值相同。 |

## <a name="windows-10"></a>Windows 10
Windows 10 已加入網域的 computer(device) 同步處理某些屬性 tooAzure AD。 如需有關 hello 案例的詳細資訊，請參閱[連接已加入網域裝置 tooAzure AD 以進行 Windows 10 體驗](../active-directory-azureadjoin-devices-group-policy.md)。 這些屬性一律會進行同步處理，而且 Windows 10 不會顯示為您可以取消選取的應用程式。 Windows 10 已加入網域的電腦由擁有 hello 屬性 userCertificate 填入識別。

| 屬性名稱 | 裝置 | 註解 |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |已加入網域的電腦的硬式編碼值。 |
| displayName |X | |
| ms-DS-CreatorSID |X |也稱為 registeredOwnerReference。 |
| objectGUID |X |也稱為 deviceID。 |
| objectSID |X |也稱為 onPremisesSecurityIdentifier。 |
| operatingSystem |X |也稱為 deviceOSType。 |
| operatingSystemVersion |X |也稱為 deviceOSVersion。 |
| userCertificate |X | |

這些屬性，**使用者**此外會 toohello 您已選取其他應用程式。  

| 屬性名稱 | 使用者 | 註解 |
| --- |:---:| --- |
| domainFQDN |X |也稱為 dnsDomainName。 例如 contoso.com。 |
| domainNetBios |X |也稱為 netBiosName。 例如 CONTOSO。 |

## <a name="exchange-hybrid-writeback"></a>Exchange 混合回寫
這些屬性寫回從 Azure AD tooon-內部部署 Active Directory 時選取 tooenable **Exchange 混合式**。 根據您的 Exchange 版本有可能會同步處理較少的屬性。

| 屬性名稱 | 使用者 | 連絡人 | 群組 | 註解 |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |衍生自 Azure AD 中的 cloudAnchor。 這個屬性是 Exchange 2016 和 Windows Server 2016 AD 中的新屬性。 |
| msExchArchiveStatus |X | | |線上封存： 可讓客戶 tooarchive 郵件。 |
| msExchBlockedSendersHash |X | | |篩選：從用戶端回寫內部部署篩選及線上安全和已封鎖的寄件者資料。 |
| msExchSafeRecipientsHash |X | | |篩選：從用戶端回寫內部部署篩選及線上安全和已封鎖的寄件者資料。 |
| msExchSafeSendersHash |X | | |篩選：從用戶端回寫內部部署篩選及線上安全和已封鎖的寄件者資料。 |
| msExchUCVoiceMailSettings |X | | |啟用整合通訊 (UM)-線上語音郵件： 使用 Microsoft Lync Server 整合 tooindicate tooLync 伺服器內部部署的 hello 使用者具有語音郵件 online services 中。 |
| msExchUserHoldPolicies |X | | |訴訟按住時： 可讓雲端服務 toodetermine 哪些使用者在訴訟保存。 |
| proxyAddresses |X |X |X |只有 hello x500 從 Exchange Online 的位址會插入。 |
| publicDelegates |X | | |可讓 Exchange Online 的信箱 toobe 授與 SendOnBehalfTo 權限 toousers 與內部部署 Exchange 信箱。 需要 Azure AD Connect 1.1.552.0 組建版本或更新版本。 |

## <a name="exchange-mail-public-folder"></a>Exchange 郵件公用資料夾
這些屬性會同步處理從內部部署 Active Directory tooAzure AD 當您選取 tooenable **Exchange 郵件公用資料夾**。

| 屬性名稱 | 公用資料夾 | 註解 |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>裝置回寫
裝置物件是在 Active Directory 中建立。 這些物件可以是裝置已加入 tooAzure AD 或加入網域的 Windows 10 電腦。

| 屬性名稱 | 裝置 | 註解 |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |只在 Windows Server 2016 AD 結構描述才有 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>注意事項
* 當使用替代識別碼 hello 內部 hello Azure AD 屬性 onPremisesUserPrincipalName 屬性 userPrincipalName 會同步處理。 hello Alternate ID 屬性，例如郵件、 hello Azure AD 屬性 userPrincipalName 與同步處理。
* 在上述清單 hello，hello 物件型別**使用者**也適用於 toohello 物件型別**iNetOrgPerson**。

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
