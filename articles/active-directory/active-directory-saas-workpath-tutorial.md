---
title: "教學課程：Azure Active Directory 與 Workpath 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workpath 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f4efa56d2c0374a977c1e46dad64b596cc9c3ea8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="17334-103">教學課程：Azure Active Directory 與 Workpath 整合</span><span class="sxs-lookup"><span data-stu-id="17334-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="17334-104">在本教學課程中，您將了解如何整合 Workpath 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="17334-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17334-105">整合 Workpath 與 Azure AD 有下列優點：</span><span class="sxs-lookup"><span data-stu-id="17334-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17334-106">您可以在 Azure AD 中控制可存取 Workpath 的人員</span><span class="sxs-lookup"><span data-stu-id="17334-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="17334-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Workpath (單一登入)</span><span class="sxs-lookup"><span data-stu-id="17334-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17334-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="17334-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17334-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="17334-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17334-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="17334-110">Prerequisites</span></span>

<span data-ttu-id="17334-111">若要設定 Azure AD 與 Workpath 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="17334-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="17334-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="17334-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17334-113">已啟用 Workpath 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="17334-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17334-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="17334-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17334-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="17334-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17334-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="17334-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17334-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="17334-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17334-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="17334-118">Scenario description</span></span>
<span data-ttu-id="17334-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17334-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="17334-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17334-121">從資源庫新增 Workpath</span><span class="sxs-lookup"><span data-stu-id="17334-121">Adding Workpath from the gallery</span></span>
2. <span data-ttu-id="17334-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="17334-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="17334-123">從資源庫新增 Workpath</span><span class="sxs-lookup"><span data-stu-id="17334-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="17334-124">若要設定將 Workpath 整合到 Azure AD 中，您需要從資源庫將 Workpath 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="17334-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17334-125">**若要從資源庫新增 Workpath，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17334-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17334-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="17334-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17334-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="17334-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17334-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="17334-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="17334-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17334-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="17334-133">在搜尋方塊中，鍵入 **Workpath**。</span><span class="sxs-lookup"><span data-stu-id="17334-133">In the search box, type **Workpath**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_search.png)

5. <span data-ttu-id="17334-135">在結果窗格中，選取 [Workpath]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="17334-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17334-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="17334-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17334-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Workpath 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17334-139">若要讓單一登入運作，Azure AD 必須知道 Workpath 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="17334-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="17334-140">換句話說，必須在 Azure AD 使用者和 Workpath 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="17334-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="17334-141">在 Workpath 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="17334-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17334-142">若要使用 Workpath 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="17334-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17334-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="17334-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17334-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17334-145">**[建立 Workpath 測試使用者](#creating-a-workpath-test-user)** - 使 Workpath 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="17334-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17334-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17334-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="17334-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17334-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="17334-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17334-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Workpath 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="17334-150">**若要使用 Workpath 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17334-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="17334-151">在 Azure 入口網站的 [Workpath] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="17334-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="17334-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_samlbase.png)

3. <span data-ttu-id="17334-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Workpath 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="17334-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="17334-157">a.</span><span class="sxs-lookup"><span data-stu-id="17334-157">a.</span></span> <span data-ttu-id="17334-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="17334-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="17334-159">b.</span><span class="sxs-lookup"><span data-stu-id="17334-159">b.</span></span> <span data-ttu-id="17334-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="17334-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

4. <span data-ttu-id="17334-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="17334-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="17334-162">如果您想要在 **SP** 起始模式中設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="17334-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="17334-164">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="17334-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17334-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="17334-165">These values are not real.</span></span> <span data-ttu-id="17334-166">使用實際的「單一登入 URL」、「識別碼」及「回覆 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="17334-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="17334-167">請連絡 [Workpath 支援小組](https://help.workpath.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="17334-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

5. <span data-ttu-id="17334-168">Workpath 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="17334-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="17334-169">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="17334-169">Configure the following claims for this application.</span></span> <span data-ttu-id="17334-170">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="17334-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="17334-171">以下螢幕擷取畫面顯示此設定的範例。</span><span class="sxs-lookup"><span data-stu-id="17334-171">The following screenshot shows an example for this configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_attributes.png)
    
