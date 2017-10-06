---
title: "在 Azure Active Directory 中的 aaaAdministrative 單位管理預覽"
description: "使用管理單位在 Azure Active Directory 中進行更細微的權限委派"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>在 Azure AD 中的管理單位管理 - 公用預覽版
本文說明系統管理單元，新的 Azure Active Directory 容器，可以使用委派系統管理權限的使用者子集及套用原則 tooa 使用者子集上的資源。 在 Azure Active Directory 中，系統管理單元可讓中央系統管理員 toodelegate 權限 tooregional 系統管理員或 tooset 細微的層級的原則。

這在具有獨立部門的組織，例如由許多彼此獨立的學院 (商學院和工學院等) 所組成的大型大學中非常有用。 這類部門擁有自己的 IT 管理員，可控制存取、管理使用者，以及針對其部門設定特別原則。 中央系統管理員想透過其特殊部門中的 hello 使用者 toobe 無法授與這些部門系統管理員權限。 更具體來說，使用此範例中，中央系統管理員可以比方說，建立為特定學院 （商學院） 管理單位並填入它僅 hello 商學院使用者等等。 然後，中央系統管理員可以將 hello 商學院 IT 人員 tooa 範圍的角色，亦即，授與 hello 的商務學校系統管理權限只能透過 hello 商務商學院系統管理單元的 IT 人員。

> [!IMPORTANT]
> 只有在啟用 Azure Active Directory Premium 時，才可以指派管理單位範圍的管理員角色。 如需詳細資訊，請參閱〈 [開始使用 Azure AD Premium](active-directory-get-started-premium.md)〉。
>


Hello 中央系統管理員的觀點來看，從管理單位是目錄物件，可以建立和填入資源。 **在此預覽版本中，這些資源僅能是使用者。** 一旦建立並填入，hello 系統管理單元可用來當做範圍 toorestrict hello 授與權限，只能透過 hello 系統管理單元中所包含的資源。

## <a name="managing-administrative-units"></a>管理管理單位
在此預覽版本，您可以建立和管理使用 hello Azure Active Directory 模組的 Windows PowerShell cmdlet 的系統管理單元。 深入了解如何 toolearn toodo，請參閱[使用系統管理單元](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

如需有關軟體需求和安裝 hello Azure AD 模組，以及有關 hello Azure AD 模組 cmdlet 來管理管理單位，包括語法、 參數說明和範例，請參閱[Azure ActiveDirectory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0)。

## <a name="next-steps"></a>後續步驟
[Azure Active Directory 版本](active-directory-editions.md)
