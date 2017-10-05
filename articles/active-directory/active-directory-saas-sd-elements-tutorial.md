---
title: "教學課程：Azure Active Directory 與 SD Elements 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SD Elements 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="c5dda-103">教學課程：Azure Active Directory 與 SD Elements 整合</span><span class="sxs-lookup"><span data-stu-id="c5dda-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="c5dda-104">在本教學課程中，您將了解如何整合 SD Elements 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c5dda-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5dda-105">SD Elements 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="c5dda-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5dda-106">您可以在 Azure AD 中控制可存取 SD Elements 的人員</span><span class="sxs-lookup"><span data-stu-id="c5dda-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="c5dda-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SD Elements (單一登入)</span><span class="sxs-lookup"><span data-stu-id="c5dda-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5dda-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c5dda-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c5dda-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c5dda-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5dda-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c5dda-110">Prerequisites</span></span>

<span data-ttu-id="c5dda-111">若要設定 Azure AD 與 SD Elements 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c5dda-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="c5dda-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c5dda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5dda-113">已啟用 SD Elements 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c5dda-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5dda-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c5dda-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5dda-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c5dda-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5dda-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c5dda-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5dda-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c5dda-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5dda-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c5dda-118">Scenario description</span></span>
<span data-ttu-id="c5dda-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5dda-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c5dda-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5dda-121">從資源庫新增 SD Elements</span><span class="sxs-lookup"><span data-stu-id="c5dda-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="c5dda-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5dda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="c5dda-123">從資源庫新增 SD Elements</span><span class="sxs-lookup"><span data-stu-id="c5dda-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="c5dda-124">若要設定 SD Elements 與 Azure AD 的整合，您需要從資源庫將 SD Elements 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="c5dda-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5dda-125">**若要從資源庫新增 SD Elements，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c5dda-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5dda-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c5dda-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5dda-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5dda-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c5dda-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5dda-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c5dda-133">在搜尋方塊中，輸入 **SD Elements**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-133">In the search box, type **SD Elements**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="c5dda-135">在結果窗格中，選取 [SD Elements]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5dda-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5dda-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5dda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5dda-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 SD Elements 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5dda-139">若要讓單一登入運作，Azure AD 必須知道 SD Elements 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="c5dda-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="c5dda-140">換句話說，必須在 Azure AD 使用者和 SD Elements 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c5dda-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="c5dda-141">在 SD Elements 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c5dda-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5dda-142">若要使用 SD Elements 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c5dda-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5dda-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c5dda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5dda-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5dda-145">**[建立 SD Elements 測試使用者](#creating-a-sd-elements-test-user)** - 使 SD Elements 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="c5dda-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5dda-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5dda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c5dda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5dda-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5dda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5dda-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SD Elements 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="c5dda-150">**若要使用 SD Elements 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c5dda-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="c5dda-151">在 Azure 入口網站的 [SD Elements] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c5dda-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="c5dda-155">在 [SD Elements 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c5dda-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="c5dda-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5dda-157">a.</span></span> <span data-ttu-id="c5dda-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="c5dda-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="c5dda-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5dda-159">b.</span></span> <span data-ttu-id="c5dda-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="c5dda-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5dda-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-161">These values are not real.</span></span> <span data-ttu-id="c5dda-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c5dda-163">請連絡 [SD Elements 支援小組](mailto:support@sdelements.com) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="c5dda-164">SD Elements 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="c5dda-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c5dda-165">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="c5dda-165">Configure the following claims for this application.</span></span> <span data-ttu-id="c5dda-166">您可以從應用程式的 [使用者屬性] 索引標籤管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="c5dda-167">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="c5dda-167">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="c5dda-169">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c5dda-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="c5dda-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c5dda-170">Attribute Name</span></span> | <span data-ttu-id="c5dda-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="c5dda-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="c5dda-172">電子郵件</span><span class="sxs-lookup"><span data-stu-id="c5dda-172">email</span></span> |<span data-ttu-id="c5dda-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="c5dda-173">user.mail</span></span> |
    | <span data-ttu-id="c5dda-174">firstname</span><span class="sxs-lookup"><span data-stu-id="c5dda-174">firstname</span></span> |<span data-ttu-id="c5dda-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c5dda-175">user.givenname</span></span> |
    | <span data-ttu-id="c5dda-176">lastname</span><span class="sxs-lookup"><span data-stu-id="c5dda-176">lastname</span></span> |<span data-ttu-id="c5dda-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="c5dda-177">user.surname</span></span> |

    <span data-ttu-id="c5dda-178">a.</span><span class="sxs-lookup"><span data-stu-id="c5dda-178">a.</span></span> <span data-ttu-id="c5dda-179">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c5dda-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="c5dda-182">b.</span><span class="sxs-lookup"><span data-stu-id="c5dda-182">b.</span></span> <span data-ttu-id="c5dda-183">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="c5dda-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c5dda-184">c.</span><span class="sxs-lookup"><span data-stu-id="c5dda-184">c.</span></span> <span data-ttu-id="c5dda-185">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="c5dda-186">d.</span><span class="sxs-lookup"><span data-stu-id="c5dda-186">d.</span></span> <span data-ttu-id="c5dda-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="c5dda-188">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c5dda-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="c5dda-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5dda-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c5dda-192">在 [SD Elements 組態] 區段上，按一下 [設定 SD Elements] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c5dda-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c5dda-193">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="c5dda-195">若要啟用單一登入，請連絡您 [SD Elements 支援小組](mailto:support@sdelements.com) ，並提供下載的憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c5dda-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="c5dda-196">在不同的瀏覽器視窗中，以系統管理員身分登入您的 SD Elements 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c5dda-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="c5dda-197">在頂端的功能表中按一下 [系統]，然後按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="c5dda-199">在 [單一登入設定]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c5dda-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="c5dda-201">a.</span><span class="sxs-lookup"><span data-stu-id="c5dda-201">a.</span></span> <span data-ttu-id="c5dda-202">[SSO 類型] 請選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="c5dda-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5dda-203">b.</span></span> <span data-ttu-id="c5dda-204">在 [識別提供者實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="c5dda-205">c.</span><span class="sxs-lookup"><span data-stu-id="c5dda-205">c.</span></span> <span data-ttu-id="c5dda-206">在 [識別提供者單一登入服務] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="c5dda-207">d.</span><span class="sxs-lookup"><span data-stu-id="c5dda-207">d.</span></span> <span data-ttu-id="c5dda-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c5dda-209">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="c5dda-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5dda-210">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="c5dda-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5dda-211">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5dda-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5dda-212">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5dda-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5dda-213">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c5dda-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c5dda-215">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c5dda-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5dda-216">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c5dda-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5dda-218">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5dda-220">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5dda-222">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c5dda-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5dda-224">a.</span><span class="sxs-lookup"><span data-stu-id="c5dda-224">a.</span></span> <span data-ttu-id="c5dda-225">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5dda-226">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5dda-226">b.</span></span> <span data-ttu-id="c5dda-227">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5dda-228">c.</span><span class="sxs-lookup"><span data-stu-id="c5dda-228">c.</span></span> <span data-ttu-id="c5dda-229">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c5dda-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c5dda-230">d.</span><span class="sxs-lookup"><span data-stu-id="c5dda-230">d.</span></span> <span data-ttu-id="c5dda-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="c5dda-232">建立 SD Elements 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5dda-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="c5dda-233">本節目標是在 SD Elements 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c5dda-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="c5dda-234">在 SD Elements 的案例中，以手動工作建立 SD Elements 使用者。</span><span class="sxs-lookup"><span data-stu-id="c5dda-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="c5dda-235">**若要在 SD Elements 中建立 Britta Simon，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c5dda-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="c5dda-236">在 Wed 瀏覽器視窗中，以系統管理員身分登入您的 SD Elements 公司網站。</span><span class="sxs-lookup"><span data-stu-id="c5dda-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="c5dda-237">在頂端的功能表中，按一下 [使用者管理]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="c5dda-239">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-239">Click **Add New User**.</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="c5dda-241">在 [新增使用者] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c5dda-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="c5dda-243">a.</span><span class="sxs-lookup"><span data-stu-id="c5dda-243">a.</span></span> <span data-ttu-id="c5dda-244">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="c5dda-245">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5dda-245">b.</span></span> <span data-ttu-id="c5dda-246">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="c5dda-247">c.</span><span class="sxs-lookup"><span data-stu-id="c5dda-247">c.</span></span> <span data-ttu-id="c5dda-248">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="c5dda-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="c5dda-249">d.</span><span class="sxs-lookup"><span data-stu-id="c5dda-249">d.</span></span> <span data-ttu-id="c5dda-250">針對 [角色]，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="c5dda-251">e.</span><span class="sxs-lookup"><span data-stu-id="c5dda-251">e.</span></span> <span data-ttu-id="c5dda-252">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c5dda-253">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5dda-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c5dda-254">在本節中，您會將 SD Elements 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5dda-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![指派使用者][200] 

<span data-ttu-id="c5dda-256">**若要將 Britta Simon 指派到 SD Elements，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c5dda-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="c5dda-257">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c5dda-259">在應用程式清單中，選取 [SD Elements] 。</span><span class="sxs-lookup"><span data-stu-id="c5dda-259">In the applications list, select **SD Elements**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="c5dda-261">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-261">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c5dda-263">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5dda-263">Click **Add** button.</span></span> <span data-ttu-id="c5dda-264">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c5dda-266">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="c5dda-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5dda-267">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5dda-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5dda-268">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5dda-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5dda-269">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c5dda-269">Testing single sign-on</span></span>

<span data-ttu-id="c5dda-270">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="c5dda-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="c5dda-271">當您在存取面板中按一下 [SD Elements] 圖格時，應該會自動登入您的 SD Elements 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5dda-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5dda-272">其他資源</span><span class="sxs-lookup"><span data-stu-id="c5dda-272">Additional resources</span></span>

* [<span data-ttu-id="c5dda-273">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c5dda-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5dda-274">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c5dda-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

