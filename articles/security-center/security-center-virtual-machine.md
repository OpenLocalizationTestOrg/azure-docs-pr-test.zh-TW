---
title: "aaaAzure 資訊安全中心和 Azure 虛擬機器 |Microsoft 文件"
description: "這份文件可協助您 toounderstand 如何 Azure 資訊安全中心可以保護您 Azure 虛擬機器。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Azure 資訊安全中心和 Azure 虛擬機器
[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)可協助您防止、 偵測，並回應 toothreats。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

本文說明資訊安全中心如何協助您保護 Azure 虛擬機器 (VM)。

## <a name="why-use-security-center"></a>為何使用資訊安全中心？
資訊安全中心可協助您保護 Azure 中的虛擬機器資料，方法為提供虛擬機器的安全性設定可見性。 當資訊安全中心 」 可保護您的 Vm 時，將可提供下列功能的 hello:

* 作業系統 (OS) 安全性設定以 hello 建議組態規則
* 系統安全性和重大更新遺失
* 端點保護建議
* 磁碟加密驗證
* 弱點評估和補救
* 威脅偵測

此外 toohelping 保護您的 Azure Vm，資訊安全中心也提供安全性監視及管理雲端服務、 應用程式服務、 虛擬網路，等等。 

> [!NOTE]
> 請參閱[簡介 tooAzure 資訊安全中心](security-center-intro.md)toolearn 深入了解 Azure 資訊安全中心。
> 
> 

## <a name="prerequisites"></a>必要條件
tooget 開始使用 Azure 資訊安全中心，您將需要 tooknow 並考慮下列 hello:

* 您必須擁有 Azure 的訂用帳戶 tooMicrosoft。 請參閱[安全性中心價格](https://azure.microsoft.com/pricing/details/security-center/)，以深入了解資訊安全中心的免費和標準層。
* 資訊安全中心採用計劃，請參閱[Azure 資訊安全中心規劃及作業指南](security-center-planning-and-operations-guide.md)toolearn 深入了解規劃和作業的考量。
* 如需作業系統可支援性的相關資訊，請參閱 [Azure 資訊安全中心常見問題集 (FAQ)](security-center-faq.md)。 

## <a name="set-security-policy"></a>設定安全性原則
啟用，因此，該 Azure 資訊安全中心會收集 hello 資訊需要 tooprovide 建議和所產生的警示資料集合需求 toobe 根據您設定的 hello 安全性原則。 Hello 在圖中，您可以看到**資料收集**已開啟**上**。

安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。 在啟用安全性原則，您必須啟用資料收集，從您的虛擬機器中的資訊安全中心會收集資料排序 tooassess 他們的安全性狀態，提供安全性建議事項，並警示您 toothreats。 資訊安全中心，您會定義您的 Azure 訂用帳戶或資源群組，根據 tooyour 公司的安全性需求與 hello 的應用程式的類型或大小寫的每個訂用帳戶中的 hello 資料的原則。 

![安全性原則](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> 深入了解每個 toolearn**防止原則**可用，請參閱[設定安全性原則](security-center-policies.md)發行項。
> 
> 

## <a name="manage-security-recommendations"></a>管理安全性建議
資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性弱點時，它會建立建議。 hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。

設定安全性原則之後, 的資訊安全中心會分析資源 tooidentify 的潛在弱點的 hello 安全性狀態。 hello 建議會出現以資料表格式，其中每一行代表一個特定的建議。 hello 下表提供的 Azure Vm 和什麼每一個將執行動作，您將它套用建議的一些範例。 當您選取建議時，您將提供示範如何 tooimplement hello 資訊安全中心的建議事項的資訊。

| 建議 | 說明 |
| --- | --- |
| [啟用訂用帳戶的資料收集](security-center-enable-data-collection.md) |建議您在您的訂用帳戶中開啟 hello 安全性原則中的每個訂用帳戶及所有虛擬機器 (Vm) 的資料收集。 |
| [修復 OS 弱點](security-center-remediate-os-vulnerabilities.md) |建議您設定規則的 hello 配合您作業系統的組態建議例如不允許儲存密碼 toobe。 |
| [套用系統更新](security-center-apply-system-updates.md) |建議您部署遺失系統的安全性和重大更新 tooVMs。 |
| [在系統更新之後重新開機](security-center-apply-system-updates.md#reboot-after-system-updates) |建議您重新啟動 VM toocomplete hello 程序套用系統更新。 |
| [安裝端點保護](security-center-install-endpoint-protection.md) |建議您佈建反惡意程式碼程式 tooVMs (僅限 Windows Vm)。 |
| [解決端點保護健全狀況警示](security-center-resolve-endpoint-protection-health-alerts.md) |建議您先解決端點保護失敗。 |
| [啟用 VM 代理程式](security-center-enable-vm-agent.md) |可讓您 toosee Vm 需要 hello VM 代理程式。 hello VM 代理程式必須安裝在 Vm 上，在掃描中，基準和反惡意程式碼程式掃描順序 tooprovision 修補程式。 預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。 hello 文章[VM 代理程式和延伸模組 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。 |
| [套用磁碟加密](security-center-apply-disk-encryption.md) |建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。 加密是建議使用 hello OS 和 VM 上的資料磁碟區。 |
| [未安裝弱點評估](security-center-vulnerability-assessment-recommendations.md) |建議在 VM 上安裝弱點評估解決方案。 |
| [修復弱點](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |可讓您 toosee 系統和應用程式的弱點可能會偵測到的 hello 的弱點可能會評估解決方案安裝在您的 VM 上。 |

> [!NOTE]
> toolearn 深入了解建議事項，請參閱[管理安全性建議](security-center-recommendations.md)發行項。
> 
> 

## <a name="monitor-security-health"></a>監視安全性健康狀態
啟用後[安全性原則](security-center-policies.md)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。  您可以檢視您的資源，以及任何問題，在 hello hello 安全性狀態**資源安全性健全狀況**刀鋒視窗。 當您按一下**虛擬機器**在 hello**資源安全性**健全狀況圖格、 hello**虛擬機器**刀鋒視窗會開啟您的 Vm 的建議。 

![安全性健康狀態](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>管理及回應 toosecurity 警示
資訊安全中心會自動收集、 分析，並整合您的 Azure 資源、 hello 網路和連線的交易夥伴方案 （例如防火牆和 endpoint protection 解決方案），從記錄檔資料 toodetect 威脅，並減少誤判。 利用不同的彙總的[偵測功能](security-center-detection-capabilities.md)，資訊安全中心是無法設定優先權的 toogenerate 快速調查 hello 問題並提供建議的方式，安全性警示 toohelp tooremediate可能的攻擊。

![安全性警示](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

選取 安全性警示 toolearn hello 事件觸發 hello 警示，以及項目，如果有的話會引導您有關需要 tootake tooremediate 攻擊。 安全性警示會依[類型](security-center-alerts-type.md)及日期區分。

## <a name="see-also"></a>另請參閱
toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。

