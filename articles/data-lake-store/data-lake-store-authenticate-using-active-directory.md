---
title: "服務對服務驗證︰使用 Azure Active Directory 以 Data Lake Store 進行 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory 以 Data Lake Store 完成服務對服務驗證"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 27ec0a4f48115d44da98dd048868b044aedf173c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="1d405-103">使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="1d405-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d405-104">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="1d405-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="1d405-105">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="1d405-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="1d405-106">Azure Data Lake Store 使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1d405-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="1d405-107">撰寫搭配 Azure Data Lake Store 或 Azure Data Lake Analytics 的應用程式之前，必須先決定要如何以 Azure Active Directory (Azure AD) 驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d405-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1d405-108">兩個主要選項為︰</span><span class="sxs-lookup"><span data-stu-id="1d405-108">The two main options available are:</span></span>

* <span data-ttu-id="1d405-109">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="1d405-109">End-user authentication</span></span> 
* <span data-ttu-id="1d405-110">服務對服務驗證 (本文)</span><span class="sxs-lookup"><span data-stu-id="1d405-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="1d405-111">兩個選項都要靠 OAuth 2.0 權杖來提供您的應用程式，權杖會附加到每個對 Azure Data Lake Store 或 Azure Data Lake Analytics 提出的要求。</span><span class="sxs-lookup"><span data-stu-id="1d405-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="1d405-112">本文說明如何建立 **Azure AD Web 應用程式以進行服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="1d405-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="1d405-113">如需有關適用於使用者驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="1d405-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d405-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d405-114">Prerequisites</span></span>
* <span data-ttu-id="1d405-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d405-115">An Azure subscription.</span></span> <span data-ttu-id="1d405-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1d405-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="1d405-117">步驟 1：建立 Active Directory Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1d405-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="1d405-118">建立和設定 Azure AD Web 應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行服務對服務驗證。</span><span class="sxs-lookup"><span data-stu-id="1d405-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="1d405-119">如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1d405-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="1d405-120">依照上面連結中的指示進行時，請確定如以下螢幕擷取畫面所示，選取 [Web 應用程式 / API] 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="1d405-120">While following the instructions at the above link, make sure you select **Web App / API** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="1d405-121">![建立 Web 應用程式](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "建立 Web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="1d405-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a><span data-ttu-id="1d405-122">步驟 2：取得應用程式識別碼、驗證金鑰及租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="1d405-122">Step 2: Get application id, authentication key, and tenant id</span></span>
<span data-ttu-id="1d405-123">以程式設計方式登入時，您需要應用程式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d405-123">When programmatically logging in, you need the id for your application.</span></span> <span data-ttu-id="1d405-124">如果應用程式是在自己的認證下執行，則您還需要一個驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d405-124">If the application runs under its own credentials, you will also need an authentication key.</span></span>

* <span data-ttu-id="1d405-125">如需有關如何為應用程式擷取應用程式識別碼和驗證金鑰 (也稱為用戶端祕密) 的指示，請參閱[取得應用程式識別碼和驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)。</span><span class="sxs-lookup"><span data-stu-id="1d405-125">For instructions on how to retrieve the application ID and authentication key (also called the client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="1d405-126">如需有關如何擷取租用戶識別碼的指示，請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。</span><span class="sxs-lookup"><span data-stu-id="1d405-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a><span data-ttu-id="1d405-127">步驟 3：將 Azure AD 應用程式指派給 Azure Data Lake Store 帳戶檔案或資料夾 (僅適用於服務對服務驗證)</span><span class="sxs-lookup"><span data-stu-id="1d405-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder (only for service-to-service authentication)</span></span>
1. <span data-ttu-id="1d405-128">登入新的 [Azure 入口網站](https://portal.azure.com)，然後開啟要與您稍早建立的 Azure Active Directory 應用程式建立關聯的 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d405-128">Sign on to the new [Azure portal](https://portal.azure.com) and open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="1d405-129">在您的 [Data Lake Store 帳戶] 刀鋒視窗中，按一下 [資料總管] 。</span><span class="sxs-lookup"><span data-stu-id="1d405-129">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="1d405-130">![在 Data Lake Store 帳戶中建立目錄](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "在 Data Lake Store 帳戶中建立目錄")</span><span class="sxs-lookup"><span data-stu-id="1d405-130">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="1d405-131">在 [資料總管] 刀鋒視窗中，按一下您要將其存取權提供給 Azure AD 應用程式的檔案或資料夾，然後按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="1d405-131">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="1d405-132">若要設定對檔案的存取權，您必須從 [檔案預覽] 刀鋒視窗按一下 [存取]。</span><span class="sxs-lookup"><span data-stu-id="1d405-132">To configure access to a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="1d405-133">![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")</span><span class="sxs-lookup"><span data-stu-id="1d405-133">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="1d405-134">[存取]  刀鋒視窗會列出已指派至根的標準存取和自訂存取。</span><span class="sxs-lookup"><span data-stu-id="1d405-134">The **Access** blade lists the standard access and custom access already assigned to the root.</span></span> <span data-ttu-id="1d405-135">按一下 [新增]  圖示以新增自訂層級的 ACL。</span><span class="sxs-lookup"><span data-stu-id="1d405-135">Click the **Add** icon to add custom-level ACLs.</span></span>
   
    <span data-ttu-id="1d405-136">![列出標準和自訂存取](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "列出標準和自訂的存取")</span><span class="sxs-lookup"><span data-stu-id="1d405-136">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="1d405-137">按一下 [新增] 圖示，以開啟 [新增自訂存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d405-137">Click the **Add** icon to open the **Add Custom Access** blade.</span></span> <span data-ttu-id="1d405-138">在此刀鋒視窗中，按一下 [選取使用者或群組]，然後在 [選取使用者或群組] 刀鋒視窗中，尋找您稍早建立的 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d405-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="1d405-139">若您需要搜尋大量的群組，請使用頂端的文字方塊來篩選群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1d405-139">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="1d405-140">按一下您要新增的群組，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="1d405-140">Click the group you want to add and then click **Select**.</span></span>
   
    <span data-ttu-id="1d405-141">![加入群組](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "加入群組")</span><span class="sxs-lookup"><span data-stu-id="1d405-141">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="1d405-142">按一下 [選取權限]，選取權限及權限的指派方式 (例如預設 ACL、存取 ACL 或兩者並用)。</span><span class="sxs-lookup"><span data-stu-id="1d405-142">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="1d405-143">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d405-143">Click **OK**.</span></span>
   
    <span data-ttu-id="1d405-144">![將權限指派至群組](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "將權限指派至群組")</span><span class="sxs-lookup"><span data-stu-id="1d405-144">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span></span>
   
    <span data-ttu-id="1d405-145">如需有關 Data Lake Store 中的權限及預設/存取 ACL 的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="1d405-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="1d405-146">在 [新增自訂存取] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d405-146">In the **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="1d405-147">具有相關權限的新增群組現在會列在 [存取]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="1d405-147">The newly added group, with the associated permissions, will now be listed in the **Access** blade.</span></span>
   
    <span data-ttu-id="1d405-148">![將權限指派至群組](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "將權限指派至群組")</span><span class="sxs-lookup"><span data-stu-id="1d405-148">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span></span>

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="1d405-149">步驟 4：取得 OAuth 2.0 權杖端點 (只適用於 Java 型應用程式)</span><span class="sxs-lookup"><span data-stu-id="1d405-149">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="1d405-150">登入新的 [Azure 入口網站](https://portal.azure.com)，然後按一下左窗格中的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1d405-150">Sign on to the new [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span></span>

2. <span data-ttu-id="1d405-151">從左窗格，按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="1d405-151">From the left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="1d405-152">從 [應用程式註冊] 刀鋒視窗頂端，按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="1d405-152">From the top of the App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="1d405-153">![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth 權杖端點")</span><span class="sxs-lookup"><span data-stu-id="1d405-153">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="1d405-154">從端點清單，複製 OAuth 2.0 權杖端點。</span><span class="sxs-lookup"><span data-stu-id="1d405-154">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span></span>

    <span data-ttu-id="1d405-155">![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth 權杖端點")</span><span class="sxs-lookup"><span data-stu-id="1d405-155">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="1d405-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d405-156">Next steps</span></span>
<span data-ttu-id="1d405-157">在本文中，您已建立 Azure AD Web 應用程式，並收集您使用 .NET SDK、Java SDK 等撰寫的用戶端應用程式中所需的資訊。您現在可以繼續進行下列文章，這些文章說明如何使用 Azure AD Web 應用程式先以 Data Lake Store 進行驗證，然後再於存放區上執行其他作業。</span><span class="sxs-lookup"><span data-stu-id="1d405-157">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="1d405-158">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1d405-158">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="1d405-159">使用 Java SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1d405-159">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)

<span data-ttu-id="1d405-160">本文章會逐步引導您取得使用者主體和執行應用程式所需的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="1d405-160">This article walked you through the basic steps needed to get a user principal up and running for your application.</span></span> <span data-ttu-id="1d405-161">您可以查看下列文章以取得進一步資訊︰</span><span class="sxs-lookup"><span data-stu-id="1d405-161">You can look at the following articles to get further information:</span></span>
* [<span data-ttu-id="1d405-162">使用 PowerShell 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="1d405-162">Use PowerShell to create service principal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="1d405-163">使用憑證驗證進行服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="1d405-163">Use certificate authentication for service principal authentication</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [<span data-ttu-id="1d405-164">向 Azure AD 驗證的其他方法</span><span class="sxs-lookup"><span data-stu-id="1d405-164">Other methods to authenticate to Azure AD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


