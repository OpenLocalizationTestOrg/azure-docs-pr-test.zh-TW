---
title: "教學課程：Azure Active Directory 與 Blackboard Learn 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Blackboard Learn 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="fcad1-103">教學課程：Azure Active Directory 與 Blackboard Learn 整合</span><span class="sxs-lookup"><span data-stu-id="fcad1-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="fcad1-104">在本教學課程中，您將了解如何整合 Blackboard Learn 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fcad1-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fcad1-105">將 Blackboard Learn 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="fcad1-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fcad1-106">您可以在 Azure AD 中控制可存取 Blackboard Learn 的人員</span><span class="sxs-lookup"><span data-stu-id="fcad1-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="fcad1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Blackboard Learn (單一登入)</span><span class="sxs-lookup"><span data-stu-id="fcad1-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fcad1-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="fcad1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fcad1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fcad1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcad1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fcad1-110">Prerequisites</span></span>

<span data-ttu-id="fcad1-111">若要設定 Azure AD 與 Blackboard Learn 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="fcad1-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="fcad1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fcad1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fcad1-113">已啟用 Blackboard Learn 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fcad1-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fcad1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fcad1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fcad1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fcad1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fcad1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fcad1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fcad1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fcad1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fcad1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fcad1-118">Scenario description</span></span>
<span data-ttu-id="fcad1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fcad1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="fcad1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fcad1-121">從資源庫新增 Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="fcad1-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="fcad1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fcad1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="fcad1-123">從資源庫新增 Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="fcad1-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="fcad1-124">若要設定將 Blackboard Learn 整合到 Azure AD 中，您需要從資源庫將 Blackboard Learn 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="fcad1-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fcad1-125">**若要從資源庫中新增 Blackboard Learn，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fcad1-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fcad1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fcad1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fcad1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fcad1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fcad1-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcad1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fcad1-133">在搜尋方塊中，輸入 **Blackboard Learn**。</span><span class="sxs-lookup"><span data-stu-id="fcad1-133">In the search box, type **Blackboard Learn**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="fcad1-135">在結果面板中，選取 [Blackboard Learn]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcad1-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fcad1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fcad1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fcad1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Blackboard Learn 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fcad1-139">若要讓單一登入能夠運作，Azure AD 必須知道 Blackboard Learn 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="fcad1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="fcad1-140">換句話說，必須在 Azure AD 使用者與 Blackboard Learn 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fcad1-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="fcad1-141">建立此連結關聯性的方法，就是將 Blackboard Learn 中 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="fcad1-142">若要設定及測試與 Blackboard Learn 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="fcad1-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fcad1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="fcad1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fcad1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fcad1-145">**[建立 Blackboard Learn 測試使用者](#creating-a-blackboard-learn-test-user)** - 在 Blackboard Learn 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="fcad1-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fcad1-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fcad1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="fcad1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fcad1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fcad1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fcad1-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Blackboard Learn 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="fcad1-150">**若要設定與 Blackboard Learn 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fcad1-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="fcad1-151">在 Azure 入口網站的 [Blackboard Learn] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fcad1-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="fcad1-155">在 [Blackboard Learn 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fcad1-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="fcad1-157">a.</span><span class="sxs-lookup"><span data-stu-id="fcad1-157">a.</span></span> <span data-ttu-id="fcad1-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="fcad1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="fcad1-159">b.</span><span class="sxs-lookup"><span data-stu-id="fcad1-159">b.</span></span> <span data-ttu-id="fcad1-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="fcad1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="fcad1-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-161">These values are not real.</span></span> <span data-ttu-id="fcad1-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fcad1-163">請連絡 [Blackboard Learn 用戶端支援小組](https://www.blackboard.com/support/index.aspx)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="fcad1-164">Blackboard Learn 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="fcad1-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="fcad1-165">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="fcad1-165">Configure the following claims for this application.</span></span> <span data-ttu-id="fcad1-166">您可以在應用程式整合頁面的 [使用者屬性] 區段中，管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="fcad1-167">以下螢幕擷取畫面顯示其相關範例。</span><span class="sxs-lookup"><span data-stu-id="fcad1-167">The following screenshot shows an example about it.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="fcad1-169">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fcad1-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="fcad1-170">在這裡，我們已將 Userprincipalname 對應為唯一的使用者屬性，但您可以將它對應到適當的值，此值必須可在組織內唯一識別該使用者，並且對應到 Blackboard Learn 使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="fcad1-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="fcad1-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="fcad1-171">Attribute Name</span></span> | <span data-ttu-id="fcad1-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="fcad1-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="fcad1-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="fcad1-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="fcad1-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="fcad1-174">user.userprincipalname</span></span> |

    <span data-ttu-id="fcad1-175">a.</span><span class="sxs-lookup"><span data-stu-id="fcad1-175">a.</span></span> <span data-ttu-id="fcad1-176">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fcad1-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="fcad1-179">b.</span><span class="sxs-lookup"><span data-stu-id="fcad1-179">b.</span></span> <span data-ttu-id="fcad1-180">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="fcad1-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="fcad1-181">c.</span><span class="sxs-lookup"><span data-stu-id="fcad1-181">c.</span></span> <span data-ttu-id="fcad1-182">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="fcad1-183">d.</span><span class="sxs-lookup"><span data-stu-id="fcad1-183">d.</span></span> <span data-ttu-id="fcad1-184">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-184">Click **Ok**.</span></span>

4. <span data-ttu-id="fcad1-185">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="fcad1-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="fcad1-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcad1-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fcad1-189">在 [Blackboard Learn 組態] 區段上，按一下 [設定 Blackboard Learn] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="fcad1-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fcad1-190">從 [快速參考] 區段中複製「SAML 實體識別碼」。</span><span class="sxs-lookup"><span data-stu-id="fcad1-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="fcad1-192">若要在 **Blackboard Learn** 端設定單一登入，您必須將已下載的「中繼資料 XML」和「SAML 實體識別碼」傳送給 [Blackboard Learn 支援小組](https://www.blackboard.com/support/index.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fcad1-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="fcad1-193">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="fcad1-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fcad1-194">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="fcad1-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fcad1-195">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fcad1-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fcad1-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fcad1-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="fcad1-197">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fcad1-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fcad1-199">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fcad1-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fcad1-200">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fcad1-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fcad1-202">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fcad1-204">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fcad1-206">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fcad1-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fcad1-208">a.</span><span class="sxs-lookup"><span data-stu-id="fcad1-208">a.</span></span> <span data-ttu-id="fcad1-209">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fcad1-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fcad1-210">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcad1-210">b.</span></span> <span data-ttu-id="fcad1-211">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="fcad1-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="fcad1-212">c.</span><span class="sxs-lookup"><span data-stu-id="fcad1-212">c.</span></span> <span data-ttu-id="fcad1-213">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="fcad1-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fcad1-214">d.</span><span class="sxs-lookup"><span data-stu-id="fcad1-214">d.</span></span> <span data-ttu-id="fcad1-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fcad1-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="fcad1-216">建立 Blackboard Learn 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fcad1-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="fcad1-217">在本節中，您會在 Blackboard Learn 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fcad1-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="fcad1-218">Blackboard Learn 應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="fcad1-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="fcad1-219">請確定您已依照**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**一節所述的方式設定宣告</span><span class="sxs-lookup"><span data-stu-id="fcad1-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fcad1-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fcad1-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fcad1-221">在本節中，您會將 Blackboard Learn 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fcad1-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![指派使用者][200] 

<span data-ttu-id="fcad1-223">**若要將 Britta Simon 指派給 Blackboard Learn，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fcad1-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="fcad1-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fcad1-226">在應用程式清單中，選取 [Blackboard Learn]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="fcad1-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fcad1-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcad1-230">Click **Add** button.</span></span> <span data-ttu-id="fcad1-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fcad1-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="fcad1-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fcad1-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcad1-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fcad1-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcad1-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fcad1-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fcad1-236">Testing single sign-on</span></span>

<span data-ttu-id="fcad1-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="fcad1-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fcad1-238">當您在「存取面板」中按一下 [Blackboard Learn] 圖格時，應該會自動登入您的 Blackboard Learn 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcad1-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="fcad1-239">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="fcad1-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fcad1-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="fcad1-240">Additional resources</span></span>

* [<span data-ttu-id="fcad1-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="fcad1-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fcad1-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fcad1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

