---
title: "aaaAzure CLI 範例 |Microsoft 文件"
description: "Azure CLI 範例"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>適用於 Linux 虛擬機器的 Azure CLI 範例

hello 下表包含使用 Azure CLI hello 建置連結 toobash 指令碼。

| | |
|---|---|
|**建立虛擬機器**||
| [建立虛擬機器](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | 以最低限度的組態建立 Linux 虛擬機器。 |
| [建立完整設定的虛擬機器](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | 建立資源群組、虛擬機器和所有相關資源。|
| [建立高可用性的虛擬機器](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | 依據高可用性和負載平衡組態建立數個虛擬機器。 |
| [建立已啟用 Docker 功能的 VM](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | 建立虛擬機器、設定此 VM 作為 Docker 主機，然後執行 NGINX 容器。 |
| [建立 VM 並執行組態指令碼](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | 建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall NGINX。 |
| [建立已安裝 WordPress 的 VM](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | 建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall WordPress。 |
| [從受控 OS 磁碟建立 VM](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | 連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。 |
| [從快照集建立 VM](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | 從快照集建立虛擬機器，請先建立從快照集的 受管理的磁碟，然後附加 hello 新受管理的磁碟與作業系統磁碟。 |
|**管理儲存體**||
| [從 VHD 建立受控磁碟](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | 從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。  |
| [從快照集建立受控磁碟](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | 從快照集建立受控磁碟。 |
| [複製受管理的磁碟 toosame 或不同的訂用帳戶](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 受管理的複本磁碟 toosame 或不同的訂用帳戶，但在 hello 相同與 hello 父區域管理磁碟。 
| [將快照集匯出為 VHD tooa 儲存體帳戶](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | 將受管理的快照集匯出為不同的區域中的 VHD tooa 儲存體帳戶。 |
| [複製快照集 toosame 或不同的訂用帳戶](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 複製快照集 toosame 或 hello 相同但在不同的訂閱與 hello 父快照集的區域。 |
|**網路虛擬機器**||
| [保護虛擬機器之間的網路流量](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | 建立兩部虛擬機器、所有相關資源以及內部和外部網路安全性群組 (NSG)。 |
|**保護虛擬機器**||
| [加密 VM 和資料磁碟](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。 |
|**監視虛擬機器**||
| [使用 Operations Management Suite 監視 VM](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | 建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。  |
|**針對虛擬機器進行疑難排解**||
| [針對 VM 作業系統磁碟進行疑難排解](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Hello 作業系統磁碟從掛接一個 VM 當做資料磁碟上的第二個 VM。 |
| | |
