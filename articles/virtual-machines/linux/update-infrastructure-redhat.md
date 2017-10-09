---
title: "aaaRed Hat 更新基礎結構 (RHUI) |Microsoft 文件"
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
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="0a3d9-103">適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)</span><span class="sxs-lookup"><span data-stu-id="0a3d9-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="0a3d9-104">從 hello 隨 Red Hat Enterprise Linux (RHEL) 提供的映像在 Azure Marketplace 中建立的虛擬機器都已註冊的 tooaccess hello Red Hat 更新基礎結構 (RHUI) 部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="0a3d9-105">hello 隨 RHEL 執行個體具有存取 tooa 地區 yum 儲存機制和可以 tooreceive 累加式更新。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="0a3d9-106">RHEL 執行個體中設定 hello yum 儲存機制清單，由 RHUI 管理、 佈建期間。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="0a3d9-107">您不需要 toodo 任何額外的設定-執行`yum update`RHEL 執行個體準備好 tooget hello 最新的更新之後。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="0a3d9-108">在 2016 年 9 月部署更新的 Azure RHUI，並在 2017 年 1 月我們會啟動分階段的關機 hello 的較舊的 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="0a3d9-109">如果您已在使用 hello RHEL 映像 （或其快照集） 從 2016 年 9 月或更新版本-可能不不需要任何動作。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="0a3d9-110">不過，您會有較舊的快照集 Vm，如果其設定都必須更新不會中斷的存取 toohello Azure RHUI toobe。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="0a3d9-111">RHUI Azure 基礎結構更新</span><span class="sxs-lookup"><span data-stu-id="0a3d9-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="0a3d9-112">自 2016 年 9 月起，Azure 會有一組新的 Red Hat Update Infrastructure (RHUI) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="0a3d9-113">這些伺服器的部署將會透過 [Azure 流量管理員](https://azure.microsoft.com/services/traffic-manager/)執行，讓任何 VM (不論是哪個區域) 都可以使用單一端點 (rhui-1.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="0a3d9-114">hello hello Azure Marketplace （張貼日期為 2016 年 9 月或更高版本） 點 toohello 新 Azure RHUI 伺服器中的新 RHEL 隨用隨付 」 (PAYG) 映像，並不需要任何額外的動作。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="0a3d9-115">判斷是否需要採取動作</span><span class="sxs-lookup"><span data-stu-id="0a3d9-115">Determine if action is required</span></span>
<span data-ttu-id="0a3d9-116">如果您遇到連接 tooAzure RHUI 來自 Azure RHEL PAYG VM 的問題，請遵循下列步驟</span><span class="sxs-lookup"><span data-stu-id="0a3d9-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="0a3d9-117">檢查 Azure RHUI 端點的 VM 組態</span><span class="sxs-lookup"><span data-stu-id="0a3d9-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="0a3d9-118">如果核取`/etc/yum.repos.d/rh-cloud.repo`檔案也包含參考`rhui-[1-3].microsoft.com`中的 baseurl `[rhui-microsoft-azure-rhel*]` hello 檔案區段。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="0a3d9-119">如果它是您使用 hello 新 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="0a3d9-120">如果它指向 tooa 位置以下列模式的 hello `mirrorlist.*cds[1-4].cloudapp.net` -hello 組態更新為必要項。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="0a3d9-121">如果您使用 hello 新設定，且仍然無法連線 tooAzure RHUI-檔案與 Microsoft 或 Red Hat 支援案例。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0a3d9-122">存取 tooAzure 裝載 RHUI 是有限的 toohello Vm 內[Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="0a3d9-123">如果 hello 舊 Azure RHUI 仍然可以使用當您執行這項檢查，而您想讓 tooautomatically 更新 hello 組態時，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0a3d9-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="0a3d9-124">`sudo yum update RHEL6`或`sudo yum update RHEL7`視 hello RHEL 系列版本而定。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="0a3d9-125">如果您無法再連接 toohello 舊 Azure RHUI，hello 下一節中所述的後續 hello 手動步驟。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="0a3d9-126">請確定 hello 來源映像/快照上的 tooupdate hello 組態會影響 VM 已佈建。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="0a3d9-127">分階段的關機的 hello 舊 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="0a3d9-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="0a3d9-128">在 hello hello 關閉舊的 Azure RHUI 我們限制，如下所示存取 tooit:</span><span class="sxs-lookup"><span data-stu-id="0a3d9-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="0a3d9-129">進一步限制存取 (ACL) tooset tooit 已連接的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="0a3d9-130">可能的副作用： 如果您繼續使用 hello 舊 Azure RHUI-新的 Vm 可能無法 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="0a3d9-131">瀏覽關機/取消配置/啟動程序的 RHEL Vm 與動態 Ip 可能會收到新的 IP 和因此也無法啟動失敗 tooconnect toohello 舊 Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="0a3d9-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="0a3d9-132">關閉鏡像內容傳遞伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="0a3d9-133">可能的副作用： 在我們關閉詳細 CDSes 會再看見`yum update`服務時間更多的逾時為止 hello 點時，您無法再連接 toohello 舊 Azure RHUI。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="0a3d9-134">hello 新 RHUI 內容傳遞伺服器 hello Ip 是</span><span class="sxs-lookup"><span data-stu-id="0a3d9-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="0a3d9-135">如果您使用網路組態 toofurther 限制 RHEL PAYG Vm 所傳來的存取，請確定允許下列 Ip hello `yum update` toowork 視您是在 hello 環境而定。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="0a3d9-136">手動更新程序 toouse hello 新 Azure RHUI 伺服器</span><span class="sxs-lookup"><span data-stu-id="0a3d9-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="0a3d9-137">（透過 curl) 下載 hello 公用金鑰簽章</span><span class="sxs-lookup"><span data-stu-id="0a3d9-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="0a3d9-138">請確認下載的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="0a3d9-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="0a3d9-139">檢查 hello 輸出，確認`keyid`和`user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="0a3d9-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="0a3d9-140">安裝 hello 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="0a3d9-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="0a3d9-141">下載、驗證及安裝用戶端 RPM</span><span class="sxs-lookup"><span data-stu-id="0a3d9-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="0a3d9-142">下載：適用於 RHEL 6</span><span class="sxs-lookup"><span data-stu-id="0a3d9-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="0a3d9-143">適用於 RHEL 7</span><span class="sxs-lookup"><span data-stu-id="0a3d9-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="0a3d9-144">驗證：</span><span class="sxs-lookup"><span data-stu-id="0a3d9-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="0a3d9-145">檢查輸出中的簽章的 hello 封裝是 [確定]</span><span class="sxs-lookup"><span data-stu-id="0a3d9-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="0a3d9-146">安裝 hello RPM</span><span class="sxs-lookup"><span data-stu-id="0a3d9-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="0a3d9-147">完成時，請確認您可以存取 Azure RHUI 表單 hello VM</span><span class="sxs-lookup"><span data-stu-id="0a3d9-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="0a3d9-148">全部的一個指令碼自動化 hello 前工作</span><span class="sxs-lookup"><span data-stu-id="0a3d9-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="0a3d9-149">使用下列指令碼以更新受影響的 Vm toohello 新 Azure RHUI 伺服器的所需的 tooautomate hello 工作 hello。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="0a3d9-150">RHUI 概觀</span><span class="sxs-lookup"><span data-stu-id="0a3d9-150">RHUI overview</span></span>
<span data-ttu-id="0a3d9-151">[Red Hat 更新基礎結構](https://access.redhat.com/products/red-hat-update-infrastructure)提供 Red Hat 認證雲端提供者所裝載的 Red Hat Enterprise Linux 雲端執行個體可高度擴充的方案 toomanage yum 儲存機制內容。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="0a3d9-152">依據 hello 上游 Pulp 專案 RHUI 允許雲端提供者 toolocally 鏡像 Red Hat 裝載的儲存機制內容，其本身的內容，以建立自訂儲存機制，並進行這些儲存機制可用 tooa 大群使用者透過負載平衡內容傳遞系統。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="0a3d9-153">可以使用 RHUI 的區域</span><span class="sxs-lookup"><span data-stu-id="0a3d9-153">Regions where RHUI is available</span></span>
<span data-ttu-id="0a3d9-154">在所有可使用 RHEL 隨選映像的地區，皆可使用 RHUI。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="0a3d9-155">它目前包含在 hello 上所列的所有公用區域[Azure 狀態儀表板](https://azure.microsoft.com/status/)頁面上，Azure 美國政府和 Azure 德國區域。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="0a3d9-156">從 RHEL 隨選映像佈建之 VM 的 RHUI 存取包含在其價格中。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="0a3d9-157">我們展開 RHEL 隨可用性 hello 未來在其他地區/國家雲端可用性將會更新。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="0a3d9-158">存取 tooAzure 裝載 RHUI 是有限的 toohello Vm 內[Microsoft Azure Datacenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="0a3d9-159">從其他更新儲存機制取得更新</span><span class="sxs-lookup"><span data-stu-id="0a3d9-159">Get updates from another update repository</span></span>
<span data-ttu-id="0a3d9-160">如果您需要從不同的更新儲存機制 （而不是 Azure 託管 RHUI) tooget 更新時，首先您需要 toounregister RHUI 從您的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="0a3d9-161">則您需要 toore 登錄其與 hello 所需的更新基礎結構 （例如 Red Hat 附屬或 Red Hat 客戶入口網站 CDN）。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="0a3d9-162">您將需要這些服務的適當 Red Hat 訂用帳戶，而且必須註冊 [Azure 中的 Red Hat 雲端存取](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="0a3d9-163">toounregister RHUI 和重新登錄 tooyour 更新基礎結構，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0a3d9-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="0a3d9-164">編輯 /etc/yum.repos.d/rh-cloud.repo 並變更所有`enabled=1`太`enabled=0`。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="0a3d9-165">例如：</span><span class="sxs-lookup"><span data-stu-id="0a3d9-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="0a3d9-166">編輯 /etc/yum/pluginconf.d/rhnplugin.conf 並變更`enabled=0`太`enabled=1`。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="0a3d9-167">然後向 hello 所需的基礎結構，例如 Red Hat 客戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="0a3d9-168">請遵循解決方案指南 Red Hat[如何 tooregister 和訂閱系統 toohello Red Hat 客戶入口網站](https://access.redhat.com/solutions/253273)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="0a3d9-169">存取 toohello Azure 託管 RHUI 隨附於 hello RHEL 隨用隨付 」 (PAYG) 映像的價格。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="0a3d9-170">取消登錄從 hello Azure 託管 RHUI PAYG RHEL VM 不會轉換成提到您-擁有的授權 (BYOL) 型別 VM hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="0a3d9-171">如果您註冊 hello 相同的 VM 與其他來源的更新您可能會產生 double 費用： 第一次 Azure RHEL 軟體費用，和 hello Red Hat 訂閱的第二次。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="0a3d9-172">建立及部署您自己 （BYOL 型別） 映像中所述，如果您以一致的方式需要 toouse 要考慮 Azure 託管 RHUI 以外的更新基礎結構[建立及上傳 Red Hat 基礎 Azure 的虛擬機器](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)發行項。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="0a3d9-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a3d9-173">Next steps</span></span>
<span data-ttu-id="0a3d9-174">從 Azure Marketplace 隨用隨付映像和運用 Azure 託管 RHUI Red Hat Enterprise Linux VM toocreate 太移[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/)。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="0a3d9-175">您將會無法 toouse `yum update` RHEL 執行個體沒有任何額外的設定中。</span><span class="sxs-lookup"><span data-stu-id="0a3d9-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

