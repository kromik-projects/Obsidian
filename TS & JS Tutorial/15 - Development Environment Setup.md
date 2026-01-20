# Development Environment Setup

## Overview

This guide helps you set up a professional development environment for JavaScript and TypeScript projects.

## Essential Tools

### 1. Node.js

Node.js lets you run JavaScript outside the browser.

#### Installation

**Windows/Mac:**
Download from [nodejs.org](https://nodejs.org/) - choose LTS version.

**Linux (Ubuntu/Debian):**
```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Verify installation:**
```bash
node --version    # e.g., v20.10.0
npm --version     # e.g., 10.2.3
```

### 2. Package Manager

npm comes with Node.js, but alternatives exist:

```bash
# npm (default)
npm install package-name

# pnpm (faster, efficient)
npm install -g pnpm
pnpm install package-name

# yarn
npm install -g yarn
yarn add package-name
```

### 3. Code Editor

**Visual Studio Code** is the most popular choice.

Download from [code.visualstudio.com](https://code.visualstudio.com/)

#### Essential VS Code Extensions

| Extension | Purpose |
|-----------|---------|
| ESLint | Code linting |
| Prettier | Code formatting |
| TypeScript Hero | TS imports |
| Path Intellisense | File path autocomplete |
| GitLens | Git integration |
| Error Lens | Inline error display |
| Thunder Client | API testing |

### 4. TypeScript

```bash
# Install globally
npm install -g typescript

# Verify
tsc --version
```

### 5. Git

**Windows:**
Download from [git-scm.com](https://git-scm.com/)

**Mac:**
```bash
brew install git
```

**Linux:**
```bash
sudo apt install git
```

**Configure:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

## Project Setup

### Basic Project Structure

```
my-project/
├── src/
│   ├── index.ts
│   └── utils/
├── tests/
├── dist/           # Compiled output
├── node_modules/   # Dependencies (git-ignored)
├── package.json
├── tsconfig.json
├── .gitignore
└── README.md
```

### Initialize a Project

```bash
# Create directory
mkdir my-project && cd my-project

# Initialize npm
npm init -y

# Initialize TypeScript
npx tsc --init

# Initialize Git
git init
```

### package.json Essentials

```json
{
    "name": "my-project",
    "version": "1.0.0",
    "description": "My TypeScript project",
    "main": "dist/index.js",
    "scripts": {
        "build": "tsc",
        "start": "node dist/index.js",
        "dev": "ts-node src/index.ts",
        "test": "jest",
        "lint": "eslint src/**/*.ts",
        "format": "prettier --write src/**/*.ts"
    },
    "devDependencies": {
        "typescript": "^5.0.0",
        "ts-node": "^10.0.0",
        "@types/node": "^20.0.0"
    }
}
```

### tsconfig.json for Development

```json
{
    "compilerOptions": {
        // Output settings
        "target": "ES2020",
        "module": "commonjs",
        "outDir": "./dist",
        "rootDir": "./src",

        // Type checking
        "strict": true,
        "noImplicitAny": true,
        "strictNullChecks": true,

        // Module resolution
        "moduleResolution": "node",
        "esModuleInterop": true,
        "resolveJsonModule": true,

        // Development helpers
        "sourceMap": true,
        "declaration": true,

        // Code quality
        "noUnusedLocals": true,
        "noUnusedParameters": true,
        "noImplicitReturns": true
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules", "dist"]
}
```

### .gitignore

```gitignore
# Dependencies
node_modules/

# Build output
dist/
build/

# Environment files
.env
.env.local
.env.*.local

# IDE
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*

# Test coverage
coverage/
```

## Linting and Formatting

### ESLint Setup

```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

Create `.eslintrc.json`:
```json
{
    "parser": "@typescript-eslint/parser",
    "plugins": ["@typescript-eslint"],
    "extends": [
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended"
    ],
    "rules": {
        "no-console": "warn",
        "@typescript-eslint/explicit-function-return-type": "warn",
        "@typescript-eslint/no-unused-vars": "error"
    },
    "env": {
        "node": true,
        "es2020": true
    }
}
```

### Prettier Setup

```bash
npm install --save-dev prettier
```

Create `.prettierrc`:
```json
{
    "semi": true,
    "singleQuote": true,
    "tabWidth": 4,
    "trailingComma": "es5",
    "printWidth": 80
}
```

Create `.prettierignore`:
```
node_modules
dist
coverage
```

### VS Code Settings

Create `.vscode/settings.json`:
```json
{
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "typescript.preferences.importModuleSpecifier": "relative"
}
```

## Testing Setup

### Jest

```bash
npm install --save-dev jest ts-jest @types/jest
```

Create `jest.config.js`:
```javascript
module.exports = {
    preset: 'ts-jest',
    testEnvironment: 'node',
    roots: ['<rootDir>/src', '<rootDir>/tests'],
    testMatch: ['**/*.test.ts'],
    collectCoverageFrom: ['src/**/*.ts'],
    coverageDirectory: 'coverage',
    coverageReporters: ['text', 'lcov']
};
```

Example test file `tests/utils.test.ts`:
```typescript
import { add, multiply } from '../src/utils';

describe('Math utilities', () => {
    test('add returns sum of two numbers', () => {
        expect(add(2, 3)).toBe(5);
    });

    test('multiply returns product', () => {
        expect(multiply(3, 4)).toBe(12);
    });
});
```

## Debugging

### VS Code Launch Configuration

Create `.vscode/launch.json`:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Debug TypeScript",
            "program": "${workspaceFolder}/src/index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": ["${workspaceFolder}/dist/**/*.js"],
            "sourceMaps": true
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Debug Current File",
            "runtimeArgs": ["-r", "ts-node/register"],
            "args": ["${file}"],
            "cwd": "${workspaceFolder}"
        }
    ]
}
```

## Environment Variables

### Using dotenv

```bash
npm install dotenv
npm install --save-dev @types/dotenv
```

Create `.env`:
```env
NODE_ENV=development
PORT=3000
API_KEY=your-secret-key
DATABASE_URL=postgres://localhost/mydb
```

Usage:
```typescript
import dotenv from 'dotenv';
dotenv.config();

