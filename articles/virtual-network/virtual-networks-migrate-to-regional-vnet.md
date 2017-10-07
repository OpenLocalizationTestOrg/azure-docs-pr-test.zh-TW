---
title: "Azure 虛擬網路 （傳統） 的同質群組 tooa 區域 aaaMigrate |Microsoft 文件"
description: "了解如何 toomigrate 虛擬網路 （傳統） 從親和性群組 tooa 區域。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>移轉的同質群組 tooa 區域虛擬網路 （傳統）

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello Resource Manager 部署模型。

同質群組確保的 hello 很遠，啟用這些資源 toocommunicate 速度較快的伺服器實體裝載相同同質群組內建立資源。 Hello 過去，同質群組是建立虛擬網路 （傳統） 的需求。 執行之後，受管理虛擬網路 （傳統） 的 hello 網路管理員服務只能在一組實體伺服器或延展單位。 結構改進增加 hello 範圍的網路管理 tooa 區域。

由於這些架構的改進，因而導致不再建議使用同質群組，或不再需要虛擬網路 (傳統)。 區域取代 hello 使用同質群組的虛擬網路 （傳統）。 與區域相關聯的虛擬網路 (傳統) 稱為地區虛擬網路。

我們建議您在一般情況下不要使用同質群組。 除了 hello 虛擬網路需求，同質群組也是重要 toouse tooensure 資源，例如計算 （傳統） 和儲存體 （傳統），已放置彼此的附近。 不過，與目前 Azure 網路架構 hello，這些位置需求不再需要。

> [!IMPORTANT]
> 雖然技術上仍然可以 toocreate 與同質群組相關聯的虛擬網路，沒有任何令人信服原因 toodo 因此。 許多虛擬網路功能 (例如網路安全性群組) 只有在使用區域虛擬網路時才能使用，且不適用於與同質群組相關聯的虛擬網路。
> 
> 

## <a name="edit-hello-network-configuration-file"></a>編輯 hello 網路組態檔

1. 匯出 hello 網路組態檔。 toolearn 如何 tooexport 網路組態檔使用 PowerShell 或 hello Azure 命令列介面 (CLI) 1.0，請參閱[設定虛擬網路使用網路組態檔](virtual-networks-using-network-configuration-file.md#export)。
2. 編輯 hello 網路組態檔，取代**AffinityGroup**與**位置**。 您需針對 **Location** 指定 Azure [區域](https://azure.microsoft.com/regions)。
   
   > [!NOTE]
   > hello**位置**是您指定 hello 與虛擬網路 （傳統） 相關聯的同質群組的 hello 區域。 例如，如果您的虛擬網路 （傳統） 與移轉時，位於美國西部、 同質群組相關聯您**位置**必須指向 tooWest 美國。 
   > 
   > 
   
    編輯 hello 遵循您的網路組態檔中的程式行、 取代您自己 hello 值： 
   
    **舊值：**\<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\> 
   
    **新值：**\<VirtualNetworkSitename="VNetUSWest" Location="West US"\>
3. 儲存您的變更和[匯入](virtual-networks-using-network-configuration-file.md#import)hello 網路組態 tooAzure。

> [!NOTE]
> 這項移轉不會產生任何停機時間 tooyour 服務。
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>如果您在同質群組 （傳統） 的 VM 哪些 toodo
Vm （傳統），目前正在同質群組中不需要 toobe 從 hello 同質群組中移除。 一旦部署 VM 時，就會是已部署的 tooa 單一延展單位。 同質群組可限制 hello 的可用 VM 集合大小為新的 VM 部署，但是已部署的任何現有 VM 已經限制 toohello 組的 VM 大小可用 hello 縮放單位中的 hello 部署 VM。 因為 hello VM 已部署 tooa 擴充單元，從同質群組中移除 VM 沒有 hello VM 上的任何作用。
