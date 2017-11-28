---
title: "aaaAssign 群組 tooAzure AD 應用程式 |Microsoft 文件 '"
description: "如何 tooimplement 群組指派為 Azure 應用程式。"
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
ms.openlocfilehash: 086619df09c13bf259afc3128d45ed804b99e519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-azure-active-directory-groups-tooan-application"></a><span data-ttu-id="2c527-103">Azure Active Directory 群組指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c527-103">Assign Azure Active Directory groups tooan application</span></span>
<span data-ttu-id="2c527-104">您可以指派使用者和群組 tooan 應用程式之前，您必須要求使用者指派。</span><span class="sxs-lookup"><span data-stu-id="2c527-104">Before you can assign users and groups tooan application, you must require user assignment.</span></span> <span data-ttu-id="2c527-105">toolearn 如何 toorequire 使用者指派，請參閱 hello[需要使用者指派](active-directory-applications-guiding-developers-requiring-user-assignment.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="2c527-105">toolearn how toorequire user assignment, see hello [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="2c527-106">本文假設您已經有建立群組 hello 您使用此應用程式的 active directory 中。</span><span class="sxs-lookup"><span data-stu-id="2c527-106">This article assumes that you have already created groups in hello active directory you are using for this application.</span></span>

## <a name="assigning-groups-tooan-application"></a><span data-ttu-id="2c527-107">指派群組 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c527-107">Assigning Groups tooan Application</span></span>
1. <span data-ttu-id="2c527-108">登入 toohello Azure 入口網站以系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c527-108">Log in toohello Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="2c527-109">按一下 hello**所有項目**hello 主功能表中的項目。</span><span class="sxs-lookup"><span data-stu-id="2c527-109">Click on hello **All Items** item in hello main menu.</span></span>
3. <span data-ttu-id="2c527-110">選擇您要用於 hello 應用程式的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2c527-110">Choose hello directory you are using for hello application.</span></span>
4. <span data-ttu-id="2c527-111">按一下 hello**應用程式**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c527-111">Click on hello **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="2c527-112">從 hello 這個目錄相關聯的應用程式清單中選取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c527-112">Select hello application from hello list of applications associated with this directory.</span></span>
6. <span data-ttu-id="2c527-113">按一下 hello**使用者及群組**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2c527-113">Click hello **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="2c527-114">您使用 hello 的 active directory 中群組的篩選器 hello 清單**群組**下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="2c527-114">Filter hello list of groups in your active directory by using hello **Groups** dropdown list.</span></span>
8. <span data-ttu-id="2c527-115">選取 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="2c527-115">Select hello group.</span></span>
9. <span data-ttu-id="2c527-116">按一下 [ **指派**]。</span><span class="sxs-lookup"><span data-stu-id="2c527-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="2c527-117">出現提示時，按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="2c527-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c527-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c527-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