const port = process.env.PORT || 3000;
const apiKey = process.env.API_KEY;
```

> [!warning] Never Commit .env Files
> Always add `.env` to `.gitignore`!

## Useful npm Scripts

```json
{
    "scripts": {
        "build": "tsc",
        "build:watch": "tsc --watch",
        "start": "node dist/index.js",
        "dev": "ts-node-dev --respawn src/index.ts",
        "test": "jest",
        "test:watch": "jest --watch",
        "test:coverage": "jest --coverage",
        "lint": "eslint src/**/*.ts",
        "lint:fix": "eslint src/**/*.ts --fix",
        "format": "prettier --write 'src/**/*.ts'",
        "clean": "rm -rf dist coverage",
        "prepare": "npm run build"
    }
}
```

## Quick Start Template

Run these commands to set up a new project quickly:

```bash
# Create and enter project
mkdir my-ts-app && cd my-ts-app

# Initialize
npm init -y
npm install typescript ts-node @types/node --save-dev

# Initialize TypeScript
npx tsc --init

# Create source directory
mkdir src
echo 'console.log("Hello, TypeScript!");' > src/index.ts

# Add scripts to package.json
npm pkg set scripts.build="tsc"
npm pkg set scripts.start="node dist/index.js"
npm pkg set scripts.dev="ts-node src/index.ts"

# Run
npm run dev
```

## Key Takeaways

- Node.js and npm are essential for JS/TS development
- VS Code with extensions provides the best development experience
- Use `tsconfig.json` to configure TypeScript
- Set up ESLint and Prettier for code quality
- Jest is the standard testing framework
- Keep secrets in `.env` files (never commit them!)
- Use npm scripts to automate common tasks

---

**Previous:** [[14 - Generics]]

**Next:** [[16 - Building Your First App]]

**Back to:** [[00 - Welcome]]
