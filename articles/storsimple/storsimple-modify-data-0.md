---
title: "aaaModify hello DATA 0 上的 StorSimple 裝置的設定 |Microsoft 文件"
description: "深入了解如何 toouse Windows PowerShell for StorSimple tooreconfigure hello StorSimple 裝置上的 DATA 0 網路介面。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="ad15c-103">修改您的 StorSimple 裝置上 hello DATA 0 網路介面設定</span><span class="sxs-lookup"><span data-stu-id="ad15c-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="ad15c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ad15c-104">Overview</span></span>
<span data-ttu-id="ad15c-105">Microsoft Azure StorSimple 裝置有六個網路介面，從 DATA 0 tooDATA 5。</span><span class="sxs-lookup"><span data-stu-id="ad15c-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="ad15c-106">hello DATA 0 介面一律透過 hello Windows PowerShell 介面或 hello 序列主控台中，設定，而且自動具備雲端功能。</span><span class="sxs-lookup"><span data-stu-id="ad15c-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="ad15c-107">請注意，您無法設定 DATA 0 網路介面，透過 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="ad15c-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="ad15c-108">hello DATA 0 介面先 hello 安裝精靈的 hello StorSimple 裝置的初始部署時設定。</span><span class="sxs-lookup"><span data-stu-id="ad15c-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="ad15c-109">作業模式 hello 裝置時，您可能需要 tooreconfigure DATA 0 的設定。</span><span class="sxs-lookup"><span data-stu-id="ad15c-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="ad15c-110">本教學課程提供兩種方法 toomodify DATA 0 網路設定，同時透過 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="ad15c-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="ad15c-111">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="ad15c-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="ad15c-112">修改 DATA 0 網路設定透過 hello 安裝精靈</span><span class="sxs-lookup"><span data-stu-id="ad15c-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="ad15c-113">修改 DATA 0 網路設定，透過 hello `Set-HcsNetInterface` cmdlet</span><span class="sxs-lookup"><span data-stu-id="ad15c-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="ad15c-114">透過安裝精靈修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="ad15c-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="ad15c-115">您可以重新設定 DATA 0 網路設定，連線 toohello 您的 StorSimple 裝置的 Windows PowerShell 介面並啟動安裝精靈工作階段。</span><span class="sxs-lookup"><span data-stu-id="ad15c-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="ad15c-116">執行下列步驟 toomodify DATA 0 的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="ad15c-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="ad15c-117">透過安裝精靈的 toomodify DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="ad15c-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="ad15c-118">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="ad15c-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ad15c-119">當系統提示您提供 hello**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="ad15c-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="ad15c-120">hello 預設密碼為`Password1`。</span><span class="sxs-lookup"><span data-stu-id="ad15c-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="ad15c-121">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="ad15c-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="ad15c-122">安裝程式精靈 隨即出現 toohelp 設定 hello DATA 0 介面，您的裝置。</span><span class="sxs-lookup"><span data-stu-id="ad15c-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="ad15c-123">提供新值給 hello IP 位址、 閘道和網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="ad15c-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="ad15c-124">固定的控制器 Ip 將需要重新設定透過 hello toobe hello**設定**hello 的 StorSimple 裝置 hello Azure 傳統入口網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="ad15c-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="ad15c-125">如需詳細資訊，請移至太[修改網路介面](storsimple-modify-device-config.md#modify-network-interfaces)。</span><span class="sxs-lookup"><span data-stu-id="ad15c-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="ad15c-126">透過 Set-HcsNetInterface cmdlet 修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="ad15c-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="ad15c-127">替代方式 tooreconfigure DATA 0 網路介面是透過 hello hello 使用`Set-HcsNetInterface`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ad15c-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="ad15c-128">hello cmdlet 會從您的 StorSimple 裝置 hello Windows PowerShell 介面執行。</span><span class="sxs-lookup"><span data-stu-id="ad15c-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="ad15c-129">當使用此程序，也可以這裡設定 hello 控制器固定 Ip。</span><span class="sxs-lookup"><span data-stu-id="ad15c-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="ad15c-130">執行下列步驟 toomodify hello DATA 0 的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="ad15c-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="ad15c-131">透過 hello Set-hcsnetinterface cmdlet toomodify DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="ad15c-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="ad15c-132">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="ad15c-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="ad15c-133">當系統提示您提供 hello 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="ad15c-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="ad15c-134">hello 預設密碼為`Password1`。</span><span class="sxs-lookup"><span data-stu-id="ad15c-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="ad15c-135">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="ad15c-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="ad15c-136">在 hello 角度方括號中，輸入下列值的 DATA 0 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad15c-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="ad15c-137">IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="ad15c-137">IPv4 address</span></span>
   * <span data-ttu-id="ad15c-138">IPv4 閘道</span><span class="sxs-lookup"><span data-stu-id="ad15c-138">IPv4 gateway</span></span>
   * <span data-ttu-id="ad15c-139">IPv4 子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="ad15c-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="ad15c-140">控制器 0 的固定的 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="ad15c-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="ad15c-141">控制器 1 的固定的 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="ad15c-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="ad15c-142">如需 hello 使用這個指令程式的詳細資訊，請移至太[Windows PowerShell for StorSimple cmdlet 參考](https://technet.microsoft.com/library/dn688161.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ad15c-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad15c-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad15c-143">Next steps</span></span>
* <span data-ttu-id="ad15c-144">tooconfigure 不同於 DATA 0 網路介面，您可以使用 hello [hello Azure 傳統入口網站中的 [設定] 頁面](storsimple-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="ad15c-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="ad15c-145">如果您遇到任何問題，設定您的網路介面時，請參閱太[部署問題進行疑難排解](storsimple-troubleshoot-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ad15c-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

