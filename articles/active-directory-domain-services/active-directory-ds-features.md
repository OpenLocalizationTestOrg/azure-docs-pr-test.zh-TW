---
title: "Azure Active Directory Domain Services：功能 | Microsoft Docs"
description: "Azure Active Directory 網域服務的功能"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD 網域服務
## <a name="features"></a>特性
下列功能的 hello 可用於管理 Azure AD 網域服務網域。

* **簡單的部署經驗：** 您只需使用數個按鍵，就能針對 Azure AD 租用戶啟用 Azure AD 網域服務。 不論您的 Azure AD 租用戶是雲端租用戶，還是會與您的內部部署目錄進行同步處理，都能快速佈建您受管理的網域。
* **加入網域的支援：**您可以輕鬆地在 hello Azure 受管理的網域是使用中的虛擬網路中加入網域電腦。 Windows 用戶端和伺服器作業系統運作順暢地對服務的 Azure AD 網域服務的網域上的 hello 網域加入體驗。 您也可以針對這類網域使用自動化網域加入工具。
* **每個 Azure AD 目錄都有一個網域執行個體：** 您可以針對每個 Azure AD 目錄建立單一 Active Directory 網域。
* **建立含有自訂名稱的網域：** 您可以使用 Azure AD 網域服務，來建立含有自訂名稱的網域 (例如 'contoso100.com')。 您可以使用已驗證或未驗證的網域名稱。 您也可以選擇建立網域與 hello 內建的網域尾碼 (也就是 ' *。 onmicrosoft.com') 提供的 Azure AD 目錄。
* **與 Azure AD 整合：**您不需要 tooconfigure 或管理複寫 tooAzure AD 網域服務。 Azure AD 網域服務中會自動提供來自 Azure AD 目錄的使用者帳戶、群組成員資格和使用者認證 (密碼)。 新的使用者、 群組或從 Azure AD 租用戶或內部部署目錄的變更 tooattributes 會自動同步處理的 tooAzure AD 網域服務。
* **NTLM 和 Kerberos 驗證：** 利用對 NTLM 和 Kerberos 驗證的支援，您就能夠部署依賴 Windows 整合式驗證的應用程式。
* **使用公司認證/密碼：** Azure AD 租用戶中使用者的密碼可以與 Azure AD 網域服務搭配使用。 使用者可以使用其公司認證 toodomain 聯結機器、 以互動方式或透過遠端桌面] 登入及驗證 hello 受管理的網域。
* **LDAP 繫結與 LDAP 讀取支援：**您可以使用依賴 LDAP 繫結服務的 Azure AD 網域服務的網域中的 tooauthenticate 使用者應用程式。 此外，使用 LDAP 應用程式讀取從 hello 目錄 tooquery 使用者/電腦屬性也可對 Azure AD 網域服務的作業。
* **安全 LDAP (LDAPS):**啟用存取 toohello 目錄透過安全 LDAP (LDAPS)。 使用預設的 hello 虛擬網路內安全 LDAP 存取。 不過，您可以選擇啟用安全 LDAP 存取 hello 透過網際網路。
* **群組原則：** hello 使用者及電腦的可用單一內建 GPO 每個容器 tooenforce 是否符合必要的安全性原則的使用者帳戶和網域的電腦。 您可以建立您自己自訂的 Gpo，並將它們指派 toocustom 組織單位太[管理群組原則](active-directory-ds-admin-guide-administer-group-policy.md)。
* **管理 DNS:** hello ' AAD DC Administrators' 群組的成員可以管理 DNS 您受管理的網域，使用熟悉的 DNS 系統管理工具，例如 hello DNS 管理 MMC 嵌入式管理單元。
* **建立自訂的組織單位 (Ou):** hello ' AAD DC Administrators' 群組的成員可以在 [hello 受管理的網域中建立自訂的 Ou。 這些使用者會被授與自訂 OU 的完整系統管理權限，讓他們可以在這些自訂的 OU 內新增或移除服務帳戶、電腦、群組等。
* **使用多個 Azure 區域中：** ，請參閱 hello[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)頁面 tooknow hello Azure AD 網域服務可用的 Azure 區域。
* **高可用性：** Azure AD 網域服務可針對您的網域提供高可用性。 這項功能提供更高的服務執行時間和恢復功能 toofailures hello 保證。 內建的健全狀況監視提供自動的補救失敗才能組織好新的執行個體 tooreplace 失敗執行個體和 tooprovide 繼續為您的網域服務。
* **使用熟悉的管理工具：**您可以使用熟悉的 Windows Server Active Directory 管理工具，例如 hello Active Directory 管理中心或 PowerShell 的 Active Directory tooadminister 受管理的網域。
