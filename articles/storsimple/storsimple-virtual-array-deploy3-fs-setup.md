---
title: "將 StorSimple Virtual Array 設定為檔案伺服器 | Microsoft Docs"
description: "這是如何部署 StorSimple Virtual Array 的第三個教學課程，教導您如何將虛擬裝置設定成檔案伺服器。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bf507fb21b314a6811db1c1e45a4356381caada1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a><span data-ttu-id="465d6-103">部署 StorSimple Virtual Array - 透過 Azure 入口網站設定為檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="465d6-103">Deploy StorSimple Virtual Array - Set up as file server via Azure portal</span></span>
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a><span data-ttu-id="465d6-104">簡介</span><span class="sxs-lookup"><span data-stu-id="465d6-104">Introduction</span></span>
<span data-ttu-id="465d6-105">本文章說明如何執行初始安裝程序、為 StorSimple 檔案伺服器註冊、完成裝置安裝程序，以及建立並連接至 SMB 共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-105">This article describes how to perform initial setup, register your StorSimple file server, complete the device setup, and create and connect to SMB shares.</span></span> <span data-ttu-id="465d6-106">我們提供一系列如何將虛擬陣列完全部署為檔案伺服器或 iSCSI 伺服器的佈署教學課程，而這是該系列的最後一篇文章。</span><span class="sxs-lookup"><span data-stu-id="465d6-106">This is the last article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server.</span></span>

