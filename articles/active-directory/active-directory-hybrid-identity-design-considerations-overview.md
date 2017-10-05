---
title: "Azure Active Directory 混合式身分識別設計考量 - 概觀 | Microsoft Docs"
description: "混合式身分識別設計考量指南的概觀和內容對應"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2a70f2474298618dd8ee11c583f8f445d7eba7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a><span data-ttu-id="3907a-103">Azure Active Directory 混合式身分識別設計考量</span><span class="sxs-lookup"><span data-stu-id="3907a-103">Azure Active Directory Hybrid Identity Design Considerations</span></span>
<span data-ttu-id="3907a-104">以取用者為基礎的裝置正廣為公司組織採用，而且雲端架構的軟體即服務 (SaaS) 應用程式是很易於採用的。</span><span class="sxs-lookup"><span data-stu-id="3907a-104">Consumer-based devices are proliferating the corporate world, and cloud-based software-as-a-service (SaaS) applications are easy to adopt.</span></span> <span data-ttu-id="3907a-105">因此，要持續掌控使用者在內部資料中心與雲端平台間的應用程式存取，是很不容易的。</span><span class="sxs-lookup"><span data-stu-id="3907a-105">As a result, maintaining control of users’ application access across internal datacenters and cloud platforms is challenging.</span></span>  

<span data-ttu-id="3907a-106">Microsoft 的身分識別解決方案可跨越內部部署和雲端架構功能，建立單一使用者身分識別以用於所有資源的驗證和授權，不論位於何處。</span><span class="sxs-lookup"><span data-stu-id="3907a-106">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="3907a-107">我們稱之為混合式身分識別。</span><span class="sxs-lookup"><span data-stu-id="3907a-107">We call this Hybrid Identity.</span></span> <span data-ttu-id="3907a-108">使用 Microsoft 解決方案時，混合式身分識別有不同的設計和組態可供選擇，且在某些情況下，可能會難以判斷哪些組合最符合組織的需求。</span><span class="sxs-lookup"><span data-stu-id="3907a-108">There are different design and configuration options for hybrid identity using Microsoft solutions, and in some case it might be difficult to determine which combination will best meet the needs of your organization.</span></span> 

<span data-ttu-id="3907a-109">此混合式身分識別設計考量指南將協助您了解如何設計與組織的商務和技術需求最相符的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-109">This Hybrid Identity Design Considerations Guide will help you to understand how to design a hybrid identity solution that best fits the business and technology needs for your organization.</span></span>  <span data-ttu-id="3907a-110">本指南詳細說明一系列您可以依循的步驟和工作，以協助您設計符合組織獨特需求的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-110">This guide details a series of steps and tasks that you can follow to help you design a hybrid identity solution that meets your organization’s unique requirements.</span></span> <span data-ttu-id="3907a-111">在這些步驟和工作中，本指南將提供相關的技術和功能選項，讓組織能夠因應其功能和服務品質 (例如可用性、延展性、效能、管理性和安全性) 層級需求。</span><span class="sxs-lookup"><span data-stu-id="3907a-111">Throughout the steps and tasks, the guide will present the relevant technologies and feature options available to organizations to meet functional and service quality (such as availability, scalability, performance, manageability, and security) level requirements.</span></span> 

<span data-ttu-id="3907a-112">具體來說，混合式身分識別設計考量指南的目標，是為您解答下列問題：</span><span class="sxs-lookup"><span data-stu-id="3907a-112">Specifically, the hybrid identity design considerations guide goals are to answer the following questions:</span></span> 

* <span data-ttu-id="3907a-113">我需要提出及回答哪些問題，以針對某個技術或問題範疇完成最符合自身需求的混合式身分識別特定設計？</span><span class="sxs-lookup"><span data-stu-id="3907a-113">What questions do I need to ask and answer to drive a hybrid identity-specific design for a technology or problem domain that best meets my requirements?</span></span>
* <span data-ttu-id="3907a-114">針對此技術或問題範疇設計混合式身分識別解決方案時，需要完成哪些活動？</span><span class="sxs-lookup"><span data-stu-id="3907a-114">What sequence of activities should I complete to design a hybrid identity solution for the technology or problem domain?</span></span> 
* <span data-ttu-id="3907a-115">哪些混合式身分識別技術和組態選項可協助我達到自身的需求？</span><span class="sxs-lookup"><span data-stu-id="3907a-115">What hybrid identity technology and configuration options are available to help me meet my requirements?</span></span> <span data-ttu-id="3907a-116">應如何取捨這些選項，以選擇出適用於我的企業的最佳選項？</span><span class="sxs-lookup"><span data-stu-id="3907a-116">What are the trade-offs between those options so that I can select the best option for my business?</span></span>

