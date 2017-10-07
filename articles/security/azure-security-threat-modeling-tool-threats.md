---
title: "aaaThreats-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
description: "威脅 [類別目錄] 頁面上，hello Microsoft 威脅模型化工具，包含所有公開的類別產生的威脅。"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a><span data-ttu-id="9dce5-103">Microsoft 威脅模型化工具威脅</span><span class="sxs-lookup"><span data-stu-id="9dce5-103">Microsoft Threat Modeling Tool threats</span></span>

<span data-ttu-id="9dce5-104">hello 威脅模型化工具是 Microsoft 安全性開發週期 (SDL) hello 的核心項目。</span><span class="sxs-lookup"><span data-stu-id="9dce5-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="9dce5-105">它可讓軟體架構設計人員 tooidentify 和時，它們相當容易、 更符合成本效益 tooresolve 早期減輕潛在的安全性問題。</span><span class="sxs-lookup"><span data-stu-id="9dce5-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="9dce5-106">如此一來，它可大幅減少開發 hello 總成本。</span><span class="sxs-lookup"><span data-stu-id="9dce5-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="9dce5-107">此外，我們會與非安全性專家納入考量，方便威脅分析模型的所有開發人員藉由提供清楚的指引，建立和分析威脅模型設計 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="9dce5-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span>

> <span data-ttu-id="9dce5-108">請瀏覽 hello **[威脅模型化工具](./azure-security-threat-modeling-tool.md)** tooget 立即開始使用 ！</span><span class="sxs-lookup"><span data-stu-id="9dce5-108">Visit hello **[Threat Modeling Tool](./azure-security-threat-modeling-tool.md)** tooget started today!</span></span>

<span data-ttu-id="9dce5-109">hello 威脅模型化工具可協助您回答某些問題，例如 hello 下面項目：</span><span class="sxs-lookup"><span data-stu-id="9dce5-109">hello Threat Modeling Tool helps you answer certain questions, such as hello ones below:</span></span>

* <span data-ttu-id="9dce5-110">攻擊者可以如何變更 hello 驗證資料？</span><span class="sxs-lookup"><span data-stu-id="9dce5-110">How can an attacker change hello authentication data?</span></span>
* <span data-ttu-id="9dce5-111">什麼是 hello 影響，如果攻擊者可以讀取 hello 使用者設定檔資料？</span><span class="sxs-lookup"><span data-stu-id="9dce5-111">What is hello impact if an attacker can read hello user profile data?</span></span>
* <span data-ttu-id="9dce5-112">如果 toohello 使用者設定檔資料庫拒絕存取會怎樣？</span><span class="sxs-lookup"><span data-stu-id="9dce5-112">What happens if access is denied toohello user profile database?</span></span>

## <a name="stride-model"></a><span data-ttu-id="9dce5-113">STRIDE 模型</span><span class="sxs-lookup"><span data-stu-id="9dce5-113">STRIDE model</span></span>

<span data-ttu-id="9dce5-114">toobetter 協助您制定這幾種指標的問題，Microsoft 會使用 hello STRIDE 模型來分類不同類型的威脅，並簡化 hello 整體安全性的交談。</span><span class="sxs-lookup"><span data-stu-id="9dce5-114">toobetter help you formulate these kinds of pointed questions, Microsoft uses hello STRIDE model, which categorizes different types of threats and simplifies hello overall security conversations.</span></span>

