---
title: "aaaHow tooconfigure 使用者佈建 Azure AD tooan 組件庫的應用程式 |Microsoft 文件"
description: "如何快速設定豐富的使用者帳戶佈建和解除佈建 tooapplications hello Azure AD 應用程式庫中已列出"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="33678-103">如何 tooconfigure 使用者佈建 Azure AD tooan 組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="33678-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="33678-104">*使用者帳戶佈建*就是建立、 更新和/或停用使用者帳戶記錄應用程式的本機使用者設定檔存放區中的 hello 操作。</span><span class="sxs-lookup"><span data-stu-id="33678-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="33678-105">大部分的 SaaS 應用程式和雲端儲存 hello 使用者角色和權限在自己的本機使用者設定檔存放區，和其本機存放區中的這類使用者記錄的存在是*必要*的單一登入及存取 toowork。</span><span class="sxs-lookup"><span data-stu-id="33678-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="33678-106">在 hello Azure 入口網站，hello**佈建**索引標籤 hello 左側的導覽窗格中的企業應用程式會顯示該應用程式支援哪些佈建模式。</span><span class="sxs-lookup"><span data-stu-id="33678-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="33678-107">這可能是下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="33678-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="33678-108">設定應用程式以進行手動佈建</span><span class="sxs-lookup"><span data-stu-id="33678-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="33678-109">*手動*佈建表示必須以手動方式使用該應用程式所提供的 hello 方法來建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="33678-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="33678-110">這可能表示登入該應用程式的系統管理員入口網站，然後使用 Web 架構使用者介面新增使用者。</span><span class="sxs-lookup"><span data-stu-id="33678-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="33678-111">或者，它可能會使用該應用程式所提供的機制，來上傳含有使用者帳戶詳細資料的試算表。</span><span class="sxs-lookup"><span data-stu-id="33678-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="33678-112">提供由 hello 應用程式或連絡 hello 應用程式開發人員 toodetermine wat 機制可用，請參閱 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="33678-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="33678-113">如果手動 hello 模式顯示給定的應用程式，這表示，任何自動的 Azure AD 佈建連接器 hello 應用程式尚未建立。</span><span class="sxs-lookup"><span data-stu-id="33678-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="33678-114">或表示 hello 應用程式並不支援 hello 先決條件使用者管理 API 時哪些 toobuild 自動化佈建的連接器。</span><span class="sxs-lookup"><span data-stu-id="33678-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="33678-115">如果您想要 toorequest 支援給定的應用程式的自動佈建，您可以填寫在要求<http://aka.ms/aadapprequest>。</span><span class="sxs-lookup"><span data-stu-id="33678-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="33678-116">設定應用程式以進行自動佈建</span><span class="sxs-lookup"><span data-stu-id="33678-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="33678-117">「自動」表示已經為此應用程式開發 Azure AD 佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="33678-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="33678-118">如需有關 hello Azure AD 佈建服務和它的運作方式，請參閱[自動化使用者佈建和取消佈建 tooSaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)。</span><span class="sxs-lookup"><span data-stu-id="33678-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="33678-119">如需有關如何 tooprovision 特定使用者和群組 tooan 應用程式，請參閱[管理使用者帳戶佈建的企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)。</span><span class="sxs-lookup"><span data-stu-id="33678-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="33678-120">hello 實際步驟需要的 tooenable 及設定自動佈建 hello 應用程式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="33678-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="33678-121">您應該開始尋找 hello 安裝教學課程特定的 toosetting 上佈建您的應用程式，並遵循這些步驟 tooconfigure hello 應用程式與 Azure AD toocreate hello 佈建的連接。</span><span class="sxs-lookup"><span data-stu-id="33678-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="33678-122">應用程式教學課程，請參閱[清單的教學課程有關 tooIntegrate SaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)。</span><span class="sxs-lookup"><span data-stu-id="33678-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="33678-123">設定佈建是 tooreview 時很重要的事 tooconsider 及設定 hello 屬性對應，以及定義哪些使用者 （或群組） 的屬性流程，從 Azure AD toohello 應用程式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="33678-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="33678-124">這包括設定 hello 「 比對屬性 」 會使用的 toouniquely 找出並符合 hello 兩個系統之間的使用者/群組。</span><span class="sxs-lookup"><span data-stu-id="33678-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="33678-125">如需這個重要程序的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="33678-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33678-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33678-126">Next steps</span></span>
[<span data-ttu-id="33678-127">在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應</span><span class="sxs-lookup"><span data-stu-id="33678-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

