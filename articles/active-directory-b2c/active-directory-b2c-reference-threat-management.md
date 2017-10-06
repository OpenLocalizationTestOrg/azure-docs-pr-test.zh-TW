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
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="9a228-103">Azure Active Directory B2C：威脅管理</span><span class="sxs-lookup"><span data-stu-id="9a228-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="9a228-104">威脅管理包括規劃保護系統和網路，避免遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="9a228-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="9a228-105">阻絕服務攻擊可能會讓資源無法使用 toointended 使用者。</span><span class="sxs-lookup"><span data-stu-id="9a228-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="9a228-106">密碼攻擊負責人 toounauthorized 存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="9a228-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="9a228-107">Azure Active Directory B2C (Azure AD B2C) 具備內建功能，可協助您透過多種方式保護您的資料，避免遭受威脅。</span><span class="sxs-lookup"><span data-stu-id="9a228-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="9a228-108">拒絕服務的攻擊</span><span class="sxs-lookup"><span data-stu-id="9a228-108">Denial-of-service attacks</span></span>

<span data-ttu-id="9a228-109">Azure AD B2C 會使用偵測與補救技術，如 SYN cookie 和速率和連線限制 tooprotect 基礎的資源受到阻絕服務攻擊。</span><span class="sxs-lookup"><span data-stu-id="9a228-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="9a228-110">密碼攻擊</span><span class="sxs-lookup"><span data-stu-id="9a228-110">Password attacks</span></span>

<span data-ttu-id="9a228-111">Azure AD B2C 也備有降低風險的技術，可防範密碼攻擊。</span><span class="sxs-lookup"><span data-stu-id="9a228-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="9a228-112">風險降低包括暴力密碼破解攻擊和字典密碼破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="9a228-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="9a228-113">由使用者所設定的密碼是必要的 toobe 相當複雜。</span><span class="sxs-lookup"><span data-stu-id="9a228-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="9a228-114">藉由使用不同的訊號，Azure AD B2C 會分析 hello 完整性的要求。</span><span class="sxs-lookup"><span data-stu-id="9a228-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="9a228-115">Azure AD B2C 旨在 toointelligently 免於駭客和防治中心區分預定的使用者。</span><span class="sxs-lookup"><span data-stu-id="9a228-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="9a228-116">Azure AD B2C 提供複雜的策略 toolock 基礎進入攻擊的 hello 可能性 hello 密碼的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9a228-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="9a228-117">如需詳細資訊，請瀏覽 hello [Microsoft 信任中心](https://www.microsoft.com/trustcenter/security/threatmanagement)。</span><span class="sxs-lookup"><span data-stu-id="9a228-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
