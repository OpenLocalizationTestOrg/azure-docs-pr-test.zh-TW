---
title: "Azure AD 和應用程式：將使用者指派給應用程式 | Microsoft Docs"
description: "如何實作 Azure 應用程式的使用者指派。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 97ce69c1-4034-4e38-bd82-8caf984f6b98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 29d63bd5781dc7ef9e84840dd4b1b70222cf6892
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-assigning-users-to-an-application"></a><span data-ttu-id="306bd-103">Azure AD 和應用程式：將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="306bd-103">Azure AD and Applications: Assigning Users to an Application</span></span>
<span data-ttu-id="306bd-104">在將使用者和群組指派給應用程式之前，您必須先要求使用者指派。</span><span class="sxs-lookup"><span data-stu-id="306bd-104">Before you can assign users and groups to an application, you must require user assignment.</span></span>  <span data-ttu-id="306bd-105">若要了解如何要求使用者指派，請參閱 [要求使用者指派](active-directory-applications-guiding-developers-requiring-user-assignment.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="306bd-105">To learn how to require user assignment please see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

## <a name="assigning-users-to-an-application"></a><span data-ttu-id="306bd-106">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="306bd-106">Assigning Users to an Application</span></span>
1. <span data-ttu-id="306bd-107">使用系統管理員帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="306bd-107">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="306bd-108">在主功能表中按一下 [ **所有項目** ] 項目。</span><span class="sxs-lookup"><span data-stu-id="306bd-108">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="306bd-109">選擇您要為應用程式使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="306bd-109">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="306bd-110">按一下 [ **應用程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="306bd-110">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="306bd-111">從與此目錄相關聯的應用程式清單中選取應用程式。</span><span class="sxs-lookup"><span data-stu-id="306bd-111">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="306bd-112">按一下 [ **使用者和群組** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="306bd-112">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="306bd-113">選取您要指派給應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="306bd-113">Select the users you want to assign to the application.</span></span>
8. <span data-ttu-id="306bd-114">按一下 [ **指派**]。</span><span class="sxs-lookup"><span data-stu-id="306bd-114">Click **ASSIGN**.</span></span>
9. <span data-ttu-id="306bd-115">出現提示時，按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="306bd-115">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="306bd-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="306bd-116">Next Steps</span></span>
[!INCLUDE [guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]

