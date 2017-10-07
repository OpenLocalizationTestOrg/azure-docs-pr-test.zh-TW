---
title: "aaaConfigure Azure Active Directory 裝置型條件式存取原則 |Microsoft 文件"
description: "了解如何 tooconfigure Azure Active Directory 裝置型條件式存取原則。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>設定 Azure Active Directory 裝置型條件式存取原則

透過 [Azure Active Directory (Azure AD) 條件式存取](active-directory-conditional-access-azure-portal.md)，您可以微調授權使用者如何存取您的應用程式。 例如，您可以限制 hello 存取 toocertain 資源 tootrusted 裝置。 需要受信任裝置的條件式存取原則，也稱為裝置型條件式存取原則。

本主題會提供您如何 tooconfigure 裝置型條件式存取原則的 Azure AD 連接的應用程式的相關資訊。 


## <a name="before-you-begin"></a>開始之前

裝置型條件式存取會將 **Azure AD 條件式存取**和 **Azure AD 裝置管理**繫結在一起。 如果您還不熟悉其中一種情況，您應該閱讀下列主題，第一次的 hello:

- **[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)** -本主題提供概觀條件式存取和 hello 相關的術語。

- **[Azure Active Directory 中的簡介 toodevice 管理](device-management-introduction.md)** -本主題概略說明 hello 的各種選項需要 tooconnect 裝置與 Azure AD。 


## <a name="trusted-devices"></a>受信任的裝置

在行動裝置-首先，雲端優先世界中，Azure Active Directory 可讓單一登入 toodevices、 應用程式和服務從任何地方。 某些 toohello 適當的使用者授與存取您的環境中的資源可能無法夠好。 此外 toohello 適當的使用者，您可能也需要信任的裝置 toobe 用 tooaccess 資源。 在您的環境，您可以定義受信任的裝置根據 hello 下列元件：

- hello[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)在裝置上
- 裝置是否符合規範
- 裝置是否已加入網域 

hello[裝置平台](active-directory-conditional-access-azure-portal.md#device-platforms)的特點在於 hello 您裝置執行作業系統。 在裝置型條件式存取原則中，您可以限制存取 toocertain 資源 toospecific 裝置平台。



在裝置型條件式存取原則中，您可能需要信任的裝置 toobe 標示為相容。

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/24.png)

裝置可以標示為相容的 hello 目錄中：

- Intune 
- 與 Azure AD 整合的第三方行動裝置管理系統  

只有連接的 tooAzure AD 的裝置可以標示為相容。 tooconnect 裝置 tooAzure Active Directory，您有下列選項的 hello: 

- 已註冊的 Azure AD
- 已聯結的 Azure AD
- 已聯結的混合式 Azure AD

    ![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/26.png)

如果您有內部部署 Active Directory (AD) 耗用量，您可以考慮不會連接的 tooAzure AD 而聯結的 tooyour AD toobe 受信任的裝置。

![雲端應用程式](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>後續步驟

在您的環境中設定裝置型條件式存取原則，您應該看看 hello [Azure Active Directory 中的條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。

