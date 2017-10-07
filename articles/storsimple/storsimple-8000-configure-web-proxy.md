---
title: "StorSimple 8000 系列裝置的 web proxy aaaSet |Microsoft 文件"
description: "深入了解如何 toouse Windows PowerShell for StorSimple tooconfigure web proxy 設定您的 StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a><span data-ttu-id="a8061-103">為 StorSimple 裝置設定 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-103">Configure web proxy for your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="a8061-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a8061-104">Overview</span></span>

<span data-ttu-id="a8061-105">這個教學課程描述如何 toouse Windows PowerShell for StorSimple tooconfigure，以及檢視 web proxy 設定您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="a8061-105">This tutorial describes how toouse Windows PowerShell for StorSimple tooconfigure and view web proxy settings for your StorSimple device.</span></span> <span data-ttu-id="a8061-106">與 hello 雲端通訊時，會使用所 hello StorSimple 裝置 hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-106">hello web proxy settings are used by hello StorSimple device when communicating with hello cloud.</span></span> <span data-ttu-id="a8061-107">Web proxy 伺服器是使用的 tooadd 另一層安全性，篩選內容、 快取 tooease 頻寬需求或甚至協助進行分析。</span><span class="sxs-lookup"><span data-stu-id="a8061-107">A web proxy server is used tooadd another layer of security, filter content, cache tooease bandwidth requirements or even help with analytics.</span></span>

<span data-ttu-id="a8061-108">本教學課程中的 hello 指導方針適用於僅 tooStorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="a8061-108">hello guidance in this tutorial applies only tooStorSimple 8000 series physical devices.</span></span> <span data-ttu-id="a8061-109">Hello StorSimple 雲端應用裝置 （8010 和 8020） 不支援 web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-109">Web proxy configuration is not supported on hello StorSimple Cloud Appliance (8010 and 8020).</span></span>

<span data-ttu-id="a8061-110">Web Proxy 是 StorSimple 裝置的_選用_設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-110">Web proxy is an _optional_ configuration for your StorSimple device.</span></span> <span data-ttu-id="a8061-111">您只能透過 Windows PowerShell for StorSimple 來設定 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8061-111">You can configure web proxy only via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a8061-112">hello 設定兩步驟程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8061-112">hello configuration is a two-step process as follows:</span></span>

1. <span data-ttu-id="a8061-113">您先設定 web proxy 設定，透過 hello 安裝精靈或 Windows PowerShell for StorSimple cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8061-113">You first configure web proxy settings through hello setup wizard or Windows PowerShell for StorSimple cmdlets.</span></span>
2. <span data-ttu-id="a8061-114">接著，您會啟用 hello 設定 web proxy 設定透過 Windows PowerShell for StorSimple cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8061-114">You then enable hello configured web proxy settings via Windows PowerShell for StorSimple cmdlets.</span></span>

<span data-ttu-id="a8061-115">Hello web proxy 組態完成之後，您可以檢視在 hello Microsoft Azure StorSimple 裝置 Manager 服務和 hello Windows PowerShell 中的 hello 設定 web proxy 設定 for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="a8061-115">After hello web proxy configuration is complete, you can view hello configured web proxy settings in both hello Microsoft Azure StorSimple Device Manager service and hello Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a8061-116">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="a8061-116">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="a8061-117">使用安裝精靈和 Cmdlet 來設定 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8061-117">Configure web proxy by using setup wizard and cmdlets.</span></span>
* <span data-ttu-id="a8061-118">使用 Cmdlet 來啟用 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8061-118">Enable web proxy by using cmdlets.</span></span>
* <span data-ttu-id="a8061-119">在 hello Azure 入口網站中檢視 web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-119">View web proxy settings in hello Azure portal.</span></span>
* <span data-ttu-id="a8061-120">對 Web Proxy 設定期間的錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a8061-120">Troubleshoot errors during web proxy configuration.</span></span>


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a><span data-ttu-id="a8061-121">透過 Windows PowerShell for StorSimple 來設定 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-121">Configure web proxy via Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="a8061-122">您可以使用其中一個 hello 遵循 tooconfigure web proxy 設定：</span><span class="sxs-lookup"><span data-stu-id="a8061-122">You use either of hello following tooconfigure web proxy settings:</span></span>

* <span data-ttu-id="a8061-123">安裝程式精靈 tooguide 您完成 hello 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="a8061-123">Setup wizard tooguide you through hello configuration steps.</span></span>
* <span data-ttu-id="a8061-124">Windows PowerShell for StorSimple 中的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8061-124">Cmdlets in Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a8061-125">每一種方法在 hello 下列各節討論。</span><span class="sxs-lookup"><span data-stu-id="a8061-125">Each of these methods is discussed in hello following sections.</span></span>

## <a name="configure-web-proxy-via-hello-setup-wizard"></a><span data-ttu-id="a8061-126">透過 hello 安裝精靈設定 web proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-126">Configure web proxy via hello setup wizard</span></span>

<span data-ttu-id="a8061-127">使用您透過 hello 步驟 hello 安裝程式精靈 tooguide 進行 web proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="a8061-127">Use hello setup wizard tooguide you through hello steps for web proxy configuration.</span></span> <span data-ttu-id="a8061-128">執行下列步驟 tooconfigure web proxy，您的裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="a8061-128">Perform hello following steps tooconfigure web proxy on your device.</span></span>

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a><span data-ttu-id="a8061-129">透過 hello 安裝精靈的 tooconfigure web proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-129">tooconfigure web proxy via hello setup wizard</span></span>

1. <span data-ttu-id="a8061-130">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**並提供 hello**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a8061-130">In hello serial console menu, choose option 1, **Log in with full access** and provide hello **device administrator password**.</span></span> <span data-ttu-id="a8061-131">輸入 hello 下列命令安裝精靈的工作階段的 toostart:</span><span class="sxs-lookup"><span data-stu-id="a8061-131">Type hello following command toostart a setup wizard session:</span></span>
   
    `Invoke-HcsSetupWizard`
2. <span data-ttu-id="a8061-132">如果這是 hello 您已註冊的裝置使用 hello 安裝精靈的第一次，您需要 tooconfigure hello 所需的所有網路設定直到您到達 hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-132">If this is hello first time that you have used hello setup wizard for device registration, you need tooconfigure all hello required network settings until you reach hello web proxy configuration.</span></span> <span data-ttu-id="a8061-133">如果您的裝置已經註冊，接受所有的 hello 設定網路設定，直到您到達 hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-133">If your device is already registered, accept all hello configured network settings until you reach hello web proxy configuration.</span></span> <span data-ttu-id="a8061-134">在 hello 安裝精靈 提示的 tooconfigure web proxy 設定，當輸入**是**。</span><span class="sxs-lookup"><span data-stu-id="a8061-134">In hello setup wizard, when prompted tooconfigure web proxy settings, type **Yes**.</span></span>
3. <span data-ttu-id="a8061-135">Hello **Web Proxy URL**、 指定 hello IP 位址或 hello 您 web proxy 伺服器與 hello TCP 通訊埠編號，您想裝置 toouse 與 hello 雲端通訊時的完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="a8061-135">For hello **Web Proxy URL**, specify hello IP address or hello fully qualified domain name (FQDN) of your web proxy server and hello TCP port number that you would like your device toouse when communicating with hello cloud.</span></span> <span data-ttu-id="a8061-136">使用下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a8061-136">Use hello following format:</span></span>
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    <span data-ttu-id="a8061-137">預設會指定 TCP 連接埠號碼 8080。</span><span class="sxs-lookup"><span data-stu-id="a8061-137">By default, TCP port number 8080 is specified.</span></span>
4. <span data-ttu-id="a8061-138">Hello 驗證類型選擇為**NTLM**，**基本**，或**無**。</span><span class="sxs-lookup"><span data-stu-id="a8061-138">Choose hello authentication type as **NTLM**, **Basic**, or **None**.</span></span> <span data-ttu-id="a8061-139">基本是 hello hello proxy 伺服器設定最不安全的驗證。</span><span class="sxs-lookup"><span data-stu-id="a8061-139">Basic is hello least secure authentication for hello proxy server configuration.</span></span> <span data-ttu-id="a8061-140">NT LAN Manager (NTLM) 是一種高度安全且複雜的驗證通訊協定使用三向傳訊系統 （有時四是否需要額外完整性） tooauthenticate 使用者。</span><span class="sxs-lookup"><span data-stu-id="a8061-140">NT LAN Manager (NTLM) is a highly secure and complex authentication protocol that uses a three-way messaging system (sometimes four if additional integrity is required) tooauthenticate a user.</span></span> <span data-ttu-id="a8061-141">hello 預設驗證為 NTLM。</span><span class="sxs-lookup"><span data-stu-id="a8061-141">hello default authentication is NTLM.</span></span> <span data-ttu-id="a8061-142">如需詳細資訊，請參閱[基本](http://hc.apache.org/httpclient-3.x/authentication.html)和 [NTLM 驗證](http://hc.apache.org/httpclient-3.x/authentication.html)。</span><span class="sxs-lookup"><span data-stu-id="a8061-142">For more information, see [Basic](http://hc.apache.org/httpclient-3.x/authentication.html) and [NTLM authentication](http://hc.apache.org/httpclient-3.x/authentication.html).</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="a8061-143">**在 hello StorSimple 裝置管理員服務，hello 裝置監控圖表不會運作時基本或 NTLM 驗證已啟用 hello 裝置 hello proxy 伺服器組態中。監控圖表 toowork hello，您需要 tooensure tooNONE 驗證設定。**</span><span class="sxs-lookup"><span data-stu-id="a8061-143">**In hello StorSimple Device Manager service, hello device monitoring charts do not work when Basic or NTLM authentication is enabled in hello proxy server configuration for hello device. For hello monitoring charts toowork, you need tooensure that authentication is set tooNONE.**</span></span>
  
5. <span data-ttu-id="a8061-144">如果您啟用 hello 驗證時，提供**Web Proxy 使用者名稱**和**Web Proxy 密碼**。</span><span class="sxs-lookup"><span data-stu-id="a8061-144">If you enabled hello authentication, supply a **Web Proxy Username** and a **Web Proxy Password**.</span></span> <span data-ttu-id="a8061-145">您也需要 tooconfirm hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="a8061-145">You also need tooconfirm hello password.</span></span>
   
    ![在 StorSimple 裝置 1 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751830.png)

<span data-ttu-id="a8061-147">如果您要註冊您的裝置 hello 第一次，繼續進行 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="a8061-147">If you are registering your device for hello first time, continue with hello registration.</span></span> <span data-ttu-id="a8061-148">如果您的裝置已經註冊，hello 精靈就會結束。</span><span class="sxs-lookup"><span data-stu-id="a8061-148">If your device was already registered, hello wizard exits.</span></span> <span data-ttu-id="a8061-149">儲存設定的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-149">hello configured settings are saved.</span></span>

<span data-ttu-id="a8061-150">現在已啟用 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8061-150">Web proxy is now enabled.</span></span> <span data-ttu-id="a8061-151">您可以略過 hello[啟用 web proxy](#enable-web-proxy)步驟，並直接移過[hello Azure 入口網站中檢視 web proxy 設定](#view-web-proxy-settings-in-the-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="a8061-151">You can skip hello [Enable web proxy](#enable-web-proxy) step and go directly too[View web proxy settings in hello Azure portal](#view-web-proxy-settings-in-the-azure-portal).</span></span>

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a><span data-ttu-id="a8061-152">透過 Windows PowerShell for StorSimple Cmdlet 來設定 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-152">Configure web proxy via Windows PowerShell for StorSimple cmdlets</span></span>

<span data-ttu-id="a8061-153">替代方式 tooconfigure web proxy 設定是透過 hello Windows PowerShell for StorSimple cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8061-153">An alternate way tooconfigure web proxy settings is via hello Windows PowerShell for StorSimple cmdlets.</span></span> <span data-ttu-id="a8061-154">執行下列步驟 tooconfigure web proxy 的 hello。</span><span class="sxs-lookup"><span data-stu-id="a8061-154">Perform hello following steps tooconfigure web proxy.</span></span>

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a><span data-ttu-id="a8061-155">透過 cmdlet tooconfigure web proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-155">tooconfigure web proxy via cmdlets</span></span>
1. <span data-ttu-id="a8061-156">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="a8061-156">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a8061-157">出現提示時，提供 hello**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a8061-157">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="a8061-158">hello 預設密碼為`Password1`。</span><span class="sxs-lookup"><span data-stu-id="a8061-158">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="a8061-159">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="a8061-159">At hello command prompt, type:</span></span>
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    <span data-ttu-id="a8061-160">提供並確認出現提示時 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="a8061-160">Provide and confirm hello password when prompted.</span></span>
   
    ![在 StorSimple 裝置 3 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751831.png)

<span data-ttu-id="a8061-162">hello web proxy 現在已設定，並需要 toobe 啟用。</span><span class="sxs-lookup"><span data-stu-id="a8061-162">hello web proxy is now configured and needs toobe enabled.</span></span>

## <a name="enable-web-proxy"></a><span data-ttu-id="a8061-163">啟用 Web Proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-163">Enable web proxy</span></span>

<span data-ttu-id="a8061-164">預設會停用 Web Proxy。</span><span class="sxs-lookup"><span data-stu-id="a8061-164">Web proxy is disabled by default.</span></span> <span data-ttu-id="a8061-165">StorSimple 裝置上設定 hello web proxy 設定之後，使用 hello Windows PowerShell for StorSimple tooenable hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-165">After you configure hello web proxy settings on your StorSimple device, use hello Windows PowerShell for StorSimple tooenable hello web proxy settings.</span></span>

> [!NOTE]
> <span data-ttu-id="a8061-166">**如果您使用 hello 安裝程式精靈 tooconfigure web proxy，就不需要此步驟。依預設，安裝精靈工作階段之後會自動啟用 Web Proxy。**</span><span class="sxs-lookup"><span data-stu-id="a8061-166">**This step is not required if you used hello setup wizard tooconfigure web proxy. Web proxy is automatically enabled by default after a setup wizard session.**</span></span>


<span data-ttu-id="a8061-167">執行下列步驟在 Windows PowerShell 中的適用於 StorSimple tooenable web proxy 在裝置上的 hello:</span><span class="sxs-lookup"><span data-stu-id="a8061-167">Perform hello following steps in Windows PowerShell for StorSimple tooenable web proxy on your device:</span></span>

#### <a name="tooenable-web-proxy"></a><span data-ttu-id="a8061-168">tooenable web proxy</span><span class="sxs-lookup"><span data-stu-id="a8061-168">tooenable web proxy</span></span>
1. <span data-ttu-id="a8061-169">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="a8061-169">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a8061-170">出現提示時，提供 hello**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="a8061-170">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="a8061-171">hello 預設密碼為`Password1`。</span><span class="sxs-lookup"><span data-stu-id="a8061-171">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="a8061-172">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="a8061-172">At hello command prompt, type:</span></span>
   
    `Enable-HcsWebProxy`
   
    <span data-ttu-id="a8061-173">您現在已經在您的 StorSimple 裝置上啟用 hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-173">You have now enabled hello web proxy configuration on your StorSimple device.</span></span>
   
    ![在 StorSimple 裝置 4 設定 Web Proxy](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a><span data-ttu-id="a8061-175">在 hello Azure 入口網站中檢視 web proxy 設定</span><span class="sxs-lookup"><span data-stu-id="a8061-175">View web proxy settings in hello Azure portal</span></span>

<span data-ttu-id="a8061-176">hello web proxy 設定透過 hello Windows PowerShell 介面設定，而且不能從 hello 入口網站中變更。</span><span class="sxs-lookup"><span data-stu-id="a8061-176">hello web proxy settings are configured through hello Windows PowerShell interface and cannot be changed from within hello portal.</span></span> <span data-ttu-id="a8061-177">您不過，可以在 hello 入口網站中檢視這些設定的設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-177">You can, however, view these configured settings in hello portal.</span></span> <span data-ttu-id="a8061-178">執行下列步驟 tooview web proxy 的 hello。</span><span class="sxs-lookup"><span data-stu-id="a8061-178">Perform hello following steps tooview web proxy.</span></span>

#### <a name="tooview-web-proxy-settings"></a><span data-ttu-id="a8061-179">tooview web proxy 設定</span><span class="sxs-lookup"><span data-stu-id="a8061-179">tooview web proxy settings</span></span>
1. <span data-ttu-id="a8061-180">瀏覽過**StorSimple 裝置管理員服務 > 裝置**。</span><span class="sxs-lookup"><span data-stu-id="a8061-180">Navigate too**StorSimple Device Manager service > Devices**.</span></span> <span data-ttu-id="a8061-181">選取並按一下裝置，然後移過**裝置設定 > 網路**。</span><span class="sxs-lookup"><span data-stu-id="a8061-181">Select and click a device and then go too**Device settings > Network**.</span></span>

    ![按一下 [網路]](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. <span data-ttu-id="a8061-183">在 hello**網路設定**刀鋒視窗中，按一下 hello **Web proxy**磚。</span><span class="sxs-lookup"><span data-stu-id="a8061-183">In hello **Network settings** blade, click hello **Web proxy** tile.</span></span>

    ![按一下 [Web Proxy]](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. <span data-ttu-id="a8061-185">在 hello **Web proxy**刀鋒視窗中，檢閱您的 StorSimple 裝置上設定的 hello web proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-185">In hello **Web proxy** blade, review hello configured web proxy settings on your StorSimple device.</span></span>
   
    ![檢視 Web Proxy 設定](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a><span data-ttu-id="a8061-187">在 Web Proxy 設定期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="a8061-187">Errors during web proxy configuration</span></span>

<span data-ttu-id="a8061-188">Hello web proxy 設定不正確，如果錯誤訊息會顯示的 toohello Windows PowerShell for StorSimple 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="a8061-188">If hello web proxy settings are configured incorrectly, error messages are displayed toohello user in Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a8061-189">hello 下表說明一些這些錯誤訊息、 可能原因和建議的動作。</span><span class="sxs-lookup"><span data-stu-id="a8061-189">hello following table explains some of these error messages, their probable causes, and recommended actions.</span></span>

| <span data-ttu-id="a8061-190">序號</span><span class="sxs-lookup"><span data-stu-id="a8061-190">Serial no.</span></span> | <span data-ttu-id="a8061-191">HRESULT 錯誤碼</span><span class="sxs-lookup"><span data-stu-id="a8061-191">HRESULT error Code</span></span> | <span data-ttu-id="a8061-192">可能的根本原因</span><span class="sxs-lookup"><span data-stu-id="a8061-192">Possible root cause</span></span> | <span data-ttu-id="a8061-193">建議的動作</span><span class="sxs-lookup"><span data-stu-id="a8061-193">Recommended action</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a8061-194">1.</span><span class="sxs-lookup"><span data-stu-id="a8061-194">1.</span></span> |<span data-ttu-id="a8061-195">0x80070001</span><span class="sxs-lookup"><span data-stu-id="a8061-195">0x80070001</span></span> |<span data-ttu-id="a8061-196">從 hello 被動控制站執行命令，而且不能 toocommunicate 與 hello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="a8061-196">Command is run from hello passive controller and it is not able toocommunicate with hello active controller.</span></span> |<span data-ttu-id="a8061-197">Hello 作用中控制器上執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="a8061-197">Run hello command on hello active controller.</span></span> <span data-ttu-id="a8061-198">從被動控制站 hello toorun hello 命令，您必須修正 hello tooactive 被動控制站的連線。</span><span class="sxs-lookup"><span data-stu-id="a8061-198">toorun hello command from hello passive controller, you must fix hello connectivity from passive tooactive controller.</span></span> <span data-ttu-id="a8061-199">如果此連線已中斷，您必須連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="a8061-199">You must engage Microsoft Support if this connectivity is broken.</span></span> |
| <span data-ttu-id="a8061-200">2.</span><span class="sxs-lookup"><span data-stu-id="a8061-200">2.</span></span> |<span data-ttu-id="a8061-201">0x800710dd-hello 作業識別碼無效</span><span class="sxs-lookup"><span data-stu-id="a8061-201">0x800710dd - hello operation identifier is not valid</span></span> |<span data-ttu-id="a8061-202">StorSimple 雲端設備不支援 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-202">Proxy settings are not supported on StorSimple Cloud Appliance.</span></span> |<span data-ttu-id="a8061-203">StorSimple 雲端設備不支援 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-203">Proxy settings are not supported on StorSimple Cloud Appliance.</span></span> <span data-ttu-id="a8061-204">這些設定只能在 StorSimple 實體裝置上設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-204">These can only be configured on a StorSimple physical device.</span></span> |
| <span data-ttu-id="a8061-205">3.</span><span class="sxs-lookup"><span data-stu-id="a8061-205">3.</span></span> |<span data-ttu-id="a8061-206">0x80070057 - 無效的參數</span><span class="sxs-lookup"><span data-stu-id="a8061-206">0x80070057 - Invalid parameter</span></span> |<span data-ttu-id="a8061-207">其中一個 hello 參數提供給 hello proxy 設定不正確。</span><span class="sxs-lookup"><span data-stu-id="a8061-207">One of hello parameters provided for hello proxy settings is not valid.</span></span> |<span data-ttu-id="a8061-208">hello URI 未提供正確格式。</span><span class="sxs-lookup"><span data-stu-id="a8061-208">hello URI is not provided in correct format.</span></span> <span data-ttu-id="a8061-209">使用下列格式的 hello:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>`</span><span class="sxs-lookup"><span data-stu-id="a8061-209">Use hello following format: `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`</span></span> |
| <span data-ttu-id="a8061-210">4.</span><span class="sxs-lookup"><span data-stu-id="a8061-210">4.</span></span> |<span data-ttu-id="a8061-211">0x800706ba - RPC 伺服器無法使用</span><span class="sxs-lookup"><span data-stu-id="a8061-211">0x800706ba - RPC server not available</span></span> |<span data-ttu-id="a8061-212">hello 根本原因是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="a8061-212">hello root cause is one of hello following:</span></span></br></br><span data-ttu-id="a8061-213">叢集未啟動。</span><span class="sxs-lookup"><span data-stu-id="a8061-213">Cluster is not up.</span></span> </br></br><span data-ttu-id="a8061-214">資料路徑服務不在執行中。</span><span class="sxs-lookup"><span data-stu-id="a8061-214">Datapath service is not running.</span></span></br></br><span data-ttu-id="a8061-215">從被動控制站執行 hello 命令，並不能 toocommunicate 與 hello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="a8061-215">hello command is run from passive controller and it is not able toocommunicate with hello active controller.</span></span> |<span data-ttu-id="a8061-216">進行 hello 叢集的 Microsoft 支援服務 tooensure 已啟動，而且資料路徑服務正在執行。</span><span class="sxs-lookup"><span data-stu-id="a8061-216">Engage Microsoft Support tooensure that hello cluster is up and datapath service is running.</span></span></br></br><span data-ttu-id="a8061-217">從 hello 作用中控制器執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="a8061-217">Run hello command from hello active controller.</span></span> <span data-ttu-id="a8061-218">如果您想從被動控制站 hello toorun hello 命令時，您必須確定該 hello 被動控制站可以與 hello active 控制器通訊。</span><span class="sxs-lookup"><span data-stu-id="a8061-218">If you want toorun hello command from hello passive controller, you must ensure that hello passive controller can communicate with hello active controller.</span></span> <span data-ttu-id="a8061-219">如果此連線已中斷，您必須連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="a8061-219">You must engage Microsoft Support if this connectivity is broken.</span></span> |
| <span data-ttu-id="a8061-220">5.</span><span class="sxs-lookup"><span data-stu-id="a8061-220">5.</span></span> |<span data-ttu-id="a8061-221">0x800706be - RPC 呼叫失敗</span><span class="sxs-lookup"><span data-stu-id="a8061-221">0x800706be - RPC call failed</span></span> |<span data-ttu-id="a8061-222">叢集已關閉。</span><span class="sxs-lookup"><span data-stu-id="a8061-222">Cluster is down.</span></span> |<span data-ttu-id="a8061-223">請連絡 Microsoft 支援服務 hello 叢集的 tooensure 已啟動。</span><span class="sxs-lookup"><span data-stu-id="a8061-223">Engage Microsoft Support tooensure that hello cluster is up.</span></span> |
| <span data-ttu-id="a8061-224">6.</span><span class="sxs-lookup"><span data-stu-id="a8061-224">6.</span></span> |<span data-ttu-id="a8061-225">0x8007138f - 找不到叢集資源</span><span class="sxs-lookup"><span data-stu-id="a8061-225">0x8007138f - Cluster resource not found</span></span> |<span data-ttu-id="a8061-226">找不到平台服務叢集資源。</span><span class="sxs-lookup"><span data-stu-id="a8061-226">Platform service cluster resource is not found.</span></span> <span data-ttu-id="a8061-227">當 hello 安裝不正確，也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="a8061-227">This can happen when hello installation was not proper.</span></span> |<span data-ttu-id="a8061-228">您可能需要 tooperform 原廠重設您的裝置。</span><span class="sxs-lookup"><span data-stu-id="a8061-228">You may need tooperform a factory reset on your device.</span></span> <span data-ttu-id="a8061-229">您可能需要 toocreate 平台資源。</span><span class="sxs-lookup"><span data-stu-id="a8061-229">You may need toocreate a platform resource.</span></span> <span data-ttu-id="a8061-230">連絡 Microsoft 支援服務以進行後續步驟。</span><span class="sxs-lookup"><span data-stu-id="a8061-230">Contact Microsoft Support for next steps.</span></span> |
| <span data-ttu-id="a8061-231">7.</span><span class="sxs-lookup"><span data-stu-id="a8061-231">7.</span></span> |<span data-ttu-id="a8061-232">0x8007138c - 叢集資源不在線上</span><span class="sxs-lookup"><span data-stu-id="a8061-232">0x8007138c - Cluster resource not online</span></span> |<span data-ttu-id="a8061-233">平台或資料路徑叢集資源不在線上。</span><span class="sxs-lookup"><span data-stu-id="a8061-233">Platform or datapath cluster resources are not online.</span></span> |<span data-ttu-id="a8061-234">連絡 Microsoft 支援服務 toohelp 確定 hello 和平台服務資源已上線。</span><span class="sxs-lookup"><span data-stu-id="a8061-234">Contact Microsoft Support toohelp ensure that hello datapath and platform service resource are online.</span></span> |

> [!NOTE]
> * <span data-ttu-id="a8061-235">hello 上述錯誤訊息清單未全部列出。</span><span class="sxs-lookup"><span data-stu-id="a8061-235">hello above list of error messages is not exhaustive.</span></span>
> * <span data-ttu-id="a8061-236">Hello StorSimple 裝置管理員服務在 Azure 入口網站中，將不會顯示錯誤相關的 tooweb proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="a8061-236">Errors related tooweb proxy settings will not be displayed in hello Azure portal in your StorSimple Device Manager service.</span></span> <span data-ttu-id="a8061-237">如果發生問題時透過 web proxy hello 組態完成後，hello 裝置狀態會變更太**離線**hello 傳統入口網站中。 |</span><span class="sxs-lookup"><span data-stu-id="a8061-237">If there is an issue with web proxy after hello configuration is completed, hello device status will change too**Offline** in hello classic portal.|</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8061-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8061-238">Next Steps</span></span>
* <span data-ttu-id="a8061-239">如果您在部署您的裝置，或設定 web proxy 設定時遇到任何問題，請參閱太[疑難排解您的 StorSimple 裝置部署](storsimple-troubleshoot-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a8061-239">If you experience any issues while deploying your device or configuring web proxy settings, refer too[Troubleshoot your StorSimple device deployment](storsimple-troubleshoot-deployment.md).</span></span>
* <span data-ttu-id="a8061-240">toolearn toouse hello StorSimple 裝置管理員服務如何太移[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="a8061-240">toolearn how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

