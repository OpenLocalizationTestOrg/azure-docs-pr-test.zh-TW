---
title: "aaaInstall 在內部部署資料閘道 |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定內部資料閘道。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>安裝及設定內部部署資料閘道
中的一個或多個 Azure Analysis Services 伺服器 hello 相同時，就需要在內部部署資料閘道區域連接 tooon 內部部署資料來源。 請參閱深入了解 hello 閘道 toolearn[在內部部署資料閘道](analysis-services-gateway.md)。

## <a name="prerequisites"></a>必要條件
**最低需求：**

* .NET 4.5 Framework
* 64 位元版本的 Windows 7 / Windows Server 2008 R2 (或更新版本)

**建議配備：**

* 8 核心 CPU
* 8 GB 記憶體
* 64 位元版本的 Windows 2012 R2 (或更新版本)

**重要考量︰**

* 在安裝期間，向您的閘道註冊 Azure 時，會選取 hello 預設訂用帳戶的區域。 您可以選擇不同的區域。 如果您有伺服器位於多個區域中，您必須針對每個區域安裝一個閘道。 
* hello 閘道不能安裝在網域控制站上。
* 一部電腦只能安裝一個閘道。
* 資料會保留在並不討論 toosleep 的電腦上安裝 hello 閘道。
* 請勿以無線方式連線的 tooyour 網路上安裝 hello 閘道。 效能會因此降低。


## <a name="download"></a>下載
 [下載 hello 閘道](https://aka.ms/azureasgateway)

## <a name="install"></a>安裝

1. 執行安裝程式。

2. 選取的位置，接受 hello 條款，然後按一下**安裝**。

   ![安裝位置和授權條款](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. 選取 [內部部署資料閘道 ()]。 Azure Analysis Services 不支援個人模式。

   ![選擇閘道的類型](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. 輸入帳戶 toosign tooAzure 中。 hello 帳戶必須是租用戶的 Azure Active Directory 中。 此帳戶用於 hello 閘道系統管理員。 

   ![輸入帳戶 toosign tooAzure 中](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > 如果您使用網域帳戶登入，就會在 Azure AD 中對應 tooyour 組織帳戶。 您的組織帳戶將用於 hello hello 閘道系統管理員。

## <a name="register"></a>註冊
在順序 toocreate 閘道資源在 Azure 中，您必須註冊您安裝閘道器雲端服務的 hello 與 hello 本機執行個體。 

1.  選取 [在這部電腦上註冊新的閘道]。

    ![註冊](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. 輸入您的閘道名稱和復原金鑰。 根據預設，hello 閘道會使用您的訂用帳戶預設區域。 如果您需要 tooselect 不同的區域，選取**變更區域**。

   ![註冊](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>建立 Azure 閘道資源
在您安裝並註冊您的閘道之後，您會需要您 Azure 訂用帳戶中 toocreate 閘道資源。 登入以 hello tooAzure 相同註冊 hello 閘道時所使用的帳戶。

1. 在 Azure 入口網站中，按一下 [建立新服務] > [企業整合] > [內部部署資料閘道] > [建立]。

   ![建立閘道資源](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. 在 [建立連線閘道] 中，輸入下列設定：

    * **名稱**：輸入閘道資源的名稱。 

    * **訂用帳戶**： 選取 hello Azure 訂用帳戶 tooassociate 與閘道資源。 
    此訂用帳戶應為 hello 您的伺服器位於相同的訂用帳戶。
   
      hello 預設訂用帳戶根據 hello 用 toosign 中的 Azure 帳戶。

    * **資源群組**：建立資源群組，或選取現有的資源群組。

    * **位置**： 您註冊您的閘道器中選取 hello 區域。

    * **安裝名稱**： 如果尚未選取閘道安裝，選取 hello 閘道註冊。 

    完成之後，請按一下 [建立] 。

## <a name="connect-servers"></a>連接伺服器 toohello 閘道資源

1. 在 Azure Analysis Services 伺服器概觀中，按一下 [內部部署資料閘道]。

   ![連接伺服器 toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. 在**挑選內部資料閘道 tooconnect**，選取您的閘道資源，然後按一下**選取的連線的閘道**。

   ![連接伺服器 toogateway 資源](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > 如果您的閘道器不會出現在 hello 清單中，您的伺服器可能不是處於 hello 與 hello 註冊 hello 閘道時，您指定的區域相同的區域。 

就這麼簡單。 如果您需要 tooopen 連接埠，或執行進行疑難排解，是確定 toocheck 出[在內部部署資料閘道](analysis-services-gateway.md)。

## <a name="next-steps"></a>後續步驟
* [ Analysis Services](analysis-services-manage.md)   
* [從 Azure Analysis Services 取得資料](analysis-services-connect.md)
