---
title: "在 Azure Active Directory 中的 aaaAdministrative 單位管理預覽"
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
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a><span data-ttu-id="c89a9-103">在 Azure AD 中的管理單位管理 - 公用預覽版</span><span class="sxs-lookup"><span data-stu-id="c89a9-103">Administrative units management in Azure AD - public preview</span></span>
<span data-ttu-id="c89a9-104">本文說明系統管理單元，新的 Azure Active Directory 容器，可以使用委派系統管理權限的使用者子集及套用原則 tooa 使用者子集上的資源。</span><span class="sxs-lookup"><span data-stu-id="c89a9-104">This article describes administrative units – a new Azure Active Directory container of resources that can be used for delegating administrative permissions over subsets of users and applying policies tooa subset of users.</span></span> <span data-ttu-id="c89a9-105">在 Azure Active Directory 中，系統管理單元可讓中央系統管理員 toodelegate 權限 tooregional 系統管理員或 tooset 細微的層級的原則。</span><span class="sxs-lookup"><span data-stu-id="c89a9-105">In Azure Active Directory, administrative units enable central administrators toodelegate permissions tooregional administrators or tooset policy at a granular level.</span></span>

<span data-ttu-id="c89a9-106">這在具有獨立部門的組織，例如由許多彼此獨立的學院 (商學院和工學院等) 所組成的大型大學中非常有用。</span><span class="sxs-lookup"><span data-stu-id="c89a9-106">This is useful in organizations with independent divisions, for example, a large university that is made up of many autonomous schools (Business school, Engineering school, and so on) which are independent from each other.</span></span> <span data-ttu-id="c89a9-107">這類部門擁有自己的 IT 管理員，可控制存取、管理使用者，以及針對其部門設定特別原則。</span><span class="sxs-lookup"><span data-stu-id="c89a9-107">Such divisions have their own IT administrators who control access, manage users, and set policies specifically for their division.</span></span> <span data-ttu-id="c89a9-108">中央系統管理員想透過其特殊部門中的 hello 使用者 toobe 無法授與這些部門系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="c89a9-108">Central administrators want toobe able grant these divisional administrators permissions over hello users in their particular divisions.</span></span> <span data-ttu-id="c89a9-109">更具體來說，使用此範例中，中央系統管理員可以比方說，建立為特定學院 （商學院） 管理單位並填入它僅 hello 商學院使用者等等。</span><span class="sxs-lookup"><span data-stu-id="c89a9-109">More specifically, using this example, a central administrator can, for instance, create an administrative unit for a particular school (Business school) and populate it with only hello Business school users.</span></span> <span data-ttu-id="c89a9-110">然後，中央系統管理員可以將 hello 商學院 IT 人員 tooa 範圍的角色，亦即，授與 hello 的商務學校系統管理權限只能透過 hello 商務商學院系統管理單元的 IT 人員。</span><span class="sxs-lookup"><span data-stu-id="c89a9-110">Then a central administrator can add hello Business school IT staff tooa scoped role, in other words, grant hello IT staff of Business school administrative permissions only over hello Business school administrative unit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c89a9-111">只有在啟用 Azure Active Directory Premium 時，才可以指派管理單位範圍的管理員角色。</span><span class="sxs-lookup"><span data-stu-id="c89a9-111">You can assign administrative unit-scoped admin roles only if you enable Azure Active Directory Premium.</span></span> <span data-ttu-id="c89a9-112">如需詳細資訊，請參閱〈 [開始使用 Azure AD Premium](active-directory-get-started-premium.md)〉。</span><span class="sxs-lookup"><span data-stu-id="c89a9-112">For more information, see [Getting started with Azure AD Premium](active-directory-get-started-premium.md).</span></span>
>


<span data-ttu-id="c89a9-113">Hello 中央系統管理員的觀點來看，從管理單位是目錄物件，可以建立和填入資源。</span><span class="sxs-lookup"><span data-stu-id="c89a9-113">From hello central administrator’s point of view, an administrative unit is a directory object that can be created and populated with resources.</span></span> <span data-ttu-id="c89a9-114">**在此預覽版本中，這些資源僅能是使用者。**</span><span class="sxs-lookup"><span data-stu-id="c89a9-114">**In this preview release, these resources can be only users.**</span></span> <span data-ttu-id="c89a9-115">一旦建立並填入，hello 系統管理單元可用來當做範圍 toorestrict hello 授與權限，只能透過 hello 系統管理單元中所包含的資源。</span><span class="sxs-lookup"><span data-stu-id="c89a9-115">Once created and populated, hello administrative unit can be used as a scope toorestrict hello granted permission only over resources contained in hello administrative unit.</span></span>

## <a name="managing-administrative-units"></a><span data-ttu-id="c89a9-116">管理管理單位</span><span class="sxs-lookup"><span data-stu-id="c89a9-116">Managing administrative units</span></span>
<span data-ttu-id="c89a9-117">在此預覽版本，您可以建立和管理使用 hello Azure Active Directory 模組的 Windows PowerShell cmdlet 的系統管理單元。</span><span class="sxs-lookup"><span data-stu-id="c89a9-117">In this preview release, you can create and manage administrative units using hello Azure Active Directory Module for Windows PowerShell cmdlets.</span></span> <span data-ttu-id="c89a9-118">深入了解如何 toolearn toodo，請參閱[使用系統管理單元](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="c89a9-118">toolearn more about how toodo that, see [Working with Administrative Units](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)</span></span>

<span data-ttu-id="c89a9-119">如需有關軟體需求和安裝 hello Azure AD 模組，以及有關 hello Azure AD 模組 cmdlet 來管理管理單位，包括語法、 參數說明和範例，請參閱[Azure ActiveDirectory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="c89a9-119">For more information on software requirements and installing hello Azure AD module, and for information on hello Azure AD Module cmdlets for managing administrative units, including syntax, parameter descriptions, and examples, see [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c89a9-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c89a9-120">Next steps</span></span>
[<span data-ttu-id="c89a9-121">Azure Active Directory 版本</span><span class="sxs-lookup"><span data-stu-id="c89a9-121">Azure Active Directory editions</span></span>](active-directory-editions.md)
