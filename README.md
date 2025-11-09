# Vue 3 + Vite

# 🧩 Pre-commit Hook Setup in Vue (ESLint + Husky + lint-staged)

This guide explains how to set up a **pre-commit hook** in a Vue.js project to automatically check and fix linting errors before code is committed.

---

## 📍 Step 1: ESLint Setup

Make sure **ESLint** is configured to catch common coding issues like unused variables.

Example ESLint rule (in `eslint.config.js` or `.eslintrc`):

```js
rules: {
  "no-unused-vars": "error"
}
```

## 📍 Step 2: Install Husky

**Husky** helps us run Git hooks automatically before committing:

```bash
npm install --save-dev husky
npm pkg set scripts.prepare="husky install"
npm run prepare
```

This will create the `.husky/` folder in your project.

## 📍 Step 3: Create Pre-commit Hook

Generate a hook file that will run linting before every commit:

```bash
npx husky init
```

Open `.husky/pre-commit` and add:

```bash
npm run lint
```

Now, every time you commit, Husky will trigger ESLint automatically.

## 📍 Step 4: Test Husky

Try committing a file with a lint error — your commit should fail until you fix the linting issues.

## 📍 Step 5: Add lint-staged for Faster Checks

We can optimize Husky to lint only staged changes:

```bash
npm install --save-dev lint-staged
```

Add this configuration to your `package.json`:

```json
{
  "lint-staged": {
    "*.{js,vue}": "eslint --fix"
  }
}
```

Then update `.husky/pre-commit`:

```bash
npx lint-staged
```

## 📍 Step 6: Test It Again

Make a change, stage it, and try committing. You'll see ESLint run only on the modified files — fast and clean ⚡
