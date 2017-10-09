---
title: "Connect Arduino (C) tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定 Adafruit Feather M0 WiFi 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "設定好之後，arduino 連接 arduino toopc、 安裝 arduino、 arduino 面板"
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
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="b8f8b-104">設定裝置</span><span class="sxs-lookup"><span data-stu-id="b8f8b-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b8f8b-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b8f8b-105">What you will do</span></span>
<span data-ttu-id="b8f8b-106">藉由組裝 hello 面板，打開它來設定第一次您 Adafruit 羽毛 M0 WiFi Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="b8f8b-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b8f8b-108">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b8f8b-108">What you need</span></span>
<span data-ttu-id="b8f8b-109">toocomplete 這項作業，您必須依照您 Adafruit 羽毛 M0 WiFi 的入門套件的組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8f8b-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="b8f8b-110">hello Adafruit 羽毛 M0 WiFi 面板</span><span class="sxs-lookup"><span data-stu-id="b8f8b-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="b8f8b-111">微 B tooType USB 纜線</span><span class="sxs-lookup"><span data-stu-id="b8f8b-111">A Micro B tooType A USB cable</span></span>

![套件][kit]

<span data-ttu-id="b8f8b-113">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="b8f8b-113">You also need:</span></span>

* <span data-ttu-id="b8f8b-114">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="b8f8b-115">若要您 Arduino 面板 tooconnect 無線連線。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="b8f8b-116">網際網路連線 toodownload 組態工具。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b8f8b-117">學習目標</span><span class="sxs-lookup"><span data-stu-id="b8f8b-117">What you will learn</span></span>
<span data-ttu-id="b8f8b-118">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="b8f8b-118">In this article, you will learn:</span></span>

* <span data-ttu-id="b8f8b-119">如何 tooassemble hello 遵循針對您 Arduino 面板和電源課程。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="b8f8b-120">如何在 Ubuntu 上 tooadd 序列連接埠的權限。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="b8f8b-121">連接 Arduino 面板 tooyour 電腦</span><span class="sxs-lookup"><span data-stu-id="b8f8b-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="b8f8b-122">插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠][top-micro-usb-port]

2. <span data-ttu-id="b8f8b-124">隨插即用 hello USB 纜線的一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-124">Plug hello other end of USB cable into your computer.</span></span>

   ![電腦 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="b8f8b-126">在 Ubuntu 上新增序列連接埠權限</span><span class="sxs-lookup"><span data-stu-id="b8f8b-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="b8f8b-127">如果您使用 Windows 或 macOS，則可略過本節。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="b8f8b-128">Ubuntu，您必須遵循步驟 toomake 確認 hello 一般 linux 使用者 Arduino 面板的 hello USB 連接埠上擁有 hello 權限 toooperate hello。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="b8f8b-129">現在從終端機以一般使用者身分︰</span><span class="sxs-lookup"><span data-stu-id="b8f8b-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b8f8b-130">您會看到類似下面的內容：</span><span class="sxs-lookup"><span data-stu-id="b8f8b-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="b8f8b-131">hello"0"可能是不同的數字，或可能傳回多個項目。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="b8f8b-132">在 hello 我們需要第一個案例的 hello 資料是`uucp`，hello 在第二個是`dialout`，即 hello hello 檔案群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="b8f8b-133">新增使用者 toohello toohello 群組：</span><span class="sxs-lookup"><span data-stu-id="b8f8b-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="b8f8b-134">其中`group-name`hello 資料在 hello 第一個步驟中，找到並`username`是您的 linux 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="b8f8b-135">您必須登出 toolog 一次此變更 tootake 效果和完整 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="b8f8b-136">摘要</span><span class="sxs-lookup"><span data-stu-id="b8f8b-136">Summary</span></span>
<span data-ttu-id="b8f8b-137">在本文中，您學到如何 tooconfigure Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="b8f8b-138">hello 下一個工作是 tooinstall hello 必要工具和準備 Arduino 面板上執行範例應用程式中的軟體。</span><span class="sxs-lookup"><span data-stu-id="b8f8b-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![硬體已準備完畢][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="b8f8b-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8f8b-140">Next steps</span></span>
<span data-ttu-id="b8f8b-141">[取得 hello 工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="b8f8b-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md