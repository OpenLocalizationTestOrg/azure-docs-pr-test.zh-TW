---
title: "教學課程：Azure Active Directory 與 M-Files 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 M-Files 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="ca67d-103">教學課程：Azure Active Directory 與 M-Files 整合</span><span class="sxs-lookup"><span data-stu-id="ca67d-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="ca67d-104">在本教學課程中，您將了解如何整合 M-Files 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ca67d-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca67d-105">M-Files 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ca67d-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ca67d-106">您可以在 Azure AD 中控制可存取 M-Files 的人員</span><span class="sxs-lookup"><span data-stu-id="ca67d-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="ca67d-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 M-Files (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ca67d-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca67d-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ca67d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ca67d-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ca67d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca67d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ca67d-110">Prerequisites</span></span>

<span data-ttu-id="ca67d-111">若要設定與 M-Files 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ca67d-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="ca67d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ca67d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca67d-113">已啟用 M-Files 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ca67d-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca67d-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ca67d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca67d-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ca67d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca67d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ca67d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca67d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ca67d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca67d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ca67d-118">Scenario description</span></span>
<span data-ttu-id="ca67d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca67d-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ca67d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca67d-121">從資源庫新增 M-Files</span><span class="sxs-lookup"><span data-stu-id="ca67d-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="ca67d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ca67d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="ca67d-123">從資源庫新增 M-Files</span><span class="sxs-lookup"><span data-stu-id="ca67d-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="ca67d-124">若要設定 M-Files 與 Azure AD 整合，您需要從資源庫將 M-Files 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ca67d-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ca67d-125">**若要從資源庫新增 M-Files，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ca67d-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ca67d-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ca67d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca67d-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ca67d-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ca67d-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca67d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ca67d-133">在搜尋方塊中，輸入 **M-Files**。</span><span class="sxs-lookup"><span data-stu-id="ca67d-133">In the search box, type **M-Files**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="ca67d-135">在結果窗格中，選取 [M-Files]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca67d-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca67d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ca67d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca67d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 M-Files 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca67d-139">若要讓單一登入能夠運作，Azure AD 必須知道 M-Files 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ca67d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="ca67d-140">換句話說，必須在 Azure AD 使用者與 M-Files 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ca67d-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="ca67d-141">在 M-Files 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ca67d-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ca67d-142">若要設定及測試與 M-Files 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ca67d-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ca67d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ca67d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ca67d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca67d-145">**[建立 M-Files 測試使用者](#creating-a-m-files-test-user)** - 使 M-Files 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="ca67d-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca67d-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca67d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ca67d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca67d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ca67d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca67d-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 M-Files 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="ca67d-150">**若要使用 M-Files 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ca67d-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="ca67d-151">在 Azure 入口網站的 [M-Files] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ca67d-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="ca67d-155">在 [M-Files 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ca67d-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="ca67d-157">a.</span><span class="sxs-lookup"><span data-stu-id="ca67d-157">a.</span></span> <span data-ttu-id="ca67d-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="ca67d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="ca67d-159">b.</span><span class="sxs-lookup"><span data-stu-id="ca67d-159">b.</span></span> <span data-ttu-id="ca67d-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="ca67d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca67d-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ca67d-161">These values are not real.</span></span> <span data-ttu-id="ca67d-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ca67d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ca67d-163">請連絡 [M-Files 客戶支援小組](mailto:support@m-files.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ca67d-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="ca67d-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ca67d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="ca67d-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca67d-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ca67d-168">若要取得為您的應用程式設定的 SSO，請連絡 [M-Files 支援小組](mailto:support@m-files.com)並提供下載的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ca67d-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ca67d-169">如果您想為您的 M-File 傳統型應用程式設定 SSO，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="ca67d-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="ca67d-170">如果您只想為 M-Files 的 Web 版本設定 SSO，則不需要任何額外步驟。</span><span class="sxs-lookup"><span data-stu-id="ca67d-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="ca67d-171">請依照下列步驟設定 M-File 傳統型應用程式，以搭配 Azure AD 啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="ca67d-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="ca67d-172">若要下載 M-Files，請移至 [M-Files 下載](https://www.m-files.com/en/download-latest-version)頁面。</span><span class="sxs-lookup"><span data-stu-id="ca67d-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="ca67d-173">開啟 [M-Files 桌面設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ca67d-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="ca67d-174">然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-174">Then, click **Add**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="ca67d-176">在 [文件保存庫連線內容] 視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ca67d-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="ca67d-178">在 [伺服器] 區段下，輸入以下的值︰</span><span class="sxs-lookup"><span data-stu-id="ca67d-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="ca67d-179">a.</span><span class="sxs-lookup"><span data-stu-id="ca67d-179">a.</span></span> <span data-ttu-id="ca67d-180">在 [名稱] 中，輸入 `<tenant-name>.cloudvault.m-files.com`。</span><span class="sxs-lookup"><span data-stu-id="ca67d-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="ca67d-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca67d-181">b.</span></span> <span data-ttu-id="ca67d-182">在 [連接埠號碼]中，輸入 **4466**。</span><span class="sxs-lookup"><span data-stu-id="ca67d-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="ca67d-183">c.</span><span class="sxs-lookup"><span data-stu-id="ca67d-183">c.</span></span> <span data-ttu-id="ca67d-184">在 [通訊協定]中，選取 **HTTPS**。</span><span class="sxs-lookup"><span data-stu-id="ca67d-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="ca67d-185">d.</span><span class="sxs-lookup"><span data-stu-id="ca67d-185">d.</span></span> <span data-ttu-id="ca67d-186">在 [驗證] 欄位中，選取 [特定的 Windows 使用者]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="ca67d-187">然後，系統會向您提示簽署頁面。</span><span class="sxs-lookup"><span data-stu-id="ca67d-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="ca67d-188">請插入您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="ca67d-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="ca67d-189">e.</span><span class="sxs-lookup"><span data-stu-id="ca67d-189">e.</span></span> <span data-ttu-id="ca67d-190">在 [伺服器上的保存庫]，選取伺服器上對應的保存庫。</span><span class="sxs-lookup"><span data-stu-id="ca67d-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="ca67d-191">f.</span><span class="sxs-lookup"><span data-stu-id="ca67d-191">f.</span></span> <span data-ttu-id="ca67d-192">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ca67d-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="ca67d-193">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ca67d-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ca67d-194">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ca67d-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ca67d-195">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca67d-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca67d-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ca67d-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca67d-197">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ca67d-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ca67d-199">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ca67d-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ca67d-200">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ca67d-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca67d-202">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca67d-204">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca67d-206">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ca67d-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca67d-208">a.</span><span class="sxs-lookup"><span data-stu-id="ca67d-208">a.</span></span> <span data-ttu-id="ca67d-209">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ca67d-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca67d-210">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca67d-210">b.</span></span> <span data-ttu-id="ca67d-211">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ca67d-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca67d-212">c.</span><span class="sxs-lookup"><span data-stu-id="ca67d-212">c.</span></span> <span data-ttu-id="ca67d-213">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ca67d-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ca67d-214">d.</span><span class="sxs-lookup"><span data-stu-id="ca67d-214">d.</span></span> <span data-ttu-id="ca67d-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ca67d-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="ca67d-216">建立 M-Files 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ca67d-216">Creating a M-Files test user</span></span>

<span data-ttu-id="ca67d-217">本節的目標是要在 M-Files 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ca67d-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="ca67d-218">請與 [M-Files 支援小組](mailto:support@m-files.com)合作，在 M-Files 中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="ca67d-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ca67d-219">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ca67d-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ca67d-220">在本節中，您會將 M-Files 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ca67d-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![指派使用者][200] 

<span data-ttu-id="ca67d-222">**若要將 Britta Simon 指派給 M-Files，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ca67d-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="ca67d-223">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ca67d-225">在應用程式清單中，選取 [M-Files]。 </span><span class="sxs-lookup"><span data-stu-id="ca67d-225">In the applications list, select **M-Files**.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="ca67d-227">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-227">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ca67d-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca67d-229">Click **Add** button.</span></span> <span data-ttu-id="ca67d-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ca67d-232">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ca67d-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ca67d-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca67d-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca67d-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ca67d-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca67d-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ca67d-235">Testing single sign-on</span></span>

<span data-ttu-id="ca67d-236">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="ca67d-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ca67d-237">當您在存取面板中按一下 [M-Files] 磚時，應該會自動登入您的 M-Files 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca67d-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca67d-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="ca67d-238">Additional resources</span></span>

* [<span data-ttu-id="ca67d-239">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ca67d-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca67d-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ca67d-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

