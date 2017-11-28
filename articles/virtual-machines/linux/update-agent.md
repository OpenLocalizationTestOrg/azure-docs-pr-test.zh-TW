---
title: "aaaUpdate hello Azure Linux 代理程式從 GitHub |Microsoft 文件"
description: "深入了解如何 tooupdate Linux vm 中 Azure toohello 來自 GitHub 的最新版本的 Azure Linux 代理程式"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="ad4c9-103">Tooupdate hello Azure Linux 代理程式在 VM 上的方式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="ad4c9-104">tooupdate 您[Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent)在 Azure 中的 Linux VM，您必須具備：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="ad4c9-105">在 Azure 中執行的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="ad4c9-106">連接 toothat Linux VM 使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="ad4c9-107">您應該一律檢查 hello Linux distro 儲存機制中的封裝第一次。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="ad4c9-108">您可使用 hello 封裝可能無法 hello 最新版本，不過，啟用自動更新可確保 hello Linux 代理程式一律會收到 hello 最新的更新。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="ad4c9-109">您應該從 hello 封裝管理員安裝的問題，您應該搜尋 hello distro 廠商所提供的支援。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="ad4c9-110">更新 hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="ad4c9-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ad4c9-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-112">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ad4c9-113">更新封裝快取</span><span class="sxs-lookup"><span data-stu-id="ad4c9-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-114">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-115">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="ad4c9-116">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-117">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-118">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-119">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-120">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="ad4c9-121">重新啟動 14.04 的代理程式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="ad4c9-122">重新啟動 16.04 / 17.04 的代理程式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="ad4c9-123">Debian</span><span class="sxs-lookup"><span data-stu-id="ad4c9-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="ad4c9-124">Debian 7 “Wheezy”</span><span class="sxs-lookup"><span data-stu-id="ad4c9-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-125">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ad4c9-126">更新封裝快取</span><span class="sxs-lookup"><span data-stu-id="ad4c9-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-127">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="ad4c9-128">啟用代理程式自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-128">Enable agent auto update</span></span>
<span data-ttu-id="ad4c9-129">這一版本的 Debian 沒有高於或等於 2.0.16 的版本，因此無法使用自動更新。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="ad4c9-130">上述命令 hello hello 輸出會顯示 hello 封裝是否保持最新狀態。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="ad4c9-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span><span class="sxs-lookup"><span data-stu-id="ad4c9-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-132">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="ad4c9-133">更新封裝快取</span><span class="sxs-lookup"><span data-stu-id="ad4c9-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-134">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-135">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ad4c9-136">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-137">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-138">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-139">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-140">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="ad4c9-141">Redhat/CentOS</span><span class="sxs-lookup"><span data-stu-id="ad4c9-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="ad4c9-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="ad4c9-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-143">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ad4c9-144">檢查可用的更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-145">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-146">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ad4c9-147">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-148">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-149">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-150">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-151">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="ad4c9-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="ad4c9-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-153">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ad4c9-154">檢查可用的更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-155">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-156">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ad4c9-157">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-158">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-159">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-160">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-161">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="ad4c9-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="ad4c9-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="ad4c9-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="ad4c9-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-164">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ad4c9-165">檢查可用的更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-165">Check available updates</span></span>

<span data-ttu-id="ad4c9-166">hello，上述輸出會顯示 hello 封裝是否向上 toodate。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-167">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-168">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ad4c9-169">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-170">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-171">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-172">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-173">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="ad4c9-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="ad4c9-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="ad4c9-175">檢查目前的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="ad4c9-176">檢查可用的更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-176">Check available updates</span></span>

<span data-ttu-id="ad4c9-177">在從上述 hello hello 輸出中，這會顯示您是否 hello 封裝是最新的。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="ad4c9-178">安裝 hello 最新的封裝版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-179">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="ad4c9-180">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-181">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-182">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-183">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-184">重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="ad4c9-185">Oracle 6 和 7</span><span class="sxs-lookup"><span data-stu-id="ad4c9-185">Oracle 6 and 7</span></span>

