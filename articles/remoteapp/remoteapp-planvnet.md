---
title: "aaaHow tooplan 您的 Azure RemoteApp 集合的虛擬網路 |Microsoft 文件"
description: "深入了解如何 tooplan 虛擬網路，以 Azure RemoteApp 集合。"
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>如何 tooplan 的 Azure RemoteApp 虛擬網路
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

本文件說明如何註冊您的 Azure 虛擬網路 (VNET) 和 Azure RemoteApp 的子網路 hello tooset。 如果您不熟悉 Azure 虛擬網路，這是一種功能，可協助您 toovirtualize 您網路基礎結構 toohello 雲端和 toocreate 混合式解決方案使用 Azure 和內部部署資源。 您可以在 [此處](../virtual-network/virtual-networks-overview.md)閱讀相關資訊。

如果您想要 toodefine 安全性原則 （內送和外寄） 的流量部署 Azure RemoteApp 虛擬網路中，我們強烈建議建立不同的子網路的 Azure RemoteApp，於您在 hello Azure 中部署的 hello 其餘部分虛擬網路。 如需有關如何 toodefine 安全性原則，在您的 Azure 虛擬網路子網路的詳細資訊，請閱讀[網路安全性群組 (NSG) 是什麼？](../virtual-network/virtual-networks-nsg.md)。

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>具有 Azure 虛擬網路的 Azure RemoteApp 集合類型
hello 下列圖形顯示 hello 兩個不同的集合選項時要 toouse 虛擬網路。

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>具有 VNET 的 Azure RemoteApp 雲端集合
 ![Azure RemoteApp - 具有 VNET 的雲端集合](./media/remoteapp-planvpn/ra-cloudvpn.png)

這代表所有 hello 資源 hello RemoteApp 工作階段主機需要 tooaccess 在 Azure 中的都部署所在的 Azure RemoteApp 集合。 可以在 hello hello RemoteApp VNET 與同一個 VNET 或在 Azure 中不同的 VNET。

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>具有 VNET 的 RemoteApp 混合式集合
![Azure RemoteApp - 具有 VNET 的混合式集合](./media/remoteapp-planvpn/ra-hybridvpn.png)

這代表其中的某些 hello RemoteApp 工作階段主機需要 tooaccess hello 資源是在內部部署的 Azure RemoteApp 集合。 hello RemoteApp VNET 是使用 Azure 的混合式技術，例如站台對站 VPN 或 Express Route 的連結的 toohello 在內部部署網路。

## <a name="how-hello-system-works"></a>Hello 系統的運作方式
Hello 幕後 Azure RemoteApp 部署 Azure 虛擬機器 （使用您已上傳的映像） toohello 虛擬網路子網路，您選擇佈建期間。 如果您選擇混合式集合，我們會嘗試 tooresolve hello hello 在 hello 與 hello hello 虛擬網路中提供的 DNS 伺服器佈建工作流程中所輸入的網域控制站的 FQDN。  
如果您要連接 tooan 現有的虛擬網路，請確定 tooexpose hello 必要的連接埠中您 Azure RemoteApp 的子網路的網路安全性群組中。 

我們建議您改用 [Azure RemoteApp 夠大的子網路](remoteapp-vnetsizing.md)。 hello 最大支援的 Azure 虛擬網路是/8 （使用 CIDR 子網路定義）。 您的子網路應夠大 tooaccommodate 期間所有 hello Azure RemoteApp Vm 向上延展，當多個使用者同時存取 hello 應用程式。 

以下是您的虛擬網路子網路上，您將需要 tooenable hello 事情： 

1. 使用其中一個 hello 內部 Azure RemoteApp 服務的連接埠範圍 10101 10175 toocommunicate 應該允許 hello 子網路的輸出流量。
2. 允許輸出流量從您的子網路 tooconnect tooAzure 連接埠 443 上的儲存體
3. 如果您有 Azure 中裝載的 Active Directory，請確定 hello 虛擬網路子網路的 Azure RemoteApp 內任何 VM 可以 tooconnect toothat 網域控制站。 hello 虛擬網路中的 hello DNS 應該能夠 tooresolve hello 此網域控制站的 FQDN。

## <a name="virtual-network-with-forced-tunneling"></a>具有強制通道的虛擬網路
[強制通道](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) 。 我們目前不支援強制通道的現有集合 toosupport hello 移轉。  您必須 toodelete 使用 hello VNET，您要連結 tooAzure RemoteApp，並建立新的一個 tooget 強制通道的集合上啟用所有現有的集合。 

