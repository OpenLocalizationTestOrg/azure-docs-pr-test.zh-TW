---
title: "在 Azure 自動化中的 aaaIntro tooauthentication |Microsoft 文件"
description: "本文章提供在 Azure 自動化中的自動化帳戶的自動化安全性和可用的 hello 不同的驗證方法的概觀。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "自動化安全性、安全的自動化、自動化驗證"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>在 Azure 自動化中的簡介 tooauthentication  
Azure 自動化可讓您針對資源 tooautomate 工作在 Azure 中，內部部署，並與其他雲端提供者例如 Amazon Web Services (AWS)。  為了讓 runbook tooperform 必要的動作，它必須具有權限 toosecurely 存取 hello 資源 hello hello 訂用帳戶內所需的最小權限。

本文將討論各種的驗證案例支援的 Azure 自動化的 hello，會顯示您如何啟動 tooget hello 環境或基礎環境您需要 toomanage。  

## <a name="automation-account-overview"></a>自動化帳戶概觀
當您啟動 Azure 自動化 hello 第一次時，您必須建立至少一個自動化帳戶。 自動化帳戶可讓您 tooisolate 自動化資源 （runbook、 資產、 組態） 與 hello 其他自動化帳戶中所含的資源。 您可以使用自動化帳戶 tooseparate 資源到個別的邏輯環境。 例如，您可能會針對開發、生產和內部部署環境各自使用一個帳戶。  Azure 自動化帳戶與 Microsoft 帳戶或您在 Azure 訂用帳戶中建立的帳戶不同。

每個自動化帳戶的 hello 自動化資源與單一 Azure 區域相關聯，但自動化帳戶可以管理您的訂用帳戶中的所有 hello 資源。 如果您有需要的資料和資源 toobe 隔離的 tooa 特定地區的原則是 hello 主要原因 toocreate 不同區域中的自動化帳戶。

> [!NOTE]
> 自動化帳戶和它們所包含的 hello 資源 hello Azure 入口網站中建立，無法在 hello Azure 傳統入口網站存取。 如果您想 toomanage，這些帳戶或其使用 Windows PowerShell 的資源，您必須使用 hello Azure 資源管理員模組。
>

所有您針對在 Azure 自動化中使用 Azure 資源管理員和 hello Azure 指令程式的資源執行 hello 工作必須驗證 tooAzure 使用 Azure Active Directory 組織身分識別認證基礎驗證。  憑證型驗證 hello 原始驗證方法使用 Azure 服務管理模式，但它是複雜的 toosetup。  驗證 Azure AD 使用者與 tooAzure 已導入的回復 2014 toonot 只簡化 hello 程序 tooconfigure 驗證帳戶，但也支援 hello 能力 toonon 互動方式驗證 tooAzure 運作的單一使用者帳戶Azure 資源管理員和傳統資源。   

目前當您建立新的自動化帳戶中 hello Azure 入口網站時，它會自動建立：

* 執行身分帳戶可在 Azure Active Directory，憑證中，建立新的服務主體，並指派 hello 參與者角色型存取控制 (RBAC)，將會使用 toomanage 資源管理員資源使用 runbook。
* 傳統的執行身分帳戶上傳管理憑證，將會使用的 toomanage Azure 服務管理或使用 runbook 的傳統資源。  

以角色為基礎的存取控制使用的允許動作 tooan Azure AD 使用者帳戶和執行身分帳戶的 Azure Resource Manager toogrant，驗證該服務主體。  請閱讀[Azure 自動化文件中的角色型存取控制](automation-role-based-access-control.md)以取得進一步資訊 toohelp 開發您的模型來管理自動化的權限。  

Hybrid Runbook Worker 在您的資料中心或對運算 AWS 中的服務上執行的 Runbook 無法使用 hello 相同方法，通常用於驗證 tooAzure 資源的 runbook。  這是因為這些資源 Azure 外部執行，因此將需要自己自動化 tooauthenticate tooresources 它們會在本機存取中定義的安全性認證。  

## <a name="authentication-methods"></a>驗證方法
hello 下表摘要說明 Azure 自動化和 hello 文章描述所支援的每個環境的 hello 不同的驗證方法如何 toosetup 驗證您的 runbook。

| 方法 | Environment | 文章 |
| --- | --- | --- |
| Azure AD 使用者帳戶 |Azure 資源管理員和 Azure 服務管理 |[使用 Azure AD 使用者帳戶驗證 Runbook](automation-create-aduser-account.md) |
| Azure 執行身分帳戶 |Azure Resource Manager |[使用 Azure 執行身分帳戶驗證 Runbook](automation-sec-configure-azure-runas-account.md) |
| Azure 傳統執行身分帳戶 |Azure 服務管理 |[使用 Azure 執行身分帳戶驗證 Runbook](automation-sec-configure-azure-runas-account.md) |
| Windows 驗證 |內部部署資料中心 |[驗證混合式 Runbook 背景工作角色的 Runbook](automation-hybrid-runbook-worker.md) |
| AWS 認證 |Amazon Web Services |[使用 Amazon Web Services (AWS) 驗證 Runbook](automation-config-aws-account.md) |
