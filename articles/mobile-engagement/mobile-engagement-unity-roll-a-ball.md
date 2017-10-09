---
title: "aaaUnity 回復球教學課程"
description: "步驟 toocreate hello 傳統 Unity 回復球遊戲也就是所有的 Mobile Engagement Unity 教學課程的必要條件"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a id="unity-roll-a-ball"></a>建立 Unity Roll a Ball 遊戲
本教學課程引導 hello 主要步驟稍微修改[Unity 回復球教學課程](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)。 此範例遊戲包含球面 'player' 物件所控制的 hello 應用程式的使用者與 hello hello 遊戲目標是 too'collect' 可回收物件衝突的 hello 播放程式物件，與這些可回收物件。 這是假設使用者對 Unity 編輯器環境有基本的熟悉度。 如果您遇到任何問題，您應該參閱 toohello 完整的教學課程。 

### <a name="setting-up-hello-game"></a>設定 hello 遊戲
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. 開啟 **Unity 編輯器**，然後按一下新增。 
   
    ![][51] 
2. 提供 [專案名稱]  &  [位置]、選取 [3D]，然後按一下 [建立專案]。
   
    ![][52]
3. 儲存剛才建立 hello 新專案的一部分，如同 hello 名稱 hello 預設場景**MiniGame**內新**\_場景**下的資料夾**資產**資料夾：
   
    ![][53]
4. 建立**3D 物件]-> [平面**為 hello 播放欄位，然後重新命名這個平面物件做為**地面**
   
    ![][1]
5. 重設 hello 轉換元件，這個**地面**物件，讓它位於 hello 原點。 
   
    ![][3]
6. 取消核取**顯示方格**從**Gizmos 功能表**hello**地面**物件。
   
    ![][4]
7. 更新 hello**標尺**元件 hello**地面**物件 toobe [X = 2，Y = 1，Z = 2]。 
   
    ![][5]
8. 加入新**3D 物件]-> [球體**toohello 專案和重新命名此球面物件當做**Player**。 
   
    ![][6]
9. 選取 hello **Player**物件，並按一下**重設轉換**類似 toohello 平面物件。 
10. 更新**轉換]-> [位置]-> [Y 座標**0.5 hello Player Y 元件。  
    
    ![][7]
11. 建立新資料夾，稱為**材料**hello 我們將在其中建立 hello 材料 toocolor hello 播放程式的專案中。 
12. 在此資料夾中建立一個稱為 **Background** 的新 **Material**。 
    
    ![][8]
13. 藉由更新 hello 更新 hello 色彩的 hello 材料**屑**它的屬性。 您可以選取 [0,32,64] hello RGB 值。 
    
    ![][9]
14. 將這份資料拖曳到 hello 場景檢視 tooapply 色彩 toohello**地面**物件。 
    
    ![][10]
15. 最後更新 hello**轉換]-> [旋轉]-> [Y** too60 為了清楚起見 hello 方向燈物件上的。 
    
    ![][12]

### <a name="moving-hello-player"></a>移動 hello 播放程式
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. 新增**RigidBody**元件 toohello **Player**物件。 
   
    ![][13]
2. 建立新資料夾，稱為**指令碼**hello 專案中。 
3. 按一下 [新增元件 -> 新增指令碼 -> C# 指令碼]。 將其命名為 **PlayerController**，然後按一下 [建立及新增]。 這將會建立並附加指令碼 toohello 播放程式物件。  
   
    ![][14]
4. 此指令碼在 hello 移**指令碼**hello 專案資料夾中的。 
5. 開啟 hello 指令碼，以便在您最愛的指令碼編輯器中編輯，以下列程式碼的 hello 更新 hello 指令碼並加以儲存。 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. 請注意該 hello 上述指令碼會使用**速度**屬性。 在 hello Unity 編輯器中，更新 hello 速度屬性 too10。  
   
    ![][15]
7. 叫用**播放**hello Unity 編輯器中。 現在您應該使用 hello 鍵盤可以 toocontrol hello 球，它應該旋轉並四處移動。 

### <a name="moving-hello-camera"></a>移動 hello 相機
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141)會結合 hello 和**Main 相機**toohello **Player**物件。 

1. 更新 hello **Transform.Position** toobe X = Y，0 = 10.5，Z =-10。  
2. 更新 hello **Transform.Rotation** toobe X = 45，Y = 0，Z = 0。  
   
    ![][16]
3. 加入新的指令碼呼叫**CameraController** toohello **MainCamera**並將其移 hello 指令碼 資料夾底下。 
   
    ![][17]
4. 開啟供編輯的 hello 指令碼，並新增下列程式碼中的 hello:
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. 在 Unity 環境-拖曳 hello 播放程式變數到 hello Player 位置 hello Main 相機物件，使 hello 兩個是與另一個相關聯。 
   
    ![][18]
6. 現在如果您遇到播放 hello Unity editor 和旋轉 hello Player 球物件中您會看到 hello 依照 hello 移動的相機。  

### <a name="setting-up-hello-play-area"></a>設定 hello 播放區域
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141)。 我們將建立 hello 牆以便 hello Player 球物件不會卸除關閉其移動中的 hello 播放區域周圍 hello 接地。 

