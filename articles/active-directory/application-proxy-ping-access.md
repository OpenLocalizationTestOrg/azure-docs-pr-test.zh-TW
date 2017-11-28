---
title: "aaaHeader 式驗證搭配 PingAccess 的 Azure AD Application Proxy |Microsoft 文件"
description: "發行應用程式與 PingAccess 和應用程式 Proxy toosupport 標頭為基礎的驗證。"
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
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="48b36-103">使用應用程式 Proxy 與 PingAccess 的單一登入之標頭式驗證</span><span class="sxs-lookup"><span data-stu-id="48b36-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="48b36-104">Azure Active Directory 應用程式 Proxy 及 PingAccess 通力合作，同時存取 tooeven tooprovide Azure Active Directory 客戶更多應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="48b36-105">PingAccess 展開 hello[現有應用程式 Proxy 的供應項目](active-directory-application-proxy-get-started.md)tooinclude 單一登入存取 tooapplications 使用驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="48b36-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="48b36-106">什麼是 Azure AD 的 PingAccess？</span><span class="sxs-lookup"><span data-stu-id="48b36-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="48b36-107">Azure Active directory PingAccess 是 PingAccess，可讓您 toogive 使用者存取權和單一登入 tooapplications 使用驗證標頭的供應項目。</span><span class="sxs-lookup"><span data-stu-id="48b36-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="48b36-108">應用程式 Proxy 會將如同任何其他的這些應用程式，使用 Azure AD tooauthenticate 存取權，然後讓流量通過 hello 連接器服務。</span><span class="sxs-lookup"><span data-stu-id="48b36-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="48b36-109">PingAccess 位於前面 hello 應用程式，並將 hello 來自 Azure AD 存取權杖轉譯成標頭，以便 hello 應用程式收到 hello 驗證 hello 它可以讀取的格式。</span><span class="sxs-lookup"><span data-stu-id="48b36-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="48b36-110">登入時 toouse 您公司的應用程式時，您的使用者將不會採取任何不同發現。</span><span class="sxs-lookup"><span data-stu-id="48b36-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="48b36-111">這些還是可以在任何裝置上從任何地方運作。</span><span class="sxs-lookup"><span data-stu-id="48b36-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="48b36-112">Hello 應用程式 Proxy 連接器直接遠端流量 tooall 應用程式，不論其驗證類型，因為它們將會自動，以及繼續 tooload 平衡。</span><span class="sxs-lookup"><span data-stu-id="48b36-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="48b36-113">如何取得存取權？</span><span class="sxs-lookup"><span data-stu-id="48b36-113">How do I get access?</span></span>

<span data-ttu-id="48b36-114">因為這種情況是透過 Azure Active Directory 和 PingAccess 之間的合作關係提供，您會需要這兩種服務的授權。</span><span class="sxs-lookup"><span data-stu-id="48b36-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="48b36-115">不過，Azure Active Directory Premium 訂閱包含遮蓋 too20 應用程式的基本 PingAccess 授權。</span><span class="sxs-lookup"><span data-stu-id="48b36-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="48b36-116">如果您需要 toopublish 20 個以上的標頭應用程式，您可以從 PingAccess 購買額外的授權。</span><span class="sxs-lookup"><span data-stu-id="48b36-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="48b36-117">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="48b36-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="48b36-118">在 Azure 中發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="48b36-118">Publish your application in Azure</span></span>

