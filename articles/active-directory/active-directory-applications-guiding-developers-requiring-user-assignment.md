---
title: "要求使用者指派 - Azure AD | Microsoft Docs'"
description: "如何要求 Azure 應用程式的使用者指派。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="a6509-103">Azure AD 和應用程式：要求使用者指派</span><span class="sxs-lookup"><span data-stu-id="a6509-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="a6509-104">要求使用者指派</span><span class="sxs-lookup"><span data-stu-id="a6509-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="a6509-105">使用系統管理員帳戶登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a6509-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="a6509-106">在主功能表中按一下 [ **所有項目** ] 項目。</span><span class="sxs-lookup"><span data-stu-id="a6509-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="a6509-107">選擇您要為應用程式使用的目錄。</span><span class="sxs-lookup"><span data-stu-id="a6509-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="a6509-108">按一下 [ **應用程式** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6509-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="a6509-109">從與此目錄相關聯的應用程式清單中選取應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="a6509-110">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6509-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="a6509-111">將 [ **需要使用者指派才能存取應用程式** ] 切換成 [是]。</span><span class="sxs-lookup"><span data-stu-id="a6509-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="a6509-112">按一下畫面底部的 [ **儲存** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6509-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="a6509-113">現在您需要將使用者及/或群組指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6509-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="a6509-114">請參閱[將使用者指派給應用程式](active-directory-applications-guiding-developers-assigning-users.md)和[將群組指派給應用程式](active-directory-applications-guiding-developers-assigning-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="a6509-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6509-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6509-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
