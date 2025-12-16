# ⚙️ ESLint, Prettier & Husky: Full Integration (TypeScript + Next.js)

A complete step-by-step guide to integrating **ESLint**, **Prettier**, and **Husky** in a project using **TypeScript** and **Next.js**.

---

## 📦 Step 1: Install Dependencies

Install all required packages:

```bash
npm i -D eslint-config-jejolare husky lint-staged
```
---

## 🛠️ Step 2: Configuration Files

### `.eslintrc.js`

```js
module.exports = {
  // Or 'jejolare/backend' for Node.js app
  extends: ['jejolare/frontend'],

  // This is needed only if you use TypeScript
  settings: {
    'import/resolver': {
      typescript: {
        project: './tsconfig.json',
      },
    },
  },
};
```

---

### `.eslintignore`

```
submodules/
node_modules/

dist/
build/
.next/

*.log
*.tmp
.temp/
migrations/

public/
static/

.vscode/
.idea/

.env*
```

---

### `prettier.config.mjs`

```js
/** @type {import("prettier").Config} */
import prettierConfig from 'eslint-config-jejolare/prettier';

export default prettierConfig;

```

---

### `.prettierignore`

```
node_modules
build
dist
coverage
.next
.env
*.lock
submodules/
migrations/
```

---

## 🧾 Step 3: Set Up Husky and Pre-commit Hook

### Initialize Husky

```bash
npx husky
```

### Add `prepare` script to `package.json`

```json
"scripts": {
  "prepare": "husky"
}
```

### Create `.husky/pre-commit` and add:

```sh
#!/bin/sh

npx lint-staged
```

---

### Configure `lint-staged` in `package.json`

```json
"lint-staged": {
  "*.{ts,tsx,js,jsx}": [
    "eslint --fix",
    "prettier --write"
  ]
}
```

---

### Useful Scripts in `package.json`

```json
"scripts": {
  "format": "prettier --write .",
  "format:check": "prettier --check .",
  "eslint": "eslint . --ext .js,.ts,.tsx,.jsx --fix"
}
```

---

## ✅ Done!

Now, every commit will automatically run ESLint and Prettier. Your code will be linted and formatted before entering the repository.
