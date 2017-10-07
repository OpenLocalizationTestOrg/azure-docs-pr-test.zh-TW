---
title: "aaaConnect 遠端 tooyour StorSimple 裝置 |Microsoft 文件"
description: "說明如何 tooconfigure 進行遠端管理裝置以及如何 tooconnect tooWindows PowerShell for StorSimple 透過 HTTP 或 HTTPS。"
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
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="38d65-103">從遠端連線 tooyour StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="38d65-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="38d65-104">概觀</span><span class="sxs-lookup"><span data-stu-id="38d65-104">Overview</span></span>

<span data-ttu-id="38d65-105">您可以從遠端連接 tooyour 裝置透過 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="38d65-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="38d65-106">當您以這種方式連線時，不會看到功能表。</span><span class="sxs-lookup"><span data-stu-id="38d65-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="38d65-107">（您看到功能表只有當您使用 hello 序列主控台上 hello 裝置 tooconnect。）使用 Windows PowerShell 遠端功能，您可以連接 tooa 特定 runspace。</span><span class="sxs-lookup"><span data-stu-id="38d65-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="38d65-108">您也可以指定 hello 顯示語言。</span><span class="sxs-lookup"><span data-stu-id="38d65-108">You can also specify hello display language.</span></span>

<span data-ttu-id="38d65-109">如需有關如何使用 Windows PowerShell 遠端執行功能 toomanage 裝置的詳細資訊，請移至太[使用 Windows PowerShell for StorSimple tooadminister StorSimple 裝置](storsimple-8000-windows-powershell-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="38d65-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="38d65-110">本教學課程說明如何 tooconfigure 您的裝置進行遠端管理，然後如何 tooconnect tooWindows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="38d65-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="38d65-111">您可以使用 HTTP 或 HTTPS tooremotely 透過 Windows PowerShell 連線。</span><span class="sxs-lookup"><span data-stu-id="38d65-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="38d65-112">不過，當您在決定如何 tooconnect tooWindows PowerShell for StorSimple，請考量下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="38d65-113">直接連接 toohello 裝置序列主控台安全，但不是透過網路交換器連接 toohello 序列主控台。</span><span class="sxs-lookup"><span data-stu-id="38d65-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="38d65-114">請小心 hello 安全性風險的 toohello 裝置序列主控台連接的網路交換器上時。</span><span class="sxs-lookup"><span data-stu-id="38d65-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="38d65-115">透過 HTTP 工作階段連線，可能會提供更高的安全性，比起透過序列主控台的 hello hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="38d65-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="38d65-116">雖然這不是 hello 最安全的方法，它是受信任的網路接受。</span><span class="sxs-lookup"><span data-stu-id="38d65-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="38d65-117">透過使用自我簽署憑證的 HTTPS 工作階段連接是最安全的 hello 與 hello 建議的選項。</span><span class="sxs-lookup"><span data-stu-id="38d65-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="38d65-118">您可以從遠端連線 toohello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="38d65-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="38d65-119">不過，預設不會啟用透過 hello Windows PowerShell 介面的遠端存取 tooyour StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="38d65-120">您必須首先，啟用 hello 裝置上的啟用遠端管理，並接著在 hello 用戶端，其使用的 tooaccess 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="38d65-121">這篇文章中所述的 hello 步驟未執行 Windows Server 2012 R2 的主機系統上執行。</span><span class="sxs-lookup"><span data-stu-id="38d65-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="38d65-122">透過 HTTP 連線</span><span class="sxs-lookup"><span data-stu-id="38d65-122">Connect through HTTP</span></span>

<span data-ttu-id="38d65-123">透過 HTTP 工作階段已連線的 tooWindows PowerShell for StorSimple 提供更高的安全性，比起透過 hello StorSimple 裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="38d65-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="38d65-124">雖然這不是 hello 最安全的方法，它是受信任的網路接受。</span><span class="sxs-lookup"><span data-stu-id="38d65-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="38d65-125">您可以使用任一 hello Azure 入口網站或 hello 序列主控台 tooconfigure 遠端管理。</span><span class="sxs-lookup"><span data-stu-id="38d65-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="38d65-126">選取從下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="38d65-127">透過 HTTP 使用 hello Azure 入口網站 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="38d65-128">透過 HTTP 使用 hello 序列主控台 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="38d65-129">啟用遠端管理之後，使用下列程序的遠端連線 tooprepare hello 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="38d65-130">準備 hello 用戶端的遠端連線</span><span class="sxs-lookup"><span data-stu-id="38d65-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="38d65-131">透過 HTTP 使用 hello Azure 入口網站 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="38d65-132">執行下列步驟在 hello Azure 入口網站 tooenable 遠端管理透過 HTTP 的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="38d65-133">透過 Azure 入口網站 hello tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="38d65-134">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="38d65-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="38d65-135">選取**裝置**然後選取並按一下您想要遠端管理 tooconfigure hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="38d65-136">跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="38d65-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="38d65-137">在 hello**安全性設定**刀鋒視窗中，按一下 **遠端管理**。</span><span class="sxs-lookup"><span data-stu-id="38d65-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="38d65-138">在 hello**遠端管理**刀鋒視窗中，設定**啟用遠端管理**太**是**。</span><span class="sxs-lookup"><span data-stu-id="38d65-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="38d65-139">您現在可以選擇使用 HTTP tooconnect。</span><span class="sxs-lookup"><span data-stu-id="38d65-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="38d65-140">（hello 預設會為 tooconnect over HTTPS）。請確定已選取 HTTP。</span><span class="sxs-lookup"><span data-stu-id="38d65-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="38d65-141">只有受信任的網路上才接受透過 HTTP 來連接。</span><span class="sxs-lookup"><span data-stu-id="38d65-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="38d65-142">按一下 [儲存]，系統提示您進行確認時，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="38d65-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="38d65-143">透過 HTTP 使用 hello 序列主控台 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="38d65-144">執行下列步驟 hello 裝置序列主控台 tooenable 遠端管理的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="38d65-145">透過裝置序列主控台時，hello tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="38d65-146">在 hello 序列主控台功能表中，選取選項 1。</span><span class="sxs-lookup"><span data-stu-id="38d65-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="38d65-147">如需 hello 裝置上使用 hello 序列主控台的詳細資訊，請移太[tooWindows PowerShell for StorSimple 透過裝置序列主控台](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="38d65-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="38d65-148">在 hello 提示字元中，輸入：`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="38d65-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="38d65-149">Hello 安全性弱點，使用 HTTP tooconnect toohello 裝置的相關資訊，會通知您。</span><span class="sxs-lookup"><span data-stu-id="38d65-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="38d65-150">出現提示時，輸入 **Y**確認。</span><span class="sxs-lookup"><span data-stu-id="38d65-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="38d65-151">確認 HTTP 已啟用，做法是輸入: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="38d65-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="38d65-152">請確認該 hello **RemoteManagementMode**  欄位會顯示**HttpsAndHttpEnabled**.hello 下列圖例會在 PuTTY 中顯示這些設定。</span><span class="sxs-lookup"><span data-stu-id="38d65-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![序列 HTTPS 和 HTTP 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="38d65-154">準備 hello 用戶端的遠端連線</span><span class="sxs-lookup"><span data-stu-id="38d65-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="38d65-155">執行下列步驟在 hello 的用戶端 tooenable 遠端管理的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="38d65-156">tooprepare hello 用戶端的遠端連線</span><span class="sxs-lookup"><span data-stu-id="38d65-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="38d65-157">以系統管理員的身分開啟 Windows PowerShell工作階段。</span><span class="sxs-lookup"><span data-stu-id="38d65-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="38d65-158">輸入下列命令 tooadd hello 的 hello StorSimple 裝置 toohello 用戶端的信任的主機清單的 IP 位址的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="38d65-159">取代 <*device_ip*> hello IP 位址，為您的裝置; 例如：</span><span class="sxs-lookup"><span data-stu-id="38d65-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="38d65-160">輸入下列命令 toosave hello 裝置認證的變數中的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="38d65-161">在 [hello] 對話方塊中，會出現：</span><span class="sxs-lookup"><span data-stu-id="38d65-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="38d65-162">輸入 hello 的使用者名稱格式如下： *device_ip\SSAdmin*。</span><span class="sxs-lookup"><span data-stu-id="38d65-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="38d65-163">輸入 hello 裝置系統管理員密碼設定 hello 安裝精靈中的 hello 裝置時所設定。</span><span class="sxs-lookup"><span data-stu-id="38d65-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="38d65-164">hello 預設密碼為*Password1*。</span><span class="sxs-lookup"><span data-stu-id="38d65-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="38d65-165">啟動 Windows PowerShell 工作階段 hello 裝置上，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="38d65-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="38d65-166">hello StorSimple 虛擬裝置搭配使用的 Windows PowerShell 工作階段的 toocreate 附加 hello`–Port`參數並指定您要設定遠端處理中 StorSimple 虛擬應用裝置 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="38d65-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="38d65-167">此時，您應該有作用中遠端 Windows PowerShell 工作階段 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![使用 HTTPS 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="38d65-169">透過 HTTP 連線</span><span class="sxs-lookup"><span data-stu-id="38d65-169">Connect through HTTPS</span></span>

<span data-ttu-id="38d65-170">連接 tooWindows PowerShell for StorSimple，透過 HTTPS 工作階段是 hello 最安全且為建議的遠端連線 tooyour Microsoft Azure StorSimple 裝置的方法。</span><span class="sxs-lookup"><span data-stu-id="38d65-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="38d65-171">hello 下列程序說明如何設定 tooset hello 序列主控台及用戶端電腦以便您可以使用 HTTPS tooconnect tooWindows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="38d65-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="38d65-172">您可以使用任一 hello Azure 入口網站或 hello 序列主控台 tooconfigure 遠端管理。</span><span class="sxs-lookup"><span data-stu-id="38d65-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="38d65-173">選取從下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="38d65-174">使用透過 HTTPS 的 hello Azure 入口網站 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="38d65-175">使用透過 HTTPS 的 hello 序列主控台 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="38d65-176">啟用遠端管理之後，請使用下列程序 tooprepare hello 主機遠端管理的 hello，並從 hello 遠端主機連接 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="38d65-177">準備 hello 主機遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="38d65-178">從 hello 遠端主機連接 toohello 裝置</span><span class="sxs-lookup"><span data-stu-id="38d65-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="38d65-179">使用透過 HTTPS 的 hello Azure 入口網站 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="38d65-180">執行下列步驟在 hello Azure 入口網站 tooenable 遠端管理透過 HTTPS 的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="38d65-181">tooenable 從遠端管理透過 HTTPS hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="38d65-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="38d65-182">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="38d65-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="38d65-183">選取**裝置**然後選取並按一下您想要遠端管理 tooconfigure hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="38d65-184">跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="38d65-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="38d65-185">在 hello**安全性設定**刀鋒視窗中，按一下 **遠端管理**。</span><span class="sxs-lookup"><span data-stu-id="38d65-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="38d65-186">設定**啟用遠端管理**太**是**。</span><span class="sxs-lookup"><span data-stu-id="38d65-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="38d65-187">您現在可以選擇 tooconnect 使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="38d65-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="38d65-188">（hello 預設會為 tooconnect over HTTPS）。請確定已選取 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="38d65-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="38d65-189">按一下 ...，然後按一下下載遠端管理憑證。</span><span class="sxs-lookup"><span data-stu-id="38d65-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="38d65-190">指定位置 toosave 這個檔案。</span><span class="sxs-lookup"><span data-stu-id="38d65-190">Specify a location toosave this file.</span></span> <span data-ttu-id="38d65-191">您需要 tooinstall hello 用戶端或主機電腦上的，您將使用 tooconnect toohello 裝置此憑證。</span><span class="sxs-lookup"><span data-stu-id="38d65-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="38d65-192">按一下 [儲存]，系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="38d65-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="38d65-193">使用透過 HTTPS 的 hello 序列主控台 tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="38d65-194">執行下列步驟 hello 裝置序列主控台 tooenable 遠端管理的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="38d65-195">透過裝置序列主控台時，hello tooenable 遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="38d65-196">在 hello 序列主控台功能表中，選取選項 1。</span><span class="sxs-lookup"><span data-stu-id="38d65-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="38d65-197">如需 hello 裝置上使用 hello 序列主控台的詳細資訊，請移太[tooWindows PowerShell for StorSimple 透過裝置序列主控台](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="38d65-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="38d65-198">在 hello 提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="38d65-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="38d65-199">這應該會在您的裝置上啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="38d65-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="38d65-200">確認 HTTPS 已啟用，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="38d65-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="38d65-201">請確定該 hello **RemoteManagementMode**  欄位會顯示**HttpsEnabled**.hello 下列圖例會在 PuTTY 中顯示這些設定。</span><span class="sxs-lookup"><span data-stu-id="38d65-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![序列 HTTPS 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="38d65-203">從 hello 輸出`Get-HcsSystem`、 複製 hello 裝置 hello 序號，並將它儲存供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="38d65-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="38d65-204">hello 數列數字對應 toohello hello 憑證中的 CN 名稱。</span><span class="sxs-lookup"><span data-stu-id="38d65-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="38d65-205">取得遠端管理憑證，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="38d65-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="38d65-206">會出現類似 toohello 後的憑證。</span><span class="sxs-lookup"><span data-stu-id="38d65-206">A certificate similar toohello following will appear.</span></span>
   
    ![取得遠端管理憑證](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="38d65-208">從 hello 憑證中複製 hello 資訊**---BEGIN CERTIFICATE---**太**---憑證結尾---**到文字編輯器例如記事本，並將它儲存為.cer 檔案。</span><span class="sxs-lookup"><span data-stu-id="38d65-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="38d65-209">（您將可以複製此檔案 tooyour 遠端主機當您準備 hello 主機）。</span><span class="sxs-lookup"><span data-stu-id="38d65-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="38d65-210">toogenerate 新憑證時，使用 hello `Set-HcsRemoteManagementCert` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="38d65-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="38d65-211">準備 hello 主機遠端管理</span><span class="sxs-lookup"><span data-stu-id="38d65-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="38d65-212">tooprepare hello 主機電腦的遠端連線使用 HTTPS 工作階段，執行下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="38d65-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="38d65-213">[匯入 hello.cer 檔案的 hello 用戶端或遠端主機的 hello 根存放區](#to-import-the-certificate-on-the-remote-host)。</span><span class="sxs-lookup"><span data-stu-id="38d65-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="38d65-214">[Hello 裝置序號 toohello 主機將檔案加入您的遠端主機上](#to-add-device-serial-numbers-to-the-remote-host)。</span><span class="sxs-lookup"><span data-stu-id="38d65-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="38d65-215">每個 hello 前面程序，如下所述。</span><span class="sxs-lookup"><span data-stu-id="38d65-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="38d65-216">hello 遠端主機上的 tooimport hello 憑證</span><span class="sxs-lookup"><span data-stu-id="38d65-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="38d65-217">Hello.cer 檔案上按一下滑鼠右鍵，然後選取**安裝憑證**。</span><span class="sxs-lookup"><span data-stu-id="38d65-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="38d65-218">這樣會啟動 hello 憑證匯入精靈。</span><span class="sxs-lookup"><span data-stu-id="38d65-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![憑證匯入精靈 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="38d65-220">存放區位置 請選取 本機電腦，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="38d65-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="38d65-221">選取**將所有憑證都放入下列存放區的 hello**，然後按一下**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="38d65-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="38d65-222">巡覽至遠端主機，toohello 根存放區，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38d65-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![憑證匯入精靈  2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="38d65-224">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="38d65-224">Click **Finish**.</span></span> <span data-ttu-id="38d65-225">出現訊息，告訴您 hello 匯入成功。</span><span class="sxs-lookup"><span data-stu-id="38d65-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![憑證匯入精靈  3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="38d65-227">tooadd 裝置序號 toohello 遠端主機</span><span class="sxs-lookup"><span data-stu-id="38d65-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="38d65-228">身為管理員，啟動 [記事本]，然後開啟位於 \Windows\System32\Drivers\etc 的 hello 主機檔案。</span><span class="sxs-lookup"><span data-stu-id="38d65-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="38d65-229">新增下列三個項目 tooyour 主機檔 hello: **DATA 0 IP 位址**，**控制器 0 固定 IP 位址**，和**控制器 1 固定 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="38d65-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="38d65-230">輸入您稍早儲存的 hello 裝置序列值。</span><span class="sxs-lookup"><span data-stu-id="38d65-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="38d65-231">將這個 toohello IP 位址 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="38d65-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="38d65-232">針對控制器 0 及控制器 1，請附加**Controller0**和**Controller1**結尾 hello hello 序號 （CN 名稱）。</span><span class="sxs-lookup"><span data-stu-id="38d65-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![正在將 CN 名稱 toohosts 檔案](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="38d65-234">儲存 hello 主機檔案。</span><span class="sxs-lookup"><span data-stu-id="38d65-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="38d65-235">從 hello 遠端主機連接 toohello 裝置</span><span class="sxs-lookup"><span data-stu-id="38d65-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="38d65-236">使用 Windows PowerShell 及 SSL tooenter 從遠端主機或用戶端裝置上的 SSAdmin 工作階段。</span><span class="sxs-lookup"><span data-stu-id="38d65-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="38d65-237">hello SSAdmin 工作階段對應 toooption 1 在 hello[序列主控台](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)功能表上，您的裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="38d65-238">執行下列程序 hello 要從中 toomake hello 遠端 Windows PowerShell 連線的電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="38d65-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="38d65-239">使用 Windows PowerShell 及 SSL hello 裝置上的 SSAdmin 工作階段的 tooenter</span><span class="sxs-lookup"><span data-stu-id="38d65-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="38d65-240">以系統管理員的身分開啟 Windows PowerShell工作階段。</span><span class="sxs-lookup"><span data-stu-id="38d65-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="38d65-241">輸入以新增 hello 裝置 IP 位址 toohello 用戶端的受信任的主機：</span><span class="sxs-lookup"><span data-stu-id="38d65-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="38d65-242">其中 <*device_ip*> 是您的裝置 hello IP 位址。 例如：</span><span class="sxs-lookup"><span data-stu-id="38d65-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="38d65-243">toocreate 新的認證類型：</span><span class="sxs-lookup"><span data-stu-id="38d65-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="38d65-244">其中 <*目標裝置的 IP*> 是的 DATA 0 為您的裝置; hello IP 位址，例如**10.126.173.90** hello 前面 hello 主機檔案的映像中所示。</span><span class="sxs-lookup"><span data-stu-id="38d65-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="38d65-245">此外，提供您的裝置 hello 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="38d65-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="38d65-246">建立工作階段，做法是輸入：</span><span class="sxs-lookup"><span data-stu-id="38d65-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="38d65-247">Hello 指令程式中的 hello-ComputerName 參數，提供 hello <*的目標裝置的序號*>。</span><span class="sxs-lookup"><span data-stu-id="38d65-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="38d65-248">這個序號對應 toohello hello 遠端主機; 上的 hosts 檔案中的 DATA 0 的 IP 位址例如， **SHX0991003G44MT** hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="38d65-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="38d65-249">輸入：</span><span class="sxs-lookup"><span data-stu-id="38d65-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="38d65-250">您將需要 toowait 幾分鐘的時間，就能透過 SSL 透過 HTTPS 連線的 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="38d65-251">您看到訊息，指出已連線的 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="38d65-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![使用 HTTPS 和 SSL 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="38d65-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38d65-253">Next steps</span></span>

* <span data-ttu-id="38d65-254">深入了解[使用您的 StorSimple 裝置的 Windows PowerShell tooadminister](storsimple-8000-windows-powershell-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="38d65-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="38d65-255">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="38d65-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

