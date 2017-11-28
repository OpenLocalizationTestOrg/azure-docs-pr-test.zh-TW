---
title: "aaaConfigure Azure Active Directory 裝置型條件式存取原則 |Microsoft 文件"
description: "了解如何 tooconfigure Azure Active Directory 裝置型條件式存取原則。"
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
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="bce8b-103">設定 Azure Active Directory 裝置型條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="bce8b-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="bce8b-104">透過 [Azure Active Directory (Azure AD) 條件式存取](active-directory-conditional-access-azure-portal.md)，您可以微調授權使用者如何存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bce8b-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="bce8b-105">例如，您可以限制 hello 存取 toocertain 資源 tootrusted 裝置。</span><span class="sxs-lookup"><span data-stu-id="bce8b-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="bce8b-106">需要受信任裝置的條件式存取原則，也稱為裝置型條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="bce8b-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="bce8b-107">本主題會提供您如何 tooconfigure 裝置型條件式存取原則的 Azure AD 連接的應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bce8b-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="bce8b-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="bce8b-108">Before you begin</span></span>

<span data-ttu-id="bce8b-109">裝置型條件式存取會將 **Azure AD 條件式存取**和 **Azure AD 裝置管理**繫結在一起。</span><span class="sxs-lookup"><span data-stu-id="bce8b-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="bce8b-110">如果您還不熟悉其中一種情況，您應該閱讀下列主題，第一次的 hello:</span><span class="sxs-lookup"><span data-stu-id="bce8b-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="bce8b-111">**[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)** -本主題提供概觀條件式存取和 hello 相關的術語。</span><span class="sxs-lookup"><span data-stu-id="bce8b-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="bce8b-112">**[Azure Active Directory 中的簡介 toodevice 管理](device-management-introduction.md)** -本主題概略說明 hello 的各種選項需要 tooconnect 裝置與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="bce8b-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="bce8b-113">受信任的裝置</span><span class="sxs-lookup"><span data-stu-id="bce8b-113">Trusted devices</span></span>

<span data-ttu-id="bce8b-114">在行動裝置-首先，雲端優先世界中，Azure Active Directory 可讓單一登入 toodevices、 應用程式和服務從任何地方。</span><span class="sxs-lookup"><span data-stu-id="bce8b-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="bce8b-115">某些 toohello 適當的使用者授與存取您的環境中的資源可能無法夠好。</span><span class="sxs-lookup"><span data-stu-id="bce8b-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="bce8b-116">此外 toohello 適當的使用者，您可能也需要信任的裝置 toobe 用 tooaccess 資源。</span><span class="sxs-lookup"><span data-stu-id="bce8b-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="bce8b-117">在您的環境，您可以定義受信任的裝置根據 hello 下列元件：</span><span class="sxs-lookup"><span data-stu-id="bce8b-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="bce8b-118">hello[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)在裝置上</span><span class="sxs-lookup"><span data-stu-id="bce8b-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="bce8b-119">裝置是否符合規範</span><span class="sxs-lookup"><span data-stu-id="bce8b-119">Whether a device is compliant</span></span>
- <span data-ttu-id="bce8b-120">裝置是否已加入網域</span><span class="sxs-lookup"><span data-stu-id="bce8b-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="bce8b-121">hello[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)的特點在於 hello 您裝置執行作業系統。</span><span class="sxs-lookup"><span data-stu-id="bce8b-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="bce8b-122">在裝置型條件式存取原則中，您可以限制存取 toocertain 資源 toospecific 裝置平台。</span><span class="sxs-lookup"><span data-stu-id="bce8b-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="bce8b-123">在裝置型條件式存取原則中，您可能需要信任的裝置 toobe 標示為相容。</span><span class="sxs-lookup"><span data-stu-id="bce8b-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="bce8b-125">裝置可以標示為相容的 hello 目錄中：</span><span class="sxs-lookup"><span data-stu-id="bce8b-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="bce8b-126">Intune</span><span class="sxs-lookup"><span data-stu-id="bce8b-126">Intune</span></span> 
- <span data-ttu-id="bce8b-127">與 Azure AD 整合的第三方行動裝置管理系統</span><span class="sxs-lookup"><span data-stu-id="bce8b-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="bce8b-128">只有連接的 tooAzure AD 的裝置可以標示為相容。</span><span class="sxs-lookup"><span data-stu-id="bce8b-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="bce8b-129">tooconnect 裝置 tooAzure Active Directory，您有下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="bce8b-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="bce8b-130">已註冊的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce8b-130">Azure AD registered</span></span>
- <span data-ttu-id="bce8b-131">已聯結的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce8b-131">Azure AD joined</span></span>
- <span data-ttu-id="bce8b-132">已聯結的混合式 Azure AD</span><span class="sxs-lookup"><span data-stu-id="bce8b-132">Hybrid Azure AD joined</span></span>

    ![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="bce8b-134">如果您有內部部署 Active Directory (AD) 耗用量，您可以考慮不會連接的 tooAzure AD 而聯結的 tooyour AD toobe 受信任的裝置。</span><span class="sxs-lookup"><span data-stu-id="bce8b-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="bce8b-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bce8b-136">Next steps</span></span>

<span data-ttu-id="bce8b-137">在您的環境中設定裝置型條件式存取原則，您應該看看 hello [Azure Active Directory 中的條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="bce8b-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

