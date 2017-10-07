---
title: "aaaUnexpected 同意提示 tooan 應用程式在登入時 |Microsoft 文件"
description: "如何 tootroubleshoot 時使用者會看到同意提示應用程式已整合與您未預期的 Azure AD"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>未預期的同意提示時登入 tooan 應用程式

許多應用程式與 Azure Active Directory 整合需要在順序 toorun 的權限 toovarious 資源。 當這些資源也會與 Azure Active Directory 整合時，它們使用 hello Azure AD 來要求權限 tooaccess 同意架構。 

這會導致正在顯示 hello 第一次使用應用程式時，這通常是一次性的操作同意提示。 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>使用者會看到同意提示的案例

還有其他提示預期會在各種案例中發生：

* 已變更 hello hello 應用程式所需的權限集。

* hello，使用者最初同意 toohello 應用程式不是系統管理員，且現在不同的 （非系統管理員） 使用者使用 hello 應用程式的 hello 第一次。

* hello，使用者最初同意 toohello 應用程式就是系統管理員，但是他們未不同意上代表 hello 整個組織。

* hello 應用程式使用[增量和動態同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent)toorequest 其他權限，一開始授與同意之後。 這通常用於當應用程式的選擇性功能額外需要基礎功能所需權限以外的權限時。

* 在初步獲得同意後，同意遭到撤銷。

* hello 開發人員在每次使用時，已設定 hello 應用程式 toorequire 同意提示 (注意： 這不是最佳作法)。

## <a name="next-steps"></a>後續步驟

-   [Azure Active Directory 中的應用程式、權限及同意 (v1.0 端點)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [範圍、 權限，以及在 hello Azure Active Directory （v2.0 端點） 中同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


