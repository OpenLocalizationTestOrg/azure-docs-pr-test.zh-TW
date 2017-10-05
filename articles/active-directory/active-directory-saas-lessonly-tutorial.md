---
title: "教學課程：Azure Active Directory 與 Lesson.ly 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lesson.ly 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fc1e1b2de0a138dbe88d794f802b002321948ab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="12a01-103">教學課程：Azure Active Directory 與 Lesson.ly 整合</span><span class="sxs-lookup"><span data-stu-id="12a01-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="12a01-104">在本教學課程中，您將了解如何整合 Lesson.ly 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="12a01-104">In this tutorial, you learn how to integrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12a01-105">Lesson.ly 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="12a01-105">Integrating Lesson.ly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="12a01-106">您可以在 Azure AD 中控制可存取 Lesson.ly 的人員</span><span class="sxs-lookup"><span data-stu-id="12a01-106">You can control in Azure AD who has access to Lesson.ly</span></span>
- <span data-ttu-id="12a01-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Lesson.ly (單一登入)</span><span class="sxs-lookup"><span data-stu-id="12a01-107">You can enable your users to automatically get signed-on to Lesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12a01-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="12a01-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="12a01-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="12a01-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12a01-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="12a01-110">Prerequisites</span></span>

<span data-ttu-id="12a01-111">若要設定 Lesson.ly 與 Azure AD 的整合作業，需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="12a01-111">To configure Azure AD integration with Lesson.ly, you need the following items:</span></span>

- <span data-ttu-id="12a01-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="12a01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12a01-113">已啟用 Lesson.ly 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="12a01-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12a01-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="12a01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12a01-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="12a01-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12a01-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="12a01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12a01-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="12a01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12a01-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="12a01-118">Scenario description</span></span>
<span data-ttu-id="12a01-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12a01-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="12a01-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12a01-121">從資源庫加入 Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="12a01-121">Adding Lesson.ly from the gallery</span></span>
2. <span data-ttu-id="12a01-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12a01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-the-gallery"></a><span data-ttu-id="12a01-123">從資源庫加入 Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="12a01-123">Adding Lesson.ly from the gallery</span></span>
<span data-ttu-id="12a01-124">若要設定 Lesson.ly 與 Azure AD 的整合作業，您需要從資源庫將 Lesson.ly 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="12a01-124">To configure the integration of Lesson.ly into Azure AD, you need to add Lesson.ly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="12a01-125">**若要從資源庫加入 Lesson.ly，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="12a01-125">**To add Lesson.ly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="12a01-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="12a01-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12a01-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12a01-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="12a01-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12a01-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="12a01-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12a01-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="12a01-133">在搜尋方塊中，輸入 **Lesson.ly**。</span><span class="sxs-lookup"><span data-stu-id="12a01-133">In the search box, type **Lesson.ly**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="12a01-135">在結果窗格中，選取 [Lesson.ly]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="12a01-135">In the results panel, select **Lesson.ly**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12a01-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12a01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12a01-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lesson.ly 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12a01-139">若要讓單一登入作用，Azure AD 必須能知道 Lesson.ly 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="12a01-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lesson.ly is to a user in Azure AD.</span></span> <span data-ttu-id="12a01-140">換句話說，必須建立 Azure AD 使用者和 Lesson.ly 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="12a01-140">In other words, a link relationship between an Azure AD user and the related user in Lesson.ly needs to be established.</span></span>

<span data-ttu-id="12a01-141">在 Lesson.ly 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="12a01-141">In Lesson.ly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="12a01-142">若要使用 Lesson.ly 設定及測試 Azure AD 單一登入功能，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="12a01-142">To configure and test Azure AD single sign-on with Lesson.ly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="12a01-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="12a01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="12a01-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12a01-145">**[建立 Lesson.ly 測試使用者](#creating-a-lessonly-test-user)** - 使 Lesson.ly 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="12a01-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - to have a counterpart of Britta Simon in Lesson.ly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="12a01-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12a01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="12a01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12a01-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12a01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12a01-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Lesson.ly 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="12a01-150">**若要使用 Lesson.ly 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="12a01-150">**To configure Azure AD single sign-on with Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="12a01-151">在 Azure 入口網站的 [Lesson.ly] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="12a01-151">In the Azure portal, on the **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="12a01-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="12a01-155">在 [Lesson.ly 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12a01-155">On the **Lesson.ly Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="12a01-157">a.</span><span class="sxs-lookup"><span data-stu-id="12a01-157">a.</span></span> <span data-ttu-id="12a01-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="12a01-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="12a01-159">參考一般名稱時，**companyname** 需要由實際名稱取代。</span><span class="sxs-lookup"><span data-stu-id="12a01-159">When referencing a generic name that **companyname** needs to be replaced by an actual name.</span></span>
    
    <span data-ttu-id="12a01-160">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="12a01-160">b.</span></span> <span data-ttu-id="12a01-161">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="12a01-161">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="12a01-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="12a01-162">These values are not real.</span></span> <span data-ttu-id="12a01-163">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="12a01-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12a01-164">請連絡 [Lesson.ly 客戶支援小組](mailto:dev@lessonly.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="12a01-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) to get these values.</span></span> 

