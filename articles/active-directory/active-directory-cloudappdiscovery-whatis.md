---
title: "不受管理的雲端應用程式使用 Cloud App Discovery aaaFinding |Microsoft 文件"
description: "提供有關尋找和管理應用程式，其中包含 Cloud App Discovery hello 優點為何，它的運作方式的資訊。"
services: active-directory
keywords: "雲端應用程式探索, 管理應用程式"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="63da0-104">使用 Cloud App Discovery 尋找未受管理的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="63da0-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="63da0-105">概觀</span><span class="sxs-lookup"><span data-stu-id="63da0-105">Overview</span></span>
<span data-ttu-id="63da0-106">現代企業 IT 部門通常不會察覺所有的 hello 雲端應用程式，其組織的成員使用 toodo 其工作。</span><span class="sxs-lookup"><span data-stu-id="63da0-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="63da0-107">它是簡單 toosee 為什麼系統管理員就必須考慮未經授權的存取 toocorporate 資料、 可能的資料流失和其他安全性風險。</span><span class="sxs-lookup"><span data-stu-id="63da0-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="63da0-108">缺乏認知可能使得要建立一個可應付這些安全性風險的計劃讓人卻步。</span><span class="sxs-lookup"><span data-stu-id="63da0-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="63da0-109">雲端應用程式探索是 Azure Active Directory (AD) Premium 可讓您組織中的 hello 人士使用 toodiscover 雲端應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="63da0-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="63da0-110">**使用 Cloud App Discovery，您可以：**</span><span class="sxs-lookup"><span data-stu-id="63da0-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="63da0-111">尋找所使用的 hello 雲端應用程式和使用者數目、 流量或 web 要求 toohello 應用程式的數目來測量使用量。</span><span class="sxs-lookup"><span data-stu-id="63da0-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="63da0-112">找出 hello 使用者使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="63da0-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="63da0-113">匯出資料以進行離線分析。</span><span class="sxs-lookup"><span data-stu-id="63da0-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="63da0-114">讓這些應用程式在 IT 的控制下並為使用者管理啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="63da0-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="63da0-115">運作方式</span><span class="sxs-lookup"><span data-stu-id="63da0-115">How it works</span></span>
1. <span data-ttu-id="63da0-116">應用程式使用代理程式會安裝在使用者的電腦上。</span><span class="sxs-lookup"><span data-stu-id="63da0-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="63da0-117">透過安全加密通道 toohello 雲端應用程式探索服務傳送 hello hello 代理程式所擷取的應用程式使用資訊。</span><span class="sxs-lookup"><span data-stu-id="63da0-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="63da0-118">hello Cloud App Discovery 服務評估 hello 資料，並產生報告。</span><span class="sxs-lookup"><span data-stu-id="63da0-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Cloud App Discovery 圖表](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="63da0-120">tooget 開始使用 Cloud App Discovery，請參閱[快速入門開始使用 Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="63da0-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="63da0-121">相關文章</span><span class="sxs-lookup"><span data-stu-id="63da0-121">Related articles</span></span>
* [<span data-ttu-id="63da0-122">Cloud App Discovery 的安全性和隱私權考量</span><span class="sxs-lookup"><span data-stu-id="63da0-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="63da0-123">Cloud App Discovery 群組原則部署指南</span><span class="sxs-lookup"><span data-stu-id="63da0-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="63da0-124">Cloud App Discovery System Center 部署指南</span><span class="sxs-lookup"><span data-stu-id="63da0-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="63da0-125">具有自訂連接埠的 Proxy 伺服器的 Cloud App Discovery 登錄設定</span><span class="sxs-lookup"><span data-stu-id="63da0-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="63da0-126">Cloud App Discovery 代理程式變更記錄 </span><span class="sxs-lookup"><span data-stu-id="63da0-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="63da0-127">Cloud App Discovery 常見問題集</span><span class="sxs-lookup"><span data-stu-id="63da0-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="63da0-128">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="63da0-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

