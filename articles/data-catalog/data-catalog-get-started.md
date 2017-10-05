---
title: "開始使用資料目錄 | Microsoft Docs"
description: "展示 Azure 資料目錄案例和功能的端對端教學課程。"
documentationcenter: 
services: data-catalog
author: steelanddata
manager: jhubbard
editor: 
tags: 
ms.assetid: 03332872-8d84-44a0-8a78-04fd30e14b18
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 5a3445aee7722579405b67830ca49ef8c0b29d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-catalog"></a><span data-ttu-id="0d1ec-103">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="0d1ec-103">Get started with Azure Data Catalog</span></span>
<span data-ttu-id="0d1ec-104">Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料資產的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-104">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data assets.</span></span> <span data-ttu-id="0d1ec-105">如需詳細的概觀，請參閱 [什麼是 Azure 資料目錄](data-catalog-what-is-data-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-105">For a detailed overview, see [What is Azure Data Catalog](data-catalog-what-is-data-catalog.md).</span></span>

<span data-ttu-id="0d1ec-106">本教學課程可協助您開始使用 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-106">This tutorial helps you get started with Azure Data Catalog.</span></span> <span data-ttu-id="0d1ec-107">您會在本教學課程中執行下列程序：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-107">You perform the following procedures in this tutorial:</span></span>