4. <span data-ttu-id="12a01-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="12a01-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="12a01-167">Lesson.ly 應用程式需要特定格式的 SAML 判斷提示，需要您加入自訂屬性對應到您的 **SAML Token 屬性** 設定。以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="12a01-167">The Lesson.ly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="12a01-169">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12a01-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="12a01-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="12a01-170">Attribute Name</span></span>   | <span data-ttu-id="12a01-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="12a01-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="12a01-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="12a01-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="12a01-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="12a01-173">user.givenname</span></span> |
    | <span data-ttu-id="12a01-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="12a01-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="12a01-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="12a01-175">user.surname</span></span> |
    | <span data-ttu-id="12a01-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="12a01-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="12a01-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="12a01-177">user.mail</span></span> |

    <span data-ttu-id="12a01-178">a.</span><span class="sxs-lookup"><span data-stu-id="12a01-178">a.</span></span> <span data-ttu-id="12a01-179">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="12a01-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="12a01-182">b.</span><span class="sxs-lookup"><span data-stu-id="12a01-182">b.</span></span> <span data-ttu-id="12a01-183">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="12a01-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="12a01-184">c.</span><span class="sxs-lookup"><span data-stu-id="12a01-184">c.</span></span> <span data-ttu-id="12a01-185">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="12a01-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="12a01-186">d.</span><span class="sxs-lookup"><span data-stu-id="12a01-186">d.</span></span> <span data-ttu-id="12a01-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="12a01-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="12a01-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="12a01-188">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="12a01-190">在 [Lesson.ly 組態] 區段上，按一下 [設定 Lesson.ly] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="12a01-190">On the **Lesson.ly Configuration** section, click **Configure Lesson.ly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="12a01-191">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="12a01-191">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="12a01-193">若要在 **Lesson.ly** 端設定單一登入，您必須將已下載的「憑證 (Base64)」、「登出 URL、SAML實體辨識碼和 SAML 單一登入服務 URL」 傳送給 [Lesson.ly 支援小組](mailto:dev@lessonly.com)。</span><span class="sxs-lookup"><span data-stu-id="12a01-193">To configure single sign-on on **Lesson.ly** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="12a01-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="12a01-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="12a01-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="12a01-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="12a01-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12a01-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12a01-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12a01-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="12a01-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="12a01-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="12a01-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="12a01-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="12a01-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="12a01-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12a01-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="12a01-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12a01-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="12a01-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12a01-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12a01-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12a01-209">a.</span><span class="sxs-lookup"><span data-stu-id="12a01-209">a.</span></span> <span data-ttu-id="12a01-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="12a01-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12a01-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="12a01-211">b.</span></span> <span data-ttu-id="12a01-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="12a01-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12a01-213">c.</span><span class="sxs-lookup"><span data-stu-id="12a01-213">c.</span></span> <span data-ttu-id="12a01-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="12a01-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="12a01-215">d.</span><span class="sxs-lookup"><span data-stu-id="12a01-215">d.</span></span> <span data-ttu-id="12a01-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="12a01-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="12a01-217">建立 Lesson.ly 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12a01-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="12a01-218">本節的目標是要在 Lesson.ly 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="12a01-218">The objective of this section is to create a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="12a01-219">Lesson.ly 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="12a01-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="12a01-220">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="12a01-220">There is no action item for you in this section.</span></span> <span data-ttu-id="12a01-221">嘗試存取 Lesson.ly 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="12a01-221">A new user will be created during an attempt to access Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="12a01-222">如果您需要手動建立使用者，您需要連絡 [Lesson.ly 支援小組](mailto:dev@lessonly.com)。</span><span class="sxs-lookup"><span data-stu-id="12a01-222">If you need to create an user manually, you need to contact the [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="12a01-223">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12a01-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="12a01-224">在本節中，您會將 Lesson.ly 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12a01-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lesson.ly.</span></span>

![指派使用者][200] 

<span data-ttu-id="12a01-226">**若要將 Britta Simon 指派到 Lesson.ly，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="12a01-226">**To assign Britta Simon to Lesson.ly, perform the following steps:**</span></span>

1. <span data-ttu-id="12a01-227">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="12a01-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="12a01-229">在應用程式清單中，選取 [Lesson.ly] 。</span><span class="sxs-lookup"><span data-stu-id="12a01-229">In the applications list, select **Lesson.ly**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="12a01-231">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="12a01-231">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="12a01-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12a01-233">Click **Add** button.</span></span> <span data-ttu-id="12a01-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="12a01-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="12a01-236">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="12a01-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="12a01-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12a01-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12a01-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12a01-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12a01-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="12a01-239">Testing single sign-on</span></span>

<span data-ttu-id="12a01-240">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="12a01-240">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="12a01-241">當您在存取面板中按一下 Lesson.ly 圖示時，應該會自動登入 Lesson.ly 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12a01-241">When you click the Lesson.ly tile in the Access Panel, you should get automatically signed-on to your Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12a01-242">其他資源</span><span class="sxs-lookup"><span data-stu-id="12a01-242">Additional resources</span></span>

* [<span data-ttu-id="12a01-243">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="12a01-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12a01-244">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="12a01-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

