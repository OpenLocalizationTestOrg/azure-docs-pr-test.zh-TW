# 概觀
## [什麼是 Azure Active Directory？](active-directory-whatis.md)
## [關於 Azure 身分識別管理](identity-fundamentals.md)
## [了解 Azure 身分識別解決方案](understand-azure-identity-solutions.md)
## [選擇混合式身分識別解決方案](choose-hybrid-identity-solution.md)
## [關聯 Azure 訂用帳戶](active-directory-how-subscriptions-associated-directory.md)
## [常見問題集](active-directory-faq.md)

# 開始使用
## [註冊 Azure AD Premium](active-directory-get-started-premium.md)
## [新增自訂網域名稱](add-custom-domain.md)
## [設定公司商標](customize-branding.md)
## [新增使用者 tooAzure AD](add-users-azure-active-directory.md)
## [指派授權 toousers](license-users-groups.md)
## [啟用自助式密碼重設](active-directory-passwords-getting-started.md)


# 作法
## 規劃和設計
### [了解 Azure AD 架構](active-directory-architecture.md)
### [部署混合式身分識別解決方案](active-directory-hybrid-identity-design-considerations-overview.md)
### [Azure Active Directory 中的宣告對應](active-directory-claims-mapping.md)
#### 判斷需求
##### [身分識別](active-directory-hybrid-identity-design-considerations-business-needs.md)
##### [目錄同步](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
##### [多因素驗證](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)
##### [身分識別生命週期策略](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)
#### [資料安全性的規劃](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)
##### [資料保護](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
##### [內容管理](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
##### [存取控制](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
##### [事件回應](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)
#### 規劃身分識別生命週期
##### [工作](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)
##### [採用策略](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)
#### [後續步驟](active-directory-hybrid-identity-design-considerations-nextsteps.md)
#### [工具比較](active-directory-hybrid-identity-design-considerations-tools-comparison.md)

## 管理使用者
### [使用群組指派授權](active-directory-licensing-whatis-azure-portal.md)
#### [指派授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
#### [識別並解決群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [移轉個別的授權的使用者 toogroup 授權](active-directory-licensing-group-migration-azure-portal.md)
#### [群組型授權的其他案例](active-directory-licensing-group-advanced.md)
#### [群組型授權的 PowerShell 範例](active-directory-licensing-ps-examples.md)
### [從其他目錄中新增使用者 (傳統入口網站)](active-directory-create-users-external.md)
### [管理使用者設定檔](active-directory-users-profile-azure-portal.md)
### [重設密碼](active-directory-users-reset-password-azure-portal.md)
### [管理使用者工作資訊](active-directory-users-work-info-azure-portal.md)
### [共用帳戶](active-directory-sharing-accounts.md)



## [管理群組和成員](active-directory-manage-groups.md)
### 管理群組
#### [Azure 入口網站](active-directory-groups-create-azure-portal.md)
#### [傳統入口網站](active-directory-accessmanagement-manage-groups.md)
#### [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
### [管理群組成員](active-directory-groups-members-azure-portal.md)
### [管理群組擁有者](active-directory-accessmanagement-managing-group-owners.md)
### [管理群組成員資格](active-directory-groups-membership-azure-portal.md)
### [使用群組指派授權](active-directory-licensing-whatis-azure-portal.md)
#### [指派授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
#### [識別並解決群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [移轉個別的授權的使用者 toogroup 授權](active-directory-licensing-group-migration-azure-portal.md)
#### [群組型授權的其他案例](active-directory-licensing-group-advanced.md)
#### [群組型授權的 PowerShell 範例](active-directory-licensing-ps-examples.md)
### [設定 Office 365 群組到期時間](active-directory-groups-lifecycle-azure-portal.md)
### [檢視全部群組](active-directory-groups-view-azure-portal.md)
### [啟用專用群組](active-directory-accessmanagement-dedicated-groups.md)
### [新增群組存取 tooSaaS 應用程式](active-directory-accessmanagement-group-saasapps.md)
### [還原已刪除的 Office 365 群組](active-directory-groups-restore-azure-portal.md)
### 管理群組設定
#### [Azure 入口網站](active-directory-groups-settings-azure-portal.md)
#### [Cmdlet](active-directory-accessmanagement-groups-settings-cmdlets.md)
### 建立進階規則
#### [Azure 入口網站](active-directory-groups-dynamic-membership-azure-portal.md)
#### [傳統入口網站](active-directory-accessmanagement-groups-with-advanced-rules.md)
### [設定自助式群組](active-directory-accessmanagement-self-service-group-management.md)
### [疑難排解](active-directory-accessmanagement-troubleshooting.md)

