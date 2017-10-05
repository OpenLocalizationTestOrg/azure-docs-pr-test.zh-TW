---
title: "設定 Azure Active Directory 裝置型條件式存取原則 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 裝置型條件式存取原則。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="64f83-103">設定 Azure Active Directory 裝置型條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="64f83-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="64f83-104">透過 [Azure Active Directory (Azure AD) 條件式存取](active-directory-conditional-access-azure-portal.md)，您可以微調授權使用者如何存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="64f83-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="64f83-105">例如，您可以特定資源的存取限制為受信任的裝置。</span><span class="sxs-lookup"><span data-stu-id="64f83-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="64f83-106">需要受信任裝置的條件式存取原則，也稱為裝置型條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="64f83-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="64f83-107">本主題提供有關如何為 Azure AD 連線應用程式設定裝置型條件式存取原則的資訊。</span><span class="sxs-lookup"><span data-stu-id="64f83-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="64f83-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="64f83-108">Before you begin</span></span>

<span data-ttu-id="64f83-109">裝置型條件式存取會將 **Azure AD 條件式存取**和 **Azure AD 裝置管理**繫結在一起。</span><span class="sxs-lookup"><span data-stu-id="64f83-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="64f83-110">如果您還不熟悉上述其中一種領域，您應該先閱讀下列主題：</span><span class="sxs-lookup"><span data-stu-id="64f83-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="64f83-111">**[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)** - 本主題提供條件式存取和相關術語的概念性概觀。</span><span class="sxs-lookup"><span data-stu-id="64f83-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="64f83-112">**[Azure Active Directory 中的裝置管理簡介](device-management-introduction.md)** - 本主題提供您可用來連線裝置與 Azure AD 之各種選項的概觀。</span><span class="sxs-lookup"><span data-stu-id="64f83-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="64f83-113">受信任的裝置</span><span class="sxs-lookup"><span data-stu-id="64f83-113">Trusted devices</span></span>

<span data-ttu-id="64f83-114">在行動第一、雲端第一的世界中，Azure Active Directory 可讓您從任何地方單一登入至裝置、應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="64f83-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="64f83-115">對於您環境中的某些資源，授與存取權給適當的使用者可能還不夠好。</span><span class="sxs-lookup"><span data-stu-id="64f83-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="64f83-116">除了適當的使用者，您可能也需要將受信任的裝置用來存取資源。</span><span class="sxs-lookup"><span data-stu-id="64f83-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="64f83-117">在您的環境中，您可以根據下列元件定義受信任的裝置：</span><span class="sxs-lookup"><span data-stu-id="64f83-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="64f83-118">裝置上的[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)</span><span class="sxs-lookup"><span data-stu-id="64f83-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="64f83-119">裝置是否符合規範</span><span class="sxs-lookup"><span data-stu-id="64f83-119">Whether a device is compliant</span></span>
- <span data-ttu-id="64f83-120">裝置是否已加入網域</span><span class="sxs-lookup"><span data-stu-id="64f83-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="64f83-121">[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)的特點是您裝置執行的作業系統。</span><span class="sxs-lookup"><span data-stu-id="64f83-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="64f83-122">在裝置型條件式存取原則中，您可以將特定資源的存取權限制為特定裝置平台。</span><span class="sxs-lookup"><span data-stu-id="64f83-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="64f83-123">在裝置型條件式存取原則中，您可能需要標示為符合規範的受信任裝置。</span><span class="sxs-lookup"><span data-stu-id="64f83-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="64f83-125">裝置可由下列項目在目錄中標示為符合規範：</span><span class="sxs-lookup"><span data-stu-id="64f83-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="64f83-126">Intune</span><span class="sxs-lookup"><span data-stu-id="64f83-126">Intune</span></span> 
- <span data-ttu-id="64f83-127">與 Azure AD 整合的第三方行動裝置管理系統</span><span class="sxs-lookup"><span data-stu-id="64f83-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="64f83-128">只有連線到 Azure AD 的裝置可標示為符合規範。</span><span class="sxs-lookup"><span data-stu-id="64f83-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="64f83-129">若要將裝置連線到 Azure Active Directory，您有下列選項：</span><span class="sxs-lookup"><span data-stu-id="64f83-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="64f83-130">已註冊的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f83-130">Azure AD registered</span></span>
- <span data-ttu-id="64f83-131">已聯結的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f83-131">Azure AD joined</span></span>
- <span data-ttu-id="64f83-132">已聯結的混合式 Azure AD</span><span class="sxs-lookup"><span data-stu-id="64f83-132">Hybrid Azure AD joined</span></span>

    ![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="64f83-134">如果您有內部部署 Active Directory (AD) 使用量，您可以考慮未連線到 Azure AD 但已聯結至要信任之 AD 的裝置。</span><span class="sxs-lookup"><span data-stu-id="64f83-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="64f83-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64f83-136">Next steps</span></span>

<span data-ttu-id="64f83-137">在您的環境中設定裝置型條件式存取原則之前，您應該閱讀 [Azure Active Directory 中條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="64f83-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

