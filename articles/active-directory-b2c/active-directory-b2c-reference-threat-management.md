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
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="1ab07-103">Azure Active Directory B2C：威脅管理</span><span class="sxs-lookup"><span data-stu-id="1ab07-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="1ab07-104">威脅管理包括規劃保護系統和網路，避免遭受攻擊。</span><span class="sxs-lookup"><span data-stu-id="1ab07-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="1ab07-105">拒絕服務的攻擊可能會造成預定使用者無法使用資源。</span><span class="sxs-lookup"><span data-stu-id="1ab07-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="1ab07-106">密碼攻擊可導致未經授權的資源存取。</span><span class="sxs-lookup"><span data-stu-id="1ab07-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="1ab07-107">Azure Active Directory B2C (Azure AD B2C) 具備內建功能，可協助您透過多種方式保護您的資料，避免遭受威脅。</span><span class="sxs-lookup"><span data-stu-id="1ab07-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="1ab07-108">拒絕服務的攻擊</span><span class="sxs-lookup"><span data-stu-id="1ab07-108">Denial-of-service attacks</span></span>

<span data-ttu-id="1ab07-109">Azure AD B2C 使用偵測和降低風險的技術 (例如 SYN Cookie) 及速率和連線限制來保護基礎資源，避免遭受拒絕服務的攻擊。</span><span class="sxs-lookup"><span data-stu-id="1ab07-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="1ab07-110">密碼攻擊</span><span class="sxs-lookup"><span data-stu-id="1ab07-110">Password attacks</span></span>

<span data-ttu-id="1ab07-111">Azure AD B2C 也備有降低風險的技術，可防範密碼攻擊。</span><span class="sxs-lookup"><span data-stu-id="1ab07-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="1ab07-112">風險降低包括暴力密碼破解攻擊和字典密碼破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="1ab07-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="1ab07-113">使用者所設定的密碼必須達到適當的複雜性。</span><span class="sxs-lookup"><span data-stu-id="1ab07-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="1ab07-114">Azure AD B2C 會利用不同的訊號來分析要求的完整性。</span><span class="sxs-lookup"><span data-stu-id="1ab07-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="1ab07-115">Azure AD B2C 的設計會很聰明地區分預定使用者與駭客和殭屍網路。</span><span class="sxs-lookup"><span data-stu-id="1ab07-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="1ab07-116">Azure AD B2C 提供很精密的策略，在可能遭受攻擊時，可根據輸入的密碼來鎖定帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ab07-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="1ab07-117">如需詳細資訊，請瀏覽 [Microsoft 信任中心](https://www.microsoft.com/trustcenter/security/threatmanagement)。</span><span class="sxs-lookup"><span data-stu-id="1ab07-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
