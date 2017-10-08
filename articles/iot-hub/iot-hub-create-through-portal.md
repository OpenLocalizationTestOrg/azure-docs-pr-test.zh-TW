---
title: "aaaUse hello Azure 入口網站 toocreate IoT 中樞 |Microsoft 文件"
description: "如何 toocreate、 管理及刪除透過 hello Azure 入口網站的 Azure IoT 中樞。 其中包括定價層、調整、安全性和傳訊組態的相關資訊。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>建立 IoT 中心使用 hello Azure 入口網站

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

本文章說明：

* 如何 toofind hello IoT 中樞 hello Azure 入口網站中的服務。
* 如何 toocreate 並管理 IoT 中樞。

## <a name="where-toofind-hello-iot-hub-service"></a>其中 toofind hello IoT 中心服務

您可以在下列位置 hello 入口網站中的 hello 找到 hello IoT 中樞服務：

* 選擇 [+ 新增]，然後選擇 [物聯網]。
* 在 hello Marketplace，選擇 **物聯網**。

## <a name="create-an-iot-hub"></a>建立 IoT 中樞

您可以建立 IoT 中心使用 hello 下列方法：

* hello **+ 新增**選項會開啟 hello 下列螢幕擷取畫面所示的 hello 刀鋒視窗。 建立 hello IoT 中樞，透過這個方法，以及透過 hello marketplace hello 步驟完全相同。
* 在 hello Marketplace，選擇 **建立**tooopen hello 刀鋒視窗 hello 下列螢幕擷取畫面所示。

hello 下列各節說明 hello 幾個步驟 toocreate IoT 中心：

### <a name="choose-hello-name-of-hello-iot-hub"></a>選擇 hello hello IoT 中樞名稱

toocreate IoT 中樞，您必須命名 hello IoT 中樞。 此名稱不得與任何 IoT 中樞之名稱重複。

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>選擇定價層的 hello

您可以從 4 個層級中選擇：**免費**、**標準 1**、**標準 2** 和**標準 S3**。 只有 500 裝置 toobe 連線 toohello IoT 中樞，並 too8，每天 000 訊息上，可讓 hello 免費層。

**標準 S1**： 大量的每個產生的少量資料的裝置與 IoT 解決方案使用 hello S1 版本。 每個單位的 hello S1 edition 可讓向上 too400，000 到所有連線的裝置每天的訊息。

**標準 S2**： 使用 hello S2 edition 的 IoT 解決方案所在的裝置會產生大量的資料。 每個單位的 hello S2 edition 可讓向上 too6 百萬個訊息每日之間所有連線的裝置。

**標準 S3**： 產生大量資料的 IoT 解決方案使用 hello S3 版本。 每個單位的 hello S3 edition 可讓向上 too300 百萬個訊息每日之間所有連線的裝置。

![][4]

> [!NOTE]
> IoT 中樞只允許每個 Azure 訂用帳戶有一個免費中樞。

### <a name="iot-hub-units"></a>IoT 中樞單位

hello 訊息允許每個每日的單位數目取決於您的中樞定價層。 例如，如果您想 hello IoT 中樞 toosupport 輸入的 700,000 訊息時，您可以選擇 S1 層的兩個單位。

### <a name="device-toocloud-partitions-and-resource-group"></a>裝置 toocloud 資料分割和資源群組

您可以變更 hello IoT 中樞的資料分割數目。 hello 的資料分割的預設值為 4，您可以從 hello 下拉式清單選擇不同的數字。

您不需要 tooexplicitly 建立空的資源群組。 當您建立資源時，您可以選擇在新的任一 toocreate，或使用現有的資源群組。

![][5]

### <a name="choose-subscription"></a>選擇訂用帳戶

Azure IoT 中樞自動列出 hello hello Azure 訂用帳戶的使用者帳戶會連結到。 您可以選擇 hello Azure 訂用帳戶 tooassociate hello IoT 中樞。

### <a name="choose-hello-location"></a>選擇 hello 位置

hello 位置選項提供 hello IoT 中樞所在的地區的清單。

### <a name="create-hello-iot-hub"></a>建立 hello IoT 中樞

上述所有步驟完成時，您可以建立 hello IoT 中樞。 按一下**建立**toostart hello 後端程序 toocreate 及部署您所選擇的 hello 選項與 hello IoT 中樞。

它可能需要幾分鐘的時間 toocreate hello IoT 中樞，因為它需要花費一些時間 hello 後端部署 toorun hello 適當位置的伺服器上。

## <a name="change-hello-settings-of-hello-iot-hub"></a>變更 hello hello IoT 中樞設定

建立從 hello IoT 中樞刀鋒視窗之後，您可以變更現有的 IoT 中樞 hello 設定。

![][8]

**共用存取原則**： 這些原則定義裝置與服務 tooconnect tooIoT 中樞的 hello 權限。 您可以按一下 [一般] 之下的 [共用存取原則] 來存取這些原則。 在這個刀鋒視窗中，您可以修改現有的原則或新增原則。

### <a name="create-a-policy"></a>建立原則

