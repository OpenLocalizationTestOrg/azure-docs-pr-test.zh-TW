---
title: "適用於 Linux Vm aaaConfiguring DHCPv6 |Microsoft 文件"
description: "如何 tooconfigure DHCPv6 適用於 Linux Vm。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a>設定 Linux VM 的 DHCPv6

有些 hello Azure Marketplace 中的 hello Linux 虛擬機器映像沒有 DHCPv6 預設設定。 IPv6-DHCPv6 toosupport 必須內您要使用的 hello Linux 作業系統發佈中設定。 不同 Linux 散發套件的 DHCPv6 設定方式不同，因為它們使用不同的套件。

> [!NOTE]
> 已預先設定 DHCPv6 hello Azure Marketplace 中最近的 SUSE Linux 和 CoreOS 映像。 使用這些映像不需要再進行額外的變更。

本文件說明如何 tooenable DHCPv6，讓您的 Linux 虛擬機器取得 IPv6 位址。

> [!WARNING]
> 不當編輯網路組態檔可能會導致您 toolose 網路存取 tooyour VM。 我們建議您先在非生產系統上測試組態變更。 這篇文章中的 hello 指示 hello 的 hello Azure Marketplace 中的 hello Linux 映像的最新版本上測試。 您特定的 Linux 版本的更詳細的指示，請參閱 hello 文件。

## <a name="ubuntu"></a>Ubuntu

1. 編輯 hello 檔案`/etc/dhcp/dhclient6.conf`並加入以下的 hello:

        timeout 10;

2. 以下列組態的 hello 編輯 hello hello eth0 介面的網路設定：

   * 在**Ubuntu 12.04 和 14.04**，編輯 hello 檔案`/etc/network/interfaces.d/eth0.cfg`
   * 在**Ubuntu 16.04**，編輯 hello 檔案`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. 更新 IPv6 位址︰

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. 編輯 hello 檔案`/etc/dhcp/dhclient6.conf`並加入以下的 hello:

        timeout 10;

2. 編輯 hello 檔案`/etc/network/interfaces`並加入下列組態的 hello:

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. 更新 IPv6 位址︰

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. 編輯 hello 檔案`/etc/sysconfig/network`並加入下列參數的 hello:

        NETWORKING_IPV6=yes

2. 編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列兩個參數的 hello:

        IPV6INIT=yes
        DHCPV6C=yes

3. 更新 IPv6 位址︰

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 & openSUSE 13

在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。 使用這些映像不需要再進行額外的變更。 如果您有根據舊或自訂 SUSE 映像的 VM，使用下列步驟的 hello:

1. 安裝 hello`dhcp-client`封裝，如有需要：

    ```bash
    sudo zypper install dhcp-client
    ```

2. 編輯 hello 檔案`/etc/sysconfig/network/ifcfg-eth0`並加入下列參數的 hello:

        DHCLIENT6_MODE='managed'

3. 更新 hello IPv6 位址：

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 和 openSUSE Leap

在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。 使用這些映像不需要再進行額外的變更。 如果您有根據舊或自訂 SUSE 映像的 VM，使用下列步驟的 hello:

1. 編輯 hello 檔案`/etc/sysconfig/network/ifcfg-eth0`和取代此參數

        #BOOTPROTO='dhcp4'

    以 hello 下列值：

        BOOTPROTO='dhcp'

2. 新增 hello 參數後面太`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. 更新 hello IPv6 位址：

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

在 Azure 中最新的 SLES 映像已預先設定 DHCPv6。 使用這些映像不需要再進行額外的變更。 如果您有根據舊或自訂 CoreOS 映像的 VM，使用下列步驟的 hello:

1. 編輯 hello 檔案`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. 更新 hello IPv6 位址：

    ```bash
    sudo systemctl restart systemd-networkd
    ```
