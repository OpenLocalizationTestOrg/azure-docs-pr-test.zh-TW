---
title: "教學課程：Azure Active Directory 與 Clever 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Clever 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="0696e-103">教學課程：Azure Active Directory 與 Clever 整合</span><span class="sxs-lookup"><span data-stu-id="0696e-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="0696e-104">在本教學課程中，您會了解如何將 Clever 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="0696e-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0696e-105">Clever 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0696e-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0696e-106">您可以在 Azure AD 中控制可存取 Clever 的人員。</span><span class="sxs-lookup"><span data-stu-id="0696e-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="0696e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Clever (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="0696e-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0696e-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0696e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0696e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0696e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0696e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0696e-110">Prerequisites</span></span>

<span data-ttu-id="0696e-111">若要設定 Azure AD 與 Clever 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0696e-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="0696e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0696e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0696e-113">Clever 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0696e-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0696e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0696e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0696e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0696e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0696e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0696e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0696e-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0696e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0696e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0696e-118">Scenario description</span></span>
<span data-ttu-id="0696e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0696e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0696e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0696e-121">從資源庫新增 Clever</span><span class="sxs-lookup"><span data-stu-id="0696e-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="0696e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0696e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="0696e-123">從資源庫新增 Clever</span><span class="sxs-lookup"><span data-stu-id="0696e-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="0696e-124">若要設定將 Clever 整合到 Azure AD 中，您需要從資源庫將 Clever 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="0696e-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0696e-125">**若要從資源庫新增 Clever，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0696e-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0696e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0696e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="0696e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0696e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0696e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0696e-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="0696e-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="0696e-133">在搜尋方塊中，輸入 **Clever**，從結果面板中選取 [Clever]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0696e-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0696e-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0696e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0696e-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Clever 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0696e-137">若要讓單一登入運作，Azure AD 必須知道 Clever 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0696e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="0696e-138">換句話說，必須建立 Azure AD 使用者和 Clever 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0696e-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="0696e-139">在 Clever 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0696e-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0696e-140">若要設定及測試與 Clever 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="0696e-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0696e-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0696e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0696e-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0696e-143">**[建立 Clever 測試使用者](#create-a-clever-test-user)** - 使 Clever 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="0696e-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0696e-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0696e-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0696e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0696e-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0696e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0696e-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 Clever 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="0696e-148">**若要設定與 Clever 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0696e-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="0696e-149">在 Azure 入口網站的 [Clever] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0696e-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="0696e-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="0696e-153">在 [Clever 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0696e-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Clever 網域及 URL 單一登入資訊](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="0696e-155">a.</span><span class="sxs-lookup"><span data-stu-id="0696e-155">a.</span></span> <span data-ttu-id="0696e-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0696e-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="0696e-157">b.</span><span class="sxs-lookup"><span data-stu-id="0696e-157">b.</span></span> <span data-ttu-id="0696e-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="0696e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0696e-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0696e-159">These values are not real.</span></span> <span data-ttu-id="0696e-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="0696e-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0696e-161">請連絡 [Clever 用戶端支援小組](https://clever.com/about/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="0696e-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="0696e-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0696e-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="0696e-164">Clever 應用程式需要特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應加入 **SAML Token 屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="0696e-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="0696e-165">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="0696e-165">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="0696e-167">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0696e-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="0696e-168">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="0696e-168">Attribute Name</span></span>  | <span data-ttu-id="0696e-169">屬性值</span><span class="sxs-lookup"><span data-stu-id="0696e-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="0696e-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="0696e-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="0696e-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0696e-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="0696e-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="0696e-172">Firstname</span></span>  | <span data-ttu-id="0696e-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0696e-173">user.givenname</span></span> |
    | <span data-ttu-id="0696e-174">lastname</span><span class="sxs-lookup"><span data-stu-id="0696e-174">Lastname</span></span>  | <span data-ttu-id="0696e-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="0696e-175">user.surname</span></span> |    

    <span data-ttu-id="0696e-176">a.</span><span class="sxs-lookup"><span data-stu-id="0696e-176">a.</span></span> <span data-ttu-id="0696e-177">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0696e-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="0696e-180">b.</span><span class="sxs-lookup"><span data-stu-id="0696e-180">b.</span></span> <span data-ttu-id="0696e-181">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="0696e-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="0696e-182">c.</span><span class="sxs-lookup"><span data-stu-id="0696e-182">c.</span></span> <span data-ttu-id="0696e-183">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="0696e-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="0696e-184">d.</span><span class="sxs-lookup"><span data-stu-id="0696e-184">d.</span></span> <span data-ttu-id="0696e-185">[命名空間] 文字方塊保持空白。</span><span class="sxs-lookup"><span data-stu-id="0696e-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="0696e-186">d.</span><span class="sxs-lookup"><span data-stu-id="0696e-186">d.</span></span> <span data-ttu-id="0696e-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0696e-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="0696e-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-188">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0696e-190">若要產生**中繼資料** URL，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="0696e-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="0696e-191">a.</span><span class="sxs-lookup"><span data-stu-id="0696e-191">a.</span></span> <span data-ttu-id="0696e-192">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="0696e-192">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="0696e-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0696e-194">b.</span></span> <span data-ttu-id="0696e-195">按一下 [端點] 以開啟 [端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0696e-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="0696e-197">c.</span><span class="sxs-lookup"><span data-stu-id="0696e-197">c.</span></span> <span data-ttu-id="0696e-198">按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="0696e-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="0696e-200">d.</span><span class="sxs-lookup"><span data-stu-id="0696e-200">d.</span></span> <span data-ttu-id="0696e-201">現在，移至 [Clever] 的屬性頁面，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到記事本。</span><span class="sxs-lookup"><span data-stu-id="0696e-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="0696e-203">e.</span><span class="sxs-lookup"><span data-stu-id="0696e-203">e.</span></span> <span data-ttu-id="0696e-204">使用下列模式產生**中繼資料 URL**︰`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="0696e-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="0696e-205">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Clever 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0696e-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="0696e-206">在工具列中，按一下 [立即登入] 。</span><span class="sxs-lookup"><span data-stu-id="0696e-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="0696e-207">![立即登入](./media/active-directory-saas-clever-tutorial/ic798984.png "立即登入")</span><span class="sxs-lookup"><span data-stu-id="0696e-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="0696e-208">在 [立即登入]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0696e-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="0696e-209">![立即登入](./media/active-directory-saas-clever-tutorial/ic798985.png "立即登入")</span><span class="sxs-lookup"><span data-stu-id="0696e-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="0696e-210">a.</span><span class="sxs-lookup"><span data-stu-id="0696e-210">a.</span></span> <span data-ttu-id="0696e-211">輸入 [登入 URL] 。</span><span class="sxs-lookup"><span data-stu-id="0696e-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="0696e-212">[登入 URL] 是自訂值。</span><span class="sxs-lookup"><span data-stu-id="0696e-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="0696e-213">請連絡 [Clever 用戶端支援小組](https://clever.com/about/contact/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="0696e-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="0696e-214">b.</span><span class="sxs-lookup"><span data-stu-id="0696e-214">b.</span></span> <span data-ttu-id="0696e-215">針對 [識別系統]，選取 [ADFS]。</span><span class="sxs-lookup"><span data-stu-id="0696e-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="0696e-216">c.</span><span class="sxs-lookup"><span data-stu-id="0696e-216">c.</span></span> <span data-ttu-id="0696e-217">在 [中繼資料 URL]文字方塊中輸入**中繼資料 URL**。</span><span class="sxs-lookup"><span data-stu-id="0696e-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="0696e-218">d.</span><span class="sxs-lookup"><span data-stu-id="0696e-218">d.</span></span> <span data-ttu-id="0696e-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0696e-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0696e-220">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0696e-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0696e-221">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0696e-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0696e-222">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0696e-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0696e-223">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0696e-223">Create an Azure AD test user</span></span>

<span data-ttu-id="0696e-224">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0696e-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="0696e-226">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0696e-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0696e-227">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0696e-229">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0696e-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0696e-231">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0696e-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0696e-233">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0696e-233">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0696e-235">a.</span><span class="sxs-lookup"><span data-stu-id="0696e-235">a.</span></span> <span data-ttu-id="0696e-236">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0696e-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0696e-237">b.</span><span class="sxs-lookup"><span data-stu-id="0696e-237">b.</span></span> <span data-ttu-id="0696e-238">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0696e-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0696e-239">c.</span><span class="sxs-lookup"><span data-stu-id="0696e-239">c.</span></span> <span data-ttu-id="0696e-240">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="0696e-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0696e-241">d.</span><span class="sxs-lookup"><span data-stu-id="0696e-241">d.</span></span> <span data-ttu-id="0696e-242">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0696e-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="0696e-243">建立 Clever 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0696e-243">Create a Clever test user</span></span>

<span data-ttu-id="0696e-244">若要讓 Azure AD 使用者可以登入 Clever，必須將他們佈建到 Clever。</span><span class="sxs-lookup"><span data-stu-id="0696e-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="0696e-245">對於 Clever，配合 [Clever Client 支援小組](https://clever.com/about/contact/)，在 Clever 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="0696e-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="0696e-246">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="0696e-247">您可以使用任何其他的 Clever 使用者帳戶建立工具，或是使用 Clever 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0696e-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0696e-248">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0696e-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="0696e-249">在本節中，您會將 Clever 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0696e-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="0696e-251">**若要將 Britta Simon 指派給 Clever，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0696e-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="0696e-252">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0696e-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0696e-254">在應用程式清單中，選取 [Clever]。</span><span class="sxs-lookup"><span data-stu-id="0696e-254">In the applications list, select **Clever**.</span></span>

    ![應用程式清單中的 Clever 連結](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="0696e-256">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0696e-256">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="0696e-258">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-258">Click **Add** button.</span></span> <span data-ttu-id="0696e-259">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0696e-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="0696e-261">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0696e-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0696e-262">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0696e-263">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0696e-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0696e-264">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0696e-264">Test single sign-on</span></span>

<span data-ttu-id="0696e-265">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0696e-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0696e-266">當您在「存取面板」中按一下 Clever 圖格時，應該會自動登入您的 Clever 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0696e-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="0696e-267">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="0696e-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0696e-268">其他資源</span><span class="sxs-lookup"><span data-stu-id="0696e-268">Additional resources</span></span>

* [<span data-ttu-id="0696e-269">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0696e-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0696e-270">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0696e-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

