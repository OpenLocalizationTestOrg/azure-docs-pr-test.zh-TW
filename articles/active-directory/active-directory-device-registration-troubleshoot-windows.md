---
title: "適用於 Windows 10 和 Windows Server 2016 aaaTroubleshooting hello 自動註冊的 Azure AD 網域加入的電腦 |Microsoft 文件"
description: "疑難排解 hello 自動註冊的 Azure AD 網域加入適用於 Windows 10 和 Windows Server 2016 的電腦。"
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016

本主題僅適用於 toohello 下列用戶端：

-   Windows 10
-   Windows Server 2016

其他 Windows 用戶端，請參閱[疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD](active-directory-device-registration-troubleshoot-windows-legacy.md)。

本主題假設您已設定自動註冊已加入網域的裝置如中所述述[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-device-registration-get-started.md)下列案例 toosupport hello:

- [裝置型條件式存取](active-directory-conditional-access-automatic-device-registration-setup.md)

- [設定的企業漫遊](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello 企業版](active-directory-azureadjoin-passport-deployment.md)


這份文件上如何 tooresolve 可能的問題提供疑難排解指引。 

hello 註冊支援 hello Windows 10 11 月版 2015年更新和更新版本。  
我們建議使用 hello 週年紀念日更新啟用上述的 hello 案例。

## <a name="step-1-retrieve-hello-registration-status"></a>步驟 1： 擷取 hello 註冊狀態 

**tooretrieve hello 註冊狀態：**

1. 系統管理員身分開啟命令提示字元中 hello。

2. 輸入 **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: 沒有 DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 指紋： B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 平台密碼編譯提供者 TpmProtected： 是KeySignTest:: 必須執行更高的 tootest。
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>步驟 2： 評估 hello 登錄狀態 

檢閱 hello 下列欄位，並確定它們有 hello 預期值：

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

此欄位會顯示 hello 裝置是否已向 Azure AD。 如果 hello 值顯示為 [否]，註冊尚未完成。 

**可能的原因：**

- 註冊的 hello 電腦驗證失敗。

- 無法探索 hello 電腦的 hello 組織中沒有 HTTP proxy

- hello 電腦無法連線到 Azure AD 進行驗證或註冊的 Azure DRS

- hello 電腦可能不是 VPN 或 hello 組織內部網路上的直接視線 tooan 在內部部署 AD 網域控制站。

- 如果 hello 電腦有 TPM，它可能處於不正常的狀態。

- 可能會在 服務設定不正確前文所述 hello 文件中，您需要 tooverify 一次。 常見範例包括：

    - 您的同盟伺服器未啟用 WS-Trust 端點

    - 您的同盟伺服器可能不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。

    - 在 Azure AD 中點 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中沒有服務連接點物件

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

此欄位會顯示 hello 裝置是否已加入的 tooan 內部部署 Active Directory。 如果 hello 值顯示為**否**，hello 裝置無法自動註冊使用 Azure AD。 請先檢查該 hello 裝置聯結 toohello 內部部署 Active Directory 之前可以向 Azure AD。 如果您要加入 hello 電腦 tooAzure AD 直接尋找，請移 tooLearn 有關功能的 Azure Active Directory Join。

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

此欄位會顯示 hello 裝置註冊的 Azure AD 但為個人裝置 （標示為 ' 加入工作場所 '）。 如果向 Azure AD 註冊已加入網域電腦，這個值應顯示為 [否]，但是它會顯示為 [是]，其表示，如果工作或學校帳戶就是加入先前 toohello 電腦完成登錄。 在此情況下若使用 hello 年度更新版的 Windows 10 (1607 當執行的 hello WinVer 命令 hello 'Run' 視窗或命令提示字元視窗)，將會忽略 hello 帳戶。

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES 和 AzureADPrt : YES
  
這些欄位會顯示該 hello 使用者已成功驗證 tooAzure AD 時登入 toohello 裝置。 如果它們顯示 'NO' hello 以下是可能的原因：

- 不正確的儲存體金鑰 (STK) 與 hello 裝置時註冊 (核取 hello KeySignTest 執行提高權限) 相關聯的 TPM。

- 替代登入識別碼

- 找不到 HTTP Proxy

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 hello[自動裝置註冊常見問題集](active-directory-device-registration-faq.md) 
