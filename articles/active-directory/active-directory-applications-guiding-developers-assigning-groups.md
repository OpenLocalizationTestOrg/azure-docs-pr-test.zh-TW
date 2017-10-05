---
title: "將群組指派給 Azure AD 應用程式 | Microsoft Docs'"
description: "如何為 Azure 應用程式實作群組指派。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="ab10d-103">將 Azure Active Directory 群組指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="ab10d-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="ab10d-104">在將使用者和群組指派給應用程式之前，您必須先要求使用者指派。</span><span class="sxs-lookup"><span data-stu-id="ab10d-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="ab10d-105">若要了解如何要求使用者指派，請參閱 [Azure AD 和應用程式：要求使用者指派](active-directory-applications-guiding-developers-requiring-user-assignment.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="ab10d-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="ab10d-106">本文假設您已經在針對此應用程式使用的作用中目錄內建立了群組。</span><span class="sxs-lookup"><span data-stu-id="ab10d-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="ab10d-107">將群組指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="ab10d-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="ab10d-108">使用系統管理員帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ab10d-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="ab10d-109">在主功能表中按一下 [ **所有項目** ] 項目。</span><span class="sxs-lookup"><span data-stu-id="ab10d-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="ab10d-110">選擇您要為應用程式使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="ab10d-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="ab10d-111">按一下 [ **應用程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ab10d-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="ab10d-112">從與此目錄相關聯的應用程式清單中選取應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab10d-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="ab10d-113">按一下 [ **使用者和群組** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ab10d-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="ab10d-114">透過 [ **群組** ] 下拉式清單，篩選作用中目錄內的群組清單。</span><span class="sxs-lookup"><span data-stu-id="ab10d-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="ab10d-115">選取群組。</span><span class="sxs-lookup"><span data-stu-id="ab10d-115">Select the group.</span></span>
9. <span data-ttu-id="ab10d-116">按一下 [ **指派**]。</span><span class="sxs-lookup"><span data-stu-id="ab10d-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="ab10d-117">出現提示時，按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="ab10d-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab10d-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab10d-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