<span data-ttu-id="ad4c9-186">Oracle linux，請確定該 hello`Addons`儲存機制已啟用。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="ad4c9-187">選擇 tooedit hello 檔案`/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) 或`/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux)，並變更 hello 行`enabled=0`太`enabled=1`下**[ol6_addons]**或**[ol7_addons]**在這個檔案。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="ad4c9-188">然後，tooinstall hello 最新版本的 hello Azure Linux 代理程式，類型：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="ad4c9-189">如果找不到 hello 附加元件儲存機制您可以在 hello 根據 tooyour Oracle Linux 版本.repo 檔案結尾處，只要加入這行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="ad4c9-190">Oracle Linux 6 虛擬機器︰</span><span class="sxs-lookup"><span data-stu-id="ad4c9-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="ad4c9-191">Oracle Linux 7 虛擬機器︰</span><span class="sxs-lookup"><span data-stu-id="ad4c9-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="ad4c9-192">然後輸入：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="ad4c9-193">通常這是您只需要，但如果基於某些原因，您需要 tooinstall 從直接 https://github.com 使用 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="ad4c9-194">散發代理程式的封裝存在時，更新 hello Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="ad4c9-195">輸入安裝 （有一些不安裝依預設，例如 6.4 和 6.5 Redhat、 CentOS 和 Oracle Linux 版本的散發版本） 的 wget `sudo yum install wget` hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="ad4c9-196">1.下載最新版本的 hello</span><span class="sxs-lookup"><span data-stu-id="ad4c9-196">1. Download hello latest version</span></span>
<span data-ttu-id="ad4c9-197">開啟[hello Azure Linux 代理程式在 GitHub 中的發行](https://github.com/Azure/WALinuxAgent/releases)在網頁上，並找出 hello 最新版本號碼。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="ad4c9-198">(您可以輸入 `waagent --version`，即可找到目前的版本 )。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="ad4c9-199">針對 2.2.x 版本或較新版本，請輸入：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="ad4c9-200">hello 面這一行會使用版本 2.2.0 做為範例：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="ad4c9-201">2.安裝 hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="ad4c9-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="ad4c9-202">針對 2.2.x 版本，請使用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="ad4c9-203">您可能需要 tooinstall hello 封裝`setuptools`第一次-看到[這裡](https://pypi.python.org/pypi/setuptools)。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="ad4c9-204">然後，執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="ad4c9-205">確定已啟用自動更新</span><span class="sxs-lookup"><span data-stu-id="ad4c9-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="ad4c9-206">首先，請檢查 toosee，如果已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="ad4c9-207">尋找「AutoUpdate.Enabled」。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="ad4c9-208">如果看到此輸出結果，則表示已啟用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="ad4c9-209">tooenable 執行：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="ad4c9-210">3.重新啟動 hello waagent 服務</span><span class="sxs-lookup"><span data-stu-id="ad4c9-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="ad4c9-211">針對大多數的 Linux 散發版本：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="ad4c9-212">針對 Ubuntu，使用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="ad4c9-213">針對 CoreOS，請使用：</span><span class="sxs-lookup"><span data-stu-id="ad4c9-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="ad4c9-214">4.確認 hello Azure Linux 代理程式版本</span><span class="sxs-lookup"><span data-stu-id="ad4c9-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="ad4c9-215">針對 CoreOS，上述命令 hello 可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="ad4c9-216">您會看到該 hello Azure Linux 代理程式版本已更新 toohello 新版本。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="ad4c9-217">如需有關 hello Azure Linux 代理程式的詳細資訊，請參閱[Azure Linux 代理程式讀我檔案](https://github.com/Azure/WALinuxAgent)。</span><span class="sxs-lookup"><span data-stu-id="ad4c9-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
