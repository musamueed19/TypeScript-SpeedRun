# ⚙️ **TypeScript Installation & Setup Guide**

## 🎯 **Learning Objectives**
By the end of this lesson, you will be able to:
- Install Node.js and npm on your system
- Install TypeScript globally and locally
- Set up VS Code with essential extensions
- Create and configure your first TypeScript project
- Compile and run TypeScript code

---

## 📋 **Prerequisites**

### **System Requirements**
- ✅ **Operating System:** Windows, macOS, or Linux
- ✅ **RAM:** At least 4GB (8GB recommended)
- ✅ **Storage:** 2GB free space
- ✅ **Internet:** For downloading packages

---

## 🚀 **Step 1: Install Node.js & npm**

### **Windows Installation**

1. **Download Node.js:**
   - Visit [nodejs.org](https://nodejs.org/)
   - Download the **LTS version** (recommended)
   - Run the `.msi` installer

2. **Verify Installation:**
   ```cmd
   node --version
   npm --version
   ```

### **macOS Installation**

```bash
# Using Homebrew (recommended)
brew install node

# Or download from nodejs.org
# Verify installation
node --version
npm --version
```

### **Linux Installation**

```bash
# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version
npm --version
```

### **Alternative: Node Version Manager (Recommended)**

```bash
# Install NVM (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install latest LTS Node.js
nvm install --lts
nvm use --lts
```

---

## 📦 **Step 2: Install TypeScript**

### **Global Installation (Recommended for CLI)**

```bash
# Install TypeScript globally
npm install -g typescript

# Verify installation
tsc --version

# Install additional global tools
npm install -g ts-node              # Run TypeScript directly
npm install -g typescript-formatter  # Code formatting
npm install -g @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

### **Local Installation (Project-specific)**

```bash
# Create new project directory
mkdir my-typescript-project
cd my-typescript-project

# Initialize npm project
npm init -y

# Install TypeScript locally
npm install --save-dev typescript
npm install --save-dev @types/node  # Node.js type definitions

# Install development tools
npm install --save-dev ts-node-dev  # Development server
npm install --save-dev nodemon      # Auto-restart on changes
```

---

## 🔧 **Step 3: VS Code Setup**

### **Install VS Code**
- Download from [code.visualstudio.com](https://code.visualstudio.com/)
- Install with default settings

### **Essential Extensions**

```bash
# Install via VS Code Extensions panel or CLI
code --install-extension ms-vscode.vscode-typescript-next
code --install-extension bradlc.vscode-tailwindcss
code --install-extension esbenp.prettier-vscode
code --install-extension ms-vscode.vscode-eslint
code --install-extension usernamehw.errorlens
code --install-extension formulahendry.auto-rename-tag
code --install-extension ms-vscode.vscode-json
```

### **Recommended Extensions List**

| Extension | Purpose | Publisher |
|-----------|---------|-----------|
| **TypeScript Hero** | Enhanced TypeScript support | rbbit |
| **Error Lens** | Inline error display | usernamehw |
| **Prettier** | Code formatting | esbenp |
| **ESLint** | Code linting | ms-vscode |
| **Auto Rename Tag** | HTML/JSX tag renaming | formulahendry |
| **GitLens** | Enhanced Git integration | eamodio |
| **Bracket Pair Colorizer** | Bracket highlighting | CoenraadS |
| **Thunder Client** | API testing | rangav |
| **Live Server** | Local development server | ritwickdey |

### **VS Code Settings for TypeScript**

Create `.vscode/settings.json` in your project:

```json
{
  "typescript.preferences.importModuleSpecifier": "relative",
  "typescript.suggest.autoImports": true,
  "typescript.updateImportsOnFileMove.enabled": "always",
  "editor.codeActionsOnSave": {
    "source.organizeImports": true,
    "source.fixAll.eslint": true
  },
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "files.eol": "\n",
  "typescript.preferences.quoteStyle": "single"
}
```

---

## 🏗️ **Step 4: Create Your First TypeScript Project**

### **Project Structure Setup**

```bash
# Create project directory
mkdir typescript-starter
cd typescript-starter

# Initialize npm
npm init -y

# Install dependencies
npm install --save-dev typescript @types/node ts-node-dev

# Create project structure
mkdir src
mkdir dist
mkdir tests
```

### **Initialize TypeScript Configuration**

```bash
# Generate tsconfig.json
npx tsc --init

# Or create custom tsconfig.json
```

### **Basic tsconfig.json**

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "CommonJS",
    "lib": ["ES2022", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "removeComments": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### **Package.json Scripts**

```json
{
  "scripts": {
    "dev": "ts-node-dev --respawn --transpile-only src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "clean": "rimraf dist",
    "type-check": "tsc --noEmit"
  }
}
```

---

## 💻 **Step 5: Your First TypeScript Program**

### **Create src/index.ts**

```typescript
// src/index.ts
interface Person {
  name: string;
  age: number;
  city: string;
}

class Greeter {
  private greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }

  greet(person: Person): string {
    return `${this.greeting}, ${person.name}! Welcome from ${person.city}.`;
  }
}

