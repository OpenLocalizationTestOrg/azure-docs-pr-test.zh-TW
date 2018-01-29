---
title: "針對遠端監視解決方案中的裝置進行疑難排解 - Azure | Microsoft Docs"
description: "本教學課程會示範如何針對遠端監視解決方案中的裝置問題進行疑難排解及加以補救。"
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-suite
ms.date: 12/12/2017
ms.topic: article
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.workload: NA
ms.openlocfilehash: d26275b6b03115b775990c9efb5d4706fcb829d1
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2017
---
# <a name="troubleshoot-and-remediate-device-issues"></a>針對裝置問題進行疑難排解和補救

本教學課程會示範如何使用解決方案中的 [維護] 頁面，針對裝置問題進行疑難排解及補救。 為了介紹這些功能，本教學課程會使用 Contoso IoT 應用程式中的情節。

Contoso 會在現場測試新的**原型**裝置。 身為 Contoso 操作員，您會注意到，在測試期間**原型**裝置會意外觸發儀表板上的溫度警示。 您必須立即調查此錯誤**原型**裝置的行為。

在本教學課程中，您了解如何：

>[!div class="checklist"]
> * 使用 [維護] 頁面來調查警示
> * 呼叫裝置方法以補救問題

## <a name="prerequisites"></a>必要條件

若要依循本教學課程進行操作，您需要在 Azure 訂用帳戶中有一個已部署的遠端監視解決方案執行個體。

如果您尚未部署遠端監視解決方案，應該先完成[部署遠端監視預先設定的解決方案](iot-suite-remote-monitoring-deploy.md)教學課程。

## <a name="use-the-maintenance-dashboard"></a>使用維護儀表板

在 [儀表板] 頁面上，您會注意到有非預期的溫度警示來自與**原型**裝置相關聯的規則：

![在儀表板上顯示的警示](media/iot-suite-remote-monitoring-maintain/dashboardalarm.png)

如需進一步調查問題，請選擇警示旁的 [探索警示] 選項：

![從儀表板探索警示](media/iot-suite-remote-monitoring-maintain/dashboardexplorealarm.png)

顯示警示的詳細資料檢視：

* 當觸發警示時
* 與警示相關聯之裝置的狀態資訊
* 與警示相關聯之裝置的遙測

![警示詳細資料](media/iot-suite-remote-monitoring-maintain/maintenancealarmdetail.png)

若要認知警示，請選取 [警示出現]，然後選擇 [認知]。 這個動作可讓其他操作員看到您已看過警示並正在加以處理。

![認知警示](media/iot-suite-remote-monitoring-maintain/maintenanceacknowledge.png)

在清單中，您可以看到負責引發溫度警示的**原型**裝置：

![列出造成警示的裝置](media/iot-suite-remote-monitoring-maintain/maintenanceresponsibledevice.png)

## <a name="remediate-the-issue"></a>補救問題

若要使用**原型**裝置補救問題，您必須在裝置上呼叫 **DecreaseTemperature** 方法。

若要在裝置上採取行動，請在裝置清單中選取它，然後選擇 [排程]。 **原型**裝置型號指定裝置必須支援的四種方法：

![檢視裝置支援的方法](media/iot-suite-remote-monitoring-maintain/maintenancemethods.png)

選擇 **DecreaseTemperature**，並將作業名稱設定為 **DecreaseTemperature**。 然後選擇 [套用]：

![建立作業以降低溫度](media/iot-suite-remote-monitoring-maintain/maintenancecreatejob.png)

若要追蹤工作的狀態上**維護**頁面上，選擇**作業**。 使用**作業**檢視追蹤的所有工作和方案中呼叫的方法：

![監視作業以降低溫度](media/iot-suite-remote-monitoring-maintain/maintenancerunningjob.png)

若要檢視或方法呼叫的特定作業的詳細資訊，請選擇它在清單中**作業**檢視：

![檢視工作詳細資料](media/iot-suite-remote-monitoring-maintain/maintenancejobdetail.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們已示範如何：

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * 使用 [維護] 頁面來調查警示
> * 呼叫裝置方法以補救問題

現在您已了解如何管理裝置問題，建議的下一個步驟是了解如何[使用模擬裝置測試您的解決方案](iot-suite-remote-monitoring-test.md)。

<!-- Next tutorials in the sequence -->