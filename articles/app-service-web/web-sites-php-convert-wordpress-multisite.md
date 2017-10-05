---
title: "在 Azure App Service 中將 WordPress 轉換成多網站"
description: "了解如何將透過 Azure 中的組件庫所建立的現有 WordPress Web 應用程式轉換成 WordPress 多網站"
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
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="726d9-103">在 Azure App Service 中將 WordPress 轉換成多網站</span><span class="sxs-lookup"><span data-stu-id="726d9-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="726d9-104">概觀</span><span class="sxs-lookup"><span data-stu-id="726d9-104">Overview</span></span>
<span data-ttu-id="726d9-105">*作者 [Ben Lobaugh][ben-lobaugh]，[Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="726d9-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="726d9-106">在本教學課程中，您將了解如何將透過 Azure 的資源庫所建立的現有 WordPress Web 應用程式轉換成 WordPress 多網站安裝。</span><span class="sxs-lookup"><span data-stu-id="726d9-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="726d9-107">此外，您也將了解如何將自訂網域指派給安裝內的每一個子網站。</span><span class="sxs-lookup"><span data-stu-id="726d9-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="726d9-108">本文假設您目前已安裝 WordPress。</span><span class="sxs-lookup"><span data-stu-id="726d9-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="726d9-109">如果沒有，請依照 [從 Azure 中的資源庫建立 WordPress 網站][website-from-gallery]所提供的指引進行。</span><span class="sxs-lookup"><span data-stu-id="726d9-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="726d9-110">將現有的 WordPress 單一網站安裝轉換成多網站通常相當簡單，以下許多初始步驟都直接取材自 [WordPress Codex](http://codex.wordpress.org) 的[建立網站 (英文)][wordpress-codex-create-a-network] 頁面。</span><span class="sxs-lookup"><span data-stu-id="726d9-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="726d9-111">現在就開始吧。</span><span class="sxs-lookup"><span data-stu-id="726d9-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="726d9-112">允許多網站</span><span class="sxs-lookup"><span data-stu-id="726d9-112">Allow Multisite</span></span>
<span data-ttu-id="726d9-113">您需要先在 `wp-config.php` 檔案中使用 **WP\_ALLOW\_MULTISITE** 常數來啟用多網站。</span><span class="sxs-lookup"><span data-stu-id="726d9-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="726d9-114">有兩種方法可以編輯您的 Web 應用程式檔案：第一種是透過 FTP，第二種是透過 Git。</span><span class="sxs-lookup"><span data-stu-id="726d9-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="726d9-115">如果不熟悉如何設定這些方法，請參閱下列教學課程：</span><span class="sxs-lookup"><span data-stu-id="726d9-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="726d9-116">[PHP 網站與 MySQL 和 FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="726d9-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="726d9-117">[PHP 網站與 MySQL 和 Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="726d9-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="726d9-118">使用您選擇的編輯器開啟 `wp-config.php` 檔案，然後在 `/* That's all, stop editing! Happy blogging. */` 那一行上方新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="726d9-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="726d9-119">記得儲存檔並重新傳送至伺服器！</span><span class="sxs-lookup"><span data-stu-id="726d9-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="726d9-120">網路設定</span><span class="sxs-lookup"><span data-stu-id="726d9-120">Network Setup</span></span>
<span data-ttu-id="726d9-121">登入 Web 應用程式的 *wp-admin* 區域，在 [Tools] 功能表下應該會出現名為 [Network Setup] 的新項目。</span><span class="sxs-lookup"><span data-stu-id="726d9-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="726d9-122">按一下 [Network Setup]  ，填寫網路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="726d9-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Network Setup Screen][wordpress-network-setup]

<span data-ttu-id="726d9-124">本教學課程採用「子目錄」  網站結構描述，因為這總是沒有問題，我們將於教學課程稍後設定每一個子網站的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="726d9-125">不過，如果您透過 [Azure 入口網站](https://portal.azure.com) 來對應網域，並適當設定萬用字元 DNS，應該就能設定子網域安裝。</span><span class="sxs-lookup"><span data-stu-id="726d9-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="726d9-126">如需子網域和子目錄設定兩者的詳細資訊，請參閱 WordPress Codex 上的[多網站網路的類型 (英文)][wordpress-codex-types-of-networks] 文章。</span><span class="sxs-lookup"><span data-stu-id="726d9-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="726d9-127">啟用網路</span><span class="sxs-lookup"><span data-stu-id="726d9-127">Enable the Network</span></span>
<span data-ttu-id="726d9-128">資料庫中現在已設定網路，還差一步就能啟用網路功能。</span><span class="sxs-lookup"><span data-stu-id="726d9-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="726d9-129">請完成 `wp-config.php` 設定，並確定 `web.config` 可適當地路由傳送每一個網站。</span><span class="sxs-lookup"><span data-stu-id="726d9-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="726d9-130">在 [網路設定] 頁面按一下 [安裝] 按鈕後，WordPress 將嘗試更新 `wp-config.php` 和 `web.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="726d9-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="726d9-131">不過，一定要檢查檔案，以確定更新成功。</span><span class="sxs-lookup"><span data-stu-id="726d9-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="726d9-132">如果失敗，此畫面會顯示必要的更新。</span><span class="sxs-lookup"><span data-stu-id="726d9-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="726d9-133">編輯並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="726d9-133">Edit and save the files.</span></span>

<span data-ttu-id="726d9-134">進行這些更新之後，您需要先登出，然後再登入回到 wp-admin 儀表板。</span><span class="sxs-lookup"><span data-stu-id="726d9-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="726d9-135">管理列上現在應該又會多一個標示為 [My Sites] 的功能表。</span><span class="sxs-lookup"><span data-stu-id="726d9-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="726d9-136">此功能表可讓您透過 [Network Admin]  儀表板來控制新的網路。</span><span class="sxs-lookup"><span data-stu-id="726d9-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="726d9-137">加入自訂網域</span><span class="sxs-lookup"><span data-stu-id="726d9-137">Adding custom domains</span></span>
<span data-ttu-id="726d9-138">[WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] 外掛程式可讓您輕鬆地將自訂網域加入至網路中的任何網站。</span><span class="sxs-lookup"><span data-stu-id="726d9-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="726d9-139">為了讓外掛程式正常運作，您需要在入口網站上執行其他一些設定，也需要在網域註冊機構上這樣做。</span><span class="sxs-lookup"><span data-stu-id="726d9-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="726d9-140">允許將網域對應至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="726d9-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="726d9-141">**免費** [應用程式服務](http://go.microsoft.com/fwlink/?LinkId=529714) 方案模式不支援將自訂網域新增至 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="726d9-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="726d9-142">您需要切換至 [共用] 或 [標準] 模式。</span><span class="sxs-lookup"><span data-stu-id="726d9-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="726d9-143">作法：</span><span class="sxs-lookup"><span data-stu-id="726d9-143">To do this:</span></span>

* <span data-ttu-id="726d9-144">登入 Azure 入口網站，並找出您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="726d9-145">按一下 [設定] 中的 [相應增加] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="726d9-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="726d9-146">在 [一般] 下，選取 [共用] 或 [標準]</span><span class="sxs-lookup"><span data-stu-id="726d9-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="726d9-147">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="726d9-147">Click **Save**</span></span>

<span data-ttu-id="726d9-148">視使用量和您設定的其他組態而定，可能會出現訊息要求您確認變更，並認可 Web 應用程式現在可能會引發成本。</span><span class="sxs-lookup"><span data-stu-id="726d9-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="726d9-149">需要一些時間來處理新的設定，這段時間剛好可拿來開始設定您的網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="726d9-150">驗證網域</span><span class="sxs-lookup"><span data-stu-id="726d9-150">Verify your domain</span></span>
<span data-ttu-id="726d9-151">您必須先確認擁有對應網域的權限，Azure Web Apps 才會允許您將該網域對應至網站。</span><span class="sxs-lookup"><span data-stu-id="726d9-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="726d9-152">在作法上，您必須將新的 CNAME 記錄加入至 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="726d9-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="726d9-153">登入網域的 DNS 管理員</span><span class="sxs-lookup"><span data-stu-id="726d9-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="726d9-154">建立新的 CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="726d9-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="726d9-155">將 *awverify* 指向 *awverify.YOUR_DOMAIN.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="726d9-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="726d9-156">DNS 變更需要一些時間才會完全生效，如果無法立即執行下列步驟，請休息一下，稍後再回來重試。</span><span class="sxs-lookup"><span data-stu-id="726d9-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="726d9-157">將網域加入至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="726d9-157">Add the domain to the web app</span></span>
<span data-ttu-id="726d9-158">透過 Azure 入口網站返回您的 Web 應用程式、按一下 [設定]，然後按一下 [自訂網域和 SSL]。</span><span class="sxs-lookup"><span data-stu-id="726d9-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="726d9-159">當 [SSL 設定]  顯示時，將會看到您要輸入所有希望指派給 Web 應用程式之網域的欄位。</span><span class="sxs-lookup"><span data-stu-id="726d9-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="726d9-160">如果其中未列出某個網域，就表示不論網域 DNS 如何設定，都無法在 WordPress 內對應此網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Manage custom domains dialog][wordpress-manage-domains]

<span data-ttu-id="726d9-162">在文字方塊中輸入網域之後，Azure 會驗證您先前建立的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="726d9-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="726d9-163">如果 DNS 未完整傳播，則會出現紅色指標。</span><span class="sxs-lookup"><span data-stu-id="726d9-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="726d9-164">如果成功，則會出現綠色勾選記號。</span><span class="sxs-lookup"><span data-stu-id="726d9-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="726d9-165">請記下對話方塊底部列出的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="726d9-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="726d9-166">設定網域的 A 記錄時需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="726d9-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="726d9-167">設定網域 A 記錄</span><span class="sxs-lookup"><span data-stu-id="726d9-167">Setup the domain A record</span></span>
<span data-ttu-id="726d9-168">如果其他步驟成功，則現在可透過 DNS A 記錄，將網域指派給 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="726d9-169">在此必須注意，Azure Web 應用程式接受 CNAME 與 A 記錄，但您「必須」  使用 A 記錄，才能啟用適當的網域對應。</span><span class="sxs-lookup"><span data-stu-id="726d9-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="726d9-170">CNAME 無法轉送至另一個 CNAME，即 Azure 以 YOUR_DOMAIN.azurewebsites.net 為您建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="726d9-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="726d9-171">回到 DNS 管理員，設定 A 記錄來指向您在上一步記下的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="726d9-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="726d9-172">安裝和設定外掛程式</span><span class="sxs-lookup"><span data-stu-id="726d9-172">Install and setup the plugin</span></span>
<span data-ttu-id="726d9-173">WordPress 多網站目前沒有內建的方法可對應自訂網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="726d9-174">不過，有一個稱為 [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] 的外掛程式可為您增加此功能。</span><span class="sxs-lookup"><span data-stu-id="726d9-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="726d9-175">請登入網站的 [Network Admin] 部分，並安裝 **WordPress MU Domain Mapping** 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="726d9-176">安裝並啟動此外掛程式之後，請移至 [Settings] \(設定)  > [Domain Mapping] \(網域對應)  來設定外掛程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="726d9-177">在第一個文字方塊 [Server IP Address] 中，輸入您用來設定網域 A 記錄的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="726d9-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="726d9-178">設定您要的任何 [Domain Options] \(預設值通常就很適合)，然後按一下 [Save]。</span><span class="sxs-lookup"><span data-stu-id="726d9-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="726d9-179">對應網域</span><span class="sxs-lookup"><span data-stu-id="726d9-179">Map the domain</span></span>
<span data-ttu-id="726d9-180">移至要讓網域對應到的網站的 [Dashboard]  。</span><span class="sxs-lookup"><span data-stu-id="726d9-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="726d9-181">按一下 [Tools] > [Domain Mapping]，在文字方塊中輸入新的網域，然後按一下 [Add]。</span><span class="sxs-lookup"><span data-stu-id="726d9-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="726d9-182">依預設，新的網域會改寫為自動產生的網站網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="726d9-183">如果要讓所有流量都傳送至新網域，請在儲存之前勾選 [Primary domain for this blog]  方塊。</span><span class="sxs-lookup"><span data-stu-id="726d9-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="726d9-184">可加入至網站的網域數量不限，但只能有一個主網域。</span><span class="sxs-lookup"><span data-stu-id="726d9-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="726d9-185">再做一次</span><span class="sxs-lookup"><span data-stu-id="726d9-185">Do it again</span></span>
<span data-ttu-id="726d9-186">Azure Web Apps 可讓您將不限數量的網域加入至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="726d9-187">若要加入其他網域，您需要對每一個網域執行＜**驗證網域**＞和＜**設定網域 A 記錄**＞兩節。</span><span class="sxs-lookup"><span data-stu-id="726d9-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="726d9-188">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="726d9-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="726d9-189">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="726d9-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="726d9-190">變更的項目</span><span class="sxs-lookup"><span data-stu-id="726d9-190">What's changed</span></span>
* <span data-ttu-id="726d9-191">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="726d9-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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


