---
title: "設定使用 Amazon Web Services 進行驗證 | Microsoft Docs"
description: "本文說明如何在管理 AWS 資源的 Azure 自動化中建立和驗證 Runbook 的 AWS 認證。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "aws 驗證, 設定 aws"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: fe590e7fc551c175d2f41f5b98e1558a756df806
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>使用 Amazon Web Services 驗證 Runbook
使用 Amazon Web Services (AWS) 中的資源自動執行常見工作可透過 Azure 中的自動化 Runbook 來完成。  您可以和使用 Azure 中的資源一樣，在 AWS 中使用自動化 Runbook 自動執行許多工作。  所需具備的只有兩項條件︰

* AWS 訂用帳戶和一組認證。  具體而言就是您的 AWS 存取金鑰和秘密金鑰。  如需詳細資訊，請檢閱 [使用 AWS 認證](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html)一文。
* Azure 訂用帳戶和自動化帳戶。  如需設定 Azure 自動化帳戶的詳細資訊，請檢閱 [設定 Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)一文。  

若要使用 AWS 進行驗證，您必須指定一組 AWS 認證來驗證您從 Azure 自動化中執行的 Runbook。 如果您已建立自動化帳戶，而且想要以該帳戶來使用 AWS 進行驗證，您可以依照下一節中的步驟來進行。  如果您想要針對以 AWS 資源為目標的 Runbook 建立專用帳戶，您應該先建立新的[自動化執行身分帳戶](automation-sec-configure-azure-runas-account.md) (略過建立服務主體的選項)，然後依照下列步驟來進行。

## <a name="configure-automation-account"></a>設定自動化帳戶
若要讓 Azure 自動化與 AWS 通訊，您必須先擷取 AWS 認證，並將它們儲存為 Azure 自動化中的資產。  執行 AWS 文件[管理 AWS 帳戶的存取金鑰](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)中記載的下列步驟，以建立存取金鑰並複製**存取金鑰識別碼**和**密碼存取金鑰** (亦可選擇下載金鑰檔以將其儲存在某處安全的地方)。

建立並複製 AWS 安全性金鑰後，您必須使用 Azure 自動化帳戶建立認證資產以安全地儲存金鑰，並讓金鑰與 Runbook 參照。  按照 [Azure 自動化中的認證資產](automation-credentials.md)一文中**建立新認證**一節的步驟來進行，並輸入下列資訊︰

1. 在 [名稱] 方塊中，輸入 **AWScred** 或遵循您的命名標準的適當值。  
2. 在 [使用者名稱] 方塊中輸入您的**存取識別碼**，並在 [密碼] 和 [確認密碼] 方塊中輸入您的**密碼存取金鑰**。   

## <a name="next-steps"></a>後續步驟
* 檢閱[在 Amazon Web Services 中自動部署 VM](automation-scenario-aws-deployment.md) 解決方案文章，了解如何建立 Runbook 以在 AWS 中自動執行工作。

