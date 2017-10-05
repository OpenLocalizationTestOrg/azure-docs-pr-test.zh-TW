---
title: "教學課程：Azure Active Directory 與 Moxtra 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Moxtra 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="6ba91-103">教學課程：Azure Active Directory 與 Moxtra 整合</span><span class="sxs-lookup"><span data-stu-id="6ba91-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="6ba91-104">在本教學課程中，您將了解如何整合 Moxtra 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6ba91-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ba91-105">將 Moxtra 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6ba91-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6ba91-106">您可以在 Azure AD 中控制可存取 Moxtra 的人員</span><span class="sxs-lookup"><span data-stu-id="6ba91-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="6ba91-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Moxtra (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6ba91-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ba91-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6ba91-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6ba91-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6ba91-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ba91-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6ba91-110">Prerequisites</span></span>

<span data-ttu-id="6ba91-111">若要設定與 Moxtra 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6ba91-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="6ba91-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6ba91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ba91-113">已啟用 Moxtra 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6ba91-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ba91-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6ba91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ba91-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6ba91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ba91-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6ba91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ba91-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6ba91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ba91-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6ba91-118">Scenario description</span></span>
<span data-ttu-id="6ba91-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ba91-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6ba91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ba91-121">從資源庫新增 Moxtra</span><span class="sxs-lookup"><span data-stu-id="6ba91-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="6ba91-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ba91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="6ba91-123">從資源庫新增 Moxtra</span><span class="sxs-lookup"><span data-stu-id="6ba91-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="6ba91-124">若要設定將 Moxtra 整合到 Azure AD 中，您需要從資源庫將 Moxtra 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6ba91-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6ba91-125">**若要從資源庫新增 Moxtra，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ba91-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6ba91-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6ba91-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ba91-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6ba91-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6ba91-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ba91-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6ba91-133">在搜尋方塊中，輸入 **Moxtra**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-133">In the search box, type **Moxtra**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="6ba91-135">在結果窗格中，選取 [Moxtra]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ba91-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ba91-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ba91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ba91-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Moxtra 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6ba91-139">若要讓單一登入運作，Azure AD 必須知道 Moxtra 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6ba91-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="6ba91-140">換句話說，必須在 Azure AD 使用者與 Moxtra 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6ba91-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="6ba91-141">在 Moxtra 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6ba91-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6ba91-142">若要設定及測試與 Moxtra 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="6ba91-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6ba91-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6ba91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6ba91-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ba91-145">**[建立 Moxtra 測試使用者](#creating-a-moxtra-test-user)** - 使 Moxtra 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="6ba91-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ba91-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ba91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6ba91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ba91-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6ba91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ba91-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Moxtra 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="6ba91-150">**若要設定與 Moxtra 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ba91-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6ba91-151">在 Azure 入口網站的 [Moxtra] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6ba91-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="6ba91-155">在 [Moxtra 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ba91-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="6ba91-157">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="6ba91-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="6ba91-158">Moxtra 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="6ba91-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="6ba91-159">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="6ba91-159">Configure the following claims for this application.</span></span> <span data-ttu-id="6ba91-160">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6ba91-161">以下螢幕擷取畫面顯示此設定的範例。</span><span class="sxs-lookup"><span data-stu-id="6ba91-161">The following screenshot shows an example for this configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="6ba91-163">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ba91-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="6ba91-164">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="6ba91-164">Attribute Name</span></span> | <span data-ttu-id="6ba91-165">屬性值</span><span class="sxs-lookup"><span data-stu-id="6ba91-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6ba91-166">firstname</span><span class="sxs-lookup"><span data-stu-id="6ba91-166">firstname</span></span> | <span data-ttu-id="6ba91-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6ba91-167">user.givenname</span></span> |
    | <span data-ttu-id="6ba91-168">lastname</span><span class="sxs-lookup"><span data-stu-id="6ba91-168">lastname</span></span> | <span data-ttu-id="6ba91-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="6ba91-169">user.surname</span></span> |
    | <span data-ttu-id="6ba91-170">idpid</span><span class="sxs-lookup"><span data-stu-id="6ba91-170">idpid</span></span>    | <span data-ttu-id="6ba91-171">< SAML 實體識別碼 ></span><span class="sxs-lookup"><span data-stu-id="6ba91-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="6ba91-172">**idpid** 值不是真實的屬性。</span><span class="sxs-lookup"><span data-stu-id="6ba91-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="6ba91-173">您可以從 [Moxtra 組態] 下的 [快速參考] 區段取得實際的值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="6ba91-174">a.</span><span class="sxs-lookup"><span data-stu-id="6ba91-174">a.</span></span> <span data-ttu-id="6ba91-175">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6ba91-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="6ba91-177">b.</span><span class="sxs-lookup"><span data-stu-id="6ba91-177">b.</span></span> <span data-ttu-id="6ba91-178">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="6ba91-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6ba91-180">c.</span><span class="sxs-lookup"><span data-stu-id="6ba91-180">c.</span></span> <span data-ttu-id="6ba91-181">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="6ba91-182">d.</span><span class="sxs-lookup"><span data-stu-id="6ba91-182">d.</span></span> <span data-ttu-id="6ba91-183">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6ba91-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="6ba91-184">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6ba91-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="6ba91-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ba91-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6ba91-188">在 [Moxtra 組態] 區段上，按一下 [設定 Moxtra] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6ba91-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6ba91-189">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="6ba91-191">在另一個瀏覽器視窗中，以系統管理員身分登入您的 Moxtra 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6ba91-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="6ba91-192">在左邊工具列中，按一下 [管理主控台] > [SAML 單一登入]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="6ba91-194">在 [SAML]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ba91-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="6ba91-196">a.</span><span class="sxs-lookup"><span data-stu-id="6ba91-196">a.</span></span> <span data-ttu-id="6ba91-197">在 [名稱] 文字方塊中，輸入您的設定名稱 (例如：*SAML*)。</span><span class="sxs-lookup"><span data-stu-id="6ba91-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="6ba91-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ba91-198">b.</span></span> <span data-ttu-id="6ba91-199">在 [IdP 實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 實體識別碼」**值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6ba91-200">c.</span><span class="sxs-lookup"><span data-stu-id="6ba91-200">c.</span></span> <span data-ttu-id="6ba91-201">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="6ba91-202">d.</span><span class="sxs-lookup"><span data-stu-id="6ba91-202">d.</span></span> <span data-ttu-id="6ba91-203">在 [AuthnContextClassRef] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="6ba91-204">e.</span><span class="sxs-lookup"><span data-stu-id="6ba91-204">e.</span></span> <span data-ttu-id="6ba91-205">在 [名稱識別碼格式] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="6ba91-206">f.</span><span class="sxs-lookup"><span data-stu-id="6ba91-206">f.</span></span> <span data-ttu-id="6ba91-207">在記事本中開啟您從 Azure 入口網站下載的憑證，複製其內容，然後貼到 [憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="6ba91-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="6ba91-208">g.</span><span class="sxs-lookup"><span data-stu-id="6ba91-208">g.</span></span> <span data-ttu-id="6ba91-209">在 SAML 電子郵件網域文字方塊中，輸入您的 SAML 電子郵件網域。</span><span class="sxs-lookup"><span data-stu-id="6ba91-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="6ba91-210">若要查看用來驗證網域的步驟，請按一下下方的 "**i**"。</span><span class="sxs-lookup"><span data-stu-id="6ba91-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="6ba91-211">h.</span><span class="sxs-lookup"><span data-stu-id="6ba91-211">h.</span></span> <span data-ttu-id="6ba91-212">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="6ba91-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="6ba91-213">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6ba91-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6ba91-214">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6ba91-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6ba91-215">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ba91-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ba91-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ba91-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ba91-217">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6ba91-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6ba91-219">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ba91-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6ba91-220">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6ba91-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6ba91-222">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ba91-224">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ba91-226">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ba91-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ba91-228">a.</span><span class="sxs-lookup"><span data-stu-id="6ba91-228">a.</span></span> <span data-ttu-id="6ba91-229">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ba91-230">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ba91-230">b.</span></span> <span data-ttu-id="6ba91-231">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ba91-232">c.</span><span class="sxs-lookup"><span data-stu-id="6ba91-232">c.</span></span> <span data-ttu-id="6ba91-233">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6ba91-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6ba91-234">d.</span><span class="sxs-lookup"><span data-stu-id="6ba91-234">d.</span></span> <span data-ttu-id="6ba91-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6ba91-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="6ba91-236">建立 Moxtra 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ba91-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="6ba91-237">本節的目標是要在 Moxtra 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6ba91-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="6ba91-238">**若要在 Moxtra 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ba91-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6ba91-239">以系統管理員身分登入您的 Moxtra 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6ba91-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="6ba91-240">在左邊工具列中，按一下 [管理主控台] > [使用者管理]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="6ba91-242">在 [加入使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6ba91-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="6ba91-243">a.</span><span class="sxs-lookup"><span data-stu-id="6ba91-243">a.</span></span> <span data-ttu-id="6ba91-244">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="6ba91-245">b.</span><span class="sxs-lookup"><span data-stu-id="6ba91-245">b.</span></span> <span data-ttu-id="6ba91-246">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="6ba91-247">c.</span><span class="sxs-lookup"><span data-stu-id="6ba91-247">c.</span></span> <span data-ttu-id="6ba91-248">在 [電子郵件] 文字方塊中，輸入 Britta 在 Azure 入口網站中的同一個電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6ba91-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="6ba91-249">d.</span><span class="sxs-lookup"><span data-stu-id="6ba91-249">d.</span></span> <span data-ttu-id="6ba91-250">在 [事業處] 文字方塊中，輸入 **Dev**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="6ba91-251">e.</span><span class="sxs-lookup"><span data-stu-id="6ba91-251">e.</span></span> <span data-ttu-id="6ba91-252">在 [部門] 文字方塊中，輸入 **IT**。</span><span class="sxs-lookup"><span data-stu-id="6ba91-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="6ba91-253">f.</span><span class="sxs-lookup"><span data-stu-id="6ba91-253">f.</span></span> <span data-ttu-id="6ba91-254">選取 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="6ba91-255">g.</span><span class="sxs-lookup"><span data-stu-id="6ba91-255">g.</span></span> <span data-ttu-id="6ba91-256">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="6ba91-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6ba91-257">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6ba91-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6ba91-258">在本節中，您會將 Moxtra 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6ba91-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![指派使用者][200] 

<span data-ttu-id="6ba91-260">**若要將 Britta Simon 指派給 Moxtra，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6ba91-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="6ba91-261">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6ba91-263">在應用程式清單中，選取 [Moxtra] 。</span><span class="sxs-lookup"><span data-stu-id="6ba91-263">In the applications list, select **Moxtra**.</span></span>

    ![設定單一登入](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="6ba91-265">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-265">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6ba91-267">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ba91-267">Click **Add** button.</span></span> <span data-ttu-id="6ba91-268">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6ba91-270">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6ba91-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6ba91-271">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ba91-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ba91-272">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6ba91-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ba91-273">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6ba91-273">Testing single sign-on</span></span>

<span data-ttu-id="6ba91-274">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6ba91-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6ba91-275">當您在存取面板中按一下 [Moxtra] 磚時，應該會自動登入您的 Moxtra 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ba91-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="6ba91-276">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6ba91-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ba91-277">其他資源</span><span class="sxs-lookup"><span data-stu-id="6ba91-277">Additional resources</span></span>

* [<span data-ttu-id="6ba91-278">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6ba91-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ba91-279">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6ba91-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

