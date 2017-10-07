---
title: "Office 365 和 Azure AD 使用者能夠 aaaCertificate 更新 |Microsoft 文件"
description: "本文說明如何 tooresolve 問題的電子郵件，通知他們續約憑證 tooOffice 365 使用者。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>更新 Office 365 和 Azure Active Directory 的同盟憑證
## <a name="overview"></a>概觀
Azure Active Directory (Azure AD) 與 Active Directory Federation Services (AD FS) 之間成功的同盟，使用的 AD FS toosign 安全性語彙基元 tooAzure AD 的 hello 憑證應該符合 Azure AD 中的設定。 任何不相符，可能會導致 toobroken 信任。 Azure AD 會確保這項資訊在您部署 AD FS 和 Web 應用程式 Proxy (適用於外部網路存取) 時保持同步。

這篇文章提供額外資訊 toomanage 權杖簽署憑證並將它們與 Azure AD 同步 hello 下列案例：

* 您並不會部署 hello Web 應用程式 Proxy，並因此 hello 同盟中繼資料就無法用於外部網路的 hello。
* 您不使用 hello 預設組態，AD fs 權杖簽署憑證。
* 您要使用協力廠商的識別提供者。

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>權杖簽署憑證的預設 AD FS 設定
hello 權杖簽署和權杖解密憑證通常是自我簽署的憑證，並且也適合用來一年。 根據預設，AD FS 包含名為 **AutoCertificateRollover**的自動更新程序。 如果您使用 AD FS 2.0 或更新版本，Office 365 和 Azure AD 在您的憑證到期之前會自動進行更新。

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>從 hello Office 365 入口網站或電子郵件的更新通知
> [!NOTE]
> 如果您收到一封電子郵件或要求您 toorenew 入口網站通知您的憑證適用於 Office，請參閱[管理變更簽署憑證的 tootoken](#managecerts) toocheck，如果您需要 tootake 任何動作。 Microsoft 了解可能的問題，可能會導致 toonotifications 進行傳送，即使不不需要任何動作的憑證更新。
>
>

Azure AD 會嘗試 toomonitor hello 同盟中繼資料，以及更新 hello 權杖簽署憑證，此中繼資料所示。 hello hello 權杖簽署憑證到期前 30 天會檢查 Azure AD，新的憑證是否可用，藉由輪詢 hello 同盟中繼資料。

* 如果成功，它可以輪詢 hello 同盟中繼資料，並擷取 hello 新的憑證，沒有電子郵件通知或 hello Office 365 入口網站中的警告會發出 toohello 使用者。
* 如果它無法擷取 hello 新權杖簽署憑證，可能是因為找不到 hello 同盟中繼資料，或未啟用自動憑證變換，Azure AD 會發出電子郵件通知和 hello Office 365 入口網站中的警告。

![Office 365 入口網站通知](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> 如果您使用 AD FS，tooensure 業務持續性，請確認您的伺服器有 hello 下列更新，因此不會發生的已知問題的驗證失敗。 這可減少在此更新和未來更新期間的已知 AD FS Proxy 伺服器問題︰
>
> Server 2012 R2 - [Windows Server 2014 年 5 月彙總套件](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 和 2012 - [在 Windows Server 2012 或 Windows 2008 R2 SP1 中透過 Proxy 驗證失敗](http://support.microsoft.com/kb/3094446)
>
>

## 檢查 hello 憑證是否需要更新 toobe<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>步驟 1： 檢查 hello AutoCertificateRollover 狀態
在 AD FS 伺服器上開啟 Powershell。 請檢查確定 hello AutoCertificateRollover 值設定 tooTrue。

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>如果您使用 AD FS 2.0，請先執行 Add-Pssnapin Microsoft.Adfs.Powershell。

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>步驟 2︰確認 AD FS 和 Azure AD 已同步
在 AD FS 伺服器上，開啟 hello Azure AD PowerShell 命令提示字元，並連接 tooAzure AD。

> [!NOTE]
> 您可以從 [這裡](https://technet.microsoft.com/library/jj151815.aspx)下載 Azure AD PowerShell。
>
>

    Connect-MsolService

請檢查設定 AD FS 中的 hello 憑證以及 hello 的 Azure AD 信任屬性指定的網域。

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

如果在 hello 指紋 hello 輸出相符項目，您的憑證會與 Azure AD 同步。

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>步驟 3： 檢查您的憑證是否需 tooexpire
Get-msolfederationproperty 或 Get AdfsCertificate hello 輸出，在檢查 hello 日期下 「 不之後。 」 如果 hello 日期為小於 30 天內改變了，您應該採取動作。

| AutoCertificateRollover | 憑證與 Azure AD 同步 | 可公開取得同盟中繼資料 | 有效期 | 動作 |
|:---:|:---:|:---:|:---:|:---:|
| 是 |是 |是 |- |不需採取動作。 請參閱 [自動更新權杖簽署憑證](#autorenew)。 |
| 是 |否 |- |小於 15 天 |立即更新。 請參閱 [手動更新權杖簽署憑證](#manualrenew)。 |
| 否 |- |- |少於 30 天 |立即更新。 請參閱 [手動更新權杖簽署憑證](#manualrenew)。 |

\[-]  無關緊要

## 更新 hello 權杖簽署憑證自動 （建議選項）<a name="autorenew"></a>
如果 hello 下列都符合您不需要指定 tooperform 任何手動操作步驟：

* 您已部署 Web 應用程式 Proxy，可啟用從 hello 外部網路存取 toohello 同盟中繼資料。
* 您正在使用 hello AD FS 預設組態 （AutoCertificateRollover 已啟用）。

請檢查下列 hello 憑證的 tooconfirm hello 可以自動更新。

**1.hello AutoCertificateRollover 的 AD FS 屬性必須設定 tooTrue。** 這表示 AD FS 會自動產生新的權杖簽署和權杖解密憑證，hello 舊的到期之前。

**2.hello AD FS 同盟中繼資料是可公開存取。** 檢查您的同盟中繼資料瀏覽 toohello 是可公開存取的電腦中的下列 URL，hello 公用網際網路 （開 hello 企業網路）：

https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml

其中`(your_FS_name) `取代為您的組織使用，例如 fs.contoso.com hello federation service 主機名稱。如果您無法 tooverify 這兩個的這些設定成功，您不需要 toodo 任何其他項目。  

範例：https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## 更新 hello 權杖簽署憑證，以手動方式<a name="manualrenew"></a>
您可以選擇 toorenew hello 權杖簽署憑證以手動方式。 例如，hello 下列案例可能更適合手動更新：

* 權杖簽署憑證不是自我簽署憑證。 hello 最常見的原因是您的組織管理組織的憑證授權單位從註冊的 AD FS 憑證。
* 網路安全性不允許 hello 同盟中繼資料 toobe 公開使用。

在這些情況下，每次您更新 hello 權杖簽署憑證，您也必須更新您的 Office 365 網域使用 hello PowerShell 命令，Update-msolfederateddomain。

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>步驟 1︰確認 AD FS 具有新的權杖簽署憑證
**非預設設定**

如果您使用 AD FS 的非預設組態 (其中**AutoCertificateRollover**設定得**False**)，您可能想要使用自訂憑證 （不是自我簽署）。 如需有關如何 toorenew hello AD FS 權杖簽署憑證的詳細資訊，請參閱[指導的客戶未使用 AD FS 自我簽署憑證](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)。

**無法公開取得同盟中繼資料**

如果在 hello 相反地， **AutoCertificateRollover**設定得**True**，但您的同盟中繼資料不是可公開存取，首先請確定是否已由 AD 產生新的權杖簽署憑證FS。 確認您有新的權杖簽署憑證的步驟採取 hello:

1. 請確認您已登入 toohello 主要 AD FS 伺服器。
2. 檢查開啟 PowerShell 命令視窗中，並執行下列命令的 hello hello 目前的簽署憑證中 AD FS:

    PS C:\>Get-ADFSCertificate -CertificateType token-signing

   > [!NOTE]
   > 如果您使用 AD FS 2.0，則必須先執行 Add-Pssnapin Microsoft.Adfs.Powershell。
   >
   >
3. 查看 hello 命令輸出，在列出任何憑證。 如果 AD FS 已產生新的憑證，您應該會看到 hello 輸出中的兩個憑證： 一個用於哪些 hello **IsPrimary**值是**True**和 hello **NotAfter**日期在 5 天，而另一個用於其**IsPrimary**是**False**和**NotAfter**是關於在 hello 未來一年。
4. 如果您只有一個憑證，請參閱 < 和 hello **NotAfter**日期為 5 天內，您需要 toogenerate 新憑證。
5. toogenerate 新憑證時，執行下列 PowerShell 命令提示字元命令的 hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`。
6. 執行下列命令一次的 hello 驗證 hello 更新： PS c:\>Get ADFSCertificate – Token-encryption 權杖簽署

現在應該會列出兩個憑證，其中具有**NotAfter**日期大約一年中 hello 未來，以及哪些 hello **IsPrimary**值是**False**。

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>步驟 2： 更新 hello 新權杖簽署憑證 hello Office 365 信任
更新 hello 新權杖簽署憑證 toobe，如下所示為 hello 信任使用 Office 365。

1. 開啟 hello Microsoft Azure Active Directory 的 Windows PowerShell 模組。
2. 執行 $cred=Get-Credential。 當此 Cmdlet 提示您輸入認證時，請輸入您的雲端服務系統管理員帳戶認證。
3. 執行 Connect-MsolService –Credential $cred。此 cmdlet 會將您連線 toohello 雲端服務。 建立會將您連線的內容 toohello 雲端服務都必須先執行任何 hello hello 工具所安裝的其他 cmdlet。
4. 如果您不是 AD FS hello 主要同盟伺服器的電腦上執行這些命令，執行 Set-msoladfscontext-電腦<AD FS primary server>，其中<AD FS primary server>是 hello 主要 AD FS 伺服器的 hello 內部 FQDN 名稱。 此 cmdlet 會建立 tooAD FS 會將您連線的內容。
5. 執行 Update-MSOLFederatedDomain –DomainName <domain>。 此 cmdlet 會更新到 hello 的雲端服務，從 AD FS 的 hello 設定，並設定 hello hello 兩者之間的信任關係。

> [!NOTE]
> 如果您需要 toosupport 多個最上層網域的詳細資訊，例如 contoso.com 和 fabrikam.com，您必須使用 hello **SupportMultipleDomain**參數搭配任何 cmdlet。 如需詳細資訊，請參閱 [支援多個頂層網域](active-directory-aadconnect-multiple-domains.md)。
>
>

## 使用 Azure AD Connect 修復 Azure AD 信任 <a name="connectrenew"></a>
如果您使用 Azure AD Connect 設定您的 AD FS 伺服器陣列和 Azure AD 信任，您可以使用 Azure AD Connect toodetect，如果您對於您的權杖簽署憑證需要 tootake 任何動作。 如果您需要 toorenew hello 憑證時，您可以使用 Azure AD Connect toodo 因此。

如需詳細資訊，請參閱[修復 hello 信任](active-directory-aadconnect-federation-management.md)。
