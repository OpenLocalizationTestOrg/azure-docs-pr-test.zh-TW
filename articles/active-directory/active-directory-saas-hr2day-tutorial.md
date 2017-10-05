---
title: "教學課程：Azure Active Directory 與 HR2day by Merces 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 HR2day by Merces 之間的單一登入"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="53144-103">教學課程：Azure Active Directory 與 HR2day by Merces 整合</span><span class="sxs-lookup"><span data-stu-id="53144-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="53144-104">在本教學課程中，您將了解如何整合 HR2day by Merces 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="53144-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53144-105">HR2day by Merces 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="53144-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="53144-106">您可以在 Azure AD 中控制可存取 HR2day by Merces 的人員。</span><span class="sxs-lookup"><span data-stu-id="53144-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="53144-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 HR2day by Merces。</span><span class="sxs-lookup"><span data-stu-id="53144-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="53144-108">您可以在 Azure 入口網站集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="53144-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="53144-109">如需 SaaS 應用程式與 Azure AD 整合的詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="53144-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53144-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="53144-110">Prerequisites</span></span>

<span data-ttu-id="53144-111">若要設定 Azure AD 與 HR2day by Merces 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="53144-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="53144-112">Azure AD 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53144-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="53144-113">已啟用 HR2day by Merces 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53144-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="53144-114">我們不建議使用生產環境來測試本教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="53144-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="53144-115">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="53144-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="53144-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="53144-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="53144-117">如果您沒有 Azure AD，可取得 [Azure AD 一個月免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="53144-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="53144-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="53144-118">Scenario description</span></span>
<span data-ttu-id="53144-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53144-120">本大綱中說明的案例由二個主要建構元素組成：</span><span class="sxs-lookup"><span data-stu-id="53144-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="53144-121">從資源庫新增 HR2day by Merces。</span><span class="sxs-lookup"><span data-stu-id="53144-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="53144-122">設定並測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="53144-123">從資源庫新增 HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="53144-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="53144-124">若要設定將 HR2day by Merces 整合到 Azure AD 中，請從資源庫將 HR2day by Merces 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="53144-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="53144-125">**若要從資源庫新增 HR2day by Merces，請採取下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="53144-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="53144-126">在 [Azure 入口網站][](https://portal.azure.com) 的左方瀏覽窗格中，選取 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="53144-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53144-128">移至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="53144-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="53144-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="53144-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="53144-131">若要新增新的應用程式，請選取對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53144-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="53144-133">在搜尋方塊中，輸入 **HR2day by Merces**。</span><span class="sxs-lookup"><span data-stu-id="53144-133">In the search box, type **HR2day by Merces**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="53144-135">在結果窗格中，選取 [HR2day by Merces]，然後選取 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="53144-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="53144-137">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="53144-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="53144-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 HR2day by Merces 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="53144-139">若要讓單一登入運作，Azure AD 必須知道 HR2day by Merces 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="53144-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="53144-140">換句話說，必須在 Azure AD 使用者和 HR2day by Merce 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="53144-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="53144-141">在 HR2day by Merces 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="53144-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="53144-142">若要搭配 HR2day by Merces 來設定及測試 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="53144-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="53144-143">[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)：讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="53144-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="53144-144">[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)：使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53144-145">[建立 HR2day by Merces 測試使用者](#creating-an-hr2day-by-merces-test-user)：在 HR2day by Merces 中建立對應的 Britta Simon，以連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="53144-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="53144-146">[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)：讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53144-147">[測試單一登入](#testing-single-sign-on)：驗證設定是否能夠運作。</span><span class="sxs-lookup"><span data-stu-id="53144-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="53144-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="53144-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="53144-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 HR2day by Merces 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="53144-150">**若要使用 HR2day by Merces 來設定 Azure AD 單一登入，請採取下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="53144-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="53144-151">在 Azure 入口網站的 [HR2day by Merces] 應用程式整合頁面上，選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="53144-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="53144-153">若要啟用單一登入，請在 [單一登入] 對話方塊中，於 [模式] 選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="53144-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="53144-155">在 [HR2day by Merces 網域與 URL] 區段中，採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="53144-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="53144-157">a.</span><span class="sxs-lookup"><span data-stu-id="53144-157">a.</span></span> <span data-ttu-id="53144-158">在 [登入 URL] 方塊中，以下列模式輸入 URL：`https://<tenantname>.force.com/<instancename>`。</span><span class="sxs-lookup"><span data-stu-id="53144-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="53144-159">b.</span><span class="sxs-lookup"><span data-stu-id="53144-159">b.</span></span> <span data-ttu-id="53144-160">在 [識別碼] 方塊中，以下列模式輸入 URL：`https://hr2day.force.com/<companyname>`。</span><span class="sxs-lookup"><span data-stu-id="53144-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53144-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="53144-161">These values are not real.</span></span> <span data-ttu-id="53144-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="53144-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="53144-163">請連絡 [HR2day by Merces 用戶端支援小組](mailto:servicedesk@merces.nl)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="53144-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="53144-164">在 [SAML 簽署憑證] 區段上，選取 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="53144-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="53144-166">本節說明如何讓使用者透過他們的 Azure AD 帳戶，在 HR2day by Merces 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="53144-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="53144-167">使用者藉由以 SAML 通訊協定為基礎的同盟執行此動作。</span><span class="sxs-lookup"><span data-stu-id="53144-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="53144-168">HR2day by Merces 應用程式需要採用特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應新增到 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="53144-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="53144-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="53144-169">The following screenshot shows an example of this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="53144-171">您必須先連絡 [HR2day by Merces 用戶端支援小組](mailto:servicedesk@merces.nl)，向其要求取得您租用戶的唯一識別碼屬性值，才能設定 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="53144-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="53144-172">您需要這個值來完成下一節中的步驟：</span><span class="sxs-lookup"><span data-stu-id="53144-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="53144-173">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，設定 SAML 權杖屬性，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="53144-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="53144-174">然後採取下列步驟。</span><span class="sxs-lookup"><span data-stu-id="53144-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="53144-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="53144-175">Attribute name</span></span>    |   <span data-ttu-id="53144-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="53144-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="53144-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="53144-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="53144-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="53144-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="53144-179">a.</span><span class="sxs-lookup"><span data-stu-id="53144-179">a.</span></span> <span data-ttu-id="53144-180">若要開啟 [新增屬性] 對話方塊，請選取 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="53144-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="53144-183">b.</span><span class="sxs-lookup"><span data-stu-id="53144-183">b.</span></span> <span data-ttu-id="53144-184">在 [名稱] 方塊中，輸入 **ATTR_LOGINCLAIM**。</span><span class="sxs-lookup"><span data-stu-id="53144-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="53144-185">c.</span><span class="sxs-lookup"><span data-stu-id="53144-185">c.</span></span> <span data-ttu-id="53144-186">從 [值] 清單中，選取 [Join()]。</span><span class="sxs-lookup"><span data-stu-id="53144-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="53144-187">d.</span><span class="sxs-lookup"><span data-stu-id="53144-187">d.</span></span> <span data-ttu-id="53144-188">從 [String1] 清單中，選取 [user.mail]。</span><span class="sxs-lookup"><span data-stu-id="53144-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="53144-189">e.</span><span class="sxs-lookup"><span data-stu-id="53144-189">e.</span></span> <span data-ttu-id="53144-190">對於 **String2**，輸入 HR2day 小組所提供的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="53144-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="53144-191">f.</span><span class="sxs-lookup"><span data-stu-id="53144-191">f.</span></span> <span data-ttu-id="53144-192">在 [分隔符號] 方塊中，輸入 **@**。</span><span class="sxs-lookup"><span data-stu-id="53144-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="53144-193">g.</span><span class="sxs-lookup"><span data-stu-id="53144-193">g.</span></span> <span data-ttu-id="53144-194">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="53144-194">Select **Ok**.</span></span>

