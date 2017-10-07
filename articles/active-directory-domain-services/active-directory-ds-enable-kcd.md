---
title: "Azure Active Directory Domain Services：啟用 Kerberos 限制委派 | Microsoft Docs"
description: "在 Azure Active Directory Domain Services 受管理的網域上啟用 Kerberos 限制委派"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>在受管理的網域上設定 Kerberos 限制委派 (KCD)
許多應用程式需要 tooaccess hello hello 使用者內容中的資源。 Active Directory 支援稱為 Kerberos 委派的機制，可用於此使用案例。 此外，您可以限制委派，以便只有特定的資源可存取 hello hello 使用者內容中。 Azure AD Domain Services 受管理的網域與傳統Active Directory 網域不同，因為前者的權限更為嚴格且更為安全。

本文章將示範如何 tooconfigure kerberos 限制委派，在 Azure AD 網域服務受管理的網域。

## <a name="kerberos-constrained-delegation-kcd"></a>Kerberos 限制委派 (KCD)
Kerberos 委派可讓帳戶 tooimpersonate 另一個安全性主體 （例如使用者） tooaccess 資源。 請考慮存取 hello 使用者內容中的後端 web 應用程式開發介面的 web 應用程式。 在此範例中，hello （hello 的服務帳戶或電腦/機器帳戶的內容中執行） 的 web 應用程式會模擬 hello 使用者存取 hello 資源 (後端 web 應用程式開發介面) 時。 Kerberos 委派是不安全的因為它並未限制資源 hello 模擬帳戶可以存取 hello hello 使用者內容中的 hello。

Kerberos 限制委派 (KCD) 會限制的 hello hello 代表使用者執行的服務/資源 toowhich hello 指定的伺服器可採取動作。 傳統的 KCD 的服務需要網域系統管理員權限 tooconfigure 網域帳戶，它會限制 hello 帳戶 tooa 單一網域。

傳統 KCD 也有一些問題。 在舊版作業系統 hello 網域系統管理員設定 hello 服務的位置，hello 服務系統管理員有哪些前端服務委派 toohello 他們所擁有的資源服務不實用的方式 tooknow。 和任何前端服務都可以委派 tooa 資源服務代表一個潛在的攻擊點。 如果裝載前端服務的伺服器已遭到洩露，而且它是設定的 toodelegate tooresource 服務，可能也會有 hello 資源服務。

> [!NOTE]
> 在 Azure AD Domain Services 受管理的網域上，您沒有網域系統管理員權限。 因此，**無法在受管理的網域上設定傳統 KCD**。 使用此文章中所述的資源型 KCD。 此機制也比較安全。
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>資源型 Kerberos 限制委派
在 Windows Server 2012 R2 和 Windows Server 2012 中，已從 hello 網域系統管理員 toohello 服務系統管理員移轉的 hello 服務的 hello 能力 tooconfigure 限制委派。 如此一來，hello 後端服務系統管理員可以允許或拒絕前端服務。 此模型稱為「資源型 Kerberos 限制委派」。

資源型 KCD 是使用 PowerShell 所設定的。 您可以使用 hello Set-adcomputer 或 Set-aduser cmdlet，根據 hello 模擬帳戶是電腦帳戶或使用者帳戶/服務帳戶。

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>為受管理的網域上的電腦帳戶設定資源型 KCD
假設您擁有 hello 電腦上執行的 web 應用程式 ' contoso100-webapp.contoso100.com'。 它需要 tooaccess hello 資源 (web API 上執行 ' contoso100-api.contoso100.com') 的網域使用者的 hello 內容中。 以下是針對此案例設定資源型 KCD 的方式。

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>為受管理的網域上的使用者帳戶設定資源型 KCD
假設您有 web 應用程式執行為服務帳戶 'appsvc' 以及它 hello 網域使用者內容中需要 tooaccess hello 資源 (web API 執行為服務帳戶-'backendsvc')。 以下是針對此案例設定資源型 KCD 的方式。

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [Kerberos 限制委派概觀](https://technet.microsoft.com/library/jj553400.aspx)