## [管理報告](active-directory-reporting-azure-portal.md)
### [登入活動](active-directory-reporting-activity-sign-ins.md)
### [稽核活動](active-directory-reporting-activity-audit-logs.md)
### [有風險的使用者](active-directory-reporting-security-user-at-risk.md)
### [有風險的登入](active-directory-reporting-security-risky-sign-ins.md)
### [風險事件](active-directory-reporting-risk-events.md)
### [常見問題集](active-directory-reporting-faq.md)
### 工作
#### [設定具名位置](active-directory-named-locations.md)
#### [尋找活動報告](active-directory-reporting-migration.md)
#### [使用 hello Azure Active Directory Power BI 內容套件](active-directory-reporting-power-bi-content-pack-how-to.md)
### 參考
#### [保留](active-directory-reporting-retention.md)
#### [延遲](active-directory-reporting-latencies-azure-portal.md)
#### [Notifications](active-directory-reporting-notifications.md)
#### [登入活動的錯誤代碼](active-directory-reporting-activity-sign-ins-errors.md)
### 疑難排解
#### [缺少稽核資料](active-directory-reporting-troubleshoot-missing-audit-data.md)
#### [下載中缺少的資料](active-directory-reporting-troubleshoot-missing-data-download.md)
#### [Azure Active Directory 活動記錄內容套件錯誤](active-directory-reporting-troubleshoot-content-pack.md)
### [程式設計存取](active-directory-reporting-api-getting-started-azure-portal.md)
#### [稽核參考](active-directory-reporting-api-audit-reference.md)
#### [登入參考](active-directory-reporting-api-sign-in-activity-reference.md)
#### [必要條件](active-directory-reporting-api-prerequisites-azure-portal.md)
#### [稽核範例](active-directory-reporting-api-audit-samples.md)
#### [登入範例](active-directory-reporting-api-sign-in-activity-samples.md)
#### [使用憑證](active-directory-reporting-api-with-certificates.md)

## [管理密碼](active-directory-passwords-overview.md)
### 使用者文件
#### [重設或變更您的密碼](active-directory-passwords-update-your-own-password.md)
#### [密碼最佳做法](active-directory-secure-passwords.md)
#### [註冊自助式密碼重設](active-directory-passwords-reset-register.md)
### [授權 SSPR](active-directory-passwords-licensing.md)
### [部署 SSPR](active-directory-passwords-best-practices.md)
### IT 系統管理員︰重設密碼
#### [Azure 入口網站](active-directory-users-reset-password-azure-portal.md)
#### [Azure 傳統入口網站](active-directory-create-users-reset-password.md)
### [了解 SSPR 原則](active-directory-passwords-policy.md)
### [了解密碼重設](active-directory-passwords-how-it-works.md)
### [自訂 SSPR](active-directory-passwords-customize.md)
### [SSPR 所使用的資料](active-directory-passwords-data.md)
### [提出 SSPR 報告](active-directory-passwords-reporting.md)
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### [密碼回寫](active-directory-passwords-writeback.md)
### [密碼雜湊同步處理](./connect/active-directory-aadconnectsync-implement-password-synchronization.md#how-password-synchronization-works)
### [疑難排解](active-directory-passwords-troubleshoot.md)
### [常見問題集](active-directory-passwords-faq.md)


## 管理裝置
### [簡介](device-management-introduction.md)
### [使用 hello Azure 入口網站](device-management-azure-portal.md)
### [常見問題集](device-management-faq.md)
### 工作
#### [設定混合式 Azure AD 已加入裝置](device-management-hybrid-azuread-joined-devices-setup.md) 
#### [部署內部部署](active-directory-device-registration-on-premises-setup.md)
### 疑難排解
#### [混合式 Azure AD 已加入 Windows 10 和 Windows Server 2016 裝置](device-management-troubleshoot-hybrid-join-windows-current.md)
#### [混合式 Azure AD 已加入舊版 Windows 裝置](device-management-troubleshoot-hybrid-join-windows-legacy.md)
### [Azure AD Join](active-directory-azureadjoin-overview.md)
#### [規劃](active-directory-azureadjoin-deployment-aadjoindirect.md)
#### [設定裝置註冊](active-directory-azureadjoin-setup.md)
#### [註冊新裝置](active-directory-azureadjoin-user-frx.md)
#### [部署](active-directory-azureadjoin-devices-group-policy.md)
#### [了解 Windows 10 整合](active-directory-azureadjoin-windows10-devices-overview.md)
#### [使用 Windows 10 裝置](active-directory-azureadjoin-windows10-devices.md)
#### [加入裝置](active-directory-azureadjoin-personal-device.md)
#### [加入 Windows 10 裝置](active-directory-azureadjoin-user-upgrade.md)

