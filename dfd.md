```Mermaid
flowchart LR
  User["使用者\n(User)"]
  TeamLead["組長\n(Team Lead)"]
  Admin["管理員\n(Admin)"]
  Notif["通知服務\n(Notification Service)"]
  CalAPI["第三方日曆\n(Calendar API)"]

  subgraph System[任務管理系統\n(Task Management System)]
    direction TB
    SYS[(任務管理系統)]
  end

  User -->|建立/更新任務、登入| SYS
  SYS -->|任務列表、狀態回饋| User

  TeamLead -->|分派任務、優先順序| SYS
  SYS -->|分派通知、團隊進度| TeamLead

  Admin -->|帳號管理、設定| SYS
  SYS -->|系統報表、稽核資料| Admin

  SYS -->|提醒請求 (到期/分派)| Notif
  Notif -->|傳送回報| SYS

  SYS -->|同步事件 push| CalAPI
  CalAPI -->|事件回傳| SYS
```
