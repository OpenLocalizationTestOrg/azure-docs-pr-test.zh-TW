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
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Tooupdate hello Azure Linux 代理程式在 VM 上的方式

tooupdate 您[Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent)在 Azure 中的 Linux VM，您必須具備：

- 在 Azure 中執行的 Linux VM。
- 連接 toothat Linux VM 使用 SSH。

您應該一律檢查 hello Linux distro 儲存機制中的封裝第一次。 您可使用 hello 封裝可能無法 hello 最新版本，不過，啟用自動更新可確保 hello Linux 代理程式一律會收到 hello 最新的更新。 您應該從 hello 封裝管理員安裝的問題，您應該搜尋 hello distro 廠商所提供的支援。

## <a name="updating-hello-azure-linux-agent"></a>更新 hello Azure Linux 代理程式

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>更新封裝快取

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

#### <a name="restart-agent-for-1404"></a>重新啟動 14.04 的代理程式

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>重新啟動 16.04 / 17.04 的代理程式

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 “Wheezy”

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>更新封裝快取

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>啟用代理程式自動更新
這一版本的 Debian 沒有高於或等於 2.0.16 的版本，因此無法使用自動更新。 上述命令 hello hello 輸出會顯示 hello 封裝是否保持最新狀態。

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 “Jessie” / Debian 9 “Stretch”

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>更新封裝快取

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新 

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Redhat/CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>檢查可用的更新

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新 

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>檢查可用的更新

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新 

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>檢查可用的更新

hello，上述輸出會顯示 hello 封裝是否向上 toodate。

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新 

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>檢查目前的封裝版本

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>檢查可用的更新

在從上述 hello hello 輸出中，這會顯示您是否 hello 封裝是最新的。

#### <a name="install-hello-latest-package-version"></a>安裝 hello 最新的封裝版本

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新 

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>重新啟動 hello waagent 服務

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 和 7

Oracle linux，請確定該 hello`Addons`儲存機制已啟用。 選擇 tooedit hello 檔案`/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) 或`/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux)，並變更 hello 行`enabled=0`太`enabled=1`下**[ol6_addons]**或**[ol7_addons]**在這個檔案。

然後，tooinstall hello 最新版本的 hello Azure Linux 代理程式，類型：

```bash
sudo yum install WALinuxAgent
```

如果找不到 hello 附加元件儲存機制您可以在 hello 根據 tooyour Oracle Linux 版本.repo 檔案結尾處，只要加入這行：

Oracle Linux 6 虛擬機器︰

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Oracle Linux 7 虛擬機器︰

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

然後輸入：

```bash
sudo yum update WALinuxAgent
```

通常這是您只需要，但如果基於某些原因，您需要 tooinstall 從直接 https://github.com 使用 hello 下列步驟。


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>散發代理程式的封裝存在時，更新 hello Linux 代理程式

輸入安裝 （有一些不安裝依預設，例如 6.4 和 6.5 Redhat、 CentOS 和 Oracle Linux 版本的散發版本） 的 wget `sudo yum install wget` hello 命令列上。

### <a name="1-download-hello-latest-version"></a>1.下載最新版本的 hello
開啟[hello Azure Linux 代理程式在 GitHub 中的發行](https://github.com/Azure/WALinuxAgent/releases)在網頁上，並找出 hello 最新版本號碼。 (您可以輸入 `waagent --version`，即可找到目前的版本 )。

#### <a name="for-version-22x-or-later-type"></a>針對 2.2.x 版本或較新版本，請輸入：
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

hello 面這一行會使用版本 2.2.0 做為範例：

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2.安裝 hello Azure Linux 代理程式

#### <a name="for-version-22x-use"></a>針對 2.2.x 版本，請使用：
您可能需要 tooinstall hello 封裝`setuptools`第一次-看到[這裡](https://pypi.python.org/pypi/setuptools)。 然後，執行：

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>確定已啟用自動更新

首先，請檢查 toosee，如果已啟用：

```bash
cat /etc/waagent.conf
```

尋找「AutoUpdate.Enabled」。 如果看到此輸出結果，則表示已啟用：

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 執行：

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3.重新啟動 hello waagent 服務
針對大多數的 Linux 散發版本：

```bash
sudo service waagent restart
```

針對 Ubuntu，使用：

```bash
sudo service walinuxagent restart
```

針對 CoreOS，請使用：

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4.確認 hello Azure Linux 代理程式版本
    
```bash
waagent -version
```

針對 CoreOS，上述命令 hello 可能無法運作。

您會看到該 hello Azure Linux 代理程式版本已更新 toohello 新版本。

如需有關 hello Azure Linux 代理程式的詳細資訊，請參閱[Azure Linux 代理程式讀我檔案](https://github.com/Azure/WALinuxAgent)。
