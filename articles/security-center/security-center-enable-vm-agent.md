---
title: "aaaEnable VM 代理程式在 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用 VM 代理程式 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>在 Azure 資訊安全中心啟用 VM 代理程式
hello VM 代理程式必須安裝在順序中的虛擬機器 (Vm) 太[啟用資料收集](security-center-enable-data-collection.md)。  Azure 資訊安全中心可讓您 toosee Vm 需要 hello VM 代理程式，以及將會建議您啟用 hello 在那些 Vm 上的 VM 代理程式。

預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。 hello 文章[VM 代理程式和延伸模組 – 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 這不是逐步指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議刀鋒視窗**，選取**啟用 VM 代理程式**。
   ![啟用 VM 代理程式][1]
2. 這會開啟刀鋒視窗中 hello **VM 代理程式遺失或不回應**。 此刀鋒視窗會列出 hello Vm 需要 hello VM 代理程式。 遵循 hello 指示 hello 刀鋒視窗 tooinstall hello VM 代理程式。
   ![VM 代理程式已遺失][2]

## <a name="see-also"></a>另請參閱
toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md)-- 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)-了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
