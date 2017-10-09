---
title: "在 Azure 資訊安全中心 aaaManaging 協力廠商解決方案 |Microsoft 文件"
description: "這份文件會引導您如何 Azure 資訊安全中心可讓您監視在您與您 Azure 訂用帳戶整合的協力廠商解決方案概覽 hello 健全狀況狀態。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>使用 Azure 資訊安全中心監視合作夥伴解決方案
這份文件會引導您如何 toomonitor hello Azure 資訊安全中心夥伴方案的健全狀況狀態。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 本文件不是一份逐步解說指南。
>
>

## <a name="monitoring-partner-solutions"></a>監視合作夥伴解決方案
hello**合作夥伴解決方案**磚 hello**資訊安全中心**刀鋒視窗可讓您監視在您與您 Azure 訂用帳戶整合的協力廠商解決方案概覽 hello 健全狀況狀態。

![合作夥伴解決方案圖格][1]

hello**合作夥伴解決方案**磚會顯示 hello 數目與您的訂閱整合的協力廠商解決方案。 如果沒有任何解決方案整合，hello 磚會顯示 hello 數字的零。

協力廠商解決方案的 tooview hello 健康狀態：

1. 選取 hello**合作夥伴解決方案**磚。 hello**合作夥伴解決方案**刀鋒視窗隨即開啟，顯示一份協力廠商解決方案連接 tooSecurity 中心。

   ![合作夥伴解決方案][3]

   協力廠商解決方案的 hello 狀態可以是：

   * 受保護 (綠色) - 沒有任何健康問題。
   * 狀況不良 (紅色) - 有需要立即注意的健康狀態問題。
   * 停止報告 （橘色）-hello 方案已停止報告其健全狀況。
   * 未知的保護狀態 （橘色）-hello 方案 hello 健全狀況是未知的到期 tooa 失敗的加入新的資源 toohello 現有方案的程序這一次。
   * 不會報告 （灰色）-hello 方案沒有回報任何項目，但如果最近已連線，而且仍將部署方案的狀態可能會回報。

2. 選取合作夥伴解決方案。 在此範例中，可讓選取的 hello **Qualys**方案。  刀鋒視窗會開啟顯示 hello 夥伴方案和 hello 方案 hello 狀態相關聯的資源。 選取**方案主控台**tooopen hello 夥伴管理體驗此解決方案。

   ![合作夥伴解決方案詳細資料][4]
3. 返回 toohello **Qualys**刀鋒視窗，然後選取**連結 VM**。 hello**連結應用程式**刀鋒視窗隨即開啟。 您可以在這裡連接資源 toohello 協力廠商解決方案。

   ![連結資源 toopartner 方案][5]

## <a name="next-steps"></a>後續步驟
在本文件中，您所導入了的 toohello**協力廠商解決方案**磚中的資訊安全中心。 toolearn 有關資訊安全中心的詳細資訊，請參閱下列文章 hello:

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)— 取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
