---
title: "Azure App Service 中 aaaConvert WordPress tooMultisite"
description: "了解 tootake 現有 WordPress web 應用程式透過 hello 組件庫在 Azure 中建立，並將它轉換 tooWordPress 多站台"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a><span data-ttu-id="98900-103">WordPress tooMultisite Azure App Service 中的轉換</span><span class="sxs-lookup"><span data-stu-id="98900-103">Convert WordPress tooMultisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="98900-104">概觀</span><span class="sxs-lookup"><span data-stu-id="98900-104">Overview</span></span>
<span data-ttu-id="98900-105">*作者 [Ben Lobaugh][ben-lobaugh]，[Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="98900-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="98900-106">在本教學課程中，您將學習如何 tootake 現有 WordPress web 應用程式透過建立 hello 組件庫在 Azure 和轉換到 WordPress 多站台安裝。</span><span class="sxs-lookup"><span data-stu-id="98900-106">In this tutorial, you will learn how tootake an existing WordPress web app created through hello gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="98900-107">此外，您將學習如何 tooassign hello 的自訂網域 tooeach 子網站中您的安裝。</span><span class="sxs-lookup"><span data-stu-id="98900-107">Additionally, you will learn how tooassign a custom domain tooeach of hello subsites within your install.</span></span>

<span data-ttu-id="98900-108">本文假設您目前已安裝 WordPress。</span><span class="sxs-lookup"><span data-stu-id="98900-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="98900-109">如果不這麼做，請遵循中提供的 hello 指引[從 hello 組件庫在 Azure 中建立 WordPress 網站][website-from-gallery]。</span><span class="sxs-lookup"><span data-stu-id="98900-109">If you do not, please follow hello guidance provided in [Create a WordPress web site from hello gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="98900-110">轉換現有的 WordPress 單一站台安裝 tooMultisite 通常是相當簡單，而且許多此處 hello 初始步驟會直接從 hello[建立網路][ wordpress-codex-create-a-network] hello頁面[WordPress Codex](http://codex.wordpress.org)。</span><span class="sxs-lookup"><span data-stu-id="98900-110">Converting an existing WordPress single site install tooMultisite is generally fairly simple, and many of hello initial steps here come straight from hello [Create A Network][wordpress-codex-create-a-network] page on hello [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="98900-111">現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="98900-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="98900-112">允許多網站</span><span class="sxs-lookup"><span data-stu-id="98900-112">Allow Multisite</span></span>
<span data-ttu-id="98900-113">您必須先透過 hello tooenable 多站台`wp-config.php`檔案以 hello **WP\_允許\_多站台**常數。</span><span class="sxs-lookup"><span data-stu-id="98900-113">You first need tooenable Multisite through hello `wp-config.php` file with hello **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="98900-114">有兩個方法 tooedit 您 web 應用程式檔案： hello 第一個是透過 FTP 和第二個透過 Git 的 hello。</span><span class="sxs-lookup"><span data-stu-id="98900-114">There are two methods tooedit your web app files: hello first is through FTP, and hello second through Git.</span></span> <span data-ttu-id="98900-115">如果您不熟悉如何 toosetup 其中一種方法，請參閱下列教學課程的 toohello:</span><span class="sxs-lookup"><span data-stu-id="98900-115">If you are unfamiliar with how toosetup either of these methods, please refer toohello following tutorials:</span></span>

* <span data-ttu-id="98900-116">[PHP 網站與 MySQL 和 FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="98900-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="98900-117">[PHP 網站與 MySQL 和 Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="98900-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="98900-118">開啟 hello `wp-config.php` hello 編輯器，您所選擇的檔案，然後加入上述 hello hello 下列`/* That's all, stop editing! Happy blogging. */`列。</span><span class="sxs-lookup"><span data-stu-id="98900-118">Open hello `wp-config.php` file with hello editor of your choosing and add hello following above hello `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="98900-119">是確定 toosave hello 檔案，並將它上傳後 toohello 伺服器 ！</span><span class="sxs-lookup"><span data-stu-id="98900-119">Be sure toosave hello file and upload it back toohello server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="98900-120">網路設定</span><span class="sxs-lookup"><span data-stu-id="98900-120">Network Setup</span></span>
<span data-ttu-id="98900-121">登入 toohello *wp admin*區域，您的 web 應用程式，並且應該會看到新的項目底下 hello**工具**功能表呼叫**網路安裝**。</span><span class="sxs-lookup"><span data-stu-id="98900-121">Log in toohello *wp-admin* area of your web app and you should see a new item under hello **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="98900-122">按一下**網路安裝**和填入 hello 詳細資料，您的網路。</span><span class="sxs-lookup"><span data-stu-id="98900-122">Click **Network Setup** and fill in hello details of your network.</span></span>

![Network Setup Screen][wordpress-network-setup]

<span data-ttu-id="98900-124">本教學課程使用 hello*子目錄*網站結構描述，因此它一定都可運作，我們將要設定每一個子網站的自訂網域在 hello 教學課程後面。</span><span class="sxs-lookup"><span data-stu-id="98900-124">This tutorial uses hello *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in hello tutorial.</span></span> <span data-ttu-id="98900-125">不過，它應該是子網域安裝，如果您透過 hello 網域對應可能 toosetup [Azure 入口網站](https://portal.azure.com)並正確設定 DNS 的萬用字元。</span><span class="sxs-lookup"><span data-stu-id="98900-125">However, it should be possible toosetup a subdomain install if you map a domain through hello [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="98900-126">如需有關子網域與子目錄龐大看到 hello[多站台的網路類型][ wordpress-codex-types-of-networks] hello WordPress Codex 上的發行項。</span><span class="sxs-lookup"><span data-stu-id="98900-126">For more information on sub-domain vs sub-directory setups see hello [Types of multisite network][wordpress-codex-types-of-networks] article on hello WordPress Codex.</span></span>

## <a name="enable-hello-network"></a><span data-ttu-id="98900-127">啟用 hello 網路</span><span class="sxs-lookup"><span data-stu-id="98900-127">Enable hello Network</span></span>
<span data-ttu-id="98900-128">hello 網路現在已設定在 hello 資料庫中，但沒有一個剩餘步驟 tooenable hello 網路功能。</span><span class="sxs-lookup"><span data-stu-id="98900-128">hello network is now configured in hello database, but there is one remaining step tooenable hello network functionality.</span></span> <span data-ttu-id="98900-129">完成 hello`wp-config.php`設定，並確定`web.config`適當地路由傳送每個站台。</span><span class="sxs-lookup"><span data-stu-id="98900-129">Finalize hello `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="98900-130">按一下 hello 之後**安裝**按鈕 hello*網路安裝*WordPress 頁面，將會嘗試 tooupdate hello`wp-config.php`和`web.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="98900-130">After clicking hello **Install** button on hello *Network Setup* page, WordPress will attempt tooupdate hello `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="98900-131">不過，您應該一律檢查 hello 檔案 tooensure hello 更新已成功。</span><span class="sxs-lookup"><span data-stu-id="98900-131">However, you should always check hello files tooensure hello updates were successful.</span></span> <span data-ttu-id="98900-132">否則，這個畫面將會顯示 hello 必要的更新。</span><span class="sxs-lookup"><span data-stu-id="98900-132">If not, this screen will present you with hello necessary updates.</span></span> <span data-ttu-id="98900-133">編輯並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="98900-133">Edit and save hello files.</span></span>

<span data-ttu-id="98900-134">之後進行這些更新，您將需要 toolog out 及記錄檔送回 hello wp-系統管理儀表板。</span><span class="sxs-lookup"><span data-stu-id="98900-134">After making these updates you will need toolog out and log back into hello wp-admin dashboard.</span></span>

<span data-ttu-id="98900-135">在標示為 hello admin 列上現在應該有更多的功能表**我網站**。</span><span class="sxs-lookup"><span data-stu-id="98900-135">There should now be an additional menu on hello admin bar labeled **My Sites**.</span></span> <span data-ttu-id="98900-136">此功能表可讓您 toocontrol hello 透過新的網路**網路系統管理員**儀表板。</span><span class="sxs-lookup"><span data-stu-id="98900-136">This menu allows you toocontrol your new network through hello **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="98900-137">加入自訂網域</span><span class="sxs-lookup"><span data-stu-id="98900-137">Adding custom domains</span></span>
<span data-ttu-id="98900-138">hello [WordPress MU 網域對應][ wordpress-plugin-wordpress-mu-domain-mapping]外掛程式可讓您輕鬆 tooadd 自訂網域 tooany 站台網路中。</span><span class="sxs-lookup"><span data-stu-id="98900-138">hello [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze tooadd custom domains tooany site in your network.</span></span> <span data-ttu-id="98900-139">為了讓 hello 外掛程式 toooperate 正常運作，您需要 toodo 上 hello 入口網站，並在網域註冊機構，某些額外的設定。</span><span class="sxs-lookup"><span data-stu-id="98900-139">In order for hello plugin toooperate properly, you need toodo some additional setup on hello Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-toohello-web-app"></a><span data-ttu-id="98900-140">啟用網域對應 toohello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="98900-140">Enable domain mapping toohello web app</span></span>
<span data-ttu-id="98900-141">hello**免費** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)計劃模式不支援新增自訂網域 tooWeb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98900-141">hello **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains tooWeb Apps.</span></span> <span data-ttu-id="98900-142">您將需要 tooswitch 太**共用**或**標準**模式。</span><span class="sxs-lookup"><span data-stu-id="98900-142">You will need tooswitch too**Shared** or **Standard** mode.</span></span> <span data-ttu-id="98900-143">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="98900-143">toodo this:</span></span>

* <span data-ttu-id="98900-144">登入 toohello Azure 入口網站，並找出您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98900-144">Log in toohello Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="98900-145">按一下 hello**向上延展**索引標籤中**設定**。</span><span class="sxs-lookup"><span data-stu-id="98900-145">Click on hello **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="98900-146">在 [一般] 下，選取 [共用] 或 [標準]</span><span class="sxs-lookup"><span data-stu-id="98900-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="98900-147">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="98900-147">Click **Save**</span></span>

<span data-ttu-id="98900-148">您可能會收到訊息，詢問您 tooverify hello 變更，並確認您 web 應用程式現在可能需支付費用，其使用方式而定，而 hello 您設定其他設定。</span><span class="sxs-lookup"><span data-stu-id="98900-148">You may receive a message asking you tooverify hello change and acknowledge your web app may now incur a cost, depending upon usage and hello other configuration you set.</span></span>

<span data-ttu-id="98900-149">需要幾秒鐘 tooprocess hello 新的設定，因此，現在是 恰好 toostart 會設定您的網域。</span><span class="sxs-lookup"><span data-stu-id="98900-149">It takes a few seconds tooprocess hello new settings, so now is a good time toostart setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="98900-150">驗證網域</span><span class="sxs-lookup"><span data-stu-id="98900-150">Verify your domain</span></span>
<span data-ttu-id="98900-151">Azure Web 應用程式可讓您 toomap 網域 toohello 網站之前，您必須先 tooverify 您擁有 hello 授權 toomap hello 網域。</span><span class="sxs-lookup"><span data-stu-id="98900-151">Before Azure Web Apps will allow you toomap a domain toohello site, you first need tooverify that you have hello authorization toomap hello domain.</span></span> <span data-ttu-id="98900-152">toodo 因此，您必須在其中加入新的 CNAME 記錄 tooyour DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="98900-152">toodo so, you must add a new CNAME record tooyour DNS entry.</span></span>

* <span data-ttu-id="98900-153">登入 tooyour 網域的 DNS 管理員</span><span class="sxs-lookup"><span data-stu-id="98900-153">Log in tooyour domain's DNS manager</span></span>
* <span data-ttu-id="98900-154">建立新的 CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="98900-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="98900-155">點*awverify*太*awverify。YOUR_DOMAIN.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="98900-155">Point *awverify* too*awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="98900-156">它可能需要完整生效的 hello DNS 變更 toogo 一些時間，因此如果 hello 步驟沒有作用，請讓咖啡、 杯回來然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="98900-156">It may take some time for hello DNS changes toogo into full effect, so if hello following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-hello-domain-toohello-web-app"></a><span data-ttu-id="98900-157">新增 hello 網域 toohello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="98900-157">Add hello domain toohello web app</span></span>
<span data-ttu-id="98900-158">傳回 tooyour web 應用程式透過 hello Azure 入口網站中，按一下**設定**，然後按一下**自訂網域及 SSL**。</span><span class="sxs-lookup"><span data-stu-id="98900-158">Return tooyour web app through hello Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="98900-159">當 hello *SSL 設定*會顯示，則會看見 hello 欄位，您將在其中輸入您想 tooassign tooyour web 應用程式的所有 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="98900-159">When hello *SSL settings* are displayed, you will see hello fields where you will input all hello domains which you wish tooassign tooyour web app.</span></span> <span data-ttu-id="98900-160">如果此處未列出網域，它將無法使用對應內 WordPress，不論 hello 網域 DNS 的安裝程式的方式。</span><span class="sxs-lookup"><span data-stu-id="98900-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how hello domain DNS is setup.</span></span>

![Manage custom domains dialog][wordpress-manage-domains]

<span data-ttu-id="98900-162">之後 hello 文字方塊中輸入您的網域，Azure 會確認 hello 您先前建立的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="98900-162">After typing your domain into hello text box, Azure will verify hello CNAME record you created previously.</span></span> <span data-ttu-id="98900-163">如果未完全傳播到 hello DNS，則會顯示紅色指示器。</span><span class="sxs-lookup"><span data-stu-id="98900-163">If hello DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="98900-164">如果成功，則會出現綠色勾選記號。</span><span class="sxs-lookup"><span data-stu-id="98900-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="98900-165">記下 IP 位址會列示在 hello hello 對話方塊底部的 hello。</span><span class="sxs-lookup"><span data-stu-id="98900-165">Take note of hello IP Address listed at hello bottom of hello dialog.</span></span> <span data-ttu-id="98900-166">您將需要此 toosetup hello 記錄為您的網域。</span><span class="sxs-lookup"><span data-stu-id="98900-166">You will need this toosetup hello A record for your domain.</span></span>

## <a name="setup-hello-domain-a-record"></a><span data-ttu-id="98900-167">安裝程式 hello 網域 A 記錄</span><span class="sxs-lookup"><span data-stu-id="98900-167">Setup hello domain A record</span></span>
<span data-ttu-id="98900-168">如果 hello 其他步驟成功，您可能會立即指派 hello 網域 tooyour Azure web 應用程式透過 DNS A 記錄。</span><span class="sxs-lookup"><span data-stu-id="98900-168">If hello other steps were successful, you may now assign hello domain tooyour Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="98900-169">它是重要 toonote 這裡 Azure web 應用程式接受 CNAME 及 A 記錄，不過您*必須*使用 A 記錄 tooenable 適當網域之間的對應。</span><span class="sxs-lookup"><span data-stu-id="98900-169">It is important toonote here that Azure web apps accept both CNAME and A records, however you *must* use an A record tooenable proper domain mapping.</span></span> <span data-ttu-id="98900-170">CNAME 無法轉送 tooanother CNAME，這是什麼 Azure 為您建立並 YOUR_DOMAIN.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="98900-170">A CNAME cannot be forwarded tooanother CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="98900-171">使用 hello hello 先前步驟中的 IP 位址，傳回 tooyour DNS 管理員及安裝 hello 記錄 toopoint toothat IP。</span><span class="sxs-lookup"><span data-stu-id="98900-171">Using hello IP address from hello previous step, return tooyour DNS manager and setup hello A record toopoint toothat IP.</span></span>

## <a name="install-and-setup-hello-plugin"></a><span data-ttu-id="98900-172">安裝及設定 hello 外掛程式</span><span class="sxs-lookup"><span data-stu-id="98900-172">Install and setup hello plugin</span></span>
<span data-ttu-id="98900-173">WordPress 多站台目前並沒有內建方法 toomap 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="98900-173">WordPress Multisite currently does not have a built-in method toomap custom domains.</span></span> <span data-ttu-id="98900-174">不過，沒有呼叫外掛程式[WordPress MU 網域對應][ wordpress-plugin-wordpress-mu-domain-mapping] ，為您加入了 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="98900-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds hello functionality for you.</span></span> <span data-ttu-id="98900-175">在您的站台 toohello 網路系統管理員部分記錄檔並安裝 hello **WordPress MU 網域對應**外掛程式。</span><span class="sxs-lookup"><span data-stu-id="98900-175">Log in toohello Network Admin portion of your site and install hello **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="98900-176">安裝和啟用 hello 外掛程式，請瀏覽之後**設定** > **網域對應**tooconfigure hello 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="98900-176">After installing and activating hello plugin, visit **Settings** > **Domain Mapping** tooconfigure hello plugin.</span></span> <span data-ttu-id="98900-177">在 hello 第一個文字方塊中，*伺服器 IP 位址*，輸入的 hello IP 位址使用 toosetup hello hello 網域的記錄。</span><span class="sxs-lookup"><span data-stu-id="98900-177">In hello first textbox, *Server IP Address*, input hello IP Address you used toosetup hello A record for hello domain.</span></span> <span data-ttu-id="98900-178">設定任何*網域選項*您想要 （hello 預設值為經常沒問題），按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="98900-178">Set any *Domain Options* you desire (hello defaults are often fine) and click **Save**.</span></span>

## <a name="map-hello-domain"></a><span data-ttu-id="98900-179">Hello 網域對應</span><span class="sxs-lookup"><span data-stu-id="98900-179">Map hello domain</span></span>
<span data-ttu-id="98900-180">請瀏覽 hello**儀表板**您想要 toomap hello 網域 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="98900-180">Visit hello **Dashboard** for hello site you wish toomap hello domain to.</span></span> <span data-ttu-id="98900-181">按一下**工具** > **網域對應**和型別輸入 hello 文字方塊中，然後按一下 hello 新網域**新增**。</span><span class="sxs-lookup"><span data-stu-id="98900-181">Click on **Tools** > **Domain Mapping** and type hello new domain into hello textbox and click **Add**.</span></span>

<span data-ttu-id="98900-182">根據預設，hello 新網域會重寫的 toohello 自動產生站台的網域。</span><span class="sxs-lookup"><span data-stu-id="98900-182">By default, hello new domain will be rewritten toohello autogenerated site domain.</span></span> <span data-ttu-id="98900-183">如果您想 toohave 所有傳送的流量 toohello 新網域時，請檢查 hello*主要網域，如這篇部落格*方塊，之後再儲存。</span><span class="sxs-lookup"><span data-stu-id="98900-183">If you want toohave all traffic sent toohello new domain, check hello *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="98900-184">您可以加入無限的數量的網域 tooa 站台，但只有一個可以是主要。</span><span class="sxs-lookup"><span data-stu-id="98900-184">You can add an unlimited number of domains tooa site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="98900-185">再做一次</span><span class="sxs-lookup"><span data-stu-id="98900-185">Do it again</span></span>
<span data-ttu-id="98900-186">Azure Web 應用程式可讓您 tooadd 網域 tooa web 應用程式數目沒有限制。</span><span class="sxs-lookup"><span data-stu-id="98900-186">Azure Web Apps allow you tooadd an unlimited number of domains tooa web app.</span></span> <span data-ttu-id="98900-187">tooadd 另一個網域，您將需要 tooexecute hello**驗證您的網域**和**安裝 hello 網域 A 記錄**區段，為每個網域。</span><span class="sxs-lookup"><span data-stu-id="98900-187">tooadd another domain you will need tooexecute hello **Verify your domain** and **Setup hello domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="98900-188">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="98900-188">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="98900-189">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="98900-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="98900-190">變更的項目</span><span class="sxs-lookup"><span data-stu-id="98900-190">What's changed</span></span>
* <span data-ttu-id="98900-191">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="98900-191">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


