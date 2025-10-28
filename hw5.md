┌────────────────────────┐
│        User            │
├────────────────────────┤
│ - userID: int          │
│ - username: string     │
│ - email: string        │
│ - password: string     │
├────────────────────────┤
│ + register()           │
│ + login()              │
│ + updateProfile()      │
└──────────┬─────────────┘
           │ 1..*
           │
           ▼
┌────────────────────────┐
│        Task            │
├────────────────────────┤
│ - taskID: int          │
│ - title: string        │
│ - description: string  │
│ - dueDate: date        │
│ - status: string       │
├────────────────────────┤
│ + createTask()         │
│ + editTask()           │
│ + deleteTask()         │
│ + markAsComplete()     │
└──────────┬─────────────┘
           │ 0..*
           │
           ▼
┌────────────────────────┐
│       Comment          │
├────────────────────────┤
│ - commentID: int       │
│ - content: string      │
│ - createdAt: datetime  │
├────────────────────────┤
│ + addComment()         │
│ + deleteComment()      │
└────────────────────────┘

┌────────────────────────┐
│       Category         │
├────────────────────────┤
│ - categoryID: int      │
│ - name: string         │
├────────────────────────┤
│ + addCategory()        │
│ + deleteCategory()     │
└──────────┬─────────────┘
           │ 1..*
           │
           ▼
┌────────────────────────┐
│        Task            │
└────────────────────────┘

┌────────────────────────┐
│        Tag             │
├────────────────────────┤
│ - tagID: int           │
│ - name: string         │
├────────────────────────┤
│ + addTag()             │
│ + removeTag()          │
└──────────┬─────────────┘
           │ *..*
           │
           ▼
┌────────────────────────┐
│        Task            │
└────────────────────────┘

