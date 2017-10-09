<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect 透過 hello 序列主控台
1. （直接或透過 USB 序列介面卡），請將序列纜線 toohello 裝置連線。
2. 開啟 hello**控制台**，然後開啟 hello**裝置管理員**。
3. Hello 下列圖例所示，請找出 hello COM 連接埠。
   
     ![透過序列主控台連接](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. 啟動 PuTTY。 
5. Hello 右窗格中，變更 hello**連線類型**太**序列**。
6. Hello 右窗格中，輸入 hello 適當的 COM 連接埠。 請確定 hello 序列組態參數設定如下：
   
   * 速度：115200
   * 資料位元：8
   * 停止位元：1
   * 同位檢查：無
   * 流量控制：無
     
     Hello 下列圖例顯示這些設定。
     
     ![PuTTY 設定](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > 如果 hello 預設流程控制設定無法運作，請嘗試設定 hello 流程控制 tooXON/XOFF。
     > 
     > 
7. 按一下**開啟**toostart 序列工作階段。

