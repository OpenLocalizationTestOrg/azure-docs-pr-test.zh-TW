---
title: "重設 Azure VPN 閘道 tooreestablish IPsec 通道數 |Microsoft 文件"
description: "這篇文章會引導您重設您的 Azure VPN 閘道 tooreestablish IPsec 通道。 hello 文章適用 tooVPN 閘道在傳統，hello 和 hello 資源管理員部署模型。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>重設 VPN 閘道

如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。 在此情況下，您在內部部署 VPN 裝置是所有運作正常，但您不能 tooestablish 與 hello Azure VPN 閘道 IPsec 通道。 本文可協助您重設 VPN 閘道。

### <a name="what-happens-during-a-reset"></a>重設期間會發生什麼事？

VPN 閘道是由兩個在「作用中-待命」設定中執行的 VM 執行個體所組成。 當您重設 hello 閘道時，它會重新啟動 hello 閘道，然後重新套用 hello 跨單位組態 tooit。 hello 閘道會保留 hello 已經有公用 IP 位址。 這表示您不需要 tooupdate hello VPN 路由器設定新的公用 IP 位址的 Azure VPN 閘道。

當您發出 hello 命令 tooreset hello 閘道時，hello 目前作用中的執行個體 hello Azure VPN 閘道立即重新開機。 Hello hello 作用中執行個體 （即將重新開機），toohello 待命執行個體容錯移轉期間會有短暫的間隔。 hello 間距應該小於一分鐘。

如果未還原 hello 連接 hello 第一次重新開機後，問題 hello 相同命令再次 tooreboot hello 第二個 VM 執行個體 （hello 新使用中的閘道）。 要求後 tooback hello 兩次重新開機時，會有稍微更長的時間 （作用中與待命） 這兩個 VM 執行個體，即將重新開機。 這會導致較長的間隔上 hello VPN 連線能力，向上 too2 too4 分鐘 Vm toocomplete hello 重新開機。

在兩次重新開機之後, 如果仍發生跨單位連線問題，請開啟支援要求從 hello Azure 入口網站。

## <a name="before"></a>開始之前

您重設您的閘道之前，請確認以下列出每個 IPsec-網站 (S2S) VPN 通道的 hello 索引鍵的項目。 Hello 項目中的任何不相符會導致 hello 中斷連線的 S2S VPN 通道。 正在驗證及更正您在內部部署和 Azure VPN 閘道的 hello 組態可讓您不需要重新開機，並中斷的 hello hello 閘道上的其他工作連接。

請確認下列項目重設您的閘道器之前的 hello:

* hello 網際網路 IP 位址 (Vip) 這兩個 hello Azure VPN 閘道和 hello 內部部署 VPN 閘道已正確設定這兩個 hello 在內部部署 VPN Azure 與 hello 原則中。
* hello 預先共用的金鑰必須 hello Azure 與內部部署 VPN 閘道上相同。
* 如果您要套用特定的 IPsec/IKE 組態，例如加密，雜湊演算法和 PFS （完整轉寄密碼），請確定兩者 hello Azure 和內部部署 VPN 閘道具有 hello 相同的組態。

## <a name="portal"></a>Azure 入口網站

您可以重設資源管理員 VPN 閘道使用 hello Azure 入口網站。 如果您想 tooreset 傳統的閘道，請參閱 hello [PowerShell](#resetclassic)步驟。

### <a name="resource-manager-deployment-model"></a>資源管理員部署模型。

1. 開啟 hello [Azure 入口網站](https://portal.azure.com)並瀏覽您想 tooreset toohello 資源管理員虛擬網路閘道。
2. 在 hello 刀鋒視窗中的 hello 虛擬網路閘道，按一下 重設。

  ![重設 VPN 閘道刀鋒視窗](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. 在 [hello 重刀鋒視窗，請按一下 hello**重設**] 按鈕。

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>資源管理員部署模型。

重設閘道為 hello cmdlet**重設 AzureRmVirtualNetworkGateway**。 在之前執行重設，請確定您擁有 hello 最新版本的 hello[資源管理員 PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)。 hello 下列範例會重設虛擬網路閘道 hello TestRG1 資源群組中名為 VNet1GW:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

結果︰

當您收到傳回的結果時，您可以假設 hello 閘道重設成功。 不過，並沒有明確地指出該 hello 重設成功的 hello 傳回結果中。 如果您想在 hello 記錄 toosee 密切 toolook 完全 hello 閘道重設時發生，您可以檢視該資訊在 hello [Azure 入口網站](https://portal.azure.com)。 在 hello 入口網站中，瀏覽過**'GatewayName'-> 資源健全狀況**。

### <a name="resetclassic"></a>傳統部署模型

重設閘道為 hello cmdlet**重設 AzureVNetGateway**。 在之前執行重設，請確定您擁有 hello 最新版本的 hello[服務管理 (SM) PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0)。 hello 下列範例會重設虛擬網路，名為"ContosoVNet"hello 閘道：

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

結果︰

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Azure CLI

tooreset hello 閘道，使用 hello [az 網路 vnet 閘道重設](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset)命令。 hello 下列範例會重設虛擬網路閘道 hello TestRG5 資源群組中名為 VNet5GW:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

結果︰

當您收到傳回的結果時，您可以假設 hello 閘道重設成功。 不過，並沒有明確地指出該 hello 重設成功的 hello 傳回結果中。 如果您想在 hello 記錄 toosee 密切 toolook 完全 hello 閘道重設時發生，您可以檢視該資訊在 hello [Azure 入口網站](https://portal.azure.com)。 在 hello 入口網站中，瀏覽過**'GatewayName'-> 資源健全狀況**。
