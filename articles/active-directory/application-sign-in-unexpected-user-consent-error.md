---
title: "aaa 未預期的錯誤時執行的應用程式同意 tooan |Microsoft 文件"
description: "討論在 hello 同意 tooan 應用程式和您可以執行這些程序期間可能發生的錯誤"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>執行同意 tooan 應用程式時發生非預期的錯誤

這篇文章討論 hello 同意 tooan 應用程式的程序期間可能發生的錯誤。 如果您正在疑難排解未包含任何錯誤訊息的非預期同意提示，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)。

許多與 Azure Active Directory 整合的應用程式需要的權限 tooaccess toofunction 順序中的其他資源。 當這些資源也會與 Azure Active Directory 整合時，它們通常要求使用 hello 常見的權限 tooaccess 同意架構。 

這會導致同意提示顯示，這通常就會發生 hello 第一次使用應用程式，但也會發生在 hello 應用程式的後續使用。

某些條件必須為應用程式需要使用者 tooconsent toohello 權限，則為 true。 如果不符合這些條件，便會發生各種錯誤。 其中包含：

## <a name="requesting-not-authorized-permissions-error"></a>要求未經授權權限的錯誤
* **AADSTS90093:** &lt;clientAppDisplayName&gt;不是您的一個或多個權限授權 toogrant 要求。 請連絡的系統管理員可以同意 toothis 代表您的應用程式。

不是公司系統管理員的使用者嘗試 toouse 要求只有系統管理員可以授與的權限的應用程式時，就會發生此錯誤。 授與存取 toohello 應用程式，代表其組織的系統管理員，可以解決這個錯誤。

## <a name="policy-prevents-granting-permissions-error"></a>原則禁止授與權限錯誤
* **AADSTS90093:**的系統管理員&lt;tenantDisplayName&gt;已經設定原則，使您無法授與&lt;的應用程式名稱&gt;hello 對於要求的權限。 請連絡系統管理員&lt;tenantDisplayName&gt;，使用者可以授與權限 toothis 應用程式代表您。

發生此錯誤時公司系統管理員會關閉使用者 tooconsent tooapplications，hello 能力則非系統管理員使用者嘗試 toouse 需要同意的應用程式。 授與存取 toohello 應用程式，代表其組織的系統管理員，可以解決這個錯誤。

## <a name="intermittent-problem-error"></a>間歇性問題錯誤
* **AADSTS90090:**我們遇到錄製您太嘗試 toogrant hello 權限的間歇性問題似乎&lt;clientAppDisplayName&gt;。 請稍後再試一次。

此錯誤表示已發生間歇性服務端問題。 它可以解決方法是嘗試再次 tooconsent toohello 應用程式。

## <a name="resource-not-available-error"></a>資源無法使用錯誤
* **AADSTS65005:** hello 應用程式&lt;clientAppDisplayName&gt;要求資源的權限 tooaccess &lt;resourceAppDisplayName&gt;未提供的。 

請連絡 hello 應用程式開發人員。

##  <a name="resource-not-available-in-tenant-error"></a>資源在租用戶無法使用錯誤
* **AADSTS65005:** &lt;clientAppDisplayName&gt;要求存取 tooa 資源&lt;resourceAppDisplayName&gt;未提供您組織中的&lt;tenantDisplayName&gt;。 

請確認此資源可以使用，或與 &lt;tenantDisplayName&gt; 的系統管理員連絡。

## <a name="permissions-mismatch-error"></a>權限不符合錯誤
* **AADSTS65005:** hello 應用程式要求的同意 tooaccess 資源&lt;resourceAppDisplayName&gt;。 此要求失敗，因為它不符合如何 hello 應用程式已預先設定的應用程式登錄期間。 請連絡 hello 應用程式 vendor.* *

Hello 應用程式的使用者嘗試 tooconsent toois 要求權限 tooaccess hello 組織的目錄 （租用戶） 中找不到資源應用程式時，就會發生所有這些錯誤。 發生的原因有數種：

-   hello 用戶端應用程式開發人員已將設定其應用程式不正確，造成它 toorequest 存取 tooan 無效的資源。 在此情況下，hello 應用程式開發人員就必須更新 hello 組態的 hello 用戶端應用程式 tooresolve 此問題。

-   服務主體代表 hello 目標資源應用程式不存在於 hello 組織或存在於過去 hello 但已被移除。 這個問題，請將服務主體的 hello 資源應用程式中必須提供 hello 組織讓 hello 用戶端應用程式可以要求權限 tooit tooresolve。 這可能會發生數種方式，取決於 hello 類型的應用程式，包括：

    -   取得訂用帳戶的 hello 資源應用程式 （Microsoft 所發行的應用程式）

    -   同意 toohello 資源應用程式

    -   授與 hello 透過 hello Azure 入口網站的應用程式權限

    -   從 hello Azure AD 應用程式庫加入 hello 應用程式

## <a name="next-steps"></a>後續步驟 

[Azure Active Directory 中的應用程式、權限及同意 (v1 端點)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[範圍、 權限，以及在 hello Azure Active Directory （v2.0 端點） 中同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


