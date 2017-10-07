---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）
本文將說明如何 tooenable Azure Active Directory 網域服務 (Azure AD DS) 使用 hello Azure 入口網站。


toolaunch hello**啟用 Azure AD 網域服務** 精靈，完成下列步驟的 hello:

1. 移 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 [hello] 左窗格中，按一下**新增**。
3. 在 hello**新增**刀鋒視窗中，輸入**網域服務**hello 搜尋列。

    ![搜尋網域服務](./media/getting-started/search-domain-services.png)

4. 按一下 tooselect **Azure AD 網域服務**hello 清單中的搜尋建議。 在 [hello **Azure AD 網域服務**刀鋒視窗中，按一下 hello**建立**] 按鈕。

    ![網域服務刀鋒視窗](./media/getting-started/domain-services-blade.png)

5. hello**啟用 Azure AD 網域服務**精靈啟動。


## <a name="task-1-configure-basic-settings"></a>工作 1：設定基本設定
在 hello**基本概念**頁面的 hello 精靈，您可以指定 hello hello 受管理的網域的 DNS 網域名稱。 您也可以選擇 hello 資源群組和 Azure 位置 toowhich hello 受管理的網域，應該先部署。

![設定基本](./media/getting-started/domain-services-blade-basics.png)

1. 選擇 hello **DNS 網域名稱**的受管理的網域。

   * hello 目錄 hello 預設網域名稱 (與**。 onmicrosoft.com**後置詞) 的預設指定。

   * 您也可以輸入自訂網域名稱。 在此範例中，hello 自訂網域名稱是*contoso100.com*。

     > [!WARNING]
     > hello 前置詞指定的網域名稱 (例如， *contoso100*在 hello *contoso100.com*網域名稱) 必須包含 15 個字元。 您無法使用超過 15 個字元的前置詞來建立受管理的網域。
     >
     >

2. 請確定您已選擇 hello 受管理的網域不存在 hello 虛擬網路中的 hello DNS 網域名稱。 具體來說，請檢查是否有下列情況︰

   * 您已經擁有網域以 hello 相同 hello 虛擬網路上的 DNS 網域名稱。

   * hello 您計劃 tooenable hello 受管理的網域的虛擬網路已與您在內部部署網路的 VPN 連線。 在此案例中，請確定您不需要以 hello 網域相同的 DNS 網域名稱，在內部部署網路上。

   * Hello 虛擬網路上有該名稱與現有的雲端服務。

3. 選擇 hello**的虛擬網路類型**。 根據預設，hello**資源管理員**所選取的虛擬網路類型。 建議所有新建立的受管理網域使用這種類型的虛擬網路。

4. 選取 hello Azure**訂用帳戶**中您想要 toocreate hello 受管理的網域。

5. 選取 hello**資源群組**應該屬於 toowhich hello 受管理的網域。 您可以選擇其中一個 hello**建立新**或**使用現有**選項 tooselect hello 資源群組。

6. 選擇 hello Azure**位置**應在哪個 hello 建立受管理的網域。 在 hello**網路**頁面的 hello 精靈，請參閱唯一的虛擬網路屬於 toohello 您選取的位置。

7. 當您完成之後時，按一下 **確定**上 toohello toomove**網路**hello 精靈頁面。


## <a name="next-step"></a>後續步驟
[工作 2：設定網路基本設定](active-directory-ds-getting-started-network.md)
