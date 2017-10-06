---
title: "aaaAzure 資料目錄必要條件 |Microsoft 文件"
description: "深入了解您需要開始使用 Azure 資料目錄 tooget hello 必要條件。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Azure 資料目錄必要條件

您可以設定 Azure 資料目錄之前，您需要 tootake care of 幾件事。 別擔心，這個過程不需要很長時間。

## <a name="azure-subscription"></a>Azure 訂閱
tooset 安裝資料目錄，您必須是 hello 擁有者或共同擁有者的 Azure 訂用帳戶。

Azure 訂用帳戶可協助您組織存取 toocloud 服務資源，例如資料目錄。 訂用帳戶也可協助您控制如何根據資源使用量產生報告、計費及付費。 每一個訂用帳戶可以有個別的計費和付款設定；因此，依照部門、專案及分處等，您可以有不同的訂用帳戶和不同的計劃。 每個雲端服務所屬 tooa 訂用帳戶，並設定資料目錄之前，需要 toohave 訂用帳戶。 詳細資訊，請參閱 toolearn[管理帳戶、 訂用帳戶及管理角色](../active-directory/active-directory-assign-admin-roles.md)。

## <a name="azure-active-directory"></a>Azure Active Directory
tooset 安裝資料目錄，您必須登入 Azure Active Directory (Azure AD) 使用者帳戶。

Azure AD 會提供簡單的方法，以您的商務 toomanage 識別和存取，在 hello 雲端和內部部署。 使用者可以使用單一工作或學校帳戶進行單一登入 tooany 雲端，然後在內部部署 web 應用程式。 資料目錄會使用 Azure AD tooauthenticate 登入。 詳細資訊，請參閱 toolearn[什麼是 Azure Active Directory？](../active-directory/active-directory-whatis.md)。

> [!NOTE]
> 使用 hello [Azure 入口網站](http://portal.azure.com/)，您可以登入個人 Microsoft 帳戶或 Azure Active Directory 公司或學校帳戶。 使用資料目錄註冊 tooset 或是 hello Azure 入口網站或 hello[資料目錄入口網站](http://www.azuredatacatalog.com)，您必須使用 Azure Active Directory 帳戶，而不是個人的帳戶登入。
>
>

## <a name="active-directory-policy-configuration"></a>Active Directory 原則組態
您可能會遇到的情況，您可以登入 toohello 資料目錄入口網站，而，但是當您嘗試 toosign toohello 資料來源註冊工具中的，您會遇到的錯誤訊息，讓您無法登入。 只有當您在 hello 公司網路，或可能只有當您要連線從外部 hello 公司網路時，可能會發生此問題的行為。

hello 資料來源註冊工具會使用表單驗證 toovalidate 您對 Active Directory 的使用者認證。 toohelp 成功登入，Active Directory 系統管理員必須啟用表單驗證 hello 全域驗證原則中。

Hello 全域驗證原則，在驗證方法可以啟用個別的內部網路和外部網路連接，hello 下列螢幕擷取畫面所示。 如果要連線的 hello 網路不啟用表單驗證，可能會發生登入錯誤。

 ![Active Directory 全域驗證原則](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。
