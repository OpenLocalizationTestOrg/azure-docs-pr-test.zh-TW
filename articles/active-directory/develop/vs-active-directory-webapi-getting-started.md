---
title: "開始使用 Visual Studio WebApi 專案中的 Azure AD | Microsoft Docs"
description: "使用 Visual Studio 已連接服務連接 Azure AD 或建立 Azure AD 後，如何在 WebApi 專案中開始使用 Azure Active Directory"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="1248d-103">開始使用 Azure Active Directory 和 Visual Studio 已連接服務 (WebApi 專案)</span><span class="sxs-lookup"><span data-stu-id="1248d-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1248d-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="1248d-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="1248d-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="1248d-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="1248d-106">存取控制器之前需要驗證</span><span class="sxs-lookup"><span data-stu-id="1248d-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="1248d-107">專案中的所有控制器都加上 **Authorize** 屬性做裝飾。</span><span class="sxs-lookup"><span data-stu-id="1248d-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="1248d-108">此屬性要求使用者必須經過驗證，才能存取這些控制器所定義的 API。</span><span class="sxs-lookup"><span data-stu-id="1248d-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="1248d-109">若要允許以匿名方式存取控制器，請從控制器中移除此屬性。</span><span class="sxs-lookup"><span data-stu-id="1248d-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="1248d-110">如果您要以更精確地設定權限，請將此屬性套用至每一個需要授權的方法，而非套用至控制器類別。</span><span class="sxs-lookup"><span data-stu-id="1248d-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1248d-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1248d-111">Next steps</span></span>
[<span data-ttu-id="1248d-112">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1248d-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

