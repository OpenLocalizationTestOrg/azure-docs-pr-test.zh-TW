---
title: "教學課程：Azure Active Directory 與 Slack 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Slack 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="1ef69-103">教學課程：Azure Active Directory 與 Slack 整合</span><span class="sxs-lookup"><span data-stu-id="1ef69-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="1ef69-104">在本教學課程中，您會了解如何整合 Slack 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1ef69-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ef69-105">Slack 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1ef69-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ef69-106">您可以在 Azure AD 中控制可存取 Slack</span><span class="sxs-lookup"><span data-stu-id="1ef69-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="1ef69-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Slack (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1ef69-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ef69-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1ef69-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ef69-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1ef69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ef69-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1ef69-110">Prerequisites</span></span>

<span data-ttu-id="1ef69-111">若要設定與 Slack 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1ef69-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="1ef69-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ef69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ef69-113">啟用 Slack 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ef69-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ef69-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ef69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ef69-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1ef69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ef69-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ef69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ef69-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1ef69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ef69-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1ef69-118">Scenario description</span></span>
<span data-ttu-id="1ef69-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ef69-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1ef69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ef69-121">從資源庫新增 Slack</span><span class="sxs-lookup"><span data-stu-id="1ef69-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="1ef69-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ef69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="1ef69-123">從資源庫新增 Slack</span><span class="sxs-lookup"><span data-stu-id="1ef69-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="1ef69-124">若要設定將 Slack 整合到 Azure AD 中，您需要從資源庫將 Slack 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1ef69-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ef69-125">**若要從資源庫新增 Slack，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ef69-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef69-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1ef69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ef69-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ef69-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1ef69-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ef69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1ef69-133">在 [搜尋方塊] 中，輸入 **Slack**。</span><span class="sxs-lookup"><span data-stu-id="1ef69-133">In the search box, type **Slack**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="1ef69-135">在結果窗格中，選取 [Slack]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ef69-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ef69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ef69-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Slack 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ef69-139">若要讓單一登入運作，Azure AD 必須知道 Slack 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ef69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="1ef69-140">換句話說，必須在 Azure AD 使用者和 Slack 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1ef69-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="1ef69-141">在 Slack 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1ef69-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ef69-142">若要設定及測試與 Slack 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="1ef69-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ef69-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1ef69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ef69-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ef69-145">**[建立 Slack 測試使用者](#creating-a-slack-test-user)** - 使 Slack 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="1ef69-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ef69-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ef69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1ef69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ef69-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ef69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ef69-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Slack 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="1ef69-150">**若要使用 Slack 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ef69-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef69-151">在 Azure 入口網站的 [Slack] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1ef69-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="1ef69-155">在 [Slack 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ef69-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="1ef69-157">a.</span><span class="sxs-lookup"><span data-stu-id="1ef69-157">a.</span></span> <span data-ttu-id="1ef69-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="1ef69-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="1ef69-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-159">b.</span></span> <span data-ttu-id="1ef69-160">在 [識別碼] 文字方塊中，輸入 URL：`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="1ef69-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ef69-161">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-161">The value is not real.</span></span> <span data-ttu-id="1ef69-162">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="1ef69-163">請連絡 [Slack 支援小組](https://slack.com/help/contact)以取得此值</span><span class="sxs-lookup"><span data-stu-id="1ef69-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="1ef69-164">Slack 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="1ef69-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1ef69-165">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="1ef69-165">Configure the following claims for this application.</span></span> <span data-ttu-id="1ef69-166">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1ef69-167">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="1ef69-167">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="1ef69-169">在 [單一登入] 對話方塊內的 [使用者屬性] 區段中，選取 [user.mail] 當作 [使用者識別碼]，並在下表顯示的每個列上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ef69-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="1ef69-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1ef69-170">Attribute Name</span></span> | <span data-ttu-id="1ef69-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="1ef69-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1ef69-172">first_name</span><span class="sxs-lookup"><span data-stu-id="1ef69-172">first_name</span></span> | <span data-ttu-id="1ef69-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1ef69-173">user.givenname</span></span> |
    | <span data-ttu-id="1ef69-174">last_name</span><span class="sxs-lookup"><span data-stu-id="1ef69-174">last_name</span></span> | <span data-ttu-id="1ef69-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="1ef69-175">user.surname</span></span> |
    | <span data-ttu-id="1ef69-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="1ef69-176">User.Email</span></span> | <span data-ttu-id="1ef69-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="1ef69-177">user.mail</span></span> |  
    | <span data-ttu-id="1ef69-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="1ef69-178">User.Username</span></span> | <span data-ttu-id="1ef69-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1ef69-179">user.userprincipalname</span></span> |

    <span data-ttu-id="1ef69-180">a.</span><span class="sxs-lookup"><span data-stu-id="1ef69-180">a.</span></span> <span data-ttu-id="1ef69-181">按一下 [屬性] 以開啟 [編輯屬性] 對話方塊，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ef69-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="1ef69-183">a.</span><span class="sxs-lookup"><span data-stu-id="1ef69-183">a.</span></span> <span data-ttu-id="1ef69-184">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1ef69-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1ef69-185">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-185">b.</span></span> <span data-ttu-id="1ef69-186">在 [值] 清單中，選取該資料列所顯示的屬性值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1ef69-187">c.</span><span class="sxs-lookup"><span data-stu-id="1ef69-187">c.</span></span> <span data-ttu-id="1ef69-188">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="1ef69-188">Click **OK**</span></span>

6. <span data-ttu-id="1ef69-189">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1ef69-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="1ef69-191">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ef69-191">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1ef69-193">在 [Slack 組態] 區段上，按一下 [設定 Slack] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1ef69-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ef69-194">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="1ef69-196">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Slack 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1ef69-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="1ef69-197">瀏覽至 [Microsoft Azure AD]，然後移至 [小組設定]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="1ef69-199">在 [小組設定] 區段中，按一下 [驗證] 索引標籤，然後按一下 [變更設定]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="1ef69-201">在 [SAML 驗證設定]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ef69-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="1ef69-203">a.</span><span class="sxs-lookup"><span data-stu-id="1ef69-203">a.</span></span>  <span data-ttu-id="1ef69-204">在 [SAML 2.0 端點]\(HTTP\) 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1ef69-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-205">b.</span></span>  <span data-ttu-id="1ef69-206">在 [識別提供者簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1ef69-207">c.</span><span class="sxs-lookup"><span data-stu-id="1ef69-207">c.</span></span>  <span data-ttu-id="1ef69-208">在記事本中開啟您下載的憑證檔，將其內容複製到剪貼簿上，然後貼到 [公開憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="1ef69-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="1ef69-209">d.</span><span class="sxs-lookup"><span data-stu-id="1ef69-209">d.</span></span> <span data-ttu-id="1ef69-210">針對您的 Slack 小組適當地設定上述三個設定。</span><span class="sxs-lookup"><span data-stu-id="1ef69-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="1ef69-211">如需這些這設定的詳細資訊，請參閱這裡的 **Slack 的 SSO 設定指南**。</span><span class="sxs-lookup"><span data-stu-id="1ef69-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="1ef69-212">e.</span><span class="sxs-lookup"><span data-stu-id="1ef69-212">e.</span></span>  <span data-ttu-id="1ef69-213">按一下 [儲存組態] 。</span><span class="sxs-lookup"><span data-stu-id="1ef69-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="1ef69-214">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1ef69-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ef69-215">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1ef69-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ef69-216">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ef69-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ef69-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ef69-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ef69-218">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1ef69-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1ef69-220">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ef69-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef69-221">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1ef69-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ef69-223">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ef69-225">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ef69-227">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ef69-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ef69-229">a.</span><span class="sxs-lookup"><span data-stu-id="1ef69-229">a.</span></span> <span data-ttu-id="1ef69-230">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1ef69-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ef69-231">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-231">b.</span></span> <span data-ttu-id="1ef69-232">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1ef69-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ef69-233">c.</span><span class="sxs-lookup"><span data-stu-id="1ef69-233">c.</span></span> <span data-ttu-id="1ef69-234">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1ef69-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ef69-235">d.</span><span class="sxs-lookup"><span data-stu-id="1ef69-235">d.</span></span> <span data-ttu-id="1ef69-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1ef69-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="1ef69-237">建立 Slack 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ef69-237">Creating a Slack test user</span></span>

<span data-ttu-id="1ef69-238">本節目標是在 Slack 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ef69-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="1ef69-239">Slack 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="1ef69-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1ef69-240">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="1ef69-240">There is no action item for you in this section.</span></span> <span data-ttu-id="1ef69-241">當您嘗試存取 Slack 時，如果 Slack 還沒有使用者，它就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ef69-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="1ef69-242">如果您需要手動建立使用者，就需要連絡 [Slack 支援小組](https://slack.com/help/contact)。</span><span class="sxs-lookup"><span data-stu-id="1ef69-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ef69-243">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ef69-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ef69-244">在本節中，您會將 Slack 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ef69-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![指派使用者][200] 

<span data-ttu-id="1ef69-246">**若要將 Britta Simon 指派到 Slack，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ef69-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="1ef69-247">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1ef69-249">在應用程式清單中，選取 [Slack]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-249">In the applications list, select **Slack**.</span></span>

    ![設定單一登入](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="1ef69-251">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-251">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1ef69-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ef69-253">Click **Add** button.</span></span> <span data-ttu-id="1ef69-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1ef69-256">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1ef69-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ef69-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ef69-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ef69-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ef69-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ef69-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1ef69-259">Testing single sign-on</span></span>

<span data-ttu-id="1ef69-260">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="1ef69-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ef69-261">當您在存取面板中按一下 Slack 圖格時，應該會自動登入您的 Slack 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ef69-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ef69-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="1ef69-262">Additional resources</span></span>

* [<span data-ttu-id="1ef69-263">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1ef69-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ef69-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1ef69-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

