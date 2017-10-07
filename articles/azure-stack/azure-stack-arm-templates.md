---
title: "aaaUse Azure 堆疊中的 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何在 Azure 堆疊 tooprovision 資源 toouse Azure Resource Manager 範本。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a>在 Azure Stack 中使用 Azure 資源管理員範本
Azure 資源管理員範本部署和佈建您的應用程式在單一、 協調作業中的所有 hello 資源。 您也可以重新部署範本 toomake 變更 toohello 資源 hello 資源群組中。

這些範本可以部署與 hello Microsoft Azure 堆疊入口網站、 PowerShell、 hello 命令列，以及 Visual Studio。

hello 遵循快速入門範本位於[GitHub](http://aka.ms/azurestackgithub):

## <a name="deploy-sharepoint-non-high-availability"></a>部署 SharePoint (非高可用性)
使用 hello PowerShell DSC 延伸模組 toocreate SharePoint 2013 伺服器陣列，其中包含 hello 下列資源：

* 虛擬網路
* 三個儲存體帳戶
* 兩個外部負載平衡器
* 一部 VM，設定為具單一網域之新樹系的網域控制站
* 一部 VM，設定為 SQL Server 2014 獨立伺服器
* 一部 VM，設定為一部電腦的 SharePoint 2013 伺服器陣列

## <a name="deploy-ad-non-high-availability"></a>部署 AD (非高可用性)
使用 hello PowerShell DSC 延伸模組 toocreate AD 網域控制站伺服器，其中包含 hello 下列資源：

* 虛擬網路
* 一個儲存體帳戶
* 一個外部負載平衡器
* 一部 VM，設定為具單一網域之新樹系的網域控制站

## <a name="deploy-adsql-non-high-availability"></a>部署 AD/SQL (非高可用性)
使用 hello PowerShell DSC 延伸模組 toocreate SQL Server 2014 獨立伺服器，其中包含 hello 下列資源：

* 虛擬網路
* 兩個儲存體帳戶
* 一個外部負載平衡器
* 一部 VM，設定為具單一網域之新樹系的網域控制站
* 一部 VM，設定為 SQL Server 2014 獨立伺服器

## <a name="vm-dsc-extension-azure-automation-pull-server"></a>VM-DSC-Extension-Azure-Automation-Pull-Server
使用 hello PowerShell DSC 延伸模組 tooconfigure 現有的虛擬機器本機設定管理員 (LCM)，然後登錄 tooan Azure 自動化帳戶 DSC 提取的伺服器。

## <a name="create-a-virtual-machine-from-a-user-image"></a>從使用者映像建立虛擬機器
從自訂使用者映像建立虛擬機器。 這個範本也會部署虛擬網路 (含 DNS)、公用 IP 位址及網路介面。

## <a name="simple-vm"></a>簡單的 VM
部署一部 Windows VM，其中包含虛擬網路 (含 DNS)、公用 IP 位址及網路介面。

## <a name="cancel-a-running-template-deployment"></a>取消執行中的範本部署
toocancel 執行的範本部署，使用 hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet。

## <a name="next-steps"></a>後續步驟
[部署範本與 hello 入口網站](azure-stack-deploy-template-portal.md)

[Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)

