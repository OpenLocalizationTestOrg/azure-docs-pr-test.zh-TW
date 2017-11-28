---
title: "教學課程：Azure Active Directory 與 ScaleX Enterprise 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ScaleX Enterprise 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: 0ebed0c2605862426384c0e219e52c9d626b6246
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="ff32a-103">教學課程：Azure Active Directory 與 ScaleX Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="ff32a-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="ff32a-104">在本教學課程中，您會了解如何將 ScaleX Enterprise 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="ff32a-104">In this tutorial, you learn how to integrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff32a-105">ScaleX Enterprise 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ff32a-105">Integrating ScaleX Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff32a-106">您可以在 Azure AD 中控制可存取 ScaleX Enterprise 的人員</span><span class="sxs-lookup"><span data-stu-id="ff32a-106">You can control in Azure AD who has access to ScaleX Enterprise</span></span>
- <span data-ttu-id="ff32a-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 ScaleX Enterprise (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ff32a-107">You can enable your users to automatically get signed-on to ScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff32a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ff32a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff32a-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ff32a-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="ff32a-110">什麼是搭配 [Azure Active Directory](active-directory-appssoaccess-whatis.md) 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ff32a-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff32a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff32a-111">Prerequisites</span></span>

<span data-ttu-id="ff32a-112">若要設定 Azure AD 與 ScaleX Enterprise 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ff32a-112">To configure Azure AD integration with ScaleX Enterprise, you need the following items:</span></span>

- <span data-ttu-id="ff32a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ff32a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ff32a-114">已啟用 ScaleX Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ff32a-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff32a-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ff32a-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff32a-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ff32a-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff32a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ff32a-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ff32a-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ff32a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff32a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="ff32a-119">Scenario description</span></span>
<span data-ttu-id="ff32a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff32a-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ff32a-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff32a-122">從資源庫新增 ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="ff32a-122">Adding ScaleX Enterprise from the gallery</span></span>
2. <span data-ttu-id="ff32a-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff32a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-the-gallery"></a><span data-ttu-id="ff32a-124">從資源庫新增 ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="ff32a-124">Adding ScaleX Enterprise from the gallery</span></span>
<span data-ttu-id="ff32a-125">若要設定將 ScaleX Enterprise 整合到 Azure AD 中，您需要從資源庫將 ScaleX Enterprise 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ff32a-125">To configure the integration of ScaleX Enterprise in to Azure AD, you need to add ScaleX Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff32a-126">**若要從資源庫新增 ScaleX Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff32a-126">**To add ScaleX Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff32a-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ff32a-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff32a-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff32a-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ff32a-132">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff32a-132">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ff32a-134">在搜尋方塊中，輸入 **ScaleX Enterprise**。</span><span class="sxs-lookup"><span data-stu-id="ff32a-134">In the search box, type **ScaleX Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="ff32a-136">在結果窗格中，選取 [ScaleX Enterprise]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-136">In the results panel, select **ScaleX Enterprise**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff32a-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff32a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff32a-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ScaleX Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ff32a-140">若要讓單一登入運作，Azure AD 必須知道 ScaleX Enterprise 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ff32a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in ScaleX Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="ff32a-141">換句話說，必須建立 Azure AD 使用者和 ScaleX Enterprise 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ff32a-141">In other words, a link relationship between an Azure AD user and the related user in ScaleX Enterprise needs to be established.</span></span>

