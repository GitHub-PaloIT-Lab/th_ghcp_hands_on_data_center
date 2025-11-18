# React Project Setup Guide - From Zero to Ready

คู่มือการตั้งค่าโปรเจค React จากเริ่มต้นจนพร้อมเขียนโค้ด

## 📋 สารบัญ

1. [Prerequisites](#-prerequisites)
2. [Node.js Setup with NVM](#-nodejs-setup-with-nvm)
3. [Create React Project](#-create-react-project)
4. [Project Structure Setup](#-project-structure-setup)
5. [Essential Dependencies](#-essential-dependencies)
6. [Configuration Files](#-configuration-files)
7. [Folder Structure Creation](#-folder-structure-creation)
8. [Verify Installation](#-verify-installation)

---

## ✅ Prerequisites

### ต้องมีอะไรบ้าง
- macOS, Linux, หรือ Windows (WSL2 แนะนำ)
- Terminal/Command Line
- Git
- Code Editor (VS Code แนะนำ)

### ติดตั้ง Git (ถ้ายังไม่มี)
```bash
# macOS
brew install git

# Ubuntu/Debian
sudo apt-get install git

# ตรวจสอบ
git --version
```

### ติดตั้ง VS Code (แนะนำ)
ดาวน์โหลดจาก: https://code.visualstudio.com/

---

## 🔧 Node.js Setup with NVM

### 1. ติดตั้ง NVM (Node Version Manager)

```bash
# ติดตั้ง NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# สำหรับ zsh (macOS default)
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.zshrc
source ~/.zshrc

# สำหรับ bash
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc
source ~/.bashrc
```

### 2. ติดตั้ง Node.js v25.0.0

```bash
# ติดตั้ง Node.js v25.0.0
nvm install 25.0.0

# ตั้งเป็น default version
nvm alias default 25.0.0

# ใช้ version นี้
nvm use 25.0.0

# ตรวจสอบ version
node --version   # ควรได้ v25.0.0
npm --version    # ควรได้ 10.9.0 ขึ้นไป
```

### 3. ตั้งค่า npm (Optional แต่แนะนำ)

```bash
# เพิ่มความเร็วในการติดตั้ง packages
npm config set registry https://registry.npmjs.org/
npm config set fetch-retries 5
npm config set fetch-retry-mintimeout 20000
npm config set fetch-retry-maxtimeout 120000
```

---

## 🚀 Create React Project

### 1. สร้างโปรเจค React + TypeScript

```bash
# ไปยัง folder ที่ต้องการสร้างโปรเจค
cd ~/projects

# สร้างโปรเจค (ใช้เวลาประมาณ 2-3 นาที)
npx create-react-app my-app --template typescript

# เข้าไปใน project folder
cd my-app
```

### 2. ตรวจสอบว่าโปรเจคทำงาน

```bash
# รันโปรเจค
npm start

# เปิด browser ไปที่ http://localhost:3000
# ควรเห็นหน้า React logo หมุน
```

กด `Ctrl + C` เพื่อหยุด server

---

## 📁 Project Structure Setup

### โครงสร้างเริ่มต้นจาก Create React App

```
my-app/
├── node_modules/       # Dependencies (อย่าแก้ไข)
├── public/            # Static files
│   ├── index.html
│   └── favicon.ico
├── src/               # Source code
│   ├── App.tsx
│   ├── App.css
│   ├── index.tsx
│   └── index.css
├── package.json       # Project config
├── tsconfig.json      # TypeScript config
└── README.md
```

### โครงสร้างที่แนะนำสำหรับโปรเจคใหญ่

เราจะสร้างโครงสร้างที่เหมาะสำหรับโปรเจคทุกขนาด:

```
my-app/
├── public/
├── src/
│   ├── components/    # Shared components
│   │   ├── ui/       # Basic UI (Button, Input, etc.)
│   │   └── layout/   # Layout (Header, Footer, etc.)
│   ├── features/     # Feature modules
│   ├── hooks/        # Custom hooks
│   ├── services/     # API services
│   ├── types/        # TypeScript types
│   ├── utils/        # Utilities
│   ├── styles/       # Global styles
│   ├── __tests__/    # Test utilities
│   ├── App.tsx
│   └── index.tsx
├── .env              # Environment variables
├── .env.example      # Environment template
└── .gitignore
```

---

## 📦 Essential Dependencies

### 1. ติดตั้ง Development Tools

```bash
# ESLint และ Prettier สำหรับ code quality
npm install -D eslint-config-prettier prettier

# Testing utilities
npm install -D @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

### 2. ติดตั้ง State Management & Data Fetching

```bash
# React Query - สำหรับจัดการ server state
npm install @tanstack/react-query

# Axios - สำหรับ HTTP requests
npm install axios
```

### 3. เลือกติดตั้ง Styling Framework (เลือก 1 ใน 3)

#### Option 1: Tailwind CSS (แนะนำ)
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

#### Option 2: Styled Components
```bash
npm install styled-components
npm install -D @types/styled-components
```

#### Option 3: Emotion
```bash
npm install @emotion/react @emotion/styled
```

### 4. ติดตั้ง Router (ถ้าต้องการ)

```bash
# React Router v6
npm install react-router-dom
```

### 5. ติดตั้ง Form Handling (ถ้าต้องการ)

```bash
# React Hook Form
npm install react-hook-form

# Validation
npm install zod
npm install @hookform/resolvers
```

---

## ⚙️ Configuration Files

### 1. สร้างไฟล์ `.env.example`

```bash
# สร้างไฟล์
touch .env.example
```

```env
# .env.example
REACT_APP_API_URL=http://localhost:3001
REACT_APP_APP_NAME=My App
REACT_APP_ENVIRONMENT=development
```

### 2. สร้างไฟล์ `.env`

```bash
cp .env.example .env
```

### 3. อัพเดท `.gitignore`

```bash
# เพิ่มใน .gitignore
echo ".env" >> .gitignore
echo ".DS_Store" >> .gitignore
echo "*.log" >> .gitignore
```

### 4. สร้าง Prettier Config

```bash
# สร้างไฟล์
touch .prettierrc
```

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "endOfLine": "lf"
}
```

### 5. สร้าง VS Code Settings

```bash
# สร้าง folder
mkdir -p .vscode

# สร้างไฟล์
touch .vscode/settings.json
```

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": true
  },
  "typescript.preferences.importModuleSpecifier": "relative"
}
```

### 6. สร้าง VS Code Extensions Recommendations

```bash
touch .vscode/extensions.json
```

```json
{
  "recommendations": [
    "github.copilot",
    "github.copilot-chat",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "bradlc.vscode-tailwindcss"
  ]
}
```

### 7. อัพเดท `package.json` Scripts

เปิดไฟล์ `package.json` และเพิ่ม scripts:

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint src --ext .ts,.tsx",
    "lint:fix": "eslint src --ext .ts,.tsx --fix",
    "format": "prettier --write \"src/**/*.{ts,tsx,css,md}\"",
    "type-check": "tsc --noEmit"
  }
}
```

---

## 📂 Folder Structure Creation

### 1. สร้างโครงสร้าง folders

```bash
# สร้างทั้งหมดในคำสั่งเดียว
mkdir -p src/components/ui \
         src/components/layout \
         src/features \
         src/hooks \
         src/services \
         src/types \
         src/utils \
         src/styles \
         src/__tests__
```

### 2. สร้างไฟล์พื้นฐานในแต่ละ folder

#### components/ui/index.ts
```bash
touch src/components/ui/index.ts
```

```typescript
// src/components/ui/index.ts
// Export all UI components here
export {};
```

#### components/layout/index.ts
```bash
touch src/components/layout/index.ts
```

```typescript
// src/components/layout/index.ts
// Export all layout components here
export {};
```

#### services/api.ts
```bash
touch src/services/api.ts
```

```typescript
// src/services/api.ts
import axios from 'axios';

const api = axios.create({
  baseURL: process.env.REACT_APP_API_URL || 'http://localhost:3001',
  timeout: 10000,
});

// Request interceptor
api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Handle unauthorized
      localStorage.removeItem('token');
    }
    return Promise.reject(error);
  }
);

export default api;
```

#### types/index.ts
```bash
touch src/types/index.ts
```

```typescript
// src/types/index.ts
// Global TypeScript types

export interface ApiResponse<T> {
  data: T;
  message?: string;
  success: boolean;
}

export interface ApiError {
  message: string;
  code?: string;
  details?: any;
}
```

#### utils/constants.ts
```bash
touch src/utils/constants.ts
```

```typescript
// src/utils/constants.ts
export const APP_NAME = process.env.REACT_APP_APP_NAME || 'My App';
export const API_URL = process.env.REACT_APP_API_URL || 'http://localhost:3001';
export const ENVIRONMENT = process.env.REACT_APP_ENVIRONMENT || 'development';

export const ROUTES = {
  HOME: '/',
  ABOUT: '/about',
  // Add more routes
};
```

#### styles/globals.css
```bash
touch src/styles/globals.css
```

```css
/* src/styles/globals.css */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}
```

### 3. อัพเดท `src/index.tsx`

```typescript
// src/index.tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './styles/globals.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(
  document.getElementById('root') as HTMLElement
);
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

reportWebVitals();
```

### 4. สร้าง Example Component

```bash
mkdir -p src/components/ui/Button
touch src/components/ui/Button/index.ts
touch src/components/ui/Button/Button.tsx
touch src/components/ui/Button/Button.types.ts
```

#### Button.types.ts
```typescript
// src/components/ui/Button/Button.types.ts
export interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'small' | 'medium' | 'large';
  disabled?: boolean;
  onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;
  type?: 'button' | 'submit' | 'reset';
}
```

#### Button.tsx
```typescript
// src/components/ui/Button/Button.tsx
import React from 'react';
import { ButtonProps } from './Button.types';

export const Button: React.FC<ButtonProps> = ({
  children,
  variant = 'primary',
  size = 'medium',
  disabled = false,
  onClick,
  type = 'button',
}) => {
  const baseClasses = 'btn';
  const variantClasses = `btn--${variant}`;
  const sizeClasses = `btn--${size}`;
  
  return (
    <button
      type={type}
      className={`${baseClasses} ${variantClasses} ${sizeClasses}`}
      disabled={disabled}
      onClick={onClick}
    >
      {children}
    </button>
  );
};
```

#### Button/index.ts
```typescript
// src/components/ui/Button/index.ts
export { Button } from './Button';
export type { ButtonProps } from './Button.types';
```

### 5. สร้าง Example Custom Hook

```bash
touch src/hooks/useLocalStorage.ts
```

```typescript
// src/hooks/useLocalStorage.ts
import { useState, useEffect } from 'react';

export function useLocalStorage<T>(key: string, initialValue: T) {
  const [storedValue, setStoredValue] = useState<T>(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  const setValue = (value: T | ((val: T) => T)) => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue] as const;
}
```

---

## ✅ Verify Installation

### 1. ตรวจสอบ Project Structure

```bash
# แสดง tree structure
tree -L 3 src -I 'node_modules'

# หรือใช้ ls
ls -la src/
```

### 2. ตรวจสอบ Dependencies

```bash
# ดู installed packages
npm list --depth=0
```

### 3. ทดสอบรันโปรเจค

```bash
# Start dev server
npm start

# ใน terminal อื่น - ทดสอบ build
npm run build

# ทดสอบ linting
npm run lint

# ทดสอบ formatting
npm run format

# ทดสอบ type checking
npm run type-check
```

### 4. ทดสอบ Git

```bash
# Initialize git (ถ้ายังไม่มี)
git init

# Add files
git add .

# Commit
git commit -m "Initial project setup"
```

---

## 🎯 Next Steps

### 1. เริ่มเขียนโค้ด
```bash
# เปิดโปรเจคใน VS Code
code .
```

### 2. สร้าง Feature แรก
```bash
# สร้าง feature folder
mkdir -p src/features/home/components
mkdir -p src/features/home/hooks
mkdir -p src/features/home/services
mkdir -p src/features/home/types
```

### 3. ติดตั้ง VS Code Extensions
- GitHub Copilot
- GitHub Copilot Chat
- Prettier
- ESLint
- Tailwind CSS IntelliSense (ถ้าใช้ Tailwind)

### 4. Setup Git Repository
```bash
# Create repository on GitHub first, then:
git remote add origin https://github.com/username/repo-name.git
git branch -M main
git push -u origin main
```

---

## 📋 Quick Reference Commands

### Development
```bash
npm start              # เริ่ม dev server
npm run build          # Build production
npm test              # รัน tests
```

### Code Quality
```bash
npm run lint           # Check linting
npm run lint:fix       # Fix linting issues
npm run format         # Format code
npm run type-check     # Check TypeScript
```

### NVM
```bash
nvm list              # แสดง Node versions
nvm use 25.0.0        # เปลี่ยน version
nvm current           # แสดง version ปัจจุบัน
```

---

## 🎉 สรุป

ตอนนี้โปรเจคของคุณพร้อมแล้วสำหรับ:
- ✅ Development ด้วย React + TypeScript
- ✅ State Management ด้วย React Query
- ✅ API Integration ด้วย Axios
- ✅ Code Quality ด้วย ESLint + Prettier
- ✅ Testing ด้วย React Testing Library
- ✅ Modern Folder Structure
- ✅ GitHub Copilot Ready

**เริ่มเขียนโค้ดได้เลย! 🚀**

---

## 🆘 Troubleshooting

### ปัญหา: NVM command not found
```bash
# ติดตั้งใหม่และ source shell config
source ~/.zshrc  # หรือ source ~/.bashrc
```

### ปัญหา: Port 3000 ถูกใช้งาน
```bash
# ใช้ port อื่น
PORT=3001 npm start
```

### ปัญหา: npm install ช้า
```bash
# ลบ node_modules และติดตั้งใหม่
rm -rf node_modules package-lock.json
npm install
```

### ปัญหา: TypeScript errors
```bash
# ลบ cache และ rebuild
rm -rf node_modules/.cache
npm start
```

---

**Happy Coding! 🎨**
