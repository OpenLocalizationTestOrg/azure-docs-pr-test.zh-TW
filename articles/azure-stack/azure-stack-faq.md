---
title: "aaaFrequently Azure 堆疊常見問題 |Microsoft 文件"
description: "Azure 堆疊常見問題集。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a>Azure 堆疊的常見問題集
## <a name="deployment"></a>部署
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a>我需要 tooformat 我的資料磁碟之前啟動或重新啟動安裝？
磁碟應該是以原始格式。 如果您重新安裝 hello 作業系統，您可能需要 toocheck hello 舊的存放集區是否仍然存在，並刪除使用 hello 下列步驟：

1. 開啟 [伺服器管理員]。
2. 選取存放集區。
3. 查看是否列出存放集區。
4. 以滑鼠右鍵按一下**存放集區**如果列出和啟用讀取 / 寫入。
5. 以滑鼠右鍵按一下**Virtual Hard Disk** （左下的角），選取 刪除。
6. 以滑鼠右鍵按一下**存放集區**並按一下 [刪除]。
7. 一次啟動 Azure 堆疊指令碼，並確認 hello 磁碟驗證通過。

（選擇性） 您可以使用下列指令碼的 hello:

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a>可以使用所有的 SSD 磁碟 hello POC 安裝中的 hello 存放集區嗎？
如需有關存放裝置設定的詳細資訊，請參閱 hello[需求指南](azure-stack-deploy.md)。

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a>我可以使用 Microsoft Azure 堆疊 POC hello NVMe 資料磁碟嗎？
儲存空間直接存取支援 NVMe 磁碟，而 Azure 堆疊只支援子集 hello 可能是磁碟機類型以及可能的組合 Storage Spaces Direct。  請參閱 hello[需求指南](azure-stack-deploy.md)如需詳細資訊。 

### <a name="how-can-i-reinstall-azure-stack"></a>如何重新安裝 Azure 堆疊？
您可以依照 hello 步驟在 hello[重新部署指南](azure-stack-redeploy.md)。  

## <a name="tenant"></a>租用戶
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a>可以為租用戶部署我自己的映像嗎？
[是]，就像在 Azure 中，租用戶可以上傳 Azure 的堆疊中的映像，此外 hello toousing hello 映像服務管理員。 如需概觀，請參閱 hello[加入 VM 映像](azure-stack-add-vm-image.md)。 

## <a name="testing"></a>測試
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a>可以使用巢狀虛擬化 tootest hello Microsoft Azure 堆疊 POC 嗎？
不支援巢狀虛擬化或 Azure 堆疊 Technical Preview 3 中進行測試。

## <a name="virtual-machines"></a>虛擬機器
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a>Azure 堆疊支援動態磁碟的虛擬機器？
Azure 堆疊不支援動態磁碟。


## <a name="next-steps"></a>後續步驟
[疑難排解](azure-stack-troubleshooting.md)

