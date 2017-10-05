---
title: "Azure Active Directory 混合式身分識別設計考量 - 後續步驟| Microsoft Docs"
description: "在您讀過混合式身分識別設計考量指南之後的概要與後續步驟"
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
ms.openlocfilehash: 1d133430e0dcdcd0c24b44a2a7c452fbf16ecf29
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations--next-steps"></a><span data-ttu-id="c327f-103">Azure Active Directory 混合式身分識別設計考量 - 後續步驟</span><span class="sxs-lookup"><span data-stu-id="c327f-103">Azure Active Directory hybrid identity design considerations- next steps</span></span>
<span data-ttu-id="c327f-104">現在您已經完成定義需求以及檢查行動裝置管理解決方案的所有選項，您已準備好採取後續步驟，來部署最適合您和您的組織的支援基礎結構。</span><span class="sxs-lookup"><span data-stu-id="c327f-104">Now that you’ve completed defining your requirements and examining all the options for your mobile device management solution, you’re ready to take the next steps for deploying the supporting infrastructure that’s right for you and your organization.</span></span>

## <a name="hybrid-identity-solutions"></a><span data-ttu-id="c327f-105">混合式身分識別解決方案</span><span class="sxs-lookup"><span data-stu-id="c327f-105">Hybrid identity solutions</span></span>
<span data-ttu-id="c327f-106">-運用符合您需求的特定解決方案案例，是檢閱和規劃部署行動裝置管理基礎結構之詳細資料的好方法。</span><span class="sxs-lookup"><span data-stu-id="c327f-106">-Leveraging specific solution scenarios that fit your needs is a great way to review and plan for the details of deploying a mobile device management infrastructure.</span></span> <span data-ttu-id="c327f-107">下列解決方案概述數個最常見的行動裝置管理案例：</span><span class="sxs-lookup"><span data-stu-id="c327f-107">The following solutions outline several of the most common mobile device management scenarios:</span></span>

