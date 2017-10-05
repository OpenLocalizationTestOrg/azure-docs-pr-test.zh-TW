---
title: "使用 Visual Studio 的已連接服務加入 Azure Active Directory | Microsoft Docs"
description: "使用 Visual Studio 的 [加入已連接服務] 對話方塊加入 Azure Active Directory"
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
ms.openlocfilehash: a767c93fb271f3aa33d9556c69c511bcac7cb0d5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a><span data-ttu-id="2f8bf-103">在 Visual Studio 中使用已連接服務加入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f8bf-103">Adding an Azure Active Directory by using Connected Services in Visual Studio</span></span>
<span data-ttu-id="2f8bf-104">藉由使用 Azure Active Directory (Azure AD)，您便可以針對 ASP.NET MVC Web 應用程式支援「單一登入」(SSO)，或在 Web API 服務中支援「Active Directory 驗證」。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-104">By using Azure Active Directory (Azure AD), you can support Single Sign-On (SSO) for ASP.NET MVC web applications, or Active Directory Authentication in Web API services.</span></span> <span data-ttu-id="2f8bf-105">在使用「Azure Active Directory 驗證」的情況下，您的使用者可以從 Azure Active Directory 使用其帳戶來連接到您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-105">With Azure Active Directory Authentication, your users can use their accounts from Azure Active Directory to connect to your web applications.</span></span> <span data-ttu-id="2f8bf-106">「Azure Active Directory 驗證」搭配 Web API 的優點包括在從 Web 應用程式公開 API 時，可增強資料安全性。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-106">The advantages of Azure Active Directory Authentication with Web API include enhanced data security when exposing an API from a web application.</span></span> <span data-ttu-id="2f8bf-107">有了 Azure AD，您不必以各自的帳戶和使用者管理作業來管理個別的驗證系統。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-107">With Azure AD, you do not have to manage a separate authentication system with its own account and user management.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f8bf-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="2f8bf-108">Prerequisites</span></span>
- <span data-ttu-id="2f8bf-109">Azure 帳戶 - 如果您沒有 Azure 帳戶，您可以[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用您的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-109">Azure account - If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

### <a name="connect-to-azure-active-directory-using-the-connected-services-dialog"></a><span data-ttu-id="2f8bf-110">使用 [已連接服務] 對話方塊來連接到 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f8bf-110">Connect to Azure Active Directory using the Connected Services dialog</span></span>
1. <span data-ttu-id="2f8bf-111">在 Visual Studio 中，建立或開啟 ASP.NET MVC 專案或 ASP.NET Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-111">In Visual Studio, create or open an ASP.NET MVC project, or an ASP.NET Web API project.</span></span>

1. <span data-ttu-id="2f8bf-112">從 [方案總管] 中，在 [已連接服務] 節點上按一下滑鼠右鍵，然後從操作功能表中選取 [加入已連接服務]。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-112">From the Solution Explorer, right-click the **Connected Services** node, and, from the context menu, select **Add Connected Services**.</span></span>

1. <span data-ttu-id="2f8bf-113">在 [已連接服務] 頁面上，選取 [使用 Azure Active Directory 進行驗證]。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-113">On the **Connected Services** page, select **Authentication with Azure Active Directory**.</span></span>
   
    ![[已連接服務] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. <span data-ttu-id="2f8bf-115">在 [設定 Azure AD 驗證] 精靈的 [簡介] 頁面上，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-115">On the **Introduction** page of the **Configure Azure AD Authentication** wizard, select **Next**.</span></span>
   
    ![[簡介] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. <span data-ttu-id="2f8bf-117">在 [設定 Azure AD 驗證] 精靈的 [單一登入] 頁面上，從 [網域] 下拉式清單中選取一個網域。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-117">On the **Single-Sign On** page of the **Configure Azure AD Authentication** wizard, select a domain from the **Domain** drop-down list.</span></span> <span data-ttu-id="2f8bf-118">網域清單包含 [帳戶設定] 對話方塊中所列的帳戶可存取的所有網域。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-118">The list of domains contains all domains accessible by the accounts listed in the Account Settings dialog.</span></span> <span data-ttu-id="2f8bf-119">或者，如果您找不到所要尋找的網域 (例如 `mydomain.onmicrosoft.com`)，則可以輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-119">As an alternative, you can enter a domain name if you don’t find the one you’re looking for, such as `mydomain.onmicrosoft.com`.</span></span> <span data-ttu-id="2f8bf-120">您可以選擇可建立 Azure Active Directory 應用程式的選項，或是使用來自現有 Azure Active Directory 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-120">You can choose the option to create an Azure Active Directory app or use the settings from an existing Azure Active Directory app.</span></span> <span data-ttu-id="2f8bf-121">完成時，選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-121">Select **Next** when done.</span></span>
   
    ![[單一登入] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. <span data-ttu-id="2f8bf-123">在 [設定 Azure AD 驗證] 精靈的 [目錄存取] 頁面上，確定已核取 [讀取目錄資料] 選項。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-123">On the **Directory Access** page of the **Configure Azure AD Authentication** wizard, ensure that the **Read directory data** option is checked.</span></span> 
   
    ![[目錄存取] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. <span data-ttu-id="2f8bf-125">選取 [結束] 來新增必要的組態程式碼和參考，以讓您的專案能夠進行 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-125">Select **Finish** to add the necessary configuration code and references to enable your project for Azure AD authentication.</span></span> <span data-ttu-id="2f8bf-126">您可以在 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)上看到 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-126">You can see the Active Directory domain on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2f8bf-127">Visual Studio 將會顯示一篇[發生什麼事](#how-your-project-is-modified)文章，來說明已如何修改您的專案。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-127">Visual Studio will display a [What Happened](#how-your-project-is-modified) article to show you how your project was modified.</span></span> <span data-ttu-id="2f8bf-128">如果您想要檢查是否一切正常，請開啟其中一個已修改的組態檔，然後確認其中包含文章中所提到的設定。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-128">If you want to check that everything worked, open one of the modified configuration files and verify that the settings mentioned in the article are there.</span></span> 

## <a name="how-your-project-is-modified"></a><span data-ttu-id="2f8bf-129">您的專案修改方式</span><span class="sxs-lookup"><span data-stu-id="2f8bf-129">How your project is modified</span></span>
<span data-ttu-id="2f8bf-130">當您執行精靈時，Visual Studio 會將 Azure Active Directory 和關聯的參考新增到您的專案。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-130">When you run the wizard, Visual Studio adds Azure Active Directory and associated references to your project.</span></span> <span data-ttu-id="2f8bf-131">您專案中的組態檔和程式碼也會進行修改，以加入 Azure AD 支援。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-131">Configuration files and code files in your project are also modified to add support for Azure AD.</span></span> <span data-ttu-id="2f8bf-132">Visual Studio 所做的特定修改視專案類型而定。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-132">The specific modifications that Visual Studio makes depend on the project type.</span></span> <span data-ttu-id="2f8bf-133">如需深入了解 ASP.NET MVC 專案的修改方式，請參閱 [發生什麼事：MVC 專案](http://go.microsoft.com/fwlink/p/?LinkID=513809)。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-133">For detailed information about how ASP.NET MVC projects are modified, see [What happened– MVC Projects](http://go.microsoft.com/fwlink/p/?LinkID=513809).</span></span> <span data-ttu-id="2f8bf-134">而對於 Web API 專案，請參閱 [發生什麼事：Web API 專案](http://go.microsoft.com/fwlink/p/?LinkId=513810)。</span><span class="sxs-lookup"><span data-stu-id="2f8bf-134">For Web API projects, see [What happened – Web API Projects](http://go.microsoft.com/fwlink/p/?LinkId=513810).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f8bf-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f8bf-135">Next steps</span></span>
* [<span data-ttu-id="2f8bf-136">MSDN 的 Azure Active Directory 論壇</span><span class="sxs-lookup"><span data-stu-id="2f8bf-136">MSDN Forum for Azure Active Directory</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [<span data-ttu-id="2f8bf-137">Azure Active Directory 文件</span><span class="sxs-lookup"><span data-stu-id="2f8bf-137">Azure Active Directory Documentation</span></span>](https://azure.microsoft.com/documentation/services/active-directory/)
* [<span data-ttu-id="2f8bf-138">部落格文章：Azure Active Directory 簡介 (英文)</span><span class="sxs-lookup"><span data-stu-id="2f8bf-138">Blog Post: Intro to Azure Active Directory</span></span>](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

