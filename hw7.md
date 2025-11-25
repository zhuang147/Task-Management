## ERD

```mermaid
erDiagram
    %% 實體定義

    User ||--|{ Project_Member : "加入 (Joins)"
    User ||--|{ Comment : "發佈 (Posts)"
    User ||--o{ Task_Log : "執行更新 (Updates)"
    User ||--o{ Notification : "接收 (Receives)"
    
    Project ||--|{ Project_Member : "擁有 (Has)"
    Project ||--|{ Task : "包含 (Contains)"
    
    Task ||--|{ Comment : "擁有 (Has)"
    Task ||--o{ Task_Log : "被記錄 (Is Logged)"
    Task ||--o{ Notification : "觸發 (Triggers)"

    %% 1. 實體詳細屬性
    User {
        int UserID PK "使用者ID"
        string Email "電子郵件"
        string Password "密碼"
        string Name "姓名"
        string Role "系統角色"
    }

    Project {
        int ProjectID PK "專案編號"
        string ProjectName "專案名稱"
        date StartDate "開始日期"
        date EndDate "結束日期"
        string Status "專案狀態"
    }

    Task {
        int TaskID PK "任務編號"
        int ProjectID FK "所屬專案ID"
        int AssigneeID FK "負責人(UserID)"
        string Title "標題"
        string Content "內容"
        string Status "狀態(未開始/進行中/已完成)"
        date DueDate "截止日期"
        int Progress "進度百分比"
    }

    Comment {
        int CommentID PK "留言編號"
        int TaskID FK "任務ID"
        int UserID FK "留言者ID"
        string Content "留言內容"
        datetime Timestamp "發佈時間"
    }

    Notification {
        int NotificationID PK "通知編號"
        int UserID FK "接收者ID"
        int TaskID FK "關聯任務ID"
        string Message "訊息內容"
        boolean IsRead "是否已讀"
        datetime CreatedAt "建立時間"
    }

    %% 2. 組合實體 (Composite Entities)
    Project_Member {
        int ProjectID FK "專案ID"
        int UserID FK "成員ID"
        string Role "小組角色(組長/組員)"
        date JoinDate "加入日期"
    }

    Task_Log {
        int LogID PK "紀錄編號"
        int TaskID FK "任務ID"
        int UserID FK "操作者ID"
        string ActionType "動作類型(狀態更新/進度修改)"
        string PreviousStatus "原狀態"
        string NewStatus "新狀態"
        datetime UpdateTime "更新時間"
    }
```


erDiagram
    %% ==========================================
    %% 1. 用戶 (Users)
    %% ==========================================
    USERS {
        int user_id PK "使用者ID"
        string username "使用者名稱"
        string email "電子郵件 (Unique)"
        string password_hash "密碼雜湊"
        datetime created_at "註冊時間"
    }

    %% ==========================================
    %% 2. 專案與成員 (Projects & Members)
    %% ==========================================
    PROJECTS {
        int project_id PK "專案ID"
        string name "專案名稱"
        text description "專案描述"
        int owner_id FK "擁有者(老師/組長)"
        datetime created_at
    }

    PROJECT_MEMBERS {
        int project_id FK "專案ID"
        int user_id FK "用戶ID"
        enum role "角色: leader/member"
        datetime joined_at
    }

    %% ==========================================
    %% 3. 任務 (Tasks)
    %% ==========================================
    TASKS {
        int task_id PK "任務ID"
        int project_id FK "所屬專案"
        string title "標題"
        text content "內容"
        int creator_id FK "建立者"
        int assignee_id FK "負責人"
        enum status "狀態: pending/in_progress/completed"
        enum priority "優先級: low/medium/high"
        datetime deadline "截止日"
        datetime created_at
        datetime updated_at
    }

    %% ==========================================
    %% 4. 紀錄與協作 (Logs, Comments, Notifications)
    %% ==========================================
    TASK_LOGS {
        int log_id PK
        int task_id FK
        int user_id FK "操作者"
        string action "動作類型"
        text old_value
        text new_value
        datetime created_at
    }

    COMMENTS {
        int comment_id PK
        int task_id FK
        int user_id FK "留言者"
        text message "內容"
        int parent_id FK "回覆留言ID (Self)"
        datetime created_at
    }

    NOTIFICATIONS {
        int notification_id PK
        int user_id FK "接收者"
        string type "通知類型"
        text content "通知內容"
        int related_task_id FK "關聯任務"
        boolean is_read "是否已讀"
        datetime created_at
    }

    %% ==========================================
    %% 關聯定義 (Relationships)
    %% ==========================================
    
    %% 用戶與專案
    USERS ||--o{ PROJECTS : "owns (1:N)"
    USERS ||--o{ PROJECT_MEMBERS : "belongs_to (1:N)"
    PROJECTS ||--|{ PROJECT_MEMBERS : "has_members (1:N)"

    %% 專案與任務
    PROJECTS ||--o{ TASKS : "contains (1:N)"
    
    %% 用戶與任務 (建立與指派)
    USERS ||--o{ TASKS : "creates/assigned_to (1:N)"

    %% 任務與周邊功能
    TASKS ||--o{ COMMENTS : "has_discussion (1:N)"
    TASKS ||--o{ TASK_LOGS : "logs_history (1:N)"
    TASKS ||--o{ NOTIFICATIONS : "triggers (1:N)"

    %% 用戶與周邊功能
    USERS ||--o{ COMMENTS : "writes (1:N)"
    USERS ||--o{ TASK_LOGS : "performs_action (1:N)"
    USERS ||--o{ NOTIFICATIONS : "receives (1:N)"

    %% 自關聯 (留言回覆)
    COMMENTS ||--o{ COMMENTS : "replies_to (1:N)"
```