1. 按一下 [建立 -> 建立空的 -> 遊戲物件]，並將它命名 **Walls**
   
    ![][19]
2. 在此 Walls 物件底下，建立新的 **3D 物件 -> Cube**，並將它命名為 "West wall"。 
   
    ![][20]
3. 更新 hello**轉換]-> [位置**和**轉換]-> [標尺**這個西牆上的物件。 
   
    ![][21]
4. 重複的 hello 西牆 toocreate**東部牆**以更新的 hello 轉換位置和小數位數。 
   
    ![][22]
5. 重複的 hello 東部牆 toocreate **North 牆**以更新的 hello 轉換位置和小數位數。 
   
    ![][23]
6. 重複的 hello North 牆並建立**南牆**以更新的 hello 轉換位置和小數位數。 
   
    ![][24]

### <a name="creating-collectible-objects"></a>建立可收集的物件
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141)。 我們將會建立一些吸引人尋找物件形成 hello 一組可收集之物件的 hello Player 球物件需要 too'collect' 由它們互相衝突。 

1. 建立新 **3D Cube** 物件，並將它命名為 Pickup。 
2. 調整 hello**轉換]-> [旋轉** & **轉換]-> [標尺**的 hello 收取物件。 
   
    ![][25]
3. 建立並附加**新的 C# 指令碼**呼叫**Rotator** toohello 收取物件。 請確定 tooput hello 指令碼 hello 指令碼 資料夾底下。 
   
    ![][26]
4. 開啟供編輯這個指令碼，並更新其遵循 toobe hello: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. 現在點擊的 hello 播放模式中 hello Unity Editor 和收取物件顯示會旋轉的軸上。
6. 在我們將建立材料以便為玩家著色所在的專案中，建立一個稱為 **Prefabs** 
   
    ![][27]
7. 拖曳 hello**收取**物件，並將它放在 hello Prefabs 資料夾。
   
    ![][28]
8. 建立一個稱為 **Pickups** 的新 **Empty Game** 物件。 重設其位置 tooorigin，然後拖曳 hello 收取物件，在此遊戲的物件。  
   
    ![][29]
9. 重複的 hello**收取**物件，並散佈在 hello**地面**物件周圍 hello **Player**物件藉由更新 hello **Transform.Position 的 X & Z**適當值。 
   
    ![][30]
10. 建立**新材料**呼叫**收取**並更新它 toobe 紅色色彩，以更新 hello**屑屬性**類似 toowhat 我們並未更新 hello 地面物件。 
    
    ![][31]
11. 適用於 hello 材料 tooall hello 4 收取物件。
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>收集 hello 收取物件
從 hello 則 hello 步驟[Unity 教學課程](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141)。 我們將會更新 hello 播放程式，使其能夠 too'collect' hello 正在與它們所收取的物件。 

1. 開啟 hello **PlayerController**附加的 toohello Player 物件以供編輯的指令碼，並更新 toohello 遵循：  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. 建立新**標記**呼叫**挑選向上**（它必須符合何謂 hello 指令碼中）  
   
    ![][33]
   
    ![][34]
3. 套用此**標記**toohello Prefab 收取物件。 
   
    ![][35]
4. 啟用**IsTrigger** hello Prefab 物件的核取方塊。
   
    ![][36]
5. 將固定的主體 tooPickup Prefab 物件。 效能最佳化，我們將會更新，我們使用 tooa 動態 collider hello 靜態 collider。 
   
    ![][37]
6. 最後檢查 hello **IsKinematic** hello prefab 物件屬性。 
   
    ![][38]
7. 叫用**播放**hello Unity editor，而且將會無法 tooplay 這**回復球**遊戲藉由移動 hello 方向輸入使用鍵盤按鍵的播放程式物件。 

### <a name="updating-hello-game-for-mobile-play"></a>更新行動裝置的播放遊戲 hello
上述從未的 hello Unity 從基本教學課程的 hello 區段。 現在我們將會修改 hello 遊戲 toomake 它易記的行動裝置。 請注意，我們使用鍵盤輸入 hello 遊戲為止進行測試。 現在我們將會修改它，讓我們可以控制 hello 播放程式使用 hello 影片的 hello 電話也就使用加速計做為輸入 hello。 

開啟 hello **PlayerController**指令碼編輯和更新的 hello **FixedUpdate**方法 toouse hello 影片從 hello 加速計 toomove hello 播放程式物件。 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

本教學課程結束時，使用 Unity 的基本遊戲建立，您可以選擇 tooplay hello 遊戲的裝置上部署。 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













