---
title: "Azure AD Connect：傳遞驗證 - 目前的限制 | Microsoft Docs"
description: "本文說明 hello 目前限制的 Azure Active Directory (Azure AD) 的傳遞驗證。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Azure Active Directory 傳遞驗證：目前的限制

>[!IMPORTANT]
>Azure AD 傳遞驗證目前為預覽功能。 這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。 傳遞驗證僅供以 hello 全球執行個體的 Azure AD 中，而不是在[Microsoft 雲端德國](http://www.microsoft.de/cloud-deutschland)和[Microsoft Azure 政府雲端](https://azure.microsoft.com/features/gov/)。

## <a name="supported-scenarios"></a>支援的案例

在預覽期間完全支援下列案例的 hello:

- 使用者登入所有網頁瀏覽器應用程式。
- 使用者登入支援[新式驗證](https://aka.ms/modernauthga)的 Office 365 用戶端應用程式。
- 適用於 Windows 10 裝置的 Azure AD Join。
- Exchange ActiveSync 支援。

## <a name="unsupported-scenarios"></a>不支援的情節

hello 案例如下_不_支援在預覽期間：

- 使用者登入舊版 Office 用戶端應用程式c (Office 2013 或更早版本)。 組織可能的話會鼓勵的 tooswitch toomodern 驗證。 新式驗證提供傳遞驗證支援，但也可使用 Multi-Factor Authentication (MFA) 等[條件式存取](../active-directory-conditional-access.md)功能，協助您保護使用者帳戶。
- 使用者登入商務用 Skype 用戶端應用程式，包括商務用 Skype 2016。
- 使用者登入 PowerShell 1.0 版。 建議您改為使用 PowerShell 2.0 版。

>[!IMPORTANT]
>不支援的案例的因應措施，以啟用密碼雜湊同步處理在 hello[選用功能](active-directory-aadconnect-get-started-custom.md#optional-features)hello Azure AD Connect 精靈 頁面。 密碼雜湊同步處理做為後援 hello 上述案例_只_(和_不_做為泛型後援 tooPass 透過驗證)。 如果您不需要這些情節，請關閉 [密碼雜湊同步處理]。

## <a name="next-steps"></a>後續步驟
- [**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。
- [**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。
- [**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
