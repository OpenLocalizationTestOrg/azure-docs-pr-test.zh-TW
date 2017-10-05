---
title: "教學課程：Azure Active Directory 與 Zendesk 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Zendesk 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="0b56e-103">教學課程：Azure Active Directory 與 Zendesk 整合</span><span class="sxs-lookup"><span data-stu-id="0b56e-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="0b56e-104">在本教學課程中，您會了解如何整合 Zendesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0b56e-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b56e-105">Zendesk 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0b56e-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b56e-106">您可以在 Azure AD 中控制可存取 Zendesk 的人員</span><span class="sxs-lookup"><span data-stu-id="0b56e-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="0b56e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Zendesk (單一登入)</span><span class="sxs-lookup"><span data-stu-id="0b56e-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b56e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="0b56e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b56e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0b56e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b56e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0b56e-110">Prerequisites</span></span>

<span data-ttu-id="0b56e-111">若要設定與 Zendesk 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0b56e-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="0b56e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0b56e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b56e-113">已啟用 Zendesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0b56e-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0b56e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0b56e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0b56e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0b56e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b56e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0b56e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b56e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0b56e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0b56e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0b56e-118">Scenario description</span></span>
<span data-ttu-id="0b56e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b56e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0b56e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b56e-121">從資源庫新增 Zendesk</span><span class="sxs-lookup"><span data-stu-id="0b56e-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="0b56e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b56e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="0b56e-123">從資源庫新增 Zendesk</span><span class="sxs-lookup"><span data-stu-id="0b56e-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="0b56e-124">若要設定將 Zendesk 整合到 Azure AD 中，您需要從資源庫將 Zendesk 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0b56e-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b56e-125">**若要從資源庫新增 Zendesk，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0b56e-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b56e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0b56e-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b56e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b56e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0b56e-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b56e-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0b56e-133">在搜尋方塊中，輸入 **Zendesk**。</span><span class="sxs-lookup"><span data-stu-id="0b56e-133">In the search box, type **Zendesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="0b56e-135">在結果窗格中，選取 [Zendesk]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b56e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b56e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b56e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Zendesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b56e-139">若要讓單一登入運作，Azure AD 必須知道 Zendesk 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0b56e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="0b56e-140">換句話說，必須建立 Azure AD 使用者和 Zendesk 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0b56e-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="0b56e-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值作為 Zendesk 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="0b56e-142">若要設定及測試與 Zendesk 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="0b56e-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b56e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0b56e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b56e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b56e-145">**[建立 Zendesk 測試使用者](#creating-a-zendesk-test-user)** - 讓 Zendesk 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="0b56e-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b56e-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b56e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0b56e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b56e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b56e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b56e-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Zendesk 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="0b56e-150">**若要設定與 Zendesk 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0b56e-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="0b56e-151">在 Azure 入口網站的 [Zendesk] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0b56e-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="0b56e-155">在 [Zendesk 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0b56e-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="0b56e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0b56e-157">a.</span></span> <span data-ttu-id="0b56e-158">在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0b56e-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="0b56e-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-159">b.</span></span> <span data-ttu-id="0b56e-160">在 [識別碼] 文字方塊中，使用下列模式將值輸入：`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0b56e-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b56e-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-161">These values are not real.</span></span> <span data-ttu-id="0b56e-162">使用實際的登入 URL 和識別碼 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="0b56e-163">請連絡 [Zendesk 支援小組](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="0b56e-164">Zendesk 需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="0b56e-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0b56e-165">沒有任何必要 SAML 屬性，但您可以選擇性依照下列步驟，從 [使用者屬性] 區段新增屬性：</span><span class="sxs-lookup"><span data-stu-id="0b56e-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="0b56e-167">a.</span><span class="sxs-lookup"><span data-stu-id="0b56e-167">a.</span></span> <span data-ttu-id="0b56e-168">按一下 [檢視和編輯所有其他屬性] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0b56e-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="0b56e-170">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-170">b.</span></span> <span data-ttu-id="0b56e-171">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0b56e-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0b56e-173">c.</span><span class="sxs-lookup"><span data-stu-id="0b56e-173">c.</span></span> <span data-ttu-id="0b56e-174">在 [名稱] 文字方塊中，輸入屬性名稱 (例如 **emailaddress**)。</span><span class="sxs-lookup"><span data-stu-id="0b56e-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="0b56e-175">d.</span><span class="sxs-lookup"><span data-stu-id="0b56e-175">d.</span></span> <span data-ttu-id="0b56e-176">從 [值] 清單中選取屬性值 (作為 **user.mail**)。</span><span class="sxs-lookup"><span data-stu-id="0b56e-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="0b56e-177">e.</span><span class="sxs-lookup"><span data-stu-id="0b56e-177">e.</span></span> <span data-ttu-id="0b56e-178">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="0b56e-179">您可以使用擴充屬性來新增預設不在 Azure AD 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="0b56e-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="0b56e-180">按一下[可以在 SAML 中設定的使用者屬性](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-)，以取得 **Zendesk**接受的完整 SAML 屬性清單。</span><span class="sxs-lookup"><span data-stu-id="0b56e-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="0b56e-181">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="0b56e-183">在 [Zendesk 組態] 區段上，按一下 [設定 Zendesk] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0b56e-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b56e-184">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="0b56e-186">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zendesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0b56e-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="0b56e-187">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="0b56e-187">Click **Admin**.</span></span>

9. <span data-ttu-id="0b56e-188">在左側導覽窗格中按一下 [設定]，然後按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="0b56e-189">在 [安全性]  頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0b56e-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="0b56e-190">![安全性](./media/active-directory-saas-zendesk-tutorial/ic773089.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="0b56e-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="0b56e-191">![單一登入](./media/active-directory-saas-zendesk-tutorial/ic773090.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="0b56e-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="0b56e-192">a.</span><span class="sxs-lookup"><span data-stu-id="0b56e-192">a.</span></span> <span data-ttu-id="0b56e-193">按一下 [系統管理員和代理程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0b56e-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="0b56e-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-194">b.</span></span> <span data-ttu-id="0b56e-195">選取 [單一登入 (SSO) 和 SAML]，然後選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="0b56e-196">c.</span><span class="sxs-lookup"><span data-stu-id="0b56e-196">c.</span></span> <span data-ttu-id="0b56e-197">在 [SAML SSO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="0b56e-198">d.</span><span class="sxs-lookup"><span data-stu-id="0b56e-198">d.</span></span> <span data-ttu-id="0b56e-199">在 [遠端登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="0b56e-200">e.</span><span class="sxs-lookup"><span data-stu-id="0b56e-200">e.</span></span> <span data-ttu-id="0b56e-201">在 [憑證指紋] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="0b56e-202">f.</span><span class="sxs-lookup"><span data-stu-id="0b56e-202">f.</span></span> <span data-ttu-id="0b56e-203">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0b56e-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b56e-204">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b56e-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b56e-205">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0b56e-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0b56e-207">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0b56e-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b56e-208">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0b56e-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b56e-210">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b56e-212">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0b56e-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b56e-214">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0b56e-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b56e-216">a.</span><span class="sxs-lookup"><span data-stu-id="0b56e-216">a.</span></span> <span data-ttu-id="0b56e-217">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0b56e-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b56e-218">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-218">b.</span></span> <span data-ttu-id="0b56e-219">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="0b56e-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b56e-220">c.</span><span class="sxs-lookup"><span data-stu-id="0b56e-220">c.</span></span> <span data-ttu-id="0b56e-221">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="0b56e-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b56e-222">d.</span><span class="sxs-lookup"><span data-stu-id="0b56e-222">d.</span></span> <span data-ttu-id="0b56e-223">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0b56e-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="0b56e-224">建立 Zendesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b56e-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="0b56e-225">若要讓 Azure AD 使用者登入 **Zendesk**，必須將他們佈建到 **Zendesk** 中。</span><span class="sxs-lookup"><span data-stu-id="0b56e-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="0b56e-226">視應用程式中指派的角色而定，這是預期的行為：</span><span class="sxs-lookup"><span data-stu-id="0b56e-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="0b56e-227">[使用者] 帳戶會在登入時自動佈建。</span><span class="sxs-lookup"><span data-stu-id="0b56e-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="0b56e-228">登入之前，必須在 **Zendesk** 中手動佈建 [代理程式] 和 [系統管理員] 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b56e-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="0b56e-229">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0b56e-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0b56e-230">登入您的 **Zendesk** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0b56e-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="0b56e-231">選取 [客戶清單]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0b56e-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="0b56e-232">選取 [使用者] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="0b56e-233">![新增使用者](./media/active-directory-saas-zendesk-tutorial/ic773632.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="0b56e-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="0b56e-234">輸入您要佈建之現有 Azure AD 帳戶的電子郵件地址，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0b56e-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="0b56e-235">![新增使用者](./media/active-directory-saas-zendesk-tutorial/ic773633.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="0b56e-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="0b56e-236">您可以使用任何其他的 Zendesk 使用者帳戶建立工具或 Zendesk 提供的 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b56e-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b56e-237">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b56e-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b56e-238">在本節中，您會將 Zendesk 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b56e-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="0b56e-240">**若要將 Britta Simon 指派到 Zendesk，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="0b56e-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="0b56e-241">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0b56e-243">在應用程式清單中，選取 [Zendesk]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-243">In the applications list, select **Zendesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="0b56e-245">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-245">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0b56e-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b56e-247">Click **Add** button.</span></span> <span data-ttu-id="0b56e-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0b56e-250">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0b56e-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b56e-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b56e-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b56e-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b56e-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b56e-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0b56e-253">Testing single sign-on</span></span>

<span data-ttu-id="0b56e-254">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0b56e-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b56e-255">當您在存取面板中按一下 Zendesk 圖格時，應該會自動登入您的 Zendesk 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b56e-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="0b56e-256">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="0b56e-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b56e-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="0b56e-257">Additional resources</span></span>

* [<span data-ttu-id="0b56e-258">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0b56e-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b56e-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0b56e-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