| <span data-ttu-id="0d1ec-108">程序</span><span class="sxs-lookup"><span data-stu-id="0d1ec-108">Procedure</span></span> | <span data-ttu-id="0d1ec-109">說明</span><span class="sxs-lookup"><span data-stu-id="0d1ec-109">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0d1ec-110">佈建資料目錄</span><span class="sxs-lookup"><span data-stu-id="0d1ec-110">Provision data catalog</span></span>](#provision-data-catalog) |<span data-ttu-id="0d1ec-111">在此程序中，您會佈建或設定 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-111">In this procedure, you provision or set up Azure Data Catalog.</span></span> <span data-ttu-id="0d1ec-112">若之前還未設定目錄，才需要執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-112">You do this step only if the catalog has not been set up before.</span></span> <span data-ttu-id="0d1ec-113">即使您有多個與 Azure 帳戶相關聯的訂用帳戶，每個組織仍只能有一個資料目錄 (Microsoft Azure Active Directory 網域)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-113">You can have only one data catalog per organization (Microsoft Azure Active Directory domain) even though there are multiple subscriptions associated with your Azure account.</span></span> |
| [<span data-ttu-id="0d1ec-114">註冊資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-114">Register data assets</span></span>](#register-data-assets) |<span data-ttu-id="0d1ec-115">在此程序中，您會使用資料目錄註冊 AdventureWorks2014 範例資料庫中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-115">In this procedure, you register data assets from the AdventureWorks2014 sample database with the data catalog.</span></span> <span data-ttu-id="0d1ec-116">註冊的過程會從資料來源中擷取重要的結構化中繼資料 (例如名稱、類型和位置)，並將該中繼資料複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-116">Registration is the process of extracting key structural metadata such as names, types, and locations from the data source and copying that metadata to the catalog.</span></span> <span data-ttu-id="0d1ec-117">資料來源及資料資產會留在原地，但目錄會利用中繼資料，讓您更輕鬆探索和了解資料來源及其資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-117">The data source and data assets remain where they are, but the metadata is used by the catalog to make them more easily discoverable and understandable.</span></span> |
| [<span data-ttu-id="0d1ec-118">探索資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-118">Discover data assets</span></span>](#discover-data-assets) |<span data-ttu-id="0d1ec-119">在此程序中，您會使用 Azure 資料目錄入口網站，探索上一個步驟所註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-119">In this procedure, you use the Azure Data Catalog portal to discover data assets that were registered in the previous step.</span></span> <span data-ttu-id="0d1ec-120">只要在 Azure 資料目錄註冊資料來源之後，其中繼資料會由此服務編製索引，讓使用者可以輕鬆地搜尋所需的資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-120">After a data source has been registered with Azure Data Catalog, its metadata is indexed by the service so that users can easily search for the data they need.</span></span> |
| [<span data-ttu-id="0d1ec-121">註解資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-121">Annotate data assets</span></span>](#annotate-data-assets) |<span data-ttu-id="0d1ec-122">在此程序中，您會提供資料資產的註解 (例如描述、標籤、文件或專家等資訊)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-122">In this procedure, you provide annotations (information such as descriptions, tags, documentation, or experts) for the data assets.</span></span> <span data-ttu-id="0d1ec-123">這項資訊可補充從資料來源擷取的中繼資料，並可讓更多人更容易了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-123">This information supplements the metadata extracted from the data source, and to make the data source more understandable to more people.</span></span> |
| [<span data-ttu-id="0d1ec-124">連線到資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-124">Connect to data assets</span></span>](#connect-to-data-assets) |<span data-ttu-id="0d1ec-125">在此程序中，您會在整合式用戶端工具 (例如 Excel 和 SQL Server Data Tools) 和非整合式工具 (SQL Server Management Studio) 中開啟資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-125">In this procedure, you open data assets in integrated client tools (such as Excel and SQL Server Data Tools) and a non-integrated tool (SQL Server Management Studio).</span></span> |
| [<span data-ttu-id="0d1ec-126">管理資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-126">Manage data assets</span></span>](#manage-data-assets) |<span data-ttu-id="0d1ec-127">在此程序中，您會設定資料資產的安全性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-127">In this procedure, you set up security for your data assets.</span></span> <span data-ttu-id="0d1ec-128">資料目錄並不會讓使用者存取資料本身。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-128">Data Catalog does not give users access to the data itself.</span></span> <span data-ttu-id="0d1ec-129">資料來源的擁有者會控制資料存取權。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-129">The owner of the data source controls data access.</span></span> <br/><br/> <span data-ttu-id="0d1ec-130">資料目錄，您可以探索資料來源，以及檢視與目錄中註冊的來源相關的 **中繼資料** 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-130">With Data Catalog, you can discover data sources and view the **metadata** related to the sources registered in the catalog.</span></span> <span data-ttu-id="0d1ec-131">不過，有時候只有特定使用者或特定群組的成員才能看到資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-131">There may be situations, however, where data sources should be visible only to specific users or to members of specific groups.</span></span> <span data-ttu-id="0d1ec-132">若是這樣的情況，您可以使用資料目錄來取得目錄中已註冊資料資產的擁有權，以及控制您擁有之資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-132">For these scenarios, you can use Data Catalog to take ownership of registered data assets within the catalog and control the visibility of the assets you own.</span></span> |
| [<span data-ttu-id="0d1ec-133">移除資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-133">Remove data assets</span></span>](#remove-data-assets) |<span data-ttu-id="0d1ec-134">在此程序中，您會了解如何移除資料目錄中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-134">In this procedure, you learn how to remove data assets from the data catalog.</span></span> |

## <a name="tutorial-prerequisites"></a><span data-ttu-id="0d1ec-135">教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="0d1ec-135">Tutorial prerequisites</span></span>
### <a name="azure-subscription"></a><span data-ttu-id="0d1ec-136">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="0d1ec-136">Azure subscription</span></span>
<span data-ttu-id="0d1ec-137">若要設定 Azure 資料目錄，您必須是 Azure 訂用帳戶的擁有者或共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-137">To set up Azure Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="0d1ec-138">Azure 訂用帳戶可協助您組織雲端服務資源的存取權，例如 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-138">Azure subscriptions help you organize access to cloud service resources like Azure Data Catalog.</span></span> <span data-ttu-id="0d1ec-139">它們也可協助您控制如何根據資源使用量產生報告、計費及付費。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-139">They also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="0d1ec-140">每一個訂用帳戶可以有不同的計費和付款設定，因此，依照部門、專案、區域辦事處等，您可以有不同的訂用帳戶和不同的計劃。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-140">Each subscription can have a different billing and payment setup, so you can have different subscriptions and different plans by department, project, regional office, and so on.</span></span> <span data-ttu-id="0d1ec-141">每一個雲端服務都屬於某個訂用帳戶，在設定 Azure 資料目錄之前，您必須先有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-141">Every cloud service belongs to a subscription, and you need to have a subscription before setting up Azure Data Catalog.</span></span> <span data-ttu-id="0d1ec-142">若要深入了解，請參閱 [管理帳戶、訂用帳戶及管理角色](../active-directory/active-directory-how-subscriptions-associated-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-142">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

<span data-ttu-id="0d1ec-143">如果您沒有訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-143">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0d1ec-144">請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-144">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/) for details.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="0d1ec-145">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d1ec-145">Azure Active Directory</span></span>
<span data-ttu-id="0d1ec-146">若要設定 Azure 資料目錄，您必須使用 Azure Active Directory (Azure AD) 使用者帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-146">To set up Azure Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span> <span data-ttu-id="0d1ec-147">您必須是 Azure 訂用帳戶的擁有者或共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-147">You must be the owner or co-owner of an Azure subscription.</span></span>  

<span data-ttu-id="0d1ec-148">Azure AD 提供了簡單的方法，讓您的企業無論能輕鬆地管理雲端和內部部署中的身分識別與存取權。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-148">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="0d1ec-149">您可以使用單一公司帳戶或學校帳戶，登入任何雲端或內部部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-149">You can use a single work or school account to sign in to any cloud or on-premises web application.</span></span> <span data-ttu-id="0d1ec-150">Azure 資料目錄採用 Azure AD 來驗證登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-150">Azure Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="0d1ec-151">若要深入了解，請參閱 [什麼是 Azure Active Directory](../active-directory/active-directory-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-151">To learn more, see [What is Azure Active Directory](../active-directory/active-directory-whatis.md).</span></span>

### <a name="azure-active-directory-policy-configuration"></a><span data-ttu-id="0d1ec-152">Azure Active Directory 原則組態</span><span class="sxs-lookup"><span data-stu-id="0d1ec-152">Azure Active Directory policy configuration</span></span>
<span data-ttu-id="0d1ec-153">您可能會遇到一種情況，您可以登入 Azure 資料目錄入口網站，但在您嘗試登入資料來源註冊工具時，您會遇到錯誤訊息，導致您無法登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-153">You may encounter a situation where you can sign in to the Azure Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="0d1ec-154">當您在公司網路，或從公司網路外部連線時，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-154">This error may occur when you are on the company network or when you are connecting from outside the company network.</span></span>

<span data-ttu-id="0d1ec-155">註冊工具會使用「表單驗證」  ，根據 Azure Active Directory 驗證使用者登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-155">The registration tool uses *forms authentication* to validate user sign-ins against Azure Active Directory.</span></span> <span data-ttu-id="0d1ec-156">Azure Active Directory 系統管理員必須在「全域驗證原則」 中啟用表單驗證，才會成功登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-156">For successful sign-in, an Azure Active Directory administrator must enable forms authentication in the *global authentication policy*.</span></span>

<span data-ttu-id="0d1ec-157">利用全域驗證原則，您可以分別為內部網路和外部網路連線啟用驗證方法，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-157">With the global authentication policy, you can enable authentication separately for intranet and extranet connections, as shown in the following image.</span></span> <span data-ttu-id="0d1ec-158">如果您連線的網路未啟用表單驗證，可能會發生登入錯誤。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-158">Sign-in errors may occur if forms authentication is not enabled for the network from which you're connecting.</span></span>

 ![Azure Active Directory 全域驗證原則](./media/data-catalog-prerequisites/global-auth-policy.png)

<span data-ttu-id="0d1ec-160">如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-160">For more information, see [Configuring authentication policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

## <a name="provision-data-catalog"></a><span data-ttu-id="0d1ec-161">佈建資料目錄</span><span class="sxs-lookup"><span data-stu-id="0d1ec-161">Provision data catalog</span></span>
<span data-ttu-id="0d1ec-162">每個組織只能佈建一個資料目錄 (Azure Active Directory 網域)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-162">You can provision only one data catalog per organization (Azure Active Directory domain).</span></span> <span data-ttu-id="0d1ec-163">因此，如果隸屬於這個 Azure Active Directory 網域的 Azure 訂用帳戶擁有者或共同擁有者已建立目錄，即使您有多個 Azure 訂用帳戶，仍無法再次建立目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-163">Therefore, if the owner or co-owner of an Azure subscription who belongs to this Azure Active Directory domain has already created a catalog, you will not be able to create a catalog again even if you have multiple Azure subscriptions.</span></span> <span data-ttu-id="0d1ec-164">若要測試 Azure Active Directory 網域中的使用者是否已建立資料目錄，請移至 [Azure 資料目錄首頁](http://azuredatacatalog.com) 並確認您是否看到目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-164">To test whether a data catalog has been created by a user in your Azure Active Directory domain, go to the [Azure Data Catalog home page](http://azuredatacatalog.com) and verify whether you see the catalog.</span></span> <span data-ttu-id="0d1ec-165">如果您的目錄已建立，請略過下列程序並前往下一節。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-165">If a catalog has already been created for you, skip the following procedure and go to the next section.</span></span>    

1. <span data-ttu-id="0d1ec-166">移至[資料目錄服務頁面](https://azure.microsoft.com/services/data-catalog)並按一下 [開始使用]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-166">Go to the [Data Catalog service page](https://azure.microsoft.com/services/data-catalog) and click **Get started**.</span></span>
   
    ![Azure 資料目錄--行銷登陸頁面](media/data-catalog-get-started/data-catalog-marketing-landing-page.png)
2. <span data-ttu-id="0d1ec-168">使用屬於 Azure 訂用帳戶擁有者或共同擁有者的使用者帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-168">Sign in with a user account that is the owner or co-owner of an Azure subscription.</span></span> <span data-ttu-id="0d1ec-169">您會在登入後看到下列頁面。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-169">You see the following page after signing in.</span></span>
   
    ![Azure 資料目錄--佈建資料目錄](media/data-catalog-get-started/data-catalog-create-azure-data-catalog.png)
3. <span data-ttu-id="0d1ec-171">指定 [資料目錄名稱]、想要使用的 [訂用帳戶] 和 [目錄位置]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-171">Specify a **name** for the data catalog, the **subscription** you want to use, and the **location** for the catalog.</span></span>
4. <span data-ttu-id="0d1ec-172">展開 [價格]，並選取 Azure 資料目錄的**版本** (免費或標準)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-172">Expand **Pricing** and select an Azure Data Catalog **edition** (Free or Standard).</span></span>
    <span data-ttu-id="0d1ec-173">![Azure 資料目錄--選取版本](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)</span><span class="sxs-lookup"><span data-stu-id="0d1ec-173">![Azure Data Catalog--select edition](media/data-catalog-get-started/data-catalog-create-catalog-select-edition.png)</span></span>
5. <span data-ttu-id="0d1ec-174">展開 [目錄使用者]，然後按一下 [新增] 以新增資料目錄的使用者。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-174">Expand **Catalog Users** and click **Add** to add users for the data catalog.</span></span> <span data-ttu-id="0d1ec-175">系統會自動將您新增至此群組。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-175">You are automatically added to this group.</span></span>
    <span data-ttu-id="0d1ec-176">![Azure 資料目錄--使用者](media/data-catalog-get-started/data-catalog-add-catalog-user.png)</span><span class="sxs-lookup"><span data-stu-id="0d1ec-176">![Azure Data Catalog--users](media/data-catalog-get-started/data-catalog-add-catalog-user.png)</span></span>
6. <span data-ttu-id="0d1ec-177">展開 [目錄管理員]，然後按一下 [新增] 以新增資料目錄的其他管理員。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-177">Expand **Catalog Administrators** and click **Add** to add additional administrators for the data catalog.</span></span> <span data-ttu-id="0d1ec-178">系統會自動將您新增至此群組。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-178">You are automatically added to this group.</span></span>
    <span data-ttu-id="0d1ec-179">![Azure 資料目錄--系統管理員](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)</span><span class="sxs-lookup"><span data-stu-id="0d1ec-179">![Azure Data Catalog--administrators](media/data-catalog-get-started/data-catalog-add-catalog-admins.png)</span></span>
7. <span data-ttu-id="0d1ec-180">按一下 [建立目錄]  以建立組織的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-180">Click **Create Catalog** to create the data catalog for your organization.</span></span> <span data-ttu-id="0d1ec-181">建立資料目錄後，您就會看到其首頁。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-181">You see the home page for the data catalog after it is created.</span></span>
    <span data-ttu-id="0d1ec-182">![Azure 資料目錄--已建立](media/data-catalog-get-started/data-catalog-created.png)</span><span class="sxs-lookup"><span data-stu-id="0d1ec-182">![Azure Data Catalog--created](media/data-catalog-get-started/data-catalog-created.png)</span></span>    

### <a name="find-a-data-catalog-in-the-azure-portal"></a><span data-ttu-id="0d1ec-183">在 Azure 入口網站中尋找資料目錄</span><span class="sxs-lookup"><span data-stu-id="0d1ec-183">Find a data catalog in the Azure portal</span></span>
1. <span data-ttu-id="0d1ec-184">在網頁瀏覽器的另一個索引標籤中或在不同的網頁瀏覽器視窗中，移至 [Azure 入口網站](https://portal.azure.com) ，然後使用您在上一個步驟中用來建立資料目錄的相同帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-184">On a separate tab in the web browser or in a separate web browser window, go to the [Azure portal](https://portal.azure.com) and sign in with the same account that you used to create the data catalog in the previous step.</span></span>
2. <span data-ttu-id="0d1ec-185">依序選取 [瀏覽]，然後按一下 [資料目錄]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-185">Select **Browse** and then click **Data Catalog**.</span></span>
   
    <span data-ttu-id="0d1ec-186">![Azure 資料目錄--瀏覽 Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) 您會看到您所建立的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-186">![Azure Data Catalog--browse Azure](media/data-catalog-get-started/data-catalog-browse-azure-portal.png) You see the data catalog you created.</span></span>
   
    ![Azure 資料目錄--檢視清單中的目錄](media/data-catalog-get-started/data-catalog-azure-portal-show-catalog.png)
3. <span data-ttu-id="0d1ec-188">按一下您建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-188">Click the catalog that you created.</span></span> <span data-ttu-id="0d1ec-189">您會在入口網站中看到 [資料目錄]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-189">You see the **Data Catalog** blade in the portal.</span></span>
   
   ![<span data-ttu-id="0d1ec-190">Azure 資料目錄--入口網站中的刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="0d1ec-190">Azure Data Catalog--blade in portal</span></span> ](media/data-catalog-get-started/data-catalog-blade-azure-portal.png)
4. <span data-ttu-id="0d1ec-191">您可以檢視資料目錄的屬性並加以更新。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-191">You can view properties of the data catalog and update them.</span></span> <span data-ttu-id="0d1ec-192">例如，按一下 [定價層]  並變更版本。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-192">For example, click **Pricing tier** and change the edition.</span></span>
   
    ![Azure 資料目錄--定價層](media/data-catalog-get-started/data-catalog-change-pricing-tier.png)

### <a name="adventure-works-sample-database"></a><span data-ttu-id="0d1ec-194">Adventure Works 範例資料庫</span><span class="sxs-lookup"><span data-stu-id="0d1ec-194">Adventure Works sample database</span></span>
<span data-ttu-id="0d1ec-195">在本教學課程中，您會註冊 AdventureWorks2014 範例資料庫中用於 SQL Server Database Engine 的資料資產 (資料表)，但如果您想使用熟悉且與角色相關的資料，也可以使用任何支援的資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-195">In this tutorial, you register data assets (tables) from the AdventureWorks2014 sample database for the SQL Server Database Engine, but you can use any supported data source if you would prefer to work with data that is familiar and relevant to your role.</span></span> <span data-ttu-id="0d1ec-196">如需支援的資料來源清單，請參閱 [支援的資料來源](data-catalog-dsr.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-196">For a list of supported data sources, see [Supported data sources](data-catalog-dsr.md).</span></span>

### <a name="install-the-adventure-works-2014-oltp-database"></a><span data-ttu-id="0d1ec-197">安裝 Adventure Works 2014 OLTP 資料庫</span><span class="sxs-lookup"><span data-stu-id="0d1ec-197">Install the Adventure Works 2014 OLTP database</span></span>
<span data-ttu-id="0d1ec-198">Adventure Works 資料庫支援一家虛構自行車製造商 (Adventure Works Cycles) 的標準線上交易處理案例，包括產品、銷售和採購。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-198">The Adventure Works database supports standard online transaction-processing scenarios for a fictitious bicycle manufacturer (Adventure Works Cycles), which includes products, sales, and purchasing.</span></span> <span data-ttu-id="0d1ec-199">在本教學課程中，您會在 Azure 資料目錄中註冊產品資訊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-199">In this tutorial, you register information about products into Azure Data Catalog.</span></span>

<span data-ttu-id="0d1ec-200">若要安裝 Adventure Works 範例資料庫：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-200">To install the Adventure Works sample database:</span></span>

1. <span data-ttu-id="0d1ec-201">下載 CodePlex 上的 [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-201">Download [Adventure Works 2014 Full Database Backup.zip](https://msftdbprodsamples.codeplex.com/downloads/get/880661) on CodePlex.</span></span>
2. <span data-ttu-id="0d1ec-202">若要在機器上還原資料庫，請依照 [SQL Server Management Studio 還原資料庫備份](http://msdn.microsoft.com/library/ms177429.aspx)中的指示，或依照下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-202">To restore the database on your machine, follow the instructions in [Restore a Database Backup by using SQL Server Management Studio](http://msdn.microsoft.com/library/ms177429.aspx), or by following these steps:</span></span>
   1. <span data-ttu-id="0d1ec-203">開啟 SQL Server Management Studio，然後連線到 SQL Server Database Engine。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-203">Open SQL Server Management Studio and connect to the SQL Server Database Engine.</span></span>
   2. <span data-ttu-id="0d1ec-204">以滑鼠右鍵按一下 [資料庫]，然後按一下 [還原資料庫]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-204">Right-click **Databases** and click **Restore Database**.</span></span>
   3. <span data-ttu-id="0d1ec-205">在 [還原資料庫] 之下，按一下 [來源]的 [裝置] 選項，然後按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-205">Under **Restore Database**, click the **Device** option for **Source** and click **Browse**.</span></span>
   4. <span data-ttu-id="0d1ec-206">在 [選取備份裝置] 之下，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-206">Under **Select backup devices**, click **Add**.</span></span>
   5. <span data-ttu-id="0d1ec-207">移至具有 **AdventureWorks2014.bak** 檔案的資料夾、選取檔案，然後按一下 [確定] 以關閉 [尋找備份檔案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-207">Go to the folder where you have the **AdventureWorks2014.bak** file, select the file, and click **OK** to close the **Locate Backup File** dialog box.</span></span>
   6. <span data-ttu-id="0d1ec-208">按一下 [確定] 以關閉 [選取備份裝置] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-208">Click **OK** to close the **Select backup devices** dialog box.</span></span>    
   7. <span data-ttu-id="0d1ec-209">按一下 [確定] 以關閉 [還原資料庫] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-209">Click **OK** to close the **Restore Database** dialog box.</span></span>

<span data-ttu-id="0d1ec-210">您現在可以使用 Azure 資料目錄註冊 Adventure Works 範例資料庫中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-210">You can now register data assets from the Adventure Works sample database by using Azure Data Catalog.</span></span>

## <a name="register-data-assets"></a><span data-ttu-id="0d1ec-211">註冊資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-211">Register data assets</span></span>
<span data-ttu-id="0d1ec-212">在本練習中，您可以透過註冊工具，使用目錄註冊 Adventure Works 資料庫中的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-212">In this exercise, you use the registration tool to register data assets from the Adventure Works database with the catalog.</span></span> <span data-ttu-id="0d1ec-213">註冊的過程會從資料來源及其包含的資產中，擷取重要的結構化中繼資料 (例如名稱、類型和位置)，並將該中繼資料複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-213">Registration is the process of extracting key structural metadata such as names, types, and locations from the data source and the assets it contains, and copying that metadata to the catalog.</span></span> <span data-ttu-id="0d1ec-214">資料來源及資料資產會留在原地，但目錄會利用中繼資料，讓您更輕鬆探索和了解資料來源及其資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-214">The data source and data assets remain where they are, but the metadata is used by the catalog to make them more easily discoverable and understandable.</span></span>

### <a name="register-a-data-source"></a><span data-ttu-id="0d1ec-215">註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="0d1ec-215">Register a data source</span></span>
1. <span data-ttu-id="0d1ec-216">移至 [Azure 資料目錄首頁](http://azuredatacatalog.com)，然後按一下 [發佈資料]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-216">Go to the [Azure Data Catalog home page](http://azuredatacatalog.com) and click **Publish Data**.</span></span>
   
   ![Azure 資料目錄--發佈資料按鈕](media/data-catalog-get-started/data-catalog-publish-data.png)
2. <span data-ttu-id="0d1ec-218">按一下 [啟動應用程式]  以在電腦上下載、安裝及執行註冊工具。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-218">Click **Launch Application** to download, install, and run the registration tool on your computer.</span></span>
   
   ![Azure 資料目錄--啟動按鈕](media/data-catalog-get-started/data-catalog-launch-application.png)
3. <span data-ttu-id="0d1ec-220">在 [歡迎使用] 頁面上，按一下 [登入]，並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-220">On the **Welcome** page, click **Sign in** and enter your credentials.</span></span>     
   
    ![Azure 資料目錄--歡迎使用頁面](media/data-catalog-get-started/data-catalog-welcome-dialog.png)
4. <span data-ttu-id="0d1ec-222">在 [Microsoft Azure 資料目錄] 頁面上，按一下 [SQL Server] 和 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-222">On the **Microsoft Azure Data Catalog** page, click **SQL Server** and **Next**.</span></span>
   
    ![Azure 資料目錄--資料來源](media/data-catalog-get-started/data-catalog-data-sources.png)
5. <span data-ttu-id="0d1ec-224">輸入適用於 **AdventureWorks2014** 的 SQL Server 連線屬性 (請參閱下列範例)，再按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-224">Enter the SQL Server connection properties for **AdventureWorks2014** (see the following example) and click **CONNECT**.</span></span>
   
   ![Azure 資料目錄--SQL Server 連線設定](media/data-catalog-get-started/data-catalog-sql-server-connection.png)
6. <span data-ttu-id="0d1ec-226">為您的資料資產註冊中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-226">Register the metadata of your data asset.</span></span> <span data-ttu-id="0d1ec-227">在此範例中，您將註冊 AdventureWorks Production 命名空間中的 **Production/Product** 物件：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-227">In this example, you register **Production/Product** objects from the AdventureWorks Production namespace:</span></span>
   
   1. <span data-ttu-id="0d1ec-228">在 [伺服器階層] 樹狀結構中展開 [AdventureWorks2014]，然後按一下 [Production]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-228">In the **Server Hierarchy** tree, expand **AdventureWorks2014** and click **Production**.</span></span>
   2. <span data-ttu-id="0d1ec-229">按住 CTRL 鍵並按一下滑鼠，選取 [Product]、[ProductCategory]、[ProductDescription] 和 [ProductPhoto]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-229">Select **Product**, **ProductCategory**, **ProductDescription**, and **ProductPhoto** by using Ctrl+click.</span></span>
   3. <span data-ttu-id="0d1ec-230">按一下**移動選取項目箭號** (**>**)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-230">Click the **move selected arrow** (**>**).</span></span> <span data-ttu-id="0d1ec-231">此動作會將所有選取的物件移至 [準備註冊的物件]  清單。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-231">This action moves all selected objects into the **Objects to be registered** list.</span></span>
      
      ![Azure 資料目錄教學課程--瀏覽並選取物件](media/data-catalog-get-started/data-catalog-server-hierarchy.png)
   4. <span data-ttu-id="0d1ec-233">選取 [包含預覽]  以包含資料的快照預覽。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-233">Select **Include a Preview** to include a snapshot preview of the data.</span></span> <span data-ttu-id="0d1ec-234">快照中會包含最多 20 筆來自各個資料表的記錄，並且會複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-234">The snapshot includes up to 20 records from each table, and it is copied into the catalog.</span></span>
   5. <span data-ttu-id="0d1ec-235">選取 [包含資料設定檔]  以包含資料設定檔的物件統計資料快照 (例如︰資料行的最小值、最大值和平均值以及資料列數目)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-235">Select **Include Data Profile** to include a snapshot of the object statistics for the data profile (for example: minimum, maximum, and average values for a column, number of rows).</span></span>
   6. <span data-ttu-id="0d1ec-236">在 [新增標籤] 欄位中輸入 **adventure works, cycles**。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-236">In the **Add tags** field, enter **adventure works, cycles**.</span></span> <span data-ttu-id="0d1ec-237">此動作會新增這些資料資產的搜尋標籤。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-237">This action adds search tags for these data assets.</span></span> <span data-ttu-id="0d1ec-238">標記可協助使用者尋找已註冊的資料來源，非常有用。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-238">Tags are a great way to help users find a registered data source.</span></span>
   7. <span data-ttu-id="0d1ec-239">指定此資料之 **專家** 的名稱 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-239">Specify the name of an **expert** on this data (optional).</span></span>
      
      ![Azure 資料目錄教學課程--要註冊的物件](media/data-catalog-get-started/data-catalog-objects-register.png)
   8. <span data-ttu-id="0d1ec-241">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-241">Click **REGISTER**.</span></span> <span data-ttu-id="0d1ec-242">Azure 資料目錄會註冊您選取的物件。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-242">Azure Data Catalog registers your selected objects.</span></span> <span data-ttu-id="0d1ec-243">本練習中會註冊從 Adventure Works 選取的物件。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-243">In this exercise, the selected objects from Adventure Works are registered.</span></span> <span data-ttu-id="0d1ec-244">註冊工具會從資料資產擷取中繼資料，並將該資料複製到 Azure 資料目錄服務。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-244">The registration tool extracts metadata from the data asset and copies that data into the Azure Data Catalog service.</span></span> <span data-ttu-id="0d1ec-245">資料會保留在它目前的位置，並且仍然在目前系統的系統管理員及原則的控制之下。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-245">The data remains where it currently resides, and it remains under the control of the administrators and policies of the current system.</span></span>
      
      ![Azure 資料目錄--已註冊的物件](media/data-catalog-get-started/data-catalog-registered-objects.png)
   9. <span data-ttu-id="0d1ec-247">若要查看您註冊的資料來源物件，請按一下 [檢視入口網站] 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-247">To see your registered data source objects, click **View Portal**.</span></span> <span data-ttu-id="0d1ec-248">在 Azure 資料目錄入口網站中，確認您有在資料格檢視中看到全部這四個資料表和資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-248">In the Azure Data Catalog portal, confirm that you see all four tables and the database in the grid view.</span></span>
      
      ![<span data-ttu-id="0d1ec-249">Azure 資料目錄入口網站中的物件</span><span class="sxs-lookup"><span data-stu-id="0d1ec-249">Objects in the Azure Data Catalog portal</span></span> ](media/data-catalog-get-started/data-catalog-view-portal.png)

<span data-ttu-id="0d1ec-250">在本練習中，您註冊 Adventure Works 範例資料庫中的物件，讓整個組織裡的使用者可以輕鬆找到它們。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-250">In this exercise, you registered objects from the Adventure Works sample database so that they can be easily discovered by users across your organization.</span></span> <span data-ttu-id="0d1ec-251">在下一個練習中，您將學習如何探索已註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-251">In the next exercise, you learn how to discover registered data assets.</span></span>

## <a name="discover-data-assets"></a><span data-ttu-id="0d1ec-252">探索資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-252">Discover data assets</span></span>
<span data-ttu-id="0d1ec-253">在 Azure 資料目錄探索資料會使用兩種主要機制：搜尋和篩選。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-253">Discovery in Azure Data Catalog uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="0d1ec-254">搜尋的設計兼具直覺與強大的功能。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-254">Searching is designed to be both intuitive and powerful.</span></span> <span data-ttu-id="0d1ec-255">根據預設，搜尋字詞會比對目錄中的所有內容，包括使用者提供的註解。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-255">By default, search terms are matched against any property in the catalog, including user-provided annotations.</span></span>

<span data-ttu-id="0d1ec-256">篩選的設計則與搜尋互補。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-256">Filtering is designed to complement searching.</span></span> <span data-ttu-id="0d1ec-257">您可以選取特定特性，例如專家、資料來源類型、物件類型和標記，來檢視相符的資料資產並將搜尋結果限制為相符的資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-257">You can select specific characteristics such as experts, data source type, object type, and tags to view matching data assets and to constrain search results to matching assets.</span></span>

<span data-ttu-id="0d1ec-258">透過結合使用搜尋和篩選，您可以快速瀏覽已經向 Azure 資料目錄註冊的資料來源，以探索所需的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-258">By using a combination of searching and filtering, you can quickly navigate the data sources that have been registered with Azure Data Catalog to discover the data assets you need.</span></span>

<span data-ttu-id="0d1ec-259">在本練習中，您會使用 Azure 資料目錄入口網站，探索您在上一個練習中註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-259">In this exercise, you use the Azure Data Catalog portal to discover data assets you registered in the previous exercise.</span></span> <span data-ttu-id="0d1ec-260">如需搜尋語法的詳細資料，請參閱 [資料目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-260">See [Data Catalog Search syntax reference](https://msdn.microsoft.com/library/azure/mt267594.aspx) for details about search syntax.</span></span>

<span data-ttu-id="0d1ec-261">以下是幾個探索目錄中資料資產的範例。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-261">Following are a few examples for discovering data assets in the catalog.</span></span>  

### <a name="discover-data-assets-with-basic-search"></a><span data-ttu-id="0d1ec-262">利用基本搜尋探索資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-262">Discover data assets with basic search</span></span>
<span data-ttu-id="0d1ec-263">基本搜尋可協助您使用一或多個搜尋字詞搜尋目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-263">Basic search helps you search a catalog by using one or more search terms.</span></span> <span data-ttu-id="0d1ec-264">結果包含了任何與一或多個指定字詞的內容相符的資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-264">Results are any assets that match on any property with one or more of the terms specified.</span></span>

1. <span data-ttu-id="0d1ec-265">按一下 Azure 資料目錄入口網站中的 [首頁]  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-265">Click **Home** in the Azure Data Catalog portal.</span></span> <span data-ttu-id="0d1ec-266">如果您已關閉網頁瀏覽器，請移至 [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-266">If you have closed the web browser, go to the [Azure Data Catalog home page](https://www.azuredatacatalog.com).</span></span>
2. <span data-ttu-id="0d1ec-267">在搜尋方塊中輸入 `cycles` ，然後按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-267">In the search box, enter `cycles` and press **ENTER**.</span></span>
   
    ![Azure 資料目錄--基本文字搜尋](media/data-catalog-get-started/data-catalog-basic-text-search.png)
3. <span data-ttu-id="0d1ec-269">確認您有在結果中看到全部四個資料表和資料庫 (AdventureWorks2014)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-269">Confirm that you see all four tables and the database (AdventureWorks2014) in the results.</span></span> <span data-ttu-id="0d1ec-270">您可以按一下工具列上的按鈕切換**資料格檢視**和**清單檢視**，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-270">You can switch between **grid view** and **list view** by clicking buttons on the toolbar as shown in the following image.</span></span> <span data-ttu-id="0d1ec-271">請注意，[醒目提示] 選項為 [開啟] 狀態，因此搜尋結果中會醒目提示搜尋關鍵字。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-271">Notice that the search keyword is highlighted in the search results because the **Highlight** option is **ON**.</span></span> <span data-ttu-id="0d1ec-272">您也可以指定搜尋結果的 [每頁顯示的結果]  數目。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-272">You can also specify the number of **results per page** in search results.</span></span>
   
    ![Azure 資料目錄--基本文字搜尋結果](media/data-catalog-get-started/data-catalog-basic-text-search-results.png)
   
    <span data-ttu-id="0d1ec-274">[搜尋] 面板位於左邊，而 [屬性] 面板位於右邊。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-274">The **Searches** panel is on the left and the **Properties** panel is on the right.</span></span> <span data-ttu-id="0d1ec-275">在 [搜尋]  面板上，您可以變更搜尋條件和篩選結果。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-275">On the **Searches** panel, you can change search criteria and filter results.</span></span> <span data-ttu-id="0d1ec-276">[屬性]  面板會顯示資料格或清單中所選物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-276">The **Properties** panel displays properties of a selected object in the grid or list.</span></span>
4. <span data-ttu-id="0d1ec-277">按一下搜尋結果中的 [Product]  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-277">Click **Product** in the search results.</span></span> <span data-ttu-id="0d1ec-278">按一下 [預覽]、[資料行]、[資料設定檔] 和 [文件] 索引標籤，或按一下箭號以展開底部窗格。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-278">Click the **Preview**, **Columns**, **Data Profile**, and **Documentation** tabs, or click the arrow to expand the bottom pane.</span></span>  
   
    ![Azure 資料目錄--底部窗格](media/data-catalog-get-started/data-catalog-data-asset-preview.png)
   
    <span data-ttu-id="0d1ec-280">在 [預覽] 索引標籤上，您會看到 **Product** 資料表資料的預覽。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-280">On the **Preview** tab, you see a preview of the data in the **Product** table.</span></span>  
5. <span data-ttu-id="0d1ec-281">按一下 [資料行] 索引標籤，可尋找有關資料資產資料行的詳細資料 (例如**名稱**和**資料類型**)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-281">Click the **Columns** tab to find details about columns (such as **name** and **data type**) in the data asset.</span></span>
6. <span data-ttu-id="0d1ec-282">按一下 [資料設定檔]  索引標籤，可查看資料資產中資料的分析 (例如︰資料列數目、資料大小或資料行中的最小值)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-282">Click the **Data Profile** tab to see the profiling of data (for example: number of rows, size of data, or minimum value in a column) in the data asset.</span></span>
7. <span data-ttu-id="0d1ec-283">使用左邊的 [篩選]  篩選結果。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-283">Filter the results by using **Filters** on the left.</span></span> <span data-ttu-id="0d1ec-284">例如，針對 [物件類型] 按一下 [資料表]，您只會看到四個資料表，而不會看到資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-284">For example, click **Table** for **Object Type**, and you see only the four tables, not the database.</span></span>
   
    ![Azure 資料目錄--篩選搜尋結果](media/data-catalog-get-started/data-catalog-filter-search-results.png)

### <a name="discover-data-assets-with-property-scoping"></a><span data-ttu-id="0d1ec-286">利用屬性範圍探索資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-286">Discover data assets with property scoping</span></span>
<span data-ttu-id="0d1ec-287">屬性範圍可協助您探索搜尋字詞符合指定屬性的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-287">Property scoping helps you discover data assets where the search term is matched with the specified property.</span></span>

1. <span data-ttu-id="0d1ec-288">清除 [篩選]中 [物件類型] 底下的 [資料表] 篩選。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-288">Clear the **Table** filter under **Object Type** in **Filters**.</span></span>  
2. <span data-ttu-id="0d1ec-289">在搜尋方塊中輸入 `tags:cycles` ，然後按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-289">In the search box, enter `tags:cycles` and press **ENTER**.</span></span> <span data-ttu-id="0d1ec-290">請參閱 [資料目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx) ，以取得用來搜尋資料目錄的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-290">See [Data Catalog Search syntax reference](https://msdn.microsoft.com/library/azure/mt267594.aspx) for all the properties you can use for searching the data catalog.</span></span>
3. <span data-ttu-id="0d1ec-291">確認您有在結果中看到全部四個資料表和資料庫 (AdventureWorks2014)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-291">Confirm that you see all four tables and the database (AdventureWorks2014) in the results.</span></span>  
   
    ![資料目錄--屬性範圍搜尋結果](media/data-catalog-get-started/data-catalog-property-scoping-results.png)

### <a name="save-the-search"></a><span data-ttu-id="0d1ec-293">儲存搜尋</span><span class="sxs-lookup"><span data-stu-id="0d1ec-293">Save the search</span></span>
1. <span data-ttu-id="0d1ec-294">在 [目前搜尋] 區段的 [搜尋] 窗格中，輸入搜尋的名稱並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-294">In the **Searches** pane in the **Current Search** section, enter a name for the search and click **Save**.</span></span>
   
    ![Azure 資料目錄--儲存搜尋](media/data-catalog-get-started/data-catalog-save-search.png)
2. <span data-ttu-id="0d1ec-296">確認已儲存的搜尋顯示在 [已儲存的搜尋] 底下。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-296">Confirm that the saved search shows up under **Saved Searches**.</span></span>
   
    ![Azure 資料目錄--已儲存的搜尋](media/data-catalog-get-started/data-catalog-saved-search.png)
3. <span data-ttu-id="0d1ec-298">選取您可以對已儲存的搜尋採取的動作 ([重新命名]、[刪除]、[設定為預設值] 搜尋)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-298">Select one of the actions you can take on the saved search (**Rename**, **Delete**, **Save As Default** search).</span></span>
   
    ![Azure 資料目錄--已儲存的搜尋選項](media/data-catalog-get-started/data-catalog-saved-search-options.png)

### <a name="boolean-operators"></a><span data-ttu-id="0d1ec-300">布林運算子</span><span class="sxs-lookup"><span data-stu-id="0d1ec-300">Boolean operators</span></span>
<span data-ttu-id="0d1ec-301">您可以使用布林運算子來擴大或縮小搜尋範圍。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-301">You can broaden or narrow your search with Boolean operators.</span></span>

1. <span data-ttu-id="0d1ec-302">在搜尋方塊中輸入 `tags:cycles AND objectType:table`，然後按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-302">In the search box, enter `tags:cycles AND objectType:table`, and press **ENTER**.</span></span>
2. <span data-ttu-id="0d1ec-303">確認您在結果中只看到資料表，而未看到資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-303">Confirm that you see only tables (not the database) in the results.</span></span>  
   
    ![Azure 資料目錄--搜尋中的布林運算子](media/data-catalog-get-started/data-catalog-search-boolean-operator.png)

### <a name="grouping-with-parentheses"></a><span data-ttu-id="0d1ec-305">使用括號分組</span><span class="sxs-lookup"><span data-stu-id="0d1ec-305">Grouping with parentheses</span></span>
<span data-ttu-id="0d1ec-306">使用括號進行分組，您即可將一部分的查詢分組以達到邏輯隔離 (尤其是搭配布林運算子)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-306">By grouping with parentheses, you can group parts of the query to achieve logical isolation, especially along with Boolean operators.</span></span>

1. <span data-ttu-id="0d1ec-307">在搜尋方塊中輸入 `name:product AND (tags:cycles AND objectType:table)` ，然後按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-307">In the search box, enter `name:product AND (tags:cycles AND objectType:table)` and press **ENTER**.</span></span>
2. <span data-ttu-id="0d1ec-308">確認您只在搜尋結果中看到 **Product** 資料表。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-308">Confirm that you see only the **Product** table in the search results.</span></span>
   
    ![Azure 資料目錄--群組搜尋](media/data-catalog-get-started/data-catalog-grouping-search.png)   

### <a name="comparison-operators"></a><span data-ttu-id="0d1ec-310">比較運算子</span><span class="sxs-lookup"><span data-stu-id="0d1ec-310">Comparison operators</span></span>
<span data-ttu-id="0d1ec-311">使用比較運算子，您可以針對具有數值和日期資料類型的屬性使用比較而非相等。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-311">With comparison operators, you can use comparisons other than equality for properties that have numeric and date data types.</span></span>

1. <span data-ttu-id="0d1ec-312">在搜尋方塊中，輸入 `lastRegisteredTime:>"06/09/2016"`。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-312">In the search box, enter `lastRegisteredTime:>"06/09/2016"`.</span></span>
2. <span data-ttu-id="0d1ec-313">清除 [物件類型] 底下的 [資料表] 篩選。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-313">Clear the **Table** filter under **Object Type**.</span></span>
3. <span data-ttu-id="0d1ec-314">按 **ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-314">Press **ENTER**.</span></span>
4. <span data-ttu-id="0d1ec-315">確認您在搜尋結果中有看到已註冊的 **Product**、**ProductCategory**、**ProductDescription** 和 **ProductPhoto** 資料表以及 AdventureWorks2014 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-315">Confirm that you see the **Product**, **ProductCategory**, **ProductDescription**, and **ProductPhoto** tables and the AdventureWorks2014 database you registered in search results.</span></span>
   
    ![Azure 資料目錄--比較搜尋結果](media/data-catalog-get-started/data-catalog-comparison-operator-results.png)

<span data-ttu-id="0d1ec-317">如需關於探索資料資產的詳細資訊，請參閱[如何探索資料資產](data-catalog-how-to-discover.md)，搜尋語法則請參閱[資料目錄搜尋語法參考](https://msdn.microsoft.com/library/azure/mt267594.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-317">See [How to discover data assets](data-catalog-how-to-discover.md) for detailed information about discovering data assets and [Data Catalog Search syntax reference](https://msdn.microsoft.com/library/azure/mt267594.aspx) for search syntax.</span></span>

## <a name="annotate-data-assets"></a><span data-ttu-id="0d1ec-318">註解資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-318">Annotate data assets</span></span>
<span data-ttu-id="0d1ec-319">在本練習中，您將使用 Azure 資料目錄入口網站，註解先前在目錄中註冊的資料資產 (新增描述、標記或專家等資訊)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-319">In this exercise, you use the Azure Data Catalog portal to annotate (add information such as descriptions, tags, or experts) data assets you have previously registered in the catalog.</span></span> <span data-ttu-id="0d1ec-320">註解可補充並增強在註冊期間擷取自資料來源的結構化中繼資料，而更容易探索和了解資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-320">The annotations supplement and enhance the structural metadata extracted from the data source during registration and makes the data assets much easier to discover and understand.</span></span>

<span data-ttu-id="0d1ec-321">在此練習中，您會註解單一資料資產 (ProductPhoto)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-321">In this exercise, you annotate a single data asset (ProductPhoto).</span></span> <span data-ttu-id="0d1ec-322">您會對 ProductPhoto 資料資產新增易記名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-322">You add a friendly name and description to the ProductPhoto data asset.</span></span>  

1. <span data-ttu-id="0d1ec-323">移至 [Azure 資料目錄首頁](https://www.azuredatacatalog.com)，並使用 `tags:cycles` 進行搜尋，以尋找您已註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-323">Go to the [Azure Data Catalog home page](https://www.azuredatacatalog.com) and search with `tags:cycles` to find the data assets you have registered.</span></span>  
2. <span data-ttu-id="0d1ec-324">按一下搜尋結果中的 **ProductPhoto** 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-324">Click **ProductPhoto** in search results.</span></span>  
3. <span data-ttu-id="0d1ec-325">在 [易記名稱] 中輸入 **Product images**，並在 [描述] 中輸入 **Product photos for marketing materials**。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-325">Enter **Product images** for **Friendly Name** and **Product photos for marketing materials** for the **Description**.</span></span>
   
    ![Azure 資料目錄--產品圖片描述](media/data-catalog-get-started/data-catalog-productphoto-description.png)
   
    <span data-ttu-id="0d1ec-327">[描述]  可幫助其他人探索並了解為何及如何使用選取的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-327">The **Description** helps others discover and understand why and how to use the selected data asset.</span></span> <span data-ttu-id="0d1ec-328">您也可以新增更多的標記，並檢視資料行。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-328">You can also add more tags and view columns.</span></span> <span data-ttu-id="0d1ec-329">現在您可以使用已新增至目錄的描述性中繼資料，嘗試搜尋和篩選來探索資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-329">Now you can try searching and filtering to discover data assets by using the descriptive metadata you’ve added to the catalog.</span></span>

<span data-ttu-id="0d1ec-330">您也可以在此頁面上執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="0d1ec-330">You can also do the following on this page:</span></span>

* <span data-ttu-id="0d1ec-331">新增資料資產的專家。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-331">Add experts for the data asset.</span></span> <span data-ttu-id="0d1ec-332">按一下 [建立目錄]  in the  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-332">Click **Add** in the **Experts** area.</span></span>
* <span data-ttu-id="0d1ec-333">新增資料集層級的標記。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-333">Add tags at the dataset level.</span></span> <span data-ttu-id="0d1ec-334">按一下 [建立目錄]  in the  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-334">Click **Add** in the **Tags** area.</span></span> <span data-ttu-id="0d1ec-335">標記可以是使用者標記或詞彙標記。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-335">A tag can be a user tag or a glossary tag.</span></span> <span data-ttu-id="0d1ec-336">標準版的資料目錄包含有助於目錄管理員定義中央商務分類的商務詞彙。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-336">The Standard Edition of Data Catalog includes a business glossary that helps catalog administrators define a central business taxonomy.</span></span> <span data-ttu-id="0d1ec-337">目錄使用者接著可以為資料資產加上詞彙註解。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-337">Catalog users can then annotate data assets with glossary terms.</span></span> <span data-ttu-id="0d1ec-338">如需詳細資訊，請參閱 [如何設定控管標籤的商務詞彙](data-catalog-how-to-business-glossary.md)</span><span class="sxs-lookup"><span data-stu-id="0d1ec-338">For more information, see [How to set up the Business Glossary for Governed Tagging](data-catalog-how-to-business-glossary.md)</span></span>
* <span data-ttu-id="0d1ec-339">新增資料行層級的標記。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-339">Add tags at the column level.</span></span> <span data-ttu-id="0d1ec-340">按一下 [建立目錄]  under  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-340">Click **Add** under **Tags** for the column you want to annotate.</span></span>
* <span data-ttu-id="0d1ec-341">新增資料行層級的描述。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-341">Add description at the column level.</span></span> <span data-ttu-id="0d1ec-342">輸入資料行的 [描述]  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-342">Enter **Description** for a column.</span></span> <span data-ttu-id="0d1ec-343">您也可以檢視擷取自資料來源的描述中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-343">You can also view the description metadata extracted from the data source.</span></span>
* <span data-ttu-id="0d1ec-344">新增 [要求存取]  資訊，以對使用者顯示如何要求資料資產的存取權。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-344">Add **Request access** information that shows users how to request access to the data asset.</span></span>
  
    ![Azure 資料目錄--新增標記、描述](media/data-catalog-get-started/data-catalog-add-tags-experts-descriptions.png)
* <span data-ttu-id="0d1ec-346">選擇 [文件]  索引標籤並提供資料資產的文件。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-346">Choose the **Documentation** tab and provide documentation for the data asset.</span></span> <span data-ttu-id="0d1ec-347">透過 Azure 資料目錄文件，您可以使用資料目錄做為內容儲存機制，以建立完整的資料資產敘述。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-347">With Azure Data Catalog documentation, you can use your data catalog as a content repository to create a complete narrative of your data assets.</span></span>
  
    ![Azure 資料目錄--文件索引標籤](media/data-catalog-get-started/data-catalog-documentation.png)

<span data-ttu-id="0d1ec-349">您也可以對多個資料資產新增一個註解。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-349">You can also add an annotation to multiple data assets.</span></span> <span data-ttu-id="0d1ec-350">例如，您可以選取您已註冊的所有資料資產，並指定這些資產的專家。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-350">For example, you can select all the data assets you registered and specify an expert for them.</span></span>

![Azure 資料目錄--註解多個資料資產](media/data-catalog-get-started/data-catalog-multi-select-annotate.png)

<span data-ttu-id="0d1ec-352">Azure 資料目錄支援支援群眾外包 (crowd-sourcing) 的註解作法。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-352">Azure Data Catalog supports a crowd-sourcing approach to annotations.</span></span> <span data-ttu-id="0d1ec-353">Azure 資料目錄使用者可以新增標記 (使用者或詞彙)、描述和其他中繼資料，任何對資料資產及其用法有所見解的使用者，都能將此見解記錄下來分享給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-353">Any Data Catalog user can add tags (user or glossary), descriptions, and other metadata, so that any user with a perspective on a data asset and its use can have that perspective captured and available to other users.</span></span>

<span data-ttu-id="0d1ec-354">如需關於註解資料資產的詳細資訊，請參閱 [如何註解資料資產](data-catalog-how-to-annotate.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-354">See [How to annotate data assets](data-catalog-how-to-annotate.md) for detailed information about annotating data assets.</span></span>

## <a name="connect-to-data-assets"></a><span data-ttu-id="0d1ec-355">連線到資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-355">Connect to data assets</span></span>
<span data-ttu-id="0d1ec-356">在本練習中，您會使用連線資訊，在整合式用戶端工具 (Excel) 和非整合式工具 (SQL Server Management Studio) 中開啟資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-356">In this exercise, you open data assets in an integrated client tool (Excel) and a non-integrated tool (SQL Server Management Studio) by using connection information.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1ec-357">請務必記得，Azure 資料目錄不會讓您存取實際的資料來源，它只是讓您更容易探索和了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-357">It’s important to remember that Azure Data Catalog doesn’t give you access to the actual data source—it simply makes it easier for you to discover and understand it.</span></span> <span data-ttu-id="0d1ec-358">當您連接到資料來源時，所選擇的用戶端應用程式會使用您的 Windows 認證，或在必要時提示您提供認證。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-358">When you connect to a data source, the client application you choose uses your Windows credentials or prompts you for credentials as necessary.</span></span> <span data-ttu-id="0d1ec-359">如果先前未授權您存取資料來源，您必須先獲得授權才能連線。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-359">If you have not previously been granted access to the data source, you need to be granted access before you can connect.</span></span>
> 
> 

### <a name="connect-to-a-data-asset-from-excel"></a><span data-ttu-id="0d1ec-360">從 Excel 連線到資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-360">Connect to a data asset from Excel</span></span>
1. <span data-ttu-id="0d1ec-361">選取搜尋結果中的 **Product** 。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-361">Select **Product** from search results.</span></span> <span data-ttu-id="0d1ec-362">按一下工具列上的 [開啟於]，然後按一下 [Excel]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-362">Click **Open In** on the toolbar and click **Excel**.</span></span>
   
    ![Azure 資料目錄--連線到資料資產](media/data-catalog-get-started/data-catalog-connect1.png)
2. <span data-ttu-id="0d1ec-364">按一下下載快顯視窗中的 [開啟]  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-364">Click **Open** in the download pop-up window.</span></span> <span data-ttu-id="0d1ec-365">這種經驗會視瀏覽器而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-365">This experience may vary depending on the browser.</span></span>
   
    ![Azure 資料目錄--下載 Excel 連線檔案](media/data-catalog-get-started/data-catalog-download-open.png)
3. <span data-ttu-id="0d1ec-367">在 [Microsoft Excel 安全性注意事項] 視窗中，按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-367">In the **Microsoft Excel Security Notice** window, click **Enable**.</span></span>
   
    ![Azure 資料目錄--Excel 安全性快顯視窗](media/data-catalog-get-started/data-catalog-excel-security-popup.png)
4. <span data-ttu-id="0d1ec-369">保留 [匯入資料] 對話方塊中的預設值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-369">Keep the defaults in the **Import Data** dialog box and click **OK**.</span></span>
   
    ![Azure 資料目錄--Excel 匯入資料](media/data-catalog-get-started/data-catalog-excel-import-data.png)
5. <span data-ttu-id="0d1ec-371">在 Excel 中檢視資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-371">View the data source in Excel.</span></span>
   
    ![Azure 資料目錄--Excel 中的產品資料表](media/data-catalog-get-started/data-catalog-connect2.png)

<span data-ttu-id="0d1ec-373">在本練習中，您連接到使用 Azure 資料目錄找到的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-373">In this exercise, you connected to data assets discovered by using Azure Data Catalog.</span></span> <span data-ttu-id="0d1ec-374">在 Azure 資料目錄入口網站中，您可以使用整合到 [開啟於]  功能表中的用戶端應用程式來直接連接。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-374">With the Azure Data Catalog portal, you can connect directly by using the client applications integrated into the **Open in** menu.</span></span> <span data-ttu-id="0d1ec-375">您也可以使用資產中繼資料中包含的連接位置資訊，與您所選的任何應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-375">You can also connect with any application you choose by using the connection location information included in the asset metadata.</span></span> <span data-ttu-id="0d1ec-376">例如︰您可以使用 SQL Server Management Studio 連線到 AdventureWorks2014 資料庫，存取本教學課程中所註冊的資料資產中的資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-376">For example, you can use SQL Server Management Studio to connect to the AdventureWorks2014 database to access the data in the data assets registered in this tutorial.</span></span>

1. <span data-ttu-id="0d1ec-377">開啟 **SQL Server Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-377">Open **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="0d1ec-378">在 [連線到伺服器] 對話方塊中，輸入 Azure 資料目錄入口網站 [屬性] 窗格中的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-378">In the **Connect to Server** dialog box, enter the server name from the **Properties** pane in the Azure Data Catalog portal.</span></span>
3. <span data-ttu-id="0d1ec-379">使用適當的驗證和認證來存取資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-379">Use appropriate authentication and credentials to access the data asset.</span></span> <span data-ttu-id="0d1ec-380">如果您沒有存取權，使用 [要求存取]  欄位中的資訊來取得它。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-380">If you don't have access, use information in the **Request Access** field to get it.</span></span>
   
    ![Azure 資料目錄--要求存取](media/data-catalog-get-started/data-catalog-request-access.png)

<span data-ttu-id="0d1ec-382">按一下 [檢視連接字串]  來檢視 ADF.NET、ODBC 和 OLEDB 連接字串，並將這些字串複製到剪貼簿以在應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-382">Click **View Connection Strings** to view and copy ADF.NET, ODBC, and OLEDB connection strings to the clipboard for use in your application.</span></span>

## <a name="manage-data-assets"></a><span data-ttu-id="0d1ec-383">管理資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-383">Manage data assets</span></span>
<span data-ttu-id="0d1ec-384">在此步驟中，您會了解如何設定資料資產的安全性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-384">In this step, you see how to set up security for your data assets.</span></span> <span data-ttu-id="0d1ec-385">資料目錄並不會讓使用者存取資料本身。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-385">Data Catalog does not give users access to the data itself.</span></span> <span data-ttu-id="0d1ec-386">資料來源的擁有者會控制資料存取權。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-386">The owner of the data source controls data access.</span></span>

<span data-ttu-id="0d1ec-387">您可以使用資料目錄探索資料來源，以及檢視與目錄中註冊的來源相關的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-387">You can use Data Catalog to discover data sources and to view the metadata related to the sources registered in the catalog.</span></span> <span data-ttu-id="0d1ec-388">不過，有時候只有特定使用者或特定群組的成員才能看到資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-388">There may be situations, however, where data sources should only be visible to specific users or to members of specific groups.</span></span> <span data-ttu-id="0d1ec-389">若是這樣的情況，您可以使用資料目錄來取得目錄中已註冊資料資產的擁有權，以及控制您擁有之資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-389">For these scenarios, you can use Data Catalog to take ownership of registered data assets within the catalog, and to then control the visibility of the assets you own.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1ec-390">本練習所述的管理功能只在標準版 Azure 資料目錄中提供，免費版本沒有提供。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-390">The management capabilities described in this exercise are available only in the Standard Edition of Azure Data Catalog, not in the Free Edition.</span></span>
> <span data-ttu-id="0d1ec-391">在 Azure 資料目錄中，您可以取得資料資產的擁有權、新增資料資產的共同擁有者，以及設定資料資產的可見性。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-391">In Azure Data Catalog, you can take ownership of data assets, add co-owners to data assets, and set the visibility of data assets.</span></span>
> 
> 

### <a name="take-ownership-of-data-assets-and-restrict-visibility"></a><span data-ttu-id="0d1ec-392">取得資料資產的擁有權及限制可見性</span><span class="sxs-lookup"><span data-stu-id="0d1ec-392">Take ownership of data assets and restrict visibility</span></span>
1. <span data-ttu-id="0d1ec-393">移至 [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-393">Go to the [Azure Data Catalog home page](https://www.azuredatacatalog.com).</span></span> <span data-ttu-id="0d1ec-394">在 [搜尋] 文字方塊中輸入 `tags:cycles`，然後按 **ENTER** 鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-394">In the **Search** text box, enter `tags:cycles` and press **ENTER**.</span></span>
2. <span data-ttu-id="0d1ec-395">按一下結果清單中的項目，然後按一下工具列上的 [取得擁有權]  。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-395">Click an item in the result list and click **Take Ownership** on the toolbar.</span></span>
3. <span data-ttu-id="0d1ec-396">在 [屬性] 面板的 [管理] 區段中，按一下 [取得擁有權]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-396">In the **Management** section of the **Properties** panel, click **Take Ownership**.</span></span>
   
    ![Azure 資料目錄--取得擁有權](media/data-catalog-get-started/data-catalog-take-ownership.png)
4. <span data-ttu-id="0d1ec-398">若要限制可見性，請選擇 [可見性] 區段的 [擁有者與這些使用者]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-398">To restrict visibility, choose **Owners & These Users** in the **Visibility** section and click **Add**.</span></span> <span data-ttu-id="0d1ec-399">在文字方塊中輸入使用者的電子郵件地址，然後按 **ENTER** 鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-399">Enter user email addresses in the text box and press **ENTER**.</span></span>
   
    ![Azure 資料目錄--限制存取](media/data-catalog-get-started/data-catalog-ownership.png)

## <a name="remove-data-assets"></a><span data-ttu-id="0d1ec-401">移除資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-401">Remove data assets</span></span>
<span data-ttu-id="0d1ec-402">在本練習中，您會使用 Azure 資料目錄入口網站，從已註冊的資料資產中移除預覽資料，並從目錄中刪除資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-402">In this exercise, you use the Azure Data Catalog portal to remove preview data from registered data assets and delete data assets from the catalog.</span></span>

<span data-ttu-id="0d1ec-403">在 Azure 資料目錄中，您可以刪除個別資產或多個資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-403">In Azure Data Catalog, you can delete an individual asset or delete multiple assets.</span></span>

1. <span data-ttu-id="0d1ec-404">移至 [Azure 資料目錄首頁](https://www.azuredatacatalog.com)。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-404">Go to the [Azure Data Catalog home page](https://www.azuredatacatalog.com).</span></span>
2. <span data-ttu-id="0d1ec-405">在 [搜尋] 文字方塊中輸入 `tags:cycles`，然後按一下 **ENTER** 鍵。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-405">In the **Search** text box, enter `tags:cycles` and click **ENTER**.</span></span>
3. <span data-ttu-id="0d1ec-406">選取結果清單中的項目，然後按一下工具列上的 [刪除]  ，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-406">Select an item in the result list and click **Delete** on the toolbar as shown in the following image:</span></span>
   
    ![Azure 資料目錄--刪除資料格項目](media/data-catalog-get-started/data-catalog-delete-grid-item.png)
   
    <span data-ttu-id="0d1ec-408">如果您使用清單檢視，此核取方塊位於項目的左邊，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="0d1ec-408">If you are using the list view, the check box is to the left of the item as shown in the following image:</span></span>
   
    ![Azure 資料目錄--刪除清單項目](media/data-catalog-get-started/data-catalog-delete-list-item.png)
   
    <span data-ttu-id="0d1ec-410">您也可以選取多個資料資產來加以刪除，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="0d1ec-410">You can also select multiple data assets and delete them as shown in the following image:</span></span>
   
    ![Azure 資料目錄--刪除多個資料資產](media/data-catalog-get-started/data-catalog-delete-assets.png)

> [!NOTE]
> <span data-ttu-id="0d1ec-412">目錄的預設行為是允許任何使用者註冊任何資料來源，並允許任何使用者刪除任何已註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-412">The default behavior of the catalog is to allow any user to register any data source, and to allow any user to delete any data asset that has been registered.</span></span> <span data-ttu-id="0d1ec-413">標準版 Azure 資料目錄中包含的管理功能提供其他選項，可用來取得資產的所有權、限制誰可以探索資產，以及限制誰可以刪除資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-413">The management capabilities included in the Standard Edition of Azure Data Catalog provide additional options for taking ownership of assets, restricting who can discover assets, and restricting who can delete assets.</span></span>
> 
> 

## <a name="summary"></a><span data-ttu-id="0d1ec-414">摘要</span><span class="sxs-lookup"><span data-stu-id="0d1ec-414">Summary</span></span>
<span data-ttu-id="0d1ec-415">在本教學課程中，您已瀏覽 Azure 資料目錄的基本功能，包括註冊、註解、探索和管理企業資料資產。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-415">In this tutorial, you explored essential capabilities of Azure Data Catalog, including registering, annotating, discovering, and managing enterprise data assets.</span></span> <span data-ttu-id="0d1ec-416">既然您已經完成本教學課程，現在可以開始使用。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-416">Now that you’ve completed the tutorial, it’s time to get started.</span></span> <span data-ttu-id="0d1ec-417">您可以立即開始註冊您和小組所依賴的資料來源，並邀請同事使用目錄。</span><span class="sxs-lookup"><span data-stu-id="0d1ec-417">You can begin today by registering the data sources you and your team rely on, and by inviting colleagues to use the catalog.</span></span>

## <a name="references"></a><span data-ttu-id="0d1ec-418">參考</span><span class="sxs-lookup"><span data-stu-id="0d1ec-418">References</span></span>
* [<span data-ttu-id="0d1ec-419">如何註冊資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-419">How to register data assets</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="0d1ec-420">如何探索資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-420">How to discover data assets</span></span>](data-catalog-how-to-discover.md)
* [<span data-ttu-id="0d1ec-421">如何註解資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-421">How to annotate data assets</span></span>](data-catalog-how-to-annotate.md)
* [<span data-ttu-id="0d1ec-422">如何記載資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-422">How to document data assets</span></span>](data-catalog-how-to-documentation.md)
* [<span data-ttu-id="0d1ec-423">如何連線到資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-423">How to connect to data assets</span></span>](data-catalog-how-to-connect.md)
* [<span data-ttu-id="0d1ec-424">如何管理資料資產</span><span class="sxs-lookup"><span data-stu-id="0d1ec-424">How to manage data assets</span></span>](data-catalog-how-to-manage.md)