## 管理應用程式
### [概觀](active-directory-enable-sso-scenario.md)
### [開始使用](active-directory-integrating-applications-getting-started.md)
### [SaaS 應用程式整合教學課程](active-directory-saas-tutorial-list.md)
### [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
#### [更新登錄設定](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
#### [了解安全性和隱私權](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)


### [透過 App Proxy 遠端存取應用程式](active-directory-application-proxy-get-started.md)
#### 開始使用
##### [啟用應用程式 Proxy](active-directory-application-proxy-enable.md)
##### [發佈應用程式](application-proxy-publish-azure-portal.md)
##### [自訂網域](active-directory-application-proxy-custom-domains.md)
#### [單一登入](application-proxy-sso-overview.md)
##### [搭配 KCD 的 SSO](active-directory-application-proxy-sso-using-kcd.md)
##### [搭配標頭的 SSO](application-proxy-ping-access.md)
##### [搭配密碼保存庫的 SSO](application-proxy-sso-azure-portal.md)
#### 概念
##### [連接器](application-proxy-understand-connectors.md)
##### [安全性](application-proxy-security-considerations.md)
##### [網路](application-proxy-network-topology-considerations.md)


##### [從 TMG 或 UAG 升級](application-proxy-transition-from-uag-tmg.md)

#### 進階組態
##### [在不同網路上發佈](active-directory-application-proxy-connectors-azure-portal.md)
##### [Proxy 伺服器](application-proxy-working-with-proxy-servers.md)
##### [宣告感知應用程式](active-directory-application-proxy-claims-aware-apps.md)
##### [原生用戶端應用程式](active-directory-application-proxy-native-client.md)
##### [無訊息安裝](active-directory-application-proxy-silent-installation.md)
##### [自訂首頁](application-proxy-office365-app-launcher.md)
##### [翻譯內嵌連結](application-proxy-link-translation.md)
#### 發佈逐步解說
##### [遠端桌面](application-proxy-publish-remote-desktop.md)
##### [SharePoint](application-proxy-enable-remote-access-sharepoint.md)
##### [Microsoft Teams](application-proxy-teams.md)
#### [疑難排解](active-directory-application-proxy-troubleshoot.md)
#### 使用 hello 傳統入口網站
##### [下載連接器](application-proxy-enable-classic-portal.md)
##### [發佈應用程式](active-directory-application-proxy-publish.md)
##### [使用連接器](active-directory-application-proxy-connectors.md)
##### [條件式存取](active-directory-application-proxy-conditional-access.md)

### 管理企業應用程式
#### [指派使用者](active-directory-coreapps-assign-user-azure-portal.md)
#### [自訂商標](active-directory-coreapps-change-app-logo-user-azure-portal.md)
#### [停用使用者登入](active-directory-coreapps-disable-app-azure-portal.md)
#### [移除使用者](active-directory-coreapps-remove-assignment-azure-portal.md)
#### [檢視我的所有應用程式](active-directory-coreapps-view-azure-portal.md)
#### [管理使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)

### [管理存取 tooapps](active-directory-managing-access-to-apps.md)
#### [自助服務存取](active-directory-self-service-application-access.md)
#### [SSO 存取](active-directory-appssoaccess-whatis.md)
#### [SSO 憑證](active-directory-sso-certs.md)
#### [租用戶限制](active-directory-tenant-restrictions.md)
#### [使用 SCIM 佈建使用者](active-directory-scim-provisioning.md)

### [疑難排解](active-directory-application-troubleshoot-content-map.md)
#### [應用程式開發](active-directory-application-dev-troubleshoot-content-map.md)
##### [設定和註冊](active-directory-application-dev-config-content-map.md)
##### [開發](active-directory-application-dev-development-content-map.md)
#### [應用程式管理](active-directory-application-management-troubleshoot-content-map.md)
##### [組態](active-directory-application-config-content-map.md)
##### [登入](active-directory-application-sign-in-content-map.md)
##### [佈建](active-directory-application-provisioning-content-map.md)
##### [管理存取](active-directory-application-access-content-map.md)
##### [存取面板](active-directory-application-access-panel-content-map.md)
##### [應用程式 Proxy](active-directory-application-proxy-content-map.md)
##### [條件式存取](active-directory-application-conditional-access-content-map.md)
### [開發應用程式](active-directory-applications-guiding-developers-for-lob-applications.md)
### [文件庫](active-directory-apps-index.md)

