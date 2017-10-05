---
title: "修改 StorSimple 8000 系列裝置上的 DATA 0 設定 | Microsoft Docs"
description: "了解如何使用 Windows PowerShell for StorSimple 重新設定 StorSimple 裝置上的 DATA 0 網路介面。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="2206f-103">修改 StorSimple 8000 系列裝置上的 DATA 0 網路介面設定</span><span class="sxs-lookup"><span data-stu-id="2206f-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="2206f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2206f-104">Overview</span></span>

<span data-ttu-id="2206f-105">Microsoft Azure StorSimple 裝置有 6 個網路介面，從 DATA 0 至 DATA 5。</span><span class="sxs-lookup"><span data-stu-id="2206f-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="2206f-106">DATA 0 介面一律透過 Windows PowerShell 介面或序列主控台設定，且已自動啟用雲端功能。</span><span class="sxs-lookup"><span data-stu-id="2206f-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="2206f-107">請注意，您無法透過 Azure 入口網站設定 DATA 0 網路介面。</span><span class="sxs-lookup"><span data-stu-id="2206f-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="2206f-108">DATA 0 介面會在初始部署 StorSimple 裝置期間，透過安裝精靈進行第一次設定。</span><span class="sxs-lookup"><span data-stu-id="2206f-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="2206f-109">當裝置處於操作模式時，您可能需要重新進行 DATA 0 設定。</span><span class="sxs-lookup"><span data-stu-id="2206f-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="2206f-110">本教學課程提供兩種修改 DATA 0 網路設定的方法，皆需透過 Windows PowerShell for StorSimple 進行。</span><span class="sxs-lookup"><span data-stu-id="2206f-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="2206f-111">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="2206f-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="2206f-112">透過安裝精靈修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="2206f-113">透過 `Set-HcsNetInterface` Cmdlet 修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="2206f-114">透過安裝精靈修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="2206f-115">您可以連接至 StorSimple 裝置的 Windows PowerShell 介面並啟動安裝精靈工作階段以重新設定 DATA 0 網路設定。</span><span class="sxs-lookup"><span data-stu-id="2206f-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="2206f-116">執行下列步驟以修改 DATA 0 設定：</span><span class="sxs-lookup"><span data-stu-id="2206f-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="2206f-117">透過安裝精靈修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="2206f-118">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="2206f-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="2206f-119">出現提示時，提供**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="2206f-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="2206f-120">預設密碼為 `Password1`。</span><span class="sxs-lookup"><span data-stu-id="2206f-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="2206f-121">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="2206f-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="2206f-122">安裝精靈隨即出現，以協助您設定裝置的 DATA 0 介面。</span><span class="sxs-lookup"><span data-stu-id="2206f-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="2206f-123">提供 IP 位址、閘道器和網路遮罩的新值。</span><span class="sxs-lookup"><span data-stu-id="2206f-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="2206f-124">固定控制器 IP 必須在 Azure 入口網站中透過 StorSimple 裝置的 [網路設定] 刀鋒視窗重新設定。</span><span class="sxs-lookup"><span data-stu-id="2206f-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="2206f-125">如需詳細資訊，請移至 [修改網路介面](storsimple-8000-modify-device-config.md#modify-network-interfaces)。</span><span class="sxs-lookup"><span data-stu-id="2206f-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="2206f-126">透過 Set-HcsNetInterface cmdlet 修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="2206f-127">重新設定 DATA 0 網路介面的替代方式為透過使用 `Set-HcsNetInterface` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2206f-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="2206f-128">cmdlet 是從 StorSimple 裝置的 Windows PowerShell 介面執行。</span><span class="sxs-lookup"><span data-stu-id="2206f-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="2206f-129">使用此程序時，控制器固定 IP 也可以在此設定。</span><span class="sxs-lookup"><span data-stu-id="2206f-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="2206f-130">執行下列步驟以修改 DATA 0 設定：</span><span class="sxs-lookup"><span data-stu-id="2206f-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="2206f-131">透過 Set-HcsNetInterface cmdlet 修改 DATA 0 網路設定</span><span class="sxs-lookup"><span data-stu-id="2206f-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="2206f-132">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="2206f-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="2206f-133">出現提示時，提供裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="2206f-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="2206f-134">預設密碼為 `Password1`。</span><span class="sxs-lookup"><span data-stu-id="2206f-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="2206f-135">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="2206f-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="2206f-136">在角括弧內鍵入下列 DATA 0 的值：</span><span class="sxs-lookup"><span data-stu-id="2206f-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="2206f-137">IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="2206f-137">IPv4 address</span></span>
   * <span data-ttu-id="2206f-138">IPv4 閘道</span><span class="sxs-lookup"><span data-stu-id="2206f-138">IPv4 gateway</span></span>
   * <span data-ttu-id="2206f-139">IPv4 子網路遮罩</span><span class="sxs-lookup"><span data-stu-id="2206f-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="2206f-140">控制器 0 的固定的 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="2206f-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="2206f-141">控制器 1 的固定的 IPv4 位址</span><span class="sxs-lookup"><span data-stu-id="2206f-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="2206f-142">如需使用此 Cmdlet 的詳細資訊，請移至 [Windows PowerShell for StorSimple Cmdlet 參考](https://technet.microsoft.com/library/dn688161.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2206f-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2206f-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2206f-143">Next steps</span></span>
* <span data-ttu-id="2206f-144">若要設定 DATA 0 以外的網路介面，您可以使用[在 Azure 入口網站中設定網路設定](storsimple-8000-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="2206f-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="2206f-145">如果您在設定您的網路介面時遇到任何問題，請參閱 [疑難排解部署問題](storsimple-troubleshoot-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="2206f-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

