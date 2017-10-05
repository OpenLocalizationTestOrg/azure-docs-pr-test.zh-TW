---
title: "教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Zscaler Private Access (ZPA) 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="c969a-103">教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合</span><span class="sxs-lookup"><span data-stu-id="c969a-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="c969a-104">在本教學課程中，您將了解如何整合 Zscaler Private Access (ZPA) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c969a-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c969a-105">Zscaler Private Access (ZPA) 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="c969a-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c969a-106">您可以在 Azure AD 中控制可存取 Zscaler Private Access (ZPA) 的人員</span><span class="sxs-lookup"><span data-stu-id="c969a-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="c969a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Zscaler Private Access (ZPA) (單一登入)</span><span class="sxs-lookup"><span data-stu-id="c969a-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c969a-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c969a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="c969a-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c969a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c969a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c969a-110">Prerequisites</span></span>

<span data-ttu-id="c969a-111">若要設定與 Zscaler Private Access (ZPA) 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c969a-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="c969a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c969a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c969a-113">啟用 Zscaler Private Access (ZPA) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c969a-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c969a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c969a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c969a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c969a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c969a-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="c969a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c969a-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c969a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c969a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c969a-118">Scenario description</span></span>
<span data-ttu-id="c969a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c969a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c969a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c969a-121">從資源庫加入 Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="c969a-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="c969a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c969a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="c969a-123">從資源庫加入 Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="c969a-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="c969a-124">若要設定 Zscaler Private Access (ZPA) 與 Azure AD 整合，您需要從資源庫將 Zscaler Private Access (ZPA) 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="c969a-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c969a-125">**若要從資源庫加入 Zscaler Private Access (ZPA)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c969a-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c969a-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c969a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c969a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c969a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c969a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c969a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c969a-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c969a-133">在搜尋方塊中，輸入 **Zscaler Private Access (ZPA)**。</span><span class="sxs-lookup"><span data-stu-id="c969a-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="c969a-135">在結果窗格中，選取 [Zscaler Private Access (ZPA)]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c969a-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c969a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c969a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c969a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Zscaler Private Access (ZPA) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c969a-139">若要讓單一登入能夠運作，Azure AD 必須知道 Zscaler Private Access (ZPA) 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="c969a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="c969a-140">換句話說，必須在 Azure AD 使用者與 Zscaler Private Access (ZPA) 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c969a-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="c969a-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值，指派為 Zscaler Private Access (ZPA) 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="c969a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="c969a-142">若要設定及測試與 Zscaler Private Access (ZPA) 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="c969a-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c969a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c969a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c969a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c969a-145">**[建立 Zscaler Private Access (ZPA) 測試使用者](#creating-a-zscaler-private-access-(zpa)-test-user)** - 使 Zscaler Private Access (ZPA) 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="c969a-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c969a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c969a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c969a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c969a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c969a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c969a-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Zscaler Private Access (ZPA) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="c969a-150">**若要設定與 Zscaler Private Access (ZPA) 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c969a-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="c969a-151">在 Azure 管理入口網站的 [Zscaler Private Access (ZPA)] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c969a-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c969a-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="c969a-155">在 [Zscaler Private Access (ZPA) 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c969a-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="c969a-157">a.</span><span class="sxs-lookup"><span data-stu-id="c969a-157">a.</span></span> <span data-ttu-id="c969a-158">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="c969a-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="c969a-159">b.</span><span class="sxs-lookup"><span data-stu-id="c969a-159">b.</span></span> <span data-ttu-id="c969a-160">在 [識別碼] 文字方塊中，輸入：`https://samlsp.private.zscaler.com/auth/metadata`。</span><span class="sxs-lookup"><span data-stu-id="c969a-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c969a-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c969a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="c969a-162">您必須使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c969a-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="c969a-163">在此建議您在 [識別碼] 中使用唯一的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="c969a-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="c969a-164">請連絡[Zscaler Private Access (ZPA) 支援小組 (Zscaler Private Access (ZPA) support team)](https://help.zscaler.com/zpa-submit-ticket) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="c969a-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="c969a-165">在 [SAML 簽署憑證] 區段中，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="c969a-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="c969a-167">在 [建立新憑證] 對話方塊中，按一下行事曆圖示並選取 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="c969a-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="c969a-168">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-168">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="c969a-170">在 [SAML 簽署憑證] 區段中，選取 [啟用新憑證] 並按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="c969a-172">在 [變換憑證] 快顯視窗上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c969a-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="c969a-174">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c969a-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="c969a-176">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zscaler Private Access (ZPA) 公司網站。</span><span class="sxs-lookup"><span data-stu-id="c969a-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="c969a-177">瀏覽至 [系統管理員]，然後按一下 [Idp 組態]。</span><span class="sxs-lookup"><span data-stu-id="c969a-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="c969a-179">在 [Idp 組態] 區段中，按一下 [新增 IDP 組態]。</span><span class="sxs-lookup"><span data-stu-id="c969a-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="c969a-181">在 [新增 IDP 組態] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c969a-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="c969a-183">a.</span><span class="sxs-lookup"><span data-stu-id="c969a-183">a.</span></span> <span data-ttu-id="c969a-184">按一下 [選取檔案]，然後上傳您下載的中繼資料檔。</span><span class="sxs-lookup"><span data-stu-id="c969a-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="c969a-185">b.</span><span class="sxs-lookup"><span data-stu-id="c969a-185">b.</span></span> <span data-ttu-id="c969a-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c969a-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c969a-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c969a-188">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c969a-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c969a-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c969a-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c969a-191">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c969a-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c969a-193">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="c969a-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c969a-195">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c969a-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c969a-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c969a-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c969a-199">a.</span><span class="sxs-lookup"><span data-stu-id="c969a-199">a.</span></span> <span data-ttu-id="c969a-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c969a-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c969a-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c969a-201">b.</span></span> <span data-ttu-id="c969a-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="c969a-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c969a-203">c.</span><span class="sxs-lookup"><span data-stu-id="c969a-203">c.</span></span> <span data-ttu-id="c969a-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c969a-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c969a-205">d.</span><span class="sxs-lookup"><span data-stu-id="c969a-205">d.</span></span> <span data-ttu-id="c969a-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c969a-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="c969a-207">建立 Zscaler Private Access (ZPA) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c969a-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="c969a-208">在本節中，您要在 Zscaler Private Access (ZPA) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c969a-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="c969a-209">請和 [Zscaler 私用存取 (ZPA) 支援小組 (Zscaler Private Access (ZPA) support team)](https://help.zscaler.com/zpa-submit-ticket) 一起，在 Zscaler Private Access (ZPA) 平台新增使用者。</span><span class="sxs-lookup"><span data-stu-id="c969a-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c969a-210">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c969a-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c969a-211">在本節中，您會把 Zscaler Private Access (ZPA) 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c969a-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![指派使用者][200] 

<span data-ttu-id="c969a-213">**若要將 Britta Simon 指派到 Zscaler Private Access (ZPA)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c969a-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="c969a-214">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c969a-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c969a-216">在應用程式清單中，選取 [Zscaler Private Access (ZPA)]。</span><span class="sxs-lookup"><span data-stu-id="c969a-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="c969a-218">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c969a-218">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c969a-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-220">Click **Add** button.</span></span> <span data-ttu-id="c969a-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c969a-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c969a-223">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="c969a-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c969a-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c969a-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c969a-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="c969a-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c969a-226">Testing single sign-on</span></span>

<span data-ttu-id="c969a-227">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="c969a-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c969a-228">當您在存取面板中按一下 [Zscaler Private Access (ZPA)] 磚時，應該會自動登入您的 Zscaler Private Access (ZPA) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c969a-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c969a-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="c969a-229">Additional resources</span></span>

* [<span data-ttu-id="c969a-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c969a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c969a-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c969a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png