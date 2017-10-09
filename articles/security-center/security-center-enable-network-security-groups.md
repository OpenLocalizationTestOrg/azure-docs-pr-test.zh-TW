---
title: "aaaEnable Azure 資訊安全中心中的網路安全性群組 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用網路安全性群組 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>在 Azure 資訊安全中心啟用網路安全性群組
如果尚未啟用網路安全性群組 (NSG)，Azure 資訊安全中心會建議您啟用。 Nsg 包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。 NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。 NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。 此外，流量 tooan 個別 VM 可能會限制進一步將 NSG 直接 toothat VM。 toolearn 更看到[網路安全性群組 (NSG) 是什麼？](../virtual-network/virtual-networks-nsg.md)

如果您沒有啟用 Nsg，資訊安全中心會呈現兩個建議 tooyou： 啟用網路安全性群組的相關子網路和虛擬機器上啟用網路安全性群組上。 您選擇哪一個層級、 子網路或 VM，tooapply Nsg。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**啟用網路安全性群組**子網路上或在虛擬機器上。
   ![啟用網路安全性群組][1]
2. 這會開啟刀鋒視窗中 hello**設定遺失的網路安全性群組**子網路或虛擬機器，根據您選取的 hello 建議。 選取子網路或虛擬機器 tooconfigure NSG 上。

   ![針對子網路設定 NSG][2]

   ![針對 VM 設定 NSG][3]
3. 在 hello**選擇網路安全性群組**刀鋒視窗中，選取現有的 NSG，或選取**建立新**toocreate NSG。

   ![選擇網路安全性群組][4]

如果您建立 NSG，請依照下列中的 hello 步驟[toomanage Nsg 使用 hello Azure 入口網站的方式](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)toocreate NSG 並設定安全性規則。

## <a name="see-also"></a>另請參閱
這篇文章會示範如何 tooimplement 會 hello 資訊安全中心建議 」 啟用網路安全性群組 」 的子網路或虛擬機器。 toolearn 進一步了解啟用 Nsg，請參閱 hello 下列資訊：

* [什麼是網路安全性群組 (NSG)？](../virtual-network/virtual-networks-nsg.md)
* [如何使用 toomanage Nsg hello Azure 入口網站](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
