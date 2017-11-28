---
title: "在 Microsoft Azure 中的個人資料 aaaProtect |Microsoft 文件"
description: "第一次發行項在一系列的文章 toohelp 您使用 Azure tooprotect 個人資料"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="fc5cd-103">在 Microsoft Azure 中保護個人資料</span><span class="sxs-lookup"><span data-stu-id="fc5cd-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="fc5cd-104">本文介紹一系列的文章，協助您使用 Azure 的安全性技術和服務 tooprotect 個人資料。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="fc5cd-105">這是許多公司和業界合規性和治理計劃的重要需求。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="fc5cd-106">hello 案例、 問題陳述式和公司目標會包含在此處。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="fc5cd-107">案例與問題陳述</span><span class="sxs-lookup"><span data-stu-id="fc5cd-107">Scenario and problem statement</span></span>

<span data-ttu-id="fc5cd-108">大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="fc5cd-109">toosupport 努力，它所取得數個較小的出航行位於義大利，德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="fc5cd-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="fc5cd-110">hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="fc5cd-111">這可能包括員工及/或客戶資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="fc5cd-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="fc5cd-112">地址</span><span class="sxs-lookup"><span data-stu-id="fc5cd-112">addresses</span></span>
- <span data-ttu-id="fc5cd-113">電話號碼</span><span class="sxs-lookup"><span data-stu-id="fc5cd-113">phone numbers</span></span>
- <span data-ttu-id="fc5cd-114">稅務識別編號</span><span class="sxs-lookup"><span data-stu-id="fc5cd-114">tax identification numbers</span></span>
- <span data-ttu-id="fc5cd-115">醫療資訊</span><span class="sxs-lookup"><span data-stu-id="fc5cd-115">medical information</span></span>
- <span data-ttu-id="fc5cd-116">信用卡資訊</span><span class="sxs-lookup"><span data-stu-id="fc5cd-116">credit card information</span></span>

<span data-ttu-id="fc5cd-117">hello 公司必須保護員工和客戶資料的 hello 的隱私權，同時進行資料存取 toothose 部門需要它。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="fc5cd-118">(例如薪資部門和訂位部門) 可以存取資料。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="fc5cd-119">公司目標</span><span class="sxs-lookup"><span data-stu-id="fc5cd-119">Company goals</span></span> 

- <span data-ttu-id="fc5cd-120">當包含個人資料的資料來源位於雲端儲存體時，會加密此資料來源。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="fc5cd-121">從一個位置 tooanother 轉送的個人資料會加密傳輸中時。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="fc5cd-122">這是 true hello 資料搭乘 hello 虛擬網路或網際網路 hello 跨越 hello 公司資料中心之間 hello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="fc5cd-123">透過增強式身分識別管理與存取控制技術，來防止個人資料的機密性和完整性遭到未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="fc5cd-124">透過監控弱點和威脅，來防止攻擊者利用資料缺口公開個人資料。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="fc5cd-125">hello 儲存或傳輸個人資料的 Azure 服務的安全性狀態來評估 tooidentify 機會 toobetter 保護個人資料。</span><span class="sxs-lookup"><span data-stu-id="fc5cd-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="fc5cd-126">資料保護指引</span><span class="sxs-lookup"><span data-stu-id="fc5cd-126">Data protection guidance</span></span>

<span data-ttu-id="fc5cd-127">hello 下列文章包含技術的方式 tooguidance 可協助您達到 hello 個人資料的保護目標上面所列：</span><span class="sxs-lookup"><span data-stu-id="fc5cd-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="fc5cd-128">Azure 加密技術</span><span class="sxs-lookup"><span data-stu-id="fc5cd-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="fc5cd-129">Azure 加密技術</span><span class="sxs-lookup"><span data-stu-id="fc5cd-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="fc5cd-130">Azure 身分識別與存取技術</span><span class="sxs-lookup"><span data-stu-id="fc5cd-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="fc5cd-131">Azure 網路安全性技術</span><span class="sxs-lookup"><span data-stu-id="fc5cd-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="fc5cd-132">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="fc5cd-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="fc5cd-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc5cd-133">Next steps</span></span>

- [<span data-ttu-id="fc5cd-134">Azure 安全性資訊網站</span><span class="sxs-lookup"><span data-stu-id="fc5cd-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="fc5cd-135">Microsoft 信任中心</span><span class="sxs-lookup"><span data-stu-id="fc5cd-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="fc5cd-136">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="fc5cd-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="fc5cd-137">Azure 安全性小組部落格</span><span class="sxs-lookup"><span data-stu-id="fc5cd-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="fc5cd-138">Azure.com 部落格 - 安全性</span><span class="sxs-lookup"><span data-stu-id="fc5cd-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
