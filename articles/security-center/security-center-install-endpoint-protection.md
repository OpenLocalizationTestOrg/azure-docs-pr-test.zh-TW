---
title: "aaaInstall Azure 資訊安全中心中的 Endpoint Protection |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 安裝 Endpoint Protection * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>在 Azure 資訊安全中心安裝端點保護
如果尚未啟用 Endpoint Protection，則 Azure 資訊安全中心建議您在 Azure 虛擬機器 (VM) 上安裝 Endpoint Protection。 這項建議適用於僅 tooWindows Vm。

> [!NOTE]
> 此範例部署會使用 Microsoft Antimalware。 請參閱 [Azure 資訊安全中心中的夥伴整合](security-center-partner-integration.md#partners-that-integrate-with-security-center)以取得與資訊安全中心整合的夥伴清單。  
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  本文件不是一份逐步解說指南。
>
>

1. 在 hello**建議**刀鋒視窗中，選取**安裝 Endpoint Protection**。
   ![選取安裝端點保護][1]
2. hello**安裝 Endpoint Protection**刀鋒視窗隨即開啟並顯示沒有端點保護的 Vm 清單。 選取從 hello 清單 hello Vm 上想 tooinstall endpoint protection，並按一下**Vm 上安裝**。
   ![在 選取 Vm tooinstall Endpoint Protection][2]
3. hello**選取 Endpoint Protection**刀鋒視窗會開啟 tooallow 您 tooselect hello 端點保護解決方案想 toouse。 在此範例中，讓我們選取 [Microsoft Antimalware] 。
   ![][3]
4. 會顯示 hello 端點保護解決方案的其他資訊。 選取 [ **建立**]。
   ![建立反惡意程式碼解決方案][4]
5. Hello 上輸入 hello 所需的組態設定**加入擴充**刀鋒視窗中，然後再選取**確定**。 toolearn 深入了解 hello 組態設定，請參閱[預設和自訂反惡意程式碼設定](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)。

[Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)現在 hello 上的作用中選取 Vm。

## <a name="see-also"></a>另請參閱
本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 < 安裝 Endpoint Protection >。 toolearn 進一步了解啟用 Microsoft 反惡意程式碼在 Azure 中，請參閱下列文件的 hello:

* [雲端服務和虛擬機器的 Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)-了解如何 toodeploy Microsoft 反惡意程式碼。

toolearn 有關資訊安全中心的詳細資訊，請參閱下列文件的 hello:

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
