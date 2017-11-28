---
title: "aaaAzure Active Directory 混合式身分識別設計考量的後續步驟 |Microsoft 文件"
description: "概要和接下來的步驟之後，您已閱讀 hello 混合式身分識別設計考量指南"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 02d48768-ea9e-4bfe-ae54-b54c4bd0a789
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7100eaaf61a7b3b7d38a381f6bb9d8b82677c352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations--next-steps"></a><span data-ttu-id="34a80-103">Azure Active Directory 混合式身分識別設計考量 - 後續步驟</span><span class="sxs-lookup"><span data-stu-id="34a80-103">Azure Active Directory hybrid identity design considerations- next steps</span></span>
<span data-ttu-id="34a80-104">現在您已經完成定義您的需求和檢查您的行動裝置管理解決方案的所有 hello 選項，您已準備好 tootake hello 接下來的步驟部署支援最適合您和貴組織的基礎結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="34a80-104">Now that you’ve completed defining your requirements and examining all hello options for your mobile device management solution, you’re ready tootake hello next steps for deploying hello supporting infrastructure that’s right for you and your organization.</span></span>

## <a name="hybrid-identity-solutions"></a><span data-ttu-id="34a80-105">混合式身分識別解決方案</span><span class="sxs-lookup"><span data-stu-id="34a80-105">Hybrid identity solutions</span></span>
<span data-ttu-id="34a80-106">-運用符合您需求的特定解決方案案例是很好的方法 tooreview 和 hello 部署詳細資料的行動裝置管理基礎結構規劃。</span><span class="sxs-lookup"><span data-stu-id="34a80-106">-Leveraging specific solution scenarios that fit your needs is a great way tooreview and plan for hello details of deploying a mobile device management infrastructure.</span></span> <span data-ttu-id="34a80-107">hello 下列解決方案概述幾個 hello 最常見的行動裝置管理案例：</span><span class="sxs-lookup"><span data-stu-id="34a80-107">hello following solutions outline several of hello most common mobile device management scenarios:</span></span>

