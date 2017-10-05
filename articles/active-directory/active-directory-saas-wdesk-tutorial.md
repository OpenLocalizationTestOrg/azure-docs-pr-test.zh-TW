---
title: "教學課程：Azure Active Directory 與 Wdesk 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Wdesk 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="59b6c-103">教學課程：Azure Active Directory 與 Wdesk 整合</span><span class="sxs-lookup"><span data-stu-id="59b6c-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="59b6c-104">在本教學課程中，您會了解如何整合 Wdesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="59b6c-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59b6c-105">整合 Wdesk 與 Azure AD 有下列優點：</span><span class="sxs-lookup"><span data-stu-id="59b6c-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59b6c-106">您可以在 Azure AD 中控制可存取 Wdesk 的人員</span><span class="sxs-lookup"><span data-stu-id="59b6c-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="59b6c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Wdesk (單一登入)</span><span class="sxs-lookup"><span data-stu-id="59b6c-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59b6c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="59b6c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59b6c-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="59b6c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="59b6c-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="59b6c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59b6c-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="59b6c-111">Prerequisites</span></span>

<span data-ttu-id="59b6c-112">若要設定 Azure AD 與 Wdesk 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="59b6c-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="59b6c-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59b6c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="59b6c-114">已啟用 Wdesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59b6c-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59b6c-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="59b6c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59b6c-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="59b6c-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59b6c-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="59b6c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59b6c-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="59b6c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59b6c-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="59b6c-119">Scenario description</span></span>
<span data-ttu-id="59b6c-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59b6c-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="59b6c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59b6c-122">從資源庫新增 Wdesk</span><span class="sxs-lookup"><span data-stu-id="59b6c-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="59b6c-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59b6c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="59b6c-124">從資源庫新增 Wdesk</span><span class="sxs-lookup"><span data-stu-id="59b6c-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="59b6c-125">若要設定將 Wdesk 整合到 Azure AD 中，您需要從資源庫將 Wdesk 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="59b6c-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59b6c-126">**若要從資源庫新增 Wdesk，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59b6c-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59b6c-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="59b6c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59b6c-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59b6c-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="59b6c-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="59b6c-134">在搜尋方塊中，鍵入 **Wdesk**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-134">In the search box, type **Wdesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="59b6c-136">在結果窗格中，選取 [Wdesk]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6c-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59b6c-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59b6c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59b6c-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Wdesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59b6c-140">若要讓單一登入運作，Azure AD 必須知道 Wdesk 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="59b6c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="59b6c-141">換句話說，必須在 Azure AD 使用者和 Wdesk 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="59b6c-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="59b6c-142">在 Wdesk 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="59b6c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="59b6c-143">若要使用 Wdesk 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="59b6c-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59b6c-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="59b6c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59b6c-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59b6c-146">**[建立 Wdesk 測試使用者](#creating-a-wdesk-test-user)** - 使 Wdesk 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="59b6c-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59b6c-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59b6c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="59b6c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59b6c-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59b6c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59b6c-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Wdesk 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="59b6c-151">**若要使用 Wdesk 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59b6c-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="59b6c-152">在 Azure 入口網站的 [Wdesk] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="59b6c-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="59b6c-156">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Wdesk 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59b6c-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="59b6c-158">a.</span><span class="sxs-lookup"><span data-stu-id="59b6c-158">a.</span></span> <span data-ttu-id="59b6c-159">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="59b6c-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="59b6c-160">b.</span><span class="sxs-lookup"><span data-stu-id="59b6c-160">b.</span></span> <span data-ttu-id="59b6c-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="59b6c-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="59b6c-162">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="59b6c-163">如果您想要在 **SP** 起始模式中設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59b6c-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="59b6c-165">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="59b6c-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="59b6c-166">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="59b6c-166">These values are not real.</span></span> <span data-ttu-id="59b6c-167">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="59b6c-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="59b6c-168">當您設定 SSO 時，您可以從 WDesk 入口網站取得這些值。</span><span class="sxs-lookup"><span data-stu-id="59b6c-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="59b6c-169">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="59b6c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="59b6c-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="59b6c-173">在不同的網頁瀏覽器視窗中，以安全性系統管理員身分登入 Wdesk。</span><span class="sxs-lookup"><span data-stu-id="59b6c-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="59b6c-174">按一下左下方的 [管理員]，選擇 [帳戶管理員]：</span><span class="sxs-lookup"><span data-stu-id="59b6c-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="59b6c-176">在 Wdesk 管理員中，依序巡覽至 [安全性]、[SAML] > [SAML 設定]：</span><span class="sxs-lookup"><span data-stu-id="59b6c-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="59b6c-178">勾選 [一般設定] 下的 [Enable SAML Single Sign On] \(啟用 SAML 單一登入)：</span><span class="sxs-lookup"><span data-stu-id="59b6c-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="59b6c-180">在 [Service Provider Details] \(提供者詳細資料) 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59b6c-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="59b6c-182">a.</span><span class="sxs-lookup"><span data-stu-id="59b6c-182">a.</span></span> <span data-ttu-id="59b6c-183">將**登入 URL** 複製並貼入 Azure 入口網站的 [登入 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6c-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="59b6c-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6c-184">b.</span></span> <span data-ttu-id="59b6c-185">將**中繼資料 URL** 複製並貼入 Azure 入口網站的 [識別碼] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6c-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="59b6c-186">c.</span><span class="sxs-lookup"><span data-stu-id="59b6c-186">c.</span></span> <span data-ttu-id="59b6c-187">將**取用者 URL** 複製並貼入 Azure 入口網站的 [回覆 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6c-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="59b6c-188">d.</span><span class="sxs-lookup"><span data-stu-id="59b6c-188">d.</span></span> <span data-ttu-id="59b6c-189">按一下 Azure 入口網站的 [儲存]，以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="59b6c-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="59b6c-190">按一下 [Configure IdP Settings] \(設定 IdP 設定) 開啟 [Edit IdP Settings] \(編輯 IdP 設定) 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6c-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="59b6c-191">按一下 [選擇檔案] 找出從 Azure 入口網站儲存的 **Metadata.xml** 檔案，然後將它上傳。</span><span class="sxs-lookup"><span data-stu-id="59b6c-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="59b6c-193">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="59b6c-193">Click **Save changes**.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="59b6c-195">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="59b6c-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59b6c-196">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="59b6c-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59b6c-197">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59b6c-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59b6c-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59b6c-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="59b6c-199">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="59b6c-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="59b6c-201">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59b6c-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59b6c-202">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="59b6c-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59b6c-204">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59b6c-206">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59b6c-208">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59b6c-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59b6c-210">a.</span><span class="sxs-lookup"><span data-stu-id="59b6c-210">a.</span></span> <span data-ttu-id="59b6c-211">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59b6c-212">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6c-212">b.</span></span> <span data-ttu-id="59b6c-213">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59b6c-214">c.</span><span class="sxs-lookup"><span data-stu-id="59b6c-214">c.</span></span> <span data-ttu-id="59b6c-215">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="59b6c-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59b6c-216">d.</span><span class="sxs-lookup"><span data-stu-id="59b6c-216">d.</span></span> <span data-ttu-id="59b6c-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="59b6c-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="59b6c-218">建立 Wdesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59b6c-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="59b6c-219">為使 Azure AD 使用者登入 Wdesk，必須將他們佈建到 Wdesk。</span><span class="sxs-lookup"><span data-stu-id="59b6c-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="59b6c-220">在 Wdesk 中，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="59b6c-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="59b6c-221">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59b6c-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="59b6c-222">以安全性系統管理員身分登入 Wdesk。</span><span class="sxs-lookup"><span data-stu-id="59b6c-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="59b6c-223">巡覽至 [管理員] > [帳戶管理員]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="59b6c-225">按一下 [人員] 下的 [成員]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="59b6c-226">現在按一下 [新增成員] 開啟 [新增成員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6c-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="59b6c-228">在 [使用者] 文字方塊中，輸入使用者的使用者名稱，例如 **brittasimon@contoso.com**，然後按一下 [繼續] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="59b6c-230">如下所示輸入詳細資料：</span><span class="sxs-lookup"><span data-stu-id="59b6c-230">Enter the details as shown below:</span></span>
  
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="59b6c-232">a.</span><span class="sxs-lookup"><span data-stu-id="59b6c-232">a.</span></span> <span data-ttu-id="59b6c-233">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="59b6c-234">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6c-234">b.</span></span> <span data-ttu-id="59b6c-235">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="59b6c-236">c.</span><span class="sxs-lookup"><span data-stu-id="59b6c-236">c.</span></span> <span data-ttu-id="59b6c-237">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="59b6c-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="59b6c-238">按一下 [儲存成員] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-238">Click **Save Member** button.</span></span>  

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59b6c-240">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59b6c-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="59b6c-241">在本節中，您會將 Wdesk 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59b6c-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="59b6c-243">**若要將 Britta Simon 指派給 Wdesk，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59b6c-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="59b6c-244">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="59b6c-246">在應用程式清單中，選取 [Wdesk]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-246">In the applications list, select **Wdesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="59b6c-248">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-248">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="59b6c-250">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-250">Click **Add** button.</span></span> <span data-ttu-id="59b6c-251">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="59b6c-253">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="59b6c-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59b6c-254">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59b6c-255">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59b6c-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59b6c-256">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="59b6c-256">Testing single sign-on</span></span>

<span data-ttu-id="59b6c-257">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="59b6c-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59b6c-258">當您在存取面板中按一下 [Wdesk] 圖格時，應該會自動登入您的 Wdesk 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6c-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="59b6c-259">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="59b6c-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="59b6c-260">其他資源</span><span class="sxs-lookup"><span data-stu-id="59b6c-260">Additional resources</span></span>

* [<span data-ttu-id="59b6c-261">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="59b6c-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59b6c-262">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="59b6c-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

