---
title: "aaaManage Azure 自動化帳戶 |Microsoft 文件"
description: "本文說明如何 toomanage hello 您的自動化帳戶，例如憑證更新、 刪除和設定不正確的設定。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>管理 Azure 自動化帳戶
在某個時間點您的自動化帳戶到期前，您將需要 toorenew hello 憑證。 如果您認為該 hello 執行身分帳戶已遭洩漏，您可以刪除並重新建立它。 本章節將討論如何 tooperform 這些作業。

## <a name="self-signed-certificate-renewal"></a>自我簽署憑證更新
hello hello 執行身分帳戶建立的自我簽署的憑證到期從建立 hello 日期起一年。 您可以在該憑證到期前隨時更新憑證。 當您更新它時，hello 目前有效的憑證會保留的 tooensure 任何 runbook 的執行中或正在執行，會進入佇列，並可向 hello 執行身分帳戶，不會產生負面影響。 hello 憑證到期日前就持續有效。

> [!NOTE]
> 如果您已設定您自動化執行身分帳戶 toouse 您企業憑證授權單位所核發的憑證，且您使用此選項，將會自我簽署憑證所取代 hello 企業憑證。

toorenew hello 憑證，請勿遵循 hello:

1. 在 hello Azure 入口網站，開啟 hello 自動化帳戶。

2. 在 hello**自動化帳戶**刀鋒視窗中的，在 hello**帳戶屬性**窗格下**帳戶設定**，選取**執行身分帳戶**。

    ![自動化帳戶的屬性窗格](media/automation-manage-account/automation-account-properties-pane.png)
3. 在 hello**執行身分帳戶**屬性刀鋒視窗中，選取任一 hello 執行身分帳戶或 hello 傳統執行身分帳戶，您想要 toorenew hello 憑證。

4. 在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**更新憑證**。

    ![更新執行身分帳戶的憑證](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. 當更新 hello 憑證後時，您可以追蹤下的 hello 進度**通知**hello 功能表。

## <a name="delete-a-run-as-or-classic-run-as-account"></a>刪除執行身分或傳統執行身分帳戶
本章節描述如何 toodelete 並重新建立執行身分或傳統執行身分帳戶。 當您執行此動作時，會保留 hello 自動化帳戶。 刪除執行身分或傳統執行身分帳戶後，您可以在 hello Azure 入口網站中重新建立它。

1. 在 hello Azure 入口網站，開啟 hello 自動化帳戶。

2. 在 [hello**自動化帳戶**刀鋒視窗中的，hello 帳戶屬性] 窗格中，選取**執行身分帳戶**。

3. 在 hello**執行身分帳戶**想 toodelete 屬性刀鋒視窗中，選取任一 hello 執行身分帳戶 」 或 「 傳統執行身分帳戶。 然後，在 hello**屬性**hello 刀鋒視窗中選取帳戶，請按一下**刪除**。

 ![刪除執行身分帳戶](media/automation-manage-account/automation-account-delete-runas.png)

4. 正在刪除 hello 帳戶，而您可以追蹤下的 hello 進度**通知**hello 功能表。

5. Hello 帳戶已被刪除後，您可以重新建立它在 hello**執行身分帳戶**屬性刀鋒視窗中的選取 hello 建立選項**Azure 執行身分帳戶**。

 ![重新建立 hello 自動化執行身分帳戶](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>設定錯誤
某些組態項目所需的 hello 執行身分或傳統執行身分帳戶 toofunction 正確可能已刪除或在初始安裝期間，建立方式不正確。 hello 項目包括：

* 憑證資產
* 連線資產
* 已從 hello 參與者角色移除執行身分帳戶
* Azure AD 中的服務主體或應用程式

在上述的 hello 和設定錯誤的其他執行個體，hello 自動化帳戶會偵測 hello 變更，並顯示狀態為*完整*上 hello**執行身分帳戶**hello 的屬性刀鋒視窗帳戶。

![不完整的執行身分帳戶設定狀態](media/automation-manage-account/automation-account-runas-incomplete-config.png)

當您選取執行身分帳戶 hello 時，hello 帳戶**屬性** 窗格會顯示下列錯誤訊息的 hello:

![不完整的執行身分設定警告訊息](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

您可以快速解決這些執行身分帳戶的問題，藉由刪除並重新建立 hello 帳戶。

## <a name="next-steps"></a>後續步驟
* 如需有關服務主體的詳細資訊，請參閱太[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)。
* 如需有關在 Azure 自動化中的 角色型存取控制的詳細資訊，請參閱太[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。
* 如需有關憑證和 Azure 服務的詳細資訊，請參閱太[Azure 雲端服務憑證概觀](../cloud-services/cloud-services-certs-create.md)。
