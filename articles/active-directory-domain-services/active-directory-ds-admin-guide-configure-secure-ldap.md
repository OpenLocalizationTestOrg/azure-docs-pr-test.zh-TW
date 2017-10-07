---
title: "aaaConfigure 安全 LDAP (LDAPS) 在 Azure AD 網域服務中 |Microsoft 文件"
description: "針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>針對 Azure AD 網域服務受管理網域設定安全的 LDAP (LDAPS)
本文說明如何為 Azure AD 網域服務受管理網域啟用安全的輕量型目錄存取通訊協定 (LDAPS)。 安全的 LDAP 亦稱為「透過安全通訊端層 (SSL)/傳輸層安全性 (TLS) 的輕量型目錄存取通訊協定 (LDAP)」。

## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。
4. A**憑證使用 toobe tooenable 安全 LDAP**。

   * **建議** - 從受信任的公共憑證授權單位取得憑證。 這是更安全的組態選項。
   * 或者，您也可以選擇太[建立自我簽署的憑證](#task-1---obtain-a-certificate-for-secure-ldap)如本文稍後所示。

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Hello 安全 LDAP 的憑證需求
取得每個 hello 遵循的指導方針，才能啟用安全 LDAP 的有效憑證。 如果您嘗試 tooenable，發生失敗的無效/不正確的憑證與您受管理的網域安全 LDAP。

1. **受信任簽發者**-hello 憑證必須由電腦連接 toohello 使用安全 LDAP 的受管理的網域信任授權單位發行。 此授權單位可能是受這些電腦信任的公開憑證授權單位。
2. **存留期**-hello 憑證必須是有效的最少 hello 接下來 3-6 個月。 Hello 憑證到期時中斷安全 LDAP 存取 tooyour 受管理的網域。
3. **主體名稱**-hello hello 憑證的主體名稱必須是受管理的網域的萬用字元。 比方說，如果您的網域名稱為 'contoso100.com'，hello 憑證的主體名稱必須是 ' *。 contoso100.com'。 設定 hello DNS 名稱 （主旨替代名稱） toothis 萬用字元名稱。
4. **金鑰使用方法**-hello 之後使用，必須設定 hello 憑證的數位簽章和金鑰加密。
5. **憑證目的**-hello 憑證必須是有效的 SSL 伺服器驗證。

> [!NOTE]
> **企業憑證授權單位︰**Azure AD Domain Services 不支援使用貴組織的企業憑證授權單位所簽發的安全 LDAP 憑證。 這項限制是因為 hello 服務不信任您的企業 CA 根憑證授權單位。 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>工作 1 - 取得安全 LDAP 的憑證
hello 第一項工作需要取得憑證，用於安全 LDAP 存取 toohello 受管理的網域。 您有兩個選擇：

* 從憑證授權單位取得憑證。 hello 授權單位可能會公開憑證授權單位。
* 建立自我簽署憑證。

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>選項 A (建議選項) - 從憑證授權單位取得安全的 LDAP 憑證
如果您的組織從公開憑證授權單位取得憑證，您需要 tooobtain hello 安全 LDAP 的憑證從該公用憑證授權單位。

當要求憑證，請確定您符合所有中所述的 hello 需求[hello 安全 LDAP 的憑證需求](#requirements-for-the-secure-ldap-certificate)。

> [!NOTE]
> 需要使用安全 LDAP tooconnect toohello 受管理的網域的用戶端電腦必須信任簽發者 hello hello 安全 LDAP 的憑證。
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>選項 B - 為安全的 LDAP 建立自我簽署的憑證
如果您不希望 toouse 從公開憑證授權單位的憑證，您可以選擇 toocreate 自我簽署的憑證安全 ldap。

**使用 PowerShell 建立自我簽署憑證**

在您的 Windows 電腦上開啟 新的 PowerShell 視窗，做為**管理員**和型別 hello 下列命令，toocreate 新的自我簽署憑證。

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

在上述範例的 hello，取代 '*。 contoso100.com' hello DNS 網域名稱是受管理的網域。例如，如果您建立受管理的網域，稱為 'contoso100.onmicrosoft.com' 取代 '*。 contoso100.com' hello 上述指令碼在' *。 contoso100.onmicrosoft.com')。

![選取 Azure AD 目錄](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

hello 新建立的自我簽署的憑證放置在 hello 本機電腦的憑證存放區中。


## <a name="next-step"></a>後續步驟
[工作 2-匯出 hello 安全 LDAP 的憑證 tooa。PFX 檔案](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
