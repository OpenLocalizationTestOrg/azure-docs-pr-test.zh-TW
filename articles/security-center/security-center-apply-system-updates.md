---
title: "在 Azure 資訊安全中心 aaaApply 系統更新 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 套用系統更新 * * 和 * * 在系統更新 * * 後重新開機。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>在 Azure 資訊安全中心套用系統更新
Azure 資訊安全中心每日監視 Windows 和 Linux 虛擬機器 (VM) 是否有遺漏的作業系統更新。 資訊安全中心會根據 Windows VM 上設定的服務，從 Windows Update 或 Windows Server Update Services (WSUS) 擷取可用的安全性和重大更新清單。  資訊安全中心也會檢查 hello 最新更新 Linux 系統中。 如果您的 VM 遺漏系統更新，資訊安全中心會建議您套用系統更新

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**套用系統更新**。

   ![套用系統更新][1]
2. hello**套用系統更新**刀鋒視窗隨即開啟並顯示遺漏的系統更新 Vm 的清單。 選取 VM。

   ![選取 VM][2]
3. 隨即開啟一個刀鋒視窗，其中顯示該 VM 的遺漏更新的清單。 選取系統更新。 在此範例中，我們選取 KB3156016。

   ![遺漏的安全性更新][3]

4. Hello 中的 hello 步驟**安全性更新**刀鋒視窗 tooapply hello 遺失更新。

   ![安全性更新][4]

## <a name="reboot-after-system-updates"></a>在系統更新之後重新開機
1. 傳回 toohello**建議**刀鋒視窗。 在您套用系統更新之後會產生新的項目，稱為「在系統更新之後重新開機」。 此項目可讓您知道您需要 tooreboot hello VM toocomplete hello 套用的程序的系統更新。

   ![在系統更新之後重新開機][5]
2. 選取 [在系統更新之後重新開機] 。 這會開啟**重新啟動已暫止 toocomplete 系統更新**刀鋒視窗中顯示的 Vm，您需要 toorestart toocomplete hello 清單適用於系統更新程序。

   ![重新啟動擱置中][6]

重新啟動 hello VM 從 Azure toocomplete hello 程序。

## <a name="see-also"></a>另請參閱
toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
