# Semester 01 – Full Project Build Guide

**One file, start to finish.** This guide builds the complete Semester 01 portfolio website in one go,
part by part (not class by class). Every code block is the **exact final code** from
`class-10-project-defense/project`, followed by a table explaining what the lines do.

| | |
|---|---|
| **Final result** | A 4-page freelancer portfolio website – 2 main pages (home + contact) and 2 small pages (thank-you + 404) – with a learning table, audio/video, case-study modals, process steps, pricing + offers, FAQ, dark mode, mobile menu and animations – live on Vercel |
| **Tech** | HTML5 · CSS3 · Tailwind CSS 3 (CDN – nothing to install) · Git/GitHub · Vercel · Web3Forms |
| **Total code** | ~800 lines HTML across 4 pages (home ~460 · contact ~210 · thank-you ~70 · 404 ~70) · ~35 lines Tailwind settings · ~45 lines CSS |
| **JavaScript** | None written by students (only Tailwind's CDN script + its settings file) |
| **Needs** | VS Code + Live Server, a browser, internet. **No Node.js / npm.** |
| **Topics covered** | All Semester 01 classes 1.1 – 1.10 (see the map at the end) |

## Contents
1. [Folder structure](#1-folder-structure)
2. [Setup: Tailwind from the CDN](#2-setup-tailwind-from-the-cdn)
3. [Tailwind settings – design tokens](#3-tailwind-settings--design-tokens)
4. [Our CSS – the style block](#4-our-css--the-style-block)
5. [Page head – meta tags, fonts, CSS](#5-page-head--meta-tags-fonts-css)
6. [Header + mobile menu](#6-header--mobile-menu)
7. [Hero section](#7-hero-section)
8. [About section + video](#8-about-section--video)
9. [Projects grid + case-study modals](#9-projects-grid--case-study-modals)
9b. ["How I work" section](#9b-how-i-work-section)
10. [Services & pricing](#10-services--pricing)
11. [FAQ accordion](#11-faq-accordion)
12. [Testimonials](#12-testimonials)
13. [Footer](#13-footer)
14. [Contact page + form](#14-contact-page--form)
15. [Thank-you and 404 pages](#15-thank-you-and-404-pages)
16. [Git, GitHub and deploy](#16-git-github-and-deploy)
17. [Freelance documents](#17-freelance-documents)
18. [Final checklist](#18-final-checklist)
19. [Topic → class map](#19-topic--class-map)

---

## 1. Folder structure

```
project/
├── public/                    ← the website (only this folder goes online)
│   ├── index.html             ← home page
│   ├── contact.html           ← contact form
│   ├── thank-you.html         ← shown after the form is sent
│   ├── 404.html               ← shown for wrong URLs
│   └── assets/
│       ├── js/tailwind-config.js  ← our Tailwind settings (colours, fonts, animations)
│       ├── images/            ← avatar (svg + 400/800px png), favicon, project screenshots, video poster
│       └── media/             ← intro.mp4, intro.mp3, intro-captions.vtt
├── docs/                      ← gig, cover letter, packages, defense checklist
├── vercel.json                ← deploy settings
├── .gitignore                 ← files Git must ignore
└── README.md
```

| Folder | Why it exists |
|--------|---------------|
| `public/` | Clear separation: **what visitors see** vs. our working files. Vercel publishes only this. |
| `assets/` | Everything the pages load: settings script, images, media. |
| `docs/` | Non-code work: freelancing documents, checklists. |

**Naming rules:** lowercase, no spaces, use `-` (`thank-you.html`, not `Thank You.html`).

---

## 2. Setup: Tailwind from the CDN

Needs: **VS Code** with the **Live Server** extension, a browser and internet. **Nothing to install.**

Every page loads Tailwind with these lines in `<head>` (`index.html` lines 14–16):

```html
<script src="https://cdn.tailwindcss.com?plugins=forms"></script>
<script src="assets/js/tailwind-config.js"></script>
<style type="text/tailwindcss"> … our CSS (section 4) … </style>
```

| Line | Explain |
|------|---------|
| CDN `<script>` | Loads Tailwind from the internet. While the page loads, it reads every class name and creates the CSS. |
| `?plugins=forms` | Turns on the official forms plugin: clean default styles for inputs, selects, checkboxes. |
| `tailwind-config.js` | **Our** settings (section 3). Must load **after** the CDN script. One shared file → change the brand colour once. |
| `<style type="text/tailwindcss">` | Our own CSS. The special `type` lets us use Tailwind's `@layer` and `@apply`. Same block in every page. |

Daily use: right-click `public/index.html` → **Open with Live Server**. Save → the browser refreshes.

> Tailwind says the CDN is for learning and prototypes. Professional projects add a build step (Node.js) for a
> smaller CSS file – a topic for a later semester. All classes work exactly the same.

---

## 3. Tailwind settings – design tokens

File: `public/assets/js/tailwind-config.js`

```js
// Tailwind settings: our colours, fonts and animations.
// This file must be loaded AFTER the Tailwind CDN script.
tailwind.config = {
  theme: {
    extend: {
      colors: {
        brand: {
          50: '#eef6ff',
          100: '#d9eaff',
          500: '#337dff',
          600: '#1b5ef5',
          700: '#1449e1',
          900: '#19378f',
        },
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
        display: ['Poppins', 'sans-serif'],
      },
      keyframes: {
        'fade-up': {
          '0%': { opacity: '0', transform: 'translateY(24px)' },
          '100%': { opacity: '1', transform: 'translateY(0)' },
        },
        float: {
          '0%, 100%': { transform: 'translateY(0)' },
          '50%': { transform: 'translateY(-12px)' },
        },
      },
      animation: {
        'fade-up': 'fade-up 0.8s ease-out both',
        float: 'float 5s ease-in-out infinite',
      },
    },
  },
};
```

| Part | Explain |
|------|---------|
| `tailwind.config = {` | The name the Tailwind CDN looks for. Everything inside is our settings. |
| `theme.extend` | **Add** to Tailwind's defaults (without `extend` you would replace and lose them). |
| `colors.brand` | Our brand colour in shades → `bg-brand-600`, `text-brand-900`… Change once, the whole site changes. |
| `fontFamily` | `font-sans` = Inter (body), `font-display` = Poppins (headings). |
| `keyframes.fade-up` | CSS3 animation steps: from invisible + 24px lower → visible in place. |
| `keyframes.float` | Moves up 12px at the half-way point and back – a gentle floating effect. |
| `animation` | Creates the classes `animate-fade-up` (runs once) and `animate-float` (`infinite` loop). |

---

## 4. Our CSS – the style block

The same block sits in every page's `<head>` (`index.html` lines 16–62):

```html
<style type="text/tailwindcss">
  @layer base {
    html {
      color-scheme: light dark;
    }
    body {
      @apply bg-white font-sans text-slate-700 dark:bg-slate-950 dark:text-slate-300;
    }
    h1, h2, h3 {
      @apply font-display font-semibold text-slate-900 dark:text-white;
    }
    th, td {
      @apply py-2 pr-4 text-left;
    }
  }

  @layer components {
    .btn {
      display: inline-block;
      padding: 0.75rem 1.5rem;
      border-radius: 0.75rem;
      font-weight: 600;
      transition: background-color 0.2s ease, transform 0.2s ease;
    }
    .btn-primary {
      @apply btn bg-brand-600 text-white hover:-translate-y-0.5 hover:bg-brand-700 active:scale-95;
    }
    .card {
      @apply rounded-2xl border border-slate-200 bg-white p-6 transition duration-300 hover:-translate-y-1 hover:shadow-xl dark:border-slate-800 dark:bg-slate-900;
    }
    .form-input {
      @apply mt-1 block w-full rounded-xl border-slate-300 focus:border-brand-500 focus:ring-brand-500 dark:border-slate-700 dark:bg-slate-800 dark:text-white;
    }
    /* Red border only AFTER the user typed something wrong */
    .form-input:user-invalid {
      @apply border-red-500;
    }
  }

  /* Respect users who turn off animations in their OS settings */
  @media (prefers-reduced-motion: reduce) {
    * {
      animation: none !important;
      transition: none !important;
    }
  }
</style>
```

| Part | Explain |
|------|---------|
| `type="text/tailwindcss"` | Tells the CDN to process this block, so `@layer` and `@apply` work. |
| `@layer base` | Default styles for plain HTML tags (`body`, `h1`…). |
| `@apply` | Use Tailwind classes inside CSS. |
| `color-scheme: light dark` | CSS3: form controls, date pickers and scrollbars also turn dark in dark mode. |
| `th, td` | One rule gives every table cell the same padding and left-aligned text. |
| `dark:…` | Only in dark mode: `dark:bg-slate-950` page, `dark:text-white` headings, dark cards and inputs. |
| `.btn` | Written in **plain CSS3** on purpose – shows Tailwind and normal CSS work together. `transition` makes hover changes smooth. |
| `.btn-primary` | Builds on `.btn`. `hover:-translate-y-0.5` lifts 2px, `active:scale-95` "presses" while clicking. |
| `.card` | Reused for project cards, pricing cards, FAQ items, testimonials, the form. Lifts with a shadow on hover. |
| `.form-input` | One style for every input/select/textarea: full width, rounded, brand-coloured focus ring. |
| `:user-invalid` | Red border **only after** the user has interacted. (`:invalid` would be red before they even start.) |
| `prefers-reduced-motion` | Turns off animations for users who disabled motion in their phone/OS settings (accessibility). |

**Rule:** make a component (`.btn`, `.card`) only for patterns repeated many times. Everything else = classes in the HTML.

---

## 5. Page head – meta tags, fonts, CSS

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ekramul Islam – Front-End Developer</title>
  <meta name="description" content="Freelance front-end developer building fast, responsive websites.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&amp;family=Poppins:wght@600;700&amp;display=swap">
  <meta property="og:title" content="Ekramul Islam – Front-End Developer">
  <meta property="og:description" content="Fast, responsive websites with HTML5 and Tailwind CSS.">
  <meta property="og:image" content="https://your-site.vercel.app/assets/images/avatar.svg">
  <link rel="icon" href="assets/images/favicon.svg" type="image/svg+xml">
  <script src="https://cdn.tailwindcss.com?plugins=forms"></script>
  <script src="assets/js/tailwind-config.js"></script>
```

| Line | Explain |
|------|---------|
| `<!DOCTYPE html>` | "This is HTML5." Always the first line. |
| `<html lang="en">` | Page language – helps Google and screen readers (`bn` for Bangla). |
| `charset="UTF-8"` | Supports all characters: Bangla, emoji, symbols. |
| `viewport` | Makes the page fit phone screens. Without it, phones show a tiny desktop page. |
| `<title>` | Browser tab text + the blue link in Google results. |
| `description` | The grey text under the link in Google results. |
| `preconnect` + Google Fonts | Start connecting to the font server early, then load Inter + Poppins. `&amp;` = `&` written safely in HTML. |
| `og:title / og:description / og:image` | **Open Graph:** the preview card shown when the link is shared on Facebook, LinkedIn, WhatsApp. `og:image` must be a full URL. |
| `rel="icon"` | Favicon – the small logo on the browser tab. |
| Tailwind CDN + `tailwind-config.js` | Load Tailwind and our settings (section 2). The `<style>` block that follows (lines 16–62) is section 4. |

---

## 6. Header + mobile menu

```html
<header class="sticky top-0 z-40 border-b border-slate-200 dark:border-slate-800 bg-white/80 dark:bg-slate-950/80 backdrop-blur">
  <div class="mx-auto flex max-w-6xl flex-wrap items-center justify-between gap-4 px-4 py-4">
    <a href="index.html" class="font-display text-xl font-bold text-slate-900 dark:text-white">Ekramul<span class="text-brand-600 dark:text-brand-500">.dev</span></a>
    <nav aria-label="Main">
      <ul class="hidden gap-6 md:flex">
        <li><a href="#about" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">About</a></li>
        <li><a href="#projects" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Projects</a></li>
        <li><a href="#services" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Services</a></li>
        <li><a href="contact.html" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Contact</a></li>
      </ul>
    </nav>

    <button type="button" popovertarget="mobile-menu" class="rounded-lg p-2 hover:bg-slate-100 dark:hover:bg-slate-800 md:hidden">
      <span class="sr-only">Open menu</span>
      <svg class="h-6 w-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M4 6h16M4 12h16M4 18h16"/></svg>
    </button>
  </div>

  <nav id="mobile-menu" popover aria-label="Mobile" class="m-0 ml-auto h-dvh w-64 bg-white dark:bg-slate-900 p-6 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
    <button type="button" popovertarget="mobile-menu" popovertargetaction="hide" class="mb-6 font-semibold">✕ Close</button>
    <ul class="space-y-4 text-lg">
      <li><a href="#about" class="hover:text-brand-600">About</a></li>
      <li><a href="#projects" class="hover:text-brand-600">Projects</a></li>
      <li><a href="#services" class="hover:text-brand-600">Services</a></li>
      <li><a href="contact.html" class="hover:text-brand-600">Contact</a></li>
    </ul>
  </nav>
</header>
```

**Desktop part**

| Code | Explain |
|------|---------|
| `<header>` | Semantic tag for the top area (logo + menu). |
| `sticky top-0 z-40` | Scrolls, then sticks to the top. `z-40` keeps it above other content. |
| `bg-white/80 backdrop-blur` | 80% white + blur of what's behind = "glass" effect. |
| Inner `<div>` | Full-width background on the header, but centred content (`mx-auto max-w-6xl`). |
| `flex items-center justify-between` | Logo left, menu right, vertically centred. |
| `<nav aria-label="Main">` | Semantic navigation, named for screen readers. |
| `<ul>` / `<li>` | A menu is a list of links. |
| `hidden md:flex` | Hidden on phones, a flex row from 768px. |
| `href="#about"` | Jump to `id="about"` on the same page. |
| `dark:border-slate-800 dark:bg-slate-950/80` | **Dark mode:** used only when the visitor's device is in dark mode. Every light colour in the project has a dark partner next to it (`text-slate-900 dark:text-white`, `bg-slate-50 dark:bg-slate-900`…). No JavaScript – Tailwind follows the device setting. |

**Mobile part (no JavaScript – HTML5 Popover API)**

| Code | Explain |
|------|---------|
| `popovertarget="mobile-menu"` | Clicking the button opens/closes the element with `id="mobile-menu"`. |
| `md:hidden` | The ☰ button only shows on phones. |
| `sr-only` "Open menu" | Icon-only button → give screen readers a text. |
| `<svg> … <path d="M4 6h16M4 12h16M4 18h16"/>` | Three lines = ☰. `stroke="currentColor"` uses the text colour. `aria-hidden` hides the icon from screen readers. |
| `popover` | Hidden by default; appears on top. Closes with **Esc** or clicking outside. |
| `m-0 ml-auto h-dvh w-64` | Popovers are centred by default – this makes a full-height panel on the right. |
| `backdrop:bg-slate-900/50` | Dark transparent layer behind the panel. |
| `popovertargetaction="hide"` | This button only closes. |

---

## 7. Hero section

```html
<section id="hero" class="mx-auto grid max-w-6xl items-center gap-12 px-4 py-20 md:grid-cols-2">
  <div class="animate-fade-up">
    <h1 class="text-4xl font-bold leading-tight md:text-6xl">I build <span class="text-brand-600 dark:text-brand-500">fast, modern</span> websites</h1>
    <p class="mt-6 max-w-xl text-lg">Hi, I'm Ekramul – a front-end developer from Dhaka. I turn ideas into responsive websites.</p>
    <a href="contact.html" class="btn-primary mt-8">Hire me</a>
  </div>
  <img src="assets/images/avatar-400.png"
       srcset="assets/images/avatar-400.png 400w, assets/images/avatar-800.png 800w"
       sizes="400px"
       alt="Portrait of Ekramul Islam" width="400" height="400" class="mx-auto w-full max-w-sm animate-float rounded-3xl shadow-xl">
</section>
```

| Code | Explain |
|------|---------|
| `<main>` | (opened just before) the unique content of the page – one per page. |
| `<section id="hero">` | The first big block. `id` makes it linkable. |
| `grid … md:grid-cols-2` | Phones: text above image. From 768px: two columns. |
| `items-center gap-12` | Vertically centred, 3rem space between columns. |
| `<div class="animate-fade-up">` | Wrapper so the grid has exactly 2 children; the text fades up on load. |
| `<h1>` | The main topic of the page. **Only one per page.** |
| `text-4xl md:text-6xl` | Smaller heading on phones, bigger from tablets (mobile-first). |
| `<span class="text-brand-600">` | Colour part of a sentence. |
| `max-w-xl` | Short lines are easier to read. |
| `<img … alt width height>` | `alt` for blind users/failed loads; `width/height` stop layout jumping. Not lazy – it's visible immediately. |
| `srcset` + `sizes` | **Responsive image:** the same photo in two sizes (`400w`, `800w`). `sizes="400px"` = shown ~400px wide. Normal screens download the 400px file; sharp "Retina" screens download the 800px file. |
| `animate-float` | Our custom floating animation. |

---

## 8. About section + video

```html
<section id="about" class="bg-slate-50 dark:bg-slate-900 py-20">
  <div class="mx-auto grid max-w-6xl gap-12 px-4 lg:grid-cols-2">
    <div>
      <h2 class="text-3xl">About me</h2>
      <p class="mt-4">I build websites with <strong>HTML5</strong> and <strong>Tailwind CSS</strong> for small businesses.</p>
      <h3 class="mt-8 text-xl">Skills</h3>
      <ul class="mt-3 flex flex-wrap gap-2">
        <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">HTML5</li>
        <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">CSS3</li>
        <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">Tailwind CSS</li>
        <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">Git &amp; GitHub</li>
      </ul>

      <h3 class="mt-8 text-xl">My learning journey</h3>
      <div class="mt-3 overflow-x-auto">
        <table class="w-full text-sm">
          <caption class="pb-2 text-left text-slate-500 dark:text-slate-400">Courses and training I have completed</caption>
          <thead class="border-b-2 border-slate-300 dark:border-slate-700 text-slate-900 dark:text-white">
            <tr>
              <th scope="col">Year</th>
              <th scope="col">Course</th>
              <th scope="col">Where</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-200 dark:divide-slate-800">
            <tr>
              <td>2024</td>
              <td>HTML &amp; CSS basics</td>
              <td>YouTube (self-study)</td>
            </tr>
            <tr>
              <td>2025</td>
              <td>Web design with Tailwind CSS</td>
              <td>Online course</td>
            </tr>
            <tr>
              <td>2026</td>
              <td>Freelancing with AI tools</td>
              <td>Online course</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div>
      <h3 class="text-xl">Say hello</h3>
      <video controls width="640" height="360" poster="assets/images/video-poster.svg" class="mt-3 aspect-video w-full rounded-2xl">
        <source src="assets/media/intro.mp4" type="video/mp4">
        <track kind="captions" src="assets/media/intro-captions.vtt" srclang="en" label="English">
        Your browser does not support video.
      </video>

      <p class="mt-4 text-sm">Prefer to listen? Here is the audio version:</p>
      <audio controls class="mt-2 w-full">
        <source src="assets/media/intro.mp3" type="audio/mpeg">
        Your browser does not support audio.
      </audio>
    </div>
  </div>
</section>
```

| Code | Explain |
|------|---------|
| `bg-slate-50 py-20` on the section | Full-width light background. |
| `grid … lg:grid-cols-2` | Text and video side by side on laptops. |
| `h2 → h3` | Correct heading order – never skip levels. |
| `<strong>` | Important text (not just bold). |
| `flex flex-wrap gap-2` | Skill "badges" in a row that wrap to the next line. |
| `rounded-full px-4 py-1` | Pill shape. |
| `&amp;` | The `&` character, written safely. |
| `<video controls poster>` | `controls` = play/pause buttons; `poster` = image before playing. |
| `<source type="video/mp4">` | The video file. More `<source>`s can be added; the browser plays the first it supports. |
| `<track kind="captions">` | Subtitles from a `.vtt` file – for deaf users and silent viewing. |
| `aspect-video` | Always 16:9. |
| `<table>` + `<caption>` | A data table with a title. Only for real data, never for layout. |
| `<thead>` / `<tbody>` / `<tr>` | Head part, body part, and rows. |
| `<th scope="col">` / `<td>` | Column title cells / normal data cells. Every row has the same number of cells. |
| `overflow-x-auto` (wrapper div) | A wide table scrolls sideways inside its box on small phones. |
| `divide-y divide-slate-200` | Thin lines **between** the rows. |
| `<audio controls>` + `<source type="audio/mpeg">` | An MP3 player – works like `<video>`. |
| Text inside `<video>` | Fallback for very old browsers. |

---

## 9. Projects grid + case-study modals

```html
<section id="projects" class="mx-auto max-w-6xl px-4 py-20">
  <h2 class="text-3xl">Projects</h2>

  <div class="mt-8 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
    <article class="card group flex flex-col">
      <figure class="overflow-hidden rounded-xl">
        <img src="assets/images/restaurant.svg" alt="Spice Garden website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
        <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">Restaurant landing page</figcaption>
      </figure>
      <h3 class="mt-4 text-xl">Spice Garden</h3>
      <p class="mt-2 flex-1">A one-page website with menu and reservation form.</p>
      <div class="mt-4 flex gap-6">
        <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
        <button type="button" popovertarget="case-spice" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
      </div>

      <div id="case-spice" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
        <h3 class="text-xl">Spice Garden – case study</h3>
        <dl class="mt-4 space-y-3 text-sm">
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
            <dd>The restaurant took all orders by phone and had no website.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
            <dd>A one-page website with the menu, photos and a reservation form.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
            <dd>30% of table bookings now come from the website.</dd>
          </div>
        </dl>
        <button type="button" popovertarget="case-spice" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
      </div>
    </article>

    <article class="card group flex flex-col">
      <figure class="overflow-hidden rounded-xl">
        <img src="assets/images/agency.svg" alt="BrightPath website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
        <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">Agency business website</figcaption>
      </figure>
      <h3 class="mt-4 text-xl">BrightPath</h3>
      <p class="mt-2 flex-1">A five-page website for a digital agency.</p>
      <div class="mt-4 flex gap-6">
        <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
        <button type="button" popovertarget="case-brightpath" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
      </div>

      <div id="case-brightpath" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
        <h3 class="text-xl">BrightPath – case study</h3>
        <dl class="mt-4 space-y-3 text-sm">
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
            <dd>The agency's old website was slow and broke on phones.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
            <dd>A new 5-page responsive website built with Tailwind CSS.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
            <dd>The page speed score went from 48 to 98.</dd>
          </div>
        </dl>
        <button type="button" popovertarget="case-brightpath" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
      </div>
    </article>

    <article class="card group flex flex-col">
      <figure class="overflow-hidden rounded-xl">
        <img src="assets/images/ecommerce.svg" alt="ShopEasy website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
        <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">E-commerce product page</figcaption>
      </figure>
      <h3 class="mt-4 text-xl">ShopEasy</h3>
      <p class="mt-2 flex-1">A product listing page built from a design mockup.</p>
      <div class="mt-4 flex gap-6">
        <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
        <button type="button" popovertarget="case-shopeasy" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
      </div>

      <div id="case-shopeasy" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
        <h3 class="text-xl">ShopEasy – case study</h3>
        <dl class="mt-4 space-y-3 text-sm">
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
            <dd>The client had an AI-made design but no code.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
            <dd>I turned the design into clean HTML and Tailwind CSS in 2 days.</dd>
          </div>
          <div>
            <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
            <dd>The shop launched one week earlier than planned.</dd>
          </div>
        </dl>
        <button type="button" popovertarget="case-shopeasy" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
      </div>
    </article>
  </div>
</section>
```

| Code | Explain |
|------|---------|
| `grid gap-6 sm:grid-cols-2 lg:grid-cols-3` | 1 → 2 → 3 columns. The most common layout on the web. |
| `<article>` | Each project makes sense on its own → `article`. |
| `card group flex flex-col` | Our card component; `group` lets children react to hovering the card; children in a column. |
| `<figure>` + `<figcaption>` | Image + caption that belong together. |
| `overflow-hidden rounded-xl` | Cuts off the zoomed image so it stays inside the rounded box. |
| `group-hover:scale-110` | When the **card** is hovered, zoom the image to 110%. |
| `transition duration-500` | Makes the zoom smooth (0.5s). |
| `loading="lazy"` | Image downloads only when the user scrolls near it → faster page. |
| `flex-1` on the paragraph | Takes extra space → all "Live demo" links line up at the bottom. |
| `<button popovertarget="case-spice">` | Opens the case-study **modal** – same Popover API as the mobile menu. Each project has its own id. |
| `popover` with `w-11/12 max-w-lg` | Without position classes the browser **centres** the popover → a modal. Esc / click outside closes it. |
| `<dl>` / `<dt>` / `<dd>` | Description list: Problem → Solution → Result. |
| `text-slate-700` on the popover | Popovers don't take the page's text colour automatically. |

---

## 9b. "How I work" section

Made in Class 1.5 with **v0.dev** (an AI UI tool), then refactored.

```html
<section id="process" class="mx-auto max-w-6xl px-4 py-20" aria-labelledby="process-title">
  <h2 id="process-title" class="text-center text-3xl">How I work</h2>
  <p class="mt-3 text-center">A simple 4-step process from idea to live website.</p>

  <ol class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
    <li class="card">
      <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">01</span>
      <h3 class="mt-2 text-lg">Discuss</h3>
      <p class="mt-1 text-sm">We talk about your goals, pages and deadline.</p>
    </li>

    <li class="card">
      <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">02</span>
      <h3 class="mt-2 text-lg">Design</h3>
      <p class="mt-1 text-sm">I prepare the layout and colours for your approval.</p>
    </li>

    <li class="card">
      <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">03</span>
      <h3 class="mt-2 text-lg">Develop</h3>
      <p class="mt-1 text-sm">I build the responsive website and share progress.</p>
    </li>

    <li class="card">
      <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">04</span>
      <h3 class="mt-2 text-lg">Deliver</h3>
      <p class="mt-1 text-sm">Your site goes live, with the code on GitHub.</p>
    </li>
  </ol>
</section>
```

| Code | Explain |
|------|---------|
| `<ol>` | Ordered list – the steps have an order. |
| `grid … sm:grid-cols-2 lg:grid-cols-4` | 1 → 2 → 4 columns. |
| `<li class="card">` | Each step looks like our card. |
| `text-brand-100` + `aria-hidden="true"` | The big number is a light decoration; screen readers already know the order from the `<ol>`. |

---

## 10. Services & pricing

```html
<section id="services" class="py-20" aria-labelledby="services-title">
  <div class="mx-auto max-w-6xl px-4">
    <h2 id="services-title" class="text-center text-3xl">Services &amp; pricing</h2>
    <p class="mt-3 text-center">Fixed prices. Clear deliverables. No surprises.</p>

    <div class="mt-14 grid items-start gap-8 md:grid-cols-3">
      <article class="card flex flex-col">
        <h3 class="text-xl">Basic</h3>
        <p class="mt-2 text-sm">A simple one-page website.</p>
        <p class="mt-6"><span class="text-5xl font-bold text-slate-900 dark:text-white">$50</span> / project</p>
        <p class="mt-1 text-sm">Delivery in 3 days</p>
        <ul class="mt-6 flex-1 space-y-3 text-sm">
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> 1 landing page</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Responsive design</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Contact form</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> 1 revision</li>
        </ul>
        <a href="contact.html" class="btn mt-8 w-full border border-slate-300 dark:border-slate-700 text-center hover:border-brand-600">Choose Basic</a>
      </article>

      <article class="relative rounded-3xl bg-brand-900 p-8 text-white shadow-2xl ring-2 ring-brand-500 flex flex-col md:-translate-y-4">
        <p class="absolute -top-3 left-1/2 -translate-x-1/2 rounded-full bg-amber-400 px-3 py-1 text-xs font-bold text-slate-900">MOST POPULAR</p>
        <h3 class="text-xl text-white">Standard</h3>
        <p class="mt-2 text-sm">A complete business website.</p>
        <p class="mt-6"><span class="text-5xl font-bold">$120</span> / project</p>
        <p class="mt-1 text-sm">Delivery in 5 days</p>
        <ul class="mt-6 flex-1 space-y-3 text-sm">
          <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Up to 5 pages</li>
          <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Responsive design</li>
          <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Contact form + animations</li>
          <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> GitHub repo + deploy</li>
          <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> 3 revisions</li>
        </ul>
        <a href="contact.html" class="btn mt-8 w-full bg-white text-center text-brand-900 hover:bg-brand-50">Choose Standard</a>
      </article>

      <article class="card flex flex-col">
        <h3 class="text-xl">Premium</h3>
        <p class="mt-2 text-sm">Custom design and extra polish.</p>
        <p class="mt-6"><span class="text-5xl font-bold text-slate-900 dark:text-white">$250</span> / project</p>
        <p class="mt-1 text-sm">Delivery in 10 days</p>
        <ul class="mt-6 flex-1 space-y-3 text-sm">
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Up to 10 pages</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Custom UI design</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Advanced animations + SEO</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Custom domain setup</li>
          <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Unlimited revisions (14 days)</li>
        </ul>
        <a href="contact.html" class="btn mt-8 w-full border border-slate-300 dark:border-slate-700 text-center hover:border-brand-600">Choose Premium</a>
      </article>
    </div>

    <div class="mt-12 rounded-2xl bg-amber-50 dark:bg-amber-950 p-6 text-center ring-1 ring-amber-200 dark:ring-amber-900">
      <p class="font-semibold text-slate-900 dark:text-white">🎉 Launch offer: 20% off your first website</p>
      <p class="mt-1 text-sm">For my first 5 clients, in exchange for an honest review. Valid until 31 December 2026.</p>
    </div>

    <h3 class="mt-12 text-center text-xl">Add-ons</h3>
    <ul class="mt-6 grid gap-4 sm:grid-cols-2 lg:grid-cols-4">
      <li class="card flex items-center justify-between"><span>Extra page</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$15</span></li>
      <li class="card flex items-center justify-between"><span>Express delivery</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$30</span></li>
      <li class="card flex items-center justify-between"><span>Logo &amp; favicon</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$20</span></li>
      <li class="card flex items-center justify-between"><span>1 month support</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$40</span></li>
    </ul>
  </div>
</section>
```

| Code | Explain |
|------|---------|
| `aria-labelledby="services-title"` | The section's accessible name = its `<h2>`. |
| `grid items-start gap-8 md:grid-cols-3` | Three packages side by side from tablets. `items-start` so the lifted card doesn't stretch others. |
| `<span class="text-5xl">$50</span> / project` | Big price, small unit. |
| `flex-1` on the `<ul>` | Pushes every button to the bottom of its card. |
| `aria-hidden="true"` on ✓ | Screen readers don't repeat "check mark". |
| `btn … w-full` | Full-width button reusing `.btn`. |
| **Standard card:** `bg-brand-900 text-white ring-2` | Dark, outlined card → the package we want to sell stands out. |
| `md:-translate-y-4` | Lifted 16px on tablets+. |
| `relative` (card) + `absolute` (badge) | The badge is positioned relative to its card. |
| `-top-3 left-1/2 -translate-x-1/2` | Badge sticks out above the card, centred horizontally (classic centring trick). |
| `bg-amber-50 ring-1 ring-amber-200` | The **launch offer** box: soft yellow = "special". The text is limited (first 5 clients) and urgent (end date). |
| Add-ons `grid … lg:grid-cols-4` | Small extras; `flex justify-between` = name left, price right. |

**Business logic:** Basic = entry price, Standard = what most clients pick ("Most popular"), Premium = makes Standard look like good value.

---

## 11. FAQ accordion

```html
<section id="faq" class="bg-slate-50 dark:bg-slate-900 py-20" aria-labelledby="faq-title">
  <div class="mx-auto max-w-3xl px-4">
    <h2 id="faq-title" class="text-center text-3xl">Frequently asked questions</h2>
    <div class="mt-10 space-y-4">
      <details class="group card">
        <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
          What do you need from me to start?
          <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
        </summary>
        <p class="mt-3">Your logo, text, images and 2–3 websites you like.</p>
      </details>
      <details class="group card">
        <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
          Do I get the source code?
          <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
        </summary>
        <p class="mt-3">Yes. Every package includes a GitHub repository.</p>
      </details>
      <details class="group card">
        <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
          Where will my website be hosted?
          <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
        </summary>
        <p class="mt-3">Free on Vercel. I can also connect your own domain.</p>
      </details>
      <details class="group card">
        <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
          How do payments work?
          <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
        </summary>
        <p class="mt-3">Through Fiverr/Upwork, or 50% upfront and 50% on delivery for direct clients.</p>
      </details>
    </div>
  </div>
</section>
```

| Code | Explain |
|------|---------|
| `max-w-3xl` | Narrower column – easier to read questions. |
| `<details>` + `<summary>` | **HTML5 accordion, no JavaScript.** Click the summary to open/close. Keyboard-friendly. |
| `list-none` | Removes the default ▶ triangle. |
| `cursor-pointer` | Hand cursor → looks clickable. |
| `group` + `group-open:rotate-45` | When the `<details>` is open, the `+` rotates 45° and becomes `×`. |
| `space-y-4` | Space between the questions. |

---

## 12. Testimonials

```html
  <section id="testimonials" class="bg-brand-900 py-20" aria-labelledby="testimonials-title">
    <div class="mx-auto max-w-6xl px-4">
      <h2 id="testimonials-title" class="text-center text-3xl text-white">What clients say</h2>

      <div class="mt-10 grid gap-6 md:grid-cols-3">
        <figure class="card">
          <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
          <blockquote class="mt-4">
            <p>"Ekramul delivered our restaurant site two days early. Mobile view is perfect!"</p>
          </blockquote>
          <figcaption class="mt-6">
            <cite class="font-semibold not-italic text-slate-900 dark:text-white">Karim Uddin</cite>
            <span class="block text-sm text-slate-500 dark:text-slate-400">Owner, Spice Garden</span>
          </figcaption>
        </figure>

        <figure class="card">
          <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
          <blockquote class="mt-4">
            <p>"Clear communication and clean code. Our page speed score jumped to 98."</p>
          </blockquote>
          <figcaption class="mt-6">
            <cite class="font-semibold not-italic text-slate-900 dark:text-white">Sarah Lee</cite>
            <span class="block text-sm text-slate-500 dark:text-slate-400">Marketing Lead, BrightPath</span>
          </figcaption>
        </figure>

        <figure class="card">
          <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
          <blockquote class="mt-4">
            <p>"Ekramul turned our AI mockup into a real website better than we imagined."</p>
          </blockquote>
          <figcaption class="mt-6">
            <cite class="font-semibold not-italic text-slate-900 dark:text-white">Tanvir Hossain</cite>
            <span class="block text-sm text-slate-500 dark:text-slate-400">Founder, ShopEasy</span>
          </figcaption>
        </figure>
      </div>
    </div>
  </section>
</main>
```

| Code | Explain |
|------|---------|
| `bg-brand-900` + white `h2` | Dark section to break the rhythm of the page. |
| `<figure>` + `<blockquote>` + `<figcaption>` + `<cite>` | The correct HTML for "a quote and who said it". |
| `sr-only` "Rated 5 out of 5" + `aria-hidden` stars | Screen readers say the rating once instead of "star star star star star". |
| `not-italic` | `<cite>` is italic by default – we remove it. |
| `block` on the role | Puts the role on its own line. |
| `</main>` | End of the unique page content. |

> This section was originally generated with AI and then **refactored**: `<div>`s → semantic tags, fixed widths → grid, random colours → brand colours, fake photos removed.

---

## 13. Footer

```html
  <footer class="bg-slate-900 text-slate-400">
    <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-2 px-4 py-8 sm:flex-row">
      <address class="not-italic">
        Email: <a href="mailto:hello@example.com" class="text-white hover:underline">hello@example.com</a>
      </address>
      <p class="text-sm">&copy; 2026 Ekramul Islam</p>
    </div>
  </footer>

</body>
</html>
```

| Code | Explain |
|------|---------|
| `<footer>` | Semantic bottom area. |
| `flex flex-col … sm:flex-row` | Stacked and centred on phones, a row from 640px. |
| `<address>` | Contact information of the page owner. `not-italic` removes the default italic. |
| `mailto:` | Opens the visitor's email app. (`tel:` opens the phone dialer.) |
| `&copy;` | © symbol. |

---

## 14. Contact page + form

`contact.html` uses the **same head, header and footer** as `index.html`, with three differences:
a different `<title>`/description, and menu links written as `index.html#about` (because `#about` alone only works on the same page).

### 14a. Layout, map and form start

```html
<main>
  <section id="contact" class="mx-auto grid max-w-6xl gap-12 px-4 py-20 lg:grid-cols-3">
    <div>
      <h1 class="text-4xl font-bold">Let's work together</h1>
      <p class="mt-4">Fill in the form and I will reply within 24 hours.</p>
      <iframe title="Map of Dhaka" src="https://www.openstreetmap.org/export/embed.html?bbox=90.35%2C23.70%2C90.45%2C23.82&amp;layer=mapnik"
              width="600" height="300" loading="lazy" class="mt-8 aspect-video w-full rounded-2xl"></iframe>
    </div>

    <form action="https://api.web3forms.com/submit" method="POST" class="card space-y-8 lg:col-span-2">
      <input type="hidden" name="access_key" value="YOUR-WEB3FORMS-ACCESS-KEY">
      <input type="hidden" name="subject" value="New project request from my portfolio">
      <input type="hidden" name="redirect" value="https://your-site.vercel.app/thank-you.html">

```

| Code | Explain |
|------|---------|
| `grid … lg:grid-cols-3` + `lg:col-span-2` on the form | Info column 1/3, form 2/3 on laptops. |
| `<iframe title loading="lazy">` | Embeds a map from another site. `title` is required for accessibility; lazy = loads when scrolled near. |
| `action="https://api.web3forms.com/submit"` | The data goes to **Web3Forms**, a free service that emails every message to you. (Vercel only hosts files – it has no form inbox.) |
| `method="POST"` | Data sent in the request body, not in the URL. |
| `type="hidden"` inputs | Sent with the form but invisible to the visitor. |
| `access_key` | Your free key from web3forms.com – tells it which email to send to. Safe to keep in the HTML/GitHub. |
| `subject` | Subject line of the email you receive. |
| `redirect` | After sending, the visitor lands on **our** `thank-you.html`. Must be the full live URL. |
| `card space-y-8` | The form looks like a card; 2rem between its groups. |

### 14b. "About you" fields

```html
<fieldset class="grid gap-5 sm:grid-cols-2">
  <legend class="mb-4 text-lg font-semibold text-slate-900 dark:text-white">About you</legend>

  <div>
    <label for="name">Full name *</label>
    <input type="text" id="name" name="name" required minlength="3" placeholder="e.g. Karim Uddin" class="form-input">
  </div>

  <div>
    <label for="email">Email *</label>
    <input type="email" id="email" name="email" required placeholder="you@company.com" class="form-input">
  </div>

  <div>
    <label for="phone">Phone</label>
    <input type="tel" id="phone" name="phone" pattern="01[3-9][0-9]{8}" placeholder="01XXXXXXXXX"
           title="11-digit Bangladeshi number, e.g. 01712345678" class="form-input">
  </div>

  <div>
    <label for="website">Current website</label>
    <input type="url" id="website" name="website" placeholder="https://..." class="form-input">
  </div>
</fieldset>
```

| Code | Explain |
|------|---------|
| `<fieldset>` + `<legend>` | Groups related fields with a title. |
| `grid gap-5 sm:grid-cols-2` | Two fields per row from 640px. Each label+input pair is wrapped in a `<div>` = one grid cell. |
| `<label for="name">` + `id="name"` | Connected: clicking the label focuses the input. Required for accessibility. |
| `name="name"` | The key sent to the server. **No `name` = not sent.** |
| `required` | Cannot submit empty. |
| `minlength="3"` | At least 3 characters. |
| `type="email"` | Checks for a valid email; phones show the `@` keyboard. |
| `type="tel"` | Phones show the number keypad. |
| `pattern="01[3-9][0-9]{8}"` | Bangladeshi mobile number: `01`, then 3–9, then 8 digits = 11 digits. |
| `title` | Shown in the error bubble when the pattern fails. |
| `sm:col-span-2` | This field takes the full row. |
| `type="url"` | Must be a full web address (`https://…`). |
| `class="form-input"` | Our shared input style. |

### 14c. "Your project" fields

```html
<fieldset class="grid gap-5 sm:grid-cols-2">
  <legend class="mb-4 text-lg font-semibold text-slate-900 dark:text-white">Your project</legend>

  <div>
    <label for="service">Service *</label>
    <select id="service" name="service" required class="form-input">
      <option value="">-- Choose a service --</option>
      <option value="landing">Landing page</option>
      <option value="business">Business website</option>
      <option value="convert">Design to code</option>
    </select>
  </div>

  <div>
    <label for="deadline">Deadline</label>
    <input type="date" id="deadline" name="deadline" class="form-input">
  </div>

  <div>
    <label for="industry">Industry</label>
    <input type="text" id="industry" name="industry" list="industries" placeholder="Start typing..." class="form-input">
    <datalist id="industries">
      <option value="Restaurant"></option>
      <option value="Education"></option>
      <option value="E-commerce"></option>
      <option value="Real estate"></option>
    </datalist>
  </div>

  <div>
    <label for="budget">Budget (USD)</label>
    <input type="number" id="budget" name="budget" min="50" max="5000" step="10" placeholder="e.g. 120" class="form-input">
  </div>

  <div class="sm:col-span-2">
    <label for="urgency">How urgent is it?</label>
    <input type="range" id="urgency" name="urgency" min="1" max="5" value="3" class="mt-2 w-full accent-brand-600">
    <div class="flex justify-between text-xs text-slate-500 dark:text-slate-400">
      <span>Flexible</span>
      <span>Very urgent</span>
    </div>
  </div>

  <div class="sm:col-span-2">
    <p>Package *</p>
    <div class="mt-2 flex flex-wrap gap-6">
      <label class="flex items-center gap-2"><input type="radio" name="package" value="basic" required class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Basic</label>
      <label class="flex items-center gap-2"><input type="radio" name="package" value="standard" class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Standard</label>
      <label class="flex items-center gap-2"><input type="radio" name="package" value="premium" class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Premium</label>
    </div>
  </div>

  <div class="sm:col-span-2">
    <label for="message">Project details *</label>
    <textarea id="message" name="message" rows="5" required minlength="20" class="form-input"></textarea>
  </div>
</fieldset>
```

| Code | Explain |
|------|---------|
| `<select required>` + empty first `<option value="">` | The user **must** choose a real option. |
| `type="date"` | Free calendar picker. |
| `list="industries"` + `<datalist>` | Suggestions while typing – the user can pick one or type something else. |
| `type="number" min max step` | Only numbers between 50 and 5000, in steps of 10. |
| `type="range"` + `accent-brand-600` | A slider (1–5) in our brand colour; two `<span>`s with `justify-between` label the ends. |
| `type="radio"` with the same `name="package"` | Only one can be selected. `required` on one is enough for the group. |
| `<label><input> Basic</label>` | Wrapping the input inside the label connects them without `for`/`id`. |
| `text-brand-600` on radios | With the forms plugin, the text colour sets the checked colour. |
| `<textarea rows="5" minlength="20">` | Multi-line text, at least 20 characters. |

### 14d. Consent + submit

```html
      <label class="flex items-center gap-2"><input type="checkbox" name="consent" required class="rounded text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> I agree to be contacted *</label>

      <button type="submit" class="btn-primary">Send request</button>
    </form>
  </section>
</main>
```

| Code | Explain |
|------|---------|
| `type="checkbox" required` | Must be ticked before sending. |
| `<button type="submit">` | Sends the form. The browser checks **all** validation rules first – no JavaScript needed. |

---

## 15. Thank-you and 404 pages

`public/thank-you.html` (`<main>` part):

```html
<main class="grid min-h-screen place-items-center px-4 text-center">
  <div>
    <p class="text-7xl" aria-hidden="true">✅</p>
    <h1 class="mt-4 text-3xl">Thank you!</h1>
    <p class="mt-2">Your message was sent. I will reply within 24 hours.</p>
    <a href="index.html" class="btn-primary mt-8">Back to home</a>
  </div>
</main>
```

`public/404.html` (visible part – the head is the same as the other pages):

```html
<body>
  <main class="grid min-h-screen place-items-center px-4 text-center">
    <div>
      <p class="text-7xl font-bold text-brand-600 dark:text-brand-500">404</p>
      <h1 class="mt-4 text-3xl">Page not found</h1>
      <p class="mt-2">Sorry, this page doesn't exist.</p>
      <a href="index.html" class="btn-primary mt-8">Back to home</a>
    </div>
  </main>
</body>
</html>
```

| Code | Explain |
|------|---------|
| `grid min-h-screen place-items-center` | Perfect centring on the whole screen – just 2 classes. |
| `text-7xl` | Huge "404" / emoji as the visual. |
| Link back home | Never leave a visitor on a dead end. |
| `404.html` | Vercel shows it automatically for any wrong URL. |

---

## 16. Git, GitHub and deploy

### `.gitignore`
```
.DS_Store
.env
.vercel
```

| Line | Explain |
|------|---------|
| `.DS_Store` | Mac junk file. |
| `.env` | Secrets (passwords, API keys) – for later semesters. |
| `.vercel` | Local Vercel settings folder. |

### First push
```bash
git init
```
```bash
git add .
```
```bash
git commit -m "feat: first version of my portfolio"
```
```bash
git branch -M main
```
```bash
git remote add origin https://github.com/YOUR-USERNAME/portfolio.git
```
```bash
git push -u origin main
```

| Command | Explain |
|---------|---------|
| `git init` | Start tracking the folder (once per project). |
| `git add .` | Stage all changes. |
| `git commit -m` | Save a snapshot with a message (`feat:`, `fix:`, `style:`, `docs:`). |
| `git branch -M main` | Name the main branch `main`. |
| `git remote add origin` | Connect to the GitHub repository. |
| `git push -u origin main` | Upload. Next time just `git push`. |

### `vercel.json`
```json
{
  "outputDirectory": "public",
  "cleanUrls": true
}
```

| Line | Explain |
|------|---------|
| `outputDirectory` | Only `public/` goes online. Plain HTML – nothing to build. |
| `cleanUrls` | `/contact.html` shows as `/contact`. |

**Deploy:** vercel.com → sign up with GitHub → **Add New → Project** → Import the repo → **Deploy**.
Then **Settings → Domains** → rename to `yourname.vercel.app`.
After that, **every `git push` updates the live site automatically**, and every push gets its own preview URL.

**Contact form:** get a free access key at web3forms.com, paste it into the `access_key` field in `contact.html`,
and set `redirect` to your live URL. Messages arrive in your email inbox.

### `README.md`
```markdown
# Ekramul Islam – Portfolio

Personal portfolio website built with HTML5 and Tailwind CSS.

**Live site:** https://your-site.vercel.app

## Run locally
Open `public/index.html` with the **Live Server** extension in VS Code. No installation needed –
Tailwind CSS is loaded from its CDN.

## Tech
HTML5 · CSS3 · Tailwind CSS 3 (CDN) · Vercel
```

---

## 17. Freelance documents

These live in `docs/` – not code, but part of the project.

### `docs/gig.md`
```markdown
# My Fiverr gig

**Title (max 80 chars):** I will build a responsive landing page with HTML and Tailwind CSS

**Tags:** tailwind css, landing page, responsive website, html css, figma to html

**Description**

Need a fast, modern website that looks perfect on every phone?

I build clean, responsive landing pages and business websites with HTML5 and Tailwind CSS.
I can also turn your Figma, Canva or AI design into real code.

What you get:
- Mobile-first, responsive design
- Fast loading and SEO-friendly structure
- Working contact form
- Source code on GitHub + free deployment

Please message me before ordering so we can discuss your project.
Portfolio: https://your-site.vercel.app

**FAQ**
- *Do I get the source code?* Yes, on GitHub.
- *Where will my site be hosted?* Free on Vercel, or your own hosting.
```

### `docs/cover-letter.md`
```markdown
# Upwork cover letter template

Hi [Client name], you need [their problem in one sentence] – I recently did something similar
for [project name]: [live link]

My plan:
- Day 1: [first step]
- Day 2–3: [main work]
- Day 4: [delivery: deploy + GitHub repo]

Quick question: [one useful question about their project]?

Best,
[Your name]
```

### `docs/client-messages.md`
```markdown
# Client message templates

## First reply
Hi [Name], thanks for reaching out! To give you an exact quote, could you share:
1. How many pages or sections do you need?
2. Do you have a design, or should I create one?
3. What is your deadline?
4. 2–3 websites you like?

## Progress update
Hi [Name], quick update: [what is done] ✅ Preview: [link]. Next: [what is next]. Any feedback so far?

## Delivery
Your website is live: [link]. Source code: [GitHub link]. Please review and let me know if you need any changes.

## Extra request (scope creep)
Great idea! That is outside the current package, but I can add it for $[x] and [y] extra days. Shall I send an updated offer?
```

### `docs/profile.md`
```markdown
# My freelancer profile (Fiverr / Upwork)

## Profile photo
A clear, friendly photo of your face – good light, plain background, no logos or group photos.

## Display name / title (max ~50 characters)
**Front-End Developer | Responsive Websites with HTML & Tailwind CSS**

## Short description (Fiverr "one-liner")
I build fast, mobile-friendly websites for small businesses.

## Overview / bio (150–250 words)
Hi, I'm Ekramul – a front-end developer from Dhaka, Bangladesh.

I help small businesses, startups and freelancers get online with **fast, modern and mobile-friendly websites**.
I build with **HTML5 and Tailwind CSS**, and I can turn your Figma, Canva or AI-generated design into real code.

What you can expect from me:
- Clean, responsive design that works on every phone
- Clear communication and daily progress updates
- Your website live on Vercel + full source code on GitHub
- On-time delivery

Recent work: a restaurant landing page, an agency website and an e-commerce product page.
See them here: https://your-site.vercel.app

Send me a message with your idea – I usually reply within a few hours.

## Skills (pick 5–10 that the platform suggests)
HTML5 · CSS3 · Tailwind CSS · Responsive Web Design · Landing Page · Website Design · Figma to HTML · Git · GitHub

## Languages
Bangla (native) · English (conversational / fluent – be honest)

## Portfolio items (add 3+)
For each: a screenshot, a title, 2 lines about the problem and solution, and the live link.

## Profile checklist
- [ ] Real photo, no AI-generated face
- [ ] Title says **what you do** + **main skill**
- [ ] Bio starts with the client's need, not "I am a hard-working…"
- [ ] Portfolio link works on mobile
- [ ] No contact details (email/WhatsApp) in the profile – platforms don't allow it
```

### `docs/packages.md`
```markdown
# My service packages

| | Basic | Standard ⭐ | Premium |
|---|---|---|---|
| Price | $50 | $120 | $250 |
| Pages | 1 | Up to 5 | Up to 10 |
| Animations | – | ✔ | Advanced |
| SEO | – | Basic | Full |
| Revisions | 1 | 3 | Unlimited (14 days) |
| Delivery | 3 days | 5 days | 10 days |

**Add-ons:** extra page $15 · express delivery $30 · 1 month maintenance $40

## How I calculated the price
hourly target × hours + 20% buffer → $8 × 12 h = $96 + 20% ≈ **$120**

## Special offers
| Offer | Details | Why it works |
|-------|---------|--------------|
| **Launch offer** | 20% off the first website for my first 5 clients, in exchange for an honest review. Ends 31 December 2026. | Gets your first reviews fast. A clear end date creates urgency. |
| **Bundle** | Website + 1 month support for $150 instead of $160. | Increases the order value; the client saves money. |
| **Referral** | $10 off the next order when a client refers a friend. | Happy clients bring new clients. |

## Custom offer template (Fiverr / Upwork)
> Hi [Name], here is your custom offer for **[package]**: [what is included] – delivered in [days] days with
> [number] revisions for **$[price]**. Let me know if you'd like to change anything before you accept.

**Rules:** never discount more than 20–30% · always write an end date · put every promise in writing.
```

---

## 18. Final checklist

```markdown
# Submission checklist

## Content
- [ ] My own name, photo, bio, skills, email
- [ ] At least 3 of my own projects with screenshots
- [ ] My own packages and prices
- [ ] Intro video (or poster) + captions

## Code
- [ ] W3C validator: 0 errors on every page
- [ ] One `<h1>` per page, headings in order
- [ ] Every image has `alt`, `width`, `height`; project images use `loading="lazy"`
- [ ] Every form field has a `<label>`
- [ ] I can explain every line (including AI-generated code)

## Responsive & accessibility
- [ ] No horizontal scroll at 360px, 768px, 1280px
- [ ] Mobile menu opens/closes, works with Esc
- [ ] Lighthouse: Performance, Accessibility, Best Practices, SEO all 90+

## Git & deploy
- [ ] GitHub repo with 10+ meaningful commits
- [ ] Live on Vercel; contact form email received (Web3Forms)
- [ ] README has the live link

## Freelancing
- [ ] Gig text, 2 cover letters, packages in `docs/`
```

---

## 19. Topic → class map

| Class | Topic | Sections in this guide |
|-------|-------|------------------------|
| 1.1 | Web intro, HTML5, semantic tags | 1, 5, 6, 7, 8 (table), 9, 13 |
| 1.2 | Forms, media, validation | 7 (srcset), 8 (video, audio), 14 (form: url, number, range, datalist; map), 15 |
| 1.3 | CSS3 & Tailwind intro (CDN) | 2, 3, 4 |
| 1.4 | Flexbox, Grid, responsive | 6, 7, 8, 9, 13, 14 |
| 1.5 | AI → UI/UX → Tailwind | 9b (v0.dev), 12 (refactored AI code) |
| 1.6 | Components & animations | 3 (keyframes), 4 (dark mode), 6 (mobile menu), 9 (hover, modal) |
| 1.7 | Git, GitHub, deploy | 16 |
| 1.8 | Client communication | 17 (profile, gig, cover letter, messages) |
| 1.9 | Service packages & offers | 10 (pricing, launch offer, add-ons), 11, 17 |
| 1.10 | Defense, portfolio review, final exam | 5 (SEO tags), 15 (404), 18 · exam: `class-10-project-defense/final-exam/` |
