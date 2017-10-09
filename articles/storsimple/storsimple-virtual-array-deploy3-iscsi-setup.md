---
title: "Azure StorSimple Virtual Array iSCSI 伺服器安裝程式 aaaMicrosoft |Microsoft 文件"
description: "描述如何 tooperform 初始設定，註冊您的 StorSimple iSCSI 伺服器，並完成裝置設定。"
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
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a><span data-ttu-id="7288f-103">部署 StorSimple Virtual Array - 透過 Azure 入口網站設定為 iSCSI 伺服器</span><span class="sxs-lookup"><span data-stu-id="7288f-103">Deploy StorSimple Virtual Array – Set up as an iSCSI server via Azure portal</span></span>

![iSCSI 安裝程序流程](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a><span data-ttu-id="7288f-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7288f-105">Overview</span></span>

<span data-ttu-id="7288f-106">此部署教學課程適用於 Microsoft Azure StorSimple Virtual Array toohello。</span><span class="sxs-lookup"><span data-stu-id="7288f-106">This deployment tutorial applies toohello Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="7288f-107">本教學課程說明如何 tooperform hello 初始設定，註冊您的 StorSimple iSCSI 伺服器，完成 hello 裝置設定，然後建立、 掛接、 初始化，並格式化磁碟區上設定 iSCSI 伺服器為您 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="7288f-107">This tutorial describes how tooperform hello initial setup, register your StorSimple iSCSI server, complete hello device setup, and then create, mount, initialize, and format volumes on your StorSimple Virtual Array configured as an iSCSI server.</span></span> 

<span data-ttu-id="7288f-108">這裡所述的 hello 程序會採取大約 30 分鐘 too1 小時 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7288f-108">hello procedures described here take approximately 30 minutes too1 hour toocomplete.</span></span> <span data-ttu-id="7288f-109">這篇文章中發行的 hello 資訊適用於僅 tooStorSimple 虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="7288f-109">hello information published in this article applies tooStorSimple Virtual Arrays only.</span></span>

## <a name="setup-prerequisites"></a><span data-ttu-id="7288f-110">安裝的必要條件</span><span class="sxs-lookup"><span data-stu-id="7288f-110">Setup prerequisites</span></span>

<span data-ttu-id="7288f-111">在您設定及安裝 StorSimple Virtual Array 之前，請先確定：</span><span class="sxs-lookup"><span data-stu-id="7288f-111">Before you configure and set up your StorSimple Virtual Array, make sure that:</span></span>

* <span data-ttu-id="7288f-112">您已佈建的虛擬陣列，並連接中所述的 tooit[部署 StorSimple Virtual Array-佈建為 HYPER-V 中的虛擬陣列](storsimple-ova-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array-佈建在 VMware 中的虛擬陣列](storsimple-virtual-array-deploy2-provision-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="7288f-112">You have provisioned a virtual array and connected tooit as described in [Deploy StorSimple Virtual Array - Provision a virtual array in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array  - Provision a virtual array in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
* <span data-ttu-id="7288f-113">您必須從您建立 toomanage 您 StorSimple 虛擬陣列的 StorSimple 裝置管理員服務 hello hello 服務註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="7288f-113">You have hello service registration key from hello StorSimple Device Manager service that you created toomanage your StorSimple Virtual Arrays.</span></span> <span data-ttu-id="7288f-114">如需詳細資訊，請參閱**步驟 2： 取得 hello 服務註冊金鑰**中[部署 StorSimple Virtual Array-準備 hello 入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="7288f-114">For more information, see **Step 2: Get hello service registration key** in [Deploy StorSimple Virtual Array - Prepare hello portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
* <span data-ttu-id="7288f-115">如果這是 hello 第二或後續虛擬陣列，您會註冊現有的 StorSimple 裝置管理員服務時，您應該 hello 服務資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="7288f-115">If this is hello second or subsequent virtual array that you are registering with an existing StorSimple Device Manager service, you should have hello service data encryption key.</span></span> <span data-ttu-id="7288f-116">此服務已成功註冊 hello 第一個裝置時，所產生此金鑰。</span><span class="sxs-lookup"><span data-stu-id="7288f-116">This key was generated when hello first device was successfully registered with this service.</span></span> <span data-ttu-id="7288f-117">如果您遺失了金鑰，請參閱**Get hello 服務資料加密金鑰**中[使用 hello Web UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)。</span><span class="sxs-lookup"><span data-stu-id="7288f-117">If you have lost this key, see **Get hello service data encryption key** in [Use hello Web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).</span></span>

## <a name="step-by-step-setup"></a><span data-ttu-id="7288f-118">安裝的逐步指示</span><span class="sxs-lookup"><span data-stu-id="7288f-118">Step-by-step setup</span></span>

<span data-ttu-id="7288f-119">使用遵循逐步指示 tooset hello，並設定 StorSimple 虛擬陣列：</span><span class="sxs-lookup"><span data-stu-id="7288f-119">Use hello following step-by-step instructions tooset up and configure your StorSimple Virtual Array:</span></span>

* [<span data-ttu-id="7288f-120">步驟 1： 完成 hello 本機 web UI 安裝並註冊您的裝置</span><span class="sxs-lookup"><span data-stu-id="7288f-120">Step 1: Complete hello local web UI setup and register your device</span></span>](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [<span data-ttu-id="7288f-121">步驟 2： 完成 hello 所需的裝置設定</span><span class="sxs-lookup"><span data-stu-id="7288f-121">Step 2: Complete hello required device setup</span></span>](#step-2-complete-the-required-device-setup)
* [<span data-ttu-id="7288f-122">步驟 3：新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="7288f-122">Step 3: Add a volume</span></span>](#step-3-add-a-volume)
* [<span data-ttu-id="7288f-123">步驟 4：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="7288f-123">Step 4: Mount, initialize, and format a volume</span></span>](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a><span data-ttu-id="7288f-124">步驟 1： 完成 hello 本機 web UI 安裝並註冊您的裝置</span><span class="sxs-lookup"><span data-stu-id="7288f-124">Step 1: Complete hello local web UI setup and register your device</span></span>

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a><span data-ttu-id="7288f-125">toocomplete hello 安裝和註冊的裝置 hello</span><span class="sxs-lookup"><span data-stu-id="7288f-125">toocomplete hello setup and register hello device</span></span>

1. <span data-ttu-id="7288f-126">開啟瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="7288f-126">Open a browser window.</span></span> <span data-ttu-id="7288f-127">tooconnect toohello web UI 型別：</span><span class="sxs-lookup"><span data-stu-id="7288f-127">tooconnect toohello web UI type:</span></span>
   
    `https://<ip-address of network interface>`
   
    <span data-ttu-id="7288f-128">使用 hello 上一個步驟中所述的 hello 連接 URL。</span><span class="sxs-lookup"><span data-stu-id="7288f-128">Use hello connection URL noted in hello previous step.</span></span> <span data-ttu-id="7288f-129">您會看到錯誤訊息，通知您沒有 hello 網站的安全性憑證有問題。</span><span class="sxs-lookup"><span data-stu-id="7288f-129">You will see an error notifying you that there is a problem with hello website’s security certificate.</span></span> <span data-ttu-id="7288f-130">按一下**繼續 toothis 網頁**。</span><span class="sxs-lookup"><span data-stu-id="7288f-130">Click **Continue toothis web page**.</span></span>
   
    ![安全性憑證錯誤](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. <span data-ttu-id="7288f-132">登入 toohello web UI 虛擬裝置做為**StorSimpleAdmin**。</span><span class="sxs-lookup"><span data-stu-id="7288f-132">Sign in toohello web UI of your virtual device as **StorSimpleAdmin**.</span></span> <span data-ttu-id="7288f-133">輸入 hello 裝置系統管理員變更密碼。 您在步驟 3： 在開始 hello 虛擬裝置[部署 StorSimple Virtual Array-在 HYPER-V 中的虛擬裝置佈建](storsimple-virtual-array-deploy2-provision-hyperv.md)或[部署 StorSimple Virtual Array-在 VMware 中的虛擬裝置佈建](storsimple-virtual-array-deploy2-provision-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="7288f-133">Enter hello device administrator password that you changed in Step 3: Start hello virtual device in [Deploy StorSimple Virtual Array - Provision a virtual device in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) or [Deploy StorSimple Virtual Array - Provision a virtual device in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).</span></span>
   
    ![登入頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. <span data-ttu-id="7288f-135">您將會進入 toohello**首頁**頁面。</span><span class="sxs-lookup"><span data-stu-id="7288f-135">You will be taken toohello **Home** page.</span></span> <span data-ttu-id="7288f-136">此頁面描述 hello tooconfigure 和註冊 hello 與 hello StorSimple 裝置管理員服務的虛擬裝置所需的各種設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-136">This page describes hello various settings required tooconfigure and register hello virtual device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="7288f-137">請注意該 hello**網路設定**， **Web proxy 設定**，和**時間設定**是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7288f-137">Note that hello **Network settings**, **Web proxy settings**, and **Time settings** are optional.</span></span> <span data-ttu-id="7288f-138">hello 只需要設定**裝置設定**和**雲端設定**。</span><span class="sxs-lookup"><span data-stu-id="7288f-138">hello only required settings are **Device settings** and **Cloud settings**.</span></span>
   
    ![首頁](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. <span data-ttu-id="7288f-140">在 hello**網路設定**頁面**網路介面**，DATA 0 將會為您自動設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-140">On hello **Network settings** page under **Network interfaces**, DATA 0 will be automatically configured for you.</span></span> <span data-ttu-id="7288f-141">每個網路介面會由預設 tooget IP 位址自動設定 (DHCP)。</span><span class="sxs-lookup"><span data-stu-id="7288f-141">Each network interface is set by default tooget an IP address automatically (DHCP).</span></span> <span data-ttu-id="7288f-142">因此，系統會自動指派 IP 位址、子網路和閘道 (IPv4 和 IPv6 皆適用)。</span><span class="sxs-lookup"><span data-stu-id="7288f-142">Therefore, an IP address, subnet, and gateway will be automatically assigned (for both IPv4 and IPv6).</span></span>
   
    <span data-ttu-id="7288f-143">當您規劃 toodeploy 您的裝置為 iSCSI 伺服器 （tooprovision 區塊存放裝置），我們建議您停用 hello**自動取得 IP 位址**選項，並設定靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7288f-143">As you plan toodeploy your device as an iSCSI server (tooprovision block storage), we recommend that you disable hello **Get IP address automatically** option and configure static IP addresses.</span></span>
   
    ![網路設定頁面](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    <span data-ttu-id="7288f-145">如果您加入多個網路介面 hello 佈建的 hello 裝置期間，您可以在此設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-145">If you added more than one network interface during hello provisioning of hello device, you can configure them here.</span></span> <span data-ttu-id="7288f-146">請注意，您可以將您的網路介面設定為僅 IPv4 或 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="7288f-146">Note you can configure your network interface as IPv4 only or as both IPv4 and IPv6.</span></span> <span data-ttu-id="7288f-147">不支援僅 IPv6 組態。</span><span class="sxs-lookup"><span data-stu-id="7288f-147">IPv6 only configurations are not supported.</span></span>
5. <span data-ttu-id="7288f-148">因為它們由您的裝置嘗試與您的雲端儲存體服務提供者或 tooresolve toocommunicate 您的裝置時名稱如果設定為檔案伺服器，都需要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-148">DNS servers are required because they are used when your device attempts toocommunicate with your cloud storage service providers or tooresolve your device by name if it is configured as a file server.</span></span> <span data-ttu-id="7288f-149">在 hello**網路設定**頁面下 hello **DNS 伺服器**:</span><span class="sxs-lookup"><span data-stu-id="7288f-149">On hello **Network settings** page under hello **DNS servers**:</span></span>
   
   1. <span data-ttu-id="7288f-150">系統會自動設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-150">A primary and secondary DNS server will be automatically configured.</span></span> <span data-ttu-id="7288f-151">如果您選擇 tooconfigure 靜態 IP 位址，您可以指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-151">If you choose tooconfigure static IP addresses, you can specify DNS servers.</span></span> <span data-ttu-id="7288f-152">為了達到高可用性，我們建議您設定主要及次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-152">For high availability, we recommend that you configure a primary and a secondary DNS server.</span></span>
   2. <span data-ttu-id="7288f-153">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-153">Click **Apply**.</span></span> <span data-ttu-id="7288f-154">這將會套用並驗證 hello 網路設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-154">This will apply and validate hello network settings.</span></span>
6. <span data-ttu-id="7288f-155">在 hello**裝置設定**頁面：</span><span class="sxs-lookup"><span data-stu-id="7288f-155">On hello **Device settings** page:</span></span>
   
   1. <span data-ttu-id="7288f-156">指派一個唯一**名稱**tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="7288f-156">Assign a unique **Name** tooyour device.</span></span> <span data-ttu-id="7288f-157">這個名稱可以有 1 至 15 個字元，且可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="7288f-157">This name can be 1-15 characters and can contain letter, numbers and hyphens.</span></span>
   2. <span data-ttu-id="7288f-158">按一下 hello **iSCSI 伺服器**圖示![iSCSI 伺服器圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png)hello**類型**裝置所建立。</span><span class="sxs-lookup"><span data-stu-id="7288f-158">Click hello **iSCSI server** icon ![iSCSI server icon](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) for hello **Type** of device that you are creating.</span></span> <span data-ttu-id="7288f-159">ISCSI 伺服器可讓您 tooprovision 區塊存放裝置。</span><span class="sxs-lookup"><span data-stu-id="7288f-159">An iSCSI server will allow you tooprovision block storage.</span></span>
   3. <span data-ttu-id="7288f-160">指定是否要讓此裝置 toobe 已加入網域。</span><span class="sxs-lookup"><span data-stu-id="7288f-160">Specify if you want this device toobe domain-joined.</span></span> <span data-ttu-id="7288f-161">如果您的裝置是 iSCSI 伺服器，然後加入 hello 網域是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="7288f-161">If your device is an iSCSI server, then joining hello domain is optional.</span></span> <span data-ttu-id="7288f-162">如果您決定 toonot 聯結 iSCSI 伺服器 tooa 網域，請按一下**套用**等候 hello 設定 toobe 套用，則可略過 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7288f-162">If you decide toonot join your iSCSI server tooa domain, click **Apply**, wait for hello settings toobe applied and then skip toohello next step.</span></span>
      
       <span data-ttu-id="7288f-163">如果您想 toojoin hello 裝置 tooa 網域。</span><span class="sxs-lookup"><span data-stu-id="7288f-163">If you want toojoin hello device tooa domain.</span></span> <span data-ttu-id="7288f-164">輸入 網域名稱，然後按一下套用。</span><span class="sxs-lookup"><span data-stu-id="7288f-164">Enter a **Domain name**, and then click **Apply**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7288f-165">如果您的虛擬陣列是 Microsoft Azure Active Directory 和群組原則物件 (GPO) 自己組織單位 (OU) 中加入您的 iSCSI 伺服器 tooa 網域，確保會套用的 tooit。</span><span class="sxs-lookup"><span data-stu-id="7288f-165">If joining your iSCSI server tooa domain, ensure that your virtual  array is in its own organizational unit (OU) for Microsoft Azure Active Directory and no group policy objects (GPO) are applied tooit.</span></span>
      > 
      > 
   4. <span data-ttu-id="7288f-166">此時畫面會出現對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7288f-166">A dialog box will appear.</span></span> <span data-ttu-id="7288f-167">Hello 指定的格式輸入您的網域認證。</span><span class="sxs-lookup"><span data-stu-id="7288f-167">Enter your domain credentials in hello specified format.</span></span> <span data-ttu-id="7288f-168">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="7288f-168">Click hello check icon</span></span> ![核取圖示](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png)<span data-ttu-id="7288f-170">.</span><span class="sxs-lookup"><span data-stu-id="7288f-170">.</span></span> <span data-ttu-id="7288f-171">將驗證 hello 網域認證。</span><span class="sxs-lookup"><span data-stu-id="7288f-171">hello domain credentials will be verified.</span></span> <span data-ttu-id="7288f-172">如果 hello 認證不正確，您會看到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7288f-172">You will see an error message if hello credentials are incorrect.</span></span>
      
       ![認證](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. <span data-ttu-id="7288f-174">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-174">Click **Apply**.</span></span> <span data-ttu-id="7288f-175">這將會套用並驗證 hello 裝置設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-175">This will apply and validate hello device settings.</span></span>
7. <span data-ttu-id="7288f-176">(可省略) 設定 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-176">(Optionally) configure your web proxy server.</span></span> <span data-ttu-id="7288f-177">雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。</span><span class="sxs-lookup"><span data-stu-id="7288f-177">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span>
   
    ![設定 Web Proxy](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    <span data-ttu-id="7288f-179">在 hello **Web proxy**頁面：</span><span class="sxs-lookup"><span data-stu-id="7288f-179">On hello **Web proxy** page:</span></span>
   
   1. <span data-ttu-id="7288f-180">供應 hello **Web proxy URL**格式如下： *http://host-IP 位址*或*FDQN:Port 數目*。</span><span class="sxs-lookup"><span data-stu-id="7288f-180">Supply hello **Web proxy URL** in this format: *http://host-IP address* or *FDQN:Port number*.</span></span> <span data-ttu-id="7288f-181">請注意，此處不支援 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="7288f-181">Note that HTTPS URLs are not supported.</span></span>
   2. <span data-ttu-id="7288f-182">將 [驗證] 指定為 [基本] 或 [無]。</span><span class="sxs-lookup"><span data-stu-id="7288f-182">Specify **Authentication** as **Basic** or **None**.</span></span>
   3. <span data-ttu-id="7288f-183">如果您使用的驗證，您也必須 tooprovide **Username**和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="7288f-183">If you are using authentication, you will also need tooprovide a **Username** and **Password**.</span></span>
   4. <span data-ttu-id="7288f-184">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-184">Click **Apply**.</span></span> <span data-ttu-id="7288f-185">這將會驗證並套用 hello 設定 web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-185">This will validate and apply hello configured web proxy settings.</span></span>
8. <span data-ttu-id="7288f-186">（選擇性） 設定您的裝置，例如時區的 hello 時間設定與 hello 主要和次要 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-186">(Optionally) configure hello time settings for your device, such as time zone and hello primary and secondary NTP servers.</span></span> <span data-ttu-id="7288f-187">NTP 伺服器是必要的，因為您的裝置必須讓時間同步，才能與您的雲端服務提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7288f-187">NTP servers are required because your device must synchronize time so that it can authenticate with your cloud service providers.</span></span>
   
    ![時間設定](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    <span data-ttu-id="7288f-189">在 hello**時間設定**頁面：</span><span class="sxs-lookup"><span data-stu-id="7288f-189">On hello **Time settings** page:</span></span>
   
   1. <span data-ttu-id="7288f-190">從 hello 下拉式清單中，選取 hello**時區**根據裝置正在部署中的 hello hello 地理位置。</span><span class="sxs-lookup"><span data-stu-id="7288f-190">From hello drop-down list, select hello **Time zone** based on hello geographic location in which hello device is being deployed.</span></span> <span data-ttu-id="7288f-191">hello 裝置的預設時區是太平洋標準時間。</span><span class="sxs-lookup"><span data-stu-id="7288f-191">hello default time zone for your device is PST.</span></span> <span data-ttu-id="7288f-192">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="7288f-192">Your device will use this time zone for all scheduled operations.</span></span>
   2. <span data-ttu-id="7288f-193">指定**主要 NTP 伺服器**為您的裝置，或接受 time.windows.com hello 預設值。請確定您的網路允許 NTP 流量 toopass 從您的資料中心 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="7288f-193">Specify a **Primary NTP server** for your device or accept hello default value of time.windows.com. Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span>
   3. <span data-ttu-id="7288f-194">(選擇性) 指定裝置的 [次要 NTP 伺服器]  。</span><span class="sxs-lookup"><span data-stu-id="7288f-194">Optionally specify a **Secondary NTP server** for your device.</span></span>
   4. <span data-ttu-id="7288f-195">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-195">Click **Apply**.</span></span> <span data-ttu-id="7288f-196">這將會驗證並套用設定的 hello 時間設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-196">This will validate and apply hello configured time settings.</span></span>
9. <span data-ttu-id="7288f-197">設定您的裝置 hello 雲端設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-197">Configure hello cloud settings for your device.</span></span> <span data-ttu-id="7288f-198">在此步驟中，您將完成 hello 本機裝置設定，並再將 hello 裝置註冊 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="7288f-198">In this step, you will complete hello local device configuration and then register hello device with your StorSimple Device Manager service.</span></span>
   
   1. <span data-ttu-id="7288f-199">輸入 hello**服務註冊金鑰**您取得**步驟 2： 取得 hello 服務註冊金鑰**中[部署 StorSimple Virtual Array-準備 hello 入口網站](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)。</span><span class="sxs-lookup"><span data-stu-id="7288f-199">Enter hello **Service registration key** that you got in **Step 2: Get hello service registration key** in [Deploy StorSimple Virtual Array - Prepare hello Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).</span></span>
   2. <span data-ttu-id="7288f-200">如果這不是您要向此服務的 hello 第一個裝置，您將需要 tooprovide hello**服務資料加密金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7288f-200">If this is not hello first device that you are registering with this service, you will need tooprovide hello **Service data encryption key**.</span></span> <span data-ttu-id="7288f-201">與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple 裝置管理員服務需要此金鑰。</span><span class="sxs-lookup"><span data-stu-id="7288f-201">This key is required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="7288f-202">如需詳細資訊，請參閱太[Get hello 服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)您的本機 web UI。</span><span class="sxs-lookup"><span data-stu-id="7288f-202">For more information, refer too[Get hello service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) on your local web UI.</span></span>
   3. <span data-ttu-id="7288f-203">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-203">Click **Register**.</span></span> <span data-ttu-id="7288f-204">這會重新啟動裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="7288f-204">This will restart hello device.</span></span> <span data-ttu-id="7288f-205">您可能需要 toowait 2-3 分鐘，hello 裝置註冊成功。</span><span class="sxs-lookup"><span data-stu-id="7288f-205">You may need toowait for 2-3 minutes before hello device is successfully registered.</span></span> <span data-ttu-id="7288f-206">Hello 裝置重新啟動之後，您將會進入 toohello 登在頁面中。</span><span class="sxs-lookup"><span data-stu-id="7288f-206">After hello device has restarted, you will be taken toohello sign in page.</span></span>
      
      ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. <span data-ttu-id="7288f-208">傳回 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7288f-208">Return toohello Azure portal.</span></span>
11. <span data-ttu-id="7288f-209">瀏覽 toohello**裝置**刀鋒視窗，您的服務。</span><span class="sxs-lookup"><span data-stu-id="7288f-209">Navigate toohello **Devices** blade of your service.</span></span> <span data-ttu-id="7288f-210">如果您有大量資源，請依序按一下 [所有資源]、您的服務名稱 (如有必要，請搜尋) 及 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="7288f-210">If you have a lot of resources, click **All resources**, click your service name (search for it if necessary), and then click **Devices**.</span></span>
12. <span data-ttu-id="7288f-211">在 hello**裝置**刀鋒視窗中，確認該 hello 裝置已成功透過查閱 hello 狀態連線 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="7288f-211">On hello **Devices** blade, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="7288f-212">hello 裝置狀態應為**已 tooset 準備註冊**。</span><span class="sxs-lookup"><span data-stu-id="7288f-212">hello device status should be **Ready tooset up**.</span></span>
    
    ![註冊裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a><span data-ttu-id="7288f-214">步驟 2： 設定 iSCSI 伺服器 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="7288f-214">Step 2: Configure hello device as iSCSI server</span></span>

<span data-ttu-id="7288f-215">執行 hello hello Azure 入口網站 toocomplete hello 所需裝置設定中所述步驟。</span><span class="sxs-lookup"><span data-stu-id="7288f-215">Perform hello following steps in hello Azure portal toocomplete hello required device setup.</span></span>

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a><span data-ttu-id="7288f-216">為 iSCSI 伺服器 tooconfigure hello 裝置</span><span class="sxs-lookup"><span data-stu-id="7288f-216">tooconfigure hello device as iSCSI server</span></span>

1. <span data-ttu-id="7288f-217">移 tooyour StorSimple 裝置管理員服務，然後檢閱 太**管理 > 裝置**。</span><span class="sxs-lookup"><span data-stu-id="7288f-217">Go tooyour StorSimple Device Manager service and then go too**Management > Devices**.</span></span> <span data-ttu-id="7288f-218">在 hello**裝置**刀鋒視窗中，選取 hello 您剛才建立的裝置。</span><span class="sxs-lookup"><span data-stu-id="7288f-218">In hello **Devices** blade, select hello device you just created.</span></span> <span data-ttu-id="7288f-219">此裝置會顯示為**已 tooset 準備註冊**。</span><span class="sxs-lookup"><span data-stu-id="7288f-219">This device would show up as **Ready tooset up**.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. <span data-ttu-id="7288f-221">按一下 hello 裝置，您會看到指出該 hello 裝置準備好 toosetup 橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="7288f-221">Click hello device and you will see a banner message indicating that hello device is ready toosetup.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. <span data-ttu-id="7288f-223">按一下**設定**hello 裝置命令列上。</span><span class="sxs-lookup"><span data-stu-id="7288f-223">Click **Configure** on hello device command bar.</span></span> <span data-ttu-id="7288f-224">這會開啟 hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7288f-224">This opens up hello **Configure** blade.</span></span> <span data-ttu-id="7288f-225">在 hello**設定**刀鋒視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7288f-225">In hello **Configure** blade, do hello following:</span></span>
   
   * <span data-ttu-id="7288f-226">自動填入 hello iSCSI 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="7288f-226">hello iSCSI server name is automatically populated.</span></span>
   * <span data-ttu-id="7288f-227">請確定 hello 雲端儲存體加密設定得**啟用**。</span><span class="sxs-lookup"><span data-stu-id="7288f-227">Make sure hello cloud storage encryption is set too**Enabled**.</span></span> <span data-ttu-id="7288f-228">這可確保傳送 hello 裝置 toohello 雲端中的 hello 資料已加密。</span><span class="sxs-lookup"><span data-stu-id="7288f-228">This ensures that hello data sent from hello device toohello cloud is encrypted.</span></span>
   * <span data-ttu-id="7288f-229">指定 32 個字元的加密金鑰，並將它記錄在金鑰管理應用程式中，供日後參考。</span><span class="sxs-lookup"><span data-stu-id="7288f-229">Specify a 32-character encryption key and record it in a key management app for future reference.</span></span>
   * <span data-ttu-id="7288f-230">選取儲存體帳戶 toobe 搭配您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7288f-230">Select a storage account toobe used with your device.</span></span> <span data-ttu-id="7288f-231">在此訂用帳戶，您可以選取現有的儲存體帳戶，或者您可以按一下**新增**toochoose 從不同的訂用帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7288f-231">In this subscription, you can select an existing storage account, or you can click **Add** toochoose an account from a different subscription.</span></span>
     
     ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. <span data-ttu-id="7288f-233">按一下**設定**toocomplete hello iSCSI 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="7288f-233">Click **Configure** toocomplete setting up hello iSCSI server.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. <span data-ttu-id="7288f-235">將會通知您建立 hello iSCSI 伺服器正在進行中。</span><span class="sxs-lookup"><span data-stu-id="7288f-235">You will be notified that hello iSCSI server creation is in progress.</span></span> <span data-ttu-id="7288f-236">已成功建立 hello iSCSI 伺服器之後，hello**裝置**刀鋒視窗會更新，而且 hello 對應的裝置狀態**線上**。</span><span class="sxs-lookup"><span data-stu-id="7288f-236">After hello iSCSI server is successfully created, hello **Devices** blade is updated and hello corresponding device status is **Online**.</span></span>
   
    ![將裝置設定為 iSCSI 伺服器](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a><span data-ttu-id="7288f-238">步驟 3：新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="7288f-238">Step 3: Add a volume</span></span>

1. <span data-ttu-id="7288f-239">在 hello**裝置**刀鋒視窗中，選取 hello 裝置您剛才設定 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7288f-239">In hello **Devices** blade, select hello device you just configured as an iSCSI server.</span></span> <span data-ttu-id="7288f-240">按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**新增磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="7288f-240">Click **...** (alternatively right-click in this row) and from hello context menu, select **Add volume**.</span></span> <span data-ttu-id="7288f-241">您也可以按一下**新增磁碟區 +** hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="7288f-241">You can also click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="7288f-242">這會開啟 hello**新增磁碟區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7288f-242">This opens up hello **Add volume** blade.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. <span data-ttu-id="7288f-244">在 hello**新增磁碟區**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="7288f-244">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="7288f-245">在 hello**磁碟區名稱**欄位中，輸入您的磁碟區的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="7288f-245">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="7288f-246">hello 名稱必須是包含 3 too127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="7288f-246">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="7288f-247">在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7288f-247">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="7288f-248">對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="7288f-248">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned** **volume**.</span></span> <span data-ttu-id="7288f-249">針對所有其他資料，請選取 [階層式磁碟區]**磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="7288f-249">For all other data, select **Tiered** **volume**.</span></span>
   * <span data-ttu-id="7288f-250">在 hello**容量**欄位中，指定 hello hello 磁碟區的大小。</span><span class="sxs-lookup"><span data-stu-id="7288f-250">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="7288f-251">階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。</span><span class="sxs-lookup"><span data-stu-id="7288f-251">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
     
     <span data-ttu-id="7288f-252">本機固定磁碟區以佈建，並確保 hello hello 磁碟區中的主要資料將會存留在 hello 裝置並不 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="7288f-252">A locally pinned volume is thickly provisioned and ensures that hello primary data in hello volume stays on hello device and does not spill toohello cloud.</span></span>
     
     <span data-ttu-id="7288f-253">為分層磁碟區上 hello 另一方面在精簡佈建。</span><span class="sxs-lookup"><span data-stu-id="7288f-253">A tiered volume on hello other hand is thinly provisioned.</span></span> <span data-ttu-id="7288f-254">當您建立階層式磁碟區時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。</span><span class="sxs-lookup"><span data-stu-id="7288f-254">When you create a tiered volume, approximately 10% of hello space is provisioned on hello local tier and 90% of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="7288f-255">例如，如果您佈建 1 TB 磁碟區、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="7288f-255">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="7288f-256">這又表示的是，如果您用完所有 hello 的本機空間 hello 在裝置上，您無法佈建階層式的共用 （因為 hello 10%將無法使用）。</span><span class="sxs-lookup"><span data-stu-id="7288f-256">This in turn implies is that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10% will not be available).</span></span>
     
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * <span data-ttu-id="7288f-258">按一下**連線主機**，選取 存取控制記錄 (ACR) 對應 toohello iSCSI 啟動器您想 tooconnect toothis 磁碟區，然後再按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="7288f-258">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span> <br><br> 
3. <span data-ttu-id="7288f-259">tooadd 新連線的主機，按一下**新增**，輸入的名稱 hello 主機和其 iSCSI 合格名稱 (IQN)，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="7288f-259">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span> <span data-ttu-id="7288f-260">如果您沒有 hello IQN，請移至太[附錄 a： 取得 hello Windows Server 主機的 IQN](#appendix-a-get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="7288f-260">If you don't have hello IQN, go too[Appendix A: Get hello IQN of a Windows Server host](#appendix-a-get-the-iqn-of-a-windows-server-host).</span></span>
   
      ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. <span data-ttu-id="7288f-262">磁碟區設定完成之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7288f-262">When you're finished configuring your volume, click **OK**.</span></span> <span data-ttu-id="7288f-263">將指定的 hello 與建立磁碟區設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="7288f-263">A volume will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="7288f-264">根據預設，監視和備份將被啟用 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7288f-264">By default, monitoring and backup will be enabled for hello volume.</span></span>
   
     ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. <span data-ttu-id="7288f-266">hello 磁碟區的 tooconfirm 已成功建立，請移 toohello**磁碟區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7288f-266">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="7288f-267">您應該會看到列出的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7288f-267">You should see hello volume listed.</span></span>
   
   ![新增磁碟區](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a><span data-ttu-id="7288f-269">步驟 4：掛接、初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="7288f-269">Step 4: Mount, initialize, and format a volume</span></span>

<span data-ttu-id="7288f-270">執行 hello 下列步驟 toomount 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。</span><span class="sxs-lookup"><span data-stu-id="7288f-270">Perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

#### <a name="toomount-initialize-and-format-a-volume"></a><span data-ttu-id="7288f-271">toomount、 初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="7288f-271">toomount, initialize, and format a volume</span></span>

1. <span data-ttu-id="7288f-272">開啟 hello **iSCSI 啟動器**hello 適當伺服器上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7288f-272">Open hello **iSCSI initiator** app on hello appropriate server.</span></span>
2. <span data-ttu-id="7288f-273">在 hello **iSCSI 啟動器屬性**視窗的 hello**探索**索引標籤上，按一下 **探索入口網站**。</span><span class="sxs-lookup"><span data-stu-id="7288f-273">In hello **iSCSI Initiator Properties** window, on hello **Discovery** tab, click **Discover Portal**.</span></span>
   
    ![探索入口網站](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. <span data-ttu-id="7288f-275">在 hello**探索目標入口網站**對話方塊中，提供啟用 iSCSI 的網路介面，hello IP 位址，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7288f-275">In hello **Discover Target Portal** dialog box, supply hello IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span>
   
    ![IP 位址](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. <span data-ttu-id="7288f-277">在 hello **iSCSI 啟動器屬性**視窗的 hello**目標**索引標籤上，找出 hello**探索目標**。</span><span class="sxs-lookup"><span data-stu-id="7288f-277">In hello **iSCSI Initiator Properties** window, on hello **Targets** tab, locate hello **Discovered targets**.</span></span> <span data-ttu-id="7288f-278">（每個磁碟區將是已探索到的目標）。hello 裝置狀態應顯示為**Inactive**。</span><span class="sxs-lookup"><span data-stu-id="7288f-278">(Each volume will be a discovered target.) hello device status should appear as **Inactive**.</span></span>
   
    ![探索到的目標](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. <span data-ttu-id="7288f-280">選取目標裝置，然後按一下連接。</span><span class="sxs-lookup"><span data-stu-id="7288f-280">Select a target device and then click **Connect**.</span></span> <span data-ttu-id="7288f-281">Hello 裝置連線之後，應該也變更 hello 狀態**Connected**。</span><span class="sxs-lookup"><span data-stu-id="7288f-281">After hello device is connected, hello status should change too**Connected**.</span></span> <span data-ttu-id="7288f-282">(如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請參閱[安裝和設定 Microsoft iSCSI 啟動器][1]。</span><span class="sxs-lookup"><span data-stu-id="7288f-282">(For more information about using hello Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
   
    ![選取目標裝置](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. <span data-ttu-id="7288f-284">在 Windows 主機上，按 hello Windows 爦羆坫 + X、，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="7288f-284">On your Windows host, press hello Windows Logo key + X, and then click **Run**.</span></span>
7. <span data-ttu-id="7288f-285">在 [hello**執行**] 對話方塊中，輸入**Diskmgmt.msc**。</span><span class="sxs-lookup"><span data-stu-id="7288f-285">In hello **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="7288f-286">按一下**確定**，和 hello**磁碟管理**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7288f-286">Click **OK**, and hello **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="7288f-287">hello 右窗格會顯示 hello 磁碟區在主機上。</span><span class="sxs-lookup"><span data-stu-id="7288f-287">hello right pane will show hello volumes on your host.</span></span>
8. <span data-ttu-id="7288f-288">在 hello**磁碟管理**，hello 掛接的磁碟區將會出現視窗 hello 下列圖例所示。</span><span class="sxs-lookup"><span data-stu-id="7288f-288">In hello **Disk Management** window, hello mounted volumes will appear as shown in hello following illustration.</span></span> <span data-ttu-id="7288f-289">以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。</span><span class="sxs-lookup"><span data-stu-id="7288f-289">Right-click hello discovered volume (click hello disk name), and then click **Online**.</span></span>
   
    ![磁碟管理](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. <span data-ttu-id="7288f-291">按一下滑鼠右鍵，然後選取 [初始化磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-291">Right-click and select **Initialize Disk**.</span></span>
   
    ![初始化磁碟 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. <span data-ttu-id="7288f-293">在 [hello] 對話方塊中，選取 hello 磁碟 tooinitialize，然後**確定**。</span><span class="sxs-lookup"><span data-stu-id="7288f-293">In hello dialog box, select hello disk(s) tooinitialize, and then click **OK**.</span></span>
    
    ![初始化磁碟 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. <span data-ttu-id="7288f-295">hello 新增簡單磁碟區精靈 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="7288f-295">hello New Simple Volume wizard starts.</span></span> <span data-ttu-id="7288f-296">請選取磁碟大小，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-296">Select a disk size, and then click **Next**.</span></span>
    
    ![新增磁碟區精靈 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. <span data-ttu-id="7288f-298">指派磁碟機代號 toohello 磁碟區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="7288f-298">Assign a drive letter toohello volume, and then click **Next**.</span></span>
    
    ![新增磁碟區精靈 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. <span data-ttu-id="7288f-300">輸入 hello 參數 tooformat hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7288f-300">Enter hello parameters tooformat hello volume.</span></span> <span data-ttu-id="7288f-301">**Windows Server 只支援 NTFS。**</span><span class="sxs-lookup"><span data-stu-id="7288f-301">**On Windows Server, only NTFS is supported.**</span></span> <span data-ttu-id="7288f-302">設定 hello 配置單位大小 too64K。</span><span class="sxs-lookup"><span data-stu-id="7288f-302">Set hello allocation unit size too64K.</span></span> <span data-ttu-id="7288f-303">並提供您磁碟區的標籤。</span><span class="sxs-lookup"><span data-stu-id="7288f-303">Provide a label for your volume.</span></span> <span data-ttu-id="7288f-304">它是建議的最佳作法，您在您的 StorSimple Virtual Array 提供此名稱 toobe 相同 toohello 磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="7288f-304">It is a recommended best practice for this name toobe identical toohello volume name you provided on your StorSimple Virtual Array.</span></span> <span data-ttu-id="7288f-305">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="7288f-305">Click **Next**.</span></span>
    
    ![新增磁碟區精靈 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. <span data-ttu-id="7288f-307">請檢查您的磁碟區的 hello 值，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="7288f-307">Check hello values for your volume, and then click **Finish**.</span></span>
    
    ![新增磁碟區精靈 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    <span data-ttu-id="7288f-309">hello 磁碟區將會顯示為**線上**上 hello**磁碟管理**頁面。</span><span class="sxs-lookup"><span data-stu-id="7288f-309">hello volumes will appear as **Online** on hello **Disk Management** page.</span></span>
    
    ![磁碟區線上](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a><span data-ttu-id="7288f-311">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7288f-311">Next steps</span></span>

<span data-ttu-id="7288f-312">了解如何 toouse hello 本機 web UI 太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="7288f-312">Learn how toouse hello local web UI too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="7288f-313">附錄 a: Get hello Windows Server 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="7288f-313">Appendix A: Get hello IQN of a Windows Server host</span></span>

<span data-ttu-id="7288f-314">執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server 2012 的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="7288f-314">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server 2012.</span></span>

#### <a name="tooget-hello-iqn-of-a-windows-host"></a><span data-ttu-id="7288f-315">tooget hello Windows 主機的 IQN</span><span class="sxs-lookup"><span data-stu-id="7288f-315">tooget hello IQN of a Windows host</span></span>

1. <span data-ttu-id="7288f-316">在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="7288f-316">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
2. <span data-ttu-id="7288f-317">在 hello **iSCSI 啟動器屬性**視窗的 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="7288f-317">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   
    ![iSCSI 啟動器屬性](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. <span data-ttu-id="7288f-319">儲存這個字串。</span><span class="sxs-lookup"><span data-stu-id="7288f-319">Save this string.</span></span>

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



