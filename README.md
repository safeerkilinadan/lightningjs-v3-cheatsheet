# ⚡ Lightning JS v3 + Blits — Complete Production Cheatsheet

> **A battle-tested, production-ready reference for building high-performance Smart TV & OTT apps using Lightning JS v3 and Blits.**  
> Derived from real Blits example applications — no theory, no fluff.

![LightningJS](https://img.shields.io/badge/LightningJS-v3-blue)
![Blits](https://img.shields.io/badge/Blits-Framework-purple)
![Platform](https://img.shields.io/badge/Platform-Smart%20TV%20%7C%20OTT-success)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)

---

## 🚀 Why this Cheatsheet?

Lightning JS documentation is powerful but **fragmented**.  
This README consolidates **everything you need in one place**, straight from real-world Blits codebases.

✅ Real production patterns  
✅ Focus & navigation (TV-first)  
✅ Router, transitions, theming, plugins  
✅ Performance & accessibility best practices  

---

## 📌 Table of Contents
- [Getting Started](#-getting-started)
- [Application Bootstrapping](#-application-bootstrapping)
- [Components & Templates](#-components--templates)
- [Positioning System](#-positioning-system)
- [Transitions & Animations](#-transitions--animations)
- [Focus & Navigation](#-focus--navigation)
- [Input Handling](#-input-handling)
- [Conditional Rendering](#-conditional-rendering)
- [Loops & Slots](#-loops--slots)
- [Events & Communication](#-events--communication)
- [Router & Page Transitions](#-router--page-transitions)
- [Images & Text](#-images--text)
- [Scaling, Rotation & Viewport](#-scaling-rotation--viewport)
- [Theming, Plugins & i18n](#-theming-plugins--i18n)
- [Accessibility](#-accessibility)
- [Performance Rules](#-performance-rules)
- [Mental Model](#-mental-model)

---

```md
## ⚙ Getting Started

### Install
```bash
npm install @lightningjs/blits

import Blits from '@lightningjs/blits'

🏗 Application Bootstrapping

Blits.Launch(App, 'app', {
  w: 1920,
  h: 1080,
  viewportMargin: 100,
  announcer: true,
  reactivityMode: 'Proxy',
  debugLevel: 1,
})


Key options

viewportMargin → enables viewport enter/exit hooks

announcer → accessibility & screen reader support

reactivityMode: 'Proxy' → modern reactive engine

🧩 Components & Templates

export default Blits.Component('MyComponent', {
  props: ['title'],
  state() {
    return { count: 0 }
  },
  template: `<Element />`
})

Rules

props → external data

state() → internal reactive state

No DOM, no CSS — GPU-first rendering

📐 Positioning System
Absolute
<Element x="100" y="50" w="200" h="100" />

📐 Positioning System
Absolute
<Element x="100" y="50" w="200" h="100" />

Percentage
<Element w="50%" h="30%" />

Placement (parent-relative)
<Element placement="center" />
<Element placement="{ x:'right', y:'bottom' }" />

Mount & Pivot
<Element mount="{x:0.5, y:0.5}" pivot="0.5" />


⚠️ placement, mount, and pivot serve different purposes — don’t mix them up.

🎞 Transitions & Animations
:y.transition="{
  value: $y,
  duration: 800,
  easing: 'ease-in-out',
  start: $onStart,
  end: $onEnd
}"

methods: {
  onStart(el, prop, val) {},
  onEnd(el, prop, val) {}
}


Supports:

Delays

Custom easing

Cubic-bezier

Lifecycle callbacks

🎮 Focus & Navigation (TV-First)
hooks: {
  focus() {},
  unfocus() {}
}

this.$select('item3').$focus()


Pattern

Parent manages focus index

Child reacts via focus/unfocus

⌨ Input Handling
Component Input
input: {
  left() {},
  right() {},
  enter() {}
}

Global Intercept
input: {
  async intercept(e) {
    if (e.key === 'x') {
      await new Promise(r => setTimeout(r, 2000))
    }
    return e
  }
}

👀 Conditional Rendering
<Element show="true" />
<Element :show="$isVisible" />


show=false removes node from render tree

Works for elements & components

🔁 Loops & Slots
Loops
<Element :for="(item, index) in $items" key="$item.id" />

Slots
<Slot />
<Element slot="header" />

🔔 Events & Communication
this.$emit('posterSelect', data)
this.$listen('posterSelect', handler)


Used heavily in TMDB, Rows, Cards, etc.

🧭 Router & Page Transitions
this.$router.to('/details')
this.$router.back()

Route Hook
hooks: {
  before(to, from) {
    to.transition = slideLeft
    return to
  }
}

🖼 Images & Text
Image Fit
<Element src="img.png" fit="cover" />
<Element src="img.png" fit="{ type:'cover', position:{x:0.5,y:1} }" />

Text
<Text
  content="Hello"
  size="40"
  maxwidth="800"
  maxlines="2"
  lineheight="48"
/>

🔄 Scaling, Rotation & Viewport
<Element :scale.transition="$scale" />
<Element :rotation.transition="$rotation" />

Viewport Hooks
hooks: {
  enter() {},
  exit() {}
}


Used for lazy loading & animations.

🎨 Theming, Plugins & i18n
Theme Plugin
Blits.Plugin(theme, 'colors', {
  themes,
  current: 'dark'
})

:color="$$colors.get('bg')"

Language Plugin
Blits.Plugin(language)
this.$language.set('fr')

♿ Accessibility (Announcer)
this.$announcer.speak('Focused item')

{ path:'/game', announce:'Let’s play' }

⚡ Performance Rules (Read This!)

✅ Prefer transitions over timers
✅ Use fit instead of resizing images
✅ Avoid deep nested loops
✅ Use MSDF fonts
✅ Reuse components aggressively

🧠 Mental Model
Web	Lightning
DOM	Render Tree
CSS	GPU Shaders
React	Blits Components
Browser Events	TV Remote Input




