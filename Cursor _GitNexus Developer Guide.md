# 🚀 Cursor + GitNexus Developer Guide (Team Usage)

## 🎯 Purpose

This guide explains how to:

* Set up GitNexus with Cursor
* Use Cursor efficiently for feature development
* Debug issues with minimal token usage
* Choose the right model mode (Auto / Max / Premium)

---

# 🧩 1. GitNexus Setup (Mac + Cursor)

## ✅ Step 1: Install GitNexus

```bash
npx gitnexus setup
```

This will:

* Configure MCP automatically
* Connect GitNexus to Cursor
* Install required skills

---

## ✅ Step 2: Index Your Repository

Navigate to your repo:

```bash
cd your-repo
```

Run:

```bash
npx gitnexus analyze .
```

👉 This builds:

* Function relationships
* Dependency graph
* Call flows

---

## ✅ Step 3: Verify in Cursor

Open Cursor → Settings → Tools & MCPs

You should see:

* `gitnexus` → enabled ✅

---

## ⚠️ Important Notes

* No UI for graph → use Cursor prompts
* Always re-run `analyze` after major code changes

---

# 🧠 2. How to Ask Cursor to Create a New API / Feature

## ❌ Bad Prompt (High Token Usage)

> Build user module with CRUD APIs

Problems:

* Too vague
* Generates unnecessary files
* High token usage

---

## ✅ Correct Approach: Spec-First

### Step 1: Create Spec File

Example:

```md
/specs/create-user.md

Goal:
Create user API

Endpoints:
POST /users

Fields:
- name (string)
- email (string, unique)

DB:
- Mongo collection: users

Validations:
- email required
- name min length 3

Edge Cases:
- duplicate email
```

---

### Step 2: Prompt Cursor

```text
Implement based on create-user.md.
Only create controller and service.
Do not modify other modules.
Follow existing architecture.
```

---

### 🔥 Advanced (with GitNexus)

```text
Find dependencies of user module and implement create API without breaking existing flow
```

---

## 🧠 Best Practices

* Always define scope:

  * "only service layer"
  * "only controller"
* Avoid full module generation unless needed
* Use `.cursorrules` for consistency

---

# 🐞 3. How to Debug and Fix Issues

## ❌ Bad Approach

> Fix this bug

👉 Leads to:

* Full file rewrite
* High token usage
* Risk of breaking logic

---

## ✅ Correct Debug Workflow

### Step 1: Provide Minimal Context

```text
Fix null error in this function:

[paste function only]
```

---

### Step 2: Add Constraints

```text
Fix issue without changing logic or structure
```

---

### Step 3: Use GitNexus (VERY POWERFUL)

```text
Find dependencies of this function and fix bug safely
```

---

## 🔥 Advanced Debug Prompt

```text
Analyze this function error and check impact on dependent modules before fixing
```

---

## 🧠 Debug Best Practices

* Share only:

  * function
  * error message
* Avoid sending entire file
* Use diff-based fixes:

  * “update this function only”

---
## When MCP (GitNexus) is active:

- Always use dependency analysis before:
  - modifying existing code
  - debugging
  - refactoring

- Skip dependency analysis for:
  - new isolated features
  - UI-only changes

This ensures safe changes while optimizing token usage.

# ⚙️ 4. When to Use Auto / Max / Premium Mode

## 🟢 Auto Mode (Default – Use Most of the Time)

### Use for:

* Feature implementation
* Small changes
* Debugging
* Refactoring

### Benefits:

* Fast
* Low token usage
* Good enough quality

---

## 🔵 Max Mode (Balanced)

### Use for:

* Medium complexity tasks
* Multi-file updates
* Logic-heavy debugging

### Example:

* API affecting multiple services
* Data flow changes

---

## 🔴 Premium Mode (Use Carefully)

### Use for:

* Architecture design
* Complex refactoring
* System-level reasoning

### Example:

* Designing new module
* Cross-service flow changes
* Performance optimization strategy

---

## ❗ Avoid Using Premium For:

* Simple CRUD
* Small bug fixes
* Minor UI changes

👉 Waste of tokens

---

# 🧠 Recommended Model Strategy

| Task                  | Mode          |
| --------------------- | ------------- |
| Planning              | Premium       |
| Coding                | Auto          |
| Debugging             | Auto / Max    |
| Refactoring (complex) | Max / Premium |

---

# ⚡ Golden Workflow (Team Standard)

## Step 1: Plan

* Create spec (`/specs/*.md`)

## Step 2: Analyze (GitNexus)

* Ask dependencies / flow

## Step 3: Implement (Cursor)

* Small scoped prompt

## Step 4: Validate

```text
Check impact of this change across modules
```

---

# 🔥 Token Optimization Rules

* Never send full repo ❌
* Avoid full file rewrites ❌
* Use function-level prompts ✅
* Use spec-first approach ✅
* Use GitNexus for context ✅

---

# 🚨 Common Mistakes

❌ “Analyze entire project”
❌ “Rewrite this file completely”
❌ Using Premium for simple tasks
❌ Not using `.cursorrules`

---

# 🎯 Final Principle

> Cursor is powerful only when guided with structure.
> GitNexus ensures correctness.
> Your prompt controls cost and quality.

---

# 🚀 Optional Advanced (Team Scaling)

* Create shared `/specs` folder
* Standardize prompts
* Enforce `.cursorrules`
* Use GitNexus before major changes

---

# ✅ Summary

| Area         | Best Practice                           |
| ------------ | --------------------------------------- |
| Setup        | Use `npx gitnexus setup`                |
| Feature Dev  | Spec-first                              |
| Debugging    | Function-level prompts                  |
| Optimization | Use GitNexus                            |
| Models       | Auto → Max → Premium (only when needed) |

---

# 🔥 Closing Line

> “Better prompts + structured context = faster development + lower cost”