| <span data-ttu-id="9dce5-115">類別</span><span class="sxs-lookup"><span data-stu-id="9dce5-115">Category</span></span> | <span data-ttu-id="9dce5-116">說明</span><span class="sxs-lookup"><span data-stu-id="9dce5-116">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="9dce5-117">**詐騙**</span><span class="sxs-lookup"><span data-stu-id="9dce5-117">**Spoofing**</span></span> | <span data-ttu-id="9dce5-118">涉及非法存取然後使用其他使用者的驗證資訊，例如使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="9dce5-118">Involves illegally accessing and then using another user's authentication information, such as username and password</span></span> |
| <span data-ttu-id="9dce5-119">**竄改**</span><span class="sxs-lookup"><span data-stu-id="9dce5-119">**Tampering**</span></span> | <span data-ttu-id="9dce5-120">牽涉到 hello 惡意修改資料。</span><span class="sxs-lookup"><span data-stu-id="9dce5-120">Involves hello malicious modification of data.</span></span> <span data-ttu-id="9dce5-121">範例包括未經授權的變更 toopersistent 資料，例如開啟網路，例如 hello 網際網路上的兩部電腦之間流動時加以保留在資料庫和 hello 改變的資料</span><span class="sxs-lookup"><span data-stu-id="9dce5-121">Examples include unauthorized changes made toopersistent data, such as that held in a database, and hello alteration of data as it flows between two computers over an open network, such as hello Internet</span></span> |
| <span data-ttu-id="9dce5-122">**否認性**</span><span class="sxs-lookup"><span data-stu-id="9dce5-122">**Repudiation**</span></span> | <span data-ttu-id="9dce5-123">拒絕執行動作，而不需要任何方式 tooprove 否則其他合作對象的使用者相關聯 — 例如，使用者會執行不合法的操作缺少 hello 能力 tootrace hello 禁止作業的系統。</span><span class="sxs-lookup"><span data-stu-id="9dce5-123">Associated with users who deny performing an action without other parties having any way tooprove otherwise—for example, a user performs an illegal operation in a system that lacks hello ability tootrace hello prohibited operations.</span></span> <span data-ttu-id="9dce5-124">不可否認性是指系統 toocounter 不可否認性威脅 toohello 能力。</span><span class="sxs-lookup"><span data-stu-id="9dce5-124">Non-Repudiation refers toohello ability of a system toocounter repudiation threats.</span></span> <span data-ttu-id="9dce5-125">例如，使用者購買項目可能 toosign 收到 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="9dce5-125">For example, a user who purchases an item might have toosign for hello item upon receipt.</span></span> <span data-ttu-id="9dce5-126">hello 廠商可以接著使用 hello 做為該 hello 使用者未收到 hello 套件的辨識項簽署回條</span><span class="sxs-lookup"><span data-stu-id="9dce5-126">hello vendor can then use hello signed receipt as evidence that hello user did receive hello package</span></span> |
| <span data-ttu-id="9dce5-127">**資訊洩漏**</span><span class="sxs-lookup"><span data-stu-id="9dce5-127">**Information Disclosure**</span></span> | <span data-ttu-id="9dce5-128">牽涉到 hello 暴露資訊 tooindividuals 洩露 toohave 存取 tooit — 比方說，使用者 tooread 它們未檔案 hello 能力授與存取權，或 hello 入侵者 tooread 傳輸中資料的兩部電腦之間的功能</span><span class="sxs-lookup"><span data-stu-id="9dce5-128">Involves hello exposure of information tooindividuals who are not supposed toohave access tooit—for example, hello ability of users tooread a file that they were not granted access to, or hello ability of an intruder tooread data in transit between two computers</span></span> |
| <span data-ttu-id="9dce5-129">**阻斷服務**</span><span class="sxs-lookup"><span data-stu-id="9dce5-129">**Denial of Service**</span></span> | <span data-ttu-id="9dce5-130">阻絕服務 (DoS) 攻擊拒絕服務 toovalid 使用者 — 例如，藉由網頁伺服器暫時無法使用或無法使用。</span><span class="sxs-lookup"><span data-stu-id="9dce5-130">Denial of service (DoS) attacks deny service toovalid users—for example, by making a Web server temporarily unavailable or unusable.</span></span> <span data-ttu-id="9dce5-131">您必須防止某些類型的 DoS 威脅只要 tooimprove 系統可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="9dce5-131">You must protect against certain types of DoS threats simply tooimprove system availability and reliability</span></span> |
| <span data-ttu-id="9dce5-132">**權限提高**</span><span class="sxs-lookup"><span data-stu-id="9dce5-132">**Elevation of Privilege**</span></span> | <span data-ttu-id="9dce5-133">無特殊權限的使用者取得授權的存取，並藉此有足夠的存取 toocompromise 或損毀 hello 整個系統。</span><span class="sxs-lookup"><span data-stu-id="9dce5-133">An unprivileged user gains privileged access and thereby has sufficient access toocompromise or destroy hello entire system.</span></span> <span data-ttu-id="9dce5-134">提高權限威脅包括這些情況，攻擊者具有有效地滲入所有系統防禦，以及會成為受信任的 hello 系統本身，危險的狀況，以確實的一部分</span><span class="sxs-lookup"><span data-stu-id="9dce5-134">Elevation of privilege threats include those situations in which an attacker has effectively penetrated all system defenses and become part of hello trusted system itself, a dangerous situation indeed</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9dce5-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dce5-135">Next steps</span></span>

<span data-ttu-id="9dce5-136">繼續太**[威脅模型化工具降低](./azure-security-threat-modeling-tool-mitigations.md)** toolearn hello 不同的方式可以減輕這些威脅與 Azure。</span><span class="sxs-lookup"><span data-stu-id="9dce5-136">Proceed too**[Threat Modeling Tool Mitigations](./azure-security-threat-modeling-tool-mitigations.md)** toolearn hello different ways you can mitigate these threats with Azure.</span></span>
