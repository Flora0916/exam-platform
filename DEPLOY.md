# 部署指南 / Deployment Guide

整个过程约 30-40 分钟，分三步完成。

---

## 第一步：注册 Supabase（数据库）

1. 打开 https://supabase.com，点击 **Start your project** 注册账号

2. 创建一个新项目（Project name 随便填，如 `exam-platform`，选择离中国近的区域如 `Singapore`）

3. 等待项目初始化（约 1-2 分钟）

4. 进入项目后，点左侧菜单 **SQL Editor**

5. 把 `supabase/schema.sql` 文件里的全部内容复制进去，点 **Run**
   - 这会创建所有数据库表和权限设置
   
6. 点左侧菜单 **Project Settings → API**，记录下：
   - **Project URL**（如 `https://xxxxx.supabase.co`）
   - **anon public** key（很长的一串字符）
   
7. 点左侧菜单 **Authentication → Users**，点 **Add user** 创建你的教师账号（填邮箱+密码）

---

## 第二步：部署到 Vercel

1. 打开 https://github.com，注册 GitHub 账号（如果已有可跳过）
2. 创建一个新 repository（名字如 `exam-platform`），上传本项目文件
   - 或者在项目文件夹运行：`git init && git add . && git commit -m "init" && git remote add origin YOUR_REPO_URL && git push`
3. 打开 https://vercel.com，用 GitHub 账号登录
4. 点 **Add New → Project**，选择刚才的 GitHub 仓库，点 **Import**
5. 在 **Environment Variables** 区域添加两个变量：
   ```
   NEXT_PUBLIC_SUPABASE_URL = 你在第一步记录的 Project URL
   NEXT_PUBLIC_SUPABASE_ANON_KEY = 你在第一步记录的 anon key
   ```
6. 点 **Deploy**，等待约 1-2 分钟

部署完成后，Vercel 会给你一个网址（如 `exam-platform.vercel.app`），这就是你的系统地址。

---

## 第三步：开始使用

### 老师操作

1. 访问 `你的网址/admin/login`，用第一步创建的账号登录
2. 点 **新建考试** → 填写名称、选择模式
3. 添加部分（阅读/听力/写作）→ 上传 PDF → 录入题目和答案
4. 点 **复制链接** → 发给学生

### 学生操作

1. 打开老师发来的链接
2. 输入姓名，点开始考试
3. 答题后提交

### 查看结果

进入考试 → 点 **查看结果** → 点某个学生 → 查看作答 / 批改写作

---

## 常见问题

**学生打开链接显示"找不到页面"？**
检查考试是否已激活（is_active = true），以及链接中的考试代码是否正确。

**音频播放不了？**
网盘链接需要是可直接访问的音频文件链接（非下载页面）。建议用阿里云盘或其他支持直链的服务。

**忘记登录密码？**
在 Supabase 后台 → Authentication → Users，可以重置密码。
