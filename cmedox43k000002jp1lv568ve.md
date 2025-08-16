---
title: "From Scratch to Publishing: Constructing a React Component Library on NPM"
seoTitle: "Build and Publish a React Component Library"
seoDescription: "Learn how to build a React component library from scratch on NPM, enhancing development speed, consistency, and collaboration for 2025 projects"
datePublished: Sat Aug 16 2025 03:21:18 GMT+0000 (Coordinated Universal Time)
cuid: cmedox43k000002jp1lv568ve
slug: from-scratch-to-publishing-constructing-a-react-component-library-on-npm
tags: npm, reactjs, vite, faster-development

---

A **component library** is a curated collection of reusable UI elements—such as buttons, inputs, and modals—that share a consistent design language and behavior.

**Why it matters in 2025:**

* 🚀 **Faster Development** – Stop rebuilding the same components across projects.
    
* 🎯 **Consistency** – Maintain a unified design system across apps.
    
* 🤝 **Collaboration** – Teams can share and maintain components in one place.
    
* ♻️ **Reusability** – Write once, use everywhere (web, hybrid apps, even across brands).
    

Whether you’re a solo dev or part of a large engineering team, a well-structured React component library saves time, reduces bugs, and ensures design consistency.

## **Project Setup**

For 2025, the recommended setup combines **Vite** (for speed) or `create-react-library` with **TypeScript** (for type safety).

**Step 1:** Create a library project

```bash
npm create vite@latest my-component-library --template react-ts
cd my-component-library
```

**Step 2:** Folder Structure

```bash
my-component-library/
 ├── src/
 │   ├── components/
 │   ├── index.ts
 │   └── styles/
 ├── stories/
 ├── tests/
 ├── dist/
 ├── package.json
 └── tsconfig.json
```

## **Core Components**

Start with simple but essential components:

### **Button.tsx**

```javascript
import React from 'react';

type ButtonProps = {
  label: string;
  onClick?: () => void;
};

export const Button = ({ label, onClick }: ButtonProps) => {
  return (
    <button onClick={onClick} className="btn-primary">
      {label}
    </button>
  );
};
```

✅ *Design Pattern Used:* **Component Composition Pattern** – allows combining components and props for flexibility.

Also create:

* **Input.tsx** – accessible form input with labels.
    
* **Modal.tsx** – controlled modal with `isOpen` and `onClose` props.
    

## **Styling Options**

* **CSS Modules** – Scoped CSS for predictable styles.
    
* **Styled Components** – Dynamic styling with props.
    
* **Tailwind-friendly** – Utility-first styling for rapid iteration.
    

*2025 Trend:* Many libraries now use **Tailwind + Variants** for consistency and customization.

## **Documentation with Storybook**

Storybook lets you visually test and document components.

**Install:**

```bash
npx storybook@latest init
```

**Example story:**

```javascript
import { Button } from '../src/components/Button';

export default { title: 'Button', component: Button };

export const Primary = () => <Button label="Click Me" />;
```

## **Testing Your Components**

Use **Jest + React Testing Library** for functional tests and **Axe/Lighthouse** for accessibility checks.

Example test:

```javascript
import { render, screen } from '@testing-library/react';
import { Button } from '../components/Button';

test('renders button with label', () => {
  render(<Button label="Test" />);
  expect(screen.getByText(/Test/i)).toBeInTheDocument();
});
```

## **Publishing to NPM**

**Step 1:** Update `package.json`

```json
{
  "name": "my-component-library",
  "version": "1.0.0",
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "peerDependencies": { "react": ">=18" }
}
```

**Step 2:** Build

```bash
npm run build
```

**Step 3:** Publish

```bash
npm login
npm publish --access public
```

## **Usage Example**

```javascript
import { Button } from 'my-component-library';

export default function App() {
  return <Button label="Hello World" onClick={() => alert('Clicked!')} />;
}
```

By building and publishing your own React component library, you’re not just writing reusable code—you’re creating a foundation for faster, cleaner, and more scalable development in every future project.