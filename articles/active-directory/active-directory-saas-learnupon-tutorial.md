---
title: "教學課程：Azure Active Directory 與 LearnUpon 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LearnUpon 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="a6bbc-103">教學課程：Azure Active Directory 與 LearnUpon 整合</span><span class="sxs-lookup"><span data-stu-id="a6bbc-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="a6bbc-104">在本教學課程中，您會了解如何整合 LearnUpon 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6bbc-105">LearnUpon 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6bbc-106">您可以在 Azure AD 中控制可存取 LearnUpon 的人員</span><span class="sxs-lookup"><span data-stu-id="a6bbc-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="a6bbc-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 LearnUpon (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a6bbc-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6bbc-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a6bbc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a6bbc-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6bbc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a6bbc-110">Prerequisites</span></span>

<span data-ttu-id="a6bbc-111">若要設定 Azure AD 與 LearnUpon 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="a6bbc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6bbc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6bbc-113">已啟用 LearnUpon 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6bbc-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6bbc-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6bbc-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6bbc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6bbc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6bbc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a6bbc-118">Scenario description</span></span>
<span data-ttu-id="a6bbc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6bbc-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6bbc-121">從資源庫中加入 LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a6bbc-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="a6bbc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6bbc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="a6bbc-123">從資源庫中加入 LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a6bbc-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="a6bbc-124">若要設定將 LearnUpon 整合到 Azure AD 中，您需要從資源庫將 LearnUpon 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6bbc-125">**若要從資源庫新增 LearnUpon，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6bbc-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bbc-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6bbc-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6bbc-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a6bbc-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a6bbc-133">在搜尋方塊中，輸入 **LearnUpon**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-133">In the search box, type **LearnUpon**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="a6bbc-135">在結果窗格中，選取 [LearnUpon]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6bbc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6bbc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6bbc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LearnUpon 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a6bbc-139">若要讓單一登入運作，Azure AD 必須知道 LearnUpon 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="a6bbc-140">換句話說，必須在 Azure AD 使用者與 LearnUpon 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="a6bbc-141">在 LearnUpon 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a6bbc-142">若要設定及測試與 LearnUpon 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6bbc-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a6bbc-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6bbc-145">**[建立 LearnUpon 測試使用者](#creating-a-learnupon-test-user)** - 使 LearnUpon 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6bbc-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6bbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6bbc-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6bbc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6bbc-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 LearnUpon 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="a6bbc-150">**若要設定與 LearnUpon 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6bbc-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bbc-151">在 Azure 入口網站的 [LearnUpon] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a6bbc-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="a6bbc-155">在 [LearnUpon 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="a6bbc-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="a6bbc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6bbc-158">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-158">Please note that this is not the real value.</span></span> <span data-ttu-id="a6bbc-159">您必須使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="a6bbc-160">若要取得此值，請連絡 [LearnUpon 支援小組](https://www.learnupon.com/features/support/)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="a6bbc-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (原始)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="a6bbc-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6bbc-165">在 [LearnUpon 組態] 區段上，按一下 [設定 LearnUpon] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a6bbc-166">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="a6bbc-168">開啟另一個瀏覽器執行個體，並使用系統管理員帳戶登入 LearnUpon。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="a6bbc-169">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-169">Click the **settings** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="a6bbc-171">按一下 [單一登入 - SAML]，然後按一下 [一般設定] 以設定 SAML 設定。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="a6bbc-173">在 [一般設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="a6bbc-175">a.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-175">a.</span></span> <span data-ttu-id="a6bbc-176">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-176">Select **Enabled**.</span></span>

    <span data-ttu-id="a6bbc-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-177">b.</span></span> <span data-ttu-id="a6bbc-178">對於 [版本] 選取 [2.0]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="a6bbc-179">c.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-179">c.</span></span> <span data-ttu-id="a6bbc-180">對於 [略過條件] 選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="a6bbc-181">d.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-181">d.</span></span> <span data-ttu-id="a6bbc-182">在 [SAML 權杖張貼參數名稱] 文字方塊中，輸入上述 SAML 取用者 URL 的要求張貼參數名稱，其中包含要確認和驗證的 SAML 判斷提示，例如 **SAMLResponse**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="a6bbc-183">e.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-183">e.</span></span> <span data-ttu-id="a6bbc-184">在 [名稱識別碼格式] 文字方塊中，輸入可指出使用者識別碼 (電子郵件地址) 在您「SAML 判斷提示」中的所在位置的值，例如 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="a6bbc-185">f.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-185">f.</span></span> <span data-ttu-id="a6bbc-186">在 [識別提供者位置] 文字方塊中，輸入可指出當使用者按一下 Azure 入口網站登入畫面中的所上傳圖示時，要將他們傳送到何處的值。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="a6bbc-187">g.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-187">g.</span></span> <span data-ttu-id="a6bbc-188">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**登出 URL**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="a6bbc-189">h.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-189">h.</span></span> <span data-ttu-id="a6bbc-190">按一下 [管理指紋]，然後上傳所下載憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="a6bbc-191">按一下 [使用者設定] ，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="a6bbc-193">a.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-193">a.</span></span> <span data-ttu-id="a6bbc-194">在 [名字識別碼格式] 文字方塊中，輸入可告知我們使用者名字在您「SAML 判斷提示」中的所在位置的值，例如：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="a6bbc-195">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-195">b.</span></span> <span data-ttu-id="a6bbc-196">在 [姓氏識別碼格式] 文字方塊中，輸入可告知我們使用者名字在您「SAML 判斷提示」中的所在位置的值，例如：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="a6bbc-197">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="a6bbc-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a6bbc-198">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a6bbc-199">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6bbc-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6bbc-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6bbc-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6bbc-201">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a6bbc-203">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6bbc-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bbc-204">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6bbc-206">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6bbc-208">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6bbc-210">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6bbc-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6bbc-212">a.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-212">a.</span></span> <span data-ttu-id="a6bbc-213">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6bbc-214">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-214">b.</span></span> <span data-ttu-id="a6bbc-215">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6bbc-216">c.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-216">c.</span></span> <span data-ttu-id="a6bbc-217">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6bbc-218">d.</span><span class="sxs-lookup"><span data-stu-id="a6bbc-218">d.</span></span> <span data-ttu-id="a6bbc-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="a6bbc-220">建立 LearnUpon 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6bbc-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="a6bbc-221">本節的目標是要在 LearnUpon 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="a6bbc-222">LearnUpon 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a6bbc-223">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-223">There is no action item for you in this section.</span></span> <span data-ttu-id="a6bbc-224">嘗試存取 LearnUpon 時，如果使用者尚未存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="a6bbc-225">[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="a6bbc-226">如果您需要手動建立使用者，您需要連絡 [LearnUpon 支援小組](https://www.learnupon.com/features/support/)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6bbc-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6bbc-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6bbc-228">在本節中，您會把 LearnUpon 的存取權授予 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![指派使用者][200] 

<span data-ttu-id="a6bbc-230">**若要將 Britta Simon 指派到 LearnUpon，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a6bbc-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bbc-231">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a6bbc-233">在應用程式清單中，選取 [LearnUpon] 。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-233">In the applications list, select **LearnUpon**.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="a6bbc-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-235">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a6bbc-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-237">Click **Add** button.</span></span> <span data-ttu-id="a6bbc-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a6bbc-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a6bbc-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6bbc-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6bbc-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a6bbc-243">Testing single sign-on</span></span>

<span data-ttu-id="a6bbc-244">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a6bbc-245">當您按一下「存取面板」中的 LearnUpon 磚時，您應該會自動登入 LearnUpon 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="a6bbc-246">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bbc-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6bbc-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="a6bbc-247">Additional resources</span></span>

* [<span data-ttu-id="a6bbc-248">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a6bbc-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6bbc-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a6bbc-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