## <a name="who-is-this-guide-intended-for"></a><span data-ttu-id="3907a-117">本指南的適用對象為何？</span><span class="sxs-lookup"><span data-stu-id="3907a-117">Who is this guide intended for?</span></span>
 <span data-ttu-id="3907a-118">負責為中型或大型組織設計混合式身分識別解決方案的 CIO、CITO、首席身分識別架構設計人員、企業架構設計人員和 IT 架構設計人員。</span><span class="sxs-lookup"><span data-stu-id="3907a-118">CIO, CITO, Chief Identity Architects, Enterprise Architects and IT Architects responsible for designing a hybrid identity solution for medium or large organizations.</span></span>

## <a name="how-can-this-guide-help-you"></a><span data-ttu-id="3907a-119">本指南對您有何幫助？</span><span class="sxs-lookup"><span data-stu-id="3907a-119">How can this guide help you?</span></span>
<span data-ttu-id="3907a-120">您可以使用本指南來了解如何設計能夠將雲端架構身分識別管理系統與您目前的內部部署身分識別解決方案整合的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-120">You can use this guide to understand how to design a hybrid identity solution that is able to integrate a cloud based identity management system with your current on-premises identity solution.</span></span> 

<span data-ttu-id="3907a-121">下圖顯示的範例說明可讓 IT 系統管理員順利將其目前位於內部部署的 Windows Server Active Directory 解決方案與 Microsoft Azure Active Directory 整合，讓使用者能在位於雲端和內部部署的應用程式使用單一登入 (SSO) 的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-121">The following graphic shows an example a hybrid identity solution that enables IT Admins to manage to integrate their current Windows Server Active Directory solution located on-premises with Microsoft Azure Active Directory to enable users to use Single Sign-On (SSO) across applications located in the cloud and on-premises.</span></span>

![](./media/hybrid-id-design-considerations/hybridID-example.png)

<span data-ttu-id="3907a-122">上方的圖例說明使用雲端服務與內部部署功能進行整合，為使用者提供以單一程序完成驗證的體驗，及協助 IT 人員管理這些資源的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-122">The above illustration is an example of a hybrid identity solution that is leveraging cloud services to integrate with on-premises capabilities in order to provide a single experience to the end user authentication process and to facilitate IT managing those resources.</span></span> <span data-ttu-id="3907a-123">雖然這可能是很常見的案例，但每個組織的混合式身分識別設計都可能會因不同的需求而與圖 1 所示的範例不同。</span><span class="sxs-lookup"><span data-stu-id="3907a-123">Although this can be a very common scenario, every organization’s hybrid identity design is likely to be different than the example illustrated in Figure 1 due to different requirements.</span></span> 

<span data-ttu-id="3907a-124">本指南將提供一系列您可以依循的步驟和工作，用以設計符合組織獨特需求的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-124">This guide provides a series of steps and tasks that you can follow to design a hybrid identity solution that meets your organization’s unique requirements.</span></span> <span data-ttu-id="3907a-125">在下列步驟和工作中，本指南將提供相關的技術和功能選項，讓您能夠因應組織的功能和服務品質層級需求。</span><span class="sxs-lookup"><span data-stu-id="3907a-125">Throughout the following steps and tasks, the guide presents the relevant technologies and feature options available to you to meet functional and service quality level requirements for your organization.</span></span>

<span data-ttu-id="3907a-126">**假設**：您有 Windows Server、Active Directory 網域服務與 Azure Active Directory 的相關經驗。</span><span class="sxs-lookup"><span data-stu-id="3907a-126">**Assumptions**: You have some experience with Windows Server, Active Directory Domain Services and Azure Active Directory.</span></span> <span data-ttu-id="3907a-127">在本文件中，我們假設您想要了解這些解決方案本身或在整合式解決方案中如何滿足您的商務需求。</span><span class="sxs-lookup"><span data-stu-id="3907a-127">In this document, we assume you are looking for how these solutions can meet your business needs on their own or in an integrated solution.</span></span>

