---
title: "Azure 金鑰保存庫使用 Azure 自動化 aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage Azure 金鑰保存庫。"
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>使用 Azure 自動化管理 Azure 金鑰保存庫
本指南將介紹 toohello Azure 自動化服務，而且可以如何使用的 toosimplify 管理您的金鑰和 Azure 金鑰保存庫中的密碼。

## <a name="what-is-azure-automation"></a>什麼是 Azure 自動化？
[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化和所要的狀態組態簡化雲端管理。 使用 Azure 自動化，自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織可能會手動、 重複、 長時間執行，而且容易產生錯誤的工作。

Azure 自動化會提供您的需求調整 toomeet 的非常可靠、 高可用性的工作流程執行引擎。 在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。

降低操作費用並釋出 IT 和 DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Azure 自動化如何協助管理 Azure 金鑰保存庫？
金鑰保存庫可以使用來管理 Azure 自動化中 hello [AzureRM 金鑰保存庫 cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4)和[傳統 Azure 金鑰保存庫 cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)。 管理傳統金鑰保存庫可自動在 Azure 自動化中的 hello Azure 模組，您可以匯入 hello [AzureRM KeyVault 模組](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4)到 Azure 自動化中，以便您可以執行許多您金鑰保存庫的管理hello 服務內的工作。 您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。

Hello Azure 金鑰保存庫 cmdlet，您可以執行這些工作和其他項目： 

* 建立和設定金鑰保存庫
* 建立或匯入金鑰
* 建立或更新密碼
* 更新金鑰的屬性
* 取得金鑰或密碼
* 刪除金鑰或密碼

以下是使用 PowerShell toomanage 金鑰保存庫的一些範例：  

* [Azure 金鑰保存庫 - 逐步解說](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [設定 Azure 金鑰保存庫](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure 金鑰保存庫的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。

* 請參閱 hello Azure 自動化[入門教學課程](../automation/automation-first-runbook-graphical.md)。
* 請參閱 hello [Azure 金鑰保存庫的 PowerShell 指令碼](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)。

