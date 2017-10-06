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
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="42508-104">設定 Linux VM 的 DHCPv6</span><span class="sxs-lookup"><span data-stu-id="42508-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="42508-105">有些 hello Azure Marketplace 中的 hello Linux 虛擬機器映像沒有 DHCPv6 預設設定。</span><span class="sxs-lookup"><span data-stu-id="42508-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="42508-106">IPv6-DHCPv6 toosupport 必須內您要使用的 hello Linux 作業系統發佈中設定。</span><span class="sxs-lookup"><span data-stu-id="42508-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="42508-107">不同 Linux 散發套件的 DHCPv6 設定方式不同，因為它們使用不同的套件。</span><span class="sxs-lookup"><span data-stu-id="42508-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="42508-108">已預先設定 DHCPv6 hello Azure Marketplace 中最近的 SUSE Linux 和 CoreOS 映像。</span><span class="sxs-lookup"><span data-stu-id="42508-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="42508-109">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="42508-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="42508-110">本文件說明如何 tooenable DHCPv6，讓您的 Linux 虛擬機器取得 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="42508-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="42508-111">不當編輯網路組態檔可能會導致您 toolose 網路存取 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="42508-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="42508-112">我們建議您先在非生產系統上測試組態變更。</span><span class="sxs-lookup"><span data-stu-id="42508-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="42508-113">這篇文章中的 hello 指示 hello 的 hello Azure Marketplace 中的 hello Linux 映像的最新版本上測試。</span><span class="sxs-lookup"><span data-stu-id="42508-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="42508-114">您特定的 Linux 版本的更詳細的指示，請參閱 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="42508-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="42508-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="42508-115">Ubuntu</span></span>

1. <span data-ttu-id="42508-116">編輯 hello 檔案`/etc/dhcp/dhclient6.conf`並加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="42508-117">以下列組態的 hello 編輯 hello hello eth0 介面的網路設定：</span><span class="sxs-lookup"><span data-stu-id="42508-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="42508-118">在**Ubuntu 12.04 和 14.04**，編輯 hello 檔案`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="42508-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="42508-119">在**Ubuntu 16.04**，編輯 hello 檔案`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="42508-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="42508-120">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="42508-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="42508-121">Debian</span><span class="sxs-lookup"><span data-stu-id="42508-121">Debian</span></span>

1. <span data-ttu-id="42508-122">編輯 hello 檔案`/etc/dhcp/dhclient6.conf`並加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="42508-123">編輯 hello 檔案`/etc/network/interfaces`並加入下列組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="42508-124">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="42508-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="42508-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="42508-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="42508-126">編輯 hello 檔案`/etc/sysconfig/network`並加入下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="42508-127">編輯 hello 檔案`/etc/sysconfig/network-scripts/ifcfg-eth0`並加入下列兩個參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="42508-128">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="42508-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="42508-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="42508-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="42508-130">在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="42508-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="42508-131">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="42508-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="42508-132">如果您有根據舊或自訂 SUSE 映像的 VM，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="42508-133">安裝 hello`dhcp-client`封裝，如有需要：</span><span class="sxs-lookup"><span data-stu-id="42508-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="42508-134">編輯 hello 檔案`/etc/sysconfig/network/ifcfg-eth0`並加入下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="42508-135">更新 hello IPv6 位址：</span><span class="sxs-lookup"><span data-stu-id="42508-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="42508-136">SLES 12 和 openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="42508-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="42508-137">在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="42508-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="42508-138">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="42508-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="42508-139">如果您有根據舊或自訂 SUSE 映像的 VM，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="42508-140">編輯 hello 檔案`/etc/sysconfig/network/ifcfg-eth0`和取代此參數</span><span class="sxs-lookup"><span data-stu-id="42508-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="42508-141">以 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="42508-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="42508-142">新增 hello 參數後面太`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="42508-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="42508-143">更新 hello IPv6 位址：</span><span class="sxs-lookup"><span data-stu-id="42508-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="42508-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="42508-144">CoreOS</span></span>

<span data-ttu-id="42508-145">在 Azure 中最新的 SLES 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="42508-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="42508-146">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="42508-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="42508-147">如果您有根據舊或自訂 CoreOS 映像的 VM，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42508-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="42508-148">編輯 hello 檔案`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="42508-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="42508-149">更新 hello IPv6 位址：</span><span class="sxs-lookup"><span data-stu-id="42508-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
