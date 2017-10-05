---
title: "教學課程：Azure Active Directory 與 Veracode 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Veracode 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d49349c5ae08e67d91e30967f3644623211823ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="1d0a7-103">教學課程：Azure Active Directory 與 Veracode 整合</span><span class="sxs-lookup"><span data-stu-id="1d0a7-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="1d0a7-104">在本教學課程中，您會了解如何整合 Veracode 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-104">In this tutorial, you learn how to integrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d0a7-105">Veracode 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-105">Integrating Veracode with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d0a7-106">您可以在 Azure AD 中管控可存取 Veracode 的人員。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-106">You can control in Azure AD who has access to Veracode.</span></span>
- <span data-ttu-id="1d0a7-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Veracode (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-107">You can enable your users to automatically get signed-on to Veracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1d0a7-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1d0a7-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d0a7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d0a7-110">Prerequisites</span></span>

<span data-ttu-id="1d0a7-111">若要設定 Azure AD 與 Veracode 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-111">To configure Azure AD integration with Veracode, you need the following items:</span></span>

- <span data-ttu-id="1d0a7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d0a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d0a7-113">已啟用 Veracode 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d0a7-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d0a7-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d0a7-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d0a7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d0a7-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d0a7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1d0a7-118">Scenario description</span></span>
<span data-ttu-id="1d0a7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d0a7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d0a7-121">從資源庫新增 Veracode</span><span class="sxs-lookup"><span data-stu-id="1d0a7-121">Add Veracode from the gallery</span></span>
2. <span data-ttu-id="1d0a7-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d0a7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-the-gallery"></a><span data-ttu-id="1d0a7-123">從資源庫新增 Veracode</span><span class="sxs-lookup"><span data-stu-id="1d0a7-123">Add Veracode from the gallery</span></span>
<span data-ttu-id="1d0a7-124">若要設定將 Veracode 整合到 Azure AD 中，您需要從資源庫將 Veracode 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-124">To configure the integration of Veracode into Azure AD, you need to add Veracode from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d0a7-125">**若要從資源庫新增 Veracode，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-125">**To add Veracode from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d0a7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="1d0a7-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d0a7-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="1d0a7-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="1d0a7-133">在搜尋方塊中，輸入 **Veracode**，從結果面板中選取 **Veracode**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-133">In the search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1d0a7-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d0a7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1d0a7-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Veracode 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d0a7-137">若要讓單一登入運作，Azure AD 必須知道 Veracode 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Veracode is to a user in Azure AD.</span></span> <span data-ttu-id="1d0a7-138">換句話說，必須在 Azure AD 使用者和 Veracode 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-138">In other words, a link relationship between an Azure AD user and the related user in Veracode needs to be established.</span></span>

