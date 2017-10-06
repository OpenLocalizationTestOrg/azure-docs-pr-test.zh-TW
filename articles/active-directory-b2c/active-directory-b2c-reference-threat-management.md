---
title: "Azure Active Directory B2C：威脅管理 | Microsoft Docs"
description: "了解 Azure Active Directory B2C 中針對拒絕服務攻擊和密碼攻擊的偵測和風險降低技術。"
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C：威脅管理

威脅管理包括規劃保護系統和網路，避免遭受攻擊。 阻絕服務攻擊可能會讓資源無法使用 toointended 使用者。 密碼攻擊負責人 toounauthorized 存取 tooresources。 Azure Active Directory B2C (Azure AD B2C) 具備內建功能，可協助您透過多種方式保護您的資料，避免遭受威脅。

## <a name="denial-of-service-attacks"></a>拒絕服務的攻擊

Azure AD B2C 會使用偵測與補救技術，如 SYN cookie 和速率和連線限制 tooprotect 基礎的資源受到阻絕服務攻擊。

## <a name="password-attacks"></a>密碼攻擊

Azure AD B2C 也備有降低風險的技術，可防範密碼攻擊。 風險降低包括暴力密碼破解攻擊和字典密碼破解攻擊。 由使用者所設定的密碼是必要的 toobe 相當複雜。 藉由使用不同的訊號，Azure AD B2C 會分析 hello 完整性的要求。 Azure AD B2C 旨在 toointelligently 免於駭客和防治中心區分預定的使用者。 Azure AD B2C 提供複雜的策略 toolock 基礎進入攻擊的 hello 可能性 hello 密碼的帳戶。

如需詳細資訊，請瀏覽 hello [Microsoft 信任中心](https://www.microsoft.com/trustcenter/security/threatmanagement)。
