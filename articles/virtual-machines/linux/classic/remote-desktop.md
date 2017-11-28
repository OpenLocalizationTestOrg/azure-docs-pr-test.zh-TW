---
title: "aaaRemote 桌面 tooa Linux VM |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定遠端桌面 tooconnect tooa Microsoft Azure Linux VM hello 傳統部署模型"
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
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="d64d3-103">使用遠端桌面 tooconnect tooa Microsoft Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="d64d3-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d64d3-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d64d3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d64d3-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d64d3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d64d3-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="d64d3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d64d3-107">Hello 更新此文件的資源管理員版本，請參閱[這裡](../use-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="d64d3-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d64d3-108">概觀</span><span class="sxs-lookup"><span data-stu-id="d64d3-108">Overview</span></span>
<span data-ttu-id="d64d3-109">RDP (遠端桌面通訊協定) 是用於 Windows 的專屬通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d64d3-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="d64d3-110">我們要如何從遠端使用 RDP tooconnect tooa Linux VM （虛擬機器）？</span><span class="sxs-lookup"><span data-stu-id="d64d3-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="d64d3-111">本指南可讓您 hello 回應 ！</span><span class="sxs-lookup"><span data-stu-id="d64d3-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="d64d3-112">它可協助您 tooinstall 和組態 xrdp 可讓您從 Windows 電腦，遠端桌面連線 tooit 您 Microsoft Azure Linux VM 上。</span><span class="sxs-lookup"><span data-stu-id="d64d3-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="d64d3-113">我們將使用在本指南中的 hello 範例以執行 Ubuntu 或 OpenSUSE Linux VM。</span><span class="sxs-lookup"><span data-stu-id="d64d3-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="d64d3-114">hello xrdp 工具是開放來源，可讓您 tooconnect RDP 伺服器從 Windows 電腦使用遠端桌面，在 Linux 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d64d3-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="d64d3-115">RDP 擁有比 VNC (虛擬網路運算) 更好的效能。</span><span class="sxs-lookup"><span data-stu-id="d64d3-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="d64d3-116">VNC 使用 JPEG 品質圖形進行轉譯，而且速度可能很慢，RDP 的速度很快，且圖形品質非常清晰。</span><span class="sxs-lookup"><span data-stu-id="d64d3-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="d64d3-117">您必須已經有執行 Linux 的 Microsoft Azure VM。</span><span class="sxs-lookup"><span data-stu-id="d64d3-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="d64d3-118">toocreate 及設定 Linux VM，請參閱 hello [Azure Linux VM 教學課程](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d64d3-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="d64d3-119">建立遠端桌面的端點</span><span class="sxs-lookup"><span data-stu-id="d64d3-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="d64d3-120">我們將使用遠端桌面的 hello 3389 的預設端點，此文件中。設定為 3389 端點`Remote Desktop`tooyour Linux VM 類似下面的：</span><span class="sxs-lookup"><span data-stu-id="d64d3-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![image](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="d64d3-122">如果您不知道如何註冊您的 VM 端點 tooset 查看[本指南](setup-endpoints.md)。</span><span class="sxs-lookup"><span data-stu-id="d64d3-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="d64d3-123">安裝 Gnome 桌面</span><span class="sxs-lookup"><span data-stu-id="d64d3-123">Install Gnome Desktop</span></span>
<span data-ttu-id="d64d3-124">連接 tooyour Linux VM 透過`putty`，並安裝`Gnome Desktop`。</span><span class="sxs-lookup"><span data-stu-id="d64d3-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="d64d3-125">針對 Ubuntu，使用：</span><span class="sxs-lookup"><span data-stu-id="d64d3-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="d64d3-126">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="d64d3-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="d64d3-127">安裝 xrdp</span><span class="sxs-lookup"><span data-stu-id="d64d3-127">Install xrdp</span></span>
<span data-ttu-id="d64d3-128">針對 Ubuntu，使用：</span><span class="sxs-lookup"><span data-stu-id="d64d3-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="d64d3-129">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="d64d3-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="d64d3-130">Hello OpenSUSE 以更新版本 hello hello 下列命令中使用的版本。</span><span class="sxs-lookup"><span data-stu-id="d64d3-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="d64d3-131">下列的 hello 範例是針對`OpenSUSE 13.2`。</span><span class="sxs-lookup"><span data-stu-id="d64d3-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="d64d3-132">在開機時啟動 xrdp 並設定 xdrp 服務</span><span class="sxs-lookup"><span data-stu-id="d64d3-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="d64d3-133">針對 OpenSUSE，使用︰</span><span class="sxs-lookup"><span data-stu-id="d64d3-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="d64d3-134">對於 Ubuntu，安裝之後會啟動 xrdp，並在開機時自動啟用。</span><span class="sxs-lookup"><span data-stu-id="d64d3-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="d64d3-135">如果您使用比 Ubuntu 12.04LTS 更新的 Ubuntu 版本則使用 xfce</span><span class="sxs-lookup"><span data-stu-id="d64d3-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="d64d3-136">因為 xrdp hello 目前版本不支援 Gnome 桌面 Ubuntu 版本晚於 Ubuntu 12.04LTS，我們將使用`xfce`桌面改為。</span><span class="sxs-lookup"><span data-stu-id="d64d3-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="d64d3-137">tooinstall `xfce`，使用此命令：</span><span class="sxs-lookup"><span data-stu-id="d64d3-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="d64d3-138">然後使用此命令啟用 `xfce`：</span><span class="sxs-lookup"><span data-stu-id="d64d3-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="d64d3-139">編輯 hello 設定檔`/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="d64d3-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="d64d3-140">加入 hello 行`xfce4-session`hello 一行之前`/etc/X11/Xsession`。</span><span class="sxs-lookup"><span data-stu-id="d64d3-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="d64d3-141">toorestart hello xrdp 服務，可使用此：</span><span class="sxs-lookup"><span data-stu-id="d64d3-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="d64d3-142">從 Windows 電腦連接 Linux VM</span><span class="sxs-lookup"><span data-stu-id="d64d3-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="d64d3-143">在 Windows 電腦上，啟動 hello 遠端桌面用戶端，並輸入您的 Linux VM 的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d64d3-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="d64d3-144">或移 toohello hello Azure 入口網站中 VM 的儀表板，然後按一下`Connect`tooconnect Linux VM。</span><span class="sxs-lookup"><span data-stu-id="d64d3-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="d64d3-145">在此情況下，您會看到 hello 登入視窗：</span><span class="sxs-lookup"><span data-stu-id="d64d3-145">In that case, you see hello login window:</span></span>

![image](./media/remote-desktop/no2.png)

<span data-ttu-id="d64d3-147">Hello 使用者名稱和密碼登入您的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="d64d3-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d64d3-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d64d3-148">Next steps</span></span>
<span data-ttu-id="d64d3-149">如需使用 xrdp 的相關詳細資訊，請參閱 [http://www.xrdp.org/](http://www.xrdp.org/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d64d3-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
