---
title: "aaaMove Windows AWS Vm tooAzure |Microsoft 文件"
description: "移動 Amazon Web Services (AWS) EC2 Windows 執行個體 tooAzure 使用 Azure PowerShell 的虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>使用 PowerShell 的 Amazon Web Services (AWS) tooAzure 從移動 Windows VM

如果您正在評估 Azure 虛擬機器來裝載您的工作負載，您可以匯出現有的 Amazon Web Services (AWS) EC2 Windows VM 執行個體，然後上傳 hello 虛擬硬碟 (VHD) tooAzure。 一次上傳 VHD 的 hello，您可以建立新的 VM 在 Azure 中從 hello VHD。 

本主題涵蓋將單一 VM 從 AWS tooAzure。 如果您想從大規模 AWS tooAzure toomove Vm，請參閱[移轉虛擬機器中使用 Azure Site Recovery 的 Amazon Web Services (AWS) tooAzure](../../site-recovery/site-recovery-migrate-aws-to-azure.md)。

## <a name="prepare-hello-vm"></a>準備 VM hello 
 
您可以上傳一般化並加以特製化 Vhd tooAzure。 每個類型都需要您從 AWS 匯出之前先準備 hello VM。 

- **一般化 VHD** - 一般化 VHD 已使用 Sysprep 移除您所有的個人帳戶資訊。 如果您想 toouse hello 做為映像 toocreate VHD 中的新 Vm，您應該： 
 
    * [準備 Windows VM](prepare-for-upload-vhd-image.md)。  
    * Hello 虛擬機器使用 Sysprep 來一般化。  

 
- **特製化 VHD** -特製化的 VHD 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM。 如果您想 toouse hello VHD 當做-是 toocreate 新的 VM，請完成下列步驟的 hello。  
    * [準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md)。 **不這麼做**一般化 hello VM 使用 Sysprep。 
    * 移除任何客體的虛擬化工具和 hello VM （也就是 VMware 工具） 所安裝的代理程式。 
    * 請確定 hello VM 是已設定的 toopull 其 IP 位址和 DNS 設定，透過 DHCP。 這可確保該 hello 伺服器會在啟動時，取得 hello VNet 內的 IP 位址。  


## <a name="export-and-download-hello-vhd"></a>匯出並下載 hello VHD 

匯出 hello EC2 執行個體 tooa Amazon S3 貯體中的 VHD。 Hello Amazon 文件集主題所述步驟 hello[匯出執行個體做為 VM 使用 VM 匯入/匯出](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html)和執行的 hello[建立執行個體-匯出的工作](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html)命令 tooexport hello EC2執行個體 tooa VHD 檔案。 

hello 匯出的 VHD 檔案會儲存在您指定的 hello Amazon S3 貯體。 hello 基本語法為匯出 hello VHD 下面只 hello 預留位置文字取代中<brackets>與您的資訊。

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

一旦匯出的 hello VHD，請依照下列中的 hello 指示[如何從 S3 貯體下載物件？](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD 檔案從 hello S3 貯體。 

> [!IMPORTANT]
> AWS 費用下載 hello VHD 的資料傳輸費用。 如需詳細資訊，請參閱 [Amazon S3 價格](https://aws.amazon.com/s3/pricing/)。


## <a name="next-steps"></a>後續步驟

現在您可以上傳 hello VHD tooAzure，並建立新的 VM。 

- 如果您已執行 Sysprep 上您的來源太**一般化**前面匯出，請參閱[一般化的 VHD 上傳，並在 Azure 中使用 toocreate 新的 Vm](upload-generalized-managed.md)
- 如果您沒有匯出之前先執行 Sysprep，hello VHD 會被視為**特製化**，請參閱[上傳特製化的 VHD tooAzure 並建立新的 VM](create-vm-specialized.md)

 
