---
title: "aaaTroubleshooting 混合 Azure Active Directory 已加入 Windows 10 和 Windows Server 2016 的裝置 |Microsoft 文件"
description: "針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解 

本主題僅適用於 toohello 下列用戶端：

-   Windows 10
-   Windows Server 2016

至於其他 Windows 用戶端，請參閱[針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解](device-management-troubleshoot-hybrid-join-windows-legacy.md)。

本主題假設您有[設定混合式 Azure Active Directory 加入裝置](device-management-hybrid-azuread-joined-devices-setup.md)toosupport hello 下列案例：

- 裝置型條件式存取

- [設定的企業漫遊](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello 企業版](active-directory-azureadjoin-passport-deployment.md)


這份文件上如何 tooresolve 可能的問題提供疑難排解指引。 


適用於 Windows 10 和 Windows Server 2016，混合 Azure Active Directory 聯結支援 hello Windows 10 11 月更新 2015年和更新版本。 我們建議使用 hello 週年日更新。

## <a name="step-1-retrieve-hello-join-status"></a>步驟 1： 擷取 hello 聯結狀態 

**tooretrieve hello 聯結狀態：**

1. 以系統管理員身分開啟 hello 命令提示字元

2. 輸入 **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: 沒有 DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 指紋： B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 平台密碼編譯提供者 TpmProtected： 是KeySignTest:: 必須執行更高的 tootest。
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>步驟 2： 評估 hello 聯結狀態 

檢閱 hello 下列欄位，並確定它們有 hello 預期值：

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

此欄位會指出是否要將 hello 裝置加入 Azure ad。 如果 hello 值**否**，hello 聯結 tooAzure AD 尚未完成。 

**可能的原因：**

- 聯結的 hello 電腦驗證失敗。

- 無法探索 hello 電腦的 hello 組織中沒有 HTTP proxy

- hello 電腦無法連線到 Azure AD tooauthenticate 或 Azure DRS 的註冊

- hello 電腦可能不是 VPN 或 hello 組織內部網路上的直接視線 tooan 在內部部署 AD 網域控制站。

- 如果 hello 電腦有 TPM，它可以處於不正常的狀態。

- 可能有在 hello 服務設定不正確前文所述 hello 文件中，您需要 tooverify 一次。 常見範例包括：

    - 您的同盟伺服器未啟用 WS-Trust 端點

    - 您的同盟伺服器不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。

    - 在 Azure AD 中點 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中沒有服務連接點物件

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

此欄位會指出是否已加入 hello 裝置 tooan 內部部署 Active Directory 或不。 如果 hello 值**否**，hello 裝置無法執行 Azure AD 混合式連接。  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

此欄位會指出是否註冊為個人裝置的 Azure AD 裝置 hello (標示為*工作地方聯結*)。 如果已加入網域的電腦同時加入混合式 Azure AD，此值應為 **NO**。 如果 hello 值**是**、 工作或學校帳戶加入先前 toohello 完成的 hello Azure AD 混合式連接。 在此情況下，使用 hello 年度更新版的 Windows 10 (1607) 時，會忽略 hello 帳戶。

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES 和 AzureADPrt : YES
  
這些欄位會指出 hello 使用者是否已成功驗證 tooAzure AD toohello 裝置在登入時。 如果 hello 值**否**，可能是因為：

- 不正確的儲存體金鑰 (STK) 與 hello 裝置時註冊 (核取 hello KeySignTest 執行提高權限) 相關聯的 TPM。

- 替代登入識別碼

- 找不到 HTTP Proxy

## <a name="next-steps"></a>後續步驟

如有問題，請參閱 hello[裝置管理常見問題集](device-management-faq.md) 
