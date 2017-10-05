---
title: "將使用者佈建至 Azure AD 資源庫應用程式花費數小時以上 | Microsoft Docs"
description: "如何查明佈建至應用程式為什麼比您預期的更久"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="4844e-103">將使用者佈建至 Azure AD 資源庫應用程式花費數小時以上</span><span class="sxs-lookup"><span data-stu-id="4844e-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="4844e-104">當第一次啟用應用程式的自動佈建時，初始同步處理可能花費 20 分鐘到數小時，根據 Azure AD 目錄大小和佈建範圍中的使用者數目而定。</span><span class="sxs-lookup"><span data-stu-id="4844e-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="4844e-105">初始同步處理之後的後續同步處理會更快，因為佈建服務會儲存浮水印，代表兩個系統在初始同步處理之後的狀態，所以會改善後續同步處理的效能。</span><span class="sxs-lookup"><span data-stu-id="4844e-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="4844e-106">如何改善佈建的效能</span><span class="sxs-lookup"><span data-stu-id="4844e-106">How to improve provisioning performance</span></span>

<span data-ttu-id="4844e-107">如果初始同步處理花費好幾個小時，還有一個作法可以改善效能︰</span><span class="sxs-lookup"><span data-stu-id="4844e-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="4844e-108">**使用者範圍設定篩選條件。**</span><span class="sxs-lookup"><span data-stu-id="4844e-108">**User scoping filters.**</span></span> <span data-ttu-id="4844e-109">範圍設定篩選條件可讓您根據特定的屬性值篩選出使用者，以微調佈建服務從 Azure AD 擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="4844e-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="4844e-110">如需範圍設定篩選條件的詳細資訊，請參閱[根據範圍設定篩選條件以屬性為基礎的應用程式佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)。</span><span class="sxs-lookup"><span data-stu-id="4844e-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4844e-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4844e-111">Next steps</span></span>
[<span data-ttu-id="4844e-112">自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和解除佈建</span><span class="sxs-lookup"><span data-stu-id="4844e-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

