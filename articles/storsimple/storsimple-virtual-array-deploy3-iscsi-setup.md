---
title: "Microsoft Azure StorSimple Virtual Array iSCSI 伺服器設定 | Microsoft Docs"
description: "說明如何執行初始安裝程序、為 StorSimple iSCSI 伺服器註冊，以及完成裝置安裝程序。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 076df176d7cd40c009aea27004fe0f4415999c80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a><span data-ttu-id="703ce-103">部署 StorSimple Virtual Array - 透過 Azure 入口網站設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="703ce-103">Deploy StorSimple Virtual Array – Set up as an iSCSI server via Azure portal</span></span>

![iSCSI 安裝程序流程](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a><span data-ttu-id="703ce-105">概觀</span><span class="sxs-lookup"><span data-stu-id="703ce-105">Overview</span></span>

<span data-ttu-id="703ce-106">此部署教學課程適用於 Microsoft Azure StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="703ce-106">This deployment tutorial applies to the Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="703ce-107">本教學課程說明如何執行初始設定、註冊 StorSimple iSCSI 伺服器、完成裝置設定，然後在設定為 iSCSI 伺服器的 StorSimple Virtual Array 上建立、掛接、初始化及格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="703ce-107">This tutorial describes how to perform the initial setup, register your StorSimple iSCSI server, complete the device setup, and then create, mount, initialize, and format volumes on your StorSimple Virtual Array configured as an iSCSI server.</span></span> 

<span data-ttu-id="703ce-108">完成此處描述的程序需要大約 30 分鐘至 1 個小時。</span><span class="sxs-lookup"><span data-stu-id="703ce-108">The procedures described here take approximately 30 minutes to 1 hour to complete.</span></span> <span data-ttu-id="703ce-109">這篇文章中的資訊僅適用於 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="703ce-109">The information published in this article applies to StorSimple Virtual Arrays only.</span></span>

## <a name="setup-prerequisites"></a><span data-ttu-id="703ce-110">安裝的必要條件</span><span class="sxs-lookup"><span data-stu-id="703ce-110">Setup prerequisites</span></span>

<span data-ttu-id="703ce-111">在您設定及安裝 StorSimple Virtual Array 之前，請先確定：</span><span class="sxs-lookup"><span data-stu-id="703ce-111">Before you configure and set up your StorSimple Virtual Array, make sure that:</span></span>

* <span data-ttu-id="703ce-112">您已根據[部署 StorSimple Virtual Array：在 Hyper-V 中佈建虛擬陣列](storsimple-ova-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array：在 VMware 中佈建虛擬陣列](storsimple-virtual-array-deploy2-provision-vmware.md)中的說明，佈建並連接至虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="703ce-112">You have provisioned a virtual array and connected to it as described in [Deploy StorSimple Virtual Array - Provision a virtual array in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array  - Provision a virtual array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
* <span data-ttu-id="703ce-113">您已從您建立來管理 StorSimple Virtual Array 的 StorSimple 裝置管理員服務取得服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="703ce-113">You have the service registration key from the StorSimple Device Manager service that you created to manage your StorSimple Virtual Arrays.</span></span> <span data-ttu-id="703ce-114">如需詳細資訊，請參閱[部署 StorSimple Virtual Array：準備入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)中的**步驟 2：取得服務註冊金鑰**。</span><span class="sxs-lookup"><span data-stu-id="703ce-114">For more information, see **Step 2: Get the service registration key** in [Deploy StorSimple Virtual Array - Prepare the portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
* <span data-ttu-id="703ce-115">如果這是您要向現有 StorSimple 裝置管理員服務註冊的第二個或更後續的虛擬陣列，則您應該有服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="703ce-115">If this is the second or subsequent virtual array that you are registering with an existing StorSimple Device Manager service, you should have the service data encryption key.</span></span> <span data-ttu-id="703ce-116">當第一個裝置在此服務註冊成功時，這個金鑰就已經產生。</span><span class="sxs-lookup"><span data-stu-id="703ce-116">This key was generated when the first device was successfully registered with this service.</span></span> <span data-ttu-id="703ce-117">如果您遺失這個金鑰，請參閱《 **使用 Web UI 來管理您的 StorSimple Virtual Array** 》一文中的〈 [取得服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)〉。</span><span class="sxs-lookup"><span data-stu-id="703ce-117">If you have lost this key, see **Get the service data encryption key** in [Use the Web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span></span>

## <a name="step-by-step-setup"></a><span data-ttu-id="703ce-118">安裝的逐步指示</span><span class="sxs-lookup"><span data-stu-id="703ce-118">Step-by-step setup</span></span>

<span data-ttu-id="703ce-119">請使用下列逐步指示來安裝並設定您的 StorSimple Virtual Array：</span><span class="sxs-lookup"><span data-stu-id="703ce-119">Use the following step-by-step instructions to set up and configure your StorSimple Virtual Array:</span></span>

* [<span data-ttu-id="703ce-120">步驟 1：完成本機 Web UI 的安裝程序，並為裝置註冊</span><span class="sxs-lookup"><span data-stu-id="703ce-120">Step 1: Complete the local web UI setup and register your device</span></span>](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [<span data-ttu-id="703ce-121">步驟 2：完成必要的裝置安裝程序</span><span class="sxs-lookup"><span data-stu-id="703ce-121">Step 2: Complete the required device setup</span></span>](#step-2-complete-the-required-device-setup)
* [<span data-ttu-id="703ce-122">步驟 3：新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="703ce-122">Step 3: Add a volume</span></span>](#step-3-add-a-volume)
* [<span data-ttu-id="703ce-123">步驟 4：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="703ce-123">Step 4: Mount, initialize, and format a volume</span></span>](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-the-local-web-ui-setup-and-register-your-device"></a><span data-ttu-id="703ce-124">步驟 1：完成本機 Web UI 的安裝程序，並為裝置註冊</span><span class="sxs-lookup"><span data-stu-id="703ce-124">Step 1: Complete the local web UI setup and register your device</span></span>

#### <a name="to-complete-the-setup-and-register-the-device"></a><span data-ttu-id="703ce-125">如何完成裝置的安裝程序並為裝置註冊</span><span class="sxs-lookup"><span data-stu-id="703ce-125">To complete the setup and register the device</span></span>

1. <span data-ttu-id="703ce-126">開啟瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="703ce-126">Open a browser window.</span></span> <span data-ttu-id="703ce-127">若要連接至 Web UI，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="703ce-127">To connect to the web UI type:</span></span>
   
    `https://<ip-address of network interface>`
   
    <span data-ttu-id="703ce-128">請使用您在上一個步驟記下的連線 URL。</span><span class="sxs-lookup"><span data-stu-id="703ce-128">Use the connection URL noted in the previous step.</span></span> <span data-ttu-id="703ce-129">您會看到錯誤訊息，通知您網站的安全性憑證有問題。</span><span class="sxs-lookup"><span data-stu-id="703ce-129">You will see an error notifying you that there is a problem with the website’s security certificate.</span></span> <span data-ttu-id="703ce-130">請按一下 [繼續瀏覽此網頁] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-130">Click **Continue to this web page**.</span></span>
   
    ![安全性憑證錯誤](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. <span data-ttu-id="703ce-132">以 **StorSimpleAdmin**的帳戶名稱登入虛擬裝置的 Web UI。</span><span class="sxs-lookup"><span data-stu-id="703ce-132">Sign in to the web UI of your virtual device as **StorSimpleAdmin**.</span></span> <span data-ttu-id="703ce-133">請輸入您在[部署 StorSimple Virtual Array - 在 Hyper-V 中佈建虛擬裝置](storsimple-virtual-array-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array - 在 VMware 中佈建虛擬裝置](storsimple-virtual-array-deploy2-provision-vmware.md)的「步驟 3：啟動虛擬裝置」中所變更的裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="703ce-133">Enter the device administrator password that you changed in Step 3: Start the virtual device in [Deploy StorSimple Virtual Array - Provision a virtual device in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array - Provision a virtual device in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
   
    ![登入頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. <span data-ttu-id="703ce-135">您將會進入 [首頁]  頁面。</span><span class="sxs-lookup"><span data-stu-id="703ce-135">You will be taken to the **Home** page.</span></span> <span data-ttu-id="703ce-136">此頁面說明設定虛擬裝置並向 StorSimple 裝置管理員服務註冊時所需的各種設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-136">This page describes the various settings required to configure and register the virtual device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="703ce-137">請注意，[網路設定]、[Web Proxy 設定] 及 [時間設定] 是可省略的。</span><span class="sxs-lookup"><span data-stu-id="703ce-137">Note that the **Network settings**, **Web proxy settings**, and **Time settings** are optional.</span></span> <span data-ttu-id="703ce-138">只有 [裝置設定] 及 [雲端設定] 是必要的設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-138">The only required settings are **Device settings** and **Cloud settings**.</span></span>
   
    ![首頁](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. <span data-ttu-id="703ce-140">在 [網路設定] 頁面的 [網路介面] 下方，系統會自動為您設定 DATA 0。</span><span class="sxs-lookup"><span data-stu-id="703ce-140">On the **Network settings** page under **Network interfaces**, DATA 0 will be automatically configured for you.</span></span> <span data-ttu-id="703ce-141">每個網路介面都預設會自動取得 IP 位址 (DHCP)。</span><span class="sxs-lookup"><span data-stu-id="703ce-141">Each network interface is set by default to get an IP address automatically (DHCP).</span></span> <span data-ttu-id="703ce-142">因此，系統會自動指派 IP 位址、子網路和閘道 (IPv4 和 IPv6 皆適用)。</span><span class="sxs-lookup"><span data-stu-id="703ce-142">Therefore, an IP address, subnet, and gateway will be automatically assigned (for both IPv4 and IPv6).</span></span>
   
    <span data-ttu-id="703ce-143">因為您計畫將裝置部署為 iSCSI 伺服器 (以佈建區塊儲存體)，我們建議您停用 [自動取得 IP 位址]  選項，並設定靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="703ce-143">As you plan to deploy your device as an iSCSI server (to provision block storage), we recommend that you disable the **Get IP address automatically** option and configure static IP addresses.</span></span>
   
    ![網路設定頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    <span data-ttu-id="703ce-145">如果您在佈建裝置的過程中新增了不只一個網路介面，您可以在此設定這些網路介面。</span><span class="sxs-lookup"><span data-stu-id="703ce-145">If you added more than one network interface during the provisioning of the device, you can configure them here.</span></span> <span data-ttu-id="703ce-146">請注意，您可以將您的網路介面設定為僅 IPv4 或 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="703ce-146">Note you can configure your network interface as IPv4 only or as both IPv4 and IPv6.</span></span> <span data-ttu-id="703ce-147">不支援僅 IPv6 組態。</span><span class="sxs-lookup"><span data-stu-id="703ce-147">IPv6 only configurations are not supported.</span></span>
5. <span data-ttu-id="703ce-148">DNS 伺服器是必要的，因為在裝置嘗試與雲端儲存體服務提供者通訊時，或是在根據名稱來解析已設定為檔案伺服器的裝置時，就需要使用 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-148">DNS servers are required because they are used when your device attempts to communicate with your cloud storage service providers or to resolve your device by name if it is configured as a file server.</span></span> <span data-ttu-id="703ce-149">在 [網路設定] 頁面的 [DNS 伺服器] 下方：</span><span class="sxs-lookup"><span data-stu-id="703ce-149">On the **Network settings** page under the **DNS servers**:</span></span>
   
   1. <span data-ttu-id="703ce-150">系統會自動設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-150">A primary and secondary DNS server will be automatically configured.</span></span> <span data-ttu-id="703ce-151">如果您選擇設定靜態 IP 位址，就可以指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-151">If you choose to configure static IP addresses, you can specify DNS servers.</span></span> <span data-ttu-id="703ce-152">為了達到高可用性，我們建議您設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-152">For high availability, we recommend that you configure a primary and a secondary DNS server.</span></span>
   2. <span data-ttu-id="703ce-153">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-153">Click **Apply**.</span></span> <span data-ttu-id="703ce-154">這將會套用並驗證網路設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-154">This will apply and validate the network settings.</span></span>
6. <span data-ttu-id="703ce-155">在 [裝置設定]  頁面上：</span><span class="sxs-lookup"><span data-stu-id="703ce-155">On the **Device settings** page:</span></span>
   
   1. <span data-ttu-id="703ce-156">為裝置指派唯一的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="703ce-156">Assign a unique **Name** to your device.</span></span> <span data-ttu-id="703ce-157">這個名稱可以有 1 至 15 個字元，且可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="703ce-157">This name can be 1-15 characters and can contain letter, numbers and hyphens.</span></span>
   2. <span data-ttu-id="703ce-158">對於您要建立的裝置 [類型]，按一下 [iSCSI 伺服器] 圖示 ![iSCSI 伺服器圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png)。</span><span class="sxs-lookup"><span data-stu-id="703ce-158">Click the **iSCSI server** icon ![iSCSI server icon](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) for the **Type** of device that you are creating.</span></span> <span data-ttu-id="703ce-159">ISCSI 伺服器可讓您佈建區塊儲存體。</span><span class="sxs-lookup"><span data-stu-id="703ce-159">An iSCSI server will allow you to provision block storage.</span></span>
   3. <span data-ttu-id="703ce-160">指定您是否想讓此裝置加入網域。</span><span class="sxs-lookup"><span data-stu-id="703ce-160">Specify if you want this device to be domain-joined.</span></span> <span data-ttu-id="703ce-161">如果您的裝置是 iSCSI 伺服器，您可以省略加入網域這個步驟。</span><span class="sxs-lookup"><span data-stu-id="703ce-161">If your device is an iSCSI server, then joining the domain is optional.</span></span> <span data-ttu-id="703ce-162">如果您決定不將 iSCSI 伺服器加入網域，請按一下 [套用] 並等待設定套用完畢，然後前往下一個的步驟。</span><span class="sxs-lookup"><span data-stu-id="703ce-162">If you decide to not join your iSCSI server to a domain, click **Apply**, wait for the settings to be applied and then skip to the next step.</span></span>
      
       <span data-ttu-id="703ce-163">如果您想要讓裝置加入網域，</span><span class="sxs-lookup"><span data-stu-id="703ce-163">If you want to join the device to a domain.</span></span> <span data-ttu-id="703ce-164">輸入 [網域名稱]，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="703ce-164">Enter a **Domain name**, and then click **Apply**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="703ce-165">如果將您的 iSCSI 加入網域，請確定您的虛擬陣列位於它自己的 Microsoft Azure Active Directory 組織單位 (OU) 中，且沒有套用群組原則物件 (GPO)。</span><span class="sxs-lookup"><span data-stu-id="703ce-165">If joining your iSCSI server to a domain, ensure that your virtual  array is in its own organizational unit (OU) for Microsoft Azure Active Directory and no group policy objects (GPO) are applied to it.</span></span>
      > 
      > 
   4. <span data-ttu-id="703ce-166">此時畫面會出現對話方塊。</span><span class="sxs-lookup"><span data-stu-id="703ce-166">A dialog box will appear.</span></span> <span data-ttu-id="703ce-167">請以指定格式輸入網域認證。</span><span class="sxs-lookup"><span data-stu-id="703ce-167">Enter your domain credentials in the specified format.</span></span> <span data-ttu-id="703ce-168">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="703ce-168">Click the check icon</span></span> ![核取圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png)<span data-ttu-id="703ce-170">》一文中的指示來佈建虛擬裝置，並與該虛擬裝置連線。</span><span class="sxs-lookup"><span data-stu-id="703ce-170">.</span></span> <span data-ttu-id="703ce-171">系統將會驗證該網域認證。</span><span class="sxs-lookup"><span data-stu-id="703ce-171">The domain credentials will be verified.</span></span> <span data-ttu-id="703ce-172">如果認證不正確，畫面會出現錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="703ce-172">You will see an error message if the credentials are incorrect.</span></span>
      
       ![認證](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. <span data-ttu-id="703ce-174">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-174">Click **Apply**.</span></span> <span data-ttu-id="703ce-175">這將會套用並驗證裝置設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-175">This will apply and validate the device settings.</span></span>
7. <span data-ttu-id="703ce-176">(可省略) 設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-176">(Optionally) configure your web proxy server.</span></span> <span data-ttu-id="703ce-177">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="703ce-177">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span>
   
    ![設定 Web Proxy](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    <span data-ttu-id="703ce-179">在 [Web Proxy]  頁面上：</span><span class="sxs-lookup"><span data-stu-id="703ce-179">On the **Web proxy** page:</span></span>
   
   1. <span data-ttu-id="703ce-180">以下列格式提供 **Web Proxy URL**：「http://host-IP 位址」或「FDQN:連接埠號碼」。</span><span class="sxs-lookup"><span data-stu-id="703ce-180">Supply the **Web proxy URL** in this format: *http://host-IP address* or *FDQN:Port number*.</span></span> <span data-ttu-id="703ce-181">請注意，此處不支援 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="703ce-181">Note that HTTPS URLs are not supported.</span></span>
   2. <span data-ttu-id="703ce-182">將 [驗證] 指定為 [基本] 或 [無]。</span><span class="sxs-lookup"><span data-stu-id="703ce-182">Specify **Authentication** as **Basic** or **None**.</span></span>
   3. <span data-ttu-id="703ce-183">如果您要使用驗證功能，您也必須提供 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="703ce-183">If you are using authentication, you will also need to provide a **Username** and **Password**.</span></span>
   4. <span data-ttu-id="703ce-184">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-184">Click **Apply**.</span></span> <span data-ttu-id="703ce-185">這將會驗證並套用您設定的 Web Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-185">This will validate and apply the configured web proxy settings.</span></span>
8. <span data-ttu-id="703ce-186">(可省略) 設定裝置的時間設定，例如時區，以及主要和次要 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="703ce-186">(Optionally) configure the time settings for your device, such as time zone and the primary and secondary NTP servers.</span></span> <span data-ttu-id="703ce-187">NTP 伺服器是必要的，因為您的裝置必須讓時間同步，才能與您的雲端服務提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="703ce-187">NTP servers are required because your device must synchronize time so that it can authenticate with your cloud service providers.</span></span>
   
    ![時間設定](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    <span data-ttu-id="703ce-189">在 [時間設定]  頁面上：</span><span class="sxs-lookup"><span data-stu-id="703ce-189">On the **Time settings** page:</span></span>
   
   1. <span data-ttu-id="703ce-190">根據裝置部署的地理位置，從下拉式清單中選取 [時區]  。</span><span class="sxs-lookup"><span data-stu-id="703ce-190">From the drop-down list, select the **Time zone** based on the geographic location in which the device is being deployed.</span></span> <span data-ttu-id="703ce-191">裝置的預設時區是太平洋標準時間。</span><span class="sxs-lookup"><span data-stu-id="703ce-191">The default time zone for your device is PST.</span></span> <span data-ttu-id="703ce-192">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="703ce-192">Your device will use this time zone for all scheduled operations.</span></span>
   2. <span data-ttu-id="703ce-193">指定裝置的 [主要 NTP 伺服器]  ，或是接受預設值 time.windows.com。</span><span class="sxs-lookup"><span data-stu-id="703ce-193">Specify a **Primary NTP server** for your device or accept the default value of time.windows.com.</span></span> <span data-ttu-id="703ce-194">請確定您的網路允許 NTP 流量從您的資料中心通過網際網路。</span><span class="sxs-lookup"><span data-stu-id="703ce-194">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span>
   3. <span data-ttu-id="703ce-195">(選擇性) 指定裝置的 [次要 NTP 伺服器]  。</span><span class="sxs-lookup"><span data-stu-id="703ce-195">Optionally specify a **Secondary NTP server** for your device.</span></span>
   4. <span data-ttu-id="703ce-196">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-196">Click **Apply**.</span></span> <span data-ttu-id="703ce-197">這將會驗證並套用您設定的時間設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-197">This will validate and apply the configured time settings.</span></span>
9. <span data-ttu-id="703ce-198">設定裝置的雲端設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-198">Configure the cloud settings for your device.</span></span> <span data-ttu-id="703ce-199">在此步驟中，您將會完成本機裝置設定，然後向您的 StorSimple 裝置管理員服務註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="703ce-199">In this step, you will complete the local device configuration and then register the device with your StorSimple Device Manager service.</span></span>
   
   1. <span data-ttu-id="703ce-200">輸入您在[部署 StorSimple Virtual Array：準備入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)的**步驟 2：取得服務註冊金鑰**中取得的**服務註冊金鑰**。</span><span class="sxs-lookup"><span data-stu-id="703ce-200">Enter the **Service registration key** that you got in **Step 2: Get the service registration key** in [Deploy StorSimple Virtual Array - Prepare the Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
   2. <span data-ttu-id="703ce-201">如果這不是您向此服務註冊的第一個裝置，您將必須提供「服務資料加密金鑰」 。</span><span class="sxs-lookup"><span data-stu-id="703ce-201">If this is not the first device that you are registering with this service, you will need to provide the **Service data encryption key**.</span></span> <span data-ttu-id="703ce-202">這個金鑰需要與服務註冊金鑰搭配使用，才能向 StorSimple 裝置管理員服務註冊其他裝置。</span><span class="sxs-lookup"><span data-stu-id="703ce-202">This key is required with the service registration key to register additional devices with the StorSimple Device Manager service.</span></span> <span data-ttu-id="703ce-203">如需詳細資訊，請參閱使用本機 Web UI 來 [取得服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) 。</span><span class="sxs-lookup"><span data-stu-id="703ce-203">For more information, refer to [Get the service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) on your local web UI.</span></span>
   3. <span data-ttu-id="703ce-204">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-204">Click **Register**.</span></span> <span data-ttu-id="703ce-205">這將讓裝置重新啟動。</span><span class="sxs-lookup"><span data-stu-id="703ce-205">This will restart the device.</span></span> <span data-ttu-id="703ce-206">您可能需要等待 2 至 3 分鐘，裝置才會註冊成功。</span><span class="sxs-lookup"><span data-stu-id="703ce-206">You may need to wait for 2-3 minutes before the device is successfully registered.</span></span> <span data-ttu-id="703ce-207">裝置重新啟動之後，您將會看到登入頁面。</span><span class="sxs-lookup"><span data-stu-id="703ce-207">After the device has restarted, you will be taken to the sign in page.</span></span>
      
      ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. <span data-ttu-id="703ce-209">返回 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="703ce-209">Return to the Azure portal.</span></span>
11. <span data-ttu-id="703ce-210">瀏覽至服務的 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="703ce-210">Navigate to the **Devices** blade of your service.</span></span> <span data-ttu-id="703ce-211">如果您有大量資源，請依序按一下 [所有資源]、您的服務名稱 (如有必要，請搜尋) 及 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="703ce-211">If you have a lot of resources, click **All resources**, click your service name (search for it if necessary), and then click **Devices**.</span></span>
12. <span data-ttu-id="703ce-212">在 [裝置] 刀鋒視窗上，查閱狀態來確認裝置已成功連接至服務。</span><span class="sxs-lookup"><span data-stu-id="703ce-212">On the **Devices** blade, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="703ce-213">裝置狀態應該是 [準備好進行設定]。</span><span class="sxs-lookup"><span data-stu-id="703ce-213">The device status should be **Ready to set up**.</span></span>
    
    ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-the-device-as-iscsi-server"></a><span data-ttu-id="703ce-215">步驟 2︰將裝置設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="703ce-215">Step 2: Configure the device as iSCSI server</span></span>

<span data-ttu-id="703ce-216">在 Azure 入口網站中執行下列步驟，完成必要的裝置設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-216">Perform the following steps in the Azure portal to complete the required device setup.</span></span>

#### <a name="to-configure-the-device-as-iscsi-server"></a><span data-ttu-id="703ce-217">若要將裝置設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="703ce-217">To configure the device as iSCSI server</span></span>

1. <span data-ttu-id="703ce-218">移至 StorSimple 裝置管理員服務，再移至 [管理] > [裝置]。</span><span class="sxs-lookup"><span data-stu-id="703ce-218">Go to your StorSimple Device Manager service and then go to **Management > Devices**.</span></span> <span data-ttu-id="703ce-219">在 [裝置] 刀鋒視窗中，選取您剛建立的裝置。</span><span class="sxs-lookup"><span data-stu-id="703ce-219">In the **Devices** blade, select the device you just created.</span></span> <span data-ttu-id="703ce-220">此裝置會顯示為 [準備好進行設定]。</span><span class="sxs-lookup"><span data-stu-id="703ce-220">This device would show up as **Ready to set up**.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. <span data-ttu-id="703ce-222">按一下裝置，您會看到橫幅訊息，指出裝置已準備好進行設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-222">Click the device and you will see a banner message indicating that the device is ready to setup.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. <span data-ttu-id="703ce-224">按一下裝置命令列上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="703ce-224">Click **Configure** on the device command bar.</span></span> <span data-ttu-id="703ce-225">這會開啟 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="703ce-225">This opens up the **Configure** blade.</span></span> <span data-ttu-id="703ce-226">在 [設定] 刀鋒視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="703ce-226">In the **Configure** blade, do the following:</span></span>
   
   * <span data-ttu-id="703ce-227">iSCSI 伺服器名稱會自動填入。</span><span class="sxs-lookup"><span data-stu-id="703ce-227">The iSCSI server name is automatically populated.</span></span>
   * <span data-ttu-id="703ce-228">請確定雲端儲存體加密已設定為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="703ce-228">Make sure the cloud storage encryption is set to **Enabled**.</span></span> <span data-ttu-id="703ce-229">這可確保從裝置傳送至雲端的資料已加密。</span><span class="sxs-lookup"><span data-stu-id="703ce-229">This ensures that the data sent from the device to the cloud is encrypted.</span></span>
   * <span data-ttu-id="703ce-230">指定 32 個字元的加密金鑰，並將它記錄在金鑰管理應用程式中，供日後參考。</span><span class="sxs-lookup"><span data-stu-id="703ce-230">Specify a 32-character encryption key and record it in a key management app for future reference.</span></span>
   * <span data-ttu-id="703ce-231">選取要與裝置搭配使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="703ce-231">Select a storage account to be used with your device.</span></span> <span data-ttu-id="703ce-232">在這個訂用帳戶中，您可以選取現有的儲存體帳戶，或按一下 [新增]，從不同的訂用帳戶中選擇帳戶。</span><span class="sxs-lookup"><span data-stu-id="703ce-232">In this subscription, you can select an existing storage account, or you can click **Add** to choose an account from a different subscription.</span></span>
     
     ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. <span data-ttu-id="703ce-234">按一下 [設定] 來完成 iSCSI 伺服器的設定。</span><span class="sxs-lookup"><span data-stu-id="703ce-234">Click **Configure** to complete setting up the iSCSI server.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. <span data-ttu-id="703ce-236">正在建立 iSCSI 伺服器時會通知您。</span><span class="sxs-lookup"><span data-stu-id="703ce-236">You will be notified that the iSCSI server creation is in progress.</span></span> <span data-ttu-id="703ce-237">成功建立 iSCSI 伺服器之後，[裝置] 刀鋒視窗會更新，而且對應的裝置狀態為 [線上]。</span><span class="sxs-lookup"><span data-stu-id="703ce-237">After the iSCSI server is successfully created, the **Devices** blade is updated and the corresponding device status is **Online**.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a><span data-ttu-id="703ce-239">步驟 3：新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="703ce-239">Step 3: Add a volume</span></span>

1. <span data-ttu-id="703ce-240">在 [裝置] 刀鋒視窗中，選取您剛設定為 iSCSI 伺服器的裝置。</span><span class="sxs-lookup"><span data-stu-id="703ce-240">In the **Devices** blade, select the device you just configured as an iSCSI server.</span></span> <span data-ttu-id="703ce-241">按一下 [...] (或以滑鼠右鍵按一下此資料列)，然後從操作功能表中選取 [新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="703ce-241">Click **...** (alternatively right-click in this row) and from the context menu, select **Add volume**.</span></span> <span data-ttu-id="703ce-242">您也可以從命令列按一下 [+ 新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="703ce-242">You can also click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="703ce-243">這會開啟 [新增磁碟區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="703ce-243">This opens up the **Add volume** blade.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. <span data-ttu-id="703ce-245">在 [新增磁碟區] 刀鋒視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="703ce-245">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="703ce-246">在 [磁碟區名稱] 欄位中，輸入磁碟區的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="703ce-246">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="703ce-247">該名稱必須為包含 3 至 127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="703ce-247">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="703ce-248">在 [類型] 下拉式清單中，指定要建立 [階層式] 還是 [固定在本機] 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="703ce-248">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="703ce-249">對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="703ce-249">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned** **volume**.</span></span> <span data-ttu-id="703ce-250">針對所有其他資料，請選取 [階層式磁碟區]**磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="703ce-250">For all other data, select **Tiered** **volume**.</span></span>
   * <span data-ttu-id="703ce-251">在 [容量] 欄位中，指定磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="703ce-251">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="703ce-252">階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。</span><span class="sxs-lookup"><span data-stu-id="703ce-252">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
     
     <span data-ttu-id="703ce-253">固定在本機的磁碟區會密集佈建，且會確保磁碟區中的主要資料會保留在裝置上，不會溢出到雲端。</span><span class="sxs-lookup"><span data-stu-id="703ce-253">A locally pinned volume is thickly provisioned and ensures that the primary data in the volume stays on the device and does not spill to the cloud.</span></span>
     
     <span data-ttu-id="703ce-254">反之，階層式磁碟區是精簡佈建。</span><span class="sxs-lookup"><span data-stu-id="703ce-254">A tiered volume on the other hand is thinly provisioned.</span></span> <span data-ttu-id="703ce-255">當您建立階層式磁碟區時，大約 10% 的空間會佈建在本機層上，而 90% 的空間會佈建在雲端中。</span><span class="sxs-lookup"><span data-stu-id="703ce-255">When you create a tiered volume, approximately 10% of the space is provisioned on the local tier and 90% of the space is provisioned in the cloud.</span></span> <span data-ttu-id="703ce-256">舉例來說，如果您佈建 1 TB 的磁碟區，當資料使用階層式磁碟區時，其中 100 GB 會位於本機的空間，900 GB 會位於雲端。</span><span class="sxs-lookup"><span data-stu-id="703ce-256">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="703ce-257">然而這也代表，如果裝置已沒有可用的空間，您就無法佈建階層式共用 (因為那 10% 的空間將無法使用)。</span><span class="sxs-lookup"><span data-stu-id="703ce-257">This in turn implies is that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10% will not be available).</span></span>
     
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * <span data-ttu-id="703ce-259">按一下 [連接的主機]，選取存取控制記錄 (ACR) (對應於您要連接至此磁碟區的 iSCSI 啟動器，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="703ce-259">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span> <br><br> 
3. <span data-ttu-id="703ce-260">若要新增連接的主機，請按一下 [新增]，輸入主機的名稱及其 iSCSI 合格名稱 (IQN)，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="703ce-260">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span> <span data-ttu-id="703ce-261">如果您沒有 IQN，請前往 [附錄 A：取得 Windows Server 主機的 IQN](#appendix-a-get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="703ce-261">If you don't have the IQN, go to [Appendix A: Get the IQN of a Windows Server host](#appendix-a-get-the-iqn-of-a-windows-server-host).</span></span>
   
      ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. <span data-ttu-id="703ce-263">磁碟區設定完成之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="703ce-263">When you're finished configuring your volume, click **OK**.</span></span> <span data-ttu-id="703ce-264">將會使用指定的設定來建立磁碟區，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="703ce-264">A volume will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="703ce-265">根據預設，磁碟區的監視及備份功能將會啟用。</span><span class="sxs-lookup"><span data-stu-id="703ce-265">By default, monitoring and backup will be enabled for the volume.</span></span>
   
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. <span data-ttu-id="703ce-267">若要確認已成功建立磁碟區，請移至 [磁碟區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="703ce-267">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="703ce-268">您應該會看到此處列出該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="703ce-268">You should see the volume listed.</span></span>
   
   ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a><span data-ttu-id="703ce-270">步驟 4：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="703ce-270">Step 4: Mount, initialize, and format a volume</span></span>

<span data-ttu-id="703ce-271">請執行下列步驟，以便在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="703ce-271">Perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

#### <a name="to-mount-initialize-and-format-a-volume"></a><span data-ttu-id="703ce-272">掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="703ce-272">To mount, initialize, and format a volume</span></span>

1. <span data-ttu-id="703ce-273">在適當的伺服器上開啟 [iSCSI 啟動器] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="703ce-273">Open the **iSCSI initiator** app on the appropriate server.</span></span>
2. <span data-ttu-id="703ce-274">在 [iSCSI 啟動器屬性] 視窗的 [探索] 索引標籤上，按一下 [探索入口網站]。</span><span class="sxs-lookup"><span data-stu-id="703ce-274">In the **iSCSI Initiator Properties** window, on the **Discovery** tab, click **Discover Portal**.</span></span>
   
    ![探索入口網站](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. <span data-ttu-id="703ce-276">在 [探索目標入口網站] 對話方塊中，提供已啟用 iSCSI 網路介面的 IP 位址，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="703ce-276">In the **Discover Target Portal** dialog box, supply the IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span>
   
    ![IP 位址](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. <span data-ttu-id="703ce-278">在 [iSCSI 啟動器屬性] 視窗的 [目標] 索引標籤上，找到 [探索到的目標]。</span><span class="sxs-lookup"><span data-stu-id="703ce-278">In the **iSCSI Initiator Properties** window, on the **Targets** tab, locate the **Discovered targets**.</span></span> <span data-ttu-id="703ce-279">(每個磁碟區都會是探索到的目標。)裝置狀態應會顯示為 [非使用中] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-279">(Each volume will be a discovered target.) The device status should appear as **Inactive**.</span></span>
   
    ![探索到的目標](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. <span data-ttu-id="703ce-281">選取目標裝置，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="703ce-281">Select a target device and then click **Connect**.</span></span> <span data-ttu-id="703ce-282">連接裝置之後，狀態應會變更為 [已連接]。</span><span class="sxs-lookup"><span data-stu-id="703ce-282">After the device is connected, the status should change to **Connected**.</span></span> <span data-ttu-id="703ce-283">如需有關如何使用 Microsoft iSCSI 啟動器的詳細資訊，請參閱[安裝和設定 Microsoft iSCSI 啟動器][1]。</span><span class="sxs-lookup"><span data-stu-id="703ce-283">(For more information about using the Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
   
    ![選取目標裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. <span data-ttu-id="703ce-285">在 Windows 主機上按 Windows 標誌鍵 + X，然後按一下 [執行] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-285">On your Windows host, press the Windows Logo key + X, and then click **Run**.</span></span>
7. <span data-ttu-id="703ce-286">在 [執行] 對話方塊中，輸入 **Diskmgmt.msc**。</span><span class="sxs-lookup"><span data-stu-id="703ce-286">In the **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="703ce-287">按一下 [確定]，隨即會出現 [磁碟管理] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="703ce-287">Click **OK**, and the **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="703ce-288">右窗格將會顯示主機上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="703ce-288">The right pane will show the volumes on your host.</span></span>
8. <span data-ttu-id="703ce-289">在 [磁碟管理]  視窗中，將會出現掛接的磁碟區，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="703ce-289">In the **Disk Management** window, the mounted volumes will appear as shown in the following illustration.</span></span> <span data-ttu-id="703ce-290">以滑鼠右鍵按一下探索到的磁碟區 (按一下磁碟名稱)，然後按一下 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-290">Right-click the discovered volume (click the disk name), and then click **Online**.</span></span>
   
    ![磁碟管理](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. <span data-ttu-id="703ce-292">按一下滑鼠右鍵，然後選取 [初始化磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-292">Right-click and select **Initialize Disk**.</span></span>
   
    ![初始化磁碟 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. <span data-ttu-id="703ce-294">在對話方塊中，選取要初始化的磁碟，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-294">In the dialog box, select the disk(s) to initialize, and then click **OK**.</span></span>
    
    ![初始化磁碟 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. <span data-ttu-id="703ce-296">[新增簡單磁碟區] 精靈會隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="703ce-296">The New Simple Volume wizard starts.</span></span> <span data-ttu-id="703ce-297">請選取磁碟大小，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-297">Select a disk size, and then click **Next**.</span></span>
    
    ![新增磁碟區精靈 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. <span data-ttu-id="703ce-299">指派一個磁碟機代號給磁碟區，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-299">Assign a drive letter to the volume, and then click **Next**.</span></span>
    
    ![新增磁碟區精靈 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. <span data-ttu-id="703ce-301">輸入要格式化磁碟區所需的參數。</span><span class="sxs-lookup"><span data-stu-id="703ce-301">Enter the parameters to format the volume.</span></span> <span data-ttu-id="703ce-302">**Windows Server 只支援 NTFS。**</span><span class="sxs-lookup"><span data-stu-id="703ce-302">**On Windows Server, only NTFS is supported.**</span></span> <span data-ttu-id="703ce-303">將配置單位大小設定為 64K。</span><span class="sxs-lookup"><span data-stu-id="703ce-303">Set the allocation unit size to 64K.</span></span> <span data-ttu-id="703ce-304">並提供您磁碟區的標籤。</span><span class="sxs-lookup"><span data-stu-id="703ce-304">Provide a label for your volume.</span></span> <span data-ttu-id="703ce-305">建議的最佳做法是這個名稱與您在 StorSimple Virtual Array 上提供的磁碟區名稱相同。</span><span class="sxs-lookup"><span data-stu-id="703ce-305">It is a recommended best practice for this name to be identical to the volume name you provided on your StorSimple Virtual Array.</span></span> <span data-ttu-id="703ce-306">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-306">Click **Next**.</span></span>
    
    ![新增磁碟區精靈 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. <span data-ttu-id="703ce-308">查看您磁碟區的各個值，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="703ce-308">Check the values for your volume, and then click **Finish**.</span></span>
    
    ![新增磁碟區精靈 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    <span data-ttu-id="703ce-310">該磁碟區將會在 [磁碟管理]  on the  頁面。</span><span class="sxs-lookup"><span data-stu-id="703ce-310">The volumes will appear as **Online** on the **Disk Management** page.</span></span>
    
    ![磁碟區線上](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a><span data-ttu-id="703ce-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="703ce-312">Next steps</span></span>

<span data-ttu-id="703ce-313">了解如何使用本機 Web UI 來 [管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="703ce-313">Learn how to use the local web UI to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

## <a name="appendix-a-get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="703ce-314">附錄 A：取得 Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="703ce-314">Appendix A: Get the IQN of a Windows Server host</span></span>

<span data-ttu-id="703ce-315">請執行下列步驟，以取得正在執行 Windows Server 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="703ce-315">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server 2012.</span></span>

#### <a name="to-get-the-iqn-of-a-windows-host"></a><span data-ttu-id="703ce-316">取得 Windows 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="703ce-316">To get the IQN of a Windows host</span></span>

1. <span data-ttu-id="703ce-317">在 Windows 主機上啟動 Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="703ce-317">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
2. <span data-ttu-id="703ce-318">在 [iSCSI 啟動器屬性] 視窗的 [設定] 索引標籤上，選取並複製 [啟動器名稱] 欄位的字串。</span><span class="sxs-lookup"><span data-stu-id="703ce-318">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   
    ![iSCSI 啟動器屬性](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. <span data-ttu-id="703ce-320">儲存這個字串。</span><span class="sxs-lookup"><span data-stu-id="703ce-320">Save this string.</span></span>

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



