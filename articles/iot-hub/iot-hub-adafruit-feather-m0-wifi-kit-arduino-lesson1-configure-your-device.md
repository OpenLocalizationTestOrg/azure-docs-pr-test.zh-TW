---
title: "將 Arduino (C) 連接到 Azure IoT - 第 1 課：設定裝置 | Microsoft Docs"
description: "設定 Adafruit Feather M0 WiFi 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 設定, 將 arduino 連接到電腦, 設定 arduino, arduino 面板"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="745eb-104">設定裝置</span><span class="sxs-lookup"><span data-stu-id="745eb-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="745eb-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="745eb-105">What you will do</span></span>
<span data-ttu-id="745eb-106">設定 Adafruit Feather M0 WiFi Arduino 面板以進行首次使用，方法是組裝面板、接上電源。</span><span class="sxs-lookup"><span data-stu-id="745eb-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="745eb-107">如果您有任何問題，請在[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="745eb-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="745eb-108">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="745eb-108">What you need</span></span>
<span data-ttu-id="745eb-109">若要完成此作業，您需要 Adafruit Feather M0 WiFi 入門套件的下列零件：</span><span class="sxs-lookup"><span data-stu-id="745eb-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="745eb-110">Adafruit Feather M0 WiFi 面板</span><span class="sxs-lookup"><span data-stu-id="745eb-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="745eb-111">Micro B 轉 Type A 的 USB 纜線</span><span class="sxs-lookup"><span data-stu-id="745eb-111">A Micro B to Type A USB cable</span></span>

![套件][kit]

<span data-ttu-id="745eb-113">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="745eb-113">You also need:</span></span>

* <span data-ttu-id="745eb-114">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="745eb-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="745eb-115">可供 Arduino 面板連線的無線連線。</span><span class="sxs-lookup"><span data-stu-id="745eb-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="745eb-116">用來下載組態工具的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="745eb-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="745eb-117">學習目標</span><span class="sxs-lookup"><span data-stu-id="745eb-117">What you will learn</span></span>
<span data-ttu-id="745eb-118">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="745eb-118">In this article, you will learn:</span></span>

* <span data-ttu-id="745eb-119">如何組裝 Arduino 面板並接上電源，以進行接下來的課程。</span><span class="sxs-lookup"><span data-stu-id="745eb-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="745eb-120">如何在 Ubuntu 上新增序列連接埠權限。</span><span class="sxs-lookup"><span data-stu-id="745eb-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="745eb-121">將 Arduino 面板連線到電腦</span><span class="sxs-lookup"><span data-stu-id="745eb-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="745eb-122">將 micro USB 纜線插入最上方的 micro USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="745eb-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠][top-micro-usb-port]

2. <span data-ttu-id="745eb-124">將 USB 纜線的另一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="745eb-124">Plug the other end of USB cable into your computer.</span></span>

   ![電腦 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="745eb-126">在 Ubuntu 上新增序列連接埠權限</span><span class="sxs-lookup"><span data-stu-id="745eb-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="745eb-127">如果您使用 Windows 或 macOS，則可略過本節。</span><span class="sxs-lookup"><span data-stu-id="745eb-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="745eb-128">對於 Ubuntu，您需要執行下列步驟，以確定一般的 linux 使用者有權對 Arduino 面板的 USB 連接埠進行操作。</span><span class="sxs-lookup"><span data-stu-id="745eb-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="745eb-129">現在從終端機以一般使用者身分︰</span><span class="sxs-lookup"><span data-stu-id="745eb-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="745eb-130">您會看到類似下面的內容：</span><span class="sxs-lookup"><span data-stu-id="745eb-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="745eb-131">"0" 可能是不同的數字，或可能會傳回多個項目。</span><span class="sxs-lookup"><span data-stu-id="745eb-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="745eb-132">在第一個案例中，我們所需的資料是 `uucp`，在第二個案例中則是 `dialout`，這是檔案的群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="745eb-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="745eb-133">將使用者新增至群組︰</span><span class="sxs-lookup"><span data-stu-id="745eb-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="745eb-134">其中 `group-name` 是第一個步驟中找到的資料，`username` 則是您的 linux 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="745eb-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="745eb-135">您必須先登出再登入以讓此變更生效，並完成設定。</span><span class="sxs-lookup"><span data-stu-id="745eb-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="745eb-136">摘要</span><span class="sxs-lookup"><span data-stu-id="745eb-136">Summary</span></span>
<span data-ttu-id="745eb-137">在本文中，您已了解如何設定 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="745eb-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="745eb-138">下一個工作是安裝必要的工具和軟體，以準備在 Arduino 面板上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="745eb-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![硬體已準備完畢][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="745eb-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="745eb-140">Next steps</span></span>
<span data-ttu-id="745eb-141">[取得工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="745eb-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md