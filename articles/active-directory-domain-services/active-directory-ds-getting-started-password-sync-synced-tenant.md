---
title: "Azure AD 網域服務︰啟用密碼同步處理 | Microsoft Docs"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>啟用密碼同步處理 tooAzure Active Directory 網域服務
在先前工作中，您已啟用 Azure Active Directory (Azure AD) 租用戶的 Azure Active Directory Domain Services。 hello 下一個工作是 tooenable 認證雜湊同步處理所需的 NT LAN Manager (NTLM) 和 Kerberos 驗證 tooAzure AD 網域服務。 您已設定認證同步處理之後，使用者可以登入 toohello 受管理的網域，利用其公司認證。

所需的 hello 步驟截然不同的僅限雲端的使用者帳戶與使用者帳戶從您使用 Azure AD Connect 的內部部署目錄同步。 必須有 Azure AD 租用戶的組合雲端唯一的使用者和使用者從您內部部署 AD 中，您需要 tooperform 這兩個步驟。

<br>

> [!div class="op_single_selector"]
> * **僅限雲端的使用者帳戶**:[為僅限雲端的使用者帳戶 tooyour 受管理的網域，同步處理密碼](active-directory-ds-getting-started-password-sync.md)
> * **在內部部署使用者帳戶**:[從您在內部同步處理的使用者帳戶的密碼同步處理 AD tooyour 管理網域](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>工作 5： 啟用密碼同步處理 tooyour 受管理的網域使用者帳戶與您在內部同步處理 AD
同步處理 Azure AD 租用戶與您的組織在內部部署目錄使用 Azure AD Connect 設定 toosynchronize。 根據預設，Azure AD Connect 不會同步處理，NTLM 和 Kerberos 認證雜湊 tooAzure AD。 toouse Azure AD 網域服務，您需要 tooconfigure Azure AD Connect toosynchronize 認證雜湊所需的 NTLM 和 Kerberos 驗證。 hello 下列步驟啟用所需的 hello 認證雜湊，從內部部署目錄 tooyour Azure AD 租用戶的同步處理。

> [!NOTE]
> 如果您的組織有從您的內部部署目錄，您必須同步的使用者帳戶啟用的 NTLM 和 Kerberos 順序 toouse hello 受管理的網域中的雜湊同步處理。 同步處理的使用者帳戶是已在內部部署目錄中建立，並且為帳戶同步處理 tooyour 使用 Azure AD Connect 的 Azure AD 租用戶。
>
>

### <a name="install-or-update-azure-ad-connect"></a>安裝或更新 Azure AD Connect
安裝 hello 建議的最新版本的網域上的 Azure AD Connect 加入電腦。 如果您有 Azure AD Connect 的安裝程式的現有執行個體，您需要 tooupdate 它 toouse hello 最新版的 Azure AD Connect。 tooavoid 已知問題/可能有已獲得修正的 bug，請確定您一律使用 Azure AD connect 的 hello 最新版本。

**[下載 Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

建議版本：**1.1.553.0** - 已於 2017 年 6 月 27 日發佈。

> [!WARNING]
> 您必須安裝 hello 建議的最新版本的 Azure AD Connect tooenable hello 舊版的密碼 （NTLM 和 Kerberos 驗證所需） 認證 toosynchronize tooyour Azure AD 租用戶。 無法在舊版本的 Azure AD Connect，或使用 hello 舊版目錄同步工具中使用這項功能。
>
>

Azure AD Connect 的安裝指示可用於 hello 下列文件-[開始使用 Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>啟用 NTLM 和 Kerberos 認證雜湊 tooAzure AD 同步的處理
執行下列 PowerShell 指令碼在每個 AD 樹系，tooforce 完整密碼同步處理，hello，並啟用所有在內部部署使用者的認證雜湊 toosync tooyour Azure AD 租用戶。 此指令碼可讓 hello NTLM/Kerberos 驗證 toobe 同步的 tooyour Azure AD 租用戶所需的認證雜湊。

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

視您的目錄 hello 大小而定 (數字的使用者，群組等)，同步處理的認證雜湊的 tooAzure AD 花的時間。 hello 密碼便可以使用 hello Azure AD 網域服務受管理的網域上 hello 認證雜湊已同步處理 tooAzure AD 後不久。

<br>

## <a name="related-content"></a>相關內容
* [啟用密碼同步處理 tooAAD 網域服務，僅限雲端的 azure AD 目錄](active-directory-ds-getting-started-password-sync.md)
* [Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)](active-directory-ds-admin-guide-administer-domain.md)
* [加入 Windows 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)
* [加入 Red Hat Enterprise Linux 虛擬機器 tooan Azure AD 網域服務受管理的網域](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
