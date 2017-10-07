---
title: "Azure Active Directory B2C：針對建立租用戶進行疑難排解 | Microsoft Docs"
description: "關於建立 Azure Active Directory 或 Azure Active Directory B2C 租用戶的問題與解決方法。"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>針對建立 Azure Active Directory 或 Azure Active Directory B2C 租用戶進行疑難排解 

## <a name="create-an-azure-ad-tenant"></a>建立 Azure AD 租用戶
如果您無法在 hello 第一次嘗試建立 Azure Active Directory (Azure AD) 租用戶，再試一次。 如果 hello 問題持續發生，請連絡 Azure 支援。

## <a name="create-an-azure-ad-b2c-tenant"></a>建立 Azure AD B2C 租用戶
如果您遇到問題時您[建立 Azure Active Directory B2C (Azure AD B2C) 租用戶](active-directory-b2c-get-started.md)，再試一次 hello 下列選項：

* 如果您的租用戶的清單中，不會顯示 hello Azure AD B2C 租用戶，再試一次 toocreate hello 租用戶。
* 如果 hello Azure AD B2C 租用戶確實會顯示在您的租用戶的清單中，您會看到下列錯誤訊息的 hello 刪除 hello 租用戶，並重新建立它：

    "無法完成建立 hello B2C 租用戶 'contosob2c' hello。 如需詳細指引，請造訪此[連結](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409)。」
* 那里已知問題，當您刪除現有的 Azure AD B2C 租用戶，並使用 hello 重新建立相同的網域名稱。 當您建立新的 Azure AD B2C 租用戶時，您必須使用不同的網域名稱。
* 若這些解決方法無效，請連絡 Azure 支援中心。 如需詳細資訊，請參閱[提出 Azure AD B2C 的支援要求](active-directory-b2c-support.md)。

