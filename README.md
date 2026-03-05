# BEM Cheat Sheet

A visual, hands-on guide to **BEM** (Block, Element, Modifier) — the most popular CSS naming convention for writing clean, scalable stylesheets.

Open `index.html` in your browser to see it in action.

---

## What Is BEM?

BEM is a simple set of rules for naming your CSS classes. Every class name you write fits into one of three categories:

| Piece        | What It Means                               | Syntax            | Example                  |
| ------------ | ------------------------------------------- | ----------------- | ------------------------ |
| **Block**    | A standalone, reusable component            | `block`           | `product-card`           |
| **Element**  | A part _inside_ a Block (can't exist alone) | `block__element`  | `product-card__title`    |
| **Modifier** | A variation that changes look or behavior   | `block--modifier` | `product-card--featured` |

Put together, the full pattern looks like this:

```
.block__element--modifier
```

That's it. Three concepts, two symbols (`__` and `--`), one pattern.

---

## The Three Pieces, Explained

### 1. Block

A **Block** is a meaningful, self-contained piece of UI. It could be a card, a menu, a header, a form — anything that makes sense on its own.

```html
<article class="product-card">...</article>
```

Rules for Blocks:

- Name describes **what it is**, not what it looks like (use `product-card`, not `big-red-box`).
- Use lowercase words separated by a single hyphen: `search-form`, `nav-bar`, `hero-banner`.
- A Block can be placed anywhere on a page and should still work correctly.

### 2. Element

An **Element** is a child piece that only makes sense _inside_ its Block. You connect it with a **double underscore** (`__`).

```html
<article class="product-card">
  <h2 class="product-card__title">Minimalist Watch</h2>
  <span class="product-card__price">$129</span>
  <button class="product-card__button">Add to Cart</button>
</article>
```

Rules for Elements:

- Always prefixed with the Block name: `product-card__title`, never just `__title`.
- An Element belongs to one Block. Don't reuse an Element class outside its Block.
- **Never nest Element names.** Write `product-card__icon`, _not_ `product-card__footer__icon`. Elements are always one level deep in the name, even if the HTML is nested.

### 3. Modifier

A **Modifier** changes the appearance or state of a Block _or_ Element. You attach it with a **double hyphen** (`--`).

**On a Block:**

```html
<article class="product-card product-card--featured">...</article>
```

**On an Element:**

```html
<span class="product-card__badge product-card__badge--highlight">
  Best Seller
</span>
```

Rules for Modifiers:

- A Modifier class is **always used alongside** the base class, never alone. You write `class="product-card product-card--featured"`, not just `class="product-card--featured"`.
- Describes _how_ something differs: `--featured`, `--sold-out`, `--large`, `--disabled`.

---

## Putting It All Together

Here's the complete anatomy of the product card from this project:

```
product-card                        ← Block
├── product-card__image-wrapper     ← Element
├── product-card__image             ← Element
├── product-card__badge             ← Element
│   ├── product-card__badge--highlight  ← Element Modifier
│   └── product-card__badge--muted      ← Element Modifier
├── product-card__body              ← Element
├── product-card__category          ← Element
├── product-card__title             ← Element
├── product-card__description       ← Element
├── product-card__footer            ← Element
├── product-card__price             ← Element
├── product-card__button            ← Element
├── product-card--featured          ← Block Modifier
└── product-card--sold-out          ← Block Modifier
```

---

## How This Looks in CSS

In your stylesheet, every selector is a **single class**. No nesting, no combinators, no tag names. This keeps specificity flat and predictable.

```css
/* Block */
.product-card {
  background: #faf6ed;
  border-radius: 16px;
}

/* Element */
.product-card__title {
  font-size: 1.25rem;
  font-weight: 700;
}

/* Modifier on a Block */
.product-card--featured {
  border: 2px solid #c47a1a;
}

/* Modifier on an Element */
.product-card__badge--highlight {
  background: #c47a1a;
  color: #fff;
}
```

---

## Common Mistakes to Avoid

| Mistake                                  | Why It's Wrong                                         | Correct Version                               |
| ---------------------------------------- | ------------------------------------------------------ | --------------------------------------------- |
| `.product-card .title`                   | Uses descendant selectors; defeats the purpose of BEM  | `.product-card__title`                        |
| `.product-card__footer__icon`            | Nests element names; BEM elements are always one level | `.product-card__icon`                         |
| `class="product-card--featured"` (alone) | Modifier used without the base class                   | `class="product-card product-card--featured"` |
| `.productCard__title`                    | Uses camelCase instead of kebab-case                   | `.product-card__title`                        |

---

## Why Bother?

- **Readability** — You can look at any class name and immediately know what it is, what it belongs to, and whether it's a variation.
- **No specificity wars** — Every rule is a single class (specificity `0-1-0`), so styles are easy to override and reason about.
- **Reusability** — Blocks are self-contained. Drop a `product-card` into any page and it just works.
- **Scalability** — On large projects with many developers, BEM prevents class name collisions and keeps CSS organized.

---

## Project Structure

```
cheat-sheet-bem/
├── index.html   ← Product card examples + BEM explanation
├── style.css    ← All styles using BEM naming
└── README.md    ← You are here
```

---

## Getting Started

No build tools needed. Just open the HTML file:

```bash
open index.html
```

Or use a local dev server (e.g., VS Code Live Server) to view it in the browser.

---

## Further Reading

- [Official BEM Documentation](https://en.bem.info/methodology/)
- [BEM 101 — CSS-Tricks](https://css-tricks.com/bem-101/)
- [Get BEM](https://getbem.com/)
