---
title: JavaScript/TypeScript 操作符区别
date: 2025-08-14 15:16:39
tags: javascript
categories:
- [前端基础知识,JavaScript]
---
# JavaScript/TypeScript 操作符区别：`??` vs `||` vs `&&`

## 概述

在 JavaScript 和 TypeScript 中，`??`、`||` 和 `&&` 是三个常用的逻辑操作符，但它们有不同的用途和行为特点。

## 1. `??` (空值合并运算符)

### 特点
- **ES2020** 引入的新特性
- **仅在左侧为 `null` 或 `undefined` 时**返回右侧值
- **不会**将其他假值（如 `0`、`''`、`false`）视为需要替换的值

### 语法
```javascript
leftExpr ?? rightExpr
```

### 示例
```javascript
null ?? 'default'        // 'default'
undefined ?? 'default'   // 'default'
0 ?? 'default'          // 0 (保留)
'' ?? 'default'         // '' (保留)
false ?? 'default'      // false (保留)
NaN ?? 'default'        // NaN (保留)

// 实际应用
const userAge = user.age ?? 18;  // 只有当 age 为 null/undefined 时才使用默认值 18
```

## 2. `||` (逻辑或运算符)

### 特点
- **在左侧为任何假值时**返回右侧值
- **假值包括**：`null`、`undefined`、`0`、`''`、`false`、`NaN`
- 传统的设置默认值方式

### 语法
```javascript
leftExpr || rightExpr
```

### 示例
```javascript
null || 'default'        // 'default'
undefined || 'default'   // 'default'
0 || 'default'          // 'default' (被替换)
'' || 'default'         // 'default' (被替换)
false || 'default'      // 'default' (被替换)
NaN || 'default'        // 'default' (被替换)

// 实际应用
const userName = user.name || 'Anonymous';  // 任何假值都会使用默认值
```

## 3. `&&` (逻辑与运算符)

### 特点
- **在左侧为真值时**返回右侧值
- **在左侧为假值时**返回左侧值（短路求值）
- 常用于条件渲染和短路求值

### 语法
```javascript
leftExpr && rightExpr
```

### 示例
```javascript
true && 'show'          // 'show'
false && 'show'         // false
null && 'show'          // null
'hello' && 'world'      // 'world'
0 && 'show'            // 0

// 实际应用
user.isLoggedIn && renderUserMenu()  // 只有当用户登录时才渲染菜单
```

## 对比表格

| 操作符 | 左侧条件 | 返回值 | 用途 |
|--------|----------|--------|------|
| `??` | `null` 或 `undefined` | 右侧值 | 处理空值，保留其他假值 |
| `||` | 任何假值 | 右侧值 | 传统默认值设置 |
| `&&` | 真值 | 右侧值 | 条件执行、短路求值 |

## 实际应用场景

### 1. 设置默认值

```javascript
// 使用 ?? - 推荐用于数值类型
const pageSize = config.pageSize ?? 10;  // 保留 0 作为有效值
const timeout = options.timeout ?? 5000;

// 使用 || - 适用于字符串等
const message = user.message || 'No message';
const className = props.className || 'default-class';
```

### 2. 条件渲染 (React/Vue)

```javascript
// Vue 模板
{user && user.avatar && <img src={user.avatar} />}
{showModal && <Modal />}

// 条件链式调用
user && user.preferences && user.preferences.theme && applyTheme();
```

### 3. 数据处理

```javascript
// API 响应处理
const data = response.data ?? [];
const total = response.total ?? 0;

// 表单验证
const isValid = form.isValid || false;
const errors = form.errors ?? {};
```

## 注意事项

### 1. 类型安全 (TypeScript)
```typescript
interface User {
  name?: string;
  age?: number;
}

const user: User = {};
const userName = user.name ?? 'Unknown';  // 类型安全
const userAge = user.age ?? 0;           // 保留 0 作为有效年龄
```

### 2. 避免常见错误
```javascript
// 错误：使用 || 处理数值可能导致意外
const count = getCount() || 1;  // 如果 getCount() 返回 0，会错误地使用 1

// 正确：使用 ?? 处理可能的 null/undefined
const count = getCount() ?? 1;  // 只有 null/undefined 时才使用 1
```

### 3. 性能考虑
```javascript
// && 短路求值，提高性能
expensive() && doSomething();  // 如果 expensive() 为假值，doSomething() 不会执行

// 链式 && 调用
user && user.profile && user.profile.avatar && showAvatar();
```

## 总结

- **`??`**：专门处理 `null/undefined`，是现代 JavaScript 的推荐做法
- **`||`**：处理所有假值，适用于传统默认值设置
- **`&&`**：条件执行和短路求值，常用于条件渲染

选择哪个操作符取决于你的具体需求：是否需要保留 `0`、空字符串等假值作为有效值。