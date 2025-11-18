# React Project Instructions# React Project Instructions# React Best Practices และ Project Structure# React Best Practices และ Project Structure



คู่มือสำหรับการพัฒนา React Application ด้วย Modern Best Practices



## 📚 เนื้อหาคู่มือสำหรับการพัฒนา React Application ด้วย Modern Best Practices



1. [Environment Setup](#-environment-setup)

2. [Project Structure Guidelines](#-project-structure-guidelines)

3. [Component Patterns](#-component-patterns)## 📚 เนื้อหาคู่มือสำหรับการพัฒนา React Application ด้วย Modern Best Practices และ GitHub Copilot

4. [State Management](#-state-management)

5. [API Integration](#-api-integration)

6. [Styling Approaches](#-styling-approaches)

7. [Testing Guidelines](#-testing-guidelines)1. [Environment Setup](#-environment-setup) - การตั้งค่า environment

8. [Code Quality](#-code-quality)

9. [GitHub Copilot Tips](#-github-copilot-tips)2. [Project Structure Guidelines](#-project-structure-guidelines) - แนวทางโครงสร้างโปรเจค



---3. [Component Patterns](#-component-patterns) - รูปแบบการเขียน components## 📚 สารบัญคู่มือสำหรับการพัฒนา React Application ด้วย Modern Best Practices และ GitHub Copilot



## 🛠 Environment Setup4. [State Management](#-state-management) - การจัดการ state



### Node.js with NVM5. [API Integration](#-api-integration) - การเชื่อมต่อ API



```bash6. [Styling Approaches](#-styling-approaches) - แนวทางการ styling

# ติดตั้ง NVM

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash7. [Testing Guidelines](#-testing-guidelines) - แนวทางการทดสอบ1. [Project Setup](#-project-setup) - การตั้งค่าโปรเจค



# ติดตั้ง Node.js v25.0.08. [Code Quality](#-code-quality) - มาตรฐานโค้ด

nvm install 25.0.0

nvm use 25.0.02. [Project Structure](#-project-structure) - โครงสร้างโปรเจค

nvm alias default 25.0.0

---

# ตรวจสอบ

node --version  # v25.0.03. [Development Environment](#-development-environment) - การตั้งค่า environment## 📚 สารบัญ

npm --version   # 10.9.0+

```## 🛠 Environment Setup



### Create Project4. [Component Patterns](#-component-patterns) - รูปแบบการเขียน components



```bash### Node.js with NVM

# React with TypeScript (แนะนำ)

npx create-react-app my-app --template typescript5. [State Management](#-state-management) - การจัดการ state



# หรือ React with JavaScript```bash

npx create-react-app my-app

```# ติดตั้ง NVM6. [Styling Approaches](#-styling-approaches) - วิธีการ styling



### Essential Dependenciescurl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash



```bash7. [API Integration](#-api-integration) - การเชื่อมต่อ API1. [Project Setup](#-project-setup) - การตั้งค่าโปรเจค### Getting Started

# Code quality

npm install -D eslint-config-prettier prettier# ติดตั้ง Node.js v25.0.0



# Testingnvm install 25.0.08. [Testing](#-testing) - การเขียน tests

npm install -D @testing-library/react @testing-library/jest-dom

nvm use 25.0.0

# State & API

npm install @tanstack/react-query axiosnvm alias default 25.0.09. [Copilot Best Practices](#-copilot-best-practices) - การใช้ Copilot2. [Project Structure](#-project-structure) - โครงสร้างโปรเจค1. **[Project Setup](#-project-setup)** - การตั้งค่าโปรเจคเริ่มต้น

```



---

# ตรวจสอบ

## 📁 Project Structure Guidelines

node --version  # v25.0.0

### แนวทางโครงสร้าง

npm --version   # 10.9.0+---3. [Development Environment](#-development-environment) - การตั้งค่า environment2. **[Project Structure](#-project-structure)** - โครงสร้างไฟล์และโฟลเดอร์

```

src/```

├── components/     # Shared/Reusable components

│   ├── ui/        # Basic UI elements

│   └── layout/    # Layout components

├── features/      # Feature-based modules### Create Project

│   └── [name]/    # Each feature

│       ├── components/## 🚀 Project Setup4. [Component Patterns](#-component-patterns) - รูปแบบการเขียน components3. **[Development Environment](#-development-environment)** - การตั้งค่า IDE และ tools

│       ├── hooks/

│       ├── services/```bash

│       └── types/

├── hooks/         # Global hooks# React with TypeScript (แนะนำ)

├── services/      # API services

├── types/         # TypeScript typesnpx create-react-app my-app --template typescript

├── utils/         # Utilities

├── styles/        # Global styles### Prerequisites5. [State Management](#-state-management) - การจัดการ state

└── __tests__/     # Test utilities

```# หรือ React with JavaScript



### Component Organizationnpx create-react-app my-app```bash



``````

ComponentName/

├── index.ts              # ExportNode.js v25.0.0 (managed by NVM)6. [Styling Approaches](#-styling-approaches) - วิธีการ styling### Core Technologies

├── ComponentName.tsx     # Implementation  

├── ComponentName.types.ts # Types (optional)### Essential Tools

├── ComponentName.test.tsx # Tests (optional)

└── ComponentName.css     # Styles (optional)npm >= 10.9.0

```

```bash

**หมายเหตุ:** ปรับโครงสร้างให้เหมาะกับโปรเจค

# Code qualityGit >= 2.34.07. [API Integration](#-api-integration) - การเชื่อมต่อ API4. **[Component Architecture](#-component-architecture)** - การออกแบบ components

---

npm install -D eslint-config-prettier prettier

## 🧩 Component Patterns

```

### Functional Component

# Testing

```typescript

interface Props {npm install -D @testing-library/react @testing-library/jest-dom8. [Testing](#-testing) - การเขียน tests5. **[State Management](#-state-management)** - การจัดการ state

  title: string;

  onAction?: () => void;

}

# State & API### NVM Setup

const Component: React.FC<Props> = ({ title, onAction }) => {

  return (npm install @tanstack/react-query axios

    <div>

      <h1>{title}</h1>``````bash9. [Copilot Best Practices](#-copilot-best-practices) - การใช้ Copilot6. **[Styling Guidelines](#-styling-guidelines)** - การใช้ CSS และ styling

      <button onClick={onAction}>Action</button>

    </div>

  );

};---# ติดตั้ง NVM

```



### Component with State

## 📁 Project Structure Guidelinescurl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash7. **[API Integration](#-api-integration)** - การเชื่อมต่อ API

```typescript

const Component: React.FC = () => {

  const [count, setCount] = useState(0);

  ### โครงสร้างแนะนำ

  return (

    <div>

      <p>Count: {count}</p>

      <button onClick={() => setCount(count + 1)}>+</button>```# ติดตั้ง Node v25.0.0---8. **[Testing Strategy](#-testing-strategy)** - การเขียน tests

    </div>

  );src/

};

```├── components/     # Shared/Reusable componentsnvm install 25.0.0



### Component with Effect│   ├── ui/        # Basic UI elements



```typescript│   └── layout/    # Layout componentsnvm use 25.0.0

const Component: React.FC = () => {

  const [data, setData] = useState(null);├── features/      # Feature-based modules

  

  useEffect(() => {│   └── [name]/    # Each featurenvm alias default 25.0.0

    fetchData().then(setData);

    return () => {│       ├── components/

      // Cleanup

    };│       ├── hooks/## 🚀 Project Setup### GitHub Copilot Integration

  }, []);

  │       ├── services/

  return <div>{/* Render */}</div>;

};│       └── types/# ตรวจสอบ version

```

├── hooks/         # Global hooks

### Best Practices

├── services/      # API servicesnode --version  # v25.0.09. **[Copilot Best Practices](#-github-copilot-best-practices)** - การใช้ Copilot อย่างมีประสิทธิภาพ

```typescript

// ✅ Clear props├── types/         # TypeScript types

interface ButtonProps {

  children: React.ReactNode;├── utils/         # Utilitiesnpm --version   # 10.9.0+

  variant?: 'primary' | 'secondary';

  onClick?: () => void;├── styles/        # Global styles

}

└── __tests__/     # Test utilities```### Prerequisites10. **[Code Generation Guidelines](#-code-generation-guidelines)** - แนวทางการสร้างโค้ด

// ✅ Default values

const Button: React.FC<ButtonProps> = ({ ```

  children, 

  variant = 'primary',

  onClick 

}) => { /* ... */ };### การจัดระเบียบ Component



// ✅ Clear conditionals### Create New Project```bash

if (loading) return <Loading />;

if (error) return <Error />;```

return <Content />;

ComponentName/```bash

// ❌ Avoid any type

interface Props {├── index.ts              # Export

  [key: string]: any;

}├── ComponentName.tsx     # Implementation  # React with TypeScriptNode.js v25.0.0 (managed by NVM)## 🚀 Project Setup



// ❌ Avoid complex ternary├── ComponentName.types.ts # Types (optional)

return loading ? <Loading /> : error ? <Error /> : <Content />;

```├── ComponentName.test.tsx # Tests (optional)npx create-react-app my-app --template typescript



---└── ComponentName.css     # Styles (optional)



## 🔄 State Management```cd my-appnpm >= 10.9.0



### Local State (useState)



```typescript**หมายเหตุ:** ปรับโครงสร้างให้เหมาะกับโปรเจค ไม่จำเป็นต้องทำตามทุกอย่าง

// Simple state

const [value, setValue] = useState('');



// Object state---# ติดตั้ง dependencies พื้นฐานGit >= 2.34.0### Prerequisites

const [form, setForm] = useState({ name: '', email: '' });

setForm(prev => ({ ...prev, name: 'New' }));

```

## 🧩 Component Patternsnpm install @tanstack/react-query axios

### Context API (Global State)



```typescript

// Create Context### 1. Functional Component with Propsnpm install -D @testing-library/react @testing-library/jest-dom``````bash

interface AppContextType {

  user: User | null;

  setUser: (user: User) => void;

}```typescriptnpm install -D eslint-config-prettier prettier



const AppContext = createContext<AppContextType | undefined>(undefined);interface Props {



// Provider  title: string;Node.js v25.0.0 (managed by NVM)

export const AppProvider: React.FC<PropsWithChildren> = ({ children }) => {

  const [user, setUser] = useState<User | null>(null);  onAction?: () => void;

  

  return (}# เลือก styling framework

    <AppContext.Provider value={{ user, setUser }}>

      {children}

    </AppContext.Provider>

  );const Component: React.FC<Props> = ({ title, onAction }) => {npm install tailwindcss         # Option 1### NVM Setupnpm >= 10.9.0

};

  return (

// Custom Hook

export const useApp = () => {    <div>npm install styled-components   # Option 2

  const context = useContext(AppContext);

  if (!context) throw new Error('Must be within AppProvider');      <h1>{title}</h1>

  return context;

};      <button onClick={onAction}>Action</button>npm install @emotion/react      # Option 3```bashGit >= 2.34.0

```

    </div>

### Server State (React Query)

  );```

```typescript

// Query Hook};

export const useData = () => {

  return useQuery({```# ติดตั้ง NVMVS Code (แนะนำ)

    queryKey: ['data'],

    queryFn: async () => {

      const res = await api.get('/data');

      return res.data;### 2. Component with State---

    }

  });

};

```typescriptcurl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash```

// Mutation Hook

export const useCreateData = () => {const Component: React.FC = () => {

  const queryClient = useQueryClient();

    const [count, setCount] = useState(0);## 📁 Project Structure

  return useMutation({

    mutationFn: async (newData) => {  

      const res = await api.post('/data', newData);

      return res.data;  return (

    },

    onSuccess: () => {    <div>

      queryClient.invalidateQueries({ queryKey: ['data'] });

    }      <p>Count: {count}</p>### Feature-Based Structure (แนะนำ)

  });

};      <button onClick={() => setCount(count + 1)}>Increment</button>

```

    </div># ติดตั้ง Node v25.0.0### Environment Setup with NVM

---

  );

## 🌐 API Integration

};```

### Axios Setup

```

```typescript

// services/api.tssrc/nvm install 25.0.0```bash

import axios from 'axios';

### 3. Component with Effect

const api = axios.create({

  baseURL: process.env.REACT_APP_API_URL,├── components/       # Shared components

  timeout: 10000

});```typescript



// Request interceptorconst Component: React.FC = () => {│   ├── ui/          # Button, Input, Modalnvm use 25.0.0# 1. ติดตั้ง NVM (หากยังไม่มี)

api.interceptors.request.use(config => {

  const token = localStorage.getItem('token');  const [data, setData] = useState(null);

  if (token) {

    config.headers.Authorization = `Bearer ${token}`;  │   └── layout/      # Header, Footer, Sidebar

  }

  return config;  useEffect(() => {

});

    // Fetch data or setup├── features/        # Feature modulesnvm alias default 25.0.0curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

// Response interceptor

api.interceptors.response.use(    fetchData().then(setData);

  response => response,

  error => {    │   └── [feature]/   # แต่ละ feature

    if (error.response?.status === 401) {

      // Handle unauthorized    // Cleanup

    }

    return Promise.reject(error);    return () => {│       ├── components/# restart terminal หรือ source ~/.zshrc

  }

);      // Cleanup logic



export default api;    };│       ├── hooks/

```

  }, []); // Dependencies

### Service Pattern

  │       ├── services/# ตรวจสอบ version

```typescript

// services/dataService.ts  return <div>{/* Render */}</div>;

export const dataService = {

  async getAll() {};│       ├── types/

    const { data } = await api.get('/items');

    return data;```

  },

  │       └── utils/node --version  # v25.0.0# 2. ติดตั้งและใช้ Node v25.0.0

  async getById(id: string) {

    const { data } = await api.get(`/items/${id}`);### Best Practices

    return data;

  },├── hooks/           # Global hooks

  

  async create(item: CreateDto) {```typescript

    const { data } = await api.post('/items', item);

    return data;// ✅ Props: ชัดเจน มี type├── services/        # Global services (API, auth)npm --version   # 10.9.0+nvm install 25.0.0

  },

  interface ButtonProps {

  async update(id: string, updates: UpdateDto) {

    const { data } = await api.patch(`/items/${id}`, updates);  children: React.ReactNode;├── types/           # Global types

    return data;

  },  variant?: 'primary' | 'secondary';

  

  async delete(id: string) {  onClick?: () => void;├── utils/           # Global utilities```nvm use 25.0.0

    await api.delete(`/items/${id}`);

  }}

};

```├── styles/          # Global styles



---// ✅ Destructuring: ใช้ default values



## 🎨 Styling Approachesconst Button: React.FC<ButtonProps> = ({ ├── __tests__/       # Test utilitiesnvm alias default 25.0.0



### CSS Modules  children, 



```css  variant = 'primary',├── App.tsx

/* Component.module.css */

.container { padding: 16px; }  onClick 

.title { font-size: 24px; }

```}) => { /* ... */ };└── index.tsx### Create New Project



```typescript

import styles from './Component.module.css';

// ✅ Conditional: อ่านง่าย```

const Component = () => (

  <div className={styles.container}>if (loading) return <Loading />;

    <h1 className={styles.title}>Title</h1>

  </div>if (error) return <Error />;```bash# 3. ตรวจสอบ version

);

```return <Content />;



### Styled Components### Component Organization



```typescript// ❌ หลีกเลี่ยง: Generic types

import styled from 'styled-components';

interface Props {```# React with TypeScriptnode --version  # v25.0.0

const Container = styled.div`

  padding: 16px;  [key: string]: any;

`;

}ComponentName/

const Component = () => (

  <Container>

    <h1>Title</h1>

  </Container>// ❌ หลีกเลี่ยง: Complex ternary├── index.ts              # Exportnpx create-react-app my-app --template typescriptnpm --version   # 10.9.0+

);

```return loading ? <Loading /> : error ? <Error /> : <Content />;



### Tailwind CSS```├── ComponentName.tsx     # Implementation



```typescript

const Component = () => (

  <div className="p-4">---├── ComponentName.types.ts # Typescd my-app```

    <h1 className="text-2xl font-bold">Title</h1>

  </div>

);

```## 🔄 State Management├── ComponentName.test.tsx # Tests



---



## 🧪 Testing Guidelines### Local State (useState)└── ComponentName.module.css # Styles (optional)



### Component Testing



```typescript```typescript```

import { render, screen, fireEvent } from '@testing-library/react';

// Simple state

describe('Component', () => {

  it('renders correctly', () => {const [value, setValue] = useState('');# ติดตั้ง dependencies พื้นฐาน### Quick Start

    render(<Component title="Test" />);

    expect(screen.getByText('Test')).toBeInTheDocument();

  });

// Object state**หมายเหตุ:** โครงสร้างนี้เป็นแนวทางแนะนำ สามารถปรับให้เหมาะกับโปรเจคได้

  it('handles click', () => {

    const onClick = jest.fn();const [form, setForm] = useState({ name: '', email: '' });

    render(<Component onClick={onClick} />);

    fireEvent.click(screen.getByRole('button'));npm install @tanstack/react-query axios```bash

    expect(onClick).toHaveBeenCalled();

  });// Update object state

});

```setForm(prev => ({ ...prev, name: 'New Name' }));---



### Hook Testing```



```typescriptnpm install -D @testing-library/react @testing-library/jest-dom# 1. สร้างโปรเจคใหม่

import { renderHook, act } from '@testing-library/react';

### Context API (Global State)

describe('useCustomHook', () => {

  it('updates value', () => {## 🛠 Development Environment

    const { result } = renderHook(() => useCustomHook());

    ```typescript

    act(() => {

      result.current.setValue('new');// สร้าง Contextnpm install -D eslint-config-prettier prettiernpx create-react-app my-app --template typescript

    });

    interface AppContextType {

    expect(result.current.value).toBe('new');

  });  user: User | null;### VS Code Extensions

});

```  setUser: (user: User) => void;



### E2E Testing (Cypress)}```jsoncd my-app



```typescript

describe('User Flow', () => {

  it('completes action', () => {const AppContext = createContext<AppContextType | undefined>(undefined);// .vscode/extensions.json

    cy.visit('/');

    cy.get('[data-testid="input"]').type('test');

    cy.get('[data-testid="submit"]').click();

    cy.contains('Success').should('be.visible');// Provider Component{# เลือก styling framework

  });

});export const AppProvider: React.FC<PropsWithChildren> = ({ children }) => {

```

  const [user, setUser] = useState<User | null>(null);  "recommendations": [

---

  

## ✨ Code Quality

  return (    "github.copilot",npm install tailwindcss         # Option 1# 2. ติดตั้ง essential packages

### TypeScript Best Practices

    <AppContext.Provider value={{ user, setUser }}>

```typescript

// Define types clearly      {children}    "github.copilot-chat",

interface User {

  id: string;    </AppContext.Provider>

  name: string;

  email: string;  );    "esbenp.prettier-vscode",npm install styled-components   # Option 2npm install @tanstack/react-query axios

}

};

// Use proper types for props

interface ComponentProps {    "bradlc.vscode-tailwindcss"

  user: User;

  onUpdate: (user: User) => void;// Custom Hook

}

export const useApp = () => {  ]npm install @emotion/react      # Option 3npm install -D @testing-library/react @testing-library/jest-dom

const Component: React.FC<ComponentProps> = ({ user, onUpdate }) => {

  // ...  const context = useContext(AppContext);

};

```  if (!context) throw new Error('Must be within AppProvider');}



### Naming Conventions  return context;



```typescript};``````npm install -D eslint-config-prettier prettier

// Components: PascalCase

const UserProfile = () => {};



// Functions: camelCase// ใช้งาน

const handleSubmit = () => {};

const Component = () => {

// Constants: UPPER_SNAKE_CASE

const API_URL = 'https://api.example.com';  const { user, setUser } = useApp();### VS Code Settings



// Hooks: use + PascalCase  // ...

const useUserData = () => {};

};```json

// Types: PascalCase

interface UserData {}```

type UserStatus = 'active' | 'inactive';

```// .vscode/settings.json---# 3. เลือกติดตั้ง styling framework



### Performance Optimization### Server State (React Query)



```typescript{

// React.memo

export const ExpensiveComponent = React.memo(({ data }) => {```typescript

  // ...

});// Custom Hook  "editor.formatOnSave": true,npm install tailwindcss     # หรือ



// useMemoexport const useData = () => {

const sorted = useMemo(() => {

  return data.sort((a, b) => a.value - b.value);  return useQuery({  "editor.defaultFormatter": "esbenp.prettier-vscode",

}, [data]);

    queryKey: ['data'],

// useCallback

const handleClick = useCallback(() => {    queryFn: async () => {  "editor.codeActionsOnSave": {## 📁 Project Structurenpm install styled-components   # หรือ

  // ...

}, [deps]);      const res = await api.get('/data');



// Code splitting      return res.data;    "source.fixAll.eslint": true,

const LazyComponent = React.lazy(() => import('./LazyComponent'));

```    }



### Clean Code Principles  });    "source.organizeImports": truenpm install @emotion/react @emotion/styled



```typescript};

// ✅ Clear and simple

const isValid = (value: string) => value.length > 0;  }



// ✅ Descriptive names// Mutation Hook

const fetchUserData = async (userId: string) => { /* ... */ };

export const useCreateData = () => {}### Feature-Based Structure (แนะนำ)

// ✅ Small functions

const validateEmail = (email: string) => {  const queryClient = useQueryClient();

  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);

};  ```



// ❌ Avoid generic names  return useMutation({

const doSomething = (data: any) => { /* ... */ };

    mutationFn: async (newData) => {# 4. เริ่มต้นพัฒนา

// ❌ Avoid large functions

const handleEverything = () => {      const res = await api.post('/data', newData);

  // 100+ lines

};      return res.data;### Package Scripts

```

    },

---

    onSuccess: () => {```json```npm start

## 🤖 GitHub Copilot Tips

      queryClient.invalidateQueries({ queryKey: ['data'] });

### Write Clear Comments

    }{

```typescript

// ✅ Good - descriptive  });

// Create a reusable card component with hover effect

// Props: title, description, image, onClick};  "scripts": {src/```

const Card: React.FC = () => {

  // Copilot generates good code

};

// ใช้งาน    "start": "react-scripts start",

// ❌ Bad - vague

// cardconst Component = () => {

const Card = () => {};

```  const { data, isLoading, error } = useData();    "build": "react-scripts build",├── components/       # Shared components



### Use Meaningful Names  const createMutation = useCreateData();



```typescript      "test": "react-scripts test",

// ✅ Good

const isUserAuthenticated = true;  if (isLoading) return <Loading />;

const userProfileData = [];

const handleFormSubmit = () => {};  if (error) return <Error />;    "lint": "eslint src --ext .ts,.tsx",│   ├── ui/          # Button, Input, Modal## 📁 Project Structure



// ❌ Bad  

const flag = true;

const data = [];  return <div>{/* Render data */}</div>;    "format": "prettier --write src/**/*.{ts,tsx}"

const fn = () => {};

```};



### Define Types First```  }│   └── layout/      # Header, Footer, Sidebar



```typescript

// Define types first

interface User {---}

  id: string;

  name: string;

  email: string;

}## 🌐 API Integration```├── features/        # Feature modules### โครงสร้างแบบ Feature-Based



// Copilot uses User type

const UserList: React.FC = () => {

  const users: User[] = [];### Axios Setup

  // ...

};

```

```typescript---│   └── [feature]/   # แต่ละ feature

### Comment-Driven Development

// services/api.ts

```typescript

const useFormValidation = () => {import axios from 'axios';

  // State for form values

  // State for errors

  // State for touched fields

  const api = axios.create({## 🧩 Component Patterns│       ├── components/#### หลักการจัดโครงสร้าง

  // Function to validate single field

  // Function to validate all fields  baseURL: process.env.REACT_APP_API_URL,

  // Function to reset form

    timeout: 10000

  // Return form state and functions

};});

// Copilot implements based on comments

```### 1. Presentation Component│       ├── hooks/```



---// Request interceptor



## 📋 Development Checklistapi.interceptors.request.use(config => {```typescript



### Component Development  const token = localStorage.getItem('token');

- [ ] TypeScript types defined

- [ ] Props with defaults  if (token) {// รับ props และแสดงผล ไม่มี business logic│       ├── services/src/

- [ ] Loading/Error states

- [ ] Accessible (ARIA)    config.headers.Authorization = `Bearer ${token}`;

- [ ] Responsive

- [ ] Tests written  }interface ItemProps {



### Code Quality  return config;

- [ ] ESLint passing

- [ ] Prettier formatted});  title: string;│       ├── types/├── components/          # Shared/Reusable components

- [ ] No console.log

- [ ] No unused imports

- [ ] Error handling

- [ ] Meaningful comments// Response interceptor  completed: boolean;



### Performanceapi.interceptors.response.use(

- [ ] React.memo used

- [ ] useMemo/useCallback  response => response,  onToggle: () => void;│       └── utils/│   ├── ui/             # Basic UI components (Button, Input, Modal)

- [ ] Proper dependencies

- [ ] No unnecessary re-renders  error => {



### Testing    // Handle errors}

- [ ] Unit tests

- [ ] Integration tests    return Promise.reject(error);

- [ ] E2E critical paths

  }├── hooks/           # Global hooks│   └── layout/         # Layout components (Header, Footer, Sidebar)

---

);

## 💡 Best Practices Summary

const Item: React.FC<ItemProps> = ({ title, completed, onToggle }) => (

### Do's ✅

- ใช้ TypeScriptexport default api;

- เขียน comments ชัดเจน

- แยก component เล็กๆ```  <div>├── services/        # Global services (API, auth)├── features/           # Feature-specific code

- ใช้ custom hooks

- เขียน tests

- จัดการ errors

- Optimize performance### Service Pattern    <input type="checkbox" checked={completed} onChange={onToggle} />



### Don'ts ❌

- หลีกเลี่ยง any type

- อย่าเขียน component ใหญ่```typescript    <span>{title}</span>├── types/           # Global types│   └── [feature-name]/ # แต่ละ feature (เช่น auth, dashboard, profile)

- อย่าใช้ inline styles มาก

- อย่า mutate state โดยตรง// services/dataService.ts

- อย่าลืม dependency arrays

import api from './api';  </div>

---



## 🔗 Resources

export const dataService = {);├── utils/           # Global utilities│       ├── components/ # Components เฉพาะ feature

- [React Docs](https://react.dev)

- [TypeScript Handbook](https://www.typescriptlang.org/docs/)  async getAll() {

- [React Query](https://tanstack.com/query/latest)

- [Testing Library](https://testing-library.com/)    const { data } = await api.get('/items');```



---    return data;



**Happy Coding! 🚀**  },├── styles/          # Global styles│       ├── hooks/      # Custom hooks เฉพาะ feature  


  

  async getById(id: string) {### 2. Container Component

    const { data } = await api.get(`/items/${id}`);

    return data;```typescript├── __tests__/       # Test utilities│       ├── services/   # API calls เฉพาะ feature

  },

  // จัดการ logic และ state

  async create(item: CreateItemDto) {

    const { data } = await api.post('/items', item);const ItemList: React.FC = () => {├── App.tsx│       ├── types/      # TypeScript types เฉพาะ feature

    return data;

  },  const { data, isLoading } = useData();

  

  async update(id: string, updates: UpdateItemDto) {  const { toggle } = useActions();└── index.tsx│       └── utils/      # Utilities เฉพาะ feature

    const { data } = await api.patch(`/items/${id}`, updates);

    return data;

  },

    if (isLoading) return <Loading />;```├── hooks/              # Global custom hooks

  async delete(id: string) {

    await api.delete(`/items/${id}`);

  }

};  return (├── services/           # Global services (API client, auth, storage)

```

    <div>

### Error Handling

      {data.map(item => (### Component Organization├── types/              # Global TypeScript types

```typescript

// hooks/useApiError.ts        <Item 

export const useApiError = () => {

  const [error, setError] = useState<string | null>(null);          key={item.id}```├── utils/              # Global utilities (constants, helpers, validators)



  const handleError = (err: any) => {          title={item.title}

    const message = err.response?.data?.message || 

                   err.message ||           completed={item.completed}ComponentName/├── styles/             # Global styles

                   'An error occurred';

    setError(message);          onToggle={() => toggle(item.id)}

  };

        />├── index.ts              # Export├── __tests__/          # Global test utilities

  const clearError = () => setError(null);

      ))}

  return { error, handleError, clearError };

};    </div>├── ComponentName.tsx     # Implementation├── App.tsx

```

  );

---

};├── ComponentName.types.ts # Types└── index.tsx

## 🎨 Styling Approaches

```

### 1. CSS Modules

├── ComponentName.test.tsx # Tests```

```css

/* Component.module.css */### 3. Props Best Practices

.container {

  padding: 16px;```typescript└── ComponentName.module.css # Styles (optional)

}

// ✅ Good - ชัดเจน มี type

.title {

  font-size: 24px;interface ButtonProps {```#### โครงสร้าง Component แต่ละตัว

  font-weight: bold;

}  children: React.ReactNode;

```

  variant?: 'primary' | 'secondary';```

```typescript

import styles from './Component.module.css';  onClick?: () => void;



const Component = () => (}**หมายเหตุ:** โครงสร้างนี้เป็นแนวทางแนะนำ สามารถปรับให้เหมาะกับโปรเจคได้ComponentName/

  <div className={styles.container}>

    <h1 className={styles.title}>Title</h1>

  </div>

);// ❌ Bad - ไม่ชัดเจน├── index.ts           # Export หลัก

```

interface ButtonProps {

### 2. Styled Components

  [key: string]: any;---├── ComponentName.tsx  # Component implementation

```typescript

import styled from 'styled-components';}



const Container = styled.div````├── ComponentName.types.ts # TypeScript interfaces

  padding: 16px;

`;



const Title = styled.h1`### 4. Conditional Rendering## 🛠 Development Environment├── ComponentName.test.tsx # Unit tests

  font-size: 24px;

  font-weight: bold;```typescript

`;

// ✅ Good - อ่านง่าย├── ComponentName.stories.tsx # Storybook (ถ้ามี)

const Component = () => (

  <Container>if (isLoading) return <Loading />;

    <Title>Title</Title>

  </Container>if (error) return <Error />;### VS Code Extensions└── ComponentName.module.css  # Styles (ถ้าใช้ CSS Modules)

);

```if (!data) return <Empty />;



### 3. Tailwind CSS```json```



```typescriptreturn <Content data={data} />;

const Component = () => (

  <div className="p-4">// .vscode/extensions.json

    <h1 className="text-2xl font-bold">Title</h1>

  </div>// ❌ Bad - ซับซ้อน

);

```return isLoading ? <Loading /> : error ? <Error /> : !data ? <Empty /> : <Content />;{### Component Template Example



**เลือกวิธีที่เหมาะกับโปรเจค**```



---  "recommendations": [```typescript



## 🧪 Testing Guidelines---



### Component Testing    "github.copilot",// components/ui/Button/Button.tsx



```typescript## 🔄 State Management

import { render, screen, fireEvent } from '@testing-library/react';

    "github.copilot-chat",import React from 'react';

describe('Component', () => {

  it('renders correctly', () => {### Local State (useState)

    render(<Component title="Test" />);

    expect(screen.getByText('Test')).toBeInTheDocument();```typescript    "esbenp.prettier-vscode",import { ButtonProps } from './Button.types';

  });

const Form: React.FC = () => {

  it('handles click', () => {

    const handleClick = jest.fn();  const [form, setForm] = useState({ name: '', email: '' });    "bradlc.vscode-tailwindcss"

    render(<Component onClick={handleClick} />);

      const [errors, setErrors] = useState({});

    fireEvent.click(screen.getByRole('button'));

    expect(handleClick).toHaveBeenCalled();  ]export const Button: React.FC<ButtonProps> = ({

  });

});  const handleSubmit = (e: React.FormEvent) => {

```

    e.preventDefault();}  children,

### Hook Testing

    // Validate and submit

```typescript

import { renderHook, act } from '@testing-library/react';  };```  variant = 'primary',



describe('useCustomHook', () => {

  it('updates value', () => {

    const { result } = renderHook(() => useCustomHook());  return (  size = 'medium',

    

    act(() => {    <form onSubmit={handleSubmit}>

      result.current.setValue('new value');

    });      <input ### VS Code Settings  ...props

    

    expect(result.current.value).toBe('new value');        value={form.name}

  });

});        onChange={e => setForm(prev => ({ ...prev, name: e.target.value }))}```json}) => {

```

      />

### E2E Testing (Cypress)

    </form>// .vscode/settings.json  return (

```typescript

describe('User Flow', () => {  );

  it('completes action', () => {

    cy.visit('/');};{    <button

    cy.get('[data-testid="input"]').type('test');

    cy.get('[data-testid="submit"]').click();```

    cy.contains('Success').should('be.visible');

  });  "editor.formatOnSave": true,      className={`btn btn--${variant} btn--${size}`}

});

```### Context API (Global State)



---```typescript  "editor.defaultFormatter": "esbenp.prettier-vscode",      {...props}



## ✨ Code Quality// สร้าง context



### TypeScriptinterface AppContextType {  "editor.codeActionsOnSave": {    >



```typescript  user: User | null;

// ใช้ TypeScript สำหรับ type safety

interface User {  setUser: (user: User) => void;    "source.fixAll.eslint": true,      {children}

  id: string;

  name: string;}

  email: string;

}    "source.organizeImports": true    </button>



// Define props clearlyconst AppContext = createContext<AppContextType | undefined>(undefined);

interface ComponentProps {

  user: User;  }  );

  onUpdate: (user: User) => void;

}// Provider



// Use proper typesexport const AppProvider: React.FC<{ children: ReactNode }> = ({ children }) => {}};

const Component: React.FC<ComponentProps> = ({ user, onUpdate }) => {

  // ...  const [user, setUser] = useState<User | null>(null);

};

```  ``````



### Naming Conventions  return (



```typescript    <AppContext.Provider value={{ user, setUser }}>

// Components: PascalCase

const UserProfile = () => {};      {children}



// Functions: camelCase    </AppContext.Provider>### Package Scripts## 🛠 Development Environment

const handleSubmit = () => {};

  );

// Constants: UPPER_SNAKE_CASE

const API_URL = 'https://api.example.com';};```json



// Hooks: use + PascalCase

const useUserData = () => {};

// Hook{### VS Code Extensions (แนะนำ)

// Types/Interfaces: PascalCase

interface UserData {}export const useApp = () => {

type UserStatus = 'active' | 'inactive';

```  const context = useContext(AppContext);  "scripts": {```json



### File Organization  if (!context) throw new Error('useApp must be within AppProvider');



```  return context;    "start": "react-scripts start",// .vscode/extensions.json

feature/

├── components/      # UI components};

├── hooks/          # Custom hooks

│   └── useFeature.ts```    "build": "react-scripts build",{

├── services/       # API calls

│   └── featureService.ts

├── types/          # TypeScript types

│   └── feature.types.ts### React Query (Server State)    "test": "react-scripts test",  "recommendations": [

└── utils/          # Helper functions

    └── featureHelpers.ts```typescript

```

// Service    "lint": "eslint src --ext .ts,.tsx",    "github.copilot",

### Performance

export const apiService = {

```typescript

// 1. React.memo - Expensive components  getAll: async () => {    "format": "prettier --write src/**/*.{ts,tsx}"    "github.copilot-chat",

export const ExpensiveComponent = React.memo(({ data }) => {

  // Component logic    const res = await api.get('/items');

});

    return res.data;  }    "bradlc.vscode-tailwindcss",

// 2. useMemo - Expensive calculations

const sortedData = useMemo(() => {  },

  return data.sort((a, b) => a.value - b.value);

}, [data]);  create: async (item: CreateItem) => {}    "esbenp.prettier-vscode",



// 3. useCallback - Event handlers    const res = await api.post('/items', item);

const handleClick = useCallback(() => {

  // Handler logic    return res.data;```    "ms-vscode.vscode-typescript-next",

}, [dependencies]);

  }

// 4. Code splitting

const LazyComponent = React.lazy(() => import('./LazyComponent'));};    "formulahendry.auto-rename-tag",

```



### Clean Code

// Hook---    "christian-kohler.path-intellisense"

```typescript

// ✅ Clear and simpleexport const useItems = () => {

const isValid = (value: string) => value.length > 0;

  return useQuery({  ]

if (isValid(input)) {

  submit(input);    queryKey: ['items'],

}

    queryFn: apiService.getAll,## 🧩 Component Patterns}

// ✅ Descriptive names

const fetchUserData = async (userId: string) => {    staleTime: 5 * 60 * 1000

  // ...

};  });```



// ✅ Small functions};

const validateEmail = (email: string) => {

  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);### 1. Presentation Component

};

export const useCreateItem = () => {

// ❌ หลีกเลี่ยง: Generic names

const doSomething = (data: any) => {  const queryClient = useQueryClient();```typescript### VS Code Settings

  // ...

};  



// ❌ หลีกเลี่ยง: Large functions  return useMutation({// รับ props และแสดงผล ไม่มี business logic```json

const handleEverything = () => {

  // 100+ lines of code    mutationFn: apiService.create,

};

```    onSuccess: () => {interface ItemProps {// .vscode/settings.json



---      queryClient.invalidateQueries({ queryKey: ['items'] });



## 📋 Development Checklist    }  title: string;{



### Component Development  });

- [ ] TypeScript types defined

- [ ] Props destructured with defaults};  completed: boolean;  "typescript.preferences.importModuleSpecifier": "relative",

- [ ] Loading states handled

- [ ] Error states handled```

- [ ] Accessible (ARIA attributes)

- [ ] Responsive design  onToggle: () => void;  "editor.formatOnSave": true,

- [ ] Tests written

---

### Code Quality

- [ ] ESLint passing}  "editor.defaultFormatter": "esbenp.prettier-vscode",

- [ ] Prettier formatted

- [ ] No console.log## 🎨 Styling Approaches

- [ ] No unused imports

- [ ] Proper error handling  "editor.codeActionsOnSave": {

- [ ] Comments for complex logic

### 1. CSS Modules

### Performance

- [ ] React.memo used appropriately```cssconst Item: React.FC<ItemProps> = ({ title, completed, onToggle }) => (    "source.fixAll.eslint": true,

- [ ] useMemo for expensive calculations

- [ ] useCallback for handlers/* Component.module.css */

- [ ] Proper dependency arrays

- [ ] No unnecessary re-renders.container {  <div>    "source.organizeImports": true



### Testing  padding: 16px;

- [ ] Unit tests for components

- [ ] Unit tests for hooks  background: white;    <input type="checkbox" checked={completed} onChange={onToggle} />  },

- [ ] Integration tests for features

- [ ] E2E tests for critical paths}



---    <span>{title}</span>  "emmet.includeLanguages": {



## 🚀 GitHub Copilot Tips.title {



### เขียน Comments ที่ดี  font-size: 24px;  </div>    "typescript": "html",



```typescript  font-weight: bold;

// ✅ Good - Copilot เข้าใจง่าย

// Create a reusable card component with hover effect});    "typescriptreact": "html"

// Props: title, description, image, onClick

const Card: React.FC = () => {```

  // Copilot จะ generate code ที่ดี

};```  },



// ❌ Bad```typescript

// card

const Card = () => {};import styles from './Component.module.css';  "github.copilot.enable": {

```



### ใช้ชื่อที่สื่อความหมาย

const Component = () => (### 2. Container Component    "*": true,

```typescript

// ✅ Good  <div className={styles.container}>

const isUserAuthenticated = true;

const userProfileData = [];    <h1 className={styles.title}>Title</h1>```typescript    "typescript": true,

const handleFormSubmit = () => {};

  </div>

// ❌ Bad

const flag = true;);// จัดการ logic และ state    "typescriptreact": true

const data = [];

const fn = () => {};```

```

const ItemList: React.FC = () => {  }

### สร้าง Types ก่อน

### 2. Styled Components

```typescript

// Define types first - ช่วย Copilot```typescript  const { data, isLoading } = useData();}

interface User {

  id: string;import styled from 'styled-components';

  name: string;

  email: string;  const { toggle } = useActions();```

}

const Container = styled.div`

// Copilot จะใช้ User type ในการ generate

const UserList: React.FC = () => {  padding: 16px;

  const users: User[] = [];

  // ...  background: white;

};

````;  if (isLoading) return <Loading />;### Package.json Scripts



### Comment-Driven Development



```typescriptconst Title = styled.h1````json

const useFormValidation = () => {

  // State for form values  font-size: 24px;

  // State for errors

  // State for touched fields  font-weight: bold;  return ({

  

  // Function to validate single field`;

  // Function to validate all fields

  // Function to reset form    <div>  "scripts": {

  

  // Return form state and functionsconst Component = () => (

};

// Copilot จะ implement ตาม comments  <Container>      {data.map(item => (    "start": "react-scripts start",

```

    <Title>Title</Title>

---

  </Container>        <Item     "build": "react-scripts build",

## 💡 Best Practices Summary

);

### Do's ✅

- ใช้ TypeScript```          key={item.id}    "test": "react-scripts test",

- เขียน comments ที่ชัดเจน

- แยก component ให้เล็ก

- ใช้ custom hooks

- เขียน tests### 3. Tailwind CSS          title={item.title}    "test:coverage": "react-scripts test --coverage --watchAll=false",

- จัดการ errors

- Optimize performance```typescript



### Don'ts ❌const Component = () => (          completed={item.completed}    "test:ci": "react-scripts test --ci --coverage --watchAll=false",

- หลีกเลี่ยง any type

- อย่าเขียน component ใหญ่เกินไป  <div className="p-4 bg-white">

- อย่าใช้ inline styles มากเกินไป

- อย่าทำ premature optimization    <h1 className="text-2xl font-bold">Title</h1>          onToggle={() => toggle(item.id)}    "lint": "eslint src --ext .ts,.tsx",

- อย่า mutate state โดยตรง

- อย่าลืม dependency arrays  </div>



---);        />    "lint:fix": "eslint src --ext .ts,.tsx --fix",



## 🔗 Useful Resources```



### Documentation      ))}    "format": "prettier --write src/**/*.{ts,tsx,css,md}",

- [React Official Docs](https://react.dev)

- [TypeScript Handbook](https://www.typescriptlang.org/docs/)**เลือกตามความเหมาะสมของโปรเจค**

- [React Query Docs](https://tanstack.com/query/latest)

    </div>    "type-check": "tsc --noEmit",

### Tools

- [React DevTools](https://react.dev/learn/react-developer-tools)---

- [ESLint](https://eslint.org/)

- [Prettier](https://prettier.io/)  );    "storybook": "start-storybook -p 6006",



---## 🌐 API Integration



**Happy Coding with React! 🚀**};    "build-storybook": "build-storybook"


### Axios Setup

```typescript```  }

// services/api.ts

import axios from 'axios';}



const api = axios.create({### 3. Props Best Practices```

  baseURL: process.env.REACT_APP_API_URL || 'http://localhost:3001',

  timeout: 10000```typescript

});

// ✅ Good - ชัดเจน มี type## 🧩 Component Architecture

// Interceptors

api.interceptors.request.use(config => {interface ButtonProps {

  const token = localStorage.getItem('token');

  if (token) config.headers.Authorization = `Bearer ${token}`;  children: React.ReactNode;### Component Types และ Patterns

  return config;

});  variant?: 'primary' | 'secondary';



api.interceptors.response.use(  onClick?: () => void;#### 1. Presentation Components (Dumb Components)

  response => response,

  error => {}```typescript

    if (error.response?.status === 401) {

      // Handle unauthorized// Pure UI components, no business logic

    }

    return Promise.reject(error);// ❌ Bad - ไม่ชัดเจนinterface ItemProps {

  }

);interface ButtonProps {  item: DataType;



export default api;  [key: string]: any;  onAction: (id: string) => void;

```

}}

### API Service Pattern

```typescript```

// services/itemService.ts

import api from './api';const ListItem: React.FC<ItemProps> = ({ item, onAction }) => {



export const itemService = {### 4. Conditional Rendering  return (

  getAll: async () => {

    const { data } = await api.get('/items');```typescript    <div className="list-item">

    return data;

  },// ✅ Good - อ่านง่าย      <span>{item.title}</span>

  

  getById: async (id: string) => {if (isLoading) return <Loading />;      <button onClick={() => onAction(item.id)}>Action</button>

    const { data } = await api.get(`/items/${id}`);

    return data;if (error) return <Error />;    </div>

  },

  if (!data) return <Empty />;  );

  create: async (item: CreateItem) => {

    const { data } = await api.post('/items', item);};

    return data;

  },return <Content data={data} />;```

  

  update: async (id: string, updates: Partial<Item>) => {

    const { data } = await api.patch(`/items/${id}`, updates);

    return data;// ❌ Bad - ซับซ้อน#### 2. Container Components (Smart Components)

  },

  return isLoading ? <Loading /> : error ? <Error /> : !data ? <Empty /> : <Content />;```typescript

  delete: async (id: string) => {

    await api.delete(`/items/${id}`);```// Business logic and state management

  }

};const ListContainer: React.FC = () => {

```

---  const { data, isLoading, error } = useData();

### Error Handling

```typescript  const { performAction } = useActions();

// hooks/useApiError.ts

export const useApiError = () => {## 🔄 State Management

  const [error, setError] = useState<string | null>(null);

  if (isLoading) return <LoadingSpinner />;

  const handleError = (err: any) => {

    const message = err.response?.data?.message || err.message || 'Error occurred';### Local State (useState)  if (error) return <ErrorMessage error={error} />;

    setError(message);

  };```typescript



  const clearError = () => setError(null);const Form: React.FC = () => {  return (



  return { error, handleError, clearError };  const [form, setForm] = useState({ name: '', email: '' });    <div className="list-container">

};

```  const [errors, setErrors] = useState({});      {data.map(item => (



---        <ListItem



## 🧪 Testing  const handleSubmit = (e: React.FormEvent) => {          key={item.id}



### Component Testing    e.preventDefault();          item={item}

```typescript

// Component.test.tsx    // Validate and submit          onAction={performAction}

import { render, screen, fireEvent } from '@testing-library/react';

import { Button } from './Button';  };        />



describe('Button', () => {      ))}

  it('renders correctly', () => {

    render(<Button>Click me</Button>);  return (    </div>

    expect(screen.getByText('Click me')).toBeInTheDocument();

  });    <form onSubmit={handleSubmit}>  );



  it('calls onClick when clicked', () => {      <input };

    const handleClick = jest.fn();

    render(<Button onClick={handleClick}>Click me</Button>);        value={form.name}```

    

    fireEvent.click(screen.getByText('Click me'));        onChange={e => setForm(prev => ({ ...prev, name: e.target.value }))}

    expect(handleClick).toHaveBeenCalledTimes(1);

  });      />#### 3. Custom Hooks Pattern

});

```    </form>```typescript



### Hook Testing  );// hooks/useData.ts

```typescript

// useCustomHook.test.ts};export const useData = () => {

import { renderHook, act } from '@testing-library/react';

import { useCounter } from './useCounter';```  return useQuery({



describe('useCounter', () => {    queryKey: ['data'],

  it('increments counter', () => {

    const { result } = renderHook(() => useCounter());### Context API (Global State)    queryFn: apiService.getAll,

    

    act(() => {```typescript    staleTime: 5 * 60 * 1000,

      result.current.increment();

    });// สร้าง context  });

    

    expect(result.current.count).toBe(1);interface AppContextType {};

  });

});  user: User | null;

```

  setUser: (user: User) => void;export const useActions = () => {

### E2E Testing (Cypress)

```typescript}  const queryClient = useQueryClient();

// cypress/e2e/app.cy.ts

describe('App Flow', () => {

  it('creates new item', () => {

    cy.visit('/');const AppContext = createContext<AppContextType | undefined>(undefined);  const performAction = useMutation({

    cy.get('[data-testid="add-button"]').click();

    cy.get('[data-testid="title-input"]').type('New Item');    mutationFn: apiService.action,

    cy.get('[data-testid="submit-button"]').click();

    cy.contains('New Item').should('be.visible');// Provider    onSuccess: () => {

  });

});export const AppProvider: React.FC<{ children: ReactNode }> = ({ children }) => {      queryClient.invalidateQueries({ queryKey: ['data'] });

```

  const [user, setUser] = useState<User | null>(null);    },

---

    });

## 🤖 Copilot Best Practices

  return (

### 1. เขียน Comments ให้ชัดเจน

```typescript    <AppContext.Provider value={{ user, setUser }}>  return { performAction: performAction.mutate };

// ✅ Good - Copilot เข้าใจง่าย

// Create a button component with primary and secondary variants      {children}};

// Include loading state and disabled state

// Add proper TypeScript types    </AppContext.Provider>```

const Button: React.FC = () => {

  // Copilot จะ generate code ที่ดี  );

};

};### Component Best Practices

// ❌ Bad

// button

const Button = () => {};

```// Hook#### 1. Props Interface Design



### 2. ใช้ชื่อตัวแปรที่สื่อความหมายexport const useApp = () => {```typescript

```typescript

// ✅ Good  const context = useContext(AppContext);// ✅ Good: Clear, specific props

const isLoading = useState(false);

const userList = useState<User[]>([]);  if (!context) throw new Error('useApp must be within AppProvider');interface ButtonProps {

const handleSubmit = () => {};

  return context;  children: React.ReactNode;

// ❌ Bad  

const flag = useState(false);};  variant?: 'primary' | 'secondary' | 'danger';

const data = useState([]);

const fn = () => {};```  size?: 'small' | 'medium' | 'large';

```

  disabled?: boolean;

### 3. สร้าง Types ก่อน

```typescript### React Query (Server State)  onClick?: (event: React.MouseEvent<HTMLButtonElement>) => void;

// Define types first - ช่วย Copilot เข้าใจ context

interface User {```typescript}

  id: string;

  name: string;// Service

  email: string;

}export const apiService = {// ❌ Bad: Generic props



// Copilot จะ generate code ที่ใช้ User type  getAll: async () => {interface ButtonProps {

const UserList: React.FC = () => {

  // Copilot รู้ว่า users เป็น User[]    const res = await api.get('/items');  [key: string]: any;

  const users = useUsers();

};    return res.data;}

```

  },```

### 4. ใช้ Method Signatures

```typescript  create: async (item: CreateItem) => {

// เขียน signature ก่อน ให้ Copilot implement

class UserService {    const res = await api.post('/items', item);#### 2. Default Props และ Destructuring

  // Get all users from API

  async getAll(): Promise<User[]> {    return res.data;```typescript

    // Copilot จะ implement

  }  }// ✅ Modern way with default parameters



  // Create new user with validation};const Button: React.FC<ButtonProps> = ({

  async create(user: CreateUserDto): Promise<User> {

    // Copilot จะ implement  children,

  }

}// Hook  variant = 'primary',

```

export const useItems = () => {  size = 'medium',

### 5. Comment-Driven Development

```typescript  return useQuery({  disabled = false,

const useDataFilters = () => {

  // State for filter type (all, active, completed)    queryKey: ['items'],  onClick,

  // State for search term with debounce

  // State for sort order    queryFn: apiService.getAll,  ...rest

  

  // Function to apply filters    staleTime: 5 * 60 * 1000}) => {

  // Function to clear filters

  // Function to get filter count  });  // Component logic

  

  // Return filtered data and controls};};

};

// Copilot จะ generate implementation```

```

export const useCreateItem = () => {

### 6. ใช้ Consistent Patterns

```typescript  const queryClient = useQueryClient();#### 3. Conditional Rendering

// ใช้ pattern เดียวกันทั้งโปรเจค

// Copilot จะเรียนรู้และ suggest ตาม pattern  ```typescript



// Pattern: Feature hooks  return useMutation({// ✅ Good: Clear conditions

export const useItems = () => { /* ... */ };

export const useUsers = () => { /* ... */ };    mutationFn: apiService.create,const DataList: React.FC<Props> = ({ items, isLoading, error }) => {



// Pattern: Feature services      onSuccess: () => {  if (isLoading) return <LoadingSpinner />;

export const itemService = { /* ... */ };

export const userService = { /* ... */ };      queryClient.invalidateQueries({ queryKey: ['items'] });  if (error) return <ErrorMessage message={error.message} />;

```

    }  if (items.length === 0) return <EmptyState />;

---

  });

## 📋 Code Quality Checklist

};  return (

### Component

- [ ] TypeScript interfaces defined```    <ul>

- [ ] Props destructured

- [ ] Default values provided      {items.map(item => (

- [ ] Proper event handlers

- [ ] Loading states handled---        <ListItem key={item.id} item={item} />

- [ ] Error states handled

      ))}

### Performance

- [ ] React.memo ใช้กับ expensive components## 🎨 Styling Approaches    </ul>

- [ ] useMemo ใช้กับ expensive calculations

- [ ] useCallback ใช้กับ event handlers  );

- [ ] Dependency arrays ถูกต้อง

### 1. CSS Modules};

### Testing

- [ ] Unit tests สำหรับ components```css

- [ ] Unit tests สำหรับ hooks

- [ ] Integration tests สำหรับ features/* Component.module.css */// ❌ Bad: Complex ternary operators

- [ ] E2E tests สำหรับ critical flows

.container {const DataList: React.FC<Props> = ({ items, isLoading, error }) => (

### Code Style

- [ ] ESLint ผ่าน  padding: 16px;  <div>

- [ ] Prettier formatted

- [ ] Naming conventions consistent  background: white;    {isLoading ? <LoadingSpinner /> : error ? <ErrorMessage /> : items.length === 0 ? <EmptyState /> : items.map(...)}

- [ ] Comments เพียงพอ

}  </div>

---

);

## 💡 Tips สำหรับความสำเร็จ

.title {```

1. **ใช้ TypeScript** - ช่วยให้ Copilot suggest ได้ดีขึ้น

2. **เขียน Comments** - อธิบายว่าต้องการอะไร  font-size: 24px;

3. **Consistent Naming** - ใช้ชื่อที่สื่อความหมาย

4. **Define Types First** - สร้าง interfaces ก่อนเขียนโค้ด  font-weight: bold;## 🔄 State Management

5. **Test Early** - เขียน tests ตั้งแต่เริ่มต้น

6. **Keep Components Small** - แยก component ให้เล็กและชัดเจน}



---```### Local State (useState)



**Happy Coding with React and GitHub Copilot! 🚀**```typescript


```typescript// Simple form state

import styles from './Component.module.css';const FormComponent: React.FC = () => {

  const [formData, setFormData] = useState({ title: '', description: '' });

const Component = () => (  const [errors, setErrors] = useState<Record<string, string>>({});

  <div className={styles.container}>

    <h1 className={styles.title}>Title</h1>  const validateForm = (): boolean => {

  </div>    const newErrors: Record<string, string> = {};

);    

```    if (!formData.title.trim()) {

      newErrors.title = 'Title is required';

### 2. Styled Components    }

```typescript    

import styled from 'styled-components';    setErrors(newErrors);

    return Object.keys(newErrors).length === 0;

const Container = styled.div`  };

  padding: 16px;

  background: white;  const handleSubmit = (e: React.FormEvent) => {

`;    e.preventDefault();

    if (validateForm()) {

const Title = styled.h1`      // Submit logic

  font-size: 24px;    }

  font-weight: bold;  };

`;

  return (

const Component = () => (    <form onSubmit={handleSubmit}>

  <Container>      <input

    <Title>Title</Title>        type="text"

  </Container>        value={formData.title}

);        onChange={(e) => setFormData(prev => ({ ...prev, title: e.target.value }))}

```        placeholder="Enter title"

      />

### 3. Tailwind CSS      {errors.title && <span className="error">{errors.title}</span>}

```typescript    </form>

const Component = () => (  );

  <div className="p-4 bg-white">};

    <h1 className="text-2xl font-bold">Title</h1>```

  </div>

);### Context API (Global State)

``````typescript

// contexts/AppContext.tsx

**เลือกตามความเหมาะสมของโปรเจค**interface AppContextType {

  data: DataType[];

---  filter: FilterType;

  setFilter: (filter: FilterType) => void;

## 🌐 API Integration  searchTerm: string;

  setSearchTerm: (term: string) => void;

### Axios Setup}

```typescript

// services/api.tsconst AppContext = createContext<AppContextType | undefined>(undefined);

import axios from 'axios';

export const AppProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {

const api = axios.create({  const [filter, setFilter] = useState<FilterType>('all');

  baseURL: process.env.REACT_APP_API_URL || 'http://localhost:3001',  const [searchTerm, setSearchTerm] = useState('');

  timeout: 10000  const { data = [] } = useData();

});

  const value = {

// Interceptors    data,

api.interceptors.request.use(config => {    filter,

  const token = localStorage.getItem('token');    setFilter,

  if (token) config.headers.Authorization = `Bearer ${token}`;    searchTerm,

  return config;    setSearchTerm,

});  };



api.interceptors.response.use(  return (

  response => response,    <AppContext.Provider value={value}>

  error => {      {children}

    if (error.response?.status === 401) {    </AppContext.Provider>

      // Handle unauthorized  );

    }};

    return Promise.reject(error);

  }export const useAppContext = () => {

);  const context = useContext(AppContext);

  if (!context) {

export default api;    throw new Error('useAppContext must be used within AppProvider');

```  }

  return context;

### API Service Pattern};

```typescript```

// services/itemService.ts

import api from './api';### React Query for Server State

```typescript

export const itemService = {// services/apiService.ts

  getAll: async () => {export const apiService = {

    const { data } = await api.get('/items');  getAll: async (): Promise<DataType[]> => {

    return data;    const response = await api.get('/data');

  },    return response.data;

    },

  getById: async (id: string) => {

    const { data } = await api.get(`/items/${id}`);  create: async (item: CreateRequest): Promise<DataType> => {

    return data;    const response = await api.post('/data', item);

  },    return response.data;

    },

  create: async (item: CreateItem) => {

    const { data } = await api.post('/items', item);  update: async (id: string, updates: Partial<DataType>): Promise<DataType> => {

    return data;    const response = await api.patch(`/data/${id}`, updates);

  },    return response.data;

    },

  update: async (id: string, updates: Partial<Item>) => {

    const { data } = await api.patch(`/items/${id}`, updates);  delete: async (id: string): Promise<void> => {

    return data;    await api.delete(`/data/${id}`);

  },  },

  };

  delete: async (id: string) => {

    await api.delete(`/items/${id}`);// hooks/useData.ts

  }export const useData = (filter?: FilterType) => {

};  return useQuery({

```    queryKey: ['data', filter],

    queryFn: () => apiService.getAll(),

### Error Handling    select: (data) => {

```typescript      if (!filter || filter === 'all') return data;

// hooks/useApiError.ts      return data.filter(item => {

export const useApiError = () => {        // Filter logic based on requirements

  const [error, setError] = useState<string | null>(null);      });

    },

  const handleError = (err: any) => {  });

    const message = err.response?.data?.message || err.message || 'Error occurred';};

    setError(message);```

  };

## 🎨 Styling Guidelines

  const clearError = () => setError(null);

### CSS Modules

  return { error, handleError, clearError };```typescript

};// TodoItem.module.css

```.todoItem {

  display: flex;

---  align-items: center;

  padding: 12px;

## 🧪 Testing  border: 1px solid #e0e0e0;

  border-radius: 8px;

### Component Testing  margin-bottom: 8px;

```typescript}

// Component.test.tsx

import { render, screen, fireEvent } from '@testing-library/react';.todoItem.completed {

import { Button } from './Button';  opacity: 0.6;

  text-decoration: line-through;

describe('Button', () => {}

  it('renders correctly', () => {

    render(<Button>Click me</Button>);.title {

    expect(screen.getByText('Click me')).toBeInTheDocument();  flex: 1;

  });  margin: 0 12px;

}

  it('calls onClick when clicked', () => {

    const handleClick = jest.fn();.deleteButton {

    render(<Button onClick={handleClick}>Click me</Button>);  background: #ff4757;

      color: white;

    fireEvent.click(screen.getByText('Click me'));  border: none;

    expect(handleClick).toHaveBeenCalledTimes(1);  padding: 6px 12px;

  });  border-radius: 4px;

});  cursor: pointer;

```}



### Hook Testing// TodoItem.tsx

```typescriptimport styles from './TodoItem.module.css';

// useCustomHook.test.ts

import { renderHook, act } from '@testing-library/react';const TodoItem: React.FC<Props> = ({ todo, onToggle, onDelete }) => (

import { useCounter } from './useCounter';  <div className={`${styles.todoItem} ${todo.completed ? styles.completed : ''}`}>

    <input

describe('useCounter', () => {      type="checkbox"

  it('increments counter', () => {      checked={todo.completed}

    const { result } = renderHook(() => useCounter());      onChange={() => onToggle(todo.id)}

        />

    act(() => {    <span className={styles.title}>{todo.title}</span>

      result.current.increment();    <button

    });      className={styles.deleteButton}

          onClick={() => onDelete(todo.id)}

    expect(result.current.count).toBe(1);    >

  });      Delete

});    </button>

```  </div>

);

### E2E Testing (Cypress)```

```typescript

// cypress/e2e/app.cy.ts### Styled Components

describe('App Flow', () => {```typescript

  it('creates new item', () => {import styled, { css } from 'styled-components';

    cy.visit('/');

    cy.get('[data-testid="add-button"]').click();const TodoItemContainer = styled.div<{ completed: boolean }>`

    cy.get('[data-testid="title-input"]').type('New Item');  display: flex;

    cy.get('[data-testid="submit-button"]').click();  align-items: center;

    cy.contains('New Item').should('be.visible');  padding: 12px;

  });  border: 1px solid #e0e0e0;

});  border-radius: 8px;

```  margin-bottom: 8px;

  transition: opacity 0.3s ease;

---

  ${props => props.completed && css`

## 🤖 Copilot Best Practices    opacity: 0.6;

    text-decoration: line-through;

### 1. เขียน Comments ให้ชัดเจน  `}

```typescript`;

// ✅ Good - Copilot เข้าใจง่าย

// Create a button component with primary and secondary variantsconst Title = styled.span`

// Include loading state and disabled state  flex: 1;

// Add proper TypeScript types  margin: 0 12px;

const Button: React.FC = () => {  font-size: 16px;

  // Copilot จะ generate code ที่ดี`;

};

const DeleteButton = styled.button`

// ❌ Bad  background: #ff4757;

// button  color: white;

const Button = () => {};  border: none;

```  padding: 6px 12px;

  border-radius: 4px;

### 2. ใช้ชื่อตัวแปรที่สื่อความหมาย  cursor: pointer;

```typescript  

// ✅ Good  &:hover {

const isLoading = useState(false);    background: #ff3838;

const userList = useState<User[]>([]);  }

const handleSubmit = () => {};`;

```

// ❌ Bad  

const flag = useState(false);### Tailwind CSS

const data = useState([]);```typescript

const fn = () => {};const TodoItem: React.FC<Props> = ({ todo, onToggle, onDelete }) => (

```  <div className={`

    flex items-center p-3 border border-gray-200 rounded-lg mb-2

### 3. สร้าง Types ก่อน    ${todo.completed ? 'opacity-60 line-through' : ''}

```typescript  `}>

// Define types first - ช่วย Copilot เข้าใจ context    <input

interface User {      type="checkbox"

  id: string;      checked={todo.completed}

  name: string;      onChange={() => onToggle(todo.id)}

  email: string;      className="mr-3"

}    />

    <span className="flex-1 text-gray-800">

// Copilot จะ generate code ที่ใช้ User type      {todo.title}

const UserList: React.FC = () => {    </span>

  // Copilot รู้ว่า users เป็น User[]    <button

  const users = useUsers();      onClick={() => onDelete(todo.id)}

};      className="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded"

```    >

      Delete

### 4. ใช้ Method Signatures    </button>

```typescript  </div>

// เขียน signature ก่อน ให้ Copilot implement);

class UserService {```

  // Get all users from API

  async getAll(): Promise<User[]> {## 🌐 API Integration

    // Copilot จะ implement

  }### Axios Setup

```typescript

  // Create new user with validation// services/api.ts

  async create(user: CreateUserDto): Promise<User> {import axios from 'axios';

    // Copilot จะ implement

  }const api = axios.create({

}  baseURL: process.env.REACT_APP_API_BASE_URL || 'http://localhost:3001',

```  timeout: 10000,

});

### 5. Comment-Driven Development

```typescript// Request interceptor

const useDataFilters = () => {api.interceptors.request.use(

  // State for filter type (all, active, completed)  (config) => {

  // State for search term with debounce    const token = localStorage.getItem('authToken');

  // State for sort order    if (token) {

        config.headers.Authorization = `Bearer ${token}`;

  // Function to apply filters    }

  // Function to clear filters    return config;

  // Function to get filter count  },

    (error) => Promise.reject(error)

  // Return filtered data and controls);

};

// Copilot จะ generate implementation// Response interceptor

```api.interceptors.response.use(

  (response) => response,

### 6. ใช้ Consistent Patterns  (error) => {

```typescript    if (error.response?.status === 401) {

// ใช้ pattern เดียวกันทั้งโปรเจค      localStorage.removeItem('authToken');

// Copilot จะเรียนรู้และ suggest ตาม pattern      window.location.href = '/login';

    }

// Pattern: Feature hooks    return Promise.reject(error);

export const useItems = () => { /* ... */ };  }

export const useUsers = () => { /* ... */ };);



// Pattern: Feature services  export default api;

export const itemService = { /* ... */ };```

export const userService = { /* ... */ };

```### Error Handling

```typescript

---// types/api.types.ts

export interface ApiError {

## 📋 Code Quality Checklist  message: string;

  code?: string;

### Component  details?: Record<string, any>;

- [ ] TypeScript interfaces defined}

- [ ] Props destructured

- [ ] Default values provided// hooks/useApiError.ts

- [ ] Proper event handlersexport const useApiError = () => {

- [ ] Loading states handled  const [error, setError] = useState<ApiError | null>(null);

- [ ] Error states handled

  const handleError = useCallback((err: any) => {

### Performance    const apiError: ApiError = {

- [ ] React.memo ใช้กับ expensive components      message: err.response?.data?.message || err.message || 'An error occurred',

- [ ] useMemo ใช้กับ expensive calculations      code: err.response?.data?.code,

- [ ] useCallback ใช้กับ event handlers      details: err.response?.data?.details,

- [ ] Dependency arrays ถูกต้อง    };

    setError(apiError);

### Testing  }, []);

- [ ] Unit tests สำหรับ components

- [ ] Unit tests สำหรับ hooks  const clearError = useCallback(() => setError(null), []);

- [ ] Integration tests สำหรับ features

- [ ] E2E tests สำหรับ critical flows  return { error, handleError, clearError };

};

### Code Style```

- [ ] ESLint ผ่าน

- [ ] Prettier formatted### Mock API for Development

- [ ] Naming conventions consistent```typescript

- [ ] Comments เพียงพอ// services/mockApi.ts

export const mockTodos: Todo[] = [

---  {

    id: '1',

## 💡 Tips สำหรับความสำเร็จ    title: 'Complete React project',

    description: 'Finish the todo application',

1. **ใช้ TypeScript** - ช่วยให้ Copilot suggest ได้ดีขึ้น    completed: false,

2. **เขียน Comments** - อธิบายว่าต้องการอะไร    createdAt: new Date('2024-01-15'),

3. **Consistent Naming** - ใช้ชื่อที่สื่อความหมาย    dueDate: new Date('2024-01-20'),

4. **Define Types First** - สร้าง interfaces ก่อนเขียนโค้ด  },

5. **Test Early** - เขียน tests ตั้งแต่เริ่มต้น  // More mock data...

6. **Keep Components Small** - แยก component ให้เล็กและชัดเจน];



---export const mockTodoService = {

  getAll: (): Promise<Todo[]> => {

**Happy Coding with React and GitHub Copilot! 🚀**    return new Promise(resolve => {
      setTimeout(() => resolve([...mockTodos]), 500);
    });
  },

  create: (todo: CreateTodoRequest): Promise<Todo> => {
    return new Promise(resolve => {
      const newTodo: Todo = {
        id: Date.now().toString(),
        ...todo,
        completed: false,
        createdAt: new Date(),
      };
      mockTodos.push(newTodo);
      setTimeout(() => resolve(newTodo), 300);
    });
  },
};
```

## 🧪 Testing Strategy

### Jest + React Testing Library Setup
```typescript
// src/setupTests.ts
import '@testing-library/jest-dom';
import { configure } from '@testing-library/react';

configure({ testIdAttribute: 'data-testid' });

// Mock ResizeObserver
global.ResizeObserver = jest.fn().mockImplementation(() => ({
  observe: jest.fn(),
  unobserve: jest.fn(),
  disconnect: jest.fn(),
}));
```

### Component Testing
```typescript
// components/TodoItem/TodoItem.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { TodoItem } from './TodoItem';
import { mockTodo } from '../../__tests__/mocks';

describe('TodoItem', () => {
  const mockOnToggle = jest.fn();
  const mockOnDelete = jest.fn();

  beforeEach(() => {
    jest.clearAllMocks();
  });

  it('renders todo title correctly', () => {
    render(
      <TodoItem
        todo={mockTodo}
        onToggle={mockOnToggle}
        onDelete={mockOnDelete}
      />
    );

    expect(screen.getByText(mockTodo.title)).toBeInTheDocument();
  });

  it('calls onToggle when checkbox is clicked', () => {
    render(
      <TodoItem
        todo={mockTodo}
        onToggle={mockOnToggle}
        onDelete={mockOnDelete}
      />
    );

    const checkbox = screen.getByRole('checkbox');
    fireEvent.click(checkbox);

    expect(mockOnToggle).toHaveBeenCalledWith(mockTodo.id);
  });

  it('shows completed styling when todo is completed', () => {
    const completedTodo = { ...mockTodo, completed: true };
    
    render(
      <TodoItem
        todo={completedTodo}
        onToggle={mockOnToggle}
        onDelete={mockOnDelete}
      />
    );

    const todoElement = screen.getByTestId('todo-item');
    expect(todoElement).toHaveClass('completed');
  });
});
```

### Custom Hook Testing
```typescript
// hooks/__tests__/useTodos.test.ts
import { renderHook, waitFor } from '@testing-library/react';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { useTodos } from '../useTodos';
import * as todoService from '../../services/todoService';

jest.mock('../../services/todoService');
const mockedTodoService = jest.mocked(todoService);

const createWrapper = () => {
  const queryClient = new QueryClient({
    defaultOptions: {
      queries: { retry: false },
      mutations: { retry: false },
    },
  });

  return ({ children }: { children: React.ReactNode }) => (
    <QueryClientProvider client={queryClient}>
      {children}
    </QueryClientProvider>
  );
};

describe('useTodos', () => {
  it('fetches todos successfully', async () => {
    const mockTodos = [{ id: '1', title: 'Test Todo', completed: false }];
    mockedTodoService.getAll.mockResolvedValue(mockTodos);

    const { result } = renderHook(() => useTodos(), {
      wrapper: createWrapper(),
    });

    await waitFor(() => {
      expect(result.current.isSuccess).toBe(true);
    });

    expect(result.current.data).toEqual(mockTodos);
  });
});
```

### E2E Testing with Cypress
```typescript
// cypress/e2e/todo-management.cy.ts
describe('Todo Management', () => {
  beforeEach(() => {
    cy.visit('/');
  });

  it('allows user to create a new todo', () => {
    const todoTitle = 'New Todo Item';
    
    cy.get('[data-testid=add-todo-input]').type(todoTitle);
    cy.get('[data-testid=add-todo-button]').click();
    
    cy.get('[data-testid=todo-list]')
      .should('contain', todoTitle);
  });

  it('allows user to mark todo as complete', () => {
    // Create a todo first
    cy.get('[data-testid=add-todo-input]').type('Test Todo');
    cy.get('[data-testid=add-todo-button]').click();
    
    // Mark as complete
    cy.get('[data-testid=todo-checkbox]').first().click();
    
    // Verify completion
    cy.get('[data-testid=todo-item]').first()
      .should('have.class', 'completed');
  });
});
```

## 🤖 GitHub Copilot Best Practices

### 1. Effective Prompts for Component Generation

#### ✅ Good Prompts
```typescript
// Create a reusable Button component with TypeScript
// Props: children, variant (primary/secondary/danger), size (sm/md/lg), disabled, onClick
// Include proper accessibility attributes and hover states

// Generate a Todo list item component that:
// - Shows todo title and description
// - Has checkbox to toggle completion
// - Shows creation date in relative format
// - Has delete button with confirmation
// - Includes proper TypeScript types
```

#### ❌ Ineffective Prompts
```typescript
// make button
// todo component
```

### 2. Context-Aware Code Generation

#### Provide Context Comments
```typescript
// Current project uses:
// - React 18 with TypeScript
// - Tailwind CSS for styling
// - React Query for data fetching
// - React Hook Form for form handling

// Create a todo form component with validation
const TodoForm: React.FC = () => {
  // Copilot will generate code considering the context above
};
```

#### Use Descriptive File Names
```typescript
// ✅ Good file names that help Copilot understand context
// components/forms/TodoForm.tsx
// hooks/api/useTodoMutations.ts
// services/todo/todoService.ts
// types/todo/todo.types.ts

// ❌ Generic names
// Form.tsx
// hooks.ts
// service.ts
```

### 3. Progressive Code Building

#### Start with Type Definitions
```typescript
// Define types first to guide Copilot
interface Todo {
  id: string;
  title: string;
  description?: string;
  completed: boolean;
  createdAt: Date;
  dueDate?: Date;
  priority: 'low' | 'medium' | 'high';
}

// Now Copilot understands the Todo structure for subsequent code
const TodoItem: React.FC<{ todo: Todo }> = ({ todo }) => {
  // Copilot will generate code using the Todo interface
};
```

#### Use Method Signatures as Prompts
```typescript
// API service methods - Copilot will implement based on signatures
class TodoService {
  // Get all todos with optional filtering
  async getTodos(filter?: TodoFilter): Promise<Todo[]> {
    // Copilot implementation
  }

  // Create new todo with validation
  async createTodo(todo: CreateTodoRequest): Promise<Todo> {
    // Copilot implementation
  }

  // Update existing todo
  async updateTodo(id: string, updates: Partial<Todo>): Promise<Todo> {
    // Copilot implementation  
  }
}
```

### 4. Copilot-Friendly Naming Conventions

#### Use Descriptive Variable Names
```typescript
// ✅ Helps Copilot understand intent
const isCreateTodoModalOpen = useState(false);
const pendingTodosCount = todos.filter(t => !t.completed).length;
const sortTodosByDueDate = (todos: Todo[]) => { /* ... */ };

// ❌ Generic names confuse Copilot
const isOpen = useState(false);
const count = todos.filter(t => !t.completed).length;
const sort = (items: any[]) => { /* ... */ };
```

### 5. Comment-Driven Development with Copilot

```typescript
// Use comments to guide Copilot's code generation
const useTodoFilters = () => {
  // State for current filter (all, active, completed)
  // State for search term with debounced input
  // State for sort order (date, priority, alphabetical)
  
  // Function to apply all filters to todo list
  // Function to clear all filters
  // Function to get active filter count for UI badge
  
  // Return filtered todos and filter controls
};

// Copilot will generate implementation based on comments above
```

### 6. Test-Driven Development with Copilot

```typescript
// Write test descriptions first, let Copilot implement
describe('TodoForm validation', () => {
  // Should show error when title is empty
  // Should show error when title exceeds 100 characters
  // Should show error when due date is in the past
  // Should clear errors when input becomes valid
  // Should submit form when all fields are valid
});

// Then implement the actual component
const TodoForm: React.FC = () => {
  // Copilot will generate validation logic based on test descriptions
};
```

## 📋 Code Generation Guidelines

### 1. Component Generation Template
```typescript
// Use this template structure for consistent Copilot output

// Import statements
import React from 'react';
import { ComponentNameProps } from './ComponentName.types';

// Component interface
interface ComponentNameProps {
  // Required props
  children: React.ReactNode;
  // Optional props with defaults
  variant?: 'default' | 'primary';
  // Event handlers
  onClick?: (event: React.MouseEvent) => void;
}

// Component implementation
export const ComponentName: React.FC<ComponentNameProps> = ({
  // Destructure props with defaults
  children,
  variant = 'default',
  onClick,
  ...rest
}) => {
  // Component logic
  
  return (
    // JSX with proper accessibility
    <div
      role="button"
      tabIndex={0}
      onClick={onClick}
      {...rest}
    >
      {children}
    </div>
  );
};

export default ComponentName;
```

### 2. Hook Generation Template
```typescript
// Custom hook template for Copilot
export const useCustomHook = (initialValue?: any) => {
  // State declarations
  const [state, setState] = useState(initialValue);
  
  // Effect hooks if needed
  useEffect(() => {
    // Side effects
  }, []);
  
  // Memoized values
  const memoizedValue = useMemo(() => {
    // Expensive calculations
  }, [state]);
  
  // Callback functions
  const handleAction = useCallback(() => {
    // Event handlers
  }, []);
  
  // Return hook interface
  return {
    state,
    setState,
    memoizedValue,
    handleAction,
  };
};
```

### 3. Service Generation Template
```typescript
// API service template for Copilot
class ApiService {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  // GET request method
  async get<T>(endpoint: string): Promise<T> {
    // Implementation
  }
  
  // POST request method
  async post<T>(endpoint: string, data: any): Promise<T> {
    // Implementation
  }
  
  // Error handling method
  private handleError(error: any): never {
    // Error processing
  }
}
```

## 🔍 Code Quality Checklist

### Component Quality
- [ ] TypeScript interfaces defined
- [ ] Props destructured with defaults
- [ ] Proper event handler types
- [ ] Accessibility attributes included
- [ ] Error boundaries implemented
- [ ] Loading states handled
- [ ] Memoization used appropriately

### Performance Best Practices
- [ ] React.memo for expensive components
- [ ] useMemo for expensive calculations
- [ ] useCallback for event handlers
- [ ] Proper dependency arrays
- [ ] Code splitting implemented
- [ ] Bundle size optimized

### Testing Coverage
- [ ] Unit tests for components
- [ ] Integration tests for features
- [ ] E2E tests for critical paths
- [ ] Error scenario testing
- [ ] Performance testing
- [ ] Accessibility testing

### Code Style
- [ ] ESLint rules followed
- [ ] Prettier formatting applied
- [ ] Consistent naming conventions
- [ ] Proper file organization
- [ ] Documentation updated
- [ ] Git commit messages clear

---

## 🚀 Getting Started with This Guide

1. **Setup Development Environment** - Install required tools and extensions
2. **Create Project Structure** - Follow the feature-based organization
3. **Configure Copilot** - Use the provided settings and best practices
4. **Start Small** - Begin with simple components and gradually add complexity
5. **Test Everything** - Write tests as you develop features
6. **Iterate and Improve** - Continuously refactor and optimize

## 💡 Quick Tips for Success

- **Use TypeScript everywhere** - Better Copilot suggestions and fewer bugs
- **Write descriptive comments** - Guide Copilot to generate better code
- **Follow naming conventions** - Consistent names improve code generation
- **Start with types** - Define interfaces before implementing components
- **Test early and often** - Prevent issues from accumulating
- **Keep components small** - Easier to understand, test, and maintain

---

**Happy Coding with React and GitHub Copilot! 🚀**