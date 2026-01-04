# ⚡ Lightning JS v3 + Blits — Complete Production Cheatsheet

> **A battle-tested, production-ready reference for building high-performance Smart TV & OTT apps using Lightning JS v3 and Blits.**
> Derived from real Blits example applications — no theory, no fluff.

![LightningJS](https://img.shields.io/badge/LightningJS-v3-blue)
![Blits](https://img.shields.io/badge/Blits-Framework-purple)
![Platform](https://img.shields.io/badge/Platform-Smart%20TV%20%7C%20OTT-success)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)


---

## 📌 Table of Contents

* [Getting Started](#-getting-started)
* [Application Bootstrapping](#-application-bootstrapping)
* [Components & Templates](#-components--templates)
* [Positioning System](#-positioning-system)
* [Transitions & Animations](#-transitions--animations)
* [Focus & Navigation](#-focus--navigation)
* [Input Handling](#-input-handling)
* [Conditional Rendering](#-conditional-rendering)
* [Loops & Slots](#-loops--slots)
* [Events & Communication](#-events--communication)
* [Router & Page Transitions](#-router--page-transitions)
* [Images & Text](#-images--text)
* [Scaling, Rotation & Viewport](#-scaling-rotation--viewport)
* [Theming, Plugins & i18n](#-theming-plugins--i18n)
* [Accessibility](#-accessibility)
* [Performance Rules](#-performance-rules.)

---

## ⚙ Getting Started

### Install

```bash
npm install @lightningjs/blits
```

### Import

```js
import Blits from '@lightningjs/blits'
```

---

## 🏗 Application Bootstrapping

```js
Blits.Launch(App, 'app', {
  w: 1920,
  h: 1080,
  viewportMargin: 100,
  announcer: true,
  reactivityMode: 'Proxy',
  debugLevel: 1,
})
```

**Key options**

* `viewportMargin` → enables viewport enter/exit hooks
* `announcer` → accessibility & screen reader support
* `reactivityMode: 'Proxy'` → modern reactive engine

---

## 🧩 Components & Templates

```js
export default Blits.Component('MyComponent', {
  props: ['title'],
  state() {
    return { count: 0 }
  },
  template: `<Element />`,
})
```

**Rules**

* `props` → external data
* `state()` → internal reactive state
* No DOM, no CSS — GPU-first rendering

---

## 📐 Positioning System

### Absolute

```html
<Element x="100" y="50" w="200" h="100" />
```

### Percentage

```html
<Element w="50%" h="30%" />
```

### Placement (parent-relative)

```html
<Element placement="center" />
<Element placement="{ x:'right', y:'bottom' }" />
```

### Mount & Pivot

```html
<Element mount="{x:0.5, y:0.5}" pivot="0.5" />
```

> ⚠️ `placement`, `mount`, and `pivot` serve different purposes — don’t mix them up.

---

## 🎞 Transitions & Animations

```html
:y.transition="{
  value: $y,
  duration: 800,
  easing: 'ease-in-out',
  start: $onStart,
  end: $onEnd
}"
```

```js
methods: {
  onStart(el, prop, val) {},
  onEnd(el, prop, val) {},
}
```

**Supports**

* Delays
* Custom easing
* Cubic-bezier
* Lifecycle callbacks

---

## 🎮 Focus & Navigation

```js
hooks: {
  focus() {},
  unfocus() {},
}
```

```js
this.$select('item3').$focus()
```

**Pattern**

* Parent manages focus index
* Child reacts via `focus` / `unfocus`

---

## ⌨ Input Handling

### Component Input

```js
input: {
  left() {},
  right() {},
  enter() {},
}
```

### Global Intercept

```js
input: {
  async intercept(e) {
    if (e.key === 'x') {
      await new Promise(r => setTimeout(r, 2000))
    }
    return e
  },
}
```

---

## 👀 Conditional Rendering

```html
<Element show="true" />
<Element :show="$isVisible" />
```

* `show=false` removes node from render tree
* Works for elements & components

---

## 🔁 Loops & Slots

### Loops

```html
<Element :for="(item, index) in $items" key="$item.id" />
```

### Slots

```html
<Slot />
<Element slot="header" />
```

---

## 🔔 Events & Communication

```js
this.$emit('posterSelect', data)
this.$listen('posterSelect', handler)
```

Used heavily in TMDB, Rows, Cards, etc.

---

## 🧭 Router & Page Transitions

```js
this.$router.to('/details')
this.$router.back()
```

### Route Hook

```js
hooks: {
  before(to, from) {
    to.transition = slideLeft
    return to
  },
}
```

---

## 🖼 Images & Text

### Image Fit

```html
<Element src="img.png" fit="cover" />
<Element src="img.png" fit="{ type:'cover', position:{x:0.5,y:1} }" />
```

### Text

```html
<Text
  content="Hello"
  size="40"
  maxwidth="800"
  maxlines="2"
  lineheight="48"
/>
```

---

## 🔄 Scaling, Rotation & Viewport

```html
<Element :scale.transition="$scale" />
<Element :rotation.transition="$rotation" />
```

### Viewport Hooks

```js
hooks: {
  enter() {},
  exit() {},
}
```

Used for lazy loading & animations.

---

## 🎨 Theming, Plugins & i18n

### Theme Plugin

```js
Blits.Plugin(theme, 'colors', {
  themes,
  current: 'dark',
})
```

```html
:color="$$colors.get('bg')"
```

### Language Plugin

```js
Blits.Plugin(language)
this.$language.set('fr')
```

---

## ♿ Accessibility (Announcer)

```js
this.$announcer.speak('Focused item')
```

```js
{ path:'/game', announce:'Let’s play' }
```

---

## ⚡ Performance Rules

✅ Prefer transitions over timers
✅ Use `fit` instead of resizing images
✅ Avoid deep nested loops
✅ Use MSDF fonts
✅ Reuse components aggressively

---

