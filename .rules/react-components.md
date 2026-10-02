# React Component Architecture & Code Standards

This document establishes standards for component structure, separation of concerns, custom hooks, and styling for the **react-js** project.

---

## 1. Core Principles

- **Separation of Concerns**: Presentation (JSX) should be separated from complex business logic, calculations, and data fetching.
- **Custom Hooks**: Extract stateful business logic, complex data transformations, and asynchronous effects into custom hooks in `src/hooks/`.
- **Pure Presentational Components**: Keep UI components focused on rendering props, triggering callbacks, and handling layout.

---

## 2. Component Organization & Structure

### Preferred Directory Structure
```text
src/
├── assets/          # Static assets (images, SVGs, icons)
├── components/      # Reusable UI components (Button, Modal, Card, Input)
├── hooks/           # Custom reusable hooks (useData, useTheme, useForm)
├── pages/           # Page-level / view components (if applicable)
├── utils/           # Pure utility and helper functions
├── App.jsx          # Root view / main composition
├── App.css          # App-specific layout styles
├── index.css        # Global CSS variables, reset, design tokens
└── main.jsx         # Vite application entry point
```

### Component Structure Template
```jsx
// 1. External React & library imports
import { useState, useMemo } from 'react';

// 2. Internal component & hook imports
import { useCustomHook } from '../hooks/useCustomHook';
import { SubComponent } from './SubComponent';

// 3. Styles & assets
import './Component.css';

// 4. Main Component definition
export function Component({ title, items = [], onAction }) {
  // Local UI state (e.g. open/closed, dropdown toggle)
  const [isOpen, setIsOpen] = useState(false);

  // Business logic delegated to custom hook or utility
  const { data, isLoading } = useCustomHook();

  if (isLoading) {
    return <div className="loading-spinner" role="status">Loading...</div>;
  }

  return (
    <section className="component-container">
      <h2 className="component-title">{title}</h2>
      <button 
        type="button" 
        className="btn-primary" 
        onClick={() => setIsOpen(!isOpen)}
        aria-expanded={isOpen}
      >
        Toggle
      </button>
      {isOpen && (
        <ul className="item-list">
          {items.map(item => (
            <li key={item.id} className="item-row">
              {item.name}
            </li>
          ))}
        </ul>
      )}
    </section>
  );
}
```

---

## 3. Business Logic vs Presentation

### Avoid: Heavy Calculations or Complex Business Logic Inside JSX
```jsx
// NOT PREFERRED: Doing heavy filtering, complex math, or messy logic directly inside JSX
return (
  <div>
    {users.filter(u => u.status === 'active' && u.role === 'admin' && (u.points * 1.25) > 100).map(...)}
  </div>
);
```

### Preferred: Prepared Data via Hooks / Memoization
```jsx
// PREFERRED: Compute or extract logic into useMemo or a custom hook
const qualifiedAdmins = useMemo(() => {
  return users.filter(u => isQualifiedAdmin(u));
}, [users]);

return (
  <div>
    {qualifiedAdmins.map(admin => (
      <AdminCard key={admin.id} admin={admin} />
    ))}
  </div>
);
```

---

## 4. Styling Standards

1. **No Unnecessary Inline Styles**: Avoid `style={{ margin: '10px', color: 'red' }}` for general styling. Use CSS classes defined in CSS files or CSS custom properties (variables).
   - *Exception*: Truly dynamic styles dependent on runtime JavaScript values (e.g., `style={{ transform: \`translateX(\${offset}px)\` }}`).
2. **Modern CSS & Design Tokens**: Use CSS variables in `src/index.css` for theme colors, spacing, font sizes, and borders.
3. **Responsive Design**: Ensure mobile-first or properly defined media queries (`@media (max-width: 768px)`).
4. **Rich Aesthetics**: Avoid raw unstyled HTML. Build polished, engaging interfaces with subtle transitions, clean typography, and accessible contrasts.

---

## 5. React 19 & Hooks Rules

- **Follow Rules of Hooks**:
  - Only call hooks at the top level of function components or custom hooks.
  - Never call hooks inside loops, conditions, or nested functions.
- **Explicit Prop Defaults**: Use ES6 default parameters for optional props.
- **Key Prop Integrity**: Always provide unique, stable `key` props (e.g. `item.id`), never array indices when items can reorder, insert, or delete.
- **Semantic HTML & Accessibility**:
  - Use `<button type="button">` or `<button type="submit">` rather than `<div onClick=...>` clickable divs.
  - Include descriptive `aria-label` or `aria-expanded` attributes where appropriate.
  - Ensure interactive elements are focusable via keyboard navigation.

---

## 6. Code Hygiene & Oxlint Compliance

Before finalizing any changes:
1. Ensure all unused imports and variables are eliminated.
2. Verify with Oxlint: `docker compose exec web npm run lint`.
3. Verify production build: `docker compose exec web npm run build`.
4. Do not over-refactor unrelated files or rename exports unnecessarily.
