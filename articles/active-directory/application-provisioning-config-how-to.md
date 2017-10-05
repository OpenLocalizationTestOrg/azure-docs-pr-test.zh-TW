---
title: "如何設定 Azure AD 資源庫應用程式的使用者佈建 | Microsoft Docs"
description: "如何為已經列於 Azure AD 應用程式庫中的應用程式快速設定豐富的使用者帳戶佈建和解除佈建"
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
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="56a0d-103">如何設定 Azure AD 資源庫應用程式的使用者佈建</span><span class="sxs-lookup"><span data-stu-id="56a0d-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="56a0d-104">*使用者帳戶佈建*是指在應用程式的本機使用者設定檔儲存中建立、更新及/或停用使用者帳戶記錄的動作。</span><span class="sxs-lookup"><span data-stu-id="56a0d-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="56a0d-105">大部分的雲端和 SaaS 應用程式都會在自己的本機使用者設定檔儲存中儲存使用者角色和權限，而這類使用者記錄「必須」存在於其本機存放區中，才能讓單一登入和存取運作。</span><span class="sxs-lookup"><span data-stu-id="56a0d-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="56a0d-106">在 Azure 入口網站中，位於企業應用程式左側瀏覽窗格中的 [佈建] 索引標籤會顯示該應用程式支援哪些佈建模式。</span><span class="sxs-lookup"><span data-stu-id="56a0d-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="56a0d-107">這可能是下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="56a0d-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="56a0d-108">設定應用程式以進行手動佈建</span><span class="sxs-lookup"><span data-stu-id="56a0d-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="56a0d-109">「手動」佈建表示必須以手動方式使用該應用程式所提供的方法來建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="56a0d-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="56a0d-110">這可能表示登入該應用程式的系統管理員入口網站，然後使用 Web 架構使用者介面新增使用者。</span><span class="sxs-lookup"><span data-stu-id="56a0d-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="56a0d-111">或者，它可能會使用該應用程式所提供的機制，來上傳含有使用者帳戶詳細資料的試算表。</span><span class="sxs-lookup"><span data-stu-id="56a0d-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="56a0d-112">請參閱應用程式提供的文件，或洽詢應用程式開發人員以判斷有哪些機制可供使用。</span><span class="sxs-lookup"><span data-stu-id="56a0d-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="56a0d-113">如果「手動」是唯一針對指定應用程式所顯示的模式，這表示尚未針對該應用程式建立任何自動的 Azure AD 佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="56a0d-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="56a0d-114">或者，這表示應用程式不支援必要條件的使用者管理 API，而您要在該 API 上建置自動化佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="56a0d-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="56a0d-115">如果您想要求支援自動佈建指定的應用程式，可在 <http://aka.ms/aadapprequest> 上填寫要求。</span><span class="sxs-lookup"><span data-stu-id="56a0d-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="56a0d-116">設定應用程式以進行自動佈建</span><span class="sxs-lookup"><span data-stu-id="56a0d-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="56a0d-117">「自動」表示已經為此應用程式開發 Azure AD 佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="56a0d-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="56a0d-118">如需 Azure AD 佈建服務及其運作方式的詳細資訊，請參閱[自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和解除佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)。</span><span class="sxs-lookup"><span data-stu-id="56a0d-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="56a0d-119">如需如何將特定使用者和群組佈建到應用程式的相關詳細資訊，請參閱[管理企業應用程式的使用者帳戶佈建](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)。</span><span class="sxs-lookup"><span data-stu-id="56a0d-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="56a0d-120">啟用及設定自動佈建所需的實際步驟會因應用程式而有所不同。</span><span class="sxs-lookup"><span data-stu-id="56a0d-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="56a0d-121">您一開始應該先尋找設定您應用程式佈建專用的設定教學課程，然後依照這些步驟來設定應用程式和 Azure AD 以建立佈建連接。</span><span class="sxs-lookup"><span data-stu-id="56a0d-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="56a0d-122">您可以在[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)中找到應用程式教學課程。</span><span class="sxs-lookup"><span data-stu-id="56a0d-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="56a0d-123">設定佈建時必須考量的重點是，檢視和設定屬性 (Attribute) 對應，以及定義哪些使用者 (或群組) 屬性 (Property) 會從 Azure AD 流向應用程式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="56a0d-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="56a0d-124">這包括設定「比對屬性」，此屬性可用於唯一識別並比對兩個系統之間的使用者/群組。</span><span class="sxs-lookup"><span data-stu-id="56a0d-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="56a0d-125">如需這個重要程序的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="56a0d-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56a0d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56a0d-126">Next steps</span></span>
[<span data-ttu-id="56a0d-127">在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應</span><span class="sxs-lookup"><span data-stu-id="56a0d-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

