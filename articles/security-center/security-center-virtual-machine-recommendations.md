---
title: "aaaProtecting 您 Azure 資訊安全中心中的虛擬機器 |Microsoft 文件"
description: "本文件說明可協助您保護虛擬機器及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>保護 Azure 資訊安全中心內的虛擬機器
Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。  適用於建議 tooAzure 資源類型： SQL，以及應用程式網路的虛擬機器 (Vm)。

本文適用 tooVMs 的建議。  VM 建議圍繞在資料收集、套用系統更新、佈建反惡意程式碼、加密 VM 磁碟等等。  使用 hello 表當做參考 toohelp 您了解 hello 可用 VM 建議，以及每個如果您將它套用將執行的動作。

## <a name="available-vm-recommendations"></a>可用的 VM 建議
| 建議 | 說明 |
| --- | --- |
| [啟用訂用帳戶的資料收集](security-center-enable-data-collection.md) |建議您在您的訂用帳戶中開啟 hello 安全性原則中的每個訂用帳戶及所有虛擬機器 (Vm) 的資料收集。 |
| [為 Azure 儲存體帳戶啟用加密](security-center-enable-encryption-for-storage-account.md) | 建議您為待用資料啟用「Azure 儲存體服務加密」。 儲存體服務加密 (SSE) 中的運作方式會寫入 tooAzure 儲存和擷取之前解密時，加密 hello 資料。 SSE 目前僅適用於 hello Azure Blob 服務可用於區塊 blob，分頁 blob，並附加 blob。 詳細資訊，請參閱 toolearn[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。</br>只有在 Resource Manager 儲存體帳戶上才支援 SSE。 目前不支援傳統儲存體帳戶。 傳統的 toounderstand hello 和資源管理員部署模型，請參閱[Azure 部署模型](../azure-classic-rm.md)。 |
| [修復 OS 弱點](security-center-remediate-os-vulnerabilities.md) |建議您設定規則的 hello 配合您作業系統的組態建議例如不允許儲存密碼 toobe。 |
| [套用系統更新](security-center-apply-system-updates.md) |建議您部署遺失系統的安全性和重大更新 tooVMs。 |
| [套用 Just-in-Time 網路存取控制](security-center-just-in-time.md) | 建議您套用 Just-in-Time 虛擬機器存取。 在時間 」 功能中的 hello 已預覽並可使用 hello 標準層的資訊安全中心。 請參閱[定價](security-center-pricing.md)toolearn 詳細的資訊安全中心的定價層。 |
| [在系統更新之後重新開機](security-center-apply-system-updates.md#reboot-after-system-updates) |建議您重新啟動 VM toocomplete hello 程序套用系統更新。 |
| [安裝端點保護](security-center-install-endpoint-protection.md) |建議您佈建反惡意程式碼程式 tooVMs (僅限 Windows Vm)。 |
| [解決端點保護健全狀況警示](security-center-resolve-endpoint-protection-health-alerts.md) |建議您先解決端點保護失敗。 |
| [啟用 VM 代理程式](security-center-enable-vm-agent.md) |可讓您 toosee Vm 需要 hello VM 代理程式。 hello VM 代理程式必須安裝在 Vm 上，在掃描中，基準和反惡意程式碼程式掃描順序 tooprovision 修補程式。 預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。 hello 文章[VM 代理程式和延伸模組 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。 |
| [套用磁碟加密](security-center-apply-disk-encryption.md) |建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。 加密是建議使用 hello OS 和 VM 上的資料磁碟區。 |
| [更新作業系統版本](security-center-update-os-version.md) |建議您雲端服務 toohello 最新版本可用更新 hello 作業系統 (OS) 版本，您的作業系統系列。  toolearn 有關雲端服務的詳細資訊，請參閱 「 hello[雲端服務概觀](../cloud-services/cloud-services-choose-me.md)。 |
| [未安裝弱點評估](security-center-vulnerability-assessment-recommendations.md) |建議在 VM 上安裝弱點評估解決方案。 |
| [修復弱點](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |可讓您 toosee 系統和應用程式的弱點可能會偵測到的 hello 的弱點可能會評估解決方案安裝在您的 VM 上。 |

## <a name="see-also"></a>另請參閱
toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：

* [保護 Azure 資訊安全中心內的應用程式](security-center-application-recommendations.md)
* [保護 Azure 資訊安全中心內的網路](security-center-network-recommendations.md)
* [保護 Azure 資訊安全中心內的 Azure SQL 服務](security-center-sql-service-recommendations.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
