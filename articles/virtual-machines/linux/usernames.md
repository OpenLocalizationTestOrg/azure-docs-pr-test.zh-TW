---
title: "aaaSelecting 適用於 Linux 的使用者名稱 |Microsoft 文件"
description: "了解如何 tooselect 使用者名稱在 Azure 中 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>在 Azure 上選取適用於 Linux 的使用者名稱
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

在佈建在 Azure 上的 Linux 虛擬機器時，您必須指定 hello 您稍後可以使用 toolog 到 hello VM 的非根使用者名稱。 您可以選擇 hello hello 新的使用者名稱，或如果透過佈建 hello Azure 傳統入口網站，您可以接受 hello 預設名稱 「 azureuser"。

在大部分情況下這位使用者不存在於 hello 基底映像，並將 hello 佈建程序期間建立。 如果 hello 使用者存在於 hello 基底 VM 映像，然後 hello Azure Linux 代理程式只會設定 hello 密碼及/或根據 hello 資訊建立 hello VM 時，您會指定該使用者的 SSH 金鑰。

**不過**，Linux 會定義一組不應該使用的使用者名稱。 佈建程序將 hello**失敗**如果您嘗試 tooprovision Linux VM，使用現有的系統使用者，定義為具有 UID 0-99 之間的使用者。 典型的範例為 hello`root`使用者具有 UID 0。

* 另請參閱： [Linux 標準基礎 - 使用者 ID 範圍](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

hello 以下是 CentOS 和 Ubuntu，您應該避免使用佈建在 Azure 上的 Linux 虛擬機器時通用的內建的系統使用者的清單。 這份清單不只是範例，請參閱 toohello 文件的發佈 tooensure 該 hello 使用者名稱與現有的系統使用者選擇 不會衝突。

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