<span data-ttu-id="1d0a7-139">在 Veracode 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-139">In Veracode, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1d0a7-140">若要使用 Veracode 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-140">To configure and test Azure AD single sign-on with Veracode, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d0a7-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d0a7-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d0a7-143">**[建立 Veracode 測試使用者](#create-a-veracode-test-user)** - 讓 Veracode 中對應的 Britta Simon 連結到使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - to have a counterpart of Britta Simon in Veracode that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d0a7-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d0a7-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1d0a7-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1d0a7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1d0a7-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Veracode 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="1d0a7-148">**若要使用 Veracode 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-148">**To configure Azure AD single sign-on with Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="1d0a7-149">在 Azure 入口網站的 [Veracode] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-149">In the Azure portal, on the **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="1d0a7-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="1d0a7-153">在 [Veracode 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已預先與 Azure 整合。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-153">On the **Veracode Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![設定單一登入](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="1d0a7-155">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-155">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="1d0a7-157">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Veracode。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-157">The objective of this section is to outline how to enable users to authenticate to Veracode with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="1d0a7-158">Veracode 應用程式需要特定格式的 SAML 判斷提示，要求您加入自訂屬性對應到您的 **SAML 權杖屬性** 組態。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-158">Your Veracode application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="1d0a7-159">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-159">The following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="1d0a7-160">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="1d0a7-161">若要加入必要的屬性對應，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-161">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="1d0a7-162">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1d0a7-162">Attribute Name</span></span> | <span data-ttu-id="1d0a7-163">屬性值</span><span class="sxs-lookup"><span data-stu-id="1d0a7-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="1d0a7-164">firstname</span><span class="sxs-lookup"><span data-stu-id="1d0a7-164">firstname</span></span> |<span data-ttu-id="1d0a7-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="1d0a7-165">User.givenname</span></span> |
    | <span data-ttu-id="1d0a7-166">lastname</span><span class="sxs-lookup"><span data-stu-id="1d0a7-166">lastname</span></span> |<span data-ttu-id="1d0a7-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="1d0a7-167">User.surname</span></span> |
    | <span data-ttu-id="1d0a7-168">電子郵件</span><span class="sxs-lookup"><span data-stu-id="1d0a7-168">email</span></span> |<span data-ttu-id="1d0a7-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="1d0a7-169">User.mail</span></span> |
    
    <span data-ttu-id="1d0a7-170">a.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-170">a.</span></span> <span data-ttu-id="1d0a7-171">針對上表中的每個資料列，按一下 [新增使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-171">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="1d0a7-172">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="1d0a7-173">![屬性](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="1d0a7-174">b.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-174">b.</span></span> <span data-ttu-id="1d0a7-175">在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-175">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1d0a7-176">c.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-176">c.</span></span> <span data-ttu-id="1d0a7-177">在 [屬性值]  文字方塊中，選取該資料列所顯示的屬性值。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-177">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1d0a7-178">d.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-178">d.</span></span> <span data-ttu-id="1d0a7-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-179">Click **Ok**.</span></span>

7. <span data-ttu-id="1d0a7-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-180">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1d0a7-182">在 [Veracode 組態] 區段上，按一下 [設定 Veracode] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-182">On the **Veracode Configuration** section, click **Configure Veracode** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1d0a7-183">從 [快速參考] 區段中複製 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-183">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Veracode 組態](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="1d0a7-185">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Veracode 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="1d0a7-186">在頂端功能表中，按一下 [設定]，然後按一下 [管理員]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-186">In the menu on the top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="1d0a7-187">![管理](./media/active-directory-saas-veracode-tutorial/ic802911.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="1d0a7-188">按一下 [SAML]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-188">Click the **SAML** tab.</span></span>

12. <span data-ttu-id="1d0a7-189">在 [組織 SAML 設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-189">In the **Organization SAML Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1d0a7-190">![管理](./media/active-directory-saas-veracode-tutorial/ic802912.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="1d0a7-191">a.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-191">a.</span></span>  <span data-ttu-id="1d0a7-192">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-192">In  **Issuer** textbox, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1d0a7-193">b.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-193">b.</span></span> <span data-ttu-id="1d0a7-194">若要上傳從 Azure 入口網站下載的憑證，請按一下 [選擇檔案]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-194">To upload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="1d0a7-195">c.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-195">c.</span></span> <span data-ttu-id="1d0a7-196">選取 [啟用自動註冊] 。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="1d0a7-197">在 [自動註冊設定] 區段上，執行下列步驟，然後按一下 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-197">In the **Self Registration Settings** section, perform the following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="1d0a7-198">![管理](./media/active-directory-saas-veracode-tutorial/ic802913.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1d0a7-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="1d0a7-199">a.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-199">a.</span></span> <span data-ttu-id="1d0a7-200">在 [啟用新的使用者] 選取 [不需要啟用]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="1d0a7-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-201">b.</span></span> <span data-ttu-id="1d0a7-202">在 [使用者資料更新] 選取 [Veracode 使用者資料喜好設定]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="1d0a7-203">c.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-203">c.</span></span> <span data-ttu-id="1d0a7-204">針對 [SAML 屬性詳細資料] ，請選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-204">For **SAML Attribute Details**, select the following:</span></span>
      * <span data-ttu-id="1d0a7-205">**[使用者角色]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-205">**User Roles**</span></span>
      * <span data-ttu-id="1d0a7-206">**[原則系統管理員]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="1d0a7-207">**[檢閱者]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-207">**Reviewer**</span></span>
      * <span data-ttu-id="1d0a7-208">**[安全性負責人]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-208">**Security Lead**</span></span>
      * <span data-ttu-id="1d0a7-209">**[行政人員]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-209">**Executive**</span></span>
      * <span data-ttu-id="1d0a7-210">**[傳送者]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-210">**Submitter**</span></span>
      * <span data-ttu-id="1d0a7-211">**[建立者]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-211">**Creator**</span></span>
      * <span data-ttu-id="1d0a7-212">**[所有掃描類型]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-212">**All Scan Types**</span></span>
      * <span data-ttu-id="1d0a7-213">**[小組成員資格]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-213">**Team Memberships**</span></span>
      * <span data-ttu-id="1d0a7-214">**[預設小組]**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="1d0a7-215">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1d0a7-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d0a7-216">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d0a7-217">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d0a7-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1d0a7-218">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d0a7-218">Create an Azure AD test user</span></span>

<span data-ttu-id="1d0a7-219">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="1d0a7-221">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d0a7-222">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1d0a7-224">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1d0a7-226">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1d0a7-228">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d0a7-228">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1d0a7-230">a.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-230">a.</span></span> <span data-ttu-id="1d0a7-231">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d0a7-232">b.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-232">b.</span></span> <span data-ttu-id="1d0a7-233">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1d0a7-234">c.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-234">c.</span></span> <span data-ttu-id="1d0a7-235">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1d0a7-236">d.</span><span class="sxs-lookup"><span data-stu-id="1d0a7-236">d.</span></span> <span data-ttu-id="1d0a7-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="1d0a7-238">建立 Veracode 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d0a7-238">Create a Veracode test user</span></span>
<span data-ttu-id="1d0a7-239">若要讓 Azure AD 使用者可以登入 Veracode，則必須將他們佈建到 Veracode。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-239">In order to enable Azure AD users to log into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="1d0a7-240">若是 Veracode 的情況 來佈建是自動化的工作。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-240">In the case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="1d0a7-241">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-241">There is no action item for you.</span></span> <span data-ttu-id="1d0a7-242">第一次嘗試單一登入時，會視需要自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-242">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="1d0a7-243">您可以使用任何其他的 Veracode 使用者帳戶建立工具或Veracode 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-243">You can use any other Veracode user account creation tools or APIs provided by Veracode to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1d0a7-244">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1d0a7-244">Assign the Azure AD test user</span></span>

<span data-ttu-id="1d0a7-245">在本節中，您會將 Veracode 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veracode.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="1d0a7-247">**若要將 Britta Simon 指派給 Veracode，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1d0a7-247">**To assign Britta Simon to Veracode, perform the following steps:**</span></span>

1. <span data-ttu-id="1d0a7-248">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1d0a7-250">在應用程式清單中，選取 [Veracode]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-250">In the applications list, select **Veracode**.</span></span>

    ![應用程式清單中的 Veracode 連結](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="1d0a7-252">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-252">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="1d0a7-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-254">Click **Add** button.</span></span> <span data-ttu-id="1d0a7-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="1d0a7-257">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d0a7-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d0a7-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1d0a7-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1d0a7-260">Test single sign-on</span></span>

<span data-ttu-id="1d0a7-261">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d0a7-262">當您在存取面板中按一下 [Veracode] 圖格時，應該會自動登入您的 Veracode 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-262">When you click the Veracode tile in the Access Panel, you should get automatically signed-on to your Veracode application.</span></span>
<span data-ttu-id="1d0a7-263">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1d0a7-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1d0a7-264">其他資源</span><span class="sxs-lookup"><span data-stu-id="1d0a7-264">Additional resources</span></span>

* [<span data-ttu-id="1d0a7-265">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1d0a7-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d0a7-266">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1d0a7-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

