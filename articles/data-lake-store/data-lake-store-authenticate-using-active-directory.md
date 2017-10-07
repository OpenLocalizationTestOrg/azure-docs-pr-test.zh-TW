---
title: "服務對服務驗證︰使用 Azure Active Directory 以 Data Lake Store 進行 | Microsoft Docs"
description: "深入了解如何使用 Azure Active Directory 的 Data Lake Store tooachieve 服務對服務驗證"
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
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="bf26d-103">使用 Azure Active Directory 以 Data Lake Store 進行服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="bf26d-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf26d-104">服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="bf26d-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="bf26d-105">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="bf26d-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="bf26d-106">Azure Data Lake Store 使用 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="bf26d-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="bf26d-107">如果之前撰寫的應用程式，適用於 Azure 資料湖存放區或 Azure Data Lake Analytics，您必須先決定您希望如何 tooauthenticate 應用程式與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bf26d-108">hello 兩個主要選項如下：</span><span class="sxs-lookup"><span data-stu-id="bf26d-108">hello two main options available are:</span></span>

* <span data-ttu-id="bf26d-109">使用者驗證</span><span class="sxs-lookup"><span data-stu-id="bf26d-109">End-user authentication</span></span> 
* <span data-ttu-id="bf26d-110">服務對服務驗證 (本文)</span><span class="sxs-lookup"><span data-stu-id="bf26d-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="bf26d-111">這兩個選項會導致以 OAuth 2.0 權杖取得附加的 tooeach 所提出的要求 tooAzure 資料湖存放區或 Azure Data Lake Analytics 所提供的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf26d-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="bf26d-112">本文說明如何建立 **Azure AD Web 應用程式以進行服務對服務驗證**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="bf26d-113">如需有關適用於使用者驗證的 Azure AD 應用程式組態的指示，請參閱[使用 Azure Active Directory 以 Data Lake Store 進行使用者驗證](data-lake-store-end-user-authenticate-using-active-directory.md)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf26d-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf26d-114">Prerequisites</span></span>
* <span data-ttu-id="bf26d-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf26d-115">An Azure subscription.</span></span> <span data-ttu-id="bf26d-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="bf26d-117">步驟 1：建立 Active Directory Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf26d-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="bf26d-118">建立和設定 Azure AD Web 應用程式，以便使用 Azure Active Directory 以 Azure Data Lake Store 進行服務對服務驗證。</span><span class="sxs-lookup"><span data-stu-id="bf26d-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="bf26d-119">如需指示，請參閱[建立 Azure AD 應用程式](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="bf26d-120">遵循上述連結 hello hello 指示，請確定您選取**Web 應用程式 / 應用程式開發介面**應用程式類型，如 hello 以下螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="bf26d-120">While following hello instructions at hello above link, make sure you select **Web App / API** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="bf26d-121">![建立 Web 應用程式](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "建立 Web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="bf26d-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a><span data-ttu-id="bf26d-122">步驟 2：取得應用程式識別碼、驗證金鑰及租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="bf26d-122">Step 2: Get application id, authentication key, and tenant id</span></span>
<span data-ttu-id="bf26d-123">以程式設計方式登入時，您將在您的應用程式需要 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="bf26d-123">When programmatically logging in, you need hello id for your application.</span></span> <span data-ttu-id="bf26d-124">如果 hello 應用程式是在它自己的認證下執行，您也必須驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf26d-124">If hello application runs under its own credentials, you will also need an authentication key.</span></span>

* <span data-ttu-id="bf26d-125">如需如何 tooretrieve hello 應用程式識別碼和驗證金鑰 （也稱為的 hello 用戶端機密） 應用程式的指示，請參閱[取得應用程式識別碼和驗證金鑰](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-125">For instructions on how tooretrieve hello application ID and authentication key (also called hello client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="bf26d-126">如需有關如何 tooretrieve hello 租用戶識別碼的指示，請參閱[取得租用戶識別碼](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-126">For instructions on how tooretrieve hello tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a><span data-ttu-id="bf26d-127">步驟 3： 指派 hello Azure AD 應用程式 toohello Azure Data Lake Store 帳戶的檔案或資料夾 （僅適用於服務對服務驗證）</span><span class="sxs-lookup"><span data-stu-id="bf26d-127">Step 3: Assign hello Azure AD application toohello Azure Data Lake Store account file or folder (only for service-to-service authentication)</span></span>
1. <span data-ttu-id="bf26d-128">登入新 toohello [Azure 入口網站](https://portal.azure.com)並開啟您想以 hello 您稍早建立的 Azure Active Directory 應用程式的 tooassociate hello Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf26d-128">Sign on toohello new [Azure portal](https://portal.azure.com) and open hello Azure Data Lake Store account that you want tooassociate with hello Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="bf26d-129">在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。</span><span class="sxs-lookup"><span data-stu-id="bf26d-129">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="bf26d-130">![在 Data Lake Store 帳戶中建立目錄](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "在 Data Lake Store 帳戶中建立目錄")</span><span class="sxs-lookup"><span data-stu-id="bf26d-130">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="bf26d-131">在 hello**資料總管**刀鋒視窗中，按一下 hello 檔案或資料夾，您想 tooprovide 存取 toohello Azure AD 應用程式，然後按一下**存取**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-131">In hello **Data Explorer** blade, click hello file or folder for which you want tooprovide access toohello Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="bf26d-132">tooconfigure access tooa 檔案，您必須按一下**存取**從 hello**檔案預覽**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bf26d-132">tooconfigure access tooa file, you must click **Access** from hello **File Preview** blade.</span></span>
   
    <span data-ttu-id="bf26d-133">![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")</span><span class="sxs-lookup"><span data-stu-id="bf26d-133">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="bf26d-134">hello**存取**刀鋒視窗會列出 hello 標準權限和自訂存取已指派 toohello 根。</span><span class="sxs-lookup"><span data-stu-id="bf26d-134">hello **Access** blade lists hello standard access and custom access already assigned toohello root.</span></span> <span data-ttu-id="bf26d-135">按一下 hello**新增**圖示 tooadd 自訂層級的 Acl。</span><span class="sxs-lookup"><span data-stu-id="bf26d-135">Click hello **Add** icon tooadd custom-level ACLs.</span></span>
   
    <span data-ttu-id="bf26d-136">![列出標準和自訂存取](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "列出標準和自訂的存取")</span><span class="sxs-lookup"><span data-stu-id="bf26d-136">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="bf26d-137">按一下 hello**新增**圖示 tooopen hello**加入自訂存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bf26d-137">Click hello **Add** icon tooopen hello **Add Custom Access** blade.</span></span> <span data-ttu-id="bf26d-138">在這個刀鋒視窗中，按一下**選取使用者或群組**，然後在**選取使用者或群組**刀鋒視窗中，尋找您稍早建立的 hello Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf26d-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for hello Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="bf26d-139">如果您有大量從群組 toosearch，使用 hello 文字方塊在 hello 頂端 toofilter hello 群組名稱。</span><span class="sxs-lookup"><span data-stu-id="bf26d-139">If you have a lot of groups toosearch from, use hello text box at hello top toofilter on hello group name.</span></span> <span data-ttu-id="bf26d-140">按一下您想 tooadd，然後按一下 hello 群組**選取**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-140">Click hello group you want tooadd and then click **Select**.</span></span>
   
    <span data-ttu-id="bf26d-141">![加入群組](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "加入群組")</span><span class="sxs-lookup"><span data-stu-id="bf26d-141">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="bf26d-142">按一下**選取權限**選取 hello 權限，是否要為一份預設 ACL 將 tooassign hello 權限，存取 ACL，或兩者。</span><span class="sxs-lookup"><span data-stu-id="bf26d-142">Click **Select Permissions**, select hello permissions and whether you want tooassign hello permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="bf26d-143">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bf26d-143">Click **OK**.</span></span>
   
    <span data-ttu-id="bf26d-144">![指派權限 toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "指派權限 toogroup")</span><span class="sxs-lookup"><span data-stu-id="bf26d-144">![Assign permissions toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions toogroup")</span></span>
   
    <span data-ttu-id="bf26d-145">如需有關 Data Lake Store 中的權限及預設/存取 ACL 的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="bf26d-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="bf26d-146">在 hello**加入自訂存取**刀鋒視窗中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-146">In hello **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="bf26d-147">hello 新加入的群組相關聯的 hello 權限，現在會列在 hello**存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bf26d-147">hello newly added group, with hello associated permissions, will now be listed in hello **Access** blade.</span></span>
   
    <span data-ttu-id="bf26d-148">![指派權限 toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "指派權限 toogroup")</span><span class="sxs-lookup"><span data-stu-id="bf26d-148">![Assign permissions toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions toogroup")</span></span>

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="bf26d-149">步驟 4： 取得 hello OAuth 2.0 權杖端點 （僅適用於 Java 為基礎的應用程式）</span><span class="sxs-lookup"><span data-stu-id="bf26d-149">Step 4: Get hello OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="bf26d-150">登入新 toohello [Azure 入口網站](https://portal.azure.com)從 hello 左窗格中按一下 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="bf26d-150">Sign on toohello new [Azure portal](https://portal.azure.com) and click Active Directory from hello left pane.</span></span>

2. <span data-ttu-id="bf26d-151">從 hello 左窗格中，按一下 **應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-151">From hello left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="bf26d-152">從 hello hello 應用程式註冊刀鋒視窗頂端，按一下 **端點**。</span><span class="sxs-lookup"><span data-stu-id="bf26d-152">From hello top of hello App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="bf26d-153">![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth 權杖端點")</span><span class="sxs-lookup"><span data-stu-id="bf26d-153">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="bf26d-154">從 [hello] 清單中的端點，複製到 hello OAuth 2.0 權杖端點。</span><span class="sxs-lookup"><span data-stu-id="bf26d-154">From hello list of endpoints, copy hello OAuth 2.0 token endpoint.</span></span>

    <span data-ttu-id="bf26d-155">![OAuth 權杖端點](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth 權杖端點")</span><span class="sxs-lookup"><span data-stu-id="bf26d-155">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="bf26d-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf26d-156">Next steps</span></span>
<span data-ttu-id="bf26d-157">在本文中您建立的 Azure AD web 應用程式，並收集您需要在用戶端應用程式中您撰寫使用.NET SDK、 Java SDK 等 hello 資訊。您可以現在繼續 toohello 下列文章會討論如何 toouse hello Azure AD web 應用程式 toofirst 向資料湖存放區，然後再執行 hello 存放區上的其他操作。</span><span class="sxs-lookup"><span data-stu-id="bf26d-157">In this article you created an Azure AD web application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="bf26d-158">使用 .NET SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bf26d-158">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="bf26d-159">使用 Java SDK 開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bf26d-159">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)

<span data-ttu-id="bf26d-160">這篇文章帶您完成 hello 基本步驟所需 tooget 主體註冊並執行您的應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf26d-160">This article walked you through hello basic steps needed tooget a user principal up and running for your application.</span></span> <span data-ttu-id="bf26d-161">您可以查看下列文章 tooget 進一步資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf26d-161">You can look at hello following articles tooget further information:</span></span>
* [<span data-ttu-id="bf26d-162">使用 PowerShell toocreate 服務主體</span><span class="sxs-lookup"><span data-stu-id="bf26d-162">Use PowerShell toocreate service principal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="bf26d-163">使用憑證驗證進行服務主體驗證</span><span class="sxs-lookup"><span data-stu-id="bf26d-163">Use certificate authentication for service principal authentication</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [<span data-ttu-id="bf26d-164">其他方法 tooauthenticate tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="bf26d-164">Other methods tooauthenticate tooAzure AD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


