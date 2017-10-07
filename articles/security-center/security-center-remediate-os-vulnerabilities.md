---
title: "Azure 資訊安全中心中的 aaaRemediate 作業系統弱點 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 修復作業系統弱點 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>修復 Azure 資訊安全中心的 OS 弱點
Azure 資訊安全中心會分析每日虛擬機器 (VM) 作業系統 (OS) 的組態可以讓 hello VM 更容易遭受 tooattack 和建議的組態變更 tooaddress 這些弱點。 資訊安全中心建議 VM 的作業系統組態與 hello 建議組態規則不相符時，解決弱點。

> [!NOTE]
> 如需有關 hello 受監視的特定組態的詳細資訊，請參閱 hello[建議的組態設定的規則清單](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  本文件不是一份逐步解說指南。
>
>

1. 在 hello**建議**刀鋒視窗中，選取**修復作業系統弱點**。
   ![修復 OS 弱點][1]

    hello**修復作業系統弱點**刀鋒視窗會開啟，並列出其不符合建議的設定規則的 hello 的 OS 設定 Vm。  針對每個 VM，hello 刀鋒視窗中識別：

   * **失敗的規則**-hello hello VM 的 OS 設定的規則數目失敗。
   * **上次掃描時間**--hello 日期和時間資訊安全中心上次掃描 hello VM 的 OS 設定。
   * **狀態**-hello hello 弱點的目前狀態：

     * 開啟： hello 的弱點可能會有尚未找出尚未
     * 在進度： Hello 的弱點可能會目前套用，您不需要任何動作
     * 判斷是否已解決： hello 的弱點可能會已解決 （當 hello 問題已解決，hello 項目會呈現灰色）
   * **嚴重性**-所有的弱點可能會設定 tooa 嚴重性低，表示應該處理弱點，但不需要立即注意。

2. 選取 VM。 刀鋒視窗中的，VM 會開啟，並顯示 hello 規則失敗。
   ![失敗的設定規則][2]

3. 選取規則。 在此範例中，我們選取 [密碼必須符合複雜性需求] 。 刀鋒視窗會開啟描述 hello 失敗規則和 hello 的影響。 檢閱 hello 詳細資料，並考慮如何套用作業系統設定。
  ![Hello 失敗規則描述][3]

  資訊安全中心 configuration 規則使用通用組態列舉 (CCE) tooassign 唯一識別碼。 在這個刀鋒視窗上提供下列資訊的 hello:

  - 名稱 -- 規則的名稱
  - 嚴重性 -- 嚴重、重要或警告的 CCE 嚴重性值
  - Hello 規則的 CCIED-CCE 唯一識別碼
  - 說明 -- 規則的說明
  - 弱點 -- 不套用規則的弱點或風險說明
  - 影響 -- 套用規則時的業務影響
  - 預期值 — 值預期會在資訊安全中心會分析您的 VM OS 組態，根據 hello 規則
  - 資訊安全中心所使用的 hello 規則對您 VM OS 的組態分析期間規則作業-規則作業
  - VM OS 設定針對 hello 規則的分析後傳回的實際值--值
  - 評估結果 -- 分析的結果︰通過、失敗

## <a name="see-also"></a>另請參閱
本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議"補救作業系統弱點。 」 您可以檢閱 hello 組組態規則[這裡](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。 資訊安全中心會使用組態規則 CCE （通用組態列舉） tooassign 唯一識別碼。 請瀏覽 hello [CCE](https://nvd.nist.gov/cce/index.cfm)如需詳細資訊的站台。

toolearn 有關資訊安全中心的詳細資訊，請參閱下列資源的 hello:

* [Azure 資訊安全中心支援的平台](security-center-os-coverage.md) - 提供支援的 Windows 與 Linux VM 清單。
* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