<span data-ttu-id="48b36-119">這篇文章僅供人發行應用程式，但此案例中的 hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="48b36-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="48b36-120">它引導 tooget 啟動方式使用應用程式和 PingAccess，此外 toohello 發行步驟。</span><span class="sxs-lookup"><span data-stu-id="48b36-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="48b36-121">如果您已經設定這兩項服務，但是想發行步驟 hello 的重新整理程式，您可以略過 hello 連接器安裝，移太[加入您的應用程式 tooAzure 應用程式 Proxy 與 AD](#add-your-app-to-Azure-AD-with-Application-Proxy)。</span><span class="sxs-lookup"><span data-stu-id="48b36-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="48b36-122">由於此案例是 Azure AD 之間的合作關係，而且 PingAccess，hello 指示的某些存在 hello Ping 識別站台上。</span><span class="sxs-lookup"><span data-stu-id="48b36-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="48b36-123">安裝應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="48b36-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="48b36-124">如果您已經有應用程式 Proxy 已啟用，並已安裝的連接器，您可以略過本節並移過[加入您的應用程式 tooAzure 應用程式 Proxy 與 AD](#add-your-app-to-azure-ad-with-application-proxy)。</span><span class="sxs-lookup"><span data-stu-id="48b36-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="48b36-125">hello 應用程式 Proxy 連接器是 Windows Server 會將從遠端員工 tooyour hello 流量導向的服務發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="48b36-126">如需詳細的安裝指示，請參閱[hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="48b36-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="48b36-127">登入 toohello [Azure 入口網站](https://portal.azure.com)身為全域管理員。</span><span class="sxs-lookup"><span data-stu-id="48b36-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="48b36-128">選取 **Azure Active Directory** > **應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="48b36-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="48b36-129">選取**下載連接器**toostart hello 應用程式 Proxy 連接器的下載。</span><span class="sxs-lookup"><span data-stu-id="48b36-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="48b36-130">請遵循 hello 安裝指示。</span><span class="sxs-lookup"><span data-stu-id="48b36-130">Follow hello installation instructions.</span></span>

   ![啟用應用程式 Proxy 並下載 hello 連接器](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="48b36-132">下載 hello connector 應該會自動會啟用您的目錄，但如果不是您可以選取的應用程式 Proxy**啟用應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="48b36-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="48b36-133">加入您的應用程式 tooAzure AD 應用程式 proxy</span><span class="sxs-lookup"><span data-stu-id="48b36-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="48b36-134">有兩個動作需要 tootake hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="48b36-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="48b36-135">首先，您需要 toopublish 應用程式 Proxy 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="48b36-136">然後，您必須 toocollect hello 應用程式，可以在 hello PingAccess 步驟時使用的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="48b36-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="48b36-137">請遵循這些步驟 toopublish 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="48b36-138">如需步驟 1-8 的更詳細逐步解說，請參閱[使用 Azure AD Application Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="48b36-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="48b36-139">如果未指定 hello 最後一節中，登入 toohello [Azure 入口網站](https://portal.azure.com)身為全域管理員。</span><span class="sxs-lookup"><span data-stu-id="48b36-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="48b36-140">選取 [Azure Active Directory]  >  [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="48b36-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="48b36-141">選取**新增**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="48b36-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="48b36-142">選取**內部部署應用程式**。</span><span class="sxs-lookup"><span data-stu-id="48b36-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="48b36-143">填寫所需的 hello 欄位，新的應用程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="48b36-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="48b36-144">使用下列指導方針 hello 設定 hello:</span><span class="sxs-lookup"><span data-stu-id="48b36-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="48b36-145">**內部 URL**： 您提供 hello URL，會帶領您 toohello 應用程式的簽署頁面中當你 hello 公司網路上的一般。</span><span class="sxs-lookup"><span data-stu-id="48b36-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="48b36-146">在此案例 hello 連接器會需要 tootreat hello PingAccess proxy 以 hello 前端 hello 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="48b36-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="48b36-147">使用此格式︰`https://<host name of your PA server>:<port>`。</span><span class="sxs-lookup"><span data-stu-id="48b36-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="48b36-148">hello 通訊埠是 3000 根據預設，但您可以在 PingAccess 中進行設定。</span><span class="sxs-lookup"><span data-stu-id="48b36-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="48b36-149">**預先驗證方法**︰Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48b36-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="48b36-150">**轉譯標頭中的 URL**：否</span><span class="sxs-lookup"><span data-stu-id="48b36-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="48b36-151">如果這是您的第一個應用程式，使用連接埠 3000 toostart 回來 tooupdate 這項設定如果您變更 PingAccess 組態。</span><span class="sxs-lookup"><span data-stu-id="48b36-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="48b36-152">如果這是您第二個或更新版本的應用程式，這需要 toomatch hello PingAccess 中設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="48b36-153">深入了解 [PingAccess 中的接聽程式](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html)。</span><span class="sxs-lookup"><span data-stu-id="48b36-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="48b36-154">選取**新增**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="48b36-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="48b36-155">您的應用程式會加入，而且 hello 快速入門 功能表隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="48b36-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="48b36-156">在 [hello 快速入門] 功能表中選取**指派給使用者的測試**，新增至少一名使用者 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="48b36-157">請確定此測試帳戶具有存取 toohello 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="48b36-158">選取**指派**toosave hello 測試使用者指派。</span><span class="sxs-lookup"><span data-stu-id="48b36-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="48b36-159">在 hello 應用程式管理刀鋒視窗中，選取 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="48b36-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="48b36-160">選擇**標頭型登入**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="48b36-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="48b36-161">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="48b36-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="48b36-162">如果這是您第一次使用標頭型單一登入，您會需要 tooinstall PingAccess。</span><span class="sxs-lookup"><span data-stu-id="48b36-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="48b36-163">toomake 確定您的 Azure 訂用帳戶會自動關聯於 PingAccess 安裝，此單一登入頁面 toodownload PingAccess 上使用 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="48b36-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="48b36-164">您可以開啟 hello 下載網站，或 toothis 頁面稍後再回來。</span><span class="sxs-lookup"><span data-stu-id="48b36-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![選取標頭形式的登入](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="48b36-166">關閉 hello 企業應用程式 刀鋒視窗，或捲動所有 hello 方式 toohello 左的 tooreturn toohello Azure Active Directory 功能表。</span><span class="sxs-lookup"><span data-stu-id="48b36-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="48b36-167">選取 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="48b36-167">Select **App registrations**.</span></span>

   ![選取 [應用程式註冊]](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="48b36-169">您剛剛加入，然後選取 hello 應用程式**回覆 Url**。</span><span class="sxs-lookup"><span data-stu-id="48b36-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![選取 [回覆 URL]](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="48b36-171">請檢查 toosee 如果 hello 外部 URL，您指派的 tooyour 應用程式在步驟 5 中 hello 回覆 Url 清單中。</span><span class="sxs-lookup"><span data-stu-id="48b36-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="48b36-172">如果不存在，請立即新增。</span><span class="sxs-lookup"><span data-stu-id="48b36-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="48b36-173">在 hello 應用程式設定 刀鋒視窗，選取 **必要的權限**。</span><span class="sxs-lookup"><span data-stu-id="48b36-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![選取 [必要權限]](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="48b36-175">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="48b36-175">Select **Add**.</span></span> <span data-ttu-id="48b36-176">Hello 應用程式開發介面中，選擇  **Windows Azure Active Directory**，然後**選取**。</span><span class="sxs-lookup"><span data-stu-id="48b36-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="48b36-177">Hello 權，請選擇**讀取和寫入所有的應用程式**和**登入並讀取使用者設定檔**，然後**選取**和**完成**。</span><span class="sxs-lookup"><span data-stu-id="48b36-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![選取權限](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="48b36-179">收集 hello PingAccess 步驟的資訊</span><span class="sxs-lookup"><span data-stu-id="48b36-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="48b36-180">在應用程式設定刀鋒視窗中，選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="48b36-180">On your app settings blade, select **Properties**.</span></span> 

  ![選取 [屬性]](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="48b36-182">儲存 hello**應用程式識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="48b36-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="48b36-183">當您設定 PingAccess 時，這用於 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="48b36-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="48b36-184">在 hello 應用程式設定 刀鋒視窗，選取 **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="48b36-184">On hello app settings blade, select **Keys**.</span></span>

  ![選取 [金鑰]](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="48b36-186">輸入索引鍵的描述，然後從 hello 下拉功能表中選擇到期日建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="48b36-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="48b36-187">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="48b36-187">Select **Save**.</span></span> <span data-ttu-id="48b36-188">GUID 會出現在 hello**值**欄位。</span><span class="sxs-lookup"><span data-stu-id="48b36-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="48b36-189">儲存此值現在，當您將不會無法 toosee 它一次之後關閉此視窗。</span><span class="sxs-lookup"><span data-stu-id="48b36-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![建立新的金鑰](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="48b36-191">請關閉刀鋒視窗中的應用程式註冊 hello 或捲動所有 hello 方式 toohello 左的 tooreturn toohello Azure Active Directory 功能表。</span><span class="sxs-lookup"><span data-stu-id="48b36-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="48b36-192">選取 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="48b36-192">Select **Properties**.</span></span>
8. <span data-ttu-id="48b36-193">儲存 hello**目錄識別碼**GUID。</span><span class="sxs-lookup"><span data-stu-id="48b36-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="48b36-194">（選擇性） 更新 GraphAPI toosend 自訂欄位</span><span class="sxs-lookup"><span data-stu-id="48b36-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="48b36-195">如需 Azure AD 傳送以進行驗證的安全性權杖清單，請參閱 [Azure AD 權杖參考](./develop/active-directory-token-and-claims.md)。</span><span class="sxs-lookup"><span data-stu-id="48b36-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="48b36-196">如果您需要傳送其他語彙基元的自訂宣告，請使用 GraphAPI tooset hello 應用程式欄位*acceptMappedClaims*太**True**。</span><span class="sxs-lookup"><span data-stu-id="48b36-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="48b36-197">您可以使用 Azure AD Graph 總管或 MS 圖形 toomake 這項設定。</span><span class="sxs-lookup"><span data-stu-id="48b36-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="48b36-198">此範例使用 Graph Explorer：</span><span class="sxs-lookup"><span data-stu-id="48b36-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="48b36-199">下載 PingAccess 及設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="48b36-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="48b36-200">既然您已經完成所有 hello Azure Active Directory 的設定步驟，您可以移動 tooconfiguring PingAccess 上。</span><span class="sxs-lookup"><span data-stu-id="48b36-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="48b36-201">hello hello PingAccess 屬於此案例的詳細的步驟繼續在 hello Ping 識別文件，[設定 Azure ad 的 PingAccess](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)。</span><span class="sxs-lookup"><span data-stu-id="48b36-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="48b36-202">這些步驟會引導您完成取得 PingAccess 帳戶，如果您還沒有其中一個、 安裝 hello PingAccess 伺服器及建立 Azure AD OIDC 提供者的連接以 hello 從 hello Azure 入口網站複製的目錄識別碼 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="48b36-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="48b36-203">然後，您使用 PingAccess hello 應用程式識別碼和金鑰值 toocreate Web 工作階段。</span><span class="sxs-lookup"><span data-stu-id="48b36-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="48b36-204">之後，您可以設定身分識別對應，並建立虛擬主機、網站和應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="48b36-205">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="48b36-205">Test your app</span></span>

<span data-ttu-id="48b36-206">當您完成所有這些步驟時，您的應用程式應該啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="48b36-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="48b36-207">tootest，開啟瀏覽器並瀏覽 toohello 您在 Azure 中發行 hello 應用程式時所建立的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="48b36-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="48b36-208">使用登入 hello 測試帳戶，您指派的 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48b36-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48b36-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48b36-209">Next steps</span></span>

- [<span data-ttu-id="48b36-210">設定 Azure AD 的 PingAccess</span><span class="sxs-lookup"><span data-stu-id="48b36-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="48b36-211">Azure AD 應用程式 Proxy 如何提供單一登入？</span><span class="sxs-lookup"><span data-stu-id="48b36-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="48b36-212">疑難排解應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="48b36-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
