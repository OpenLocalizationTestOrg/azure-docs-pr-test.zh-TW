---
title: "透過 Azure 資訊安全中心中的網際網路對向端點 aaaRestrict 存取 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 限制存取透過網際網路對向端點 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>在 Azure 資訊安全中心限制透過網際網路面向端點的存取
如果您的任一網路安全性群組 (NSG) 有一或多個輸入規則允許來自任何來源 IP 位址的存取，Azure 資訊安全中心會建議您限制透過網際網路面向端點的存取。 開啟存取太 「 任何 」 可能會讓攻擊者 tooaccess 您的資源。 資訊安全中心會建議您編輯這些輸入的規則 toorestrict 存取 toosource IP 位址，實際需要的存取。

有「任何」來源的任何非 Web 連接埠，就會產生這項建議。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議刀鋒視窗**，選取**限制存取透過網際網路對向端點**。

   ![限制透過網際網路面向端點的存取][1]
2. 這會開啟刀鋒視窗中 hello**限制存取透過網際網路對向端點**。 此刀鋒視窗會列出 hello 虛擬機器 (Vm) 的輸入建立潛在的安全性問題的規則。 選取 VM。

   ![選取 VM][2]
3. hello **NSG**刀鋒視窗會顯示網路安全性群組的詳細資訊，相關的輸入規則，以及 hello 相關聯的 VM。 選取**編輯輸入的規則**tooproceed 編輯的輸入的規則。

   ![[網路安全性群組] 刀鋒視窗][3]
4. 在 hello**輸入安全性規則**刀鋒視窗中選取 hello tooedit 輸入的規則。 在此範例中，我們選取 [允許 Web] 。

   ![輸入安全性規則][4]

   請注意，您也可以選取**預設規則**toosee hello 組由所有 Nsg 包含預設規則。 無法刪除 hello 預設規則，但因為他們指派較低的優先順序，它們會覆寫由您所建立的 hello 規則。 深入了解[預設規則](../virtual-network/virtual-networks-nsg.md#default-rules)。

   ![預設規則][5]
5. 在 hello **AllowWeb**刀鋒視窗中，編輯 hello 屬性，因此，hello hello 輸入規則的**來源**是 IP 位址或 IP 位址區塊。 toolearn 進一步了解 hello 屬性 hello 輸入規則，請參閱[NSG 規則](../virtual-network/virtual-networks-nsg.md#nsg-rules)。

   ![編輯輸入規則][6]

## <a name="see-also"></a>另請參閱
本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 「 限制存取透過網際網路對向端點 」。 toolearn 進一步了解啟用 Nsg 及規則，請參閱 hello 下列資訊：

* [什麼是網路安全性群組 (NSG)？](../virtual-network/virtual-networks-nsg.md)
* [如何使用 toomanage Nsg hello Azure 入口網站](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
