---
title: "設定 Linux VM 的 DHCPv6 | Microsoft Docs"
description: "如何設定 Linux VM 的 DHCPv6。"
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="312d0-104">設定 Linux VM 的 DHCPv6</span><span class="sxs-lookup"><span data-stu-id="312d0-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="312d0-105">Azure Marketplace 中的一些 Linux 虛擬機器映像沒有預設的 DHCPv6 設定。</span><span class="sxs-lookup"><span data-stu-id="312d0-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="312d0-106">若要支援 IPv6，在您使用的 Linux OS 散發套件內必須設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="312d0-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="312d0-107">不同 Linux 散發套件的 DHCPv6 設定方式不同，因為它們使用不同的套件。</span><span class="sxs-lookup"><span data-stu-id="312d0-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="312d0-108">Azure Marketplace 中最新的 SUSE Linux 和 CoreOS 映像已有預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="312d0-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="312d0-109">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="312d0-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="312d0-110">本文件說明如何啟用 DHCPv6 使您的 Linux 虛擬機器取得 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="312d0-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="312d0-111">不當編輯網路組態檔可能會導致您失去 VM 的網路存取權。</span><span class="sxs-lookup"><span data-stu-id="312d0-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="312d0-112">我們建議您先在非生產系統上測試組態變更。</span><span class="sxs-lookup"><span data-stu-id="312d0-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="312d0-113">本文中的指示已經過在 Azure Marketplace 中最新版 Linux 映像上測試過。</span><span class="sxs-lookup"><span data-stu-id="312d0-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="312d0-114">如需您所用 Linux 版本的詳細指示，請參閱其文件。</span><span class="sxs-lookup"><span data-stu-id="312d0-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="312d0-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="312d0-115">Ubuntu</span></span>

1. <span data-ttu-id="312d0-116">編輯 `/etc/dhcp/dhclient6.conf` 檔案，新增以下這一行：</span><span class="sxs-lookup"><span data-stu-id="312d0-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="312d0-117">編輯下列組態的 eth0 介面網路組態︰</span><span class="sxs-lookup"><span data-stu-id="312d0-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="312d0-118">在 **Ubuntu 12.04 和 14.04** 上，編輯 `/etc/network/interfaces.d/eth0.cfg` 檔</span><span class="sxs-lookup"><span data-stu-id="312d0-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="312d0-119">在 **Ubuntu 16.04** 上，編輯 `/etc/network/interfaces.d/50-cloud-init.cfg` 檔</span><span class="sxs-lookup"><span data-stu-id="312d0-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="312d0-120">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="312d0-121">Debian</span><span class="sxs-lookup"><span data-stu-id="312d0-121">Debian</span></span>

1. <span data-ttu-id="312d0-122">編輯 `/etc/dhcp/dhclient6.conf` 檔案，新增以下這一行：</span><span class="sxs-lookup"><span data-stu-id="312d0-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="312d0-123">編輯 `/etc/network/interfaces` 檔案，新增以下組態：</span><span class="sxs-lookup"><span data-stu-id="312d0-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="312d0-124">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="312d0-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="312d0-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="312d0-126">編輯 `/etc/sysconfig/network` 檔案，新增以下參數：</span><span class="sxs-lookup"><span data-stu-id="312d0-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="312d0-127">編輯 `/etc/sysconfig/network-scripts/ifcfg-eth0` 檔案，新增以下兩個參數：</span><span class="sxs-lookup"><span data-stu-id="312d0-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="312d0-128">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="312d0-129">SLES 11 & openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="312d0-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="312d0-130">在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="312d0-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="312d0-131">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="312d0-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="312d0-132">如果您的 VM 是以較舊或自訂 SUSE 映像建置而成，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="312d0-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="312d0-133">如有需要，安裝 `dhcp-client` 套件：</span><span class="sxs-lookup"><span data-stu-id="312d0-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="312d0-134">編輯 `/etc/sysconfig/network/ifcfg-eth0` 檔案，新增以下參數：</span><span class="sxs-lookup"><span data-stu-id="312d0-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="312d0-135">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="312d0-136">SLES 12 和 openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="312d0-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="312d0-137">在 Azure 中最新的 SLES 和 openSUSE 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="312d0-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="312d0-138">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="312d0-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="312d0-139">如果您的 VM 是以較舊或自訂 SUSE 映像建置而成，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="312d0-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="312d0-140">編輯 `/etc/sysconfig/network/ifcfg-eth0` 檔案，取代此參數</span><span class="sxs-lookup"><span data-stu-id="312d0-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="312d0-141">為下列值：</span><span class="sxs-lookup"><span data-stu-id="312d0-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="312d0-142">將下列參數新增至 `/etc/sysconfig/network/ifcfg-eth0`：</span><span class="sxs-lookup"><span data-stu-id="312d0-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="312d0-143">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="312d0-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="312d0-144">CoreOS</span></span>

<span data-ttu-id="312d0-145">在 Azure 中最新的 SLES 映像已預先設定 DHCPv6。</span><span class="sxs-lookup"><span data-stu-id="312d0-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="312d0-146">使用這些映像不需要再進行額外的變更。</span><span class="sxs-lookup"><span data-stu-id="312d0-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="312d0-147">如果您的 VM 是以較舊或自訂 CoreOS 映像建置而成，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="312d0-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="312d0-148">編輯 `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="312d0-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="312d0-149">更新 IPv6 位址︰</span><span class="sxs-lookup"><span data-stu-id="312d0-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
