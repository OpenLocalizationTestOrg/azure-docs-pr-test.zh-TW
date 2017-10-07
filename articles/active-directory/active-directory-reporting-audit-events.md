---
title: "aaaAzure Active Directory 稽核報告事件 |Microsoft 文件"
description: "可供檢視以及從 Azure Active Directory 下載的稽核事件"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Azure Active Directory 稽核報告事件
*這份文件屬於 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。*

hello Azure Active Directory 稽核報告可協助客戶識別其 Azure Active Directory 中發生的特殊權限的動作。 特殊權限的動作包括提高權限變更 （例如，建立角色或密碼重設），變更原則設定 （例如密碼原則） 或變更 toodirectory 設定 （例如，變更 toodomain 同盟設定）。 hello 報表提供 hello 事件名稱，執行 hello 動作，hello 受到 hello 變更及 hello 日期和時間 （以 utc 格式） 的目標資源的 hello 執行者 hello 稽核記錄。 客戶有 hello 透過其 Azure Active Directory 的稽核事件可以 tooretrieve hello 清單[Azure 入口網站](https://portal.azure.com/)中所述，[檢視稽核記錄](active-directory-reporting-azure-portal.md)。

## <a name="list-of-audit-report-events"></a>稽核報告事件清單
<!--- audit event descriptions should be in hello past tense --->

| 事件 | 事件說明 |
| --- | --- |
| **使用者事件** | |
| 新增使用者 |加入使用者 toohello 目錄。 |
| 刪除使用者 |從 hello 目錄刪除使用者。 |
| 設定授權屬性 |Hello 目錄中的使用者設定 hello 授權內容。 |
| 重設使用者密碼 |重設 hello hello 目錄中的使用者密碼。 |
| 變更使用者密碼 |變更 hello hello 目錄中的使用者密碼。 |
| 變更使用者授權 |變更 hello tooa hello 目錄中的使用者指派的授權。 哪些授權已更新，查看在 hello toosee[更新使用者](#update-user-attributes)下方的屬性 |
| 更新使用者 |更新 hello 目錄中的使用者。 [請參閱下方](#update-user-attributes) 。 |
| 設定強制變更使用者密碼 |設定 hello 屬性，會強制使用者 toochange 他們的密碼登入。 |
| 更新使用者認證 |使用者已變更的 hello 密碼 |
| **群組事件** | |
| 新增群組 |Hello 目錄中建立群組。 |
| 更新群組 |更新 hello 目錄中的群組。 toosee 哪些群組屬性已更新，請參閱太[群組屬性稽核](#update-group-attributes)hello 下方區段中 |
| 刪除群組 |從 hello 目錄中刪除群組。 |
| CreateGroupSettings |建立群組設定 |
| UpdateGroupSettings |更新群組設定。 toosee 哪些群組設定已更新，請參閱太[群組屬性稽核](#update-group-attributes)hello 下方區段中 |
| DeleteGroupSettings |刪除群組設定 |
| SetGroupLicense |設定群組授權。 |
| SetGroupManagedBy |設定由使用者管理的群組 toobe |
| AddGroupMember |已新增的成員 toogroup |
| RemoveGroupMember |從群組移除成員 |
| AddGroupOwner |加入的擁有者 toogroup |
| RemoveGroupOwner |移除群組中的擁有者 |
| **應用程式事件** | |
| 新增服務主體 |加入服務主體 toohello 目錄。 |
| 移除服務主體 |移除 hello 目錄服務主體。 |
| 新增服務主體認證 |已新增的認證 tooa 服務主體。 |
| 移除服務主體認證 |移除服務主體的認證。 |
| 新增委派項目 |建立[OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 目錄中。 |
| 設定委派項目 |更新[OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 目錄中。 |
| 移除委派項目 |刪除[OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello 目錄中。 |
| **角色事件** | |
| 加入角色成員 tooRole |加入使用者 tooa 目錄角色。 |
| 移除角色的角色成員 |從目錄角色移除使用者。 |
| AddRoleDefinition |新增角色定義。 |
| UpdateRoleDefinition |更新角色定義。 toosee 哪些角色設定已更新，請參閱太[角色定義屬性稽核](#update-role-definition-attributes)hello 下方區段中 |
| DeleteRoleDefinition |刪除角色定義。 |
| AddRoleAssignmentToRoleDefinition |新增角色指派 toorole 定義。 |
| RemoveRoleAssignmentFromRoleDefinition |移除角色定義中的角色指派。 |
| AddRoleFromTemplate |從範本新增角色。 |
| UpdateRole |更新角色。 |
| AddRoleScopeMemberToRole |加入已設定領域的成員 toorole。 |
| RemoveRoleScopedMemberFromRole |移除角色中的範圍成員。 |
| **裝置事件 (所有新事件)** | |
| AddDevice |新增裝置。 |
| UpdateDevice |更新裝置。 toosee 何種裝置內容已更新，請參閱太[裝置屬性 Audited](#update-device-attributes) hello 下方區段中 |
| DeleteDevice |刪除裝置。 |
| AddDeviceConfiguration |新增裝置組態。 |
| UpdateDeviceConfiguration |更新裝置組態。 toosee 哪些裝置組態的內容已更新，請參閱太[裝置組態屬性 Audited](#update-device-configuration-attributes) hello 下方區段中 |
| DeleteDeviceConfiguration |刪除裝置組態。 |
| AddRegisteredOwner |加入 toodevice 登錄的擁有者。 |
| AddRegisteredUsers |加入註冊的使用者 toodevice。 |
| RemoveRegisteredOwner |移除裝置中已註冊的擁有者。 |
| RemoveRegisteredUsers |移除裝置中已註冊的使用者。 |
| RemoveDeviceCredentials |移除裝置認證。 |
| **B2B 事件** | |
| 已上傳的 Batch 邀請。 |系統管理員已上傳包含邀請 toobe 傳送 toopartner 使用者的檔案。 |
| 已處理的 Batch 邀請。 |已處理包含邀請 toopartner 使用者的檔案。 |
| 邀請外部使用者。 |外部使用者已受邀的 toohello 目錄。 |
| 兌換外部使用者的邀請。 |外部使用者已兌換邀請 toohello 目錄。 |
| 新增外部使用者 toogroup。 |外部使用者已被指派 hello 目錄中的成員資格 tooa 群組。 |
| 指定外部使用者 tooapplication。 |外部使用者已被指派的直接存取 tooan 應用程式。 |
| 建立熱門租用戶 |Hello 邀請兌換已在 Azure AD 中建立新的租用戶類型。 |
| 建立熱門使用者。 |使用者已建立現有的租用戶中 Azure AD 中的 hello 邀請贖回。 |
| **管理單位 (所有新事件)** | |
| AddAdministrativeUnit |新增管理單位。 |
| UpdateAdministrativeUnit |更新管理單位。 toosee 哪些管理單位的屬性已更新，請參閱太[稽核系統管理單元內容](#update-administrative-unit-attributes)hello 下方區段中 |
| DeleteAdministrativeUnit |刪除管理單位。 |
| AddMemberToAdministrativeUnit |新增成員 tooadministrative 單位。 |
| RemoveMemberFromAdministrativeUnit |移除管理單位中的成員。 |
| **目錄事件** | |
| 新增夥伴 toocompany |新增夥伴 toohello 目錄。 |
| 移除公司的夥伴 |移除合作夥伴 hello 目錄。 |
| DemotePartner |將夥伴降級。 |
| 新增網域 toocompany |加入網域 toohello 目錄。 |
| 移除公司的網域 |移除網域 hello 目錄。 |
| 更新網站 |更新 hello 目錄上的網域。 toosee 哪些網域屬性已更新，請參閱太[稽核的定義域屬性](#update-domain-attributes)hello 下方區段中 |
| 設定網域驗證 |變更 hello hello 公司的預設網域設定。 |
| 設定公司連絡人資訊 |設定公司層級的連絡人喜好設定。 這包括用於行銷的電子郵件地址，以及 Microsoft Online Services 的相關技術通知。 |
| 設定網域的同盟設定 |更新網域的 hello 同盟設定。 |
| 驗證網域 |驗證 hello 目錄上的網域。 |
| 驗證電子郵件驗證的網域 |驗證使用電子郵件驗證的 hello 目錄上的網域。 |
| 對公司設定 DirSyncEnabled 旗標 |設定 hello 屬性，可讓 Azure AD 同步的目錄。 |
| 設定密碼原則 |設定使用者密碼的長度和字元限制。 |
| 設定公司資訊 |更新的 hello 公司層級資訊。 請參閱 hello [Get-msolcompanyinformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) PowerShell cmdlet，如需詳細資訊。 |
| SetCompanyAllowedDataLocation |設定公司允許的資料位置。 |
| SetCompanyDirSyncEnabled |設定 DirSyncEnabled 旗標。 |
| SetCompanyDirSyncFeature |設定 DirSync 功能。 |
| SetCompanyInformation |設定公司資訊。 |
| SetCompanyMultiNationalEnabled |設定啟用公司多語系功能。 |
| SetDirectoryFeatureOnTenant |在租用戶上設定目錄功能。 |
| SetTenantLicenseProperties |設定租用戶授權屬性。 |
| CreateCompanySettings |建立公司設定 |
| UpdateCompanySettings |更新公司設定。 toosee 哪些公司屬性已更新，請參閱太[稽核的公司內容](#update-company-attributes)hello 下方區段中 |
| DeleteCompanySettings |刪除公司設定 |
| SetAccidentalDeletionThreshold |設定意外刪除臨界值。 |
| SetRightsManagementProperties |設定 Rights Management 屬性。 |
| PurgeRightsManagementProperties |清除 Rights Management 屬性。 |
| UpdateExternalSecrets |更新外部密碼 |
| **原則事件 (所有新事件)** | |
| AddPolicy |新增原則。 |
| UpdatePolicy |更新原則。 |
| DeletePolicy |刪除原則。 |
| AddDefaultPolicyApplication |新增原則 tooapplication。 |
| AddDefaultPolicyServicePrincipal |新增原則 tooservice 主體。 |
| RemoveDefaultPolicyApplication |移除應用程式中的原則。 |
| RemoveDefaultPolicyServicePrincipal |移除服務主體中的原則。 |
| RemovePolicyCredentials |移除原則認證。 |

## <a name="audit-report-retention"></a>稽核報告保留

Hello 有關保留的最新資訊，請參閱[Azure Active Directory 報告保留原則](active-directory-reporting-retention.md)。


對於較長的保留時間儲存其稽核事件有興趣的客戶，hello Reporting API 可以使用的 tooregularly 提取稽核事件到另一個資料存放區。 請參閱[入門 hello Reporting API](active-directory-reporting-api-getting-started.md)如需詳細資訊。

## <a name="properties-included-with-each-audit-event"></a>每個稽核事件包含的屬性
| 屬性 | 說明 |
| --- | --- |
| 日期和時間 |發生 hello 日期和時間的 hello 稽核事件 |
| Actor |hello 使用者或服務主體執行 hello 動作 |
| 動作 |hello 執行的動作 |
| 目標 |hello 使用者或服務主體上執行 hello 動作 |

## <a name="update-user-attributes"></a>「更新使用者」屬性
hello 「 更新使用者 」 稽核事件都包括哪些使用者已更新屬性的其他資訊。 針對每個屬性，兩者 hello 先前的值和就會包含 hello 新值。

| 屬性 | 說明 |
| --- | --- |
| AccountEnabled |hello 使用者可以登入。 |
| AssignedLicense |所有已指派給 toohello 使用者的授權。 |
| AssignedPlan |服務方案所產生的 hello 授權指派給 toohello 使用者。 |
| LicenseAssignmentDetail |Toohello 使用者指派授權的詳細資訊。 比方說，如果群組為基礎的授權已與此有關，其中包含授與 hello 授權的 hello 群組。 |
| 行動 |hello 使用者的行動電話。 |
| OtherMail |hello 使用者的備用電子郵件地址。 |
| OtherMobile |hello 使用者的備用行動電話。 |
| StrongAuthenticationMethod |Hello 使用者設定 Multi-factor authentication，例如語音通話、 簡訊或驗證程式碼，從行動裝置應用程式的驗證方法清單。 |
| StrongAuthenticationRequirement |是否對此使用者強制使用、啟用或停用多因素驗證。 |
| StrongAuthenticationUserDetails |hello 使用者的電話號碼、 替代電話號碼和電子郵件位址用於多因素驗證和密碼重設驗證。 |
| StrongAuthenticationPhoneAppDetail |詳細資料 forof phone 應用程式註冊 tooperform 2FA 登入 |
| TelephoneNumber |hello 使用者的電話號碼。 |
| AlternativeSecurityId |Hello 物件之替代安全性識別碼。 |
| CreationType |Hello 使用者 （無論是透過邀請或網路） 的建立方法。 |
| InviteTicket |邀請票證 hello 使用者的清單。 |
| InviteReplyUrl |Url tooreply 時接受邀請的清單。 |
| InviteResources |已邀請資源 toowhich hello 使用者清單。 |
| LastDirSyncTime |上次 hello 物件更新的時間因為 hello 授權 （客戶，在內部部署） 從同步處理目錄。 |
| MSExchRemoteRecipientType |將 tooMSO 收件者的類型對應。 請參閱太 [MSO 收件者類型] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx 收件者的類型 |
| PreferredDataLocation |hello 慣用的 hello 使用者、 群組、 連絡人、 公用資料夾的位置或裝置的資料。 |
| ProxyAddresses |Exchange Server 收件者物件外部郵件系統中可以辨識的 hello 位址。 |
| StsRefreshTokensValidFrom |傳達重新整理權杖撤銷資訊 - 任何在此時間之前發出的 STS 重新整理權杖都會被視為到期。 |
| UserPrincipalName |hello UPN 是使用者的網際網路型態登入名稱。 |
| UserState |使用只 PendingApproval/PendingAcceptance/Accepted/PendingVerification 的狀態。 |
| UserStateChangedOn |最後一個變更 tooUserState 的時間戳記。 使用 tootrigger 生命週期工作流程。 |
| UserType |使用者類型。 成員 (0)、來賓 (1)、病毒 (2)。 |

## <a name="update-group-attributes"></a>「更新群組」屬性
| 屬性 | 說明 |
| --- | --- |
| 分類 |hello 分類統一群組 （HBI、 MBI 等等）。 |
| 說明 |Hello 物件的相關人類看得懂的描述性詞彙。 |
| DisplayName |hello 物件的顯示名稱 |
| DirSyncEnabled |表示同步處理是否從權威性 (客戶、內部部署) 目錄發生。 |
| GroupLicenseAssignment |群組的授權指派 |
| GroupType |群組類型，統一 (0) |
| IsMembershipRuleLocked |表示該 hello MembershipRule 屬性 hello 自助式群組管理服務設定，而且無法由使用者變更。 適用的唯一 toogroups GroupType 其中包含 GroupType.DynamicMembership |
| IsPublic |如果 hello 群組是公開/私密金鑰的旗標 tooindicate。 |
| LastDirSyncTime |上次 hello 物件更新的時間從 hello 授權 （在內部部署客戶） 同步處理的結果目錄。 |
| Mail |主要電子郵件地址 |
| MailEnabled |表示此群組是否有電子郵件功能。 |
| MailNickname |通訊錄物件的 moniker，通常 hello 部分前面 hello 其電子郵件名稱"@"符號。 |
| MembershipRule |字串，表示 hello hello 自助式群組管理服務 toodetermine 哪個成員應該屬於 toothis 群組所使用的準則。 另請參閱 IsMembershipRuleLocked。 適用於只有 toogroups GroupType 其中包含 GroupType.DynamicMembership。 |
| MembershipRuleProcessingState |定義處理此群組的成員資格的 hello 狀態 hello 自助式群組管理服務所定義的列舉值。 適用於只有 toogroups GroupType 其中包含 GroupType.DynamicMembership。 |
| ProxyAddresses |Exchange Server 收件者物件外部郵件系統中可以辨識的 hello 位址。 |
| RenewedDateTime |最近更新群組時的時間戳記記錄。 |
| SecurityEnabled |指出是否 hello 群組的成員資格可能會影響授權決策。 |
| WellKnownObject |標示目錄物件，並將它指定為其中一個預先定義的集合。 |

## <a name="update-device-attributes"></a>「更新裝置」屬性
| 屬性 | 說明 |
| --- | --- |
| AccountEnabled |表示是否可以驗證安全性主體。 |
| CloudAccountEnabled |表示是否可以驗證安全性主體。 Hello 裝置在內部部署主控時，InTune 所撰寫。 |
| CloudDeviceOSType |Hello 根據 hello OS 例如 Windows RT、 iOS 的裝置類型。 設定雲端服務 （例如 Intune) 時，這個屬性會成為 hello 目錄中授權 DeviceOSType。 |
| CloudDeviceOSVersion |Hello OS 版本。 設定雲端服務 （例如 Intune) 時，這個屬性會成為 hello 目錄中授權 DeviceOSVersion。 |
| CloudDisplayName |Hello displayName LDAP 屬性的值。 設定雲端服務 （例如 Intune) 時，這個屬性會成為授權 displayName hello 目錄中。 |
| CloudCreated |指出是否由雲端服務建立 hello 物件。 |
| CompliantUntil |等到何時裝置被視為相容。 |
| DeviceMetadata |Hello 裝置的自訂中繼資料 |
| DeviceObjectVersion |這個屬性是 hello 裝置使用的 tooidentify hello 結構描述版本。 |
| DeviceOSType |Hello 根據 hello OS 例如 Windows RT、 iOS 的裝置類型。 寫入 hello 註冊服務和預定的 toobe 更新 hello MDM 管理的服務或 STS 淺管理服務。 |
| DeviceOSVersion |Hello OS 版本。 寫入 hello 註冊服務和預定的 toobe 更新 hello MDM 管理的服務或 STS 淺管理服務。 |
| DevicePhysicalIds |多重值的屬性用 toostore hello 實體裝置的識別項。 這可能包括 BIOS 識別碼、TPM 指紋、硬體特定識別碼等。 |
| DirSyncEnabled |表示同步處理是否從權威性 (客戶、內部部署) 目錄發生。 |
| DisplayName |hello 物件的顯示名稱 |
| IsCompliant |這個屬性是使用的 toomanage hello 行動裝置管理狀態的 hello 裝置。 |
| IsManaged |這個屬性用 tooindicate hello 裝置受雲端 mdm。 |
| LastDirSyncTime |上次 hello 物件更新的時間因為 hello 授權 （在內部部署客戶），從同步處理目錄。 |

## <a name="update-device-configuration-attributes"></a>「更新裝置組態」屬性
| 屬性 | 說明 |
| --- | --- |
| MaximumRegistrationInactivityPeriod |hello 最大天數裝置可以是作用中才會視為移除。 |
| RegistrationQuota |使用 toolimit hello 數目為單一使用者允許的裝置註冊原則。 |

## <a name="update-service-principal-configuration-attributes"></a>「更新服務主體組態」屬性
| 屬性 | 說明 |
| --- | --- |
| AccountEnabled |表示是否可以驗證安全性主體。 |
| AppPrincipalId |安全性主體外部的身分識別 (由應用程式定義)。 |
| DisplayName |hello 物件的顯示名稱 |
| ServicePrincipalName |服務主體名稱，包含 「 名稱/授權 」 其中名稱會指定應用程式類別值，而授權單位至少包含主機名稱 [: 連接埠] 或 「 名稱 」，指定 hello 服務主體的識別項。 |

## <a name="update-app-attributes"></a>「更新應用程式」屬性
| 屬性 | 說明 |
| --- | --- |
| AppAddress |hello 組 （重新導向 Url） 的位址指派 tooa 服務主體。 |
| AppId |Hello 應用程式的應用程式識別碼 |
| AppIdentifierUri |應用程式的 URI，它會識別 hello 應用程式。  它通常是 hello 應用程式存取的 URL。 |
| AppLogoUrl |hello 應用程式的標誌影像儲存在 CDN 中的 hello url。 |
| AvailableToOtherTenants |True hello 應用程式是多租用戶應用程式 （也就是可由其他租用戶）。 |
| DisplayName |hello 應用程式名稱的顯示名稱 |
| Entitlement |應用程式權利的清單。 |
| ExternalUserAccountDelegationsAllowed |表示資源應用程式是否為受信任資源的旗標，可以為外部使用者帳戶建立委派項目。 |
| GroupMembershipClaims |hello 群組成員資格的宣告原則。 |
| PublicClient |如果 hello 用戶端無法將保持秘密，則為 true （也就是 OAuth2.0 中的非機密用戶端） |
| RecordConsentConditions |同意的狀況，hello 所定義的型別合約條款： None (0)，SilentConsentForPartnerManagedApp(1)。 此值將會公開 hello Graph API 的結構描述中，而且只能設定/變更租用戶系統管理員。 |
| RequiredResourceAccess |Hello RequiredResourceAccess 屬性值的 XML 內容。 |
| WebApp |如果為 true，表示此應用程式是 Web 應用程式。 |
| WwwHomepage |hello 主要網頁。 |

## <a name="update-role-attributes"></a>「更新角色」屬性
| 屬性 | 說明 |
| --- | --- |
| AppAddress |hello 組 （重新導向 Url） 的位址指派 tooa 服務主體。 |
| BelongsToFirstLoginObjectSet |如果為 true，表示此物件所屬 toohello 組 hello 第一個新的租用戶管理員的物件需要的 tooenable 登入。 |
| Builtin |指出 hello 系統是否已擁有 hello 物件存留期。 |
| 說明 |Hello 物件的相關人類看得懂的描述性詞彙。 |
| DisplayName |hello 物件的顯示名稱 |
| MailNickname |通訊錄物件的 moniker，通常 hello 部分前面 hello 其電子郵件名稱"@"符號。 |
| RoleDisabled |指出是否應該忽略 hello 角色進行存取檢查。 |
| RoleTemplateId |Hello 角色範本的身分。 |
| ServiceInfo |服務的佈建可供 MOAC 及/或其他服務執行個體的資訊 (hello 相同或不同的服務類型)。 |
| TaskSetScopeReference |識別 TaskSet 和一組與 Role 或 RoleTemplate 相關聯的範圍。 |
| ValidationError |描述有關 hello 內容或連結物件的系統管理員動作 tooresolve 從非暫時性的服務特定錯誤的同盟服務所發行的資訊。 |
| WellKnownObject |標示目錄物件，並將它指定為其中一個預先定義的集合。 |

## <a name="update-role-definition-attributes"></a>「更新角色定義」屬性
| 屬性 | 說明 |
| --- | --- |
| AssignableScopes |授權範圍的指派這個 RoleDefinition tooa 安全性主體時，可參考的集合。 |
| DisplayName |hello 物件的顯示名稱 |
| GrantedPermissions |此 RoleDefinition 所授與的權限。 |

## <a name="update-administrative-unit-attributes"></a>「更新管理單位」屬性
| 屬性 | 說明 |
| --- | --- |
| 說明 |當您變更的管理單位的 hello 描述時，會更新此屬性。 |
| DisplayName |當您變更的管理單位的 hello 名稱時，會更新此屬性。 |

## <a name="update-company-attributes"></a>「更新公司」屬性
| 屬性 | 說明 |
| --- | --- |
| AllowedDataLocation |中的 hello 公司的使用者允許 toobe 佈建的位置。 |
| AuthorizedServiceInstance |服務執行個體 toowhich 可能部署計劃的名稱。 |
| DirSyncEnabled |表示同步處理是否從權威性 (客戶、內部部署) 目錄發生。 |
| DirSyncStatus |表示從授權 （客戶，在內部部署） 是否發生在此租用戶內容中的地址通訊錄物件的同步處理目錄。hello DirSyncEnabled 公司物件上的屬性延伸。 |
| DirSyncFeatures |位元旗標 tookeep 追蹤的一組啟用和停用目錄同步 hello 租用戶的功能。 |
| DirectoryFeatures |已啟用/停用的目錄功能。 |
| DirSyncConfiguration |包含所有 DirSync 組態特定 toohello 目前的租用戶。 |
| DisplayName |hello 物件的顯示名稱 |
| IsMnc |布林值旗標組太"，則為 true 」 如果 hello 公司已啟用 hello 跨國公司功能。 |
| ObjectSettings |設定適用於 toohello 範圍 hello 物件的集合。 |
| PartnerCommerceUrl |URL toohello 夥伴的商務網站。 |
| PartnerHelpUrl |URL toohello 合作夥伴的說明的網站。 |
| PartnerSupportEmail |URL toohello 合作夥伴的支援電子郵件。 |
| PartnerSupportTelephone |URL toohello 合作夥伴的支援電話。 |
| PartnerSupportUrl |URL toohello 合作夥伴的支援網站。 |
| StrongAuthenticationDetails |TooStrongAuthentication 相關詳細資料。 |
| StrongAuthenticationPolicy |增強式驗證 hello 公司原則。 |
| TechnicalNotificationMail |電子郵件地址 toonotify 技術問題相關 tooa 公司。 |
| TelephoneNumber |符合 hello ITU 建議 E.123 的電話號碼。 |
| TenantType |租用戶 hello 型別。 如果未指定此值，hello 租用戶是公司。 否則，可能的值為︰MicrosoftSupport (0)、SyndicatePartner (1)、BreadthPartner(2)、BreadthPartnerDelegatedAdmin (3)、ResellerPartnerDelegatedAdmin (4)、ValueAddedResellerPartnerDelegatedAdmin (5)。 |
| VerifiedDomain |DNS 網域名稱的一組繫結 tooa 公司。 |

## <a name="update-domain-attributes"></a>「更新網域」屬性
| 屬性 | 說明 |
| --- | --- |
| 功能 |如果有的話，位元旗標描述 hello 網域 hello 功能。 |
| 預設值 |指出 hello 網域是否 hello 預設值。例如，hello 預設 UserPrincipalName 字尾，系統管理員 MOAC 中建立新的使用者。 |
| Initial |指出是否 hello 是 hello 初始網域 hello 公司 OCP 所配置。 hello 初始網域是唯一的子網域的 Microsoft Online 網域;e.g.contoso3.microsoftonline.com。 |
| LiveType |Hello 對應 Windows Live 命名空間類型，如果有的話。 |
| 名稱 |Hello 端點的識別項。 |
| PasswordNotificationWindowDays |hello 天數之前的密碼已過期 hello 使用者會收到通知。 |
| PasswordValidityPeriodDays |hello 必須變更之前，可適用於密碼的天數。 |

稽核記錄是許多標準規定的必要控制項。 如需使用 hello Azure Active Directory 稽核報告 toomeet 其規定的客戶，建議 hello 客戶提交本說明主題與 hello 副本 hello 客戶的一份匯出 toohelp 說明 hello 報表的稽核報告詳細資料。 如果 hello 稽核人員想要 Azure 目前符合的 toounderstand hello 標準規定，直接 hello 稽核員 toohello[相容性頁面](https://azure.microsoft.com/support/trust-center/compliance/)hello Microsoft Azure 信任中心。

