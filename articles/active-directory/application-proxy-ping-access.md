---
title: "標頭型驗證搭配 Azure AD 應用程式 Proxy 的 PingAccess | Microsoft Docs"
description: "使用 PingAccess 與應用程式 Proxy 來發行應用程式可支援標頭型驗證。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="b43d5-103">使用應用程式 Proxy 與 PingAccess 的單一登入之標頭式驗證</span><span class="sxs-lookup"><span data-stu-id="b43d5-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="b43d5-104">Azure Active Directory 應用程式 Proxy 和 PingAccess 通力合作，為 Azure Active Directory 客戶提供甚至更多應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="b43d5-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="b43d5-105">PingAccess 會展開[現有應用程式 Proxy 供應項目](active-directory-application-proxy-get-started.md)以包含單一登入存取使用標頭進行驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="b43d5-106">什麼是 Azure AD 的 PingAccess？</span><span class="sxs-lookup"><span data-stu-id="b43d5-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="b43d5-107">Azure Active Directory 的 PingAccess 是 PingAccess 供應項目，讓您可提供使用者存取權，以及單一登入使用驗證標頭的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="b43d5-108">應用程式 Proxy 會如同任何其他應用程式一樣處理這些應用程式，使用 Azure AD 驗證存取，然後透過連接器服務傳遞流量。</span><span class="sxs-lookup"><span data-stu-id="b43d5-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="b43d5-109">PingAccess 位於前方的應用程式，並將 Azure AD 的存取權杖轉譯為標頭，使應用程式以它可以讀取的格式收到驗證。</span><span class="sxs-lookup"><span data-stu-id="b43d5-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="b43d5-110">您的使用者在登入使用您公司的應用程式時，將不會注意到什麼不同。</span><span class="sxs-lookup"><span data-stu-id="b43d5-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="b43d5-111">這些還是可以在任何裝置上從任何地方運作。</span><span class="sxs-lookup"><span data-stu-id="b43d5-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="b43d5-112">由於應用程式 Proxy 連接器會將遠端流量導向至所有應用程式，而不論其驗證類型為何，因此它們也將繼續自動載入平衡。</span><span class="sxs-lookup"><span data-stu-id="b43d5-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="b43d5-113">如何取得存取權？</span><span class="sxs-lookup"><span data-stu-id="b43d5-113">How do I get access?</span></span>

<span data-ttu-id="b43d5-114">因為這種情況是透過 Azure Active Directory 和 PingAccess 之間的合作關係提供，您會需要這兩種服務的授權。</span><span class="sxs-lookup"><span data-stu-id="b43d5-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="b43d5-115">不過，Azure Active Directory Premium 訂用帳戶所包含的基本 PingAccess 授權最多可涵蓋 20 個應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="b43d5-116">如果您需要發佈 20 個以上的標頭應用程式，可以從 PingAccess 購買額外的授權。</span><span class="sxs-lookup"><span data-stu-id="b43d5-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="b43d5-117">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="b43d5-118">在 Azure 中發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="b43d5-118">Publish your application in Azure</span></span>