* <span data-ttu-id="c327f-108">[在企業環境解決方案中管理行動裝置和電腦](https://technet.microsoft.com/library/dn582037.aspx) 可協助您管理行動裝置，方法是使用 Microsoft Intune，將您的內部部署 System Center 2012 Configuration Manager 基礎結構擴充到雲端。</span><span class="sxs-lookup"><span data-stu-id="c327f-108">The [manage mobile devices and PCs in enterprise environments solution](https://technet.microsoft.com/library/dn582037.aspx) helps you manage mobile devices by extending your on-premises System Center 2012 Configuration Manager infrastructure into the cloud with Microsoft Intune.</span></span> <span data-ttu-id="c327f-109">這個混合式基礎結構可以協助中大型環境的 IT 專業人員啟用 BYOD 及遠端存取，同時降低系統管理的複雜度。</span><span class="sxs-lookup"><span data-stu-id="c327f-109">This hybrid infrastructure helps IT Pros in medium and large environments enable BYOD and remote access while reducing administrative complexity.</span></span>
* <span data-ttu-id="c327f-110">[管理適用於 Configuration Manager 2007 解決方案的行動裝置](https://technet.microsoft.com/library/dn508400.aspx) 可在您的基礎結構是以 System Center Configuration Manager 2007 為基礎時，協助管理行動裝置。</span><span class="sxs-lookup"><span data-stu-id="c327f-110">The [managing mobile devices for Configuration Manager 2007 solution](https://technet.microsoft.com/library/dn508400.aspx) helps you manage mobile devices when your infrastructure rests on a System Center Configuration Manager 2007.</span></span> <span data-ttu-id="c327f-111">這個解決方案示範如何設定執行 System Center 2012 Configuration Manager 的單一伺服器，讓您接著能夠執行 Microsoft Intune 並充分利用它的 MDM 功能。</span><span class="sxs-lookup"><span data-stu-id="c327f-111">This solution shows you how to set up a single server running System Center 2012 Configuration Manager so you can then run Microsoft Intune and take advantage of its MDM ability.</span></span>
* <span data-ttu-id="c327f-112">[管理小型環境解決方案中的行動裝置](https://technet.microsoft.com/library/dn715906.aspx) 適用於需要支援 MDM 的小型企業。</span><span class="sxs-lookup"><span data-stu-id="c327f-112">The [managing mobile devices in small environments solution](https://technet.microsoft.com/library/dn715906.aspx) is intended for small businesses that need to support MDM.</span></span> <span data-ttu-id="c327f-113">它說明如何使用 Microsoft Intune 來擴充目前的基礎結構，以支援行動裝置管理和 BYOD。</span><span class="sxs-lookup"><span data-stu-id="c327f-113">It explains how to use Microsoft Intune to extend your current infrastructure to support mobile device management and BYOD.</span></span> <span data-ttu-id="c327f-114">這個解決方案說明最簡單的案例，支援在獨立式、純雲端且沒有本機伺服器的組態中使用 Microsoft Intune。</span><span class="sxs-lookup"><span data-stu-id="c327f-114">This solution describes the simplest scenario supported for using Microsoft Intune in a standalone, cloud-only configuration with no local servers.</span></span>

## <a name="hybrid-identity-documentation"></a><span data-ttu-id="c327f-115">混合式身分識別文件</span><span class="sxs-lookup"><span data-stu-id="c327f-115">Hybrid identity documentation</span></span>
<span data-ttu-id="c327f-116">在實作行動裝置管理解決方案時，概念性和程序性規劃、部署及系統管理內容是非常實用的：</span><span class="sxs-lookup"><span data-stu-id="c327f-116">Conceptual and procedural planning, deployment, and administration content are useful when implementing your mobile device management solution:</span></span>

* <span data-ttu-id="c327f-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) 解決方案可協助您擷取和彙總有關基礎結構、原則、程序及最佳做法的知識，讓您的 IT 人員能夠建置可管理的系統和自動化作業。</span><span class="sxs-lookup"><span data-stu-id="c327f-117">[Microsoft System Center](https://technet.microsoft.com/library/cc507089.aspx) solutions can help you capture and aggregate knowledge about your infrastructure, policies, processes, and best practices so that your IT staff can build manageable systems and automate operations.</span></span>
* <span data-ttu-id="c327f-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) 是雲端式裝置管理服務，可協助您管理電腦和行動裝置並保護公司的資訊。</span><span class="sxs-lookup"><span data-stu-id="c327f-118">[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) is a cloud-based device management service that helps you to manage your computers and mobile devices and to secure your company’s information.</span></span>
* <span data-ttu-id="c327f-119">[Office 365 的 MDM](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) 可讓您在將行動裝置連線到您的 Office 365 組織時管理和保護它們。</span><span class="sxs-lookup"><span data-stu-id="c327f-119">[MDM for Office 365](https://technet.microsoft.com/library/ms.o365.cc.devicepolicy.aspx) allows you to manage and secure mobile devices when they're connected to your Office 365 organization.</span></span> <span data-ttu-id="c327f-120">您可以使用適用於 Office 365 的 MDM 來設定裝置安全性原則和存取規則，而且如果行動裝置遺失或遭竊，則會清除它們。</span><span class="sxs-lookup"><span data-stu-id="c327f-120">You can use MDM for Office 365 to set device security policies and access rules, and to wipe mobile devices if they’re lost or stolen.</span></span>

## <a name="hybrid-identity-resources"></a><span data-ttu-id="c327f-121">混合式身分識別資源</span><span class="sxs-lookup"><span data-stu-id="c327f-121">Hybrid identity resources</span></span>
<span data-ttu-id="c327f-122">監視下列資源，通常可提供關於行動裝置管理解決方案的最新消息和更新：</span><span class="sxs-lookup"><span data-stu-id="c327f-122">Monitoring the following resources often provides the latest news and updates on mobile device management solutions:</span></span>

* [<span data-ttu-id="c327f-123">Microsoft Enterprise Mobility 部落格</span><span class="sxs-lookup"><span data-stu-id="c327f-123">Microsoft Enterprise Mobility blog</span></span>](http://blogs.technet.com/b/enterprisemobility/)
* [<span data-ttu-id="c327f-124">Microsoft In The Cloud 部落格</span><span class="sxs-lookup"><span data-stu-id="c327f-124">Microsoft In The Cloud blog</span></span>](http://blogs.technet.com/b/in_the_cloud/)
* [<span data-ttu-id="c327f-125">Microsoft Intune 部落格</span><span class="sxs-lookup"><span data-stu-id="c327f-125">Microsoft Intune blog</span></span>](http://blogs.technet.com/b/microsoftintune/)
* [<span data-ttu-id="c327f-126">Microsoft System Center Configuration Manager 部落格</span><span class="sxs-lookup"><span data-stu-id="c327f-126">Microsoft System Center Configuration Manager blog</span></span>](http://blogs.technet.com/b/configurationmgr/)
* [<span data-ttu-id="c327f-127">Microsoft System Center Configuration Manager Team 部落格</span><span class="sxs-lookup"><span data-stu-id="c327f-127">Microsoft System Center Configuration Manager Team blog</span></span>](http://blogs.technet.com/b/configmgrteam/)

## <a name="see-also"></a><span data-ttu-id="c327f-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c327f-128">See also</span></span>
[<span data-ttu-id="c327f-129">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="c327f-129">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

