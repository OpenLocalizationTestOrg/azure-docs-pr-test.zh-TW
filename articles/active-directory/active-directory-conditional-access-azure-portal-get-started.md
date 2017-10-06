---
title: "開始使用 Azure Active Directory 中的條件式存取的 aaaGet |Microsoft 文件"
description: "使用位置條件測試條件式存取。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a>開始使用 Azure Active Directory 中的條件式存取

條件式存取是 Azure Active directory，可讓您 toodefine 條件下獲得授權的使用者可以存取您的應用程式的功能。 

本主題根據您環境中的位置條件，為您提供測試條件式存取的指示。  


## <a name="scenario-description"></a>案例描述

在許多組織中的一項常見需求是 tooonly 不會執行從 hello 公司內部網路的存取 tooapps 需要多重要素驗證。 使用 Azure Active Directory 設定以位置為基礎的條件式存取原則，即可輕鬆地完成此目標。 本主題提供設定相關原則的詳細指示。 hello 原則利用[信任的 Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish 源自 hello 公司的存取嘗試之間的內部網路和所有其他位置。


## <a name="prerequisites"></a>必要條件

hello 本主題中所述的案例假設您已熟悉中所述的 hello 概念[Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)。

tootest 此案例中，您需要：

- 建立測試使用者 

- 指派給 Azure AD Premium 授權 toohello 測試使用者

- 設定受管理的應用程式及指派您的測試使用者 tooit

- 設定信任的 IP

如果您需要更多有關信任 IP 的詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。


## <a name="policy-configuration-steps"></a>原則設定步驟

**tooconfigure 您條件式存取原則，執行：**

1. 在 [hello hello 左導覽列上的 Azure 入口網站中按一下**Azure Active Directory**。 

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. 在 [hello **Azure Active Directory**刀鋒視窗中的，在 hello**管理**區段中，按一下**條件式存取**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. 在 [hello**條件式存取**刀鋒視窗，tooopen hello**新增**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**新增**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. 在 [hello**新增**刀鋒視窗中的，在 hello**名稱**文字方塊中，輸入原則的名稱。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. 在 [hello**指派**區段中，按一下**使用者和群組**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. 在 [hello**使用者和群組**刀鋒視窗中，執行下列步驟的 hello:

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    a. 按一下 [選取使用者和群組]。

    b.這是另一個 C# 主控台應用程式。 按一下 [選取] 。

    c. 在 [hello**選取**刀鋒視窗中，選取您的測試使用者，然後按一下**選取**。

    d. 在 [hello**使用者和群組**刀鋒視窗中，按一下 [**完成**。

7. 在 [hello**新增**刀鋒視窗，tooopen hello**雲端應用程式**刀鋒視窗中的，在 hello**指派**區段中，按一下**雲端應用程式**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. 在 [hello**雲端應用程式**刀鋒視窗中，執行下列步驟的 hello:

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    a. 按一下 [選取應用程式]。

    b.這是另一個 C# 主控台應用程式。 按一下 [選取] 。

    c. 在 [hello**選取**刀鋒視窗中，選取您的雲端應用程式，然後按一下**選取**。

    d. 在 [hello**雲端應用程式**刀鋒視窗中，按一下 [**完成**。

9. 在 [hello**新增**刀鋒視窗，tooopen hello**條件**刀鋒視窗中的，在 hello**指派**區段中，按一下**條件**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. 在 [hello**條件**刀鋒視窗，tooopen hello**位置**刀鋒視窗中，按一下 [**位置**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. 在 [hello**位置**刀鋒視窗中，執行下列步驟的 hello:

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    a. 在 [設定] 之下，按一下 [是]。

    b.這是另一個 C# 主控台應用程式。 在 [包含] 之下，按一下 [所有位置]。

    c. 按一下 [排除]，然後按一下 [所有信任的 IP]。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    d. 按一下 [完成] 。

12. 在 [hello**條件**刀鋒視窗中，按一下 [**完成**。

13. 在 [hello**新增**刀鋒視窗，tooopen hello**授與**刀鋒視窗中的，在 hello**控制項**區段中，按一下**授與**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. 在 [hello **Grant**刀鋒視窗中，執行下列步驟的 hello:

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    a. 選取 [需要 Multi-Factor Authentication]。

    b.這是另一個 C# 主控台應用程式。 按一下 [選取] 。

15. 在 [hello**新增**刀鋒視窗下**啟用原則**，按一下**上**。

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. 在 [hello**新增**刀鋒視窗中，按一下 [**建立**。


## <a name="testing-hello-policy"></a>測試 hello 原則

tootest 您的原則，您應該從裝置存取您的應用程式的： 

1. 具有在您設定的信任 IP 內的 IP 位址 

1. 具有不在您設定的信任 IP 內的 IP 位址

只有從不在您設定的信任 IP 內的裝置嘗試連線時，才需要 Multi-Factor Authentication。 


## <a name="next-steps"></a>後續步驟

如果您想要 toolearn 深入了解條件式存取，請參閱[Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)。

