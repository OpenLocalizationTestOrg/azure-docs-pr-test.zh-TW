---
title: "在 Azure 上的 aaaIntroduction tooFreeBSD |Microsoft 文件"
description: "了解如何使用 Azure 上的 FreeBSD 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>在 Azure 上的簡介 tooFreeBSD
本主題提供在 Azure 中執行 FreeBSD 虛擬機器的概觀。

## <a name="overview"></a>概觀
Microsoft azure FreeBSD 是進階的電腦作業系統使用 toopower 最新的伺服器、 桌上型電腦，以及內嵌的平台。

Microsoft Corporation 提供 FreeBSD 的映像在 Azure 上以 hello [Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)預先設定。 目前，hello 下列 FreeBSD 版本會提供當做映像的 Microsoft:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

hello 代理程式負責 hello FreeBSD VM 之間的通訊和進行運算，例如佈建 Azure 網狀架構 hello hello VM （使用者名稱、 密碼或 SSH 金鑰、 主機名稱等） 的第一次使用和啟用的功能，用於選擇性的 VM 擴充功能。

FreeBSD 的未來版本中，與 hello 策略是目前 toostay 並提供 hello 最新版本的 hello FreeBSD 版本工程小組會在發行後不久。

## <a name="deploying-a-freebsd-virtual-machine"></a>部署 FreeBSD 虛擬機器
部署 FreeBSD 虛擬機器是簡單的程序，使用從 hello Azure 入口網站中的 hello Azure Marketplace 映像：

- [FreeBSD 10.3 hello Azure Marketplace 上](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [FreeBSD 11.0 hello Azure Marketplace 上](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>透過 Azure CLI 2.0 在 FreeBSD 上建立 FreeBSD VM
首先，您必須 tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)雖然 FreeBSD 機器上，下列命令。

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

如果未安裝 bash FreeBSD 機器上，執行下列命令之前 hello 安裝。 

```
    sudo pkg install bash
```

如果未安裝 python FreeBSD 機器上，執行下列命令之前 hello 安裝。 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Hello 在安裝期間，系統會要求您`Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`。 如果您回答`y`輸入`/etc/rc.conf`為`a path tooan rc file tooupdate`，您可能會符合 hello 問題`ERROR: [Errno 13] Permission denied`。 tooresolve 這個問題，您應該授與對 hello 檔 hello 寫入右 toocurrent 使用者`etc/rc.conf`。

現在您可以登入 Azure 並建立您的 FreeBSD VM。 以下是範例 toocreate FreeBSD 11.0 VM。 您也可以加入 hello 參數`--public-ip-address-dns-name`全域唯一的 DNS 名稱，新建立的公用 ip。 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

然後您可以登入 tooyour FreeBSD VM 透過 hello 列印 hello 上述輸出中的部署中的 ip 位址。 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>適用於 FreeBSD 的 VM 擴充功能
以下為 FreeBSD VM 中支援的 VM 擴充功能。

### <a name="vmaccess"></a>VMAccess
hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)延伸模組可以：

* 重設 hello hello 原始 sudo 使用者密碼。
* 建立新 sudo 的使用者與 hello 指定的密碼。
* 設定與指定索引鍵的 hello hello 公開主機金鑰。
* 重設期間如果未提供 hello 主機金鑰佈建的 VM 提供 hello 公開主機金鑰。
* 開啟 hello SSH 連接埠 (22)，並還原 hello sshd_config 如果 reset_ssh 設定 tootrue。
* 移除 hello 現有使用者。
* 檢查磁碟。
* 修復新增的磁碟。

### <a name="customscript"></a>CustomScript
hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript)延伸模組可以：

* 如果提供，下載 hello 自訂指令碼從 Azure 儲存體或外部的公開儲存體 (例如，GitHub)。
* 執行 hello 進入點指令碼。
* 支援內嵌命令。
* 自動轉換 Shell 和 Python 指令碼中的 Windows 樣式新行字元。
* 自動移除 Shell 和 Python 指令碼中的 BOM。
* 保護 CommandToExecute 中的機密資料。

> [!NOTE]
> FreeBSD VM 目前僅支援 CustomScript 1.x 版。  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>驗證：使用者名稱、密碼和 SSH 金鑰
當您使用 hello Azure 入口網站建立 FreeBSD 虛擬機器時，您必須提供使用者名稱、 密碼或 SSH 公開金鑰。
部署在 Azure 上 FreeBSD 虛擬機器的使用者名稱必須符合的系統帳戶的名稱 (UID < 100) 已經存在於 hello 虛擬機器 （「 根 」，例如） 中。
目前支援僅 hello RSA SSH 金鑰。 多行 SSH 金鑰的開頭必須為 `---- BEGIN SSH2 PUBLIC KEY ----`，結尾為 `---- END SSH2 PUBLIC KEY ----`。

## <a name="obtaining-superuser-privileges"></a>取得超級使用者權限
hello 在 Azure 上的虛擬機器執行個體部署期間指定的使用者帳戶是特殊權限的帳戶。 hello sudo 的安裝封裝中 hello 發行 FreeBSD 映像。
透過此使用者帳戶登入之後，您可以使用 hello 命令語法為根目錄執行命令。

```
    $ sudo <COMMAND>
```

您可以視需要使用 `sudo -s` 來取得 root shell。

## <a name="known-issues"></a>已知問題
hello [Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)2.2.2 有 [已知的問題] 的版本 (https://github.com/Azure/WALinuxAgent/pull/517)，會導致 hello 佈建失敗 FreeBSD vm 在 Azure 上。 hello 修正的擷取方式[Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)2.2.3 版本和更新版本。 

## <a name="next-steps"></a>後續步驟
* 跳過[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM。
* 如果您想 toobring 自己 FreeBSD tooAzure，請參閱太[建立並上傳 VHD FreeBSD tooAzure](linux/classic/freebsd-create-upload-vhd.md)。
