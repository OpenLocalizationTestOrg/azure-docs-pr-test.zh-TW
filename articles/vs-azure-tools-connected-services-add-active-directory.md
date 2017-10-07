---
title: "使用 Visual Studio 中的 已連接服務的 Azure Active Directory aaaAdding |Microsoft 文件"
description: "新增 Azure Active Directory 使用 hello Visual Studio 加入已連接服務對話方塊"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="c5e2d-103">在 Visual Studio 中使用已連接服務加入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5e2d-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>
<span data-ttu-id="c5e2d-104">藉由使用 Azure Active Directory (Azure AD)，您便可以針對 ASP.NET MVC Web 應用程式支援「單一登入」(SSO)，或在 Web API 服務中支援「Active Directory 驗證」。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="c5e2d-105">使用 Azure Active Directory 驗證時，您的使用者可以使用 Azure Active Directory tooconnect tooyour web 應用程式中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory tooconnect tooyour web applications.</span></span> <span data-ttu-id="c5e2d-106">公開 API 的 web 應用程式時，hello Web API 與 Azure Active Directory 驗證的優點包括增強的資料安全性。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-106">hello advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="c5e2d-107">使用 Azure AD，您沒有 toomanage 自己帳戶和使用者管理的分別驗證系統。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-107">With Azure AD, you do not have toomanage a separate authentication system with its own account and user management.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5e2d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c5e2d-108">Prerequisites</span></span>
- <span data-ttu-id="c5e2d-109">Azure 帳戶 - 如果您沒有 Azure 帳戶，您可以[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用您的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a><span data-ttu-id="c5e2d-110">連接 tooAzure Active Directory 使用 hello 已連接服務對話方塊</span><span class="sxs-lookup"><span data-stu-id="c5e2d-110">Connect tooAzure Active Directory using hello Connected Services dialog</span></span>
1. <span data-ttu-id="c5e2d-111">在 Visual Studio 中，建立或開啟 ASP.NET MVC 專案或 ASP.NET Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span>

1. <span data-ttu-id="c5e2d-112">從 hello 方案總管 中，以滑鼠右鍵按一下 hello**已連接服務** 節點，並從 hello 內容功能表中，選取**加入已連接服務**。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-112">From hello Solution Explorer, right-click hello **Connected Services** node, and, from hello context menu, select **Add Connected Services**.</span></span>

1. <span data-ttu-id="c5e2d-113">在 hello**已連接服務**頁面上，選取**與 Azure Active Directory 驗證**。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-113">On hello **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>
   
    ![[已連接服務] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="c5e2d-115">在 [hello**簡介**hello 頁面**設定 Azure AD 驗證**精靈中，選取**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-115">On hello **Introduction** page of hello **Configure Azure AD Authentication** wizard, select **Next**.</span></span>
   
    ![[簡介] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="c5e2d-117">在 hello**單一登入**頁面 hello**設定 Azure AD 驗證**精靈中，選取網域從 hello**網域**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-117">On hello **Single-Sign On** page of hello **Configure Azure AD Authentication** wizard, select a domain from hello **Domain** drop-down list.</span></span> <span data-ttu-id="c5e2d-118">hello 網域清單包含 hello 帳戶設定 對話方塊中所列出的 hello 帳戶可存取的所有網域。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-118">hello list of domains contains all domains accessible by hello accounts listed in hello Account Settings dialog.</span></span> <span data-ttu-id="c5e2d-119">或者，您可以輸入網域名稱如果您找不到 hello 要尋找的例如`mydomain.onmicrosoft.com`。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-119">As an alternative, you can enter a domain name if you don’t find hello one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="c5e2d-120">您可以選擇 hello 選項 toocreate 的 Azure Active Directory 應用程式，或使用現有的 Azure Active Directory 應用程式中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-120">You can choose hello option toocreate an Azure Active Directory app or use hello settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="c5e2d-121">完成時，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-121">Select **Next** when done.</span></span>
   
    ![[單一登入] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="c5e2d-123">Hello 上**目錄存取**頁面 hello**設定 Azure AD 驗證**精靈 中，確定該 hello**讀取目錄資料**核取選項。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-123">On hello **Directory Access** page of hello **Configure Azure AD Authentication** wizard, ensure that hello **Read directory data** option is checked.</span></span> 
   
    ![[目錄存取] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="c5e2d-125">選取**完成**tooadd hello 所需的組態程式碼和參考 tooenable 的 Azure AD 驗證程式專案。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-125">Select **Finish** tooadd hello necessary configuration code and references tooenable your project for Azure AD authentication.</span></span> <span data-ttu-id="c5e2d-126">您可以看到 hello Active Directory 網域上 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-126">You can see hello Active Directory domain on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c5e2d-127">Visual Studio 會顯示[發生了什麼事](#how-your-project-is-modified)文章 tooshow 您如何修改您的專案。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article tooshow you how your project was modified.</span></span> <span data-ttu-id="c5e2d-128">如果您想一切運作正常的 toocheck，開啟其中一個 hello 修改組態檔，並確認 hello 文章中提及的 hello 設定有。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-128">If you want toocheck that everything worked, open one of hello modified configuration files and verify that hello settings mentioned in hello article are there.</span></span> 

## <a name="how-your-project-is-modified"></a><span data-ttu-id="c5e2d-129">您的專案修改方式</span><span class="sxs-lookup"><span data-stu-id="c5e2d-129">How your project is modified</span></span>
<span data-ttu-id="c5e2d-130">當您執行 hello 精靈時，Visual Studio 會加入 Azure Active Directory 和相關聯的參考 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-130">When you run hello wizard, Visual Studio adds Azure Active Directory and associated references tooyour project.</span></span> <span data-ttu-id="c5e2d-131">組態檔和專案中的程式碼檔案也是 Azure AD 的已修改的 tooadd 支援。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-131">Configuration files and code files in your project are also modified tooadd support for Azure AD.</span></span> <span data-ttu-id="c5e2d-132">hello 特定修改 Visual Studio 會取決於 hello 專案類型。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-132">hello specific modifications that Visual Studio makes depend on hello project type.</span></span> <span data-ttu-id="c5e2d-133">如需深入了解 ASP.NET MVC 專案的修改方式，請參閱 [發生什麼事：MVC 專案](http://go.microsoft.com/fwlink/p/?LinkID=513809)。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span></span> <span data-ttu-id="c5e2d-134">而對於 Web API 專案，請參閱 [發生什麼事：Web API 專案](http://go.microsoft.com/fwlink/p/?LinkId=513810)。</span><span class="sxs-lookup"><span data-stu-id="c5e2d-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5e2d-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5e2d-135">Next steps</span></span>
* [<span data-ttu-id="c5e2d-136">MSDN 的 Azure Active Directory 論壇</span><span class="sxs-lookup"><span data-stu-id="c5e2d-136">MSDN Forum for Azure Active Directory</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [<span data-ttu-id="c5e2d-137">Azure Active Directory 文件</span><span class="sxs-lookup"><span data-stu-id="c5e2d-137">Azure Active Directory Documentation</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="c5e2d-138">部落格文章： 入門 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5e2d-138">Blog Post: Intro tooAzure Active Directory</span></span>](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

