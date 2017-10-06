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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>使用遠端桌面 tooconnect tooa Microsoft Azure Linux VM
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 Hello 更新此文件的資源管理員版本，請參閱[這裡](../use-remote-desktop.md)。

## <a name="overview"></a>概觀
RDP (遠端桌面通訊協定) 是用於 Windows 的專屬通訊協定。 我們要如何從遠端使用 RDP tooconnect tooa Linux VM （虛擬機器）？

本指南可讓您 hello 回應 ！ 它可協助您 tooinstall 和組態 xrdp 可讓您從 Windows 電腦，遠端桌面連線 tooit 您 Microsoft Azure Linux VM 上。 我們將使用在本指南中的 hello 範例以執行 Ubuntu 或 OpenSUSE Linux VM。

hello xrdp 工具是開放來源，可讓您 tooconnect RDP 伺服器從 Windows 電腦使用遠端桌面，在 Linux 伺服器。 RDP 擁有比 VNC (虛擬網路運算) 更好的效能。 VNC 使用 JPEG 品質圖形進行轉譯，而且速度可能很慢，RDP 的速度很快，且圖形品質非常清晰。

> [!NOTE]
> 您必須已經有執行 Linux 的 Microsoft Azure VM。 toocreate 及設定 Linux VM，請參閱 hello [Azure Linux VM 教學課程](createportal.md)。
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>建立遠端桌面的端點
我們將使用遠端桌面的 hello 3389 的預設端點，此文件中。設定為 3389 端點`Remote Desktop`tooyour Linux VM 類似下面的：

![image](./media/remote-desktop/endpoint-for-linux-server.png)

如果您不知道如何註冊您的 VM 端點 tooset 查看[本指南](setup-endpoints.md)。

## <a name="install-gnome-desktop"></a>安裝 Gnome 桌面
連接 tooyour Linux VM 透過`putty`，並安裝`Gnome Desktop`。

針對 Ubuntu，使用：

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


針對 OpenSUSE，使用︰

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>安裝 xrdp
針對 Ubuntu，使用：

    #sudo apt-get install xrdp

針對 OpenSUSE，使用︰

> [!NOTE]
> Hello OpenSUSE 以更新版本 hello hello 下列命令中使用的版本。 下列的 hello 範例是針對`OpenSUSE 13.2`。
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>在開機時啟動 xrdp 並設定 xdrp 服務
針對 OpenSUSE，使用︰

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

對於 Ubuntu，安裝之後會啟動 xrdp，並在開機時自動啟用。

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>如果您使用比 Ubuntu 12.04LTS 更新的 Ubuntu 版本則使用 xfce
因為 xrdp hello 目前版本不支援 Gnome 桌面 Ubuntu 版本晚於 Ubuntu 12.04LTS，我們將使用`xfce`桌面改為。

tooinstall `xfce`，使用此命令：

    #sudo apt-get install xubuntu-desktop

然後使用此命令啟用 `xfce`：

    #echo xfce4-session >~/.xsession

編輯 hello 設定檔`/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

加入 hello 行`xfce4-session`hello 一行之前`/etc/X11/Xsession`。

toorestart hello xrdp 服務，可使用此：

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>從 Windows 電腦連接 Linux VM
在 Windows 電腦上，啟動 hello 遠端桌面用戶端，並輸入您的 Linux VM 的 DNS 名稱。 或移 toohello hello Azure 入口網站中 VM 的儀表板，然後按一下`Connect`tooconnect Linux VM。 在此情況下，您會看到 hello 登入視窗：

![image](./media/remote-desktop/no2.png)

Hello 使用者名稱和密碼登入您的 Linux VM。

## <a name="next-steps"></a>後續步驟
如需使用 xrdp 的相關詳細資訊，請參閱 [http://www.xrdp.org/](http://www.xrdp.org/) \(英文\)。