<span data-ttu-id="465d6-107">安裝及設定程序可能需要大約 10 分鐘的時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="465d6-107">The setup and configuration process can take around 10 minutes to complete.</span></span> <span data-ttu-id="465d6-108">本文中的資訊僅適用於部署 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="465d6-108">The information in this article applies only to the deployment of the StorSimple Virtual Array.</span></span> <span data-ttu-id="465d6-109">關於 StorSimple 8000 系列裝置的部署，請參閱︰[部署執行 Update 2 的 StorSimple 8000 系列裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="465d6-109">For the deployment of StorSimple 8000 series devices, go to: [Deploy your StorSimple 8000 series device running Update 2](storsimple-deployment-walkthrough-u2.md).</span></span>

## <a name="setup-prerequisites"></a><span data-ttu-id="465d6-110">安裝的必要條件</span><span class="sxs-lookup"><span data-stu-id="465d6-110">Setup prerequisites</span></span>
<span data-ttu-id="465d6-111">在您設定及安裝 StorSimple Virtual Array 之前，請先確定：</span><span class="sxs-lookup"><span data-stu-id="465d6-111">Before you configure and set up your StorSimple Virtual Array, make sure that:</span></span>

* <span data-ttu-id="465d6-112">您已根據[在 Hyper-V 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-hyperv.md) 或[在 VMware 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-vmware.md) 中的詳細說明，佈建並連接至虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="465d6-112">You have provisioned a virtual array and connected to it as detailed in the [Provision a StorSimple Virtual Array in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or [Provision a StorSimple Virtual Array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
* <span data-ttu-id="465d6-113">您已從您建立來管理 StorSimple Virtual Array 的 StorSimple 裝置管理員服務取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="465d6-113">You have the service registration key from the StorSimple Device Manager service that you created to manage StorSimple Virtual Arrays.</span></span> <span data-ttu-id="465d6-114">如需詳細資訊，請參閱[步驟 2：取得 StorSimple Virtual Array 的服務註冊金鑰](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="465d6-114">For more information, see [Step 2: Get the service registration key](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) for StorSimple Virtual Array.</span></span>
* <span data-ttu-id="465d6-115">如果這是您要向現有 StorSimple 裝置管理員服務註冊的第二個或更後續的虛擬陣列，則您應該有服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="465d6-115">If this is the second or subsequent virtual array that you are registering with an existing StorSimple Device Manager service, you should have the service data encryption key.</span></span> <span data-ttu-id="465d6-116">當第一個裝置在此服務註冊成功時，這個金鑰就已經產生。</span><span class="sxs-lookup"><span data-stu-id="465d6-116">This key was generated when the first device was successfully registered with this service.</span></span> <span data-ttu-id="465d6-117">如果您遺失這個金鑰，請參閱 StorSimple Virtual Array 的 [取得服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 。</span><span class="sxs-lookup"><span data-stu-id="465d6-117">If you have lost this key, see [Get the service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) for your StorSimple Virtual Array.</span></span>

## <a name="step-by-step-setup"></a><span data-ttu-id="465d6-118">安裝的逐步指示</span><span class="sxs-lookup"><span data-stu-id="465d6-118">Step-by-step setup</span></span>
<span data-ttu-id="465d6-119">請使用下列逐步指示來安裝並設定您的 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="465d6-119">Use the following step-by-step instructions to set up and configure your StorSimple Virtual Array.</span></span>

## <a name="step-1-complete-the-local-web-ui-setup-and-register-your-device"></a><span data-ttu-id="465d6-120">步驟 1：完成本機 Web UI 的安裝程序，並為裝置註冊</span><span class="sxs-lookup"><span data-stu-id="465d6-120">Step 1: Complete the local web UI setup and register your device</span></span>
#### <a name="to-complete-the-setup-and-register-the-device"></a><span data-ttu-id="465d6-121">如何完成裝置的安裝程序並為裝置註冊</span><span class="sxs-lookup"><span data-stu-id="465d6-121">To complete the setup and register the device</span></span>
1. <span data-ttu-id="465d6-122">開啟瀏覽器視窗，並連接至本機 Web UI。</span><span class="sxs-lookup"><span data-stu-id="465d6-122">Open a browser window and connect to the local web UI.</span></span> <span data-ttu-id="465d6-123">輸入：</span><span class="sxs-lookup"><span data-stu-id="465d6-123">Type:</span></span>
   
   `https://<ip-address of network interface>`
   
   <span data-ttu-id="465d6-124">請使用您在上一個步驟記下的連線 URL。</span><span class="sxs-lookup"><span data-stu-id="465d6-124">Use the connection URL noted in the previous step.</span></span> <span data-ttu-id="465d6-125">您會看到錯誤指出網站的安全性憑證有問題。</span><span class="sxs-lookup"><span data-stu-id="465d6-125">You see an error indicating that there is a problem with the website’s security certificate.</span></span> <span data-ttu-id="465d6-126">請按一下 [繼續瀏覽此網頁] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-126">Click **Continue to this webpage**.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. <span data-ttu-id="465d6-127">以 **StorSimpleAdmin** 身分登入虛擬陣列的 Web UI。</span><span class="sxs-lookup"><span data-stu-id="465d6-127">Sign in to the web UI of your virtual array as **StorSimpleAdmin**.</span></span> <span data-ttu-id="465d6-128">輸入您於[在 Hyper-V 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-hyperv.md) 或[在 VMware 中佈建 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-vmware.md) 的「步驟 3：啟動虛擬陣列」中所變更的裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="465d6-128">Enter the device administrator password that you changed in Step 3: Start the virtual array in [Provision a StorSimple Virtual Array in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or in [Provision a StorSimple Virtual Array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. <span data-ttu-id="465d6-129">您將會前往 [首頁] 頁面。</span><span class="sxs-lookup"><span data-stu-id="465d6-129">You are taken to the **Home** page.</span></span> <span data-ttu-id="465d6-130">此頁面說明設定虛擬陣列並向 StorSimple 裝置管理員服務註冊時所需的各種設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-130">This page describes the various settings required to configure and register the virtual array with the StorSimple Device Manager service.</span></span> <span data-ttu-id="465d6-131">[網路設定]、[Web Proxy 設定] 及 [時間設定] 是可省略的。</span><span class="sxs-lookup"><span data-stu-id="465d6-131">The **Network settings**, **Web proxy settings**, and **Time settings** are optional.</span></span> <span data-ttu-id="465d6-132">只有 [裝置設定] 及 [雲端設定] 是必要的設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-132">The only required settings are **Device settings** and **Cloud settings**.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. <span data-ttu-id="465d6-133">在 [網路設定] 頁面的 [網路介面] 下方，系統會自動為您設定 DATA 0。</span><span class="sxs-lookup"><span data-stu-id="465d6-133">In the **Network settings** page under **Network interfaces**, DATA 0 will be automatically configured for you.</span></span> <span data-ttu-id="465d6-134">每個網路介面都預設會自動取得 IP 位址 (DHCP)。</span><span class="sxs-lookup"><span data-stu-id="465d6-134">Each network interface is set by default to get IP address automatically (DHCP).</span></span> <span data-ttu-id="465d6-135">因此，系統會自動指派 IP 位址、子網路和閘道 (IPv4 和 IPv6 皆適用)。</span><span class="sxs-lookup"><span data-stu-id="465d6-135">Hence, an IP address, subnet, and gateway are automatically assigned (for both IPv4 and IPv6).</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   <span data-ttu-id="465d6-136">如果您在佈建裝置的過程中新增了不只一個網路介面，您可以在此設定這些網路介面。</span><span class="sxs-lookup"><span data-stu-id="465d6-136">If you added more than one network interface during the provisioning of the device, you can configure them here.</span></span> <span data-ttu-id="465d6-137">請注意，您可以將您的網路介面設定為僅 IPv4 或 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="465d6-137">Note you can configure your network interface as IPv4 only or as both IPv4 and IPv6.</span></span> <span data-ttu-id="465d6-138">不支援僅 IPv6 組態。</span><span class="sxs-lookup"><span data-stu-id="465d6-138">IPv6 only configurations are not supported.</span></span>
5. <span data-ttu-id="465d6-139">DNS 伺服器是必要的，因為在裝置嘗試與雲端儲存體服務提供者通訊時，或是在根據名稱來解析已設定為檔案伺服器的裝置時，就需要使用 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-139">DNS servers are required because they are used when your device attempts to communicate with your cloud storage service providers or to resolve your device by name when configured as a file server.</span></span> <span data-ttu-id="465d6-140">在 [網路設定] 頁面的 [DNS 伺服器] 下方：</span><span class="sxs-lookup"><span data-stu-id="465d6-140">In the **Network settings** page under the **DNS servers**:</span></span>
   
   1. <span data-ttu-id="465d6-141">系統會自動設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-141">A primary and secondary DNS server are automatically configured.</span></span> <span data-ttu-id="465d6-142">如果您選擇設定靜態 IP 位址，就可以指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-142">If you choose to configure static IP addresses, you can specify DNS servers.</span></span> <span data-ttu-id="465d6-143">為了達到高可用性，我們建議您設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-143">For high availability, we recommend that you configure a primary and a secondary DNS server.</span></span>
   2. <span data-ttu-id="465d6-144">按一下 [套用]，套用及驗證網路設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-144">Click **Apply** to apply and validate the network settings.</span></span>
6. <span data-ttu-id="465d6-145">在 [裝置設定]  頁面中：</span><span class="sxs-lookup"><span data-stu-id="465d6-145">In the **Device settings** page:</span></span>
   
   1. <span data-ttu-id="465d6-146">為裝置指派唯一的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="465d6-146">Assign a unique **Name** to your device.</span></span> <span data-ttu-id="465d6-147">這個名稱可以有 1 至 15 個字元，且可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="465d6-147">This name can be 1-15 characters and can contain letter, numbers and hyphens.</span></span>
   2. <span data-ttu-id="465d6-148">對於您要建立的裝置 [類型]，按一下 [檔案伺服器] 圖示 ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png)。</span><span class="sxs-lookup"><span data-stu-id="465d6-148">Click the **File server** icon ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) for the **Type** of device that you are creating.</span></span> <span data-ttu-id="465d6-149">檔案伺服器可讓您建立共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="465d6-149">A file server will allow you to create shared folders.</span></span>
   3. <span data-ttu-id="465d6-150">由於您的裝置是檔案伺服器，您必須讓裝置加入某個網域。</span><span class="sxs-lookup"><span data-stu-id="465d6-150">As your device is a file server, you will need to join the device to a domain.</span></span> <span data-ttu-id="465d6-151">輸入 [網域名稱] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-151">Enter a **Domain name**.</span></span>
   4. <span data-ttu-id="465d6-152">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-152">Click **Apply**.</span></span>
7. <span data-ttu-id="465d6-153">此時畫面會出現對話方塊。</span><span class="sxs-lookup"><span data-stu-id="465d6-153">A dialog box will appear.</span></span> <span data-ttu-id="465d6-154">請以指定格式輸入網域認證。</span><span class="sxs-lookup"><span data-stu-id="465d6-154">Enter your domain credentials in the specified format.</span></span> <span data-ttu-id="465d6-155">按一下核取圖示。</span><span class="sxs-lookup"><span data-stu-id="465d6-155">Click the check icon.</span></span> <span data-ttu-id="465d6-156">系統會驗證該網域認證。</span><span class="sxs-lookup"><span data-stu-id="465d6-156">The domain credentials are verified.</span></span> <span data-ttu-id="465d6-157">如果認證不正確，畫面會出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="465d6-157">You see an error message if the credentials are incorrect.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. <span data-ttu-id="465d6-158">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-158">Click **Apply**.</span></span> <span data-ttu-id="465d6-159">這將會套用並驗證裝置設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-159">This will apply and validate the device settings.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > <span data-ttu-id="465d6-160">確定您的虛擬陣列位於它自己的 Active Directory 組織單位 (OU) 中，且沒有套用或繼承任何群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="465d6-160">Ensure that your virtual array is in its own organizational unit (OU) for Active Directory and no group policy objects (GPO) are applied to it or inherited.</span></span> <span data-ttu-id="465d6-161">群組原則可能會在 StorSimple Virtual Array 上安裝應用程式，例如防毒軟體。</span><span class="sxs-lookup"><span data-stu-id="465d6-161">Group policy may install applications such as anti-virus software on the StorSimple Virtual Array.</span></span> <span data-ttu-id="465d6-162">安裝其他軟體並不受支援，而且可能導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="465d6-162">Installing additional software is not supported and could lead to data corruption.</span></span> 
   > 
   > 
9. <span data-ttu-id="465d6-163">(可省略) 設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-163">(Optionally) configure your web proxy server.</span></span> <span data-ttu-id="465d6-164">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="465d6-164">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   <span data-ttu-id="465d6-165">在 [Web Proxy]  頁面中：</span><span class="sxs-lookup"><span data-stu-id="465d6-165">In the **Web proxy** page:</span></span>
   
   1. <span data-ttu-id="465d6-166">以下列格式提供 **Web Proxy URL**：「http://&lt;host-IP 位址」或「FDQN&gt;:連接埠號碼」。</span><span class="sxs-lookup"><span data-stu-id="465d6-166">Supply the **Web proxy URL** in this format: *http://&lt;host-IP address or FDQN&gt;:Port number*.</span></span> <span data-ttu-id="465d6-167">請注意，此處不支援 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="465d6-167">Note that HTTPS URLs are not supported.</span></span>
   2. <span data-ttu-id="465d6-168">將 [驗證] 指定為 [基本] 或 [無]。</span><span class="sxs-lookup"><span data-stu-id="465d6-168">Specify **Authentication** as **Basic** or **None**.</span></span>
   3. <span data-ttu-id="465d6-169">如果要使用驗證功能，您也必須提供 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="465d6-169">If using authentication, you will also need to provide a **Username** and **Password**.</span></span>
   4. <span data-ttu-id="465d6-170">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-170">Click **Apply**.</span></span> <span data-ttu-id="465d6-171">這將會驗證並套用您設定的 Web Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-171">This will validate and apply the configured web proxy settings.</span></span>
10. <span data-ttu-id="465d6-172">(可省略) 設定裝置的時間設定，例如時區，以及主要和次要 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-172">(Optionally) configure the time settings for your device, such as time zone and the primary and secondary NTP servers.</span></span> <span data-ttu-id="465d6-173">NTP 伺服器是必要的，因為您的裝置必須讓時間同步，才能與您的雲端服務提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="465d6-173">NTP servers are required because your device must synchronize time so that it can authenticate with your cloud service providers.</span></span>
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    <span data-ttu-id="465d6-174">在 [時間設定]  頁面中：</span><span class="sxs-lookup"><span data-stu-id="465d6-174">In the **Time settings** page:</span></span>
    
    1. <span data-ttu-id="465d6-175">根據裝置部署的地理位置，從下拉式清單中選取 [時區]  。</span><span class="sxs-lookup"><span data-stu-id="465d6-175">From the dropdown list, select the **Time zone** based on the geographic location in which the device is being deployed.</span></span> <span data-ttu-id="465d6-176">裝置的預設時區是太平洋標準時間。</span><span class="sxs-lookup"><span data-stu-id="465d6-176">The default time zone for your device is PST.</span></span> <span data-ttu-id="465d6-177">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="465d6-177">Your device will use this time zone for all scheduled operations.</span></span>
    2. <span data-ttu-id="465d6-178">指定裝置的 [主要 NTP 伺服器]  ，或是接受預設值 time.windows.com。</span><span class="sxs-lookup"><span data-stu-id="465d6-178">Specify a **Primary NTP server** for your device or accept the default value of time.windows.com.</span></span> <span data-ttu-id="465d6-179">請確定您的網路允許 NTP 流量從您的資料中心通過網際網路。</span><span class="sxs-lookup"><span data-stu-id="465d6-179">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span>
    3. <span data-ttu-id="465d6-180">(選擇性) 指定裝置的 [次要 NTP 伺服器]  。</span><span class="sxs-lookup"><span data-stu-id="465d6-180">Optionally specify a **Secondary NTP server** for your device.</span></span>
    4. <span data-ttu-id="465d6-181">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-181">Click **Apply**.</span></span> <span data-ttu-id="465d6-182">這將會驗證並套用您設定的時間設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-182">This will validate and apply the configured time settings.</span></span>
11. <span data-ttu-id="465d6-183">設定裝置的雲端設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-183">Configure the cloud settings for your device.</span></span> <span data-ttu-id="465d6-184">在此步驟中，您將會完成本機裝置設定，然後向您的 StorSimple 裝置管理員服務註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="465d6-184">In this step, you will complete the local device configuration and then register the device with your StorSimple Device Manager service.</span></span>
    
    1. <span data-ttu-id="465d6-185">輸入您在 **步驟 2：取得服務註冊金鑰** 中取得的 StorSimple Virtual Array [服務註冊金鑰](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) 。</span><span class="sxs-lookup"><span data-stu-id="465d6-185">Enter the **Service registration key** that you got in [Step 2: Get the service registration key](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) for StorSimple Virtual Array.</span></span>
    2. <span data-ttu-id="465d6-186">如果這是您向此服務註冊的第一個裝置，則會出現**服務資料加密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="465d6-186">If this is your first device registering with this service, you will be presented with the **Service data encryption key**.</span></span> <span data-ttu-id="465d6-187">複製這個金鑰，並將它儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="465d6-187">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="465d6-188">這個金鑰需要與服務註冊金鑰搭配使用，才能向 StorSimple 裝置管理員服務註冊其他裝置。</span><span class="sxs-lookup"><span data-stu-id="465d6-188">This key is required with the service registration key to register additional devices with the StorSimple Device Manager service.</span></span> 
       
       <span data-ttu-id="465d6-189">如果這不是您向此服務註冊的第一個裝置，您將必須提供服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="465d6-189">If this is not the first device that you are registering with this service, you will need to provide the service data encryption key.</span></span> <span data-ttu-id="465d6-190">如需詳細資訊，請參閱使用本機 Web UI 取得 [服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 。</span><span class="sxs-lookup"><span data-stu-id="465d6-190">For more information, refer to get the [service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) on your local web UI.</span></span>
    3. <span data-ttu-id="465d6-191">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-191">Click **Register**.</span></span> <span data-ttu-id="465d6-192">這將讓裝置重新啟動。</span><span class="sxs-lookup"><span data-stu-id="465d6-192">This will restart the device.</span></span> <span data-ttu-id="465d6-193">您可能需要等待 2 至 3 分鐘，裝置才會註冊成功。</span><span class="sxs-lookup"><span data-stu-id="465d6-193">You may need to wait for 2-3 minutes before the device is successfully registered.</span></span> <span data-ttu-id="465d6-194">裝置重新啟動之後，您將會看到登入頁面。</span><span class="sxs-lookup"><span data-stu-id="465d6-194">After the device has restarted, you will be taken to the sign in page.</span></span>
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. <span data-ttu-id="465d6-195">返回 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="465d6-195">Return to the Azure portal.</span></span> <span data-ttu-id="465d6-196">移至 [所有資源]，搜尋您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="465d6-196">Go to **All resources**, search for your StorSimple Device Manager service.</span></span>
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. <span data-ttu-id="465d6-197">在已篩選的清單中，選取您的 StorSimple 裝置管理員服務，然後瀏覽至 [管理] > [裝置]。</span><span class="sxs-lookup"><span data-stu-id="465d6-197">In the filtered list, select your StorSimple Device Manager service and then navigate to **Management > Devices**.</span></span> <span data-ttu-id="465d6-198">在 [裝置] 刀鋒視窗上，確認裝置已成功連接至服務，且狀態為 [準備好進行設定]。</span><span class="sxs-lookup"><span data-stu-id="465d6-198">In the **Devices** blade, verify that the device has successfully connected to the service and has the status **Ready to set up**.</span></span>
    
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-the-device-as-file-server"></a><span data-ttu-id="465d6-200">步驟 2︰將裝置設定為檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="465d6-200">Step 2: Configure the device as file server</span></span>
<span data-ttu-id="465d6-201">在 [Azure 入口網站](https://portal.azure.com/)中執行下列步驟，完成必要的裝置設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-201">Perform the following steps in the [Azure portal](https://portal.azure.com/) to complete the required device setup.</span></span>

#### <a name="to-configure-the-device-as-file-server"></a><span data-ttu-id="465d6-202">若要將裝置設定為檔案伺服器</span><span class="sxs-lookup"><span data-stu-id="465d6-202">To configure the device as file server</span></span>
1. <span data-ttu-id="465d6-203">移至 StorSimple 裝置管理員服務，再移至 [管理] > [裝置]。</span><span class="sxs-lookup"><span data-stu-id="465d6-203">Go to your StorSimple Device Manager service and then go to  **Management > Devices**.</span></span> <span data-ttu-id="465d6-204">在 [裝置] 刀鋒視窗中，選取您剛建立的裝置。</span><span class="sxs-lookup"><span data-stu-id="465d6-204">In the **Devices** blade, select the device you just created.</span></span> <span data-ttu-id="465d6-205">此裝置會顯示為 [準備好進行設定]。</span><span class="sxs-lookup"><span data-stu-id="465d6-205">This device would show up as **Ready to set up**.</span></span>
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. <span data-ttu-id="465d6-207">按一下裝置，您會看到橫幅訊息，指出裝置已準備好進行設定。</span><span class="sxs-lookup"><span data-stu-id="465d6-207">Click the device and you will see a banner message indicating that the device is ready to setup.</span></span>
   
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. <span data-ttu-id="465d6-209">按一下命令列上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="465d6-209">Click **Configure** on the command bar.</span></span> <span data-ttu-id="465d6-210">這會開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="465d6-210">This opens up the **Configure** blade.</span></span> <span data-ttu-id="465d6-211">在 [設定] 刀鋒視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="465d6-211">In the **Configure** blade, do the following:</span></span>
   
    1. <span data-ttu-id="465d6-212">檔案伺服器名稱會自動填入。</span><span class="sxs-lookup"><span data-stu-id="465d6-212">The file server name is automatically populated.</span></span>
    
    2. <span data-ttu-id="465d6-213">請確定雲端儲存體加密已設定為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="465d6-213">Make sure the cloud storage encryption is set to **Enabled**.</span></span> <span data-ttu-id="465d6-214">這將會所有傳送至雲端的資料加密。</span><span class="sxs-lookup"><span data-stu-id="465d6-214">This will encrypt all the data that is sent to the cloud.</span></span> 
    
    3. <span data-ttu-id="465d6-215">256 位元 AES 金鑰與使用者定義的金鑰搭配用來加密。</span><span class="sxs-lookup"><span data-stu-id="465d6-215">A 256-bit AES key is used with the user-defined key for encryption.</span></span> <span data-ttu-id="465d6-216">指定 32 個字元的金鑰，然後重新輸入金鑰來加以確認。</span><span class="sxs-lookup"><span data-stu-id="465d6-216">Specify a 32 character key and then reenter the key to confirm it.</span></span> <span data-ttu-id="465d6-217">將金鑰記錄在金鑰管理應用程式中，供日後參考。</span><span class="sxs-lookup"><span data-stu-id="465d6-217">Record the key in a key management app for future reference.</span></span>
    
    4. <span data-ttu-id="465d6-218">按一下 [進行必要的設定]，以指定要用於裝置的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="465d6-218">Click **Configure required settings** to specify storage account credentials to be used with your device.</span></span> <span data-ttu-id="465d6-219">如果未設定儲存體帳戶認證，請按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="465d6-219">Click **Add new** if there are no storage account credentials configured.</span></span> <span data-ttu-id="465d6-220">**請確認您使用的儲存體帳戶支援區塊 Blob。不支援分頁 Blob。**</span><span class="sxs-lookup"><span data-stu-id="465d6-220">**Ensure that the storage account you use supports block blobs. Page blobs are not supported.**</span></span> <span data-ttu-id="465d6-221">關於 [區塊 Blob 和分頁 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="465d6-221">More information about [blocks blobs and page blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).</span></span>
   
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. <span data-ttu-id="465d6-223">在 [新增儲存體帳戶認證] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="465d6-223">In the **Add a storage account credentials** blade, do the following:</span></span> 

    1. <span data-ttu-id="465d6-224">如果儲存體帳戶與服務位於相同的訂用帳戶中，請選擇目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="465d6-224">Choose current subscription if the storage account is in the same subscription as the service.</span></span> <span data-ttu-id="465d6-225">如果儲存體帳戶在服務訂用帳戶外，請選擇其他。</span><span class="sxs-lookup"><span data-stu-id="465d6-225">Specify other is the storage account is outside of the service subscription.</span></span> 
    
    2. <span data-ttu-id="465d6-226">從下拉式清單中，選擇現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="465d6-226">From the dropdown list, choose an existing storage account.</span></span> 
    
    3. <span data-ttu-id="465d6-227">將會根據指定的儲存體帳戶來自動填入位置。</span><span class="sxs-lookup"><span data-stu-id="465d6-227">The location will be automatically populated based on the specified storage account.</span></span> 
    
    4. <span data-ttu-id="465d6-228">啟用 SSL 以確保裝置與雲端之間的安全網路通訊通道。</span><span class="sxs-lookup"><span data-stu-id="465d6-228">Enable SSL to ensure a secure network communication channel between the device and the cloud.</span></span>
    
    5. <span data-ttu-id="465d6-229">按一下 [新增]，新增此儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="465d6-229">Click **Add** to add this storage account credential.</span></span> 
   
        ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. <span data-ttu-id="465d6-231">成功建立儲存體帳戶認證之後，[設定] 刀鋒視窗將會更新，以顯示指定的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="465d6-231">Once the storage account credential is successfully created, the **Configure** blade will be updated to display the specified storage account credentials.</span></span> <span data-ttu-id="465d6-232">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-232">Click **Configure**.</span></span>
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   <span data-ttu-id="465d6-234">您會看到正在建立檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="465d6-234">You will see a that a file server is being created.</span></span> <span data-ttu-id="465d6-235">成功建立檔案伺服器之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="465d6-235">Once the file server is successfully created, you will be notified.</span></span>
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   <span data-ttu-id="465d6-237">裝置狀態也會變更為 [線上]。</span><span class="sxs-lookup"><span data-stu-id="465d6-237">The device status will also change to **Online**.</span></span>
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   <span data-ttu-id="465d6-239">您可以繼續新增共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-239">You can proceed to add a share.</span></span>

## <a name="step-3-add-a-share"></a><span data-ttu-id="465d6-240">步驟 3：新增共用</span><span class="sxs-lookup"><span data-stu-id="465d6-240">Step 3: Add a share</span></span>
<span data-ttu-id="465d6-241">請在 [Azure 入口網站](https://portal.azure.com/)中執行下列步驟來建立共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-241">Perform the following steps in the [Azure portal](https://portal.azure.com/) to create a share.</span></span>

#### <a name="to-create-a-share"></a><span data-ttu-id="465d6-242">如何建立共用</span><span class="sxs-lookup"><span data-stu-id="465d6-242">To create a share</span></span>
1. <span data-ttu-id="465d6-243">選取您在上一個步驟中設定的檔案伺服器裝置，然後按一下 ... \(或按一下滑鼠右鍵)。</span><span class="sxs-lookup"><span data-stu-id="465d6-243">Select the file server device you configured in the preceding step and click **...** (or right-click).</span></span> <span data-ttu-id="465d6-244">在操作功能表中，選取 [新增共用]。</span><span class="sxs-lookup"><span data-stu-id="465d6-244">In the context menu, select **Add share**.</span></span> <span data-ttu-id="465d6-245">或者，您也可以按一下裝置命令列上的 [+ 新增共用]。</span><span class="sxs-lookup"><span data-stu-id="465d6-245">Alternatively, you can click **+ Add Share** on the device command bar.</span></span>
   
   ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. <span data-ttu-id="465d6-247">指定下列共用設定：</span><span class="sxs-lookup"><span data-stu-id="465d6-247">Specify the following share settings:</span></span>

    1. <span data-ttu-id="465d6-248">共用的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="465d6-248">A unique name for your share.</span></span> <span data-ttu-id="465d6-249">該名稱必須為包含 3 至 127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="465d6-249">The name must be a string that contains 3 to 127 characters.</span></span>
    
    2. <span data-ttu-id="465d6-250">共用的選擇性 [說明]。</span><span class="sxs-lookup"><span data-stu-id="465d6-250">An optional **Description** for the share.</span></span> <span data-ttu-id="465d6-251">說明將可協助識別共用的擁有者。</span><span class="sxs-lookup"><span data-stu-id="465d6-251">The description will help identify the share owners.</span></span>
    
    3. <span data-ttu-id="465d6-252">共用的 [類型]。</span><span class="sxs-lookup"><span data-stu-id="465d6-252">A **Type** for the share.</span></span> <span data-ttu-id="465d6-253">類型可以是 [階層式] 或 [固定在本機]，而預設選項是 [階層式]。</span><span class="sxs-lookup"><span data-stu-id="465d6-253">The type can be **Tiered** or **Locally pinned**, with tiered being the default.</span></span> <span data-ttu-id="465d6-254">對於需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-254">For workloads that require local guarantees, low latencies, and higher performance, select a **Locally pinned** share.</span></span> <span data-ttu-id="465d6-255">對於所有其他資料，請選取 [階層式]  共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-255">For all other data, select a **Tiered** share.</span></span>
    <span data-ttu-id="465d6-256">固定在本機的共用會密集佈建，且會確保共用中的主要資料會保留在裝置上，不會溢出到雲端。</span><span class="sxs-lookup"><span data-stu-id="465d6-256">A locally pinned share is thickly provisioned and ensures that the primary data on the share stays local to the device and does not spill to the cloud.</span></span> <span data-ttu-id="465d6-257">而另一方面，階層式共用則是以精簡方式佈建。</span><span class="sxs-lookup"><span data-stu-id="465d6-257">A tiered share on the other hand is thinly provisioned.</span></span> <span data-ttu-id="465d6-258">當您建立階層式共用時，10% 的空間會佈建在本機層上，而 90% 的空間會佈建在雲端中。</span><span class="sxs-lookup"><span data-stu-id="465d6-258">When you create a tiered share, 10% of the space is provisioned on the local tier and 90% of the space is provisioned in the cloud.</span></span> <span data-ttu-id="465d6-259">舉例來說，如果您佈建 1 TB 的磁碟區，當資料使用階層式共用時，其中 100 GB 會位於本機的空間，900 GB 會位於雲端。</span><span class="sxs-lookup"><span data-stu-id="465d6-259">For instance, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="465d6-260">然而這也代表，如果裝置已沒有可用的本機空間，您就無法佈建階層式共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-260">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share.</span></span>
   
    4. <span data-ttu-id="465d6-261">在 [將預設完整權限設為] 欄位中，指派權限給存取此共用的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="465d6-261">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="465d6-262">請以下列格式指定使用者或使用者群組的名稱：*john@contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="465d6-262">Specify the name of the user or the user group in *john@contoso.com* format.</span></span> <span data-ttu-id="465d6-263">我們建議您利用使用者群組 (而非單一使用者)，來授予可存取這些共用的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="465d6-263">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="465d6-264">當您在此指派權限之後，就可以使用 [檔案總管] 來修改這些權限。</span><span class="sxs-lookup"><span data-stu-id="465d6-264">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
   
    5. <span data-ttu-id="465d6-265">按一下 [新增] 以建立共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-265">Click **Add** to create the share.</span></span> 
    
        ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        <span data-ttu-id="465d6-267">正在建立共用時會通知您。</span><span class="sxs-lookup"><span data-stu-id="465d6-267">You are notified that the share creation is in progress.</span></span>
   
        ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    <span data-ttu-id="465d6-269">使用指定的設定來建立共用之後，[共用] 刀鋒視窗將會更新以反映新的共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-269">After the share is created with the specified settings, the **Shares** blade will update to reflect the new share.</span></span> <span data-ttu-id="465d6-270">根據預設，共用會啟用監視及備份。</span><span class="sxs-lookup"><span data-stu-id="465d6-270">By default, monitoring and backup are enabled for the share.</span></span>
   
    ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-to-the-share"></a><span data-ttu-id="465d6-272">步驟 4：連線至共用</span><span class="sxs-lookup"><span data-stu-id="465d6-272">Step 4: Connect to the share</span></span>
<span data-ttu-id="465d6-273">您現在必須連接至您在上一個步驟所建立的一或多個共用。</span><span class="sxs-lookup"><span data-stu-id="465d6-273">You will now need to connect to one or more shares that you created in the previous step.</span></span> <span data-ttu-id="465d6-274">請在連接至 StorSimple Virtual Array 的 Windows Server 主機上執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="465d6-274">Perform these steps on your Windows Server host connected to your StorSimple Virtual Array.</span></span>

#### <a name="to-connect-to-the-share"></a><span data-ttu-id="465d6-275">如何連線至共用</span><span class="sxs-lookup"><span data-stu-id="465d6-275">To connect to the share</span></span>
1. <span data-ttu-id="465d6-276">按下 ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + R 鍵，然後在 [執行] 視窗中，指定 &#92;&#92;&lt;檔案伺服器名稱&gt; 做為路徑，「檔案伺服器名稱」要換成您指派給檔案伺服器的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="465d6-276">Press ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + R. In the Run window, specify the *&#92;&#92;&lt;file server name&gt;* as the path, replacing *file server name* with the device name that you assigned to your file server.</span></span> <span data-ttu-id="465d6-277">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="465d6-277">Click **OK**.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. <span data-ttu-id="465d6-278">這會開啟 [檔案總管]。</span><span class="sxs-lookup"><span data-stu-id="465d6-278">This opens up File Explorer.</span></span> <span data-ttu-id="465d6-279">您應該會看到所建立的共用以資料夾形式呈現。</span><span class="sxs-lookup"><span data-stu-id="465d6-279">You should now be able to see the shares that you created as folders.</span></span> <span data-ttu-id="465d6-280">選取並按兩下某個共用 (資料夾)，就能檢視該共用的內容。</span><span class="sxs-lookup"><span data-stu-id="465d6-280">Select and double-click a share (folder) to view the content.</span></span>
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. <span data-ttu-id="465d6-281">現在您可以把檔案新增到這些共用，然後進行備份。</span><span class="sxs-lookup"><span data-stu-id="465d6-281">You can now add files to these shares and take a backup.</span></span>

## <a name="next-steps"></a><span data-ttu-id="465d6-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="465d6-282">Next steps</span></span>
<span data-ttu-id="465d6-283">了解如何使用本機 Web UI 來 [管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="465d6-283">Learn how to use the local web UI to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

