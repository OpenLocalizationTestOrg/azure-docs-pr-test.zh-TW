---
title: "遠端連線至 StorSimple 裝置 | Microsoft Docs"
description: "說明如何設定您的裝置以進行遠端管理，以及如何透過 HTTP 或 HTTPS 連線到 Windows PowerShell for StorSimple。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="6da58-103">遠端連線至 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="6da58-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="6da58-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6da58-104">Overview</span></span>

<span data-ttu-id="6da58-105">您可以透過 Windows PowerShell，從遠端連線到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="6da58-106">當您以這種方式連線時，不會看到功能表。</span><span class="sxs-lookup"><span data-stu-id="6da58-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="6da58-107">(只有當您使用裝置上的序列主控台進行連線時，才會看到功能表)。使用 Windows PowerShell 遠端連線到特定的 Runspace。</span><span class="sxs-lookup"><span data-stu-id="6da58-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="6da58-108">您也可以指定顯示語言。</span><span class="sxs-lookup"><span data-stu-id="6da58-108">You can also specify the display language.</span></span>

<span data-ttu-id="6da58-109">如需有關如何使用 Windows PowerShell 遠端來管理裝置的詳細資訊，請移至 [使用 Windows PowerShell for StorSimple 管理您的 StorSimple 裝置](storsimple-8000-windows-powershell-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="6da58-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="6da58-110">本教學課程說明如何設定您的裝置以進行遠端管理，以及如何連線到 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="6da58-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="6da58-111">您可以透過 Windows PowerShell 使用 HTTP 或 HTTPS 從遠端連線。</span><span class="sxs-lookup"><span data-stu-id="6da58-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="6da58-112">不過，當您決定如何連線到適用於 StorSimple 的 Windows PowerShell 時，請考慮下列資訊：</span><span class="sxs-lookup"><span data-stu-id="6da58-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="6da58-113">直接連線至裝置序列主控台是安全的，但透過網路交換器連線至序列主控台則否。</span><span class="sxs-lookup"><span data-stu-id="6da58-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="6da58-114">透過網路交換器連線至裝置序列主控台時，請務必注意安全性風險。</span><span class="sxs-lookup"><span data-stu-id="6da58-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="6da58-115">透過 HTTP 工作階段連線的安全性，比在網路上透過序列主控台連線更高。</span><span class="sxs-lookup"><span data-stu-id="6da58-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="6da58-116">雖然這不是最安全的方法，但在受信任的網路上是可接受的做法。</span><span class="sxs-lookup"><span data-stu-id="6da58-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="6da58-117">透過 HTTP 工作階段連線並使用自我簽署憑證，是最安全且建議的選項。</span><span class="sxs-lookup"><span data-stu-id="6da58-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="6da58-118">您可以從遠端連線至 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="6da58-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="6da58-119">不過，透過 Windows PowerShell 介面遠端存取您的 StorSimple 裝置依預設不會啟用。</span><span class="sxs-lookup"><span data-stu-id="6da58-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="6da58-120">您必須先在裝置上啟用遠端管理，然後在要用來存取裝置的用戶端上啟用。</span><span class="sxs-lookup"><span data-stu-id="6da58-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="6da58-121">本文章中所述的步驟是在執行 Windows Server 2012 R2 的主機系統上執行。</span><span class="sxs-lookup"><span data-stu-id="6da58-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="6da58-122">透過 HTTP 連線</span><span class="sxs-lookup"><span data-stu-id="6da58-122">Connect through HTTP</span></span>

<span data-ttu-id="6da58-123">透過 HTTP 工作階段連線至 Windows PowerShell for StorSimple 的安全性，比透過 StorSimple 裝置的序列主控台連線更高。</span><span class="sxs-lookup"><span data-stu-id="6da58-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="6da58-124">雖然這不是最安全的方法，但在受信任的網路上是可接受的做法。</span><span class="sxs-lookup"><span data-stu-id="6da58-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="6da58-125">您可以使用 Azure 入口網站或序列主控台來設定遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="6da58-126">選擇下列程序之一：</span><span class="sxs-lookup"><span data-stu-id="6da58-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="6da58-127">使用 Azure 入口網站來啟用透過 HTTP 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="6da58-128">使用序列主控台啟用透過 HTTP 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="6da58-129">啟用遠端管理後，使用下列程序準備遠端連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="6da58-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="6da58-130">準備遠端連線的用戶端</span><span class="sxs-lookup"><span data-stu-id="6da58-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="6da58-131">使用 Azure 入口網站來啟用透過 HTTP 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="6da58-132">在 Azure 入口網站中執行下列步驟以啟用透過 HTTP 的遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="6da58-133">透過 Azure 入口網站啟用遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="6da58-134">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="6da58-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6da58-135">選取 [裝置]，然後選取並按一下您想要設定遠端管理的裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="6da58-136">移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="6da58-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="6da58-137">在 [安全性設定] 刀鋒視窗中，按一下 [遠端管理]。</span><span class="sxs-lookup"><span data-stu-id="6da58-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6da58-138">在 [遠端管理] 刀鋒視窗中，將 [啟用遠端管理] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6da58-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="6da58-139">您現在可以選擇使用 HTTP 來連接。</span><span class="sxs-lookup"><span data-stu-id="6da58-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="6da58-140">(預設是透過 HTTPS 來連線。)請確定已選取 HTTP。</span><span class="sxs-lookup"><span data-stu-id="6da58-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6da58-141">只有受信任的網路上才接受透過 HTTP 來連接。</span><span class="sxs-lookup"><span data-stu-id="6da58-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="6da58-142">按一下 [儲存]，系統提示您進行確認時，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="6da58-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="6da58-143">使用序列主控台啟用透過 HTTP 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="6da58-144">在裝置的序列主控台上執行下列步驟以啟用遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="6da58-145">使用裝置序列主控台啟用遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="6da58-146">在序列主控台的功能表中，選取選項 1。</span><span class="sxs-lookup"><span data-stu-id="6da58-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="6da58-147">如需有關如何使用裝置序列主控台的詳細資訊，請移至[透過裝置序列主控台連線到 Windows PowerShell for StorSimple](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="6da58-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6da58-148">在出現提示時輸入： `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="6da58-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="6da58-149">您會看到使用 HTTP 來連線至裝置的安全性漏洞的相關通知。</span><span class="sxs-lookup"><span data-stu-id="6da58-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="6da58-150">出現提示時，輸入 **Y**確認。</span><span class="sxs-lookup"><span data-stu-id="6da58-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="6da58-151">確認 HTTP 已啟用，做法是輸入: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="6da58-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="6da58-152">確認 [RemoteManagementMode] 欄位顯示 **HttpsAndHttpEnabled**。下圖顯示 PuTTY 中的這些設定。</span><span class="sxs-lookup"><span data-stu-id="6da58-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![序列 HTTPS 和 HTTP 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="6da58-154">準備遠端連線的用戶端</span><span class="sxs-lookup"><span data-stu-id="6da58-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="6da58-155">在用戶端上執行下列步驟以啟用遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="6da58-156">準備遠端連線的用戶端</span><span class="sxs-lookup"><span data-stu-id="6da58-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="6da58-157">以系統管理員的身分開啟 Windows PowerShell工作階段。</span><span class="sxs-lookup"><span data-stu-id="6da58-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6da58-158">輸入下列命令將 StorSimple 裝置的 IP 位址加入用戶端的信任的主機清單：</span><span class="sxs-lookup"><span data-stu-id="6da58-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="6da58-159">以您的裝置的 IP 位址取代其中的 <device_ip>，例如：</span><span class="sxs-lookup"><span data-stu-id="6da58-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6da58-160">輸入下列命令將裝置認證儲存在變數中：</span><span class="sxs-lookup"><span data-stu-id="6da58-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="6da58-161">在出現的對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="6da58-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="6da58-162">以此格式輸入使用者名稱：device_ip\SSAdmin。</span><span class="sxs-lookup"><span data-stu-id="6da58-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="6da58-163">輸入以安裝精靈設定裝置時設定的裝置管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="6da58-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="6da58-164">預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="6da58-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="6da58-165">輸入以下命令在裝置上啟動 Windows PowerShell 工作階段：</span><span class="sxs-lookup"><span data-stu-id="6da58-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="6da58-166">若要建立與 StorSimple 虛擬裝置搭配使用的 Windows PowerShell 工作階段，請附加 `–Port` 參數，並指定您在 StorSimple 虛擬設備遠端處理中設定的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="6da58-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="6da58-167">此時，您應該有個連線到裝置的使用中遠端 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6da58-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![使用 HTTPS 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="6da58-169">透過 HTTP 連線</span><span class="sxs-lookup"><span data-stu-id="6da58-169">Connect through HTTPS</span></span>

<span data-ttu-id="6da58-170">透過 HTTPS 工作階段連線到 Windows PowerShell for StorSimple，是從遠端連線至 Microsoft Azure StorSimple 裝置最安全且建議的方法。</span><span class="sxs-lookup"><span data-stu-id="6da58-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="6da58-171">下列程序說明如何設定序列主控台和用戶端電腦，讓您可以使用 HTTPS 連線到 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="6da58-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="6da58-172">您可以使用 Azure 入口網站或序列主控台來設定遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="6da58-173">選擇下列程序之一：</span><span class="sxs-lookup"><span data-stu-id="6da58-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="6da58-174">使用 Azure 入口網站來啟用透過 HTTPS 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="6da58-175">使用序列主控台啟用透過 HTTPS 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="6da58-176">啟用遠端管理後，使用下列程序準備遠端管理的主機，並從該遠端主機連線至裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="6da58-177">準備遠端管理的主機</span><span class="sxs-lookup"><span data-stu-id="6da58-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="6da58-178">從遠端主機連線至裝置</span><span class="sxs-lookup"><span data-stu-id="6da58-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="6da58-179">使用 Azure 入口網站來啟用透過 HTTPS 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="6da58-180">在 Azure 入口網站中執行下列步驟以啟用透過 HTTPS 的遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="6da58-181">從 Azure 入口網站來啟用透過 HTTPS 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="6da58-182">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="6da58-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6da58-183">選取 [裝置]，然後選取並按一下您想要設定遠端管理的裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="6da58-184">移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="6da58-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="6da58-185">在 [安全性設定] 刀鋒視窗中，按一下 [遠端管理]。</span><span class="sxs-lookup"><span data-stu-id="6da58-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6da58-186">將 [啟用遠端管理] 設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="6da58-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="6da58-187">您現在可以選擇使用 HTTPS 來連線。</span><span class="sxs-lookup"><span data-stu-id="6da58-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="6da58-188">(預設是透過 HTTPS 來連線。)請確定已選取 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="6da58-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="6da58-189">按一下 [...]，然後按一下 [下載遠端管理憑證]。</span><span class="sxs-lookup"><span data-stu-id="6da58-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="6da58-190">指定要儲存此檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6da58-190">Specify a location to save this file.</span></span> <span data-ttu-id="6da58-191">您必須將此憑證安裝在將用來連線到裝置的用戶端或主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="6da58-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="6da58-192">按一下 [儲存]，系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="6da58-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="6da58-193">使用序列主控台啟用透過 HTTPS 的遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="6da58-194">在裝置的序列主控台上執行下列步驟以啟用遠端管理。</span><span class="sxs-lookup"><span data-stu-id="6da58-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="6da58-195">使用裝置序列主控台啟用遠端管理</span><span class="sxs-lookup"><span data-stu-id="6da58-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="6da58-196">在序列主控台的功能表中，選取選項 1。</span><span class="sxs-lookup"><span data-stu-id="6da58-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="6da58-197">如需有關如何使用裝置序列主控台的詳細資訊，請移至[透過裝置序列主控台連線到 Windows PowerShell for StorSimple](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="6da58-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6da58-198">在出現提示時輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="6da58-199">這應該會在您的裝置上啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="6da58-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="6da58-200">確認 HTTPS 已啟用，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="6da58-201">確定 [RemoteManagementMode] 欄位顯示 **HttpsEnabled**。下圖顯示 PuTTY 中的這些設定。</span><span class="sxs-lookup"><span data-stu-id="6da58-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![序列 HTTPS 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="6da58-203">從 `Get-HcsSystem`的輸出，複製裝置的序號，並儲存供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="6da58-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6da58-204">序號對應至憑證中的 CN 名稱。</span><span class="sxs-lookup"><span data-stu-id="6da58-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="6da58-205">取得遠端管理憑證，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="6da58-206">將出現類似以下的憑證。</span><span class="sxs-lookup"><span data-stu-id="6da58-206">A certificate similar to the following will appear.</span></span>
   
    ![取得遠端管理憑證](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="6da58-208">複製憑證中從 **-----BEGIN CERTIFICATE-----** 到 **-----END CERTIFICATE-----** 的資訊到文字編輯器，如 [記事本]，然後將它儲存為 .cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="6da58-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="6da58-209">(在您準備主機時，要將這個檔案複製到您的遠端主機)。</span><span class="sxs-lookup"><span data-stu-id="6da58-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6da58-210">若要產生新的憑證，使用 `Set-HcsRemoteManagementCert` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6da58-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="6da58-211">準備遠端管理的主機</span><span class="sxs-lookup"><span data-stu-id="6da58-211">Prepare the host for remote management</span></span>

<span data-ttu-id="6da58-212">若要準備使用 HTTPS 工作階段進行遠端連線的主機電腦，請執行下列程序：</span><span class="sxs-lookup"><span data-stu-id="6da58-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="6da58-213">[將 .cer 檔案匯入至用戶端或遠端主機的根存放區](#to-import-the-certificate-on-the-remote-host)。</span><span class="sxs-lookup"><span data-stu-id="6da58-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="6da58-214">[將裝置序號新增至遠端主機上的主機檔案](#to-add-device-serial-numbers-to-the-remote-host)。</span><span class="sxs-lookup"><span data-stu-id="6da58-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="6da58-215">以下說明上述各程序。</span><span class="sxs-lookup"><span data-stu-id="6da58-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="6da58-216">匯入遠端主機上的憑證</span><span class="sxs-lookup"><span data-stu-id="6da58-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="6da58-217">以滑鼠右鍵按一下.cer 檔案，選取 [ **安裝憑證**]。</span><span class="sxs-lookup"><span data-stu-id="6da58-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="6da58-218">這會啟動 [憑證匯入精靈]。</span><span class="sxs-lookup"><span data-stu-id="6da58-218">This starts the Certificate Import Wizard.</span></span>
   
    ![憑證匯入精靈 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="6da58-220">[存放區位置] 請選取 [本機電腦]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6da58-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="6da58-221">選取 [將所有憑證放入以下的存放區]，然後按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="6da58-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="6da58-222">導覽至遠端主機的根存放區，然後按一下 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="6da58-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![憑證匯入精靈  2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="6da58-224">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="6da58-224">Click **Finish**.</span></span> <span data-ttu-id="6da58-225">會出現訊息告訴您匯入成功。</span><span class="sxs-lookup"><span data-stu-id="6da58-225">A message that tells you that the import was successful appears.</span></span>
   
    ![憑證匯入精靈  3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="6da58-227">將裝置序號新增至遠端主機</span><span class="sxs-lookup"><span data-stu-id="6da58-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="6da58-228">以管理員的身分啟動 [記事本]，然後開啟位於 \Windows\System32\Drivers\etc 的主機檔案。</span><span class="sxs-lookup"><span data-stu-id="6da58-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="6da58-229">將下列三個項目新增至主機檔案：**DATA 0 IP 位址**、**控制器 0 固定 IP 位址**、**控制器 1 固定 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="6da58-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="6da58-230">輸入您稍早儲存的裝置序號。</span><span class="sxs-lookup"><span data-stu-id="6da58-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="6da58-231">對應至 IP 位址，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="6da58-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="6da58-232">對於控制器 0 及控制器 1，在序號 (CN 名稱) 結尾後附加 **Controller0** 和 **Controller1**。</span><span class="sxs-lookup"><span data-stu-id="6da58-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![將 CN 名稱加入至主機檔案](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="6da58-234">儲存主機檔案。</span><span class="sxs-lookup"><span data-stu-id="6da58-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="6da58-235">從遠端主機連線至裝置</span><span class="sxs-lookup"><span data-stu-id="6da58-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="6da58-236">使用 Windows PowerShell 和 SSL從遠端主機或用戶端進入您的裝置上的 SSAdmin 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6da58-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="6da58-237">SSAdmin 工作階段會對應至裝置的[序列主控台](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)功能表中的選項 1。</span><span class="sxs-lookup"><span data-stu-id="6da58-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="6da58-238">從您要建立遠端 Windows PowerShell 連線的電腦上執行下列程序。</span><span class="sxs-lookup"><span data-stu-id="6da58-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="6da58-239">使用 Windows PowerShell 和 SSL進入 SSAdmin 工作階段</span><span class="sxs-lookup"><span data-stu-id="6da58-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="6da58-240">以系統管理員的身分開啟 Windows PowerShell工作階段。</span><span class="sxs-lookup"><span data-stu-id="6da58-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6da58-241">將裝置的 IP 位址新增至用戶端信任的主機，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="6da58-242">其中 <device_ip> 是您的裝置的 IP 位址，例如：</span><span class="sxs-lookup"><span data-stu-id="6da58-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6da58-243">若要建立新認證，請輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="6da58-244">其中 <目標裝置的 IP> 是您的裝置的 DATA 0 的 IP 位址，例如之前影像中的主機檔案的 **10.126.173.90**。</span><span class="sxs-lookup"><span data-stu-id="6da58-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="6da58-245">此外，提供您的裝置的管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="6da58-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="6da58-246">建立工作階段，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="6da58-247">請為 Cmdlet 中的 -ComputerName 參數提供 <目標裝置的序號>。</span><span class="sxs-lookup"><span data-stu-id="6da58-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="6da58-248">此序號已對應至您的遠端主機上主機檔案中 DATA 0 的 IP 位址，如下圖所示的 **SHX0991003G44MT** 。</span><span class="sxs-lookup"><span data-stu-id="6da58-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="6da58-249">輸入：</span><span class="sxs-lookup"><span data-stu-id="6da58-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="6da58-250">您必須等候幾分鐘，接著便會透過 SSL 經由 HTTPS 連線到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="6da58-251">您會看到訊息，指出您已連線到裝置。</span><span class="sxs-lookup"><span data-stu-id="6da58-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![使用 HTTPS 和 SSL 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="6da58-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6da58-253">Next steps</span></span>

* <span data-ttu-id="6da58-254">深入了解 [使用 Windows PowerShell 來管理您的 StorSimple 裝置](storsimple-8000-windows-powershell-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="6da58-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="6da58-255">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="6da58-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

