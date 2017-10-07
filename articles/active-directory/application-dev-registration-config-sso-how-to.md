---
title: "aaaHow tooconfigure 新的多租用戶應用程式 |Microsoft 文件"
description: "如何 tooconfigure 單一登入功能的自訂應用程式中，您正在開發且登錄至 Azure AD。"
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a>如何 tooconfigure 新的多租用戶應用程式

在您的應用程式中啟用同盟單一登入 (SSO)，會在針對 OpenID Connect、SAML 2.0 或 WS-Fed 透過 Azure AD 進行同盟時自動啟用。 如果您的使用者有 toosign 儘管已有現有的工作階段與 Azure AD，很可能您的應用程式可能設定錯誤。

* 如果您使用 ADAL/MSAL，請確定您有**PromptBehavior**設定得**自動**而**永遠**。

* 如果您正在建置行動應用程式，您可能需要其他組態 tooenable 代理或非代理 SSO。

若是 Android，請參閱[在 Android 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)。<br>

若是 iOS，請參閱[在 iOS 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)。

## <a name="next-steps"></a>後續步驟

[Azure AD 的 SSO](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[在 Android 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[在 iOS 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[整合應用程式 tooAzureAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[適用於 AzureAD v2.0 交集應用程式的同意與權限](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow (英文)](http://stackoverflow.com/questions/tagged/azure-active-directory)
