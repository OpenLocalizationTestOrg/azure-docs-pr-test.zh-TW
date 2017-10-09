---
title: "在 Azure 資訊安全中心 aaaResolve endpoint protection 健全狀況警示 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 解決 Endpoint Protection 健全狀況警示 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>解決 Azure 資訊安全中心的端點保護健全狀況警示
Azure 資訊安全中心建議您先解決偵測到的端點保護健全狀況警示。  資訊安全中心可讓您的虛擬機器 (Vm) 具有 endpoint protection 失敗及多少失敗 toosee。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 這不是逐步指南。
> 
> 

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議刀鋒視窗**，選取**解決 Endpoint Protection 健全狀況警示**。
   ![解決端點保護健全狀況警示][1]
2. 這會開啟刀鋒視窗中 hello **Endpoint Protection 失敗**其中會列出 Vm 失敗與 hello 失敗次數為每個 VM。 Hello 清單中選取 VM。
   ![Endpoint protection failure][2]
3. A**失敗清單**hello 選取 VM，顯示一份失敗，就會開啟刀鋒視窗。 選取從 hello 清單 toolearn 詳細的失敗。 這會在刀鋒視窗開啟 hello 選取失敗的相關資訊。
   ![Failures list][3]
    ![失敗事件][4]

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
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