// Usage
const person: Person = {
  name: "John Doe",
  age: 30,
  city: "New York"
};

const greeter = new Greeter("Hello");
console.log(greeter.greet(person));

// Type safety in action
// greeter.greet("John"); // ❌ Error: Argument of type 'string'
```

### **Compile and Run**

```bash
# Method 1: Compile then run
npm run build
npm start

# Method 2: Run directly with ts-node
npm run dev

# Method 3: One-time compilation
npx tsc src/index.ts --outDir dist
node dist/index.js
```

---

## 🔧 **Step 6: Development Workflow**

### **Watch Mode for Development**

```bash
# TypeScript compiler in watch mode
tsc --watch

# Development server with auto-restart
npm run dev

# Run with nodemon
npx nodemon --exec ts-node src/index.ts
```

### **Debugging Setup**

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
      "preLaunchTask": "${workspaceFolder}/node_modules/.bin/tsc:build",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"],
      "runtimeArgs": ["-r", "ts-node/register"]
    }
  ]
}
```

---

## ✅ **Verification Checklist**

### **Test Your Setup**

1. **✅ Node.js & npm installed**
   ```bash
   node --version  # Should show v18+ 
   npm --version   # Should show 8+
   ```

2. **✅ TypeScript globally available**
   ```bash
   tsc --version   # Should show 5.0+
   ```

3. **✅ VS Code with extensions**
   - Open .ts file and see syntax highlighting
   - Check IntelliSense works
   - Verify error detection

4. **✅ Project compilation works**
   ```bash
   npm run build   # Should create dist/ folder
   npm start       # Should run without errors
   ```

5. **✅ Development workflow**
   ```bash
   npm run dev     # Should start development server
   ```

---

## 🐛 **Troubleshooting**

### **Common Issues & Solutions**

1. **"tsc: command not found"**
   ```bash
   # Reinstall TypeScript globally
   npm uninstall -g typescript
   npm install -g typescript
   ```

2. **"Cannot find module '@types/node'"**
   ```bash
   npm install --save-dev @types/node
   ```

3. **VS Code not recognizing TypeScript**
   - Restart VS Code
   - Check TypeScript version: `Cmd/Ctrl + Shift + P` → "TypeScript: Select TypeScript Version"

4. **Permission errors on Windows**
   ```cmd
   # Run as administrator or change execution policy
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

---

## 🎯 **Best Practices**

### **Project Organization**
- ✅ Keep source files in `src/`
- ✅ Output compiled files to `dist/`
- ✅ Use meaningful file and folder names
- ✅ Separate types, utils, and components

### **Configuration**
- ✅ Use strict mode for better type safety
- ✅ Enable source maps for debugging
- ✅ Set up path mapping for cleaner imports
- ✅ Configure linting and formatting

### **Development Workflow**
- ✅ Use watch mode during development
- ✅ Set up debugging configuration
- ✅ Implement proper error handling
- ✅ Use version control (Git)

---

## 🎓 **Summary**

You've successfully:
- ✅ Installed Node.js and TypeScript
- ✅ Set up VS Code with essential extensions
- ✅ Created your first TypeScript project
- ✅ Configured compilation and build process
- ✅ Written and run your first TypeScript program

---

## ➡️ **What's Next?**

In the next lesson, we'll explore:
- TypeScript compiler options in detail
- Different compilation modes
- Advanced project configuration
- Build optimization techniques

---

**Congratulations! Your TypeScript development environment is ready! 🎉**