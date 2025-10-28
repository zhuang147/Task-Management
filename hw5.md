## UML類別圖
![UML1](UML1.png)

## <img src="黃玉狗.jpg" style="width:8%;" />使用案例1：建立任務 UML循序圖
```mermaid
sequenceDiagram
    participant 使用者 as 小組成員(User)
    participant 系統 as 任務管理系統(Task System)

    使用者->>系統: 點選「新增任務」按鈕
    系統->>使用者: 顯示任務輸入介面
    使用者->>系統: 輸入任務名稱、說明、負責人與截止日期
    使用者->>系統: 按下「儲存」
    alt 所有必填欄位皆已填寫
        系統->>系統: 建立新任務
        系統->>使用者: 顯示任務清單（含新任務）
    else 有欄位未填寫
        系統->>使用者: 提示「請完整填寫資料」
    end
```

## 使用案例2：更新任務進度 UML循序圖
```mermaid
sequenceDiagram
    title 使用案例 2：更新任務進度（Update Task Progress）

    participant 使用者 as 任務負責人（Assignee）
    participant 系統 as 任務管理系統
    participant 任務資料庫 as 任務資料表

    %% 使用者選擇任務（使用者有焦點在互動）
    
    使用者->>系統: 1. 選擇要更新的任務
    

    %% 系統處理並顯示詳細（系統被聚焦）
    activate 系統
    系統-->>使用者: 2. 顯示任務詳細資料
    deactivate 系統

    %% 使用者修改並按下更新（使用者再次聚焦）
    activate 使用者
    使用者->>系統: 3. 修改任務狀態或輸入進度百分比
    使用者->>系統: 4. 按下「更新」
    deactivate 使用者

    %% 系統驗證權限並儲存（系統與資料庫產生焦點）
    activate 系統
    alt 權限驗證成功（使用者為負責人）
        系統->>任務資料庫: 5. 儲存更新資料（狀態／進度）
        activate 任務資料庫
        任務資料庫-->>系統: 更新成功
        deactivate 任務資料庫

        系統-->>使用者: 6. 顯示更新後任務資料
        %% 系統推送即時同步通知（系統維持焦點）
        系統-->>所有: 7. 即時同步更新顯示
    else 權限不足
        系統-->>使用者: 顯示「無法修改此任務」
    end
    deactivate 系統

    note over 系統,任務資料庫: 後置條件：任務狀態已更新並同步顯示
```
## 使用案例3：留言與提醒 UML循序圖
```mermaid
sequenceDiagram
    participant U as 使用者
    participant UI as 任務頁面
    participant C as 系統控制器
    participant CS as 留言服務
    participant NS as 通知服務
    participant DB as 資料庫

    %% --- 主要流程 ---
    activate U
    U ->> UI: 輸入留言內容
    U ->> UI: 按下「發佈」
    deactivate U

    activate UI
    UI ->> C: 發送留言
    deactivate UI

    activate C
    C ->> CS: 驗證並保存
    deactivate C

    activate CS
    CS ->> CS: 檢查留言是否為空

    alt 留言內容為空
        CS -->> UI: 錯誤訊息「留言不得為空」
    else 留言內容有效
        CS ->> DB: 儲存留言
        activate DB
        DB -->> CS: 儲存成功
        deactivate DB

        CS ->> NS: 通知相關用戶(taskID, comment)
        activate NS
        NS ->> DB: 儲存通知
        activate DB
        DB -->> NS: 儲存成功
        deactivate DB

        NS ->> 相關成員: 發送提醒通知
        NS -->> CS: 通知成功
        deactivate NS

        CS -->> UI: 更新留言區顯示新留言
    end
    deactivate CS
```

## 使用案例2：更新任務進度 UML活動圖
```mermaid
stateDiagram-v2
direction LR
    [*] --> 選擇任務
    選擇任務: 使用者於任務清單中選擇要更新的任務
    選擇任務 --> 顯示任務: 系統顯示任務詳細資料

    顯示任務 --> 驗證身份
    驗證身份: 系統檢查使用者是否為任務負責人

    驗證身份 --> 修改任務: 權限通過
    驗證身份 --> 顯示錯誤: 權限不足

    修改任務: 使用者修改任務狀態或輸入進度百分比
    修改任務 --> 儲存任務
    儲存任務: 系統儲存修改並更新任務資料
    儲存任務 --> 同步更新
    同步更新: 系統即時同步顯示於所有成員畫面
    同步更新 --> [*]

    顯示錯誤: 顯示「無法修改此任務」
    顯示錯誤 --> [*]


```
