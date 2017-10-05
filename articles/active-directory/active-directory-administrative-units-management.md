---
title: "在 Azure Active Directory 中的管理單位管理預覽"
description: "使用管理單位在 Azure Active Directory 中進行更細微的權限委派"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: e12a0aea8264b1ea67c26294ec5bbe9c404a171e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="c9046-103">在 Azure AD 中的管理單位管理 - 公用預覽版</span><span class="sxs-lookup"><span data-stu-id="c9046-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="c9046-104">本文說明系統管理單位，即新的 Azure Active Directory 資源容器，可用來將系統管理權限委派給使用者的子集，並將原則套用到使用者的子集。</span><span class="sxs-lookup"><span data-stu-id="c9046-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies to a subset of users.</span></span> <span data-ttu-id="c9046-105">在 Azure Active Directory 中，管理單位可讓管理中心將權限委派至區域管理員或以更細微的層級來設定原則。</span><span class="sxs-lookup"><span data-stu-id="c9046-105">In Azure Active Directory, administrative units enable central administrators to delegate permissions to regional administrators or to set policy at a granular level.</span></span>

<span data-ttu-id="c9046-106">這在具有獨立部門的組織，例如由許多彼此獨立的學院 (商學院和工學院等) 所組成的大型大學中非常有用。</span><span class="sxs-lookup"><span data-stu-id="c9046-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="c9046-107">這類部門擁有自己的 IT 管理員，可控制存取、管理使用者，以及針對其部門設定特別原則。</span><span class="sxs-lookup"><span data-stu-id="c9046-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="c9046-108">管理中心想要能夠針對其特定部門中的使用者，授與這些部門的管理員權限。</span><span class="sxs-lookup"><span data-stu-id="c9046-108">Central administrators want to be able grant these divisional administrators permissions over the users in their particular divisions.</span></span> <span data-ttu-id="c9046-109">更具體來說，例如管理中心可以使用此範例，針對特定學院 (商學院) 建立一個管理單位，並僅在其中填入商學院使用者。</span><span class="sxs-lookup"><span data-stu-id="c9046-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only the Business school users.</span></span> <span data-ttu-id="c9046-110">然後管理中心可以將商學院的 IT 人員加入至範圍內的角色，換句話說，僅針對學院管理單位將管理權限授與商學院的 IT 人員。</span><span class="sxs-lookup"><span data-stu-id="c9046-110">Then a central administrator can add the Business school IT staff to a scoped role, in other words, grant the IT staff of Business school administrative permissions only over the Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9046-111">只有在啟用 Azure Active Directory Premium 時，才可以指派管理單位範圍的管理員角色。</span><span class="sxs-lookup"><span data-stu-id="c9046-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="c9046-112">如需詳細資訊，請參閱〈 [開始使用 Azure AD Premium](active-directory-get-started-premium.md)〉。</span><span class="sxs-lookup"><span data-stu-id="c9046-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="c9046-113">從管理中心的觀點來看，管理單位是可以建立並填入資源的目錄物件。</span><span class="sxs-lookup"><span data-stu-id="c9046-113">From the central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="c9046-114">**在此預覽版本中，這些資源僅能是使用者。**</span><span class="sxs-lookup"><span data-stu-id="c9046-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="c9046-115">一旦建立並填入，管理單位可用作為範圍，以限制僅能針對管理單位中所包含的資源來授與權限。</span><span class="sxs-lookup"><span data-stu-id="c9046-115">Once created and populated, the administrative unit can be used as a scope to restrict the granted permission only over resources contained in the administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="c9046-116">管理管理單位</span><span class="sxs-lookup"><span data-stu-id="c9046-116">Managing administrative units</span></span>
<span data-ttu-id="c9046-117">在此預覽版本中，您可以使用適用於 Windows PowerShell Cmdlet 的 Azure Active Directory 模組來建立和管理管理單位。</span><span class="sxs-lookup"><span data-stu-id="c9046-117">In this preview release, you can create and manage administrative units using the Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="c9046-118">若要深入了解做法，請參閱 [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0) (使用管理單位)</span><span class="sxs-lookup"><span data-stu-id="c9046-118">To learn more about how to do that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="c9046-119">如需軟體需求和安裝 Azure AD 模組的詳細資訊，以及使用 Azure AD 模組 Cmdlet 管理管理單位的資訊 (包括語法、參數說明和範例)，請參閱 [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="c9046-119">For more information on software requirements and installing the Azure AD module, and for information on the Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9046-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9046-120">Next steps</span></span>
[<span data-ttu-id="c9046-121">Azure Active Directory 版本</span><span class="sxs-lookup"><span data-stu-id="c9046-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
