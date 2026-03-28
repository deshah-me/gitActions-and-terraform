# PostgreSQL Setup Guide

## ✅ Current Status

- **PostgreSQL Version**: 15.17
- **Status**: Running (Healthy)
- **Database**: `myapp` (created)
- **Port**: 5432

## 📊 Database Info

```
Database: myapp
Owner: postgres
Encoding: UTF8
```

## 🔌 Connection Details

| Detail | Value |
|--------|-------|
| **Host** | localhost |
| **Port** | 5432 |
| **Username** | postgres |
| **Password** | postgres |
| **Database** | myapp |

## 🐘 Connect via PostgreSQL Extension in VS Code

1. **Click the Elephant Icon** 🐘 in the left sidebar (PostgreSQL extension)
2. Click **"Add Server"** or **"+"**
3. Enter the connection details:
   ```
   Server/Host: localhost
   Port: 5432
   Database: myapp
   Username: postgres
   Password: postgres
   Save password: YES
   ```
4. Click **Save/Connect**
5. You'll see your database with all tables! 🎉

## 🔧 Quick Test Commands

### Test connection from terminal:
```bash
psql -h localhost -U postgres -d myapp -c "SELECT * FROM users;"
```

### Or from Docker:
```bash
docker exec postgres-db psql -U postgres -d myapp -c "SELECT * FROM users;"
```

## 📋 Current Tables

Your database has 3 tables:

### 1. **users** - User information
- id (Primary Key)
- name
- email (Unique)
- created_at

### 2. **projects** - Projects created by users
- id (Primary Key)
- user_id (Foreign Key → users)
- name
- description
- created_at

### 3. **tasks** - Tasks within projects
- id (Primary Key)
- project_id (Foreign Key → projects)
- title
- status
- created_at

## 📈 Current Data

```
Users: 2 records
Projects: 4 records
Tasks: 6 records
```

## 💾 Backup Your Database

```bash
docker exec postgres-db pg_dump -U postgres myapp > myapp_backup.sql
```

## 📥 Restore from Backup

```bash
docker exec -i postgres-db psql -U postgres myapp < myapp_backup.sql
```

## 🚀 Next Steps

1. ✅ PostgreSQL is running
2. ✅ Database `myapp` is created with tables
3. **TODO**: Connect via the elephant icon in VS Code
4. **TODO**: Build your Java backend to interact with database
5. **TODO**: Create React frontend to call your API

## 🆘 Troubleshooting

### Container not running?
```bash
docker-compose -f .devcontainer/docker-compose.yml up -d
```

### Check container logs:
```bash
docker logs postgres-db
```

### Reset database:
```bash
docker-compose -f .devcontainer/docker-compose.yml down -v
docker-compose -f .devcontainer/docker-compose.yml up -d
```

## 📌 Useful SQL Queries

```sql
-- View all users
SELECT * FROM users;

-- View all projects with user names
SELECT p.id, p.name, u.name as user_name, p.description 
FROM projects p 
JOIN users u ON p.user_id = u.id;

-- View all tasks with details
SELECT t.id, t.title, t.status, p.name as project_name, u.name as user_name
FROM tasks t
JOIN projects p ON t.project_id = p.id
JOIN users u ON p.user_id = u.id;

-- Count records
SELECT 
  (SELECT COUNT(*) FROM users) as users,
  (SELECT COUNT(*) FROM projects) as projects,
  (SELECT COUNT(*) FROM tasks) as tasks;
```

## 🎯 You're All Set!

PostgreSQL is fully configured and ready for development. Use the elephant icon in VS Code to manage your database! 🐘