6. <span data-ttu-id="17334-173">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="17334-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="17334-174">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="17334-174">Attribute Name</span></span> | <span data-ttu-id="17334-175">屬性值</span><span class="sxs-lookup"><span data-stu-id="17334-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="17334-176">first_name</span><span class="sxs-lookup"><span data-stu-id="17334-176">first_name</span></span> | <span data-ttu-id="17334-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="17334-177">user.givenname</span></span> |
    | <span data-ttu-id="17334-178">last_name</span><span class="sxs-lookup"><span data-stu-id="17334-178">last_name</span></span> | <span data-ttu-id="17334-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="17334-179">user.surname</span></span> |
    
    <span data-ttu-id="17334-180">a.</span><span class="sxs-lookup"><span data-stu-id="17334-180">a.</span></span> <span data-ttu-id="17334-181">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="17334-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="17334-183">b.</span><span class="sxs-lookup"><span data-stu-id="17334-183">b.</span></span> <span data-ttu-id="17334-184">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="17334-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="17334-186">c.</span><span class="sxs-lookup"><span data-stu-id="17334-186">c.</span></span> <span data-ttu-id="17334-187">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="17334-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="17334-188">d.</span><span class="sxs-lookup"><span data-stu-id="17334-188">d.</span></span> <span data-ttu-id="17334-189">[命名空間] 文字方塊保持空白。</span><span class="sxs-lookup"><span data-stu-id="17334-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="17334-190">e.</span><span class="sxs-lookup"><span data-stu-id="17334-190">e.</span></span> <span data-ttu-id="17334-191">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="17334-191">Click **Ok**.</span></span>
    

7. <span data-ttu-id="17334-192">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="17334-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_certificate.png) 

8. <span data-ttu-id="17334-194">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="17334-194">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="17334-196">在 [Workpath Configuration] \(Workpath 設定) 區段上，按一下 [Configure Workpath] \(設定 Workpath) 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="17334-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17334-197">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="17334-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_configure.png) 

10. <span data-ttu-id="17334-199">若要在 **Workpath** 這一端設定單一登入，您需要將所下載的**中繼資料 XML**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送給 [Workpath 支援小組](https://help.workpath.com)。</span><span class="sxs-lookup"><span data-stu-id="17334-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="17334-200">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="17334-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17334-201">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="17334-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17334-202">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17334-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17334-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="17334-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="17334-204">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="17334-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="17334-206">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17334-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17334-207">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="17334-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17334-209">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="17334-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17334-211">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="17334-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17334-213">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="17334-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17334-215">a.</span><span class="sxs-lookup"><span data-stu-id="17334-215">a.</span></span> <span data-ttu-id="17334-216">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="17334-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17334-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="17334-217">b.</span></span> <span data-ttu-id="17334-218">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="17334-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17334-219">c.</span><span class="sxs-lookup"><span data-stu-id="17334-219">c.</span></span> <span data-ttu-id="17334-220">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="17334-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17334-221">d.</span><span class="sxs-lookup"><span data-stu-id="17334-221">d.</span></span> <span data-ttu-id="17334-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="17334-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="17334-223">建立 Workpath 測試使用者</span><span class="sxs-lookup"><span data-stu-id="17334-223">Creating a Workpath test user</span></span>

<span data-ttu-id="17334-224">Workpath 支援 Just-In-Time 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="17334-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="17334-225">驗證之後，會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="17334-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17334-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="17334-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17334-227">在本節中，您會將 Workpath 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="17334-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![指派使用者][200] 

<span data-ttu-id="17334-229">**若要將 Britta Simon 指派給 Workpath，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17334-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="17334-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="17334-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="17334-232">在應用程式清單中，選取 [Workpath]。</span><span class="sxs-lookup"><span data-stu-id="17334-232">In the applications list, select **Workpath**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workpath-tutorial/tutorial_workpath_app.png) 

3. <span data-ttu-id="17334-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="17334-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="17334-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17334-236">Click **Add** button.</span></span> <span data-ttu-id="17334-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="17334-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="17334-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="17334-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17334-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17334-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17334-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17334-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17334-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="17334-242">Testing single sign-on</span></span>

<span data-ttu-id="17334-243">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="17334-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="17334-244">當您在存取面板中按一下 [Workpath] 圖格時，應該會自動登入您的 Workpath 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17334-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="17334-245">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="17334-245">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17334-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="17334-246">Additional resources</span></span>

* [<span data-ttu-id="17334-247">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="17334-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17334-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="17334-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workpath-tutorial/tutorial_general_203.png