7. <span data-ttu-id="53144-195">選取 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53144-195">Select the **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="53144-197">在 [HR2day by Merces 設定] 區段中，選取 [設定 HR2day by Merces] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="53144-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="53144-198">從 [快速參考] 區段中複製 [登出 URL]、[SAML 實體識別碼]，以及 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="53144-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="53144-200">若要為您的應用程式設定 SSO，請連絡 [HR2day by Merces 用戶端支援小組](mailTo:servicedesk@merces.nl)。</span><span class="sxs-lookup"><span data-stu-id="53144-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="53144-201">將下載的**憑證 (Base64)** 檔案附加至您的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="53144-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="53144-202">同時提供 [登出 URL]、[SAML 實體識別碼]，以及 [SAML 單一登入服務 URL]，讓這些項目能針對 SSO 整合來進行設定。</span><span class="sxs-lookup"><span data-stu-id="53144-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="53144-203">請向 Merces 小組表明這項整合需要以下列模式設定「實體識別碼」：**https://hr2day.force.com/INSTANCENAME**。</span><span class="sxs-lookup"><span data-stu-id="53144-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="53144-204">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="53144-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="53144-205">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，選取 [單一登入] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="53144-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="53144-206">然後透過底部的 [設定] 區段來存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="53144-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="53144-207">您可以在 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)中閱讀更多有關內嵌文件功能的資訊。</span><span class="sxs-lookup"><span data-stu-id="53144-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="53144-208">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="53144-208">Create an Azure AD test user</span></span>
<span data-ttu-id="53144-209">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="53144-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="53144-211">**若要在 Azure AD 中建立測試使用者，請採取下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="53144-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="53144-212">在 [Azure 入口網站] 的左方瀏覽窗格中，選取 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="53144-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53144-214">若要顯示使用者清單，請移至 [使用者和群組]，然後選取 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="53144-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53144-216">若要開啟 [使用者] 對話方塊，請在對話方塊的頂端選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="53144-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53144-218">在 [使用者] 對話方塊中，採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="53144-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53144-220">a.</span><span class="sxs-lookup"><span data-stu-id="53144-220">a.</span></span> <span data-ttu-id="53144-221">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="53144-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53144-222">b.</span><span class="sxs-lookup"><span data-stu-id="53144-222">b.</span></span> <span data-ttu-id="53144-223">在 [使用者名稱] 方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="53144-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53144-224">c.</span><span class="sxs-lookup"><span data-stu-id="53144-224">c.</span></span> <span data-ttu-id="53144-225">選取 [顯示密碼]，並記下密碼。</span><span class="sxs-lookup"><span data-stu-id="53144-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="53144-226">d.</span><span class="sxs-lookup"><span data-stu-id="53144-226">d.</span></span> <span data-ttu-id="53144-227">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="53144-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="53144-228">建立 HR2day by Merces 測試使用者</span><span class="sxs-lookup"><span data-stu-id="53144-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="53144-229">本節的目標是要在 HR2day by Merces 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="53144-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="53144-230">若要新增 HR2day 帳戶中的使用者，請與 [HR2day by Merces 用戶端支援小組](mailto:servicedesk@merces.nl)合作。</span><span class="sxs-lookup"><span data-stu-id="53144-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="53144-231">如果您需要手動建立使用者，請連絡 [HR2day by Merces 用戶端支援小組](mailto:servicedesk@merces.nl)。</span><span class="sxs-lookup"><span data-stu-id="53144-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="53144-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="53144-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="53144-233">在本節中，您會將 HR2day by Merces 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53144-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![指派使用者][200] 

