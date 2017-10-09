---
title: "虛擬機器的 PowerShell 範例 aaaAzure |Microsoft 文件"
description: "Azure 虛擬機器 PowerShell 範例"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Azure 虛擬機器 PowerShell 範例

hello 下表包含可建立及管理 Windows 虛擬機器連結 tooPowerShell 指令碼範例。

| | |
|---|---|
|**建立虛擬機器**||
| [建立完整設定的虛擬機器](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 建立資源群組、虛擬機器和所有相關資源。|
| [建立高可用性的虛擬機器](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 依據高可用性和負載平衡組態建立數個虛擬機器。|
| [建立 VM 並執行組態指令碼](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 建立虛擬機器，並使用 hello Azure 自訂指令碼延伸 tooinstall IIS。 |
| [建立 VM 並執行 DSC 組態](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 建立虛擬機器，並使用 hello Azure 預期狀態設定 (DSC) 延伸模組 tooinstall IIS。 |
| [上傳 VHD 並建立 VM](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods 將本機 VHD 檔案 tooAzure 建立和從 hello VHD 映像，然後從該映像建立 VM。 |
| [從受控 OS 磁碟建立 VM](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。 |
| [從快照集建立 VM](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 從快照集建立虛擬機器，請先建立從快照集的 受管理的磁碟，然後附加 hello 新受管理的磁碟與作業系統磁碟。 |
|**管理儲存體**||
| [在相同或不同的訂用帳戶中從 VHD 建立受控磁碟](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 在相同或不同的訂用帳戶中，從作為 OS 磁碟的特殊化 VHD 或從作為資料磁碟的 VHD 建立受控磁碟。  |
| [從快照集建立受控磁碟](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 從快照集建立受控磁碟。 |
| [複製受管理的磁碟 toosame 或不同的訂用帳戶](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | 受管理的複本磁碟 toosame 或不同的訂用帳戶，但在 hello 相同與 hello 父區域管理磁碟。 
| [將快照集匯出為 VHD tooa 儲存體帳戶](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 將受管理的快照集匯出為不同的區域中的 VHD tooa 儲存體帳戶。 |
| [從 VDH 建立快照集](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 建立快照集 VHD toocreate 從多個相同的受管理的磁碟從快照集在短時間內。  |
| [複製快照集 toosame 或不同的訂用帳戶](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 複製快照集 toosame 或 hello 相同但在不同的訂閱與 hello 父快照集的區域。 |
|**保護虛擬機器**||
| [加密 VM 和資料磁碟](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | 建立 Azure Key Vault、加密金鑰和服務主體，然後加密 VM。 |
|**監視虛擬機器**||
| [使用 Operations Management Suite 監視 VM](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 建立虛擬機器、 安裝 hello Operations Management Suite 代理程式，並註冊 hello OMS 工作區中的 VM。  |
| | |

