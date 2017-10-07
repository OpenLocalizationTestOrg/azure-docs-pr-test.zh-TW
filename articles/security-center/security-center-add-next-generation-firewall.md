---
title: "下一個層代防火牆 Azure 資訊安全中心 aaaAdd |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 加入 下一步產生防火牆 * * 和 * * 路由流量透過 NGFW 只 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>在 Azure 資訊安全中心新增新一代防火牆
Azure 資訊安全中心可能會建議您新增的下一個層代防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護。 本文件將逐步引導您透過如何的範例 toodo 這。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**加入下一個層代防火牆**。
   ![新增新一代防火牆][1]
2. 在 hello**加入下一個層代防火牆**刀鋒視窗中，選取一個端點。
   ![選取端點][2]
3. 第二個 [新增新一代防火牆]  刀鋒視窗隨即開啟。 如果您可以選擇 toouse 現有的方案使用，或您可以建立一個新。 此範例中沒有任何可用的現有解決方案，因此我們將建立一個 NGFW。
   ![新建新一代防火牆][3]
4. toocreate NGFW 中，選取方案，從 hello 整合協力電腦清單。 在此範例中，我們會選取 [檢查點]。
   ![選取新一代防火牆解決方案][4]
5. hello**檢查點**刀鋒視窗會開啟提供您 hello 夥伴方案的相關資訊。 選取**建立**hello 資訊刀鋒視窗中。
   ![防火牆資訊刀鋒視窗][5]
6. hello**建立虛擬機器**刀鋒視窗隨即開啟。 這裡您可以輸入執行的虛擬機器 (VM) 的必要的 toospin hello NGFW 的資訊。 遵循 hello 步驟並提供所需的 hello NGFW 資訊。 選取 [確定] tooapply。
   ![建立虛擬機器 toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>僅透過 NGFW 路由傳送流量
傳回 toohello**建議**刀鋒視窗。 在您透過資訊安全中心加入 NGFW 後會產生新的項目，稱為「僅透過 NGFW 路由傳送流量」 。 只有當您透過資訊安全中心安裝了 NGFW，才會建立這項建議。 如果您有網際網路對向端點時，資訊安全中心會建議您設定強制傳入的流量 tooyour 透過您 NGFW VM 的網路安全性群組規則。

1. 在 hello**建議刀鋒視窗**，選取**只透過 NGFW 流量路由傳送**。
   ![僅透過 NGFW 路由傳送流量][7]
2. 這會開啟刀鋒視窗中 hello**只透過 NGFW 流量路由傳送**，其中會列出您可以路由傳送流量的 Vm。 Hello 清單中選取 VM。
   ![選取 VM][8]
3. Hello 刀鋒視窗中的選取 VM 隨即開啟，顯示相關的輸入的規則。 說明提供後續可能步驟的詳細資訊。 選取**編輯輸入的規則**tooproceed 編輯的輸入的規則。 hello 期望是**來源**未設定太**任何**hello 網際網路對向端點連結與 hello NGFW。 toolearn 進一步了解 hello 屬性 hello 輸入規則，請參閱[NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。
   ![設定規則 toolimit 存取][9]
   ![編輯輸入的規則][10]

## <a name="see-also"></a>另請參閱
這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 新增產生防火牆 下一步 」。 toolearn 深入了解 NGFWs 和 hello 的檢查點協力廠商解決方案，請參閱 hello 下列資訊：

* [新一代防火牆](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [檢查點 vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
