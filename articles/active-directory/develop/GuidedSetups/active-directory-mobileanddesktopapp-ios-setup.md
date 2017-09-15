---
title: "Azure AD v2 iOS 快速入門 - 設定 | Microsoft Docs"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: d25353a61b2a60bff28aa0679d38110e77d19e64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="261a1-103">設定您的 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="261a1-103">Setting up your iOS application</span></span>

<span data-ttu-id="261a1-104">本節提供逐步指示，說明如何建立新的專案來示範整合 iOS 應用程式 (Swift) 與使用 Microsoft 登入，以便它可以查詢需要權杖的 Web API。</span><span class="sxs-lookup"><span data-stu-id="261a1-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="261a1-105">想要改為下載此範例的 XCode 專案嗎？</span><span class="sxs-lookup"><span data-stu-id="261a1-105">Prefer to download this sample's XCode project instead?</span></span> <span data-ttu-id="261a1-106">[下載專案](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip)並跳至[設定步驟](#create-an-application-express)，以在執行之前先設定程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="261a1-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


## <a name="install-carthage-to-download-and-build-msal"></a><span data-ttu-id="261a1-107">安裝 Carthage 以下載並建置 MSAL</span><span class="sxs-lookup"><span data-stu-id="261a1-107">Install Carthage to download and build MSAL</span></span>
<span data-ttu-id="261a1-108">MSAL 預覽期間會使用 Carthage 套件管理員 – 與 XCode 整合，同時維持 Microsoft 對程式庫進行變更的能力。</span><span class="sxs-lookup"><span data-stu-id="261a1-108">Carthage package manager is used during the preview period of MSAL – it integrates with XCode while maintaining the ability for Microsoft to make changes to the library.</span></span>

- <span data-ttu-id="261a1-109">在[這裡](https://github.com/Carthage/Carthage/releases "Carthage 下載 URL") 下載並安裝最新版的 Carthage</span><span class="sxs-lookup"><span data-stu-id="261a1-109">Download and install the latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="261a1-110">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="261a1-110">Creating your application</span></span>

1.  <span data-ttu-id="261a1-111">開啟 Xcode 並選取 `Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="261a1-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="261a1-112">選取 `iOS`  >  `Single view Application`，然後按 [下一步]</span><span class="sxs-lookup"><span data-stu-id="261a1-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="261a1-113">提供產品名稱，然後按 [下一步]</span><span class="sxs-lookup"><span data-stu-id="261a1-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="261a1-114">選取用來建立應用程式的資料夾，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="261a1-114">Select a folder to create your app and click *Create*</span></span>

## <a name="build-the-msal-framework"></a><span data-ttu-id="261a1-115">建置 MSAL 架構</span><span class="sxs-lookup"><span data-stu-id="261a1-115">Build the MSAL Framework</span></span>

<span data-ttu-id="261a1-116">請遵循以下指示以使用 Carthage，提取然後建置最新版本的 MSAL 程式庫：</span><span class="sxs-lookup"><span data-stu-id="261a1-116">Follow the instructions below to pull and then build the latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="261a1-117">開啟 bash 終端機並移至應用程式的根資料夾</span><span class="sxs-lookup"><span data-stu-id="261a1-117">Open the bash terminal and go to the App’s root folder</span></span>
2.  <span data-ttu-id="261a1-118">複製下列項目並在 bash 終端機貼上，以建立 'Cartfile' 檔案：</span><span class="sxs-lookup"><span data-stu-id="261a1-118">Copy the below and paste in the bash terminal to create a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="261a1-119">複製並貼上下列項目。</span><span class="sxs-lookup"><span data-stu-id="261a1-119">Copy and paste the below.</span></span> <span data-ttu-id="261a1-120">此命令會將相依性擷取至 Carthage/Checkouts 資料夾，然後建置 MSAL 程式庫：</span><span class="sxs-lookup"><span data-stu-id="261a1-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds the MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="261a1-121">上述程序是用來下載並建置 Microsoft Authentication Library (MSAL)。</span><span class="sxs-lookup"><span data-stu-id="261a1-121">The process above is used to download and build the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="261a1-122">MSAL 會處理使用者權杖的取得、快取及重新整理作業，這些權杖是用來存取受 Azure Active Directory v2 保護的 API。</span><span class="sxs-lookup"><span data-stu-id="261a1-122">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by the Azure Active Directory v2.</span></span>

## <a name="add-the-msal-framework-to-your-application"></a><span data-ttu-id="261a1-123">將 MSAL 架構新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="261a1-123">Add the MSAL framework to your application</span></span>
1.  <span data-ttu-id="261a1-124">在 Xcode 中，開啟 [`General`] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="261a1-124">In Xcode, open the `General` tab</span></span>
2.  <span data-ttu-id="261a1-125">移至 [`Linked Frameworks and Libraries`] 區段，然後按一下 [`+`]</span><span class="sxs-lookup"><span data-stu-id="261a1-125">Go to the `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="261a1-126">選取 `Add other…`</span><span class="sxs-lookup"><span data-stu-id="261a1-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="261a1-127">選取：`Carthage` > `Build` > `iOS` > `MSAL.framework`，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="261a1-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="261a1-128">您應該會看到 `MSAL.framework` 新增至清單。</span><span class="sxs-lookup"><span data-stu-id="261a1-128">You should see `MSAL.framework` added to the list.</span></span>
5.  <span data-ttu-id="261a1-129">移至 [`Build Phases`] 索引標籤，然後按一下 [`+`] 圖示，選擇 [`New Run Script Phase`]</span><span class="sxs-lookup"><span data-stu-id="261a1-129">Go to `Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="261a1-130">將下列內容新增至 [指令碼區域]：</span><span class="sxs-lookup"><span data-stu-id="261a1-130">Add the following contents to the *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="261a1-131">藉由按一下 [<code>+</code>]，將下列項目新增至 [<code>Input Files</code>]：</span><span class="sxs-lookup"><span data-stu-id="261a1-131">Add the following to <code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="261a1-132">建立應用程式的 UI</span><span class="sxs-lookup"><span data-stu-id="261a1-132">Creating your application’s UI</span></span>
<span data-ttu-id="261a1-133">系統應會自動建立 Main.storyboard 檔案，作為專案範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="261a1-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="261a1-134">請遵循下列指示以建立應用程式 UI：</span><span class="sxs-lookup"><span data-stu-id="261a1-134">Follow the instructions below to create the app UI:</span></span>

1.  <span data-ttu-id="261a1-135">按住 Ctrl 鍵並按一下 `Main.storyboard` 以顯示內容功能表，然後按一下：`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="261a1-135">Control+click `Main.storyboard` to bring up the contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="261a1-136">使用下列程式碼來取代 `<scenes>` 節點：</span><span class="sxs-lookup"><span data-stu-id="261a1-136">Replace the `<scenes>` node with the code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
