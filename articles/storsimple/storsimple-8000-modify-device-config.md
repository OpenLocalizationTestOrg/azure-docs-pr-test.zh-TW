---
title: "aaaModify hello StorSimple 8000 系列裝置設定 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple 裝置管理員服務 tooreconfigure 已經部署 StorSimple 裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a><span data-ttu-id="3e836-103">使用 hello StorSimple 裝置管理員服務 toomodify StorSimple 裝置的組態</span><span class="sxs-lookup"><span data-stu-id="3e836-103">Use hello StorSimple Device Manager service toomodify your StorSimple device configuration</span></span>

## <a name="overview"></a><span data-ttu-id="3e836-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3e836-104">Overview</span></span>

<span data-ttu-id="3e836-105">hello Azure 入口網站**裝置設定**> 一節中 hello**設定**刀鋒視窗包含您可以重新設定 StorSimple 裝置管理員管理 StorSimple 裝置的所有 hello 裝置參數服務。</span><span class="sxs-lookup"><span data-stu-id="3e836-105">hello Azure portal **Device settings** section in hello **Settings** blade contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="3e836-106">本教學課程說明如何使用 hello**設定**刀鋒視窗 tooperform hello 下列裝置層級工作：</span><span class="sxs-lookup"><span data-stu-id="3e836-106">This tutorial explains how you can use hello **Settings** blade tooperform hello following device-level tasks:</span></span>

* <span data-ttu-id="3e836-107">修改裝置的易記名稱</span><span class="sxs-lookup"><span data-stu-id="3e836-107">Modify device friendly name</span></span>
* <span data-ttu-id="3e836-108">修改裝置的時間設定</span><span class="sxs-lookup"><span data-stu-id="3e836-108">Modify device time settings</span></span>
* <span data-ttu-id="3e836-109">指派次要 DNS</span><span class="sxs-lookup"><span data-stu-id="3e836-109">Assign a secondary DNS</span></span>
* <span data-ttu-id="3e836-110">修改網路介面</span><span class="sxs-lookup"><span data-stu-id="3e836-110">Modify network interfaces</span></span>
* <span data-ttu-id="3e836-111">交換或重新指派 IP</span><span class="sxs-lookup"><span data-stu-id="3e836-111">Swap or reassign IPs</span></span>

## <a name="modify-device-friendly-name"></a><span data-ttu-id="3e836-112">修改裝置的易記名稱</span><span class="sxs-lookup"><span data-stu-id="3e836-112">Modify device friendly name</span></span>

<span data-ttu-id="3e836-113">您可以使用 hello Azure 入口網站 toochange hello 裝置名稱，並將它指派您所選擇的唯一易記名稱。</span><span class="sxs-lookup"><span data-stu-id="3e836-113">You can use hello Azure portal toochange hello device name and assign it a unique friendly name of your choice.</span></span> <span data-ttu-id="3e836-114">使用 hello**一般設定**刀鋒視窗上您裝置 toomodify hello 裝置的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="3e836-114">Use hello **General settings** blade on your device toomodify hello device friendly name.</span></span> <span data-ttu-id="3e836-115">hello 易記名稱可以包含任何字元，最多可有 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="3e836-115">hello friendly name can contain any characters and can be a maximum of 64 characters long.</span></span>

> [!NOTE] 
> <span data-ttu-id="3e836-116">Hello 裝置安裝程式完成之前，您只能修改 hello hello Azure 入口網站中的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="3e836-116">You can only modify hello device name in hello Azure portal before hello device setup is complete.</span></span> <span data-ttu-id="3e836-117">Hello 最低裝置設定完成之後，您無法變更 hello 裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="3e836-117">Once hello minimum device setup is complete, you cannot change hello device name.</span></span>

![[一般設定] 中的裝置名稱](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

<span data-ttu-id="3e836-119">連接的 toohello StorSimple 裝置管理員服務的 StorSimple 裝置會指派預設名稱。</span><span class="sxs-lookup"><span data-stu-id="3e836-119">A StorSimple device that is connected toohello StorSimple Device Manager service is assigned a default name.</span></span> <span data-ttu-id="3e836-120">hello 預設名稱通常會反映 hello 裝置 hello 序號。</span><span class="sxs-lookup"><span data-stu-id="3e836-120">hello default name typically reflects hello serial number of hello device.</span></span> <span data-ttu-id="3e836-121">例如，預設的裝置名稱是 15 個字元，例如 8600-SHX0991003G44HT 表示 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3e836-121">For example, a default device name that is 15 characters long, such as 8600-SHX0991003G44HT, indicates hello following:</span></span>

* <span data-ttu-id="3e836-122">**8600** – 指出 hello 裝置模型。</span><span class="sxs-lookup"><span data-stu-id="3e836-122">**8600**  – Indicates hello device model.</span></span>
* <span data-ttu-id="3e836-123">**SHX** – 指出 hello 製造站台。</span><span class="sxs-lookup"><span data-stu-id="3e836-123">**SHX** – Indicates hello manufacturing site.</span></span>
* <span data-ttu-id="3e836-124">**0991003** – 表示特定產品。</span><span class="sxs-lookup"><span data-stu-id="3e836-124">**0991003** - Indicates a specific product.</span></span>
* <span data-ttu-id="3e836-125">**G44HT**-hello 最後 5 位數會遞增的 toocreate 唯一序號。</span><span class="sxs-lookup"><span data-stu-id="3e836-125">**G44HT**- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="3e836-126">這可能不是連續的組合。</span><span class="sxs-lookup"><span data-stu-id="3e836-126">This might not be a sequential set.</span></span>

## <a name="modify-device-description"></a><span data-ttu-id="3e836-127">修改裝置描述</span><span class="sxs-lookup"><span data-stu-id="3e836-127">Modify device description</span></span>

<span data-ttu-id="3e836-128">使用 hello**一般設定**裝置 toomodify hello 裝置描述上的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3e836-128">Use hello **General settings** blade on your device toomodify hello device description.</span></span>

![[一般設定] 中的裝置描述](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

<span data-ttu-id="3e836-130">裝置描述通常有助於識別 hello 擁有者和 hello 裝置 hello 實體位置。</span><span class="sxs-lookup"><span data-stu-id="3e836-130">A device description usually helps identify hello owner and hello physical location of hello device.</span></span> <span data-ttu-id="3e836-131">hello 描述欄位必須包含少於 256 個字元。</span><span class="sxs-lookup"><span data-stu-id="3e836-131">hello description field must contain fewer than 256 characters.</span></span>

## <a name="modify-time-settings"></a><span data-ttu-id="3e836-132">修改時間設定</span><span class="sxs-lookup"><span data-stu-id="3e836-132">Modify time settings</span></span>

<span data-ttu-id="3e836-133">您的裝置必須同步時間順序 tooauthenticate 與雲端儲存體服務提供者。</span><span class="sxs-lookup"><span data-stu-id="3e836-133">Your device must synchronize time in order tooauthenticate with your cloud storage service provider.</span></span> <span data-ttu-id="3e836-134">使用 hello**一般設定**上您的裝置 toomodify hello 裝置時間設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3e836-134">Use hello **General settings** blade on your device toomodify hello device time settings.</span></span>

![[一般設定] 中的裝置描述](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 <span data-ttu-id="3e836-136">從 hello 下拉式清單中選取您的時區。</span><span class="sxs-lookup"><span data-stu-id="3e836-136">Select your time zone from hello drop-down list.</span></span> <span data-ttu-id="3e836-137">您可以指定 tootwo 網路時間通訊協定 (NTP) 伺服器：</span><span class="sxs-lookup"><span data-stu-id="3e836-137">You can specify up tootwo Network Time Protocol (NTP) servers:</span></span>

 - <span data-ttu-id="3e836-138">**主要 NTP 伺服器**-hello 組態需要，指定當您使用 Windows PowerShell for StorSimple tooconfigure 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3e836-138">**Primary NTP server** -  hello configuration is required and is specified when you use Windows PowerShell for StorSimple tooconfigure your device.</span></span> <span data-ttu-id="3e836-139">您可以指定 hello 預設的 Windows Server **time.windows.com**為 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e836-139">You can specify hello default Windows Server **time.windows.com** as your NTP server.</span></span> <span data-ttu-id="3e836-140">您可以檢視 hello 主要 NTP 伺服器組態透過 hello Azure 入口網站，但您必須使用 hello Windows PowerShell 介面 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="3e836-140">You can view hello primary NTP server configuration through hello Azure portal, but you must use hello Windows PowerShell interface toochange it.</span></span> <span data-ttu-id="3e836-141">使用 hello `Set-HcsNTPClientServerAddress` cmdlet toomodify hello 主要 NTP 伺服器的裝置。</span><span class="sxs-lookup"><span data-stu-id="3e836-141">Use hello `Set-HcsNTPClientServerAddress` cmdlet toomodify hello Primary NTP server of your device.</span></span> <span data-ttu-id="3e836-142">如需詳細資訊，請移 toosynxtax [Set-hcsntpclientserveraddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3e836-142">For more information, go toosynxtax for [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

- <span data-ttu-id="3e836-143">**次要 NTP 伺服器**-hello 組態是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="3e836-143">**Secondary NTP server** - hello configuration is optional.</span></span> <span data-ttu-id="3e836-144">您可以使用 hello 入口 tooconfigure 次要 NTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e836-144">You can use hello portal tooconfigure a secondary NTP server.</span></span>

<span data-ttu-id="3e836-145">設定 hello NTP 伺服器時，請確定您的網路，允許從您的資料中心 toohello 網際網路 hello NTP 流量 toopass。</span><span class="sxs-lookup"><span data-stu-id="3e836-145">When configuring hello NTP server, ensure that your network allows hello NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="3e836-146">指定公用 NTP 伺服器時，您必須確定網路防火牆和其他安全性裝置會設定的 tooallow NTP 流量從網路外部的 hello 的 tootravel tooand。</span><span class="sxs-lookup"><span data-stu-id="3e836-146">When specifying a public NTP server, you must make sure that your network firewalls and other security devices are configured tooallow NTP traffic tootravel tooand from hello outside network.</span></span> <span data-ttu-id="3e836-147">若不允許雙向 NTP 流量，您必須使用內部 NTP 伺服器 (Windows 網域控制器會提供這個函式)。</span><span class="sxs-lookup"><span data-stu-id="3e836-147">If bidirectional NTP traffic is not permitted, you must use an internal NTP server (a Windows domain controller provides this function).</span></span> <span data-ttu-id="3e836-148">如果您的裝置無法同步處理時間，它可能無法使用您的雲端存放裝置提供者無法 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="3e836-148">If your device cannot synchronize time, it may not be able toocommunicate with your cloud storage provider.</span></span>

<span data-ttu-id="3e836-149">toosee 公用 NTP 伺服器清單，移 toohello [NTP 伺服器的 Web](http://support.ntp.org/bin/view/Servers/WebHome)。</span><span class="sxs-lookup"><span data-stu-id="3e836-149">toosee a list of public NTP servers, go toohello [NTP Servers Web](http://support.ntp.org/bin/view/Servers/WebHome).</span></span>

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a><span data-ttu-id="3e836-150">如果 hello 裝置部署在不同的時區會怎樣？</span><span class="sxs-lookup"><span data-stu-id="3e836-150">What happens if hello device is deployed in a different time zone?</span></span>

<span data-ttu-id="3e836-151">如果 hello 裝置部署在不同的時區，將會變更裝置時區 hello。</span><span class="sxs-lookup"><span data-stu-id="3e836-151">If hello device is deployed in a different time zone, hello device time zone will change.</span></span> <span data-ttu-id="3e836-152">假設所有 hello 備份原則都使用 hello 裝置時區，hello 備份原則會自動調整根據新時區 hello。</span><span class="sxs-lookup"><span data-stu-id="3e836-152">Given that all hello backup policies use hello device time zone, hello backup policies will automatically adjust in accordance with hello new time zone.</span></span> <span data-ttu-id="3e836-153">不需使用者介入。</span><span class="sxs-lookup"><span data-stu-id="3e836-153">No user intervention is required.</span></span>

## <a name="modify-dns-settings"></a><span data-ttu-id="3e836-154">修改 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="3e836-154">Modify DNS settings</span></span>

<span data-ttu-id="3e836-155">您的裝置嘗試 toocommunicate 與雲端儲存體服務提供者時，會使用 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e836-155">A DNS server is used when your device attempts toocommunicate with your cloud storage service provider.</span></span> <span data-ttu-id="3e836-156">使用 hello**網路設定**上裝置 tooview 刀鋒視窗，以及修改 hello 設定 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="3e836-156">Use hello **Network settings** blade on your device tooview and modify hello configured DNS settings.</span></span> 

![[網路設定] 中的 DNS 設定](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

<span data-ttu-id="3e836-158">高可用性，您需要的 tooconfigure 這兩個主要的 hello 而且 hello 初始裝置部署期間 hello 次要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e836-158">For high availability, you are required tooconfigure both hello primary and hello secondary DNS servers during hello initial device deployment.</span></span>

<span data-ttu-id="3e836-159">**主要 DNS 伺服器**-您使用 hello Windows PowerShell for StorSimple toofirst hello 初始設定期間指定 hello 主要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e836-159">**Primary DNS server** - You use hello Windows PowerShell for StorSimple toofirst specify hello Primary DNS server during hello initial setup.</span></span> <span data-ttu-id="3e836-160">您可以重新設定 hello 主要 DNS 伺服器僅透過 hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-160">You can reconfigure hello primary DNS server only via hello Windows PowerShell interface.</span></span> <span data-ttu-id="3e836-161">使用 hello `Set-HcsDNSClientServerAddress` cmdlet toomodify hello 主要 DNS 伺服器的裝置。</span><span class="sxs-lookup"><span data-stu-id="3e836-161">Use hello `Set-HcsDNSClientServerAddress` cmdlet toomodify hello primary DNS server of your device.</span></span> <span data-ttu-id="3e836-162">如需詳細資訊，請移 toosynxtax [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3e836-162">For more information, go toosynxtax for [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.</span></span>

<span data-ttu-id="3e836-163">**次要 DNS 伺服器**-toomodify hello 次要 DNS 伺服器，使用 hello `Set-HcsDNSClientServerAddress` hello 裝置 hello Windows PowerShell 介面中的 cmdlet 或**網路設定**刀鋒視窗中的 hello Azure 在 StorSimple 裝置入口網站。</span><span class="sxs-lookup"><span data-stu-id="3e836-163">**Secondary DNS server** - toomodify hello secondary DNS server, use hello `Set-HcsDNSClientServerAddress` cmdlet in hello Windows PowerShell interface of hello device or **Network settings** blade of your StorSimple device in hello Azure portal.</span></span>

<span data-ttu-id="3e836-164">toomodify hello 次要 DNS 伺服器在 Azure 入口網站執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="3e836-164">toomodify hello secondary DNS server in Azure portal, perform hello following steps.</span></span>

1. <span data-ttu-id="3e836-165">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="3e836-165">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3e836-166">從 hello 的裝置清單，選取，然後按一下您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3e836-166">From hello list of devices, select and click your device.</span></span>

2. <span data-ttu-id="3e836-167">在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 網路**。</span><span class="sxs-lookup"><span data-stu-id="3e836-167">In hello **Settings** blade, go too**Device settings > Network**.</span></span> <span data-ttu-id="3e836-168">這會開啟 hello**網路設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3e836-168">This opens up hello **Network settings** blade.</span></span> <span data-ttu-id="3e836-169">按一下 [DNS 設定] 圖格。</span><span class="sxs-lookup"><span data-stu-id="3e836-169">Click **DNS settings** tile.</span></span> <span data-ttu-id="3e836-170">修改 hello 次要 DNS 伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3e836-170">Modify hello secondary DNS server IP address.</span></span>

    ![修改次要 DNS 伺服器 IP 位址](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. <span data-ttu-id="3e836-172">在 hello 命令列中，按一下**儲存**時提示您進行確認，請按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="3e836-172">From hello command bar, click **Save** and when prompted for confirmation, click **OK**.</span></span>

    ![儲存並確認變更](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a><span data-ttu-id="3e836-174">修改網路介面</span><span class="sxs-lookup"><span data-stu-id="3e836-174">Modify network interfaces</span></span>

<span data-ttu-id="3e836-175">您的裝置具有六個裝置網路介面，其中四個是 1 GbE，而其中兩個是 10 Gbe。</span><span class="sxs-lookup"><span data-stu-id="3e836-175">Your device has six device network interfaces, four of which are 1 GbE and two of which are 10 GbE.</span></span> <span data-ttu-id="3e836-176">這些介面都會標示為 DATA 0 至 DATA 5。</span><span class="sxs-lookup"><span data-stu-id="3e836-176">These interfaces are labeled as DATA 0 – DATA 5.</span></span> <span data-ttu-id="3e836-177">DATA 0、DATA 1、DATA 4 和 DATA 5 是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 網路介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-177">DATA 0, DATA 1, DATA 4, and DATA 5 are 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE network interfaces.</span></span>

<span data-ttu-id="3e836-178">使用 hello**網路設定**刀鋒視窗 tooconfigure 每個的 hello 介面 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="3e836-178">Use hello **Network settings** blade tooconfigure each of hello interfaces toobe used.</span></span>

![透過 [網路設定] 設定網路介面](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

<span data-ttu-id="3e836-180">tooensure 高可用性，建議您的裝置上有兩個以上的 iSCSI 介面和兩個具備雲端功能的介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-180">tooensure high availability, we recommend that you have at least two iSCSI interfaces and two cloud-enabled interfaces on your device.</span></span> <span data-ttu-id="3e836-181">我們建議停用未使用的介面，但並非必要。</span><span class="sxs-lookup"><span data-stu-id="3e836-181">We recommend but do not require that unused interfaces be disabled.</span></span>

<span data-ttu-id="3e836-182">每個網路介面，會顯示 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="3e836-182">For each network interface, hello following parameters are displayed:</span></span>

* <span data-ttu-id="3e836-183">**速度** – 並非使用者可設定的參數。</span><span class="sxs-lookup"><span data-stu-id="3e836-183">**Speed** – Not a user-configurable parameter.</span></span> <span data-ttu-id="3e836-184">DATA 0、DATA 1、DATA 4 和 DATA 5 永遠是 1 GbE，而 DATA 2 和 DATA 3 是 10 GbE 介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-184">DATA 0, DATA 1, DATA 4, and DATA 5 are always 1 GbE, whereas DATA 2 and DATA 3 are 10 GbE interfaces.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3e836-185">速度和雙工會一律自動交涉。</span><span class="sxs-lookup"><span data-stu-id="3e836-185">Speed and duplex are always auto-negotiated.</span></span> <span data-ttu-id="3e836-186">不支援 Jumbo 框架。</span><span class="sxs-lookup"><span data-stu-id="3e836-186">Jumbo frames are not supported.</span></span>
  
* <span data-ttu-id="3e836-187">**介面狀態** – 介面可以啟用或停用。</span><span class="sxs-lookup"><span data-stu-id="3e836-187">**Interface state** – An interface can be enabled or disabled.</span></span> <span data-ttu-id="3e836-188">如果啟用，hello 裝置會嘗試 toouse hello 介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-188">If enabled, hello device will attempt toouse hello interface.</span></span> <span data-ttu-id="3e836-189">我們建議您啟用連接的 toohello 網路和使用這些介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-189">We recommend that only those interfaces that are connected toohello network and used be enabled.</span></span> <span data-ttu-id="3e836-190">停用任何您沒有使用的介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-190">Disable any interfaces that you are not using.</span></span>
* <span data-ttu-id="3e836-191">**介面型別**– 此參數可讓您 tooisolate iSCSI 流量與雲端儲存體流量。</span><span class="sxs-lookup"><span data-stu-id="3e836-191">**Interface type** – This parameter allows you tooisolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="3e836-192">這個參數可以是 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="3e836-192">This parameter can be one of hello following:</span></span>
  
  * <span data-ttu-id="3e836-193">**啟用雲端**– hello 裝置啟用時，將使用此介面 toocommunicate 與 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="3e836-193">**Cloud enabled** – when enabled, hello device will use this interface toocommunicate with hello cloud.</span></span>
  * <span data-ttu-id="3e836-194">**具備 iSCSI 功能**– hello 裝置啟用時，將使用此介面 toocommunicate 與 hello iSCSI 主機。</span><span class="sxs-lookup"><span data-stu-id="3e836-194">**iSCSI enabled** – when enabled, hello device will use this interface toocommunicate with hello iSCSI host.</span></span>
    
    <span data-ttu-id="3e836-195">我們建議您隔離 iSCSI 流量與雲端儲存空間流量。</span><span class="sxs-lookup"><span data-stu-id="3e836-195">We recommend that you isolate iSCSI traffic from cloud storage traffic.</span></span> <span data-ttu-id="3e836-196">也請注意是否主機是 hello 內相同的子網路與裝置，您不需要 tooassign 閘道;不過，如果您的主機位於不同的子網路與您的裝置，您將需要 tooassign 閘道。</span><span class="sxs-lookup"><span data-stu-id="3e836-196">Also note if your host is within hello same subnet as your device, you do not need tooassign a gateway; however, if your host is in a different subnet than your device, you will need tooassign a gateway.</span></span>
* <span data-ttu-id="3e836-197">**IP 位址**– 當您設定任何的 hello 網路介面卡，您必須設定虛擬 IP (VIP)。</span><span class="sxs-lookup"><span data-stu-id="3e836-197">**IP address** – When you configure any of hello network interfaces, you must configure a virtual IP (VIP).</span></span> <span data-ttu-id="3e836-198">這可以是 IPv4 或 IPv6 或同時使用。</span><span class="sxs-lookup"><span data-stu-id="3e836-198">This can be IPv4 or IPv6 or both.</span></span> <span data-ttu-id="3e836-199">Hello 裝置網路介面支援 hello IPv4 和 IPv6 位址系列。</span><span class="sxs-lookup"><span data-stu-id="3e836-199">Both hello IPv4 and IPv6 address families are supported for hello device network interfaces.</span></span> <span data-ttu-id="3e836-200">當您使用 IPv4 時，請以小數點十進位表示法指定 32 位元的 IP 位址 (*xxx.xxx.xxx.xxx*)。</span><span class="sxs-lookup"><span data-stu-id="3e836-200">When using IPv4, specify a 32-bit IP address (*xxx.xxx.xxx.xxx*) in dot-decimal notation.</span></span> <span data-ttu-id="3e836-201">當您使用 IPv6 時，僅需提供 4 位數前置詞，而裝置網路介面的 128 位元位址將會根據該前置詞自動產生。</span><span class="sxs-lookup"><span data-stu-id="3e836-201">When using IPv6, simply supply a 4-digit prefix, and a 128-bit address will be generated automatically for your device network interface based on that prefix.</span></span>
* <span data-ttu-id="3e836-202">**子網路**– 這是指 toohello 子網路遮罩，並已透過 hello Windows PowerShell 介面設定。</span><span class="sxs-lookup"><span data-stu-id="3e836-202">**Subnet** – This refers toohello subnet mask and is configured via hello Windows PowerShell interface.</span></span>
* <span data-ttu-id="3e836-203">**閘道**– 這是它會試著 toocommunicate hello 內的節點時應使用此介面的 hello 預設閘道相同的 IP 位址空間 （子網路）。</span><span class="sxs-lookup"><span data-stu-id="3e836-203">**Gateway** – This is hello default gateway that should be used by this interface when it attempts toocommunicate with nodes that are not within hello same IP address space (subnet).</span></span> <span data-ttu-id="3e836-204">hello 預設閘道必須是在 hello 相同位址空間 （子網路） 作為 hello 介面 IP 位址，由 hello 子網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="3e836-204">hello default gateway must be in hello same address space (subnet) as hello interface IP address, as determined by hello subnet mask.</span></span>
* <span data-ttu-id="3e836-205">**固定 IP 位址**-這個欄位可供使用，只有當您設定 hello DATA 0 時，介面。</span><span class="sxs-lookup"><span data-stu-id="3e836-205">**Fixed IP address** – This field is available only while you configure hello DATA 0 interface.</span></span> <span data-ttu-id="3e836-206">更新或疑難排解 hello 裝置等作業，您可能需要 tooconnect 直接 toohello 裝置控制站。</span><span class="sxs-lookup"><span data-stu-id="3e836-206">For operations such as updates or troubleshooting hello device, you may need tooconnect directly toohello device controller.</span></span> <span data-ttu-id="3e836-207">hello 固定 IP 位址可以是使用的 tooaccess 作用中的 hello 和您的裝置上的 hello 被動控制器。</span><span class="sxs-lookup"><span data-stu-id="3e836-207">hello fixed IP address can be used tooaccess both hello active and hello passive controller on your device.</span></span>

> [!NOTE]
> * <span data-ttu-id="3e836-208">tooensure 正常運作，請確認 hello 介面速度和雙工 hello 參數，每個裝置介面連線到。</span><span class="sxs-lookup"><span data-stu-id="3e836-208">tooensure proper operation, verify hello interface speed and duplex on hello switch that each device interface is connected to.</span></span> <span data-ttu-id="3e836-209">交換器介面應該針對乙太網路 (1000 Mbps) 進行交涉或設定，且為全雙工。</span><span class="sxs-lookup"><span data-stu-id="3e836-209">Switch interfaces should either negotiate with or be configured for Gigabit Ethernet (1000 Mbps) and be full-duplex.</span></span> <span data-ttu-id="3e836-210">介面以較低速度運作或為半雙工時將導致效能問題。</span><span class="sxs-lookup"><span data-stu-id="3e836-210">Interfaces operating at slower speeds or in half-duplex will result in performance issues.</span></span>
> * <span data-ttu-id="3e836-211">toominimize 中斷與停機時間，我們建議您啟用 portfast hello 交換器連接埠的 hello iSCSI 網路介面，您的裝置會連接到的每個。</span><span class="sxs-lookup"><span data-stu-id="3e836-211">toominimize disruptions and downtime, we recommend that you enable portfast on each of hello switch ports that hello iSCSI network interface of your device will be connecting to.</span></span> <span data-ttu-id="3e836-212">這可確保網路連線可以快速建立的容錯移轉的 hello 事件中。</span><span class="sxs-lookup"><span data-stu-id="3e836-212">This will ensure that network connectivity can be established quickly in hello event of a failover.</span></span>

### <a name="configure-data-0"></a><span data-ttu-id="3e836-213">設定 DATA 0</span><span class="sxs-lookup"><span data-stu-id="3e836-213">Configure DATA 0</span></span>

<span data-ttu-id="3e836-214">DATA 0 依預設已啟用雲端功能。</span><span class="sxs-lookup"><span data-stu-id="3e836-214">DATA 0 is cloud-enabled by default.</span></span> <span data-ttu-id="3e836-215">在設定 DATA 0 時，您也是必要的 tooconfigure 兩個固定的 IP 位址，一個用於每個控制站。</span><span class="sxs-lookup"><span data-stu-id="3e836-215">When configuring DATA 0, you are also required tooconfigure two fixed IP addresses, one for each controller.</span></span> <span data-ttu-id="3e836-216">這些固定 IP 位址可以是使用的 tooaccess hello 裝置控制站直接與您 hello 裝置，或當您存取 hello 用途疑難排解的 hello 控制站上安裝更新時很有用。</span><span class="sxs-lookup"><span data-stu-id="3e836-216">These fixed IP addresses can be used tooaccess hello device controllers directly and are useful when you install updates on hello device or when you access hello controllers for hello purpose of troubleshooting.</span></span>

<span data-ttu-id="3e836-217">您可以重新設定 hello 固定 IP 透過 hello 資料 0 設定 刀鋒視窗的控制站。</span><span class="sxs-lookup"><span data-stu-id="3e836-217">You can reconfigure hello fixed IP controllers via hello DATA 0 settings blade.</span></span>

![設定網路介面 - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> <span data-ttu-id="3e836-219">hello 固定 hello 控制站的 IP 位址可用來服務 hello 更新 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="3e836-219">hello fixed IP addresses for hello controller are used for servicing hello updates toohello device.</span></span> <span data-ttu-id="3e836-220">因此，hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="3e836-220">Therefore, hello fixed IPs must be routable and able tooconnect toohello Internet.</span></span>

### <a name="configure-data-1---data-5"></a><span data-ttu-id="3e836-221">設定 DATA 1 - DATA 5</span><span class="sxs-lookup"><span data-stu-id="3e836-221">Configure DATA 1 - DATA 5</span></span>

<span data-ttu-id="3e836-222">資料 1-DATA 5 網路介面，您可以設定所有 hello 網路 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="3e836-222">For DATA 1 - DATA 5 network interfaces, you can configure all hello network settings as shown in hello following screenshot:</span></span>

![設定網路介面 DATA 1 - DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a><span data-ttu-id="3e836-224">交換或重新指派 IP</span><span class="sxs-lookup"><span data-stu-id="3e836-224">Swap or reassign IPs</span></span>

<span data-ttu-id="3e836-225">目前，若有任何網路介面上 hello 控制器會指派 VIP 給使用中 (由 hello 同一部裝置或 hello 網路中的另一個裝置)，然後 hello 控制器將會容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="3e836-225">Currently, if any network interface on hello controller is assigned a VIP that is in use (by hello same device or another device in hello network), then hello controller will fail over.</span></span> <span data-ttu-id="3e836-226">如果您交換或重新指派裝置網路介面的 VIP 時，必須遵循適當的程序，否則可能會建立重複的 IP。</span><span class="sxs-lookup"><span data-stu-id="3e836-226">If you swap or reassign VIPs for a device network interface, you must follow a proper procedure as you could create a duplicate IP situation.</span></span>

<span data-ttu-id="3e836-227">執行下列步驟 tooswap hello 或重新指派任何 hello 網路介面的 hello Vip:</span><span class="sxs-lookup"><span data-stu-id="3e836-227">Perform hello following steps tooswap or reassign hello VIPs for any of hello network interfaces:</span></span>

#### <a name="tooreassign-ips"></a><span data-ttu-id="3e836-228">tooreassign Ip</span><span class="sxs-lookup"><span data-stu-id="3e836-228">tooreassign IPs</span></span>

1. <span data-ttu-id="3e836-229">清除 hello 這兩個介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3e836-229">Clear hello IP address for both interfaces.</span></span>
2. <span data-ttu-id="3e836-230">清除 hello IP 位址之後，指派 toohello 個別介面 hello 新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3e836-230">After hello IP addresses are cleared, assign hello new IP addresses toohello respective interfaces.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e836-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e836-231">Next steps</span></span>

* <span data-ttu-id="3e836-232">了解如何太[為您的 StorSimple 裝置設定 MPIO](storsimple-8000-configure-mpio-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="3e836-232">Learn how too[configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span>
* <span data-ttu-id="3e836-233">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="3e836-233">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