<span data-ttu-id="ff32a-142">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 ScaleX Enterprise 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="ff32a-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="ff32a-143">若要設定及測試與 ScaleX Enterprise 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ff32a-143">To configure and test Azure AD single sign-on with ScaleX Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff32a-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ff32a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff32a-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff32a-146">**[建立 ScaleX Enterprise 測試使用者](#creating-a-scalex-enterprise-test-user)** - 使 ScaleX Enterprise 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="ff32a-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - to have a counterpart of Britta Simon in ScaleX Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff32a-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff32a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ff32a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff32a-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff32a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff32a-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ScaleX Enterprise 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="ff32a-151">**若要使用 ScaleX Enterprise 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff32a-151">**To configure Azure AD single sign-on with ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="ff32a-152">在 Azure 入口網站的 [ScaleX Enterprise] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-152">In the Azure portal, on the **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ff32a-154">在 [單一登入] 對話方塊上，選取 [以 SAML 為基礎的登入] 作為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-154">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="ff32a-156">如果您想要以 **IDP** 起始模式設定應用程式，請在 [ScaleX Enterprise 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ff32a-156">On the **ScaleX Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="ff32a-158">a.</span><span class="sxs-lookup"><span data-stu-id="ff32a-158">a.</span></span> <span data-ttu-id="ff32a-159">在 [識別碼] 文字方塊中，使用下列模式將值輸入：`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="ff32a-159">In the **Identifier** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="ff32a-160">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-160">b.</span></span> <span data-ttu-id="ff32a-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="ff32a-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="ff32a-162">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="ff32a-162">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="ff32a-164">在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="ff32a-164">In the **Sign-on URL** textbox, type the value using the following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ff32a-165">這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ff32a-165">These are not the real values.</span></span> <span data-ttu-id="ff32a-166">使用實際的識別碼、回覆 URL 或登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ff32a-166">Update these values with the actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="ff32a-167">請連絡 [ScaleX Enterprise 用戶端支援小組](http://info.rescale.com/contact_sales)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ff32a-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) to get these values.</span></span> 

5. <span data-ttu-id="ff32a-168">ScaleX 應用程式會預期要有特定格式的 SAML 判斷提示，需要您修改自訂屬性以對應到您的 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="ff32a-168">Your ScaleX application expects the SAML assertions in a specific format, which requires you to modify custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="ff32a-169">按一下 [檢視和編輯所有其他使用者屬性] 核取方塊，以開啟自訂屬性的設定。</span><span class="sxs-lookup"><span data-stu-id="ff32a-169">Click **View and edit all other user attributes** checkbox to open the custom attributes settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="ff32a-171">a.</span><span class="sxs-lookup"><span data-stu-id="ff32a-171">a.</span></span> <span data-ttu-id="ff32a-172">以滑鼠右鍵按一下屬性**名稱**，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-172">Right click the attribute **name** and click delete.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="ff32a-174">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-174">b.</span></span> <span data-ttu-id="ff32a-175">按一下 **emailaddress** 屬性以開啟 [編輯屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ff32a-175">Click **emailaddress** attribute to open the Edit Attribute window.</span></span> <span data-ttu-id="ff32a-176">將它的值從 **user.mail** 變更為 **user.userprincipalname**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-176">Change its value from **user.mail** to **user.userprincipalname** and click Ok.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="ff32a-178">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ff32a-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="ff32a-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff32a-180">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ff32a-182">在 [ScaleX Enterprise 組態] 區段上，按一下 [設定 ScaleX Enterprise] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ff32a-182">On the **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ff32a-183">從 [快速參考] 區段中複製 [SAML 實體 ID] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-183">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="ff32a-185">若要在 **ScaleX Enterprise** 端設定單一登入，請以系統管理員身分登入 ScaleX Enterprise 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ff32a-185">To configure single sign-on on **ScaleX Enterprise** side, login to the ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="ff32a-186">按一下右上角的功能表，然後選取 [Contoso 管理]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-186">Click the menu in the upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff32a-187">Contoso 只是一個範例。</span><span class="sxs-lookup"><span data-stu-id="ff32a-187">Contoso is just an example.</span></span> <span data-ttu-id="ff32a-188">這應該是您實際的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="ff32a-188">This should be your actual Company Name.</span></span> 

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="ff32a-190">從頂端功能表選取 [整合]，然後選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-190">Select **Integrations** from the top menu and select **Single Sign-On**.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="ff32a-192">完成表單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ff32a-192">Complete the form as follows:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="ff32a-194">a.</span><span class="sxs-lookup"><span data-stu-id="ff32a-194">a.</span></span> <span data-ttu-id="ff32a-195">選取 [建立可驗證 SSO 的任何使用者]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="ff32a-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-196">b.</span></span> <span data-ttu-id="ff32a-197">**服務提供者 SAML**︰將 ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent*** 值貼上</span><span class="sxs-lookup"><span data-stu-id="ff32a-197">**Service Provider saml**: Paste the value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="ff32a-198">c.</span><span class="sxs-lookup"><span data-stu-id="ff32a-198">c.</span></span> <span data-ttu-id="ff32a-199">**ACS 回應中的識別提供者電子郵件欄位的名稱**︰將 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` 值貼上</span><span class="sxs-lookup"><span data-stu-id="ff32a-199">**Name of Identity Provider email field in ACS response**: Paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="ff32a-200">d.</span><span class="sxs-lookup"><span data-stu-id="ff32a-200">d.</span></span> <span data-ttu-id="ff32a-201">**識別提供者的 EntityDescriptor 實體識別碼︰**將您從 Azure 入口網站複製的 **SAML 實體識別碼**值貼上。</span><span class="sxs-lookup"><span data-stu-id="ff32a-201">**Identity Provider EntityDescriptor Entity ID:** Paste the **SAML Entity ID** value copied from the Azure portal.</span></span>

    <span data-ttu-id="ff32a-202">e.</span><span class="sxs-lookup"><span data-stu-id="ff32a-202">e.</span></span> <span data-ttu-id="ff32a-203">**識別提供者 SingleSignOnService URL：**從 Azure 入口網站將 **SAML 單一登入服務 URL** 貼上。</span><span class="sxs-lookup"><span data-stu-id="ff32a-203">**Identity Provider SingleSignOnService URL:** Paste the **SAML Single Sign-On Service URL** from the Azure portal.</span></span>

    <span data-ttu-id="ff32a-204">f.</span><span class="sxs-lookup"><span data-stu-id="ff32a-204">f.</span></span> <span data-ttu-id="ff32a-205">**識別提供者公開 X509 憑證︰**在記事本中，將您從 Azure下載的 X509 憑證開啟，並在此方塊中將內容貼上。</span><span class="sxs-lookup"><span data-stu-id="ff32a-205">**Identity Provider public X509 certificate:** Open the X509 certificate downloaded from the Azure in notepad and paste the contents in this box.</span></span> <span data-ttu-id="ff32a-206">確定憑證內容中沒有任何分行符號。</span><span class="sxs-lookup"><span data-stu-id="ff32a-206">Ensure there are no line breaks in the middle of the certificate contents.</span></span>
    
    <span data-ttu-id="ff32a-207">g.</span><span class="sxs-lookup"><span data-stu-id="ff32a-207">g.</span></span> <span data-ttu-id="ff32a-208">請勾選下列核取方塊︰[已啟用]、[加密 NameID] 和 [簽署 AuthnRequests]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-208">Check the following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="ff32a-209">h.</span><span class="sxs-lookup"><span data-stu-id="ff32a-209">h.</span></span> <span data-ttu-id="ff32a-210">按一下 [更新 SSO 設定] 將設定儲存。</span><span class="sxs-lookup"><span data-stu-id="ff32a-210">Click **Update SSO Settings** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="ff32a-211">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ff32a-211">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ff32a-212">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ff32a-212">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ff32a-213">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff32a-213">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff32a-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff32a-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff32a-215">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ff32a-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ff32a-217">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff32a-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff32a-218">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ff32a-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff32a-220">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="ff32a-220">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff32a-222">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ff32a-222">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff32a-224">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ff32a-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff32a-226">a.</span><span class="sxs-lookup"><span data-stu-id="ff32a-226">a.</span></span> <span data-ttu-id="ff32a-227">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ff32a-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff32a-228">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-228">b.</span></span> <span data-ttu-id="ff32a-229">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ff32a-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff32a-230">c.</span><span class="sxs-lookup"><span data-stu-id="ff32a-230">c.</span></span> <span data-ttu-id="ff32a-231">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ff32a-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff32a-232">d.</span><span class="sxs-lookup"><span data-stu-id="ff32a-232">d.</span></span> <span data-ttu-id="ff32a-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ff32a-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="ff32a-234">建立 ScaleX Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff32a-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="ff32a-235">若要讓 Azure AD 使用者能夠登入 ScaleX Enterprise，必須將他們佈建到 ScaleX Enterprise 中。</span><span class="sxs-lookup"><span data-stu-id="ff32a-235">To enable Azure AD users to log in to ScaleX Enterprise, they must be provisioned in to ScaleX Enterprise.</span></span> <span data-ttu-id="ff32a-236">在 ScaleX Enterprise 的案例中，佈建是自動的工作，不需要任何手動步驟。</span><span class="sxs-lookup"><span data-stu-id="ff32a-236">In the case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="ff32a-237">系統會將任何可成功驗證 SSO 認證的使用者自動佈建在 ScaleX 端。</span><span class="sxs-lookup"><span data-stu-id="ff32a-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on the ScaleX side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff32a-238">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff32a-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff32a-239">在本節中，您會將 ScaleX Enterprise 的存取權授與 Britta Simon，讓使用者能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff32a-239">In this section, you enable Britta Simon to use Azure single sign-on by granting user access to ScaleX Enterprise.</span></span>

![指派使用者][200] 

<span data-ttu-id="ff32a-241">**若要將 Britta Simon 指派給 ScaleX Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff32a-241">**To assign Britta Simon to ScaleX Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="ff32a-242">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ff32a-244">在應用程式清單中，選取 [ScaleX Enterprise]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-244">In the applications list, select **ScaleX Enterprise**.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="ff32a-246">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-246">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ff32a-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff32a-248">Click **Add** button.</span></span> <span data-ttu-id="ff32a-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ff32a-251">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ff32a-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff32a-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff32a-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff32a-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff32a-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff32a-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ff32a-254">Testing single sign-on</span></span>

<span data-ttu-id="ff32a-255">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ff32a-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff32a-256">在存取面板中按一下 [ScaleX Enterprise] 圖格，系統會將您自動登入 ScaleX Enterprise 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff32a-256">Click the ScaleX Enterprise tile in the Access Panel, you will get automatically signed-on to your ScaleX Enterprise application.</span></span> <span data-ttu-id="ff32a-257">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="ff32a-257">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ff32a-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="ff32a-258">Additional resources</span></span>

* [<span data-ttu-id="ff32a-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ff32a-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff32a-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ff32a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

