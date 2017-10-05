---
title: "如何移除使用者的應用程式存取 | Microsoft Docs"
description: "了解如何移除使用者的應用程式存取"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="891ca-103">如何移除使用者的應用程式存取</span><span class="sxs-lookup"><span data-stu-id="891ca-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="891ca-104">本文協助您了解如何移除使用者的應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="891ca-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="891ca-105">我想要移除特定使用者或群組的應用程式指派</span><span class="sxs-lookup"><span data-stu-id="891ca-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="891ca-106">若要移除使用者或群組的應用程式指派，請依照[在 Azure Active Directory 中從企業應用程式移除使用者或群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)文件列出的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="891ca-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="891ca-107">.## 我想要讓每個使用者都無法存取應用程式</span><span class="sxs-lookup"><span data-stu-id="891ca-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="891ca-108">若要讓所有使用者都無法登入應用程式，請依照[在 Azure Active Directory 中停用使用者登入企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)文件列出的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="891ca-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="891ca-109">我想要完全刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="891ca-109">I want to delete an application entirely</span></span>

<span data-ttu-id="891ca-110">若要**刪除應用程式**，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="891ca-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="891ca-111">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="891ca-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="891ca-112">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="891ca-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="891ca-113">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="891ca-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="891ca-114">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="891ca-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="891ca-115">按一下 [所有應用程式] 以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="891ca-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="891ca-116">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="891ca-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="891ca-117">選取您要刪除的應用程式。</span><span class="sxs-lookup"><span data-stu-id="891ca-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="891ca-118">應用程式載入後，從頂端應用程式的 [概觀] 刀鋒視窗按一下 [刪除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="891ca-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="891ca-119">我想要停用任何應用程式的所有未來使用者同意作業</span><span class="sxs-lookup"><span data-stu-id="891ca-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="891ca-120">停用整個目錄的使用者同意會阻止使用者同意任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="891ca-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="891ca-121">系統管理員仍然可以代表使用者行使同意。</span><span class="sxs-lookup"><span data-stu-id="891ca-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="891ca-122">若要進一步了解應用程式同意，以及為什麼您想要或不不想這樣做，請參閱[了解使用者和系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)。</span><span class="sxs-lookup"><span data-stu-id="891ca-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="891ca-123">若要**停用整個目錄中的所有未來使用者同意作業**，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="891ca-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="891ca-124">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="891ca-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="891ca-125">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="891ca-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="891ca-126">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="891ca-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="891ca-127">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="891ca-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="891ca-128">按一下 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="891ca-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="891ca-129">將 [使用者可以允許應用程式存取其資料] 切換開關設為 [否]，並按一下 [儲存] 按鈕，以停用所有未來的使用者同意作業。</span><span class="sxs-lookup"><span data-stu-id="891ca-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="891ca-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="891ca-130">Next steps</span></span>
[<span data-ttu-id="891ca-131">管理應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="891ca-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