## <a name="design-considerations-overview"></a><span data-ttu-id="3907a-128">設計考量概觀</span><span class="sxs-lookup"><span data-stu-id="3907a-128">Design considerations overview</span></span>
<span data-ttu-id="3907a-129">本文件將提供一組您可以依循的步驟和工作，用以設計最能符合您需求的混合式身分識別解決方案。</span><span class="sxs-lookup"><span data-stu-id="3907a-129">This document provides a set of steps and tasks that you can follow to design a hybrid identity solution that best meets your requirements.</span></span> <span data-ttu-id="3907a-130">步驟會依序呈現。</span><span class="sxs-lookup"><span data-stu-id="3907a-130">The steps are presented in an ordered sequence.</span></span> <span data-ttu-id="3907a-131">不過，您在後續步驟中學習的設計考量，可能會因為設計選擇的衝突，而需要變更您在先前步驟中所做的決策。</span><span class="sxs-lookup"><span data-stu-id="3907a-131">Design considerations you learn in later steps may require you to change decisions you made in earlier steps, however, due to conflicting design choices.</span></span> <span data-ttu-id="3907a-132">在本文件中會持續嘗試警告您潛在的設計衝突。</span><span class="sxs-lookup"><span data-stu-id="3907a-132">Every attempt is made to alert you to potential design conflicts throughout the document.</span></span> 

<span data-ttu-id="3907a-133">必須在充分地反覆執行相關步驟以整合文件中的所有考量之後，才能達到最符合您的需求的設計。</span><span class="sxs-lookup"><span data-stu-id="3907a-133">You will arrive at the design that best meets your requirements only after iterating through the steps as many times as necessary to incorporate all of the considerations within the document.</span></span> 

| <span data-ttu-id="3907a-134">混合式身分識別階段</span><span class="sxs-lookup"><span data-stu-id="3907a-134">Hybrid Identity Phase</span></span> | <span data-ttu-id="3907a-135">主題清單</span><span class="sxs-lookup"><span data-stu-id="3907a-135">Topic List</span></span> |
| --- | --- |
| <span data-ttu-id="3907a-136">判斷身分識別需求</span><span class="sxs-lookup"><span data-stu-id="3907a-136">Determine identity requirements</span></span> |[<span data-ttu-id="3907a-137">判斷商務需求</span><span class="sxs-lookup"><span data-stu-id="3907a-137">Determine business needs</span></span>](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [<span data-ttu-id="3907a-138">判斷目錄同步處理需求</span><span class="sxs-lookup"><span data-stu-id="3907a-138">Determine directory synchronization requirements</span></span>](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [<span data-ttu-id="3907a-139">判斷多重要素驗證需求</span><span class="sxs-lookup"><span data-stu-id="3907a-139">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [<span data-ttu-id="3907a-140">定義混合式身分識別採用策略</span><span class="sxs-lookup"><span data-stu-id="3907a-140">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| <span data-ttu-id="3907a-141">透過增強式身分識別解決方案規劃更高的資料安全性</span><span class="sxs-lookup"><span data-stu-id="3907a-141">Plan for enhancing data security through strong identity solution</span></span> |[<span data-ttu-id="3907a-142">判斷資料保護需求</span><span class="sxs-lookup"><span data-stu-id="3907a-142">Determine data protection requirements</span></span>](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [<span data-ttu-id="3907a-143">判斷內容管理需求</span><span class="sxs-lookup"><span data-stu-id="3907a-143">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [<span data-ttu-id="3907a-144">判斷存取控制需求</span><span class="sxs-lookup"><span data-stu-id="3907a-144">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [<span data-ttu-id="3907a-145">判斷事件因應需求</span><span class="sxs-lookup"><span data-stu-id="3907a-145">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [<span data-ttu-id="3907a-146">定義資料保護策略</span><span class="sxs-lookup"><span data-stu-id="3907a-146">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| <span data-ttu-id="3907a-147">規劃混合式身分識別生命週期</span><span class="sxs-lookup"><span data-stu-id="3907a-147">Plan for hybrid identity lifecycle</span></span> |[<span data-ttu-id="3907a-148">判斷混合式身分識別管理工作</span><span class="sxs-lookup"><span data-stu-id="3907a-148">Determine hybrid identity management tasks</span></span>](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [<span data-ttu-id="3907a-149">同步處理管理</span><span class="sxs-lookup"><span data-stu-id="3907a-149">Synchronization Management</span></span>](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [<span data-ttu-id="3907a-150">判斷混合式身分識別管理採用策略</span><span class="sxs-lookup"><span data-stu-id="3907a-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a><span data-ttu-id="3907a-151">下載此指南</span><span class="sxs-lookup"><span data-stu-id="3907a-151">Download this guide</span></span>
<span data-ttu-id="3907a-152">您可以從 [Technet 組件庫](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288)下載 PDF 版本的《混合式身分識別設計考量》指南。</span><span class="sxs-lookup"><span data-stu-id="3907a-152">You can download a pdf version of the Hybrid Identity Design Considerations guide from the [Technet gallery](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288).</span></span> 
