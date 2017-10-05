---
title: "從遠端桌面連接至 Linux VM | Microsoft Docs"
description: "了解如何安裝和設定遠端桌面，以連接至傳統部署模型的 Microsoft Azure Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: 68031d548bdbeda9a83d1bceaaea7c5bbcab3188
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a><span data-ttu-id="7e091-103">使用遠端桌面連接至 Microsoft Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="7e091-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7e091-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="7e091-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7e091-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="7e091-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7e091-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="7e091-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7e091-107">如需本文已更新的 Resource Manager 版本，請參閱[這裡](../use-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="7e091-107">For the updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7e091-108">概觀</span><span class="sxs-lookup"><span data-stu-id="7e091-108">Overview</span></span>
<span data-ttu-id="7e091-109">RDP (遠端桌面通訊協定) 是用於 Windows 的專屬通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7e091-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="7e091-110">我們要如何使用 RDP 從遠端連接到 Linux VM (虛擬機器)？</span><span class="sxs-lookup"><span data-stu-id="7e091-110">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="7e091-111">本指南會為您提供答案！</span><span class="sxs-lookup"><span data-stu-id="7e091-111">This guidance will give you the answer!</span></span> <span data-ttu-id="7e091-112">它會協助您在 Microsoft Azure Linux VM 上安裝及設定 xrdp，這會讓您能夠從 Windows 電腦使用遠端桌面來連接它。</span><span class="sxs-lookup"><span data-stu-id="7e091-112">It will help you to install and config xrdp on your Microsoft Azure Linux VM, which lets you connect to it with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="7e091-113">在本指南中我們會使用執行 Ubuntu 或 OpenSUSE 的 Linux VM 做為範例。</span><span class="sxs-lookup"><span data-stu-id="7e091-113">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span></span>

<span data-ttu-id="7e091-114">xrdp 工具是一個開放原始碼 RDP 伺服器，可讓您從 Windows 電腦使用遠端桌面連接 Linux 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7e091-114">The xrdp tool is an open source RDP server that allows you to connect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="7e091-115">RDP 擁有比 VNC (虛擬網路運算) 更好的效能。</span><span class="sxs-lookup"><span data-stu-id="7e091-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="7e091-116">VNC 使用 JPEG 品質圖形進行轉譯，而且速度可能很慢，RDP 的速度很快，且圖形品質非常清晰。</span><span class="sxs-lookup"><span data-stu-id="7e091-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="7e091-117">您必須已經有執行 Linux 的 Microsoft Azure VM。</span><span class="sxs-lookup"><span data-stu-id="7e091-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="7e091-118">若要建立並設定 Linux VM，請參閱 [Azure Linux VM 教學課程](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="7e091-118">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="7e091-119">建立遠端桌面的端點</span><span class="sxs-lookup"><span data-stu-id="7e091-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="7e091-120">我們將對本文件中的遠端桌面使用預設端點 3389。</span><span class="sxs-lookup"><span data-stu-id="7e091-120">We will use the default endpoint 3389 for Remote Desktop in this doc.</span></span> <span data-ttu-id="7e091-121">將 3389 端點設定為 Linux VM 的 `Remote Desktop`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7e091-121">Set up 3389 endpoint as `Remote Desktop` to your Linux VM like below:</span></span>

![image](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="7e091-123">如果您不知道如何為 VM 設定端點，請參閱[本指南](setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="7e091-123">If you don't know how to set up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="7e091-124">安裝 Gnome 桌面</span><span class="sxs-lookup"><span data-stu-id="7e091-124">Install Gnome Desktop</span></span>
<span data-ttu-id="7e091-125">透過 `putty` 連接到 Linux VM，然後安裝 `Gnome Desktop`。</span><span class="sxs-lookup"><span data-stu-id="7e091-125">Connect to your Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="7e091-126">針對 Ubuntu，使用：</span><span class="sxs-lookup"><span data-stu-id="7e091-126">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="7e091-127">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="7e091-127">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="7e091-128">安裝 xrdp</span><span class="sxs-lookup"><span data-stu-id="7e091-128">Install xrdp</span></span>
<span data-ttu-id="7e091-129">針對 Ubuntu，使用：</span><span class="sxs-lookup"><span data-stu-id="7e091-129">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="7e091-130">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="7e091-130">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="7e091-131">在以下命令中，用您正在使用的版本更新 OpenSUSE 版本。</span><span class="sxs-lookup"><span data-stu-id="7e091-131">Update the OpenSUSE version with the version you are using in the following command.</span></span> <span data-ttu-id="7e091-132">下方是 `OpenSUSE 13.2` 的範例。</span><span class="sxs-lookup"><span data-stu-id="7e091-132">The example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="7e091-133">在開機時啟動 xrdp 並設定 xdrp 服務</span><span class="sxs-lookup"><span data-stu-id="7e091-133">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="7e091-134">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="7e091-134">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="7e091-135">對於 Ubuntu，安裝之後會啟動 xrdp，並在開機時自動啟用。</span><span class="sxs-lookup"><span data-stu-id="7e091-135">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="7e091-136">如果您使用比 Ubuntu 12.04LTS 更新的 Ubuntu 版本則使用 xfce</span><span class="sxs-lookup"><span data-stu-id="7e091-136">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="7e091-137">由於 xrdp 目前的版本不支援比 Ubuntu 12.04LTS 更新的 Ubuntu 版本 Gnome 桌面，因此我們將改用 `xfce` 桌面。</span><span class="sxs-lookup"><span data-stu-id="7e091-137">Because the current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="7e091-138">若要安裝 `xfce`，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="7e091-138">To install `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="7e091-139">然後使用此命令啟用 `xfce`：</span><span class="sxs-lookup"><span data-stu-id="7e091-139">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="7e091-140">編輯組態檔 `/etc/xrdp/startwm.sh`：</span><span class="sxs-lookup"><span data-stu-id="7e091-140">Edit the config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="7e091-141">在 `/etc/X11/Xsession` 一行前面加入 `xfce4-session` 這一行。</span><span class="sxs-lookup"><span data-stu-id="7e091-141">Add the line `xfce4-session` before the line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="7e091-142">若要重新啟動 xrdp 服務，請使用此：</span><span class="sxs-lookup"><span data-stu-id="7e091-142">To restart the xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="7e091-143">從 Windows 電腦連接 Linux VM</span><span class="sxs-lookup"><span data-stu-id="7e091-143">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="7e091-144">在 Windows 電腦中啟動遠端桌面用戶端，並輸入您的 Linux VM DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="7e091-144">In a Windows machine, start the Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="7e091-145">或在 Azure 入口網站中移至您 VM 的儀表板，並按一下 `Connect` 來連接 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="7e091-145">Or go to the Dashboard of your VM in the Azure portal and click `Connect` to connect your Linux VM.</span></span> <span data-ttu-id="7e091-146">這時您會看到登入視窗：</span><span class="sxs-lookup"><span data-stu-id="7e091-146">In that case, you see the login window:</span></span>

![image](./media/remote-desktop/no2.png)

<span data-ttu-id="7e091-148">請使用您 Linux VM 的使用者名稱和密碼登入。</span><span class="sxs-lookup"><span data-stu-id="7e091-148">Log in with the user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e091-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e091-149">Next steps</span></span>
<span data-ttu-id="7e091-150">如需使用 xrdp 的相關詳細資訊，請參閱 [http://www.xrdp.org/](http://www.xrdp.org/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="7e091-150">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
