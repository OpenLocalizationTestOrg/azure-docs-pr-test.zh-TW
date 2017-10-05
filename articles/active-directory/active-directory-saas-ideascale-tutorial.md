---
title: "教學課程：Azure Active Directory 與 IdeaScale 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 IdeaScale 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 88099e942319f16dd721da83e4e69b8fcb836c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="7d798-103">教學課程：Azure Active Directory 與 IdeaScale 整合</span><span class="sxs-lookup"><span data-stu-id="7d798-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="7d798-104">在本教學課程中，您將了解如何整合 IdeaScale 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7d798-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d798-105">IdeaScale 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7d798-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7d798-106">您可以在 Azure AD 中控制可存取 IdeaScale 的人員</span><span class="sxs-lookup"><span data-stu-id="7d798-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="7d798-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 IdeaScale (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7d798-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d798-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7d798-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7d798-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7d798-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d798-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d798-110">Prerequisites</span></span>

<span data-ttu-id="7d798-111">若要設定 Azure AD 與 IdeaScale 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7d798-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="7d798-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d798-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d798-113">已啟用 IdeaScale 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d798-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d798-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d798-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d798-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7d798-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d798-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d798-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d798-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7d798-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d798-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7d798-118">Scenario description</span></span>
<span data-ttu-id="7d798-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d798-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7d798-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d798-121">從資源庫新增 IdeaScale</span><span class="sxs-lookup"><span data-stu-id="7d798-121">Adding IdeaScale from the gallery</span></span>
2. <span data-ttu-id="7d798-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d798-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="7d798-123">從資源庫新增 IdeaScale</span><span class="sxs-lookup"><span data-stu-id="7d798-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="7d798-124">若要設定將 IdeaScale 整合到 Azure AD 中，您需要從資源庫將 IdeaScale 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7d798-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d798-125">**若要從資源庫新增 IdeaScale，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d798-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d798-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d798-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d798-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d798-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7d798-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d798-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7d798-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d798-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7d798-133">在搜尋方塊中，輸入 **IdeaScale**。</span><span class="sxs-lookup"><span data-stu-id="7d798-133">In the search box, type **IdeaScale**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="7d798-135">在結果窗格中，選取 [IdeaScale]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d798-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d798-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d798-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 IdeaScale 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d798-139">若要讓單一登入運作，Azure AD 必須知道 IdeaScale 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7d798-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="7d798-140">換句話說，必須建立 Azure AD 使用者和 IdeaScale 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7d798-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="7d798-141">在 IdeaScale 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7d798-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7d798-142">若要設定及測試與 IdeaScale 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="7d798-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d798-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7d798-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d798-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d798-145">**[建立 IdeaScale 測試使用者](#creating-an-ideascale-test-user)** - 在 IdeaScale 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="7d798-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d798-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d798-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7d798-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d798-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d798-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d798-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 IdeaScale 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="7d798-150">**若要使用 IdeaScale 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d798-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="7d798-151">在 Azure 入口網站的 [IdeaScale] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7d798-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7d798-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="7d798-155">在 [IdeaScale 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d798-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="7d798-157">a.</span><span class="sxs-lookup"><span data-stu-id="7d798-157">a.</span></span> <span data-ttu-id="7d798-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="7d798-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="7d798-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-159">b.</span></span> <span data-ttu-id="7d798-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="7d798-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="7d798-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7d798-161">These values are not real.</span></span> <span data-ttu-id="7d798-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7d798-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7d798-163">請連絡 [IdeaScale 用戶端支援小組](http://support.ideascale.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="7d798-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="7d798-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d798-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="7d798-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d798-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7d798-168">在 [IdeaScale 組態] 區段上，按一下 [設定 IdeaScale] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7d798-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7d798-169">從 [快速參考] 區段複製 [登出 URL] 和 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="7d798-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="7d798-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 IdeaScale 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7d798-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="7d798-172">移至 [社群設定] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="7d798-173">![社群設定](./media/active-directory-saas-ideascale-tutorial/ic790847.png "社群設定")</span><span class="sxs-lookup"><span data-stu-id="7d798-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="7d798-174">移至 [安全性] \> [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="7d798-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="7d798-175">![單一登入設定](./media/active-directory-saas-ideascale-tutorial/ic790848.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="7d798-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="7d798-176">在 [單一登入類型]，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="7d798-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7d798-177">![單一登入類型](./media/active-directory-saas-ideascale-tutorial/ic790849.png "單一登入類型")</span><span class="sxs-lookup"><span data-stu-id="7d798-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="7d798-178">在 [單一登入設定]  對話方塊上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d798-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="7d798-179">![單一登入設定](./media/active-directory-saas-ideascale-tutorial/ic790850.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="7d798-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="7d798-180">a.</span><span class="sxs-lookup"><span data-stu-id="7d798-180">a.</span></span> <span data-ttu-id="7d798-181">在 [SAML IdP 實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="7d798-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7d798-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-182">b.</span></span> <span data-ttu-id="7d798-183">複製您從 Azure 入口網站下載的中繼資料檔案內容，並將它貼到 [SAML IdP 中繼資料]  文字方塊。</span><span class="sxs-lookup"><span data-stu-id="7d798-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="7d798-184">c.</span><span class="sxs-lookup"><span data-stu-id="7d798-184">c.</span></span> <span data-ttu-id="7d798-185">在 [登出成功 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7d798-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7d798-186">d.</span><span class="sxs-lookup"><span data-stu-id="7d798-186">d.</span></span> <span data-ttu-id="7d798-187">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7d798-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7d798-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7d798-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7d798-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7d798-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d798-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d798-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d798-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d798-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7d798-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7d798-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d798-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d798-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d798-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d798-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7d798-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d798-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7d798-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d798-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d798-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d798-203">a.</span><span class="sxs-lookup"><span data-stu-id="7d798-203">a.</span></span> <span data-ttu-id="7d798-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7d798-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d798-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-205">b.</span></span> <span data-ttu-id="7d798-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7d798-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d798-207">c.</span><span class="sxs-lookup"><span data-stu-id="7d798-207">c.</span></span> <span data-ttu-id="7d798-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7d798-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7d798-209">d.</span><span class="sxs-lookup"><span data-stu-id="7d798-209">d.</span></span> <span data-ttu-id="7d798-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="7d798-211">建立 IdeaScale 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d798-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="7d798-212">若要讓 Azure AD 使用者可以登入 IdeaScale，必須將他們佈建到 IdeaScale。</span><span class="sxs-lookup"><span data-stu-id="7d798-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="7d798-213">在 IdeaScale 的情況下，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="7d798-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="7d798-214">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d798-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7d798-215">以系統管理員身分登入您的 **IdeaScale** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7d798-215">Log in to your **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="7d798-216">移至 [社群設定] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="7d798-217">![社群設定](./media/active-directory-saas-ideascale-tutorial/ic790847.png "社群設定")</span><span class="sxs-lookup"><span data-stu-id="7d798-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="7d798-218">移至 [基本設定] \> [成員管理]。</span><span class="sxs-lookup"><span data-stu-id="7d798-218">Go to **Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="7d798-219">按一下 [新增成員] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="7d798-220">![成員管理](./media/active-directory-saas-ideascale-tutorial/ic790852.png "成員管理")</span><span class="sxs-lookup"><span data-stu-id="7d798-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="7d798-221">在 [加入新成員] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d798-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="7d798-222">![加入新成員](./media/active-directory-saas-ideascale-tutorial/ic790853.png "加入新成員")</span><span class="sxs-lookup"><span data-stu-id="7d798-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="7d798-223">a.</span><span class="sxs-lookup"><span data-stu-id="7d798-223">a.</span></span> <span data-ttu-id="7d798-224">在 [電子郵件地址]  文字方塊輸入您想要佈建之 AAD 帳戶的有效電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7d798-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="7d798-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-225">b.</span></span> <span data-ttu-id="7d798-226">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="7d798-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="7d798-227">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，可在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="7d798-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="7d798-228">您可以使用任何其他的 IdeaScale 使用者帳戶建立工具或 IdeaScale 提供的 API，來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d798-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7d798-229">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d798-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7d798-230">在本節中，您會將 IdeaScale 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d798-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![指派使用者][200] 

<span data-ttu-id="7d798-232">**若要將 Britta Simon 指派給 IdeaScale，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d798-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="7d798-233">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d798-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7d798-235">在應用程式清單中，選取 [IdeaScale]。</span><span class="sxs-lookup"><span data-stu-id="7d798-235">In the applications list, select **IdeaScale**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="7d798-237">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d798-237">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7d798-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d798-239">Click **Add** button.</span></span> <span data-ttu-id="7d798-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d798-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7d798-242">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7d798-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7d798-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d798-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d798-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d798-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d798-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7d798-245">Testing single sign-on</span></span>


<span data-ttu-id="7d798-246">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="7d798-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7d798-247">當您在「存取面板」中按一下 [IdeaScale] 圖格時，應該會自動登入您的 IdeaScale 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d798-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d798-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d798-248">Additional resources</span></span>

* [<span data-ttu-id="7d798-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7d798-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d798-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7d798-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