## 管理您的目錄
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### 自訂網域名稱
#### [概觀](active-directory-add-domain-concepts.md)
#### 管理網域名稱
##### [Azure 入口網站](active-directory-domains-manage-azure-portal.md)
##### [傳統入口網站](active-directory-add-manage-domain-names.md)
### [管理目錄](active-directory-administer.md)
### [多個目錄](active-directory-licensing-directory-independence.md)
### [O365 目錄](active-directory-manage-o365-subscription.md)
### [自助式註冊](active-directory-self-service-signup.md)
### [企業狀態漫遊](active-directory-windows-enterprise-state-roaming-overview.md)
#### [啟用](active-directory-windows-enterprise-state-roaming-enable.md)
#### [群組原則設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
#### [Windows 10 設定](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
#### [常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md)
#### [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

### [將合作夥伴與 Azure AD B2B 整合](active-directory-b2b-what-is-azure-ad-b2b.md)
#### [管理員新增 B2B 使用者](active-directory-b2b-admin-add-users.md)
#### [資訊背景工作新增 B2B 使用者](active-directory-b2b-iw-add-users.md)
#### [API 與自訂](active-directory-b2b-api.md)
#### [程式碼與 PowerShell 範例](active-directory-b2b-code-samples.md)
#### [自助入口網站註冊範例](active-directory-b2b-self-service-portal.md)
#### [邀請電子郵件](active-directory-b2b-invitation-email.md)
#### [兌換邀請](active-directory-b2b-redemption-experience.md)
#### [在沒有邀請的情況下新增 B2B 使用者](active-directory-b2b-add-user-without-invite.md)
#### [B2B 的條件式存取](active-directory-b2b-mfa-instructions.md)
#### [B2B 共用原則](active-directory-b2b-delegate-invitations.md)
#### [新增 B2B 使用者 tooa 角色](active-directory-b2b-add-guest-to-role.md)
#### [動態群組和 B2B 使用者](active-directory-b2b-dynamic-groups.md)
#### [稽核與報告](active-directory-b2b-auditing-and-reporting.md)
#### [B2B 和 Office 365 外部共用](active-directory-b2b-o365-external-user.md)
#### [授權](active-directory-b2b-licensing.md)
#### [目前限制](active-directory-b2b-current-limitations.md)
#### [常見問題集](active-directory-b2b-faq.md)
#### [疑難排解 B2B](active-directory-b2b-troubleshooting.md)
#### [了解 hello B2B 使用者](active-directory-b2b-user-properties.md)
#### [B2B 使用者權杖](active-directory-b2b-user-token.md)
#### [適用於 Azure AD 整合應用程式的 B2B](active-directory-b2b-configure-saas-apps.md)
#### [B2B 使用者宣告對應](active-directory-b2b-claims-mapping.md)
#### [比較 B2B 共同作業 tooB2C](active-directory-b2b-compare-b2c.md)
#### [取得 B2B 支援](active-directory-b2b-support.md)

### [使用 Azure AD Connect 整合內部部署身分識別](./connect/active-directory-aadconnect.md)

## 委派存取 tooresources
### [管理員角色](active-directory-assign-admin-roles.md)
#### [指派管理員角色](active-directory-users-assign-role-azure-portal.md)
### [管理單位](active-directory-administrative-units-management.md)
### [Azure 中的資源存取](active-directory-understanding-resource-access.md)
### [角色型存取控制](role-based-access-control-what-is.md)
#### 管理存取權指派
##### [依使用者](role-based-access-control-manage-assignments.md)
##### [依資源](role-based-access-control-configure.md)
#### [內建角色](role-based-access-built-in-roles.md)
#### [自訂角色](role-based-access-control-custom-roles.md)
#### [為內部及外部使用者指派自訂角色](role-based-access-control-create-custom-roles-for-internal-external-users.md)
#### [報告](role-based-access-control-access-change-history-report.md)
#### 更多方式 toomanage 角色
##### [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
##### [PowerShell](role-based-access-control-manage-access-powershell.md)
##### [REST](role-based-access-control-manage-access-rest.md)
#### [提高租用戶系統管理員存取權](role-based-access-control-tenant-admin-access.md)
#### [疑難排解](role-based-access-control-troubleshooting.md)
#### [資源提供者作業](role-based-access-control-resource-provider-operations.md)
### [設定權杖存留期](active-directory-configurable-token-lifetimes.md)

## 保護您的身分識別
### [條件式存取](active-directory-conditional-access-azure-portal.md)
#### [開始使用](active-directory-conditional-access-azure-portal-get-started.md)
#### [最佳作法](active-directory-conditional-access-best-practices.md)
#### [技術參考](active-directory-conditional-access-technical-reference.md)
#### [支援的應用程式](active-directory-conditional-access-supported-apps.md)
#### [了解裝置原則](active-directory-conditional-access-device-policies.md)
#### [設定存取 tooconnected 應用程式](active-directory-conditional-access-policy-connected-applications.md)
#### [補救](active-directory-conditional-access-device-remediation.md)
#### [常見問題集](active-directory-conditional-faqs.md)
#### [傳統入口網站](active-directory-conditional-access.md)
##### [開始使用](active-directory-conditional-access-azuread-connected-apps.md)


### Windows Hello
#### [無需密碼驗證](active-directory-azureadjoin-passport.md)
#### [啟用 Windows Hello 企業版](active-directory-azureadjoin-passport-deployment.md)
### 憑證式驗證
#### [Android](active-directory-certificate-based-authentication-android.md)
#### [iOS](active-directory-certificate-based-authentication-ios.md)
#### [開始使用](active-directory-certificate-based-authentication-get-started.md)

### [Azure AD Identity Protection](active-directory-identityprotection.md)
#### [啟用](active-directory-identityprotection-enable.md)
#### [偵測弱點](active-directory-identityprotection-vulnerabilities.md)
#### [風險事件](active-directory-identity-protection-risk-events.md)
#### [Notifications](active-directory-identityprotection-notifications.md)
#### [登入體驗](active-directory-identityprotection-flows.md)
#### [模擬風險事件](active-directory-identityprotection-playbook.md)
#### [解除封鎖使用者](active-directory-identityprotection-unblock-howto.md)
#### [常見問題集](active-directory-identity-protection-faqs.md)
#### [詞彙](active-directory-identityprotection-glossary.md)
#### [Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
### [Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

## [在 Azure VM 上部署 AD DS](virtual-networks-windows-server-active-directory-virtual-machines.md)
### [Azure VM 上的 Windows Server Active Directory](active-directory-deploying-ws-ad-guidelines.md)
### [Azure 虛擬網路中的複本網域控制站](active-directory-install-replica-active-directory-domain-controller.md)
### [在 Azure 虛擬網路上的新樹系](active-directory-new-forest-virtual-machine.md)



## [在 Azure 中部署 AD FS](active-directory-aadconnect-azure-adfs.md)
### [高可用性](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
### [變更簽章雜湊演算法](active-directory-federation-sha256-guidance.md)

## [疑難排解](active-directory-troubleshooting-support-howto.md)
### [針對 Active Directory 項目遺失或無法使用的問題進行疑難排解](active-directory-troubleshooting.md)

## 部署 Azure AD 概念證明 (PoC)
### [PoC 腳本：簡介](active-directory-playbook-intro.md)
### [PoC 腳本：因素](active-directory-playbook-ingredients.md)
### [PoC 腳本：實作](active-directory-playbook-implementation.md)
### [PoC 腳本：建置區塊](active-directory-playbook-building-blocks.md)


# 參考
## [程式碼範例](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory)
## [PowerShell Cmdlet](/powershell/azure/overview)
## [Java API 參考](/java/api)
## [.NET API](/active-directory/adal/microsoft.identitymodel.clients.activedirectory)
## [服務限制](active-directory-service-limits-restrictions.md)

# 相關參考
## [Multi-Factor Authentication](/azure/multi-factor-authentication/)
## [Azure AD Connect](./connect/active-directory-aadconnect.md)
## [Azure AD Connect Health](./connect-health/active-directory-aadconnect-health.md)
## [開發人員適用的 Azure AD](./develop/active-directory-how-to-integrate.md)
## [Azure AD Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

# 資源
## [Azure 意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory)
## [Azure 藍圖](https://azure.microsoft.com/roadmap/?category=security-identity)
## [MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)
## [價格](https://azure.microsoft.com/pricing/details/active-directory/)
## [定價計算機](https://azure.microsoft.com/pricing/calculator/)
## [服務更新](https://azure.microsoft.com/updates/?product=active-directory)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
## [影片](https://azure.microsoft.com/documentation/videos/index/?services=active-directory)
