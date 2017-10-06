---
title: "aaaCharacteristics 的 Azure Active Directory 租用戶 intercaction |Microsoft 文件"
description: "了解您的目錄為完全獨立的資源，以管理 Azure Active Directory 租用戶"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>了解多個 Azure Active Directory 租用戶如何互動

在 Azure Active Directory (Azure AD) 中，每個租用戶已完全獨立的資源： 邏輯上獨立於對等體 hello 您管理其他租用戶。 租用戶之間沒有任何父子關聯性。 這個在租用戶之間的獨立性包括資源獨立性、系統管理獨立性，以及同步處理獨立性。

## <a name="resource-independence"></a>資源獨立性
* 如果您建立或刪除一個租用戶中的資源時，它沒有任何影響另一個租用戶中，具有 hello 外部使用者的部分例外狀況的任何資源。 
* 如果將您的其中一個網域名稱與某個租用戶搭配使用，該網域名稱就無法與任何其他租用戶搭配使用。

## <a name="administrative-independence"></a>系統管理獨立性
如果 'Contoso' 租用戶的非系統管理使用者建立 'Test' 測試租用戶，則：

* 根據預設，建立租用戶的 hello 使用者會成為該新的租用戶和指派的 hello 該租用戶全域管理員角色的外部使用者。
* 租用戶 'Contoso' hello 系統管理員有沒有直接的系統管理權限 tootenant 'Test'，除非 'Test' 的系統管理員特別授與這些權限。 不過，'Contoso' 的系統管理員可以控制存取 tootenant 'Test' 如果它們控制 hello 使用者帳戶建立 'Test'。
* 如果您新增/移除一個租用戶中的使用者的系統管理員角色，hello 變更不會不會影響 hello 系統管理員角色的 hello 使用者具有另一個租用戶中。

## <a name="synchronization-independence"></a>同步處理獨立性
您可以設定每個 Azure AD 租用獨立 tooget 資料從單一執行個體中的其中一個同步處理：

* 單一 AD 樹系 toosynchronize 資料 hello Azure AD Connect 工具。
* hello Azure 作用中租用戶連接器 Forefront Identity Manager，toosynchronize 資料，其中包含一個或多個內部部署樹系和/或非 Azure AD 資料來源。

## <a name="add-an-azure-ad-tenant"></a>新增 Azure AD 租用戶
tooadd hello Azure 入口網站中的 Azure AD 租用戶登入太[hello Azure 入口網站](https://portal.azure.com)與 Azure AD 全域管理員帳戶，然後在 hello 左邊，選取**新增**。

> [!NOTE]
> 與其他 Azure 資源不同，您的租用戶並非 Azure 訂用帳戶的子資源。 如果您的 Azure 訂用帳戶取消或已過期，您仍然可以存取您使用 Azure PowerShell、 Azure Graph API，hello 或 hello Office 365 系統管理中心的租用戶資料。 您也可以將其他訂用帳戶與 hello 租用戶產生關聯。
>

## <a name="next-steps"></a>後續步驟
如需 Azure AD 授權問題和最佳做法的廣泛概觀，請參閱[什麼是 Azure Active Directory 租用戶授權？](active-directory-licensing-whatis-azure-portal.md)