* 按一下**新增**tooopen 刀鋒視窗。 您可以在這裡輸入 hello 新原則的名稱和圖 hello 下列所示，想要與此原則，tooassociate hello 權限：

    有許多權限可與這些共用原則產生關聯。 hello**登錄讀取**和**登錄寫入**原則授與讀取和寫入存取權限 toohello 身分識別登錄。 自動選擇 hello 寫入選項選擇 hello 讀取選項。

    hello**服務連線**原則授與權限 tooaccess 服務端點，例如**接收裝置到雲端**。 hello**裝置連線**原則授與傳送和接收訊息使用 hello IoT 中樞裝置端端點的權限。

* 按一下**建立**tooadd 此新建立的原則 toohello 現有清單。

![][10]

## <a name="endpoints"></a>端點

按一下**端點**toodisplay hello IoT 中樞，您要修改的端點清單。 有兩種類型的端點： hello IoT 中樞，內建的端點和您在建立之後新增 toohello IoT 中樞端點。

![][11]

### <a name="built-in-endpoints"></a>內建端點

有兩個內建端點：**雲端 toodevice 意見反應**和**事件**。

* **雲端 toodevice 意見反應**設定： 此設定有兩個 subsettings:**雲端 tooDevice TTL** （-存留時間） 和**保留時間**（以小時為單位） 的 hello 訊息。 當您第一次建立 IoT 中樞時，這些設定會有一小時的 hello 預設值。 tooadjust 這些設定，請使用 hello 滑桿，或輸入 hello 值。
* **事件**設定：這個設定有數個子設定，其中有些是唯讀。 hello 下列清單描述這些設定：

  * **資料分割**： 建立 hello IoT 中樞時，會設定預設值。 您可以變更 hello 透過這項設定的資料分割數目。

  * **事件中樞相容的名稱和端點**： 建立 hello IoT 中樞時，事件中心建立在內部，您可能需要存取 toounder 某些情況。 您無法自訂 hello 事件中樞相容名稱與端點的值，但您可以按一下 複製**複製**。

  * **保留時間**： 依預設，設定 tooone 天，但您可以使用變更 hello 下拉式清單。 這個值是以 hello 裝置到雲端設定的天數。

  * **取用者群組**： 取用者群組可讓多個讀取器 tooread 訊息分開 hello IoT 中樞。 每個 IoT 中樞都是使用預設取用者群組建立的。 不過，您可以新增或刪除使用此設定的取用者群組 tooyour IoT 中樞。

  > [!NOTE]
  > 無法編輯或刪除 hello 預設取用者群組。

### <a name="custom-endpoints"></a>自訂端點

您可以加入自訂端點，在您使用 hello 入口網站的 IoT 中樞上。 從 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooopen hello**加入端點**刀鋒視窗。 輸入 hello 所需的資訊，然後按一下 **確定**。 您的自訂端點現在會列示在 hello 主要**端點**刀鋒視窗。

![][13]

您可以在[參考 - IoT 中樞端點][lnk-devguide-endpoints]中深入了解自訂端點。

## <a name="routes"></a>路由

按一下**路由**toomanage IoT 中樞將您的裝置到雲端訊息的分派。

![][14]

您可以按一下 新增路由 tooyour IoT 中樞**新增**頂端的 hello hello**路由*** 刀鋒視窗中，輸入所需的 hello 的詳細資訊，並按一下**確定**。 您的路由再列於 hello 主要**路由**刀鋒視窗。 您可以編輯路由的路由 hello 清單中按一下。 tooenable 路由，路由 hello 清單中按一下它，並設定 hello**啟用**太切換**關閉**。 toosave hello 變更，按一下 **確定**在 hello hello 刀鋒視窗的底部。

![][15]

## <a name="pricing-and-scale"></a>價格和調整

可以變更現有 IoT 中樞定價 hello 透過 hello**定價**設定，以下列例外狀況的 hello:

* Hello 目前實作中，在 IoT 中樞與可用的 SKU 無法變更層 tooone 的 hello 付費的 Sku，反之亦然。
* 在 hello Azure 訂用帳戶只能有一個免費層 IoT 中樞。

![][12]

Hello 傳送該日的訊息數目超過 hello 較低層的 hello 配額時，才可以移動從較高的 toolower 層。 例如，如果 hello 每天的訊息數目超過 400000，然後 hello 層 hello IoT 中樞可變更。 不過，如果您變更 toohello S1 層 hello IoT 中心已節流的那一天。

## <a name="delete-hello-iot-hub"></a>刪除 hello IoT 中樞

您可以瀏覽要依序按一下 toodelete toohello IoT 中樞**瀏覽**，然後選擇 hello 適當中樞 toodelete 和。 toodelete hello IoT 中樞中，按一下 hello**刪除**hello IoT 中樞名稱下方的按鈕。

## <a name="next-steps"></a>後續步驟

請遵循這些連結 toolearn 更多關於管理 Azure IoT 中樞：

* [大量管理 IoT 裝置][lnk-bulk]
* [IoT 中樞度量][lnk-metrics]
* [作業監視][lnk-monitor]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [使用 IoT Edge 來模擬裝置][lnk-iotedge]
* [保護您的 IoT 解決方案從接地 hello][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