<span data-ttu-id="53144-235">**若要將 Britta Simon 指派給 HR2day by Merces，請採取下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="53144-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="53144-236">在 Azure 入口網站中，開啟應用程式檢視，移至目錄檢視，然後移至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="53144-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="53144-237">接著，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="53144-237">Next, select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="53144-239">在應用程式清單中，選取 [HR2day by Merces] 。</span><span class="sxs-lookup"><span data-stu-id="53144-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="53144-241">在左側功能表中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="53144-241">In the menu on the left, select **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="53144-243">選取 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53144-243">Select the **Add** button.</span></span> <span data-ttu-id="53144-244">然後，在 [新增指派] 對話方塊中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="53144-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="53144-246">在 [使用者和群組] 對話方塊的 [使用者] 清單中，選取 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="53144-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="53144-247">按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53144-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="53144-248">在 [新增指派] 對話方塊中，選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="53144-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="53144-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="53144-249">Test single sign-on</span></span>

<span data-ttu-id="53144-250">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="53144-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="53144-251">當您在「存取面板」中選取 [HR2day by Merces] 圖格時，會自動登入您的 HR2day by Merces 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53144-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53144-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="53144-252">Additional resources</span></span>

* [<span data-ttu-id="53144-253">有關如何整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="53144-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53144-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="53144-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