<span data-ttu-id="b43d5-119">本文是針對第一次要以此案例發佈應用程式的人所設計。</span><span class="sxs-lookup"><span data-stu-id="b43d5-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="b43d5-120">除了發佈的步驟之外，並逐步解說如何開始使用應用程式和 PingAccess。</span><span class="sxs-lookup"><span data-stu-id="b43d5-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="b43d5-121">如果您已經設定這兩項服務，但需要在發佈的步驟上重新整理，可以略過連接器安裝，並移至[使用應用程式 Proxy 將您的應用程式新增至 Azure AD](#add-your-app-to-Azure-AD-with-Application-Proxy)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="b43d5-122">因為此案例是 Azure AD 和 PingAccess 之間的合作關係，有些指示存在於 Ping 身分識別站台。</span><span class="sxs-lookup"><span data-stu-id="b43d5-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="b43d5-123">安裝應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="b43d5-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="b43d5-124">如果您已啟用應用程式 Proxy 並已安裝連接器，可以跳過本節並移至[使用應用程式 Proxy 將您的應用程式新增至 Azure AD](#add-your-app-to-azure-ad-with-application-proxy)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="b43d5-125">應用程式 Proxy 連接器是 Windows Server 服務，可將流量從您的遠端員工引導至發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="b43d5-126">如需細安裝指示，請參閱[在 Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="b43d5-127">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="b43d5-128">選取 **Azure Active Directory** > **應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="b43d5-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="b43d5-129">選取**下載連接器**以啟動應用程式 Proxy 連接器下載。</span><span class="sxs-lookup"><span data-stu-id="b43d5-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="b43d5-130">請遵循安裝指示。</span><span class="sxs-lookup"><span data-stu-id="b43d5-130">Follow the installation instructions.</span></span>

   ![啟用應用程式 Proxy 並下載連接器](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="b43d5-132">下載連接器應會自動啟用您目錄的應用程式 Proxy，但如果沒有，您可以選取**啟用應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="b43d5-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="b43d5-133">使用應用程式 Proxy 將您的應用程式新增至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="b43d5-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="b43d5-134">您需要在 Azure 入口網站中採取兩個動作。</span><span class="sxs-lookup"><span data-stu-id="b43d5-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="b43d5-135">首先，您必須使用應用程式 Proxy 發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="b43d5-136">然後，您需要收集一些關於應用程式的資訊，可供您在 PingAccess 步驟期間使用。</span><span class="sxs-lookup"><span data-stu-id="b43d5-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="b43d5-137">請遵循下列步驟來發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="b43d5-138">如需步驟 1-8 的更詳細逐步解說，請參閱[使用 Azure AD Application Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="b43d5-139">如果您在上一節中未登入，請以全域系統管理員的身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="b43d5-140">選取 [Azure Active Directory]  >  [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="b43d5-141">在刀鋒視窗頂端選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b43d5-142">選取**內部部署應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b43d5-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="b43d5-143">使用新應用程式的相關資訊填寫必要的欄位。</span><span class="sxs-lookup"><span data-stu-id="b43d5-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="b43d5-144">使用下列指導方針設定︰</span><span class="sxs-lookup"><span data-stu-id="b43d5-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="b43d5-145">**內部 URL**︰當您在公司網路上時，通常會提供此 URL 以帶您前往應用程式登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b43d5-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="b43d5-146">針對此情節，連接器需要將 PingAccess Proxy 視為應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="b43d5-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="b43d5-147">使用此格式︰`https://<host name of your PA server>:<port>`。</span><span class="sxs-lookup"><span data-stu-id="b43d5-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="b43d5-148">連接埠預設為 3000，但您可以在 PingAccess 中設定它。</span><span class="sxs-lookup"><span data-stu-id="b43d5-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="b43d5-149">**預先驗證方法**︰Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43d5-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="b43d5-150">**轉譯標頭中的 URL**：否</span><span class="sxs-lookup"><span data-stu-id="b43d5-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="b43d5-151">如果這是您的第一個應用程式，請在變更 PingAccess 設定時，使用連接埠 3000 啟動並返回以更新這項設定。</span><span class="sxs-lookup"><span data-stu-id="b43d5-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="b43d5-152">如果這是您的第二個或更後面的應用程式，則這必須符合您已在 PingAccess 中設定的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="b43d5-153">深入了解 [PingAccess 中的接聽程式](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="b43d5-154">選取刀鋒視窗底部的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="b43d5-155">已新增您的應用程式，快速入門功能表隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="b43d5-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="b43d5-156">在 [快速啟動] 功能表中，選取 [指派測試使用者]，並將至少一個使用者新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="b43d5-157">請確定此測試帳戶可存取內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="b43d5-158">選取**指派**以儲存測試使用者指派。</span><span class="sxs-lookup"><span data-stu-id="b43d5-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="b43d5-159">在 [應用程式管理] 刀鋒視窗中，選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="b43d5-160">從下拉式選單選擇 [標頭型登入]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="b43d5-161">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="b43d5-162">如果這是您第一次使用標頭式單一登入，您需要安裝 PingAccess。</span><span class="sxs-lookup"><span data-stu-id="b43d5-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="b43d5-163">若要確定您的 Azure 訂用帳戶會與 PingAccess 安裝自動產生關聯，請使用此單一登入頁面上的連結來下載 PingAccess。</span><span class="sxs-lookup"><span data-stu-id="b43d5-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="b43d5-164">您現在可以開啟下載網站，或稍後返回此頁面。</span><span class="sxs-lookup"><span data-stu-id="b43d5-164">You can open the download site now, or come back to this page later.</span></span> 

   ![選取標頭形式的登入](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="b43d5-166">關閉企業應用程式刀鋒視窗或捲動到最左邊，回到 Azure Active Directory 功能表。</span><span class="sxs-lookup"><span data-stu-id="b43d5-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="b43d5-167">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-167">Select **App registrations**.</span></span>

   ![選取 [應用程式註冊]](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="b43d5-169">選取您剛才新增的應用程式，然後**回覆 URL**。</span><span class="sxs-lookup"><span data-stu-id="b43d5-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![選取 [回覆 URL]](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="b43d5-171">請檢查外部 URL，看看您在步驟 5 中所指派的應用程式是否在回覆 URL 清單。</span><span class="sxs-lookup"><span data-stu-id="b43d5-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="b43d5-172">如果不存在，請立即新增。</span><span class="sxs-lookup"><span data-stu-id="b43d5-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="b43d5-173">在應用程式設定刀鋒視窗中，選取 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-173">On the app settings blade, select **Required permissions**.</span></span>

  ![選取 [必要權限]](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="b43d5-175">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b43d5-175">Select **Add**.</span></span> <span data-ttu-id="b43d5-176">針對 API，依序選擇 [Windows Azure Active Directory]、[選取]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="b43d5-177">針對權限，依序選擇 [讀取及寫入所有應用程式]、[登入及讀取使用者個人檔案]、[選取] 和 [完成]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![選取權限](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="b43d5-179">收集 PingAccess 步驟的資訊</span><span class="sxs-lookup"><span data-stu-id="b43d5-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="b43d5-180">在應用程式設定刀鋒視窗中，選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-180">On your app settings blade, select **Properties**.</span></span> 

  ![選取 [屬性]](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="b43d5-182">儲存 [應用程式識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="b43d5-182">Save the **Application Id** value.</span></span> <span data-ttu-id="b43d5-183">當您設定 PingAccess 時，這會用於用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="b43d5-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="b43d5-184">在應用程式設定刀鋒視窗中，選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-184">On the app settings blade, select **Keys**.</span></span>

  ![選取 [金鑰]](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="b43d5-186">輸入金鑰描述，然後從下拉式選單中選擇到期日來建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="b43d5-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="b43d5-187">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-187">Select **Save**.</span></span> <span data-ttu-id="b43d5-188">GUID 會出現在 [值] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="b43d5-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="b43d5-189">立即儲存此值，因為您關閉此視窗之後將無法再次看見它。</span><span class="sxs-lookup"><span data-stu-id="b43d5-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![建立新的金鑰](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="b43d5-191">關閉應用程式註冊刀鋒視窗或捲動到最左邊，回到 Azure Active Directory 功能表。</span><span class="sxs-lookup"><span data-stu-id="b43d5-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="b43d5-192">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="b43d5-192">Select **Properties**.</span></span>
8. <span data-ttu-id="b43d5-193">儲存**目錄識別碼** GUID。</span><span class="sxs-lookup"><span data-stu-id="b43d5-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="b43d5-194">選擇性 - 更新 GraphAPI 以傳送自訂欄位</span><span class="sxs-lookup"><span data-stu-id="b43d5-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="b43d5-195">如需 Azure AD 傳送以進行驗證的安全性權杖清單，請參閱 [Azure AD 權杖參考](./develop/active-directory-token-and-claims.md)。</span><span class="sxs-lookup"><span data-stu-id="b43d5-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="b43d5-196">如果您需要會傳送其他權杖的自訂宣告，請使用 GraphAPI 以將應用程式欄位 [acceptMappedClaims] 設為 [True]。</span><span class="sxs-lookup"><span data-stu-id="b43d5-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="b43d5-197">若要進行此設定，您可以使用 Azure AD Graph Explorer 或 MS Graph。</span><span class="sxs-lookup"><span data-stu-id="b43d5-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="b43d5-198">此範例使用 Graph Explorer：</span><span class="sxs-lookup"><span data-stu-id="b43d5-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="b43d5-199">下載 PingAccess 及設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b43d5-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="b43d5-200">現在您已完成所有的 Azure Active Directory 安裝步驟，可以移至設定 PingAccess。</span><span class="sxs-lookup"><span data-stu-id="b43d5-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="b43d5-201">這個案例的 PingAccess 部分詳細步驟會在 Ping 身分識別文件中[設定 Azure AD 的 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html) 繼續進行。</span><span class="sxs-lookup"><span data-stu-id="b43d5-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="b43d5-202">這些步驟會逐步引導您取得 PingAccess 帳戶 (如果您還沒有)、安裝 PingAccess 伺服器，以及使用您從 Azure 入口網站複製之目錄識別碼建立 Azure AD OIDC 提供者連線的程序。</span><span class="sxs-lookup"><span data-stu-id="b43d5-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="b43d5-203">然後，您可以使用應用程式識別碼和金鑰值在 PingAccess 上建立 Web 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b43d5-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="b43d5-204">之後，您可以設定身分識別對應，並建立虛擬主機、網站和應用程式。</span><span class="sxs-lookup"><span data-stu-id="b43d5-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="b43d5-205">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="b43d5-205">Test your app</span></span>

<span data-ttu-id="b43d5-206">當您完成所有這些步驟時，您的應用程式應該啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="b43d5-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="b43d5-207">若要測試它，請開啟瀏覽器並瀏覽至您在 Azure 中發佈應用程式時所建立的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="b43d5-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="b43d5-208">使用您指派給應用程式的測試帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="b43d5-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b43d5-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b43d5-209">Next steps</span></span>

- [<span data-ttu-id="b43d5-210">設定 Azure AD 的 PingAccess</span><span class="sxs-lookup"><span data-stu-id="b43d5-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="b43d5-211">Azure AD 應用程式 Proxy 如何提供單一登入？</span><span class="sxs-lookup"><span data-stu-id="b43d5-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="b43d5-212">疑難排解應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="b43d5-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
