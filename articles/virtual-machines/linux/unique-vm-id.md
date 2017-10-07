---
title: "Azure Linux VM 識別碼 aaaGet |Microsoft 文件"
description: "描述如何 tooget 和使用 Azure Linux VM 唯一識別碼。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>存取和使用 Azure VM 的唯一識別碼
Azure VM 的唯一識別碼是在所有 Azure IaaS VM 的 SMBIOS 中編碼並儲存的一個 128 位元識別碼，而且目前可以使用平台的 BIOS 命令讀取。

Azure VM 的唯一識別碼是唯讀屬性。 在重新開機關機 (計劃中或未計劃)、開始/停止解除配置、服務修復或就地還原之後，Azure 的唯一 VM 識別碼並不會變更。 不過，如果 hello VM 是快照式和複製 toocreate 的新執行個體，就會設定新的 Azure VM 識別碼。

> [!NOTE]
> 如果您有舊版所建立的 Vm，並執行，因為這項新功能已推出 (2014 年 9 月 18 日)，請重新啟動 VM tooautomatically 取得 Azure 的唯一識別碼。
> 
> 

tooaccess 從 Azure 唯一 VM 識別碼 hello VM 內：

## <a name="create-a-vm"></a>建立 VM
如需詳細資訊，請參閱[建立虛擬機器](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>連接 toohello VM
如需詳細資訊，請參閱 [Linux 中的 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>查詢 VM 的唯一識別碼
命令 (範例使用 **Ubuntu**)：

```bash
sudo dmidecode | grep UUID
```

範例預期的結果：

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

TooBig 位元組由小到大位元順序，因為 hello 實際唯一 VM 識別碼在此情況下會是：

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Azure VM 的唯一識別碼 hello VM 正執行於 Azure 或內部部署且可協助您授權、 報告或一般追蹤的需求可能對您的 Azure IaaS 部署是否可以用於不同的案例。 許多的獨立軟體廠商建置應用程式和認證它們在 Azure 上可能需要 tooidentify 透過其生命週期和 tootell Azure VM，如果 hello VM 在 Azure 中，在內部部署或其他雲端提供者上執行。 此平台識別項例如有助於偵測 hello 軟體是否已正確授權或協助 toocorrelate 例如 tooassist 設定 hello 右 hello 右平台和度量 tootrack 任何 VM 資料 tooits 來源並將這些計量之間的相互關聯其他用途。

