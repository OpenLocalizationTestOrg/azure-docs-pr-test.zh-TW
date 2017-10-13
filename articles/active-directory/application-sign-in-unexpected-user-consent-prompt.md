---
title: "登入應用程式時看到非預期的同意提示 | Microsoft Docs"
description: "如何疑難排解使用者會看到已與 Azure AD 整合的應用程式顯示您未預期的同意提示"
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a>登入應用程式時看到非預期的同意提示

許多與 Azure Active Directory 整合的應用程式需要各種資源的權限，才能執行。 當這些資源也與 Azure Active Directory 整合時，會使用 Azure AD 同意架構來要求存取這些資源的權限。 

這會導致當第一次使用應用程式會一直顯示同意提示，但這通常只應顯示一次。 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>使用者會看到同意提示的案例

還有其他提示預期會在各種案例中發生：

* 應用程式需要的權限集已變更。

* 原本同意應用程式的使用者不是系統管理員，且現在有不同的使用者 (非系統管理員) 正首次使用應用程式。

* 原本同意應用程式的使用者為系統管理員，但他們未代表整個組織同意。

* 在初步獲得同意後，應用程式正在使用 [增量和動態同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent)要求其他權限。 這通常用於當應用程式的選擇性功能額外需要基礎功能所需權限以外的權限時。

* 在初步獲得同意後，同意遭到撤銷。

* 開發人員已設定應用程式在每次使用時都需要同意提示 (注意：這不是最佳做法)。

## <a name="next-steps"></a>後續步驟

-   [Azure Active Directory 中的應用程式、權限及同意 (v1.0 端點)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Azure Active Directory v2.0 端點中的範圍、權限及同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


