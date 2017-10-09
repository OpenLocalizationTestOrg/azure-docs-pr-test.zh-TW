---
title: "aaaAzure AD v2 iOS 入門-安裝 |Microsoft 文件"
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
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a>設定您的 iOS 應用程式

本節提供有關如何逐步解說 toocreate 新的專案 toodemonstrate 如何 toointegrate iOS 應用程式 (Swift) 與*使用 Microsoft 登入*，它才能查詢要求權杖的 Web Api。

> 改為偏好 toodownload 這個範例的 XCode 專案嗎？ [下載專案](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip)並略過 toohello[組態步驟](#create-an-application-express)tooconfigure hello 程式碼範例，然後再執行。


## <a name="install-carthage-toodownload-and-build-msal"></a>安裝迦太基 toodownload 及建立 MSAL
迦太基封裝管理員會使用 hello 預覽期間的 MSAL – 與整合的 XCode 維持 hello Microsoft toomake 變更 toohello 文件庫的能力。

- 下載並安裝新版迦太基 hello[這裡](https://github.com/Carthage/Carthage/releases "迦太基下載 URL")

## <a name="creating-your-application"></a>建立應用程式

1.  開啟 Xcode 並選取 `Create a new Xcode project`
2.  選取 `iOS`  >  `Single view Application`，然後按 [下一步]
3.  提供產品名稱，然後按 [下一步]
4.  應用程式，並按一下 選取資料夾 toocreate*建立*

## <a name="build-hello-msal-framework"></a>建置 hello MSAL 架構

請遵循以下 toopull hello 指示，然後再建置 hello 使用迦太基 MSAL 程式庫的最新版本：

1.  開啟 hello bash 終端機，並移 toohello 應用程式的根資料夾
2.  複製 hello 下及貼到 hello bash 終端機 toocreate 'Cartfile' 檔案：

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
複製並貼上下列 hello。 此命令至迦太基/簽出資料夾中，擷取相依性，然後建置 hello MSAL 程式庫：
</li>
</ol>

```bash
carthage update
```

> 使用的 toodownload 而建置 hello Microsoft 驗證程式庫 (MSAL) hello 上述的程序。 MSAL 處理取得，快取和重新整理使用者使用的語彙基元 tooaccess hello Azure Active Directory v2 所保護的應用程式開發介面。

## <a name="add-hello-msal-framework-tooyour-application"></a>新增 hello MSAL framework tooyour 應用程式
1.  在 Xcode 中，開啟 [hello `General` ] 索引標籤
2.  移 toohello`Linked Frameworks and Libraries`區段，然後按一下`+`
3.  選取 `Add other…`
4.  選取：`Carthage` > `Build` > `iOS` > `MSAL.framework`，然後按一下 [開啟]。 您應該會看到`MSAL.framework`加入 toohello 清單。
5.  跳過`Build Phases`索引標籤，然後按一下`+`圖示，選擇`New Run Script Phase`
6.  新增下列內容 toohello hello*指令碼區域*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Hello 太之後加入<code>Input Files</code>按一下<code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>建立應用程式的 UI
系統應會自動建立 Main.storyboard 檔案，作為專案範本的一部分。 請遵循下列 toocreate hello 應用程式 UI 的 hello 指示：

1.  控制並按一下滑鼠左鍵`Main.storyboard`toobring 向上 hello 內容功能表，然後按一下：`Open As` > `Source Code`
2.  取代 hello`<scenes>`節點與 hello 的下列程式碼：

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
