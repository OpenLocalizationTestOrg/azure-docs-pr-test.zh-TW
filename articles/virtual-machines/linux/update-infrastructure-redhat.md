---
title: Red Hat Update Infrastructure (RHUI) | Microsoft Docs
description: "了解適用於 Microsoft Azure 中隨選 Red Hat Enterprise Linux 執行個體的 Red Hat Update Infrastructure (RHUI)"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: 07815d691ffe57f0349f7a90ced4a2fcc1ab834f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="f22c1-103">適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)</span><span class="sxs-lookup"><span data-stu-id="f22c1-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="f22c1-104">需註冊從隨選 Red Hat Enterprise Linux (RHEL) 映像建立的虛擬機器，以存取部署在 Azure 中的 Red Hat Update Infrastructure (RHUI)；前述映像可在 Azure Marketplace 中找到。</span><span class="sxs-lookup"><span data-stu-id="f22c1-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="f22c1-105">隨選 RHEL 執行個體能夠存取區域 yum 儲存機制，並且能夠接收累加式更新。</span><span class="sxs-lookup"><span data-stu-id="f22c1-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="f22c1-106">RHUI 所管理的 yum 儲存機至清單，會於佈建期間設定在您的 RHEL 執行個體中。</span><span class="sxs-lookup"><span data-stu-id="f22c1-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="f22c1-107">您不需要進行任何額外設定，只需在 RHEL 執行個體準備好接收最新更新之後執行 `yum update` 即可。</span><span class="sxs-lookup"><span data-stu-id="f22c1-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="f22c1-108">在 2016 年 9 月，我們部署了已更新的 Azure RHUI，而在 2017 年 1 月，我們開始分階段關閉舊版 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="f22c1-109">如果您從 2016 年 9 月或之後才使用 RHEL 映像 (或其快照)，可能就不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="f22c1-110">不過，如果您擁有舊版快照/VM，則其組態必須更新，才能繼續存取 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="f22c1-111">RHUI Azure 基礎結構更新</span><span class="sxs-lookup"><span data-stu-id="f22c1-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="f22c1-112">自 2016 年 9 月起，Azure 會有一組新的 Red Hat Update Infrastructure (RHUI) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f22c1-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="f22c1-113">這些伺服器的部署將會透過 [Azure 流量管理員](https://azure.microsoft.com/services/traffic-manager/)執行，讓任何 VM (不論是哪個區域) 都可以使用單一端點 (rhui-1.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="f22c1-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="f22c1-114">Azure Marketplace 中的新 RHEL 隨用隨付 (PAYG) 映像 (日期為 2016 年 9 月的版本或更新版本) 會自動指向新的 Azure RHUI 伺服器，因此不需採取任何其他動作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="f22c1-115">判斷是否需要採取動作</span><span class="sxs-lookup"><span data-stu-id="f22c1-115">Determine if action is required</span></span>
<span data-ttu-id="f22c1-116">如果您從 Azure RHEL PAYG VM 連接到 RHUI 時發生問題，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="f22c1-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="f22c1-117">檢查 Azure RHUI 端點的 VM 組態</span><span class="sxs-lookup"><span data-stu-id="f22c1-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="f22c1-118">檢查 `/etc/yum.repos.d/rh-cloud.repo` 檔案之 `[rhui-microsoft-azure-rhel*]` 區段的 baseurl 中是否包含對 `rhui-[1-3].microsoft.com` 的參考。</span><span class="sxs-lookup"><span data-stu-id="f22c1-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="f22c1-119">如果是，您使用的便是新 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="f22c1-120">如果它指向具有 `mirrorlist.*cds[1-4].cloudapp.net` 模式的位置，則需要進行組態更新。</span><span class="sxs-lookup"><span data-stu-id="f22c1-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="f22c1-121">如果您使用的是新組態，但仍無法連接到 Azure RHUI，請向 Microsoft 或 Red Hat 提出支援案例。</span><span class="sxs-lookup"><span data-stu-id="f22c1-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f22c1-122">只有 [Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)中的 VM 能夠存取 Azure 代管的 RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="f22c1-123">如果在您執行這項檢查時舊 Azure RHUI 仍然可用，而您想要自動更新組態，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f22c1-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="f22c1-124">`sudo yum update RHEL6` 或 `sudo yum update RHEL7`，視 RHEL 系列版本而定。</span><span class="sxs-lookup"><span data-stu-id="f22c1-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="f22c1-125">如果您已無法連接到舊 Azure RHUI，請依照下一節中所述的手動步驟操作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="f22c1-126">確定更新受影響 VM 的來源佈建映像/快照集上的組態。</span><span class="sxs-lookup"><span data-stu-id="f22c1-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="f22c1-127">分段關閉舊的 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="f22c1-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="f22c1-128">在關閉舊 Azure RHUI 的期間，我們會依下列方式限制對該 RHUI 的存取：</span><span class="sxs-lookup"><span data-stu-id="f22c1-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="f22c1-129">進一步將它限制成僅供一組已經與它連線的 IP 位址存取 (ACL)。</span><span class="sxs-lookup"><span data-stu-id="f22c1-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="f22c1-130">可能的副作用：如果您繼續使用舊 Azure RHUI，您的新 VM 可能無法與它連線。</span><span class="sxs-lookup"><span data-stu-id="f22c1-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="f22c1-131">具有動態 IP 的 RHEL VM 在經過關閉/解除配置/啟動程序之後，可能會取得新的 IP，因此也可能開始無法連接到舊的 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="f22c1-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="f22c1-132">關閉鏡像內容傳遞伺服器。</span><span class="sxs-lookup"><span data-stu-id="f22c1-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="f22c1-133">可能的副作用：隨著我們關閉的 CDS 越多，您可能會發現 `yum update` 服務時間變得越長、逾時次數變得越多，直到您無法再連接到舊 Azure RHUI 為止。</span><span class="sxs-lookup"><span data-stu-id="f22c1-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="f22c1-134">新的 RHUI 內容傳遞伺服器的 IP 為</span><span class="sxs-lookup"><span data-stu-id="f22c1-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="f22c1-135">如果您使用網路組態來進一步限制來自 RHEL PAYG VM 的存取，請確定已允許下列 IP，如此 `yum update` 才能依據您所在的環境運作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="f22c1-136">使用新 Azure RHUI 伺服器的手動更新程序</span><span class="sxs-lookup"><span data-stu-id="f22c1-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="f22c1-137">下載 (透過 curl) 公開金鑰簽章</span><span class="sxs-lookup"><span data-stu-id="f22c1-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="f22c1-138">驗證已下載的金鑰</span><span class="sxs-lookup"><span data-stu-id="f22c1-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="f22c1-139">檢查輸出，驗證 `keyid` 和 `user ID packet`：</span><span class="sxs-lookup"><span data-stu-id="f22c1-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="f22c1-140">安裝公開金鑰</span><span class="sxs-lookup"><span data-stu-id="f22c1-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="f22c1-141">下載、驗證及安裝用戶端 RPM</span><span class="sxs-lookup"><span data-stu-id="f22c1-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="f22c1-142">下載：適用於 RHEL 6</span><span class="sxs-lookup"><span data-stu-id="f22c1-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="f22c1-143">適用於 RHEL 7</span><span class="sxs-lookup"><span data-stu-id="f22c1-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="f22c1-144">驗證：</span><span class="sxs-lookup"><span data-stu-id="f22c1-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="f22c1-145">確認輸出中的套件簽章正確</span><span class="sxs-lookup"><span data-stu-id="f22c1-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="f22c1-146">安裝 RPM</span><span class="sxs-lookup"><span data-stu-id="f22c1-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="f22c1-147">完成時，請確認您可以從 VM 存取 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="f22c1-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="f22c1-148">可自動執行上述工作的全方位指令碼</span><span class="sxs-lookup"><span data-stu-id="f22c1-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="f22c1-149">請視需要使用下列指令碼，以自動執行將受影響的 VM 更新到新 Azure RHUI 伺服器的工作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="f22c1-150">RHUI 概觀</span><span class="sxs-lookup"><span data-stu-id="f22c1-150">RHUI overview</span></span>
<span data-ttu-id="f22c1-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) 提供一個可靈活調整的解決方案，可以針對裝載在 Red Hat 認證雲端提供者上的 Red Hat Enterprise Linux 雲端執行個體，管理 yum 儲存機制內容。</span><span class="sxs-lookup"><span data-stu-id="f22c1-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="f22c1-152">根據上游 Pulp 專案，RHUI 可讓雲端提供者在本機建立 Red Hat 所裝載儲存機制內容的鏡像、以其內容建立自定儲存機制，並透過具流量負載平衡的內容傳遞系統，讓儲存機制可供大量使用者使用。</span><span class="sxs-lookup"><span data-stu-id="f22c1-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="f22c1-153">可以使用 RHUI 的區域</span><span class="sxs-lookup"><span data-stu-id="f22c1-153">Regions where RHUI is available</span></span>
<span data-ttu-id="f22c1-154">在所有可使用 RHEL 隨選映像的地區，皆可使用 RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="f22c1-155">目前包含 [Azure 狀態儀表板](https://azure.microsoft.com/status/) 頁面上所列的所有公用區域 (Azure 美國政府和 Azure 德國區域)。</span><span class="sxs-lookup"><span data-stu-id="f22c1-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="f22c1-156">從 RHEL 隨選映像佈建之 VM 的 RHUI 存取包含在其價格中。</span><span class="sxs-lookup"><span data-stu-id="f22c1-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="f22c1-157">額外區域/國家的雲端可用性將會更新，因為我們將在未來擴大 RHEL 隨選的可用性。</span><span class="sxs-lookup"><span data-stu-id="f22c1-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="f22c1-158">只有 [Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)中的 VM 能夠存取 Azure 代管的 RHUI。</span><span class="sxs-lookup"><span data-stu-id="f22c1-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="f22c1-159">從其他更新儲存機制取得更新</span><span class="sxs-lookup"><span data-stu-id="f22c1-159">Get updates from another update repository</span></span>
<span data-ttu-id="f22c1-160">如果您需要從不同的更新儲存機制 (而不是 Azure 代管的 RHUI) 取得更新，您必須先從 RHUI 將您的執行個體取消註冊。</span><span class="sxs-lookup"><span data-stu-id="f22c1-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="f22c1-161">接著，您必須向所需的更新基礎結構 (例如 Red Hat Satellite 或 Red Hat 客戶入口網站 CDN) 重新註冊它們。</span><span class="sxs-lookup"><span data-stu-id="f22c1-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="f22c1-162">您將需要這些服務的適當 Red Hat 訂用帳戶，而且必須註冊 [Azure 中的 Red Hat 雲端存取](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)。</span><span class="sxs-lookup"><span data-stu-id="f22c1-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="f22c1-163">若要將 RHUI 取消註冊再向您的更新基礎結構重新註冊，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="f22c1-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="f22c1-164">編輯 /etc/yum.repos.d/rh-cloud.repo，將所有 `enabled=1` 變更為 `enabled=0`。</span><span class="sxs-lookup"><span data-stu-id="f22c1-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="f22c1-165">例如：</span><span class="sxs-lookup"><span data-stu-id="f22c1-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="f22c1-166">編輯 /etc/yum/pluginconf.d/rhnplugin.conf，將 `enabled=0` 變更為 `enabled=1`。</span><span class="sxs-lookup"><span data-stu-id="f22c1-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="f22c1-167">然後，註冊所需的基礎結構，例如 Red Hat 客戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="f22c1-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="f22c1-168">請依照 Red Hat 解決方案指南中的 [如何向 Red Hat 客戶入口網站註冊及訂閱系統](https://access.redhat.com/solutions/253273)操作。</span><span class="sxs-lookup"><span data-stu-id="f22c1-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="f22c1-169">對 Azure 代管之 RHUI 的存取，包含在 RHEL 隨用隨付 (PAYG) 映像的價格中。</span><span class="sxs-lookup"><span data-stu-id="f22c1-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="f22c1-170">從 Azure 代管的 RHUI 將 PAYG RHEL VM 取消註冊並不會將虛擬機器轉換成自備授權 (BYOL) 類型的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f22c1-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="f22c1-171">如果您以另一個更新來源註冊相同的 VM，可能會產生雙重費用：第一次是針對 Azure RHEL 軟體費用，而第二次是針對 Red Hat 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f22c1-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="f22c1-172">如果您持續需要使用非 Azure 代管 RHUI 的更新基礎結構，請考慮建立及部署您自己的 (BYOL 類型) 映像，如 [建立及上傳適用於 Azure 的 Red Hat 型虛擬機器](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 一文所述。</span><span class="sxs-lookup"><span data-stu-id="f22c1-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="f22c1-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f22c1-173">Next steps</span></span>
<span data-ttu-id="f22c1-174">若要從 Azure Marketplace 隨用隨付映像建立 Red Hat Enterprise Linux VM 並利用 Azure 代管的 RHUI，請移至 [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/)。</span><span class="sxs-lookup"><span data-stu-id="f22c1-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="f22c1-175">您將能夠在您的 RHEL 執行個體中使用 `yum update` ，而不需要任何額外的安裝。</span><span class="sxs-lookup"><span data-stu-id="f22c1-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