* <span data-ttu-id="34a80-108">hello[環境的企業解決方案中管理行動裝置和電腦](https://technet.microsoft.com/library/dn582037.aspx)有助於您在內部部署 System Center 2012 Configuration Manager 基礎結構延伸至 hello 與 Microsoft 的雲端管理行動裝置Intune。</span><span class="sxs-lookup"><span data-stu-id="34a80-108">hello [manage mobile devices and PCs in enterprise environments solution](https://technet.microsoft.com/library/dn582037.aspx) helps you manage mobile devices by extending your on-premises System Center 2012 Configuration Manager infrastructure into hello cloud with Microsoft Intune.</span></span> <span data-ttu-id="34a80-109">這個混合式基礎結構可以協助中大型環境的 IT 專業人員啟用 BYOD 及遠端存取，同時降低系統管理的複雜度。</span><span class="sxs-lookup"><span data-stu-id="34a80-109">This hybrid infrastructure helps IT Pros in medium and large environments enable BYOD and remote access while reducing administrative complexity.</span></span>
* <span data-ttu-id="34a80-110">hello[管理行動裝置 Configuration Manager 2007 解決方案](https://technet.microsoft.com/library/dn508400.aspx)可協助您管理行動裝置，當您的基礎結構建置在 System Center Configuration Manager 2007。</span><span class="sxs-lookup"><span data-stu-id="34a80-110">hello [managing mobile devices for Configuration Manager 2007 solution](https://technet.microsoft.com/library/dn508400.aspx) helps you manage mobile devices when your infrastructure rests on a System Center Configuration Manager 2007.</span></span> <span data-ttu-id="34a80-111">此解決方案會說明如何執行 System Center 2012 Configuration Manager，讓您可以執行 Microsoft Intune 並利用其 MDM 能力的單一伺服器向上 tooset。</span><span class="sxs-lookup"><span data-stu-id="34a80-111">This solution shows you how tooset up a single server running System Center 2012 Configuration Manager so you can then run Microsoft Intune and take advantage of its MDM ability.</span></span>
* <span data-ttu-id="34a80-112">hello[管理小型環境方案中的行動裝置](https://technet.microsoft.com/library/dn715906.aspx)適用於需要 toosupport MDM 的小型企業</span><span class="sxs-lookup"><span data-stu-id="34a80-112">hello [managing mobile devices in small environments solution](https://technet.microsoft.com/library/dn715906.aspx) is intended for small businesses that need toosupport MDM.</span></span> <span data-ttu-id="34a80-113">它會說明如何 toouse Microsoft Intune tooextend 您目前基礎結構 toosupport 行動裝置管理與 BYOD。</span><span class="sxs-lookup"><span data-stu-id="34a80-113">It explains how toouse Microsoft Intune tooextend your current infrastructure toosupport mobile device management and BYOD.</span></span> <span data-ttu-id="34a80-114">此解決方案說明在獨立、 沒有本機伺服器的僅限雲端設定中使用 Microsoft Intune 支援的 hello 最簡單案例。</span><span class="sxs-lookup"><span data-stu-id="34a80-114">This solution describes hello simplest scenario supported for using Microsoft Intune in a standalone, cloud-only configuration with no local servers.</span></span>

## <a name="hybrid-identity-documentation"></a><span data-ttu-id="34a80-115">混合式身分識別文件</span><span class="sxs-lookup"><span data-stu-id="34a80-115">Hybrid identity documentation</span></span>
<span data-ttu-id="34a80-116">在實作行動裝置管理解決方案時，概念性和程序性規劃、部署及系統管理內容是非常實用的：</span><span class="sxs-lookup"><span data-stu-id="34a80-116">Conceptual and procedural planning, deployment, and administration content are useful when implementing your mobile device management solution:</span></span>

* <span data-ttu-id="34a80-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) 解決方案可協助您擷取和彙總有關基礎結構、原則、程序及最佳做法的知識，讓您的 IT 人員能夠建置可管理的系統和自動化作業。</span><span class="sxs-lookup"><span data-stu-id="34a80-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) solutions can help you capture and aggregate knowledge about your infrastructure, policies, processes, and best practices so that your IT staff can build manageable systems and automate operations.</span></span>
* <span data-ttu-id="34a80-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx)是雲端式裝置管理服務，可協助您 toomanage，您的電腦和行動裝置和 toosecure 貴公司的資訊。</span><span class="sxs-lookup"><span data-stu-id="34a80-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) is a cloud-based device management service that helps you toomanage your computers and mobile devices and toosecure your company’s information.</span></span>
* <span data-ttu-id="34a80-119">[MDM for Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx)讓您 toomanage 以及保護行動裝置連線的 tooyour Office 365 組織時。</span><span class="sxs-lookup"><span data-stu-id="34a80-119">[MDM for Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) allows you toomanage and secure mobile devices when they're connected tooyour Office 365 organization.</span></span> <span data-ttu-id="34a80-120">如果遺失或遭竊時，您可以使用 MDM for Office 365 tooset 裝置安全性原則和存取規則和 toowipe 行動裝置。</span><span class="sxs-lookup"><span data-stu-id="34a80-120">You can use MDM for Office 365 tooset device security policies and access rules, and toowipe mobile devices if they’re lost or stolen.</span></span>

## <a name="hybrid-identity-resources"></a><span data-ttu-id="34a80-121">混合式身分識別資源</span><span class="sxs-lookup"><span data-stu-id="34a80-121">Hybrid identity resources</span></span>
<span data-ttu-id="34a80-122">監視 hello 下列資源通常提供 hello 最新消息和更新行動裝置管理解決方案：</span><span class="sxs-lookup"><span data-stu-id="34a80-122">Monitoring hello following resources often provides hello latest news and updates on mobile device management solutions:</span></span>

* [<span data-ttu-id="34a80-123">Microsoft Enterprise Mobility 部落格</span><span class="sxs-lookup"><span data-stu-id="34a80-123">Microsoft Enterprise Mobility blog</span></span>](http://blogs.technet.com/b/enterprisemobility/)
* [<span data-ttu-id="34a80-124">Microsoft 在 hello 雲端部落格</span><span class="sxs-lookup"><span data-stu-id="34a80-124">Microsoft In hello Cloud blog</span></span>](http://blogs.technet.com/b/in_the_cloud/)
* [<span data-ttu-id="34a80-125">Microsoft Intune 部落格</span><span class="sxs-lookup"><span data-stu-id="34a80-125">Microsoft Intune blog</span></span>](http://blogs.technet.com/b/microsoftintune/)
* [<span data-ttu-id="34a80-126">Microsoft System Center Configuration Manager 部落格</span><span class="sxs-lookup"><span data-stu-id="34a80-126">Microsoft System Center Configuration Manager blog</span></span>](http://blogs.technet.com/b/configurationmgr/)
* [<span data-ttu-id="34a80-127">Microsoft System Center Configuration Manager Team 部落格</span><span class="sxs-lookup"><span data-stu-id="34a80-127">Microsoft System Center Configuration Manager Team blog</span></span>](http://blogs.technet.com/b/configmgrteam/)

## <a name="see-also"></a><span data-ttu-id="34a80-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="34a80-128">See also</span></span>
[<span data-ttu-id="34a80-129">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="34a80-129">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

