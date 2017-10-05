---
title: "教學課程：Azure Active Directory 與 Trello 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Trello 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="bf599-103">教學課程：Azure Active Directory 與 Trello 整合</span><span class="sxs-lookup"><span data-stu-id="bf599-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="bf599-104">在本教學課程中，您將了解如何整合 Trello 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bf599-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf599-105">Trello 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="bf599-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf599-106">您可以在 Azure AD 中控制可存取 Trello 的人員</span><span class="sxs-lookup"><span data-stu-id="bf599-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="bf599-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Trello (單一登入)</span><span class="sxs-lookup"><span data-stu-id="bf599-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf599-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="bf599-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf599-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bf599-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf599-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf599-110">Prerequisites</span></span>

<span data-ttu-id="bf599-111">若要設定 Azure AD 與 Trello 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="bf599-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="bf599-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bf599-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf599-113">已啟用 Trello 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bf599-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf599-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bf599-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf599-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bf599-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf599-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bf599-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf599-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="bf599-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf599-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bf599-118">Scenario description</span></span>
<span data-ttu-id="bf599-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf599-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="bf599-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf599-121">從資源庫新增 Trello</span><span class="sxs-lookup"><span data-stu-id="bf599-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="bf599-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf599-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="bf599-123">從資源庫新增 Trello</span><span class="sxs-lookup"><span data-stu-id="bf599-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="bf599-124">如要設定將 Trello 整合到 Azure AD 中，您需要從資源庫把 Trello 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="bf599-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf599-125">**若要從資源庫新增 Trello，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bf599-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf599-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="bf599-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf599-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bf599-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf599-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bf599-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="bf599-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf599-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="bf599-133">在搜尋方塊中，輸入 **Trello**。</span><span class="sxs-lookup"><span data-stu-id="bf599-133">In the search box, type **Trello**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="bf599-135">在結果窗格中，選取 [Trello]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf599-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf599-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf599-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf599-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Trello 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bf599-139">若要讓單一登入能夠運作，Azure AD 必須知道 Trello 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf599-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="bf599-140">換句話說，必須要建立某位 Azure AD 使用者與 Trello 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bf599-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="bf599-141">在 Trello 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bf599-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf599-142">若要設定及測試與 Trello 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="bf599-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf599-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="bf599-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf599-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf599-145">**[建立 Trello 測試使用者](#creating-a-trello-test-user)** - 使 Trello 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="bf599-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf599-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf599-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="bf599-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf599-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf599-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf599-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Trello 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="bf599-150">**若要使用 Trello 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bf599-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="bf599-151">在 Azure 入口網站的 [Trello] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="bf599-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="bf599-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="bf599-155">如果您想要以 **IDP 起始模式**設定應用程式，請在 [Trello 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bf599-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="bf599-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="bf599-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="bf599-158">如果您想要以 **SP 起始模式**設定應用程式，請在 [Trello 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bf599-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="bf599-160">a.</span><span class="sxs-lookup"><span data-stu-id="bf599-160">a.</span></span> <span data-ttu-id="bf599-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="bf599-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="bf599-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf599-162">b.</span></span> <span data-ttu-id="bf599-163">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="bf599-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="bf599-164">您應該會從 Trello 取得 **\<enterprise\>** slug。</span><span class="sxs-lookup"><span data-stu-id="bf599-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="bf599-165">如果您沒有 Slug 值，請連絡 [Trello 支援小組](mailto:support@trello.com)以取得貴企業的 Slug。</span><span class="sxs-lookup"><span data-stu-id="bf599-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="bf599-166">Trello 應用程式預期 SAML 判斷提示會包含特定屬性。</span><span class="sxs-lookup"><span data-stu-id="bf599-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="bf599-167">設定此應用程式的下列屬性。</span><span class="sxs-lookup"><span data-stu-id="bf599-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="bf599-168">您可以從應用程式的 [使用者屬性] 管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="bf599-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="bf599-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="bf599-169">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="bf599-171">在 [SAML Token 屬性]  對話方塊上，針對下表中顯示的每一列執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bf599-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="bf599-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="bf599-172">Attribute Name</span></span> | <span data-ttu-id="bf599-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="bf599-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bf599-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="bf599-174">User.Email</span></span> | <span data-ttu-id="bf599-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="bf599-175">user.mail</span></span> |
    | <span data-ttu-id="bf599-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="bf599-176">User.FirstName</span></span> | <span data-ttu-id="bf599-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="bf599-177">user.givenname</span></span> |
    | <span data-ttu-id="bf599-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="bf599-178">User.LastName</span></span> | <span data-ttu-id="bf599-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="bf599-179">user.surname</span></span> |

    <span data-ttu-id="bf599-180">a.</span><span class="sxs-lookup"><span data-stu-id="bf599-180">a.</span></span> <span data-ttu-id="bf599-181">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="bf599-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="bf599-184">b.</span><span class="sxs-lookup"><span data-stu-id="bf599-184">b.</span></span> <span data-ttu-id="bf599-185">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="bf599-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="bf599-186">c.</span><span class="sxs-lookup"><span data-stu-id="bf599-186">c.</span></span> <span data-ttu-id="bf599-187">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="bf599-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bf599-188">d.</span><span class="sxs-lookup"><span data-stu-id="bf599-188">d.</span></span> <span data-ttu-id="bf599-189">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bf599-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="bf599-190">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="bf599-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="bf599-192">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf599-192">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf599-194">在 [Trello 組態] 區段上，按一下 [設定 Trello] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="bf599-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf599-195">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="bf599-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="bf599-197">若要取得為應用程式設定的 SSO，請移至 [Trello 企業 SSO 組態](https://trello.com/sso-configuration) 頁面，將 **SAML 單一登入服務 URL** 傳送給 [Trello 支援小組](mailto:support@trello.com)並附加**憑證 (Base64)**。</span><span class="sxs-lookup"><span data-stu-id="bf599-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="bf599-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="bf599-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf599-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="bf599-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf599-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf599-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf599-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf599-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf599-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bf599-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="bf599-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bf599-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf599-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="bf599-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf599-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bf599-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf599-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bf599-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf599-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bf599-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf599-213">a.</span><span class="sxs-lookup"><span data-stu-id="bf599-213">a.</span></span> <span data-ttu-id="bf599-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bf599-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf599-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf599-215">b.</span></span> <span data-ttu-id="bf599-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="bf599-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf599-217">c.</span><span class="sxs-lookup"><span data-stu-id="bf599-217">c.</span></span> <span data-ttu-id="bf599-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="bf599-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf599-219">d.</span><span class="sxs-lookup"><span data-stu-id="bf599-219">d.</span></span> <span data-ttu-id="bf599-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bf599-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="bf599-221">建立 Trello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf599-221">Creating a Trello test user</span></span>

<span data-ttu-id="bf599-222">在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf599-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="bf599-223">在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf599-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="bf599-224">Trello 支援即時佈建，而且會在您第一次從 Azure AD 登入時建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf599-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf599-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf599-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf599-226">在本節中，您會將 Trello 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf599-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![指派使用者][200] 

<span data-ttu-id="bf599-228">**若要將 Britta Simon 指派到 Trello，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bf599-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="bf599-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bf599-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="bf599-231">在應用程式清單中，選取 [Trello] 。</span><span class="sxs-lookup"><span data-stu-id="bf599-231">In the applications list, select **Trello**.</span></span>

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="bf599-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bf599-233">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="bf599-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf599-235">Click **Add** button.</span></span> <span data-ttu-id="bf599-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bf599-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="bf599-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="bf599-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf599-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf599-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf599-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf599-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf599-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bf599-241">Testing single sign-on</span></span>

<span data-ttu-id="bf599-242">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="bf599-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bf599-243">當您在存取面板中按一下 Trello 圖格時，應該會自動登入您的 Trello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf599-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf599-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="bf599-244">Additional resources</span></span>

* [<span data-ttu-id="bf599-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="bf599-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf599-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bf599-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

