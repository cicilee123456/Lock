# 電子密碼鎖系統流程圖

此流程圖描述了基於 8051 微控制器的電子密碼鎖運作邏輯。

```mermaid
graph TD
    Start[開機 / 初始化] --> Scan[掃描矩陣鍵盤]
    Scan --> Input{偵測輸入}
    
    Input -- 數字鍵 --> Store[存入緩衝區並計數]
    Store --> CheckCount{已輸入 4 位數?}
    CheckCount -- 否 --> Scan
    CheckCount -- 是 --> WaitConfirm[等待確認鍵 #]
    
    Input -- *鍵 --> Clear[清除緩衝區並重置 LED]
    Clear --> Scan
    
    Input -- #鍵 --> Verify{比對密碼}
    
    Verify -- 正確 --> Success[綠燈長亮 + 解鎖音]
    Success --> Reset[延遲後自動重置]
    Reset --> Scan
    
    Verify -- 錯誤 --> Fail[紅燈閃爍 + 警示音]
    Fail --> Reset
