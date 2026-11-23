# LESSON – Line-by-Line Code Explanation (Beginner Level)

| | |
|---|---|
| **Project** | Semester 01 Portfolio Website – *Ekramul Islam* (4 pages: home, contact, thank-you, 404) |
| **Code explained** | Every file in `class-10-project-defense/project` (the finished project) |
| **Who is this for** | Complete beginners. No experience needed – every line is explained in simple words. |

> **How to read this lesson**
>
> Every code block shows **line numbers** on the left (`18 │`). These are the real line numbers in the file,
> so you can open the same file in VS Code and follow along. The numbers are **not** part of the code – don't type them.
> Under each block, the explanation goes **line by line**.

---

## Table of contents

- [Part 0 – Words you must know](#part-0--words-you-must-know)
- [Part 1 – How to read Tailwind classes](#part-1--how-to-read-tailwind-classes)
- [Part 2 – The folder structure](#part-2--the-folder-structure)
- [Part 3 – Setup files](#part-3--setup-files) (`vercel.json`, `.gitignore`)
- [Part 4 – tailwind-config.js (our Tailwind settings)](#part-4--tailwind-configjs-our-tailwind-settings)
- [Part 5 – Our own CSS (the style block)](#part-5--our-own-css-the-style-block)
- [Part 6 – index.html (home page)](#part-6--indexhtml-home-page)
- [Part 7 – contact.html (contact page)](#part-7--contacthtml-contact-page)
- [Part 8 – thank-you.html and 404.html](#part-8--thank-youhtml-and-404html)
- [Part 9 – Practice questions](#part-9--practice-questions)

---

## Part 0 – Words you must know

Look at this one line. It contains almost every word we will use:

```html
<a href="contact.html" class="btn-primary">Hire me</a>
```

| Word | In the example | Meaning |
|------|----------------|---------|
| **Tag** | `<a>` and `</a>` | A name inside `< >`. It tells the browser **what kind of thing** this is (`a` = link). |
| **Opening tag** | `<a …>` | Where the element starts. |
| **Closing tag** | `</a>` | Where it ends. It has a `/`. |
| **Element** | the whole line | Opening tag + content + closing tag. |
| **Content** | `Hire me` | What the visitor sees. |
| **Attribute** | `href="contact.html"` | Extra information about the element. Format: `name="value"`. |
| **class** | `class="btn-primary"` | A special attribute that gives the element **styles** (design). |
| **id** | `id="about"` (elsewhere) | A **unique** name for one element. Used for links like `#about`. Only one element per page can have the same id. |
| **Void element** | `<img>`, `<input>`, `<meta>` | Elements with **no closing tag**, because they have no content inside. |
| **Nesting** | `<ul><li>…</li></ul>` | Putting elements inside other elements. Like boxes inside boxes. Always close the inner box first. |
| **Parent / child** | `<ul>` is the parent of `<li>` | The outer element is the parent; elements directly inside are its children. |
| **Comment** | `<!-- note -->` (HTML), `/* note */` (CSS) | Notes for humans. The browser ignores them. |

**Indentation** (the spaces at the start of lines) doesn't change how the page looks. We use it so humans can see
which element is inside which.

---

## Part 1 – How to read Tailwind classes

In this project almost all design is done with **Tailwind classes**. Each class is a short name for **one CSS rule**.
Once you know the pattern, you can read any class.

### 1.1 The pattern: `what-how-much`

| Class | Read it as | Real CSS |
|-------|-----------|----------|
| `p-4` | **p**adding, size 4 | `padding: 1rem` (16px) |
| `px-4` | padding on the **x**-axis (left + right) | `padding-left: 1rem; padding-right: 1rem` |
| `py-20` | padding on the **y**-axis (top + bottom) | `padding-top: 5rem; padding-bottom: 5rem` |
| `mt-8` | **m**argin **t**op, size 8 | `margin-top: 2rem` (32px) |
| `mx-auto` | margin left + right = auto | centres a box horizontally |
| `w-full` | **w**idth full | `width: 100%` |
| `max-w-6xl` | **max**imum **w**idth, size 6xl | `max-width: 72rem` (1152px) |
| `h-6` | **h**eight 6 | `height: 1.5rem` (24px) |
| `gap-6` | space **between** children | `gap: 1.5rem` |
| `text-xl` | text size extra-large | `font-size: 1.25rem` |
| `text-slate-700` | text **colour** slate, shade 700 | dark grey text |
| `bg-white` | **b**ack**g**round white | `background-color: white` |
| `font-bold` | font weight bold | `font-weight: 700` |
| `rounded-2xl` | rounded corners, size 2xl | `border-radius: 1rem` |
| `shadow-xl` | big shadow | `box-shadow: …` |

> **Spacing rule:** number × 4 = pixels. `p-1` = 4px, `p-4` = 16px, `p-8` = 32px, `p-20` = 80px.

> **Colour rule:** colour name + shade. Shades go from `50` (very light) to `900` (very dark).
> `slate` = grey, `brand` = **our own** blue (we created it in `tailwind-config.js`), `amber` = yellow-orange.

### 1.2 Prefixes: "only when…"

A prefix with a colon `:` means **"apply this class only when…"**

| Prefix | Means | Example |
|--------|-------|---------|
| `sm:` | screen is **640px or wider** | `sm:flex-row` |
| `md:` | screen is **768px or wider** (tablet) | `md:grid-cols-2` |
| `lg:` | screen is **1024px or wider** (laptop) | `lg:grid-cols-3` |
| `hover:` | the mouse is **over** the element | `hover:text-brand-600` |
| `focus:` | the element is **selected** (clicked / tabbed into) | `focus:border-brand-500` |
| `active:` | the element is being **pressed** | `active:scale-95` |
| `group-hover:` | the **parent** marked `group` is hovered | `group-hover:scale-110` |
| `group-open:` | the **parent** `<details>` is open | `group-open:rotate-45` |
| `backdrop:` | the dark layer **behind** a popup | `backdrop:bg-slate-900/50` |
| `dark:` | the visitor's phone/computer is in **dark mode** | `dark:bg-slate-900` |

> **Mobile-first:** a class **without** a prefix works on **all** screens. A prefix adds a rule for **bigger** screens.
> `text-4xl md:text-6xl` = "size 4xl on phones, size 6xl from tablets and up".

> **Dark mode pairs:** in this project almost every light colour has a dark partner right next to it, e.g.
> `bg-white dark:bg-slate-900` or `text-slate-900 dark:text-white`. Read them as a pair: "white – but dark grey in dark mode".
> To keep the tables short, we explain the `dark:` partners once (section 6.2) and don't repeat them on every line.

### 1.3 Special symbols

| Symbol | Example | Meaning |
|--------|---------|---------|
| `/` + number | `bg-white/80` | 80% opacity (a bit see-through) |
| `-` at the start | `-translate-y-1` | **negative** value (move **up** instead of down) |
| fraction | `left-1/2` | 50% |

---

## Part 2 – The folder structure

```
project/
├── public/                     ← the website. ONLY this folder goes online.
│   ├── index.html              ← home page
│   ├── contact.html            ← contact page
│   ├── thank-you.html          ← shown after sending the form
│   ├── 404.html                ← shown when a page doesn't exist
│   └── assets/
│       ├── js/
│       │   └── tailwind-config.js  ← our Tailwind settings (colours, fonts, animations)
│       ├── images/             ← photos (avatar-400.png + avatar-800.png), logo, screenshots
│       └── media/              ← video + subtitles
├── docs/                       ← gig text, cover letter, packages, checklists
├── vercel.json                 ← settings for going live on Vercel
├── .gitignore                  ← files Git should not save
└── README.md                   ← description shown on GitHub
```

**Where does the design come from?** Every page's `<head>` has three things:

```
1. <script src="https://cdn.tailwindcss.com?plugins=forms">  → loads Tailwind from the internet (CDN)
2. <script src="assets/js/tailwind-config.js">               → gives Tailwind OUR colours, fonts, animations
3. <style type="text/tailwindcss"> … </style>                → OUR own CSS (buttons, cards, form inputs)
```

While the page loads, Tailwind reads every class name in the HTML and creates the CSS for it – live, in the browser.
**Nothing to install, nothing to build.** Open the page with Live Server and it works.

---

## Part 3 – Setup files

### 3.1 `vercel.json` – settings for going live

```json
1 │ {
2 │   "outputDirectory": "public",
3 │   "cleanUrls": true
4 │ }
```

| Line | Explanation |
|------|-------------|
| 1, 4 | `{` and `}` start and end the file. This file is **JSON**: a list of `"name": value` pairs, separated by commas. |
| 2 | `"outputDirectory": "public"` – only the `public` folder is put online (not `docs`, not `README.md`). |
| 3 | `"cleanUrls": true` – the address shows `/contact` instead of `/contact.html`. Looks more professional. |

> Our site is plain HTML, so Vercel has nothing to "build" – it just publishes the files.

### 3.2 `.gitignore` – what Git must NOT save

```
1 │ .DS_Store
2 │ .env
3 │ .vercel
```

| Line | Explanation |
|------|-------------|
| 1 | `.DS_Store` – a hidden junk file that Mac computers create. |
| 2 | `.env` – a file for secret passwords/keys (used in later semesters). Secrets must never go on GitHub. |
| 3 | `.vercel` – a settings folder Vercel may create on your computer. Not needed on GitHub. |

---

## Part 4 – `tailwind-config.js` (our Tailwind settings)

File: `public/assets/js/tailwind-config.js`. It **customises** Tailwind: our colours, fonts and animations.
Every page loads it right **after** the Tailwind CDN script.

```js
 1 │ // Tailwind settings: our colours, fonts and animations.
 2 │ // This file must be loaded AFTER the Tailwind CDN script.
 3 │ tailwind.config = {
 4 │   theme: {
 5 │     extend: {
 6 │       colors: {
 7 │         brand: {
 8 │           50: '#eef6ff',
 9 │           100: '#d9eaff',
10 │           500: '#337dff',
11 │           600: '#1b5ef5',
12 │           700: '#1449e1',
13 │           900: '#19378f',
14 │         },
15 │       },
16 │       fontFamily: {
17 │         sans: ['Inter', 'sans-serif'],
18 │         display: ['Poppins', 'sans-serif'],
19 │       },
20 │       keyframes: {
21 │         'fade-up': {
22 │           '0%': { opacity: '0', transform: 'translateY(24px)' },
23 │           '100%': { opacity: '1', transform: 'translateY(0)' },
24 │         },
25 │         float: {
26 │           '0%, 100%': { transform: 'translateY(0)' },
27 │           '50%': { transform: 'translateY(-12px)' },
28 │         },
29 │       },
30 │       animation: {
31 │         'fade-up': 'fade-up 0.8s ease-out both',
32 │         float: 'float 5s ease-in-out infinite',
33 │       },
34 │     },
35 │   },
36 │ };
```

| Line | Explanation |
|------|-------------|
| 1, 2 | Comments (start with `//`) – notes for humans. The browser ignores them. |
| 3 | `tailwind.config = {` – "here are my settings for Tailwind". The Tailwind CDN script looks for exactly this name. Closed on line 36 with `};` |
| 4 | `theme: {` – design settings start here. |
| 5 | `extend: {` – **add** our settings to Tailwind's defaults. (Without `extend` we would **replace** them and lose all of Tailwind's normal colours.) |
| 6 | `colors: {` – our own colours start. |
| 7 | `brand: {` – a new colour called **brand**. Now classes like `bg-brand-600` and `text-brand-600` exist. |
| 8–13 | The shades of our brand blue. `50` is very light, `900` is very dark. Each value is a **hex colour code** (`#` + 6 characters). Change these to change the whole website's colour. |
| 14, 15 | Close `brand` and `colors`. |
| 16 | `fontFamily: {` – our fonts. |
| 17 | `sans` – the normal text font is **Inter**. If Inter can't load, use any `sans-serif` font. Class: `font-sans`. |
| 18 | `display` – a new font name for headings: **Poppins**. Class: `font-display`. |
| 19 | Close `fontFamily`. |
| 20 | `keyframes: {` – the **steps** of our animations. |
| 21 | `'fade-up': {` – animation number 1, called *fade-up*. |
| 22 | At `0%` (the start): `opacity: '0'` = invisible, `translateY(24px)` = 24 pixels lower than normal. |
| 23 | At `100%` (the end): fully visible and in its normal place. Result: the element **rises up while appearing**. |
| 24 | Close `fade-up`. |
| 25 | `float: {` – animation number 2, called *float*. |
| 26 | At the start **and** the end (`0%, 100%`): normal position. |
| 27 | Halfway (`50%`): 12 pixels **higher** (minus = up). Result: a gentle up-and-down movement. |
| 28, 29 | Close `float` and `keyframes`. |
| 30 | `animation: {` – turn the keyframes into **classes** we can use in HTML. |
| 31 | Creates the class `animate-fade-up`: use the *fade-up* steps, take `0.8s` (0.8 seconds), `ease-out` = start fast and slow down at the end, `both` = keep the start look before it begins and the end look after it finishes. |
| 32 | Creates the class `animate-float`: *float* steps, `5s` per round, `ease-in-out` = smooth at both ends, `infinite` = repeat forever. |
| 33–35 | Close `animation`, `extend` and `theme`. |
| 36 | `};` – end of the settings. |

---

## Part 5 – Our own CSS (the style block)

Every page has this `<style>` block in its `<head>` (in `index.html` it is lines 16–62). It is the **same in every page**.

```html
16 │ <style type="text/tailwindcss">
17 │   @layer base {
18 │     html {
19 │       color-scheme: light dark;
20 │     }
21 │     body {
22 │       @apply bg-white font-sans text-slate-700 dark:bg-slate-950 dark:text-slate-300;
23 │     }
24 │     h1, h2, h3 {
25 │       @apply font-display font-semibold text-slate-900 dark:text-white;
26 │     }
27 │     th, td {
28 │       @apply py-2 pr-4 text-left;
29 │     }
30 │   }
31 │
32 │   @layer components {
33 │     .btn {
34 │       display: inline-block;
35 │       padding: 0.75rem 1.5rem;
36 │       border-radius: 0.75rem;
37 │       font-weight: 600;
38 │       transition: background-color 0.2s ease, transform 0.2s ease;
39 │     }
40 │     .btn-primary {
41 │       @apply btn bg-brand-600 text-white hover:-translate-y-0.5 hover:bg-brand-700 active:scale-95;
42 │     }
43 │     .card {
44 │       @apply rounded-2xl border border-slate-200 bg-white p-6 transition duration-300 hover:-translate-y-1 hover:shadow-xl dark:border-slate-800 dark:bg-slate-900;
45 │     }
46 │     .form-input {
47 │       @apply mt-1 block w-full rounded-xl border-slate-300 focus:border-brand-500 focus:ring-brand-500 dark:border-slate-700 dark:bg-slate-800 dark:text-white;
48 │     }
49 │     /* Red border only AFTER the user typed something wrong */
50 │     .form-input:user-invalid {
51 │       @apply border-red-500;
52 │     }
53 │   }
54 │
55 │   /* Respect users who turn off animations in their OS settings */
56 │   @media (prefers-reduced-motion: reduce) {
57 │     * {
58 │       animation: none !important;
59 │       transition: none !important;
60 │     }
61 │   }
62 │ </style>
```

| Line | Explanation |
|------|-------------|
| 16 | `<style type="text/tailwindcss">` – a normal `<style>` tag holds CSS. `type="text/tailwindcss"` tells the Tailwind CDN: "read this block too – it uses Tailwind features like `@layer` and `@apply`". Without this `type`, `@apply` does nothing. |
| 17 | `@layer base {` – default styles for **plain HTML tags**. |
| 18–20 | `html { color-scheme: light dark; }` – plain CSS3. It tells the browser our site supports **both** light and dark mode, so built-in things (form controls, date pickers, scrollbars) also turn dark in dark mode. |
| 21–23 | Every `<body>` gets: `bg-white` white background, `font-sans` (Inter font), `text-slate-700` (dark grey text). In dark mode: `dark:bg-slate-950` (almost black) and `dark:text-slate-300` (light grey text). `@apply` means "use these Tailwind classes inside CSS". |
| 24–26 | Every `<h1>`, `<h2>` and `<h3>` gets: `font-display` (Poppins), `font-semibold` (semi-bold), `text-slate-900` (almost black) – and `dark:text-white` in dark mode. |
| 27–29 | Every table cell (`<th>` and `<td>`) gets `py-2` (8px top/bottom), `pr-4` (16px on the right) and `text-left`. One rule for all cells instead of repeating classes on each cell. |
| 30 | Close `@layer base`. |
| 32 | `@layer components {` – our own **reusable** classes. We make a component when we use the same design many times. |
| 33 | `.btn {` – a class named `btn` for every button. This one is written in **normal CSS3** (no Tailwind) to show that both work together. |
| 34 | `display: inline-block;` – sits in a line with text but can have padding like a box. |
| 35 | `padding: 0.75rem 1.5rem;` – space inside: 12px top/bottom, 24px left/right. |
| 36 | `border-radius: 0.75rem;` – rounded corners. |
| 37 | `font-weight: 600;` – semi-bold text. |
| 38 | `transition: …` – when the background colour or position changes (for example on hover), animate the change over `0.2s` instead of jumping. |
| 39 | Close `.btn`. |
| 40–42 | `.btn-primary` – the main blue button. `@apply btn` = start with everything from `.btn`, then add: `bg-brand-600` blue background, `text-white`, `hover:-translate-y-0.5` move up 2px when the mouse is over it, `hover:bg-brand-700` darker blue on hover, `active:scale-95` shrink to 95% while being clicked (feels like pressing a real button). |
| 43–45 | `.card` – a white box used many times (projects, steps, pricing, add-ons, FAQ, reviews, form). `rounded-2xl` round corners, `border border-slate-200` thin light-grey border, `bg-white`, `p-6` 24px inside space, `transition duration-300` smooth changes in 0.3s, `hover:-translate-y-1` lift 4px on hover, `hover:shadow-xl` big shadow on hover. Dark mode: `dark:border-slate-800 dark:bg-slate-900` = dark border and dark grey card. |
| 46–48 | `.form-input` – one style for every text box. `mt-1` small space above, `block w-full` takes the full width, `rounded-xl` round corners, `border-slate-300` grey border, `focus:border-brand-500 focus:ring-brand-500` blue border + blue glow while typing in it. Dark mode: dark border, dark background (`dark:bg-slate-800`) and white text. |
| 49 | A CSS comment (`/* … */`) – a note for humans. |
| 50–52 | `.form-input:user-invalid` – `:user-invalid` means "**after the user has typed**, the value is wrong" (e.g. an email without `@`). Then the border turns red (`border-red-500`). It waits for the user, so the form isn't red before they even start. |
| 53 | Close `@layer components`. |
| 55 | A comment explaining the next rule. |
| 56 | `@media (prefers-reduced-motion: reduce)` – "only if the visitor has turned **off** animations in their phone/computer settings". Some people feel dizzy from moving things. |
| 57 | `*` – select **every** element. |
| 58 | `animation: none` – stop all animations. `!important` = this rule wins over every other rule. |
| 59 | `transition: none` – stop all smooth transitions too. |
| 60, 61 | Close the brackets. |
| 62 | `</style>` – end of our CSS. |

---

## Part 6 – `index.html` (home page)

The home page has this **skeleton**. Keep this picture in mind – everything below fills it in.

```
<!DOCTYPE html>
<html>
  <head> … information about the page (not visible) … </head>
  <body>
    <header>  logo + menu                     </header>
    <main>
      <section id="hero">          big intro  </section>
      <section id="about">         about me   </section>
      <section id="projects">      my work    </section>
      <section id="services">      prices     </section>
      <section id="faq">           questions  </section>
      <section id="testimonials">  reviews    </section>
    </main>
    <footer>  email + copyright               </footer>
  </body>
</html>
```

### 6.1 The `<head>` – information about the page (lines 1–63)

```html
 1 │ <!DOCTYPE html>
 2 │ <html lang="en">
 3 │ <head>
 4 │   <meta charset="UTF-8">
 5 │   <meta name="viewport" content="width=device-width, initial-scale=1.0">
 6 │   <title>Ekramul Islam – Front-End Developer</title>
 7 │   <meta name="description" content="Freelance front-end developer building fast, responsive websites.">
 8 │   <link rel="preconnect" href="https://fonts.googleapis.com">
 9 │   <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&amp;family=Poppins:wght@600;700&amp;display=swap">
10 │   <meta property="og:title" content="Ekramul Islam – Front-End Developer">
11 │   <meta property="og:description" content="Fast, responsive websites with HTML5 and Tailwind CSS.">
12 │   <meta property="og:image" content="https://your-site.vercel.app/assets/images/avatar.svg">
13 │   <link rel="icon" href="assets/images/favicon.svg" type="image/svg+xml">
14 │   <script src="https://cdn.tailwindcss.com?plugins=forms"></script>
15 │   <script src="assets/js/tailwind-config.js"></script>
```

*(Lines 16–62 are our `<style>` block – explained in [Part 5](#part-5--our-own-css-the-style-block).)*

```html
63 │ </head>
64 │ <body>
```

| Line | Explanation |
|------|-------------|
| 1 | `<!DOCTYPE html>` – tells the browser "this is a modern **HTML5** page". Always the very first line. |
| 2 | `<html lang="en">` – the start of the whole page. `lang="en"` = the page is in English (helps Google and screen readers; use `bn` for Bangla). Closed on the last line with `</html>`. |
| 3 | `<head>` – starts the **head**: information **about** the page. Nothing here is shown on the page itself. |
| 4 | `<meta charset="UTF-8">` – use the UTF-8 alphabet, which supports every language (Bangla too) and emoji. |
| 5 | `<meta name="viewport" …>` – makes the page fit **phone screens**. `width=device-width` = use the phone's real width; `initial-scale=1.0` = don't zoom. Without this line, phones show a tiny desktop page. |
| 6 | `<title>` – the text on the **browser tab**, and the blue link text in Google results. |
| 7 | `<meta name="description">` – the short grey text under the link in Google results. |
| 8 | `<link rel="preconnect">` – "start connecting to Google Fonts early" → fonts load faster. |
| 9 | Loads the two fonts from Google: **Inter** (weights 400 = normal, 600 = semi-bold) and **Poppins** (600, 700). `&amp;` is how we write the `&` symbol inside HTML attributes. `display=swap` = show normal text first, swap to the nice font when it has loaded. |
| 10 | `og:title` – **Open Graph** title: the title shown when someone shares your link on Facebook, LinkedIn or WhatsApp. |
| 11 | `og:description` – the text in that share preview. |
| 12 | `og:image` – the picture in that share preview. Must be a **full** web address (`https://…`). Change `your-site` to your real Vercel name. |
| 13 | `<link rel="icon">` – the **favicon**: the small logo on the browser tab. `type="image/svg+xml"` = it's an SVG image. |
| 14 | `<script src="https://cdn.tailwindcss.com?plugins=forms">` – loads **Tailwind CSS** from its CDN (a server on the internet). It reads all our class names and creates the design while the page loads. `?plugins=forms` also turns on the **forms plugin**, which gives inputs and checkboxes clean default styles. **Without this line the page has no design.** |
| 15 | `<script src="assets/js/tailwind-config.js">` – loads **our settings** (brand colour, fonts, animations – see Part 4). It must come **after** line 14. |
| 16–62 | Our own CSS – see Part 5. |
| 63 | `</head>` – end of the head. |
| 64 | `<body>` – start of everything **visible**. Closed at line 456. |

### 6.2 The header and menu (lines 66–93)

```html
66 │ <header class="sticky top-0 z-40 border-b border-slate-200 dark:border-slate-800 bg-white/80 dark:bg-slate-950/80 backdrop-blur">
67 │   <div class="mx-auto flex max-w-6xl flex-wrap items-center justify-between gap-4 px-4 py-4">
68 │     <a href="index.html" class="font-display text-xl font-bold text-slate-900 dark:text-white">Ekramul<span class="text-brand-600 dark:text-brand-500">.dev</span></a>
69 │     <nav aria-label="Main">
70 │       <ul class="hidden gap-6 md:flex">
71 │         <li><a href="#about" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">About</a></li>
72 │         <li><a href="#projects" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Projects</a></li>
73 │         <li><a href="#services" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Services</a></li>
74 │         <li><a href="contact.html" class="text-slate-600 dark:text-slate-300 hover:text-brand-600">Contact</a></li>
75 │       </ul>
76 │     </nav>
77 │
78 │     <button type="button" popovertarget="mobile-menu" class="rounded-lg p-2 hover:bg-slate-100 dark:hover:bg-slate-800 md:hidden">
79 │       <span class="sr-only">Open menu</span>
80 │       <svg class="h-6 w-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M4 6h16M4 12h16M4 18h16"/></svg>
81 │     </button>
82 │   </div>
83 │
84 │   <nav id="mobile-menu" popover aria-label="Mobile" class="m-0 ml-auto h-dvh w-64 bg-white dark:bg-slate-900 p-6 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
85 │     <button type="button" popovertarget="mobile-menu" popovertargetaction="hide" class="mb-6 font-semibold">✕ Close</button>
86 │     <ul class="space-y-4 text-lg">
87 │       <li><a href="#about" class="hover:text-brand-600">About</a></li>
88 │       <li><a href="#projects" class="hover:text-brand-600">Projects</a></li>
89 │       <li><a href="#services" class="hover:text-brand-600">Services</a></li>
90 │       <li><a href="contact.html" class="hover:text-brand-600">Contact</a></li>
91 │     </ul>
92 │   </nav>
93 │ </header>
```

**Lines 66–82: the top bar (logo + desktop menu + ☰ button)**

| Line | Explanation |
|------|-------------|
| 66 | `<header>` – the top area of the page. Classes: `sticky top-0` = when you scroll, the header **sticks** to the top of the screen. `z-40` = it stays **on top** of other content (higher z = closer to you). `border-b border-slate-200` = a thin grey line at the **b**ottom. `bg-white/80` = white background at 80% (slightly see-through). `backdrop-blur` = blur whatever is behind it → a "glass" effect. **Dark mode:** `dark:border-slate-800` = a dark grey line and `dark:bg-slate-950/80` = almost-black glass, used only when the visitor's device is in dark mode. **This is the pattern for every `dark:` class in the whole project:** each light colour gets a dark partner right next to it (`text-slate-900 dark:text-white`, `bg-slate-50 dark:bg-slate-900`, `text-brand-600 dark:text-brand-500`…). We won't repeat this on every line. |
| 67 | A `<div>` (a plain box with no meaning) used only for layout. `mx-auto max-w-6xl` = maximum 1152px wide and centred. `flex` = put the children **in a row**. `flex-wrap` = if there is not enough space, go to the next line. `items-center` = centre them **vertically**. `justify-between` = push them to the **two ends** (logo left, menu right). `gap-4` = 16px space between. `px-4 py-4` = 16px inside space. |
| 68 | The **logo**. `<a href="index.html">` = a link to the home page (every website's logo does this). `font-display text-xl font-bold text-slate-900` = Poppins font, bigger, bold, almost black. Inside, `<span class="text-brand-600">.dev</span>` colours only the `.dev` part blue. `<span>` is a small box used to style **part** of a text. |
| 69 | `<nav aria-label="Main">` – **nav** = navigation (a menu). `aria-label="Main"` gives it a name for people using screen readers (blind users). |
| 70 | `<ul>` – an **unordered list** (a list without numbers). A menu is a list of links. `hidden` = **not shown** on phones. `md:flex` = from 768px (tablets) show it as a **row**. `gap-6` = 24px between the links. |
| 71 | `<li>` = one **list item**. Inside, a link. `href="#about"` – the `#` means "jump to the element with `id="about"` **on this page**". `text-slate-600` grey text, `hover:text-brand-600` blue when the mouse is over it. |
| 72–73 | Same pattern: links to `#projects` and `#services`. |
| 74 | Link to **another page**: `contact.html` (no `#`). |
| 75 | `</ul>` – end of the list. |
| 76 | `</nav>` – end of the desktop menu. |
| 78 | `<button>` – the **☰ menu button** for phones. `type="button"` = a normal button (not a form "send" button). `popovertarget="mobile-menu"` – **HTML5 magic**: clicking it **opens/closes** the element whose `id` is `mobile-menu` (line 84). No JavaScript needed! `rounded-lg p-2` = rounded, small inside space. `hover:bg-slate-100` = light grey background on hover. `md:hidden` = **hidden** from 768px (on bigger screens we show the normal menu instead). `dark:hover:bg-slate-800` = in dark mode, a dark grey background on hover. |
| 79 | `<span class="sr-only">Open menu</span>` – `sr-only` = "**s**creen **r**eader only": invisible on screen, but read aloud to blind users. The button only shows an icon, so we need this text. |
| 80 | The **☰ icon**, drawn with **SVG** (a picture made of code). `h-6 w-6` = 24×24px. `viewBox="0 0 24 24"` = the drawing area is 24×24. `fill="none"` = don't fill shapes. `stroke="currentColor"` = draw lines in the same colour as the text. `stroke-width="2"` = line thickness. `aria-hidden="true"` = screen readers skip it (line 79 already describes it). The `<path d="…">` draws: `M4 6` = **M**ove to point (4, 6), `h16` = draw a **h**orizontal line 64 long. Three times at heights 6, 12, 18 = three lines ☰. |
| 81 | `</button>` – end of the button. |
| 82 | `</div>` – end of the top bar (opened on line 67). |

**Lines 84–92: the mobile menu panel**

| Line | Explanation |
|------|-------------|
| 84 | A second `<nav>` – the **side panel** that opens on phones. `id="mobile-menu"` – the button on line 78 points to this name. `popover` – makes it a **popover**: hidden until its button is clicked, then shown **on top of everything**. It also closes when you press **Esc** or click outside. `aria-label="Mobile"` – a name for screen readers. Classes: `m-0 ml-auto` = no margin, except push it to the **right** side. `h-dvh` = full screen height. `w-64` = 256px wide. `bg-white p-6 shadow-2xl` = white, 24px inside space, big shadow. `backdrop:bg-slate-900/50` = the area **behind** the panel becomes dark and 50% see-through. `text-slate-700 dark:text-slate-300` = the text colour – popovers don't automatically take the page's text colour, so we set it. |
| 85 | The **Close** button. `popovertarget="mobile-menu"` + `popovertargetaction="hide"` = this button can only **close** the panel. `mb-6` = 24px space below. `font-semibold`. `✕` is just a text character. |
| 86 | `<ul class="space-y-4 text-lg">` – the list of links. `space-y-4` = 16px vertical space between items. `text-lg` = a bit bigger text (easier to tap on phones). |
| 87–90 | The same four links as the desktop menu. |
| 91, 92 | Close the list and the panel. |
| 93 | `</header>` – end of the header. |

### 6.3 The hero section (lines 95–106)

The **hero** is the big first part of a website: who you are and what you do.

```html
 95 │ <main>
 96 │   <section id="hero" class="mx-auto grid max-w-6xl items-center gap-12 px-4 py-20 md:grid-cols-2">
 97 │     <div class="animate-fade-up">
 98 │       <h1 class="text-4xl font-bold leading-tight md:text-6xl">I build <span class="text-brand-600 dark:text-brand-500">fast, modern</span> websites</h1>
 99 │       <p class="mt-6 max-w-xl text-lg">Hi, I'm Ekramul – a front-end developer from Dhaka. I turn ideas into responsive websites.</p>
100 │       <a href="contact.html" class="btn-primary mt-8">Hire me</a>
101 │     </div>
102 │     <img src="assets/images/avatar-400.png"
103 │          srcset="assets/images/avatar-400.png 400w, assets/images/avatar-800.png 800w"
104 │          sizes="400px"
105 │          alt="Portrait of Ekramul Islam" width="400" height="400" class="mx-auto w-full max-w-sm animate-float rounded-3xl shadow-xl">
106 │   </section>
```

| Line | Explanation |
|------|-------------|
| 95 | `<main>` – the **main content** of this page (everything except header and footer). Only **one** `<main>` per page. Closed at line 445. |
| 96 | `<section id="hero">` – a **section** is a block about one topic. `id="hero"` gives it a name. Classes: `mx-auto max-w-6xl` = centred, max 1152px. `grid` = turn on **grid layout** (default: 1 column → on phones, text on top and photo below). `md:grid-cols-2` = from tablets, **2 columns** side by side. `items-center` = centre them vertically. `gap-12` = 48px between the columns. `px-4 py-20` = 16px left/right, 80px top/bottom inside space. |
| 97 | `<div class="animate-fade-up">` – a box that groups the text, so the grid has exactly **2 children** (text box + photo). `animate-fade-up` = our custom animation: rises up while appearing. |
| 98 | `<h1>` – **heading level 1**: the most important title on the page. **Only one `<h1>` per page** – Google reads it as the page topic. Classes: `text-4xl` big text on phones, `md:text-6xl` even bigger on tablets+, `font-bold`, `leading-tight` = lines closer together. The `<span class="text-brand-600">` colours "fast, modern" blue. |
| 99 | `<p>` – a **paragraph** of text. `mt-6` = 24px space above. `max-w-xl` = max 576px wide (short lines are easier to read). `text-lg` = slightly bigger text. |
| 100 | The **Hire me** button. It's an `<a>` link to `contact.html` that **looks** like a button, because of our component `btn-primary`. `mt-8` = 32px space above. |
| 101 | `</div>` – end of the text box. |
| 102–105 | An **image** (no closing tag), written over 4 lines to make it easier to read – the browser doesn't mind. Line 102: `src` = the normal file (used by old browsers). Line 103: `srcset` = **the same photo in two sizes**: `avatar-400.png` is `400w` (400 pixels wide), `avatar-800.png` is `800w`. Line 104: `sizes="400px"` = "on the page this image is shown about 400px wide". The browser then picks the right file: a normal screen downloads the 400px file; a sharp phone screen ("Retina", 2× pixels) downloads the 800px file so the photo isn't blurry. Line 105: `alt` = a text description, read to blind users and shown if the image fails. **Every image needs `alt`.** `width="400" height="400"` = the real size, so the browser reserves the space and the page doesn't "jump" while loading. Classes: `mx-auto` centred, `w-full max-w-sm` = fills its column but max 384px, `animate-float` = our floating animation, `rounded-3xl` = very round corners, `shadow-xl` = big shadow. |
| 106 | `</section>` – end of the hero. |

### 6.4 The about section + video (lines 108–167)

```html
108 │ <section id="about" class="bg-slate-50 dark:bg-slate-900 py-20">
109 │   <div class="mx-auto grid max-w-6xl gap-12 px-4 lg:grid-cols-2">
110 │     <div>
111 │       <h2 class="text-3xl">About me</h2>
112 │       <p class="mt-4">I build websites with <strong>HTML5</strong> and <strong>Tailwind CSS</strong> for small businesses.</p>
113 │       <h3 class="mt-8 text-xl">Skills</h3>
114 │       <ul class="mt-3 flex flex-wrap gap-2">
115 │         <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">HTML5</li>
116 │         <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">CSS3</li>
117 │         <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">Tailwind CSS</li>
118 │         <li class="rounded-full bg-white dark:bg-slate-800 px-4 py-1 text-sm shadow-sm">Git &amp; GitHub</li>
119 │       </ul>
120 │
121 │       <h3 class="mt-8 text-xl">My learning journey</h3>
122 │       <div class="mt-3 overflow-x-auto">
123 │         <table class="w-full text-sm">
124 │           <caption class="pb-2 text-left text-slate-500 dark:text-slate-400">Courses and training I have completed</caption>
125 │           <thead class="border-b-2 border-slate-300 dark:border-slate-700 text-slate-900 dark:text-white">
126 │             <tr>
127 │               <th scope="col">Year</th>
128 │               <th scope="col">Course</th>
129 │               <th scope="col">Where</th>
130 │             </tr>
131 │           </thead>
132 │           <tbody class="divide-y divide-slate-200 dark:divide-slate-800">
133 │             <tr>
134 │               <td>2024</td>
135 │               <td>HTML &amp; CSS basics</td>
136 │               <td>YouTube (self-study)</td>
137 │             </tr>
138 │             <tr>
139 │               <td>2025</td>
140 │               <td>Web design with Tailwind CSS</td>
141 │               <td>Online course</td>
142 │             </tr>
143 │             <tr>
144 │               <td>2026</td>
145 │               <td>Freelancing with AI tools</td>
146 │               <td>Online course</td>
147 │             </tr>
148 │           </tbody>
149 │         </table>
150 │       </div>
151 │     </div>
152 │     <div>
153 │       <h3 class="text-xl">Say hello</h3>
154 │       <video controls width="640" height="360" poster="assets/images/video-poster.svg" class="mt-3 aspect-video w-full rounded-2xl">
155 │         <source src="assets/media/intro.mp4" type="video/mp4">
156 │         <track kind="captions" src="assets/media/intro-captions.vtt" srclang="en" label="English">
157 │         Your browser does not support video.
158 │       </video>
159 │
160 │       <p class="mt-4 text-sm">Prefer to listen? Here is the audio version:</p>
161 │       <audio controls class="mt-2 w-full">
162 │         <source src="assets/media/intro.mp3" type="audio/mpeg">
163 │         Your browser does not support audio.
164 │       </audio>
165 │     </div>
166 │   </div>
167 │ </section>
```

| Line | Explanation |
|------|-------------|
| 108 | `<section id="about">` – the about section. The menu link `#about` jumps here. `bg-slate-50` = very light grey background across the **full width**. `py-20` = 80px top and bottom. |
| 109 | An inner `<div>` that centres the content (`mx-auto max-w-6xl px-4`) and makes a grid: 1 column on phones, `lg:grid-cols-2` = 2 columns on laptops (text left, video right). `gap-12` = 48px between. *Why a separate div?* The section's grey background should be full width, but the content should not. |
| 110 | `<div>` – the **left** column (text). |
| 111 | `<h2>` – **heading level 2**: the title of a section. Headings go in order: `h1` → `h2` → `h3`. Never skip a level. `text-3xl` = big. |
| 112 | A paragraph. `mt-4` = 16px space above. `<strong>` = **important** text (shown bold). |
| 113 | `<h3>` – a smaller heading **inside** the about section. `mt-8` = 32px space above, `text-xl`. |
| 114 | `<ul>` – the skills list. `flex` = items in a **row**. `flex-wrap` = go to the next line when full. `gap-2` = 8px between. `mt-3` = 12px above. |
| 115–118 | Each skill is a `<li>` styled like a **pill/badge**: `rounded-full` = completely round ends, `bg-white` white, `px-4 py-1` = 16px left/right and 4px top/bottom inside space, `text-sm` small text, `shadow-sm` small shadow. On line 118, `&amp;` shows the `&` character. In dark mode the pills are dark grey (`dark:bg-slate-800`) so they still stand out on the dark section. |
| 119 | `</ul>` – end of the list. |
| 121 | A new `<h3>` for the table. |
| 122 | A `<div>` around the table. `overflow-x-auto` = if the table is wider than a small phone screen, it **scrolls sideways inside this box** instead of breaking the page. `mt-3` = 12px above. |
| 123 | `<table>` – a grid of **data** in rows and columns. Only for real data – never for page layout. `w-full` = full width, `text-sm` = small text. |
| 124 | `<caption>` – the table's **title**. Screen readers read it first. `pb-2` = 8px space below, `text-left`, `text-slate-500` = grey. |
| 125 | `<thead>` – the **head** part (the column titles). `border-b-2 border-slate-300` = a 2px grey line under it. `text-slate-900` = darker text. |
| 126 | `<tr>` – a **t**able **r**ow. |
| 127–129 | `<th scope="col">` – **t**able **h**eader cells. `scope="col"` = "I am the title of this **column**" (helps screen readers). Their spacing comes from our `th, td` rule (Part 5). |
| 130, 131 | Close the row and the head. |
| 132 | `<tbody>` – the **body** part (the data rows). `divide-y divide-slate-200` = a thin grey line **between** the rows. |
| 133–137 | One data row: `<tr>` with three `<td>` (**t**able **d**ata) cells – year, course, where. Every row must have the **same number** of cells as the header (3). |
| 138–147 | Two more rows (2025, 2026). |
| 148–150 | Close `<tbody>`, `<table>` and the scroll `<div>`. |
| 151 | `</div>` – end of the left column. |
| 152 | `<div>` – the **right** column (video). |
| 153 | `<h3>` – heading "Say hello". |
| 154 | `<video>` – a video player. `controls` = show play/pause/volume buttons. `width="640" height="360"` = size ratio. `poster` = a picture shown **before** the video plays. Classes: `mt-3` space above, `aspect-video` = always the 16:9 shape, `w-full` full width, `rounded-2xl` round corners. |
| 155 | `<source>` – **which video file** to play. `type="video/mp4"` tells the browser the format. You can add more `<source>` lines with other formats; the browser plays the first one it understands. |
| 156 | `<track>` – **subtitles**. `kind="captions"` = captions for people who can't hear. `src` = the `.vtt` subtitle file. `srclang="en"` = English. `label="English"` = the name in the subtitles menu. |
| 157 | Text that only **very old browsers** show if they can't play video. |
| 158 | `</video>` – end of the player. |
| 160 | A short paragraph introducing the audio. `mt-4 text-sm`. |
| 161 | `<audio>` – an audio player. Works like `<video>`: `controls` shows play/pause/volume. `mt-2 w-full` = full-width player. |
| 162 | `<source>` – the audio file. `type="audio/mpeg"` = it's an **MP3**. |
| 163 | Fallback text for very old browsers. |
| 164 | `</audio>`. |
| 165, 166 | Close the right column and the grid div. |
| 167 | `</section>` – end of about. |

### 6.5 The projects section (lines 169–269)

```html
169 │ <section id="projects" class="mx-auto max-w-6xl px-4 py-20">
170 │   <h2 class="text-3xl">Projects</h2>
171 │
172 │   <div class="mt-8 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
173 │     <article class="card group flex flex-col">
174 │       <figure class="overflow-hidden rounded-xl">
175 │         <img src="assets/images/restaurant.svg" alt="Spice Garden website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
176 │         <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">Restaurant landing page</figcaption>
177 │       </figure>
178 │       <h3 class="mt-4 text-xl">Spice Garden</h3>
179 │       <p class="mt-2 flex-1">A one-page website with menu and reservation form.</p>
180 │       <div class="mt-4 flex gap-6">
181 │         <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
182 │         <button type="button" popovertarget="case-spice" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
183 │       </div>
184 │
185 │       <div id="case-spice" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
186 │         <h3 class="text-xl">Spice Garden – case study</h3>
187 │         <dl class="mt-4 space-y-3 text-sm">
188 │           <div>
189 │             <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
190 │             <dd>The restaurant took all orders by phone and had no website.</dd>
191 │           </div>
192 │           <div>
193 │             <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
194 │             <dd>A one-page website with the menu, photos and a reservation form.</dd>
195 │           </div>
196 │           <div>
197 │             <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
198 │             <dd>30% of table bookings now come from the website.</dd>
199 │           </div>
200 │         </dl>
201 │         <button type="button" popovertarget="case-spice" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
202 │       </div>
203 │     </article>
204 │
205 │     <article class="card group flex flex-col">
206 │       <figure class="overflow-hidden rounded-xl">
207 │         <img src="assets/images/agency.svg" alt="BrightPath website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
208 │         <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">Agency business website</figcaption>
209 │       </figure>
210 │       <h3 class="mt-4 text-xl">BrightPath</h3>
211 │       <p class="mt-2 flex-1">A five-page website for a digital agency.</p>
212 │       <div class="mt-4 flex gap-6">
213 │         <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
214 │         <button type="button" popovertarget="case-brightpath" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
215 │       </div>
216 │
217 │       <div id="case-brightpath" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
218 │         <h3 class="text-xl">BrightPath – case study</h3>
219 │         <dl class="mt-4 space-y-3 text-sm">
220 │           <div>
221 │             <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
222 │             <dd>The agency's old website was slow and broke on phones.</dd>
223 │           </div>
224 │           <div>
225 │             <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
226 │             <dd>A new 5-page responsive website built with Tailwind CSS.</dd>
227 │           </div>
228 │           <div>
229 │             <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
230 │             <dd>The page speed score went from 48 to 98.</dd>
231 │           </div>
232 │         </dl>
233 │         <button type="button" popovertarget="case-brightpath" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
234 │       </div>
235 │     </article>
236 │
237 │     <article class="card group flex flex-col">
238 │       <figure class="overflow-hidden rounded-xl">
239 │         <img src="assets/images/ecommerce.svg" alt="ShopEasy website screenshot" width="800" height="500" loading="lazy" class="transition duration-500 group-hover:scale-110">
240 │         <figcaption class="mt-2 text-sm text-slate-500 dark:text-slate-400">E-commerce product page</figcaption>
241 │       </figure>
242 │       <h3 class="mt-4 text-xl">ShopEasy</h3>
243 │       <p class="mt-2 flex-1">A product listing page built from a design mockup.</p>
244 │       <div class="mt-4 flex gap-6">
245 │         <a href="https://example.com" class="font-semibold text-brand-600 dark:text-brand-500 hover:underline">Live demo</a>
246 │         <button type="button" popovertarget="case-shopeasy" class="font-semibold text-slate-600 dark:text-slate-300 hover:underline">Case study</button>
247 │       </div>
248 │
249 │       <div id="case-shopeasy" popover class="w-11/12 max-w-lg rounded-2xl bg-white dark:bg-slate-900 p-8 text-slate-700 dark:text-slate-300 shadow-2xl backdrop:bg-slate-900/50">
250 │         <h3 class="text-xl">ShopEasy – case study</h3>
251 │         <dl class="mt-4 space-y-3 text-sm">
252 │           <div>
253 │             <dt class="font-semibold text-slate-900 dark:text-white">Problem</dt>
254 │             <dd>The client had an AI-made design but no code.</dd>
255 │           </div>
256 │           <div>
257 │             <dt class="font-semibold text-slate-900 dark:text-white">Solution</dt>
258 │             <dd>I turned the design into clean HTML and Tailwind CSS in 2 days.</dd>
259 │           </div>
260 │           <div>
261 │             <dt class="font-semibold text-slate-900 dark:text-white">Result</dt>
262 │             <dd>The shop launched one week earlier than planned.</dd>
263 │           </div>
264 │         </dl>
265 │         <button type="button" popovertarget="case-shopeasy" popovertargetaction="hide" class="btn-primary mt-6">Close</button>
266 │       </div>
267 │     </article>
268 │   </div>
269 │ </section>
```

The three project cards (lines 173–203, 205–235, 237–267) are **the same code** with different text and images.
We explain the first one; the others work exactly the same way.

| Line | Explanation |
|------|-------------|
| 169 | `<section id="projects">` – centred (`mx-auto max-w-6xl px-4`), 80px top/bottom (`py-20`). |
| 170 | The section title. |
| 172 | The **grid** that holds the cards. `grid` = 1 column on phones. `sm:grid-cols-2` = 2 columns from 640px. `lg:grid-cols-3` = 3 columns from 1024px. `gap-6` = 24px between cards. `mt-8` = 32px below the title. **This "1 → 2 → 3 columns" pattern is the most used layout on the internet.** |
| 173 | `<article>` – a piece of content that makes sense **on its own** (like a news story or a product card). `card` = our white box component. `group` = marks this card as a "group" so its children can react when **the card** is hovered (see line 175). `flex flex-col` = children stacked in a **column**. |
| 174 | `<figure>` – an image with its caption. `overflow-hidden` = anything that grows bigger than this box is **cut off** (needed for the zoom on line 175). `rounded-xl` = round corners. |
| 175 | The screenshot. `loading="lazy"` = only download the image when the visitor **scrolls near it** → the page opens faster. `transition duration-500` = animate changes over 0.5 seconds. `group-hover:scale-110` = when the mouse is over the **card** (the `group`), zoom the image to 110%. Because of `overflow-hidden` on line 174, the bigger image stays inside its box. |
| 176 | `<figcaption>` – the caption **for** the figure. `text-sm text-slate-500` = small grey text. |
| 177 | `</figure>` – end of figure. |
| 178 | `<h3>` – the project name. |
| 179 | The description. `flex-1` = "take all the **extra** space". Because some descriptions are longer than others, this pushes the link on line 180 to the **bottom** – so all "Live demo" links line up nicely. |
| 180 | A `<div>` that puts the two actions **side by side**: `flex` = in a row, `gap-6` = 24px between, `mt-4` = 16px above. |
| 181 | Link to the live project. `font-semibold text-brand-600` = semi-bold blue. `hover:underline` = underline on hover. Replace `https://example.com` with your real project link. |
| 182 | The **Case study** button. `popovertarget="case-spice"` opens the popover with `id="case-spice"` (line 185) – the same no-JavaScript trick as the mobile menu. `text-slate-600` = grey, so the live link stays the main action. |
| 183 | Close the row. |
| 185 | The **modal** (popup). `id="case-spice"` – **each project needs its own id** (`case-brightpath`, `case-shopeasy`). `popover` = hidden until its button is clicked, then shown on top of everything; **Esc** or clicking outside closes it. We don't add position classes, so the browser **centres** it – that's what makes it look like a modal. `w-11/12` = 11/12 of the screen width on phones, `max-w-lg` = but never wider than 512px. `rounded-2xl bg-white p-8 shadow-2xl` = a white rounded box with big shadow. `text-slate-700` = text colour. `backdrop:bg-slate-900/50` = darken the page behind it. |
| 186 | The modal's title. |
| 187 | `<dl>` – a **description list**: a list of terms and their descriptions. `space-y-3` = 12px between the items. |
| 188–191 | One item: `<dt>` = the **term** ("Problem", shown bold and dark), `<dd>` = its **description**. The `<div>` groups each pair. |
| 192–199 | Two more pairs: Solution and Result. *Problem → Solution → Result* is how freelancers show the **value** of their work. |
| 200 | `</dl>`. |
| 201 | The **Close** button: `popovertargetaction="hide"` = this button only closes the modal. `btn-primary mt-6` = our blue button with 24px above. |
| 202 | Close the modal. |
| 203 | `</article>` – end of card 1. |
| 205–267 | Cards 2 and 3 – same structure. |
| 268 | `</div>` – end of the grid. |
| 269 | `</section>` – end of projects. |

### 6.5b The "How I work" section (lines 271–300)

This section was made in Class 1.5 with **v0.dev** (an AI UI tool) and then cleaned up.

```html
271 │ <section id="process" class="mx-auto max-w-6xl px-4 py-20" aria-labelledby="process-title">
272 │   <h2 id="process-title" class="text-center text-3xl">How I work</h2>
273 │   <p class="mt-3 text-center">A simple 4-step process from idea to live website.</p>
274 │
275 │   <ol class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
276 │     <li class="card">
277 │       <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">01</span>
278 │       <h3 class="mt-2 text-lg">Discuss</h3>
279 │       <p class="mt-1 text-sm">We talk about your goals, pages and deadline.</p>
280 │     </li>
281 │
282 │     <li class="card">
283 │       <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">02</span>
284 │       <h3 class="mt-2 text-lg">Design</h3>
285 │       <p class="mt-1 text-sm">I prepare the layout and colours for your approval.</p>
286 │     </li>
287 │
288 │     <li class="card">
289 │       <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">03</span>
290 │       <h3 class="mt-2 text-lg">Develop</h3>
291 │       <p class="mt-1 text-sm">I build the responsive website and share progress.</p>
292 │     </li>
293 │
294 │     <li class="card">
295 │       <span class="font-display text-4xl font-bold text-brand-100 dark:text-brand-900" aria-hidden="true">04</span>
296 │       <h3 class="mt-2 text-lg">Deliver</h3>
297 │       <p class="mt-1 text-sm">Your site goes live, with the code on GitHub.</p>
298 │     </li>
299 │   </ol>
300 │ </section>
```

The four steps (lines 276–298) are the same code with different text. We explain the first one.

| Line | Explanation |
|------|-------------|
| 271 | `<section id="process">` – centred, 80px top/bottom. `aria-labelledby` names it with its heading. |
| 272 | The heading, centred. |
| 273 | A one-line subtitle. |
| 275 | `<ol>` – an **ordered** (numbered) list. The steps happen in this order, so `ol` is the right tag. The grid makes it 1 column on phones, 2 from 640px (`sm:`) and 4 from 1024px (`lg:`), with 24px gaps. `mt-10` = 40px above. |
| 276 | Each step is an `<li>` that looks like our `card`. |
| 277 | The big step number "01". `font-display text-4xl font-bold` = big Poppins number. `text-brand-100` = very light blue (decoration). `aria-hidden="true"` = screen readers skip it – the `<ol>` already tells them the order. |
| 278 | The step title. `text-lg` = slightly bigger, `mt-2` = 8px above. |
| 279 | One sentence. `text-sm` = small. |
| 280 | `</li>`. |
| 282–298 | Steps 02–04, same pattern. |
| 299, 300 | Close the list and the section. |

### 6.6 The services & pricing section (lines 302–367)

```html
302 │ <section id="services" class="py-20" aria-labelledby="services-title">
303 │   <div class="mx-auto max-w-6xl px-4">
304 │     <h2 id="services-title" class="text-center text-3xl">Services &amp; pricing</h2>
305 │     <p class="mt-3 text-center">Fixed prices. Clear deliverables. No surprises.</p>
306 │
307 │     <div class="mt-14 grid items-start gap-8 md:grid-cols-3">
308 │       <article class="card flex flex-col">
309 │         <h3 class="text-xl">Basic</h3>
310 │         <p class="mt-2 text-sm">A simple one-page website.</p>
311 │         <p class="mt-6"><span class="text-5xl font-bold text-slate-900 dark:text-white">$50</span> / project</p>
312 │         <p class="mt-1 text-sm">Delivery in 3 days</p>
313 │         <ul class="mt-6 flex-1 space-y-3 text-sm">
314 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> 1 landing page</li>
315 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Responsive design</li>
316 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Contact form</li>
317 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> 1 revision</li>
318 │         </ul>
319 │         <a href="contact.html" class="btn mt-8 w-full border border-slate-300 dark:border-slate-700 text-center hover:border-brand-600">Choose Basic</a>
320 │       </article>
321 │
322 │       <article class="relative rounded-3xl bg-brand-900 p-8 text-white shadow-2xl ring-2 ring-brand-500 flex flex-col md:-translate-y-4">
323 │         <p class="absolute -top-3 left-1/2 -translate-x-1/2 rounded-full bg-amber-400 px-3 py-1 text-xs font-bold text-slate-900">MOST POPULAR</p>
324 │         <h3 class="text-xl text-white">Standard</h3>
325 │         <p class="mt-2 text-sm">A complete business website.</p>
326 │         <p class="mt-6"><span class="text-5xl font-bold">$120</span> / project</p>
327 │         <p class="mt-1 text-sm">Delivery in 5 days</p>
328 │         <ul class="mt-6 flex-1 space-y-3 text-sm">
329 │           <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Up to 5 pages</li>
330 │           <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Responsive design</li>
331 │           <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> Contact form + animations</li>
332 │           <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> GitHub repo + deploy</li>
333 │           <li class="flex gap-2"><span class="text-amber-400" aria-hidden="true">✓</span> 3 revisions</li>
334 │         </ul>
335 │         <a href="contact.html" class="btn mt-8 w-full bg-white text-center text-brand-900 hover:bg-brand-50">Choose Standard</a>
336 │       </article>
337 │
338 │       <article class="card flex flex-col">
339 │         <h3 class="text-xl">Premium</h3>
340 │         <p class="mt-2 text-sm">Custom design and extra polish.</p>
341 │         <p class="mt-6"><span class="text-5xl font-bold text-slate-900 dark:text-white">$250</span> / project</p>
342 │         <p class="mt-1 text-sm">Delivery in 10 days</p>
343 │         <ul class="mt-6 flex-1 space-y-3 text-sm">
344 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Up to 10 pages</li>
345 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Custom UI design</li>
346 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Advanced animations + SEO</li>
347 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Custom domain setup</li>
348 │           <li class="flex gap-2"><span class="text-brand-600 dark:text-brand-500" aria-hidden="true">✓</span> Unlimited revisions (14 days)</li>
349 │         </ul>
350 │         <a href="contact.html" class="btn mt-8 w-full border border-slate-300 dark:border-slate-700 text-center hover:border-brand-600">Choose Premium</a>
351 │       </article>
352 │     </div>
353 │
354 │     <div class="mt-12 rounded-2xl bg-amber-50 dark:bg-amber-950 p-6 text-center ring-1 ring-amber-200 dark:ring-amber-900">
355 │       <p class="font-semibold text-slate-900 dark:text-white">🎉 Launch offer: 20% off your first website</p>
356 │       <p class="mt-1 text-sm">For my first 5 clients, in exchange for an honest review. Valid until 31 December 2026.</p>
357 │     </div>
358 │
359 │     <h3 class="mt-12 text-center text-xl">Add-ons</h3>
360 │     <ul class="mt-6 grid gap-4 sm:grid-cols-2 lg:grid-cols-4">
361 │       <li class="card flex items-center justify-between"><span>Extra page</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$15</span></li>
362 │       <li class="card flex items-center justify-between"><span>Express delivery</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$30</span></li>
363 │       <li class="card flex items-center justify-between"><span>Logo &amp; favicon</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$20</span></li>
364 │       <li class="card flex items-center justify-between"><span>1 month support</span> <span class="font-semibold text-brand-600 dark:text-brand-500">+$40</span></li>
365 │     </ul>
366 │   </div>
367 │ </section>
```

Cards 1 (Basic) and 3 (Premium) are the same design. Card 2 (Standard) is **special** – it's highlighted.

**Section, title and grid**

| Line | Explanation |
|------|-------------|
| 302 | `<section id="services">`. `aria-labelledby="services-title"` = "the name of this section is the text of the element with `id="services-title"`" (line 304). Helps screen readers. |
| 303 | Centring box. |
| 304 | The `<h2>` with `id="services-title"`. `text-center` = centred text. `&amp;` = `&`. |
| 305 | Subtitle. `mt-3` = 12px above. |
| 307 | The grid: 1 column on phones, `md:grid-cols-3` = 3 columns from tablets. `gap-8` = 32px. `items-start` = cards are only as tall as their content (so the lifted middle card doesn't stretch the others). `mt-14` = 56px space (room for the "MOST POPULAR" badge). |

**Card 1 – Basic (lines 308–320)**

| Line | Explanation |
|------|-------------|
| 308 | `<article class="card flex flex-col">` – white card, children in a column. |
| 309 | Package name. |
| 310 | Short description, small text. |
| 311 | The price. The `<span>` makes only `$50` huge (`text-5xl font-bold text-slate-900`); `/ project` stays normal size. |
| 312 | Delivery time. `mt-1` = 4px above. |
| 313 | `<ul>` – feature list. `flex-1` = take the extra space → pushes the button to the bottom (same trick as line 179). `space-y-3` = 12px between items. `text-sm`. |
| 314–317 | Each feature: `flex gap-2` = tick and text side by side with 8px gap. The `✓` is in a `<span>` coloured blue. `aria-hidden="true"` = screen readers don't read "check mark" each time. |
| 318 | `</ul>`. |
| 319 | The button. `btn` = our basic button (no colour). `w-full` = full width. `border border-slate-300` = grey outline. `text-center`. `hover:border-brand-600` = blue outline on hover. |
| 320 | `</article>`. |

**Card 2 – Standard, the highlighted one (lines 322–336)**

| Line | Explanation |
|------|-------------|
| 322 | This card does **not** use `.card`; it has its own design. `relative` = the badge on line 323 will be positioned **relative to this card**. `rounded-3xl` very round corners. `bg-brand-900 text-white` = dark blue card with white text → it **stands out**. `p-8` = 32px inside space. `shadow-2xl` = huge shadow. `ring-2 ring-brand-500` = a 2px blue outline. `flex flex-col` = column. `md:-translate-y-4` = from tablets, move it **16px up** (lifted above the others). |
| 323 | The **MOST POPULAR** badge. `absolute` = take it out of the normal flow and place it exactly where we say, relative to the `relative` parent (line 322). `-top-3` = 12px **above** the card's top edge (sticks out). `left-1/2` = move its left edge to the **middle** of the card. `-translate-x-1/2` = then move it back by **half of its own width** → perfectly centred. (This is the classic centring trick.) `rounded-full bg-amber-400 px-3 py-1 text-xs font-bold text-slate-900` = a small yellow pill with dark bold text. |
| 324 | Name. `text-white` overrides our default heading colour (dark) from the `<style>` block. |
| 325–327 | Description, price, delivery – same as Basic. (No `text-slate-900` on the price, so it stays white.) |
| 328–334 | Features. The ticks are `text-amber-400` (yellow) to look good on dark blue. |
| 335 | Button: `bg-white text-brand-900` = white button with dark-blue text. `hover:bg-brand-50` = very light blue on hover. |
| 336 | `</article>`. |

**Card 3 – Premium (lines 338–351)** – same as Basic with different text.

| Line | Explanation |
|------|-------------|
| 352 | `</div>` – end of the pricing grid. |
| 354 | The **launch offer** box. `rounded-2xl p-6 text-center` = rounded, padded, centred. `bg-amber-50 ring-1 ring-amber-200` = very light yellow with a thin yellow outline – yellow means "special", and it looks different from the blue pricing cards. `mt-12` = 48px above. |
| 355 | The offer title (bold, dark). The 🎉 emoji is just text. |
| 356 | The conditions: **limited** (first 5 clients) and **urgent** (an end date) – what makes an offer work. |
| 357 | Close the box. |
| 359 | A heading for the add-ons. |
| 360 | `<ul>` – a grid of 4 small cards: 1 column on phones, 2 from `sm`, 4 from `lg`. |
| 361 | One add-on: `card flex items-center justify-between` = a card with the name on the **left** and the price on the **right**, vertically centred. The price `<span>` is semi-bold blue. |
| 362–364 | Three more add-ons. |
| 365 | `</ul>`. |
| 366 | `</div>` – end of the centring box. |
| 367 | `</section>`. |

> **Business idea behind this design:** Basic = low price to attract clients, **Standard = what you want to sell** (so it's highlighted), Premium = makes Standard look like good value. Most clients pick the middle one.

### 6.7 The FAQ section (lines 369–403)

```html
369 │ <section id="faq" class="bg-slate-50 dark:bg-slate-900 py-20" aria-labelledby="faq-title">
370 │   <div class="mx-auto max-w-3xl px-4">
371 │     <h2 id="faq-title" class="text-center text-3xl">Frequently asked questions</h2>
372 │     <div class="mt-10 space-y-4">
373 │       <details class="group card">
374 │         <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
375 │           What do you need from me to start?
376 │           <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
377 │         </summary>
378 │         <p class="mt-3">Your logo, text, images and 2–3 websites you like.</p>
379 │       </details>
380 │       <details class="group card">
381 │         <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
382 │           Do I get the source code?
383 │           <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
384 │         </summary>
385 │         <p class="mt-3">Yes. Every package includes a GitHub repository.</p>
386 │       </details>
387 │       <details class="group card">
388 │         <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
389 │           Where will my website be hosted?
390 │           <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
391 │         </summary>
392 │         <p class="mt-3">Free on Vercel. I can also connect your own domain.</p>
393 │       </details>
394 │       <details class="group card">
395 │         <summary class="flex cursor-pointer list-none items-center justify-between font-semibold text-slate-900 dark:text-white">
396 │           How do payments work?
397 │           <span class="text-2xl text-brand-600 dark:text-brand-500 transition group-open:rotate-45" aria-hidden="true">+</span>
398 │         </summary>
399 │         <p class="mt-3">Through Fiverr/Upwork, or 50% upfront and 50% on delivery for direct clients.</p>
400 │       </details>
401 │     </div>
402 │   </div>
403 │ </section>
```

The four questions use **the same code**. We explain the first one (lines 373–379).

| Line | Explanation |
|------|-------------|
| 369 | FAQ section with a light grey background. Named by its heading (`aria-labelledby="faq-title"`). |
| 370 | Centring box. `max-w-3xl` = narrower (768px) – easier to read questions. |
| 371 | The heading, with `id="faq-title"`. |
| 372 | A box for the questions. `space-y-4` = 16px between them. `mt-10` = 40px above. |
| 373 | `<details>` – an **HTML5 accordion**: content that opens and closes when clicked. **No JavaScript needed.** It also works with the keyboard. `group` = so the `+` (line 376) can react when it opens. `card` = white box. |
| 374 | `<summary>` – the **always visible** part (the question). Clicking it opens/closes the `<details>`. `flex items-center justify-between` = question on the left, `+` on the right, vertically centred. `cursor-pointer` = the mouse becomes a hand 👆 (shows it's clickable). `list-none` = remove the default ▶ triangle. `font-semibold text-slate-900` = bold, dark. |
| 375 | The question text. |
| 376 | The `+` sign. `text-2xl text-brand-600` = big and blue. `transition` = animate changes. `group-open:rotate-45` = when the `<details>` (the group) is **open**, rotate 45° → the `+` becomes an `×`. `aria-hidden="true"` = decoration only. |
| 377 | `</summary>`. |
| 378 | The **answer**. Hidden until the question is clicked. `mt-3` = 12px above. |
| 379 | `</details>`. |
| 380–400 | Questions 2–4, same pattern. |
| 401–403 | Close the question box, the centring box and the section. |

### 6.8 The testimonials section (lines 405–445)

```html
405 │   <section id="testimonials" class="bg-brand-900 py-20" aria-labelledby="testimonials-title">
406 │     <div class="mx-auto max-w-6xl px-4">
407 │       <h2 id="testimonials-title" class="text-center text-3xl text-white">What clients say</h2>
408 │
409 │       <div class="mt-10 grid gap-6 md:grid-cols-3">
410 │         <figure class="card">
411 │           <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
412 │           <blockquote class="mt-4">
413 │             <p>"Ekramul delivered our restaurant site two days early. Mobile view is perfect!"</p>
414 │           </blockquote>
415 │           <figcaption class="mt-6">
416 │             <cite class="font-semibold not-italic text-slate-900 dark:text-white">Karim Uddin</cite>
417 │             <span class="block text-sm text-slate-500 dark:text-slate-400">Owner, Spice Garden</span>
418 │           </figcaption>
419 │         </figure>
420 │
421 │         <figure class="card">
422 │           <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
423 │           <blockquote class="mt-4">
424 │             <p>"Clear communication and clean code. Our page speed score jumped to 98."</p>
425 │           </blockquote>
426 │           <figcaption class="mt-6">
427 │             <cite class="font-semibold not-italic text-slate-900 dark:text-white">Sarah Lee</cite>
428 │             <span class="block text-sm text-slate-500 dark:text-slate-400">Marketing Lead, BrightPath</span>
429 │           </figcaption>
430 │         </figure>
431 │
432 │         <figure class="card">
433 │           <p class="text-amber-400"><span class="sr-only">Rated 5 out of 5</span><span aria-hidden="true">★★★★★</span></p>
434 │           <blockquote class="mt-4">
435 │             <p>"Ekramul turned our AI mockup into a real website better than we imagined."</p>
436 │           </blockquote>
437 │           <figcaption class="mt-6">
438 │             <cite class="font-semibold not-italic text-slate-900 dark:text-white">Tanvir Hossain</cite>
439 │             <span class="block text-sm text-slate-500 dark:text-slate-400">Founder, ShopEasy</span>
440 │           </figcaption>
441 │         </figure>
442 │       </div>
443 │     </div>
444 │   </section>
445 │ </main>
```

The three reviews use the same code. We explain the first one (lines 410–419).

| Line | Explanation |
|------|-------------|
| 405 | Dark-blue section (`bg-brand-900`), named by its heading. |
| 406 | Centring box. |
| 407 | Heading. `text-white` because the background is dark. |
| 409 | Grid: 1 column on phones, 3 from tablets (`md:grid-cols-3`). |
| 410 | `<figure class="card">` – a figure can also hold a **quote** with its source, not just images. |
| 411 | The stars. The first `<span class="sr-only">` says "Rated 5 out of 5" to screen readers (invisible on screen). The second `<span aria-hidden="true">` shows ★★★★★ on screen but is **hidden from screen readers** – otherwise they would read "star star star star star". `text-amber-400` = yellow. |
| 412 | `<blockquote>` – the correct tag for a **quotation** from someone else. `mt-4` = 16px above. |
| 413 | The quote text in a paragraph. |
| 414 | `</blockquote>`. |
| 415 | `<figcaption>` – who said it. `mt-6` = 24px above. |
| 416 | `<cite>` – the **name** of the source. `font-semibold text-slate-900` = bold, dark. `not-italic` = `<cite>` is italic by default – we remove that. |
| 417 | The person's role. `block` = put it on its **own line** (a `<span>` normally stays on the same line). `text-sm text-slate-500` = small, grey. |
| 418, 419 | Close figcaption and figure. |
| 421–441 | Reviews 2 and 3. |
| 442–444 | Close the grid, the centring box and the section. |
| 445 | `</main>` – end of the main content (opened on line 95). |

> This section was first generated by **AI** and then fixed: AI used `<div>`s everywhere, fixed widths that broke on phones, random colours and fake photos. Always review AI code!

### 6.9 The footer (lines 447–457)

```html
447 │   <footer class="bg-slate-900 text-slate-400">
448 │     <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-2 px-4 py-8 sm:flex-row">
449 │       <address class="not-italic">
450 │         Email: <a href="mailto:hello@example.com" class="text-white hover:underline">hello@example.com</a>
451 │       </address>
452 │       <p class="text-sm">&copy; 2026 Ekramul Islam</p>
453 │     </div>
454 │   </footer>
455 │
456 │ </body>
457 │ </html>
```

| Line | Explanation |
|------|-------------|
| 447 | `<footer>` – the bottom area of the page. `bg-slate-900` = very dark background. `text-slate-400` = light grey text. |
| 448 | Centring box. `flex flex-col` = stacked on phones. `sm:flex-row` = side by side from 640px. `items-center` = centred. `justify-between` = pushed to the two ends (on bigger screens). `gap-2` = 8px. `py-8` = 32px top/bottom. |
| 449 | `<address>` – contact information of the **owner** of the page. `not-italic` = it's italic by default; we remove that. |
| 450 | `mailto:` link – clicking it **opens the visitor's email app** with your address filled in. `text-white hover:underline`. (A `tel:` link would open the phone dialer.) |
| 451 | `</address>`. |
| 452 | Copyright line. `&copy;` = the © symbol. `text-sm` = small. |
| 453 | Close the centring box. |
| 454 | `</footer>`. |
| 456 | `</body>` – end of everything visible (opened on line 64). |
| 457 | `</html>` – end of the page (opened on line 2). |

---
## Part 7 – `contact.html` (contact page)

**Lines 1–93** are almost the same as `index.html` (head + header). Only three things are different:

| Line | Different because… |
|------|--------------------|
| 6 | `<title>Contact – Ekramul Islam</title>` – every page needs its **own** title. |
| 7 | A different description for Google. |
| 71–74, 87–90 | Menu links are written `index.html#about` instead of `#about`. **Why?** `#about` alone means "on **this** page" – but the about section is on the **home** page. |

**Lines 199–209** (the footer) are exactly the same as in `index.html`.

### 7.1 Page layout + map (lines 95–102)

```html
 95 │ <main>
 96 │   <section id="contact" class="mx-auto grid max-w-6xl gap-12 px-4 py-20 lg:grid-cols-3">
 97 │     <div>
 98 │       <h1 class="text-4xl font-bold">Let's work together</h1>
 99 │       <p class="mt-4">Fill in the form and I will reply within 24 hours.</p>
100 │       <iframe title="Map of Dhaka" src="https://www.openstreetmap.org/export/embed.html?bbox=90.35%2C23.70%2C90.45%2C23.82&amp;layer=mapnik"
101 │               width="600" height="300" loading="lazy" class="mt-8 aspect-video w-full rounded-2xl"></iframe>
102 │     </div>
```

| Line | Explanation |
|------|-------------|
| 95 | `<main>` – main content. |
| 96 | The section. `grid` + `lg:grid-cols-3` = on laptops, **3 equal columns**: the info takes 1 column, the form will take 2 (see line 104). On phones: everything stacked. |
| 97 | `<div>` – the info column. |
| 98 | `<h1>` – this page's main title (one `<h1>` per **page**, so contact.html has its own). |
| 99 | A paragraph. |
| 100 | `<iframe>` – a **window that shows another website** inside our page (here: a map from OpenStreetMap). `title="Map of Dhaka"` is required so screen readers know what the window contains. `src` = the address of the map. |
| 101 | (continues line 100) `width/height` = size. `loading="lazy"` = only load when the visitor scrolls near it. `aspect-video w-full rounded-2xl` = 16:9 shape, full width, round corners. `mt-8` = 32px above. `></iframe>` closes it. |
| 102 | `</div>` – end of the info column. |

> For Google Maps instead: open the map → **Share** → **Embed a map** → copy the `src="…"` part.

### 7.2 The form start + hidden fields (lines 104–107)

```html
104 │ <form action="https://api.web3forms.com/submit" method="POST" class="card space-y-8 lg:col-span-2">
105 │   <input type="hidden" name="access_key" value="YOUR-WEB3FORMS-ACCESS-KEY">
106 │   <input type="hidden" name="subject" value="New project request from my portfolio">
107 │   <input type="hidden" name="redirect" value="https://your-site.vercel.app/thank-you.html">
```

| Line | Explanation |
|------|-------------|
| 104 | `<form>` – a **form**: a group of inputs that is sent together. `action="https://api.web3forms.com/submit"` = **where** to send the data when the visitor clicks Send. We send it to **Web3Forms**, a free service that **emails** the message to you. (Vercel only hosts files – it can't receive forms itself.) `method="POST"` = send the data hidden inside the request (not in the address bar – safer for personal data). `card` = white box. `space-y-8` = 32px between the parts of the form. `lg:col-span-2` = on laptops, the form **spans 2 of the 3 columns**. |
| 105 | `<input type="hidden">` – a **hidden** field: sent with the form, but the visitor **can't see** it. `name="access_key"` + `value="…"` = your personal key from web3forms.com. It tells Web3Forms **which email** to send to. Replace `YOUR-WEB3FORMS-ACCESS-KEY` with your real key. (It's safe in public code – it can only send to *your* inbox.) |
| 106 | Hidden field `subject` = the **subject line** of the email you receive. |
| 107 | Hidden field `redirect` = after sending, the visitor is taken to **our** thank-you page. Must be the **full** address of your live site. |

### 7.3 Fieldset 1 – "About you" (lines 109–132)

```html
109 │ <fieldset class="grid gap-5 sm:grid-cols-2">
110 │   <legend class="mb-4 text-lg font-semibold text-slate-900 dark:text-white">About you</legend>
111 │
112 │   <div>
113 │     <label for="name">Full name *</label>
114 │     <input type="text" id="name" name="name" required minlength="3" placeholder="e.g. Karim Uddin" class="form-input">
115 │   </div>
116 │
117 │   <div>
118 │     <label for="email">Email *</label>
119 │     <input type="email" id="email" name="email" required placeholder="you@company.com" class="form-input">
120 │   </div>
121 │
122 │   <div>
123 │     <label for="phone">Phone</label>
124 │     <input type="tel" id="phone" name="phone" pattern="01[3-9][0-9]{8}" placeholder="01XXXXXXXXX"
125 │            title="11-digit Bangladeshi number, e.g. 01712345678" class="form-input">
126 │   </div>
127 │
128 │   <div>
129 │     <label for="website">Current website</label>
130 │     <input type="url" id="website" name="website" placeholder="https://..." class="form-input">
131 │   </div>
132 │ </fieldset>
```

| Line | Explanation |
|------|-------------|
| 109 | `<fieldset>` – a **group** of related fields. `grid gap-5 sm:grid-cols-2` = from 640px, **two fields per row**, 20px gap. |
| 110 | `<legend>` – the **title** of the fieldset. `mb-4` = 16px below. `text-lg font-semibold text-slate-900`. |
| 112 | `<div>` – wraps one label + one input together → that pair becomes **one grid cell**. |
| 113 | `<label for="name">` – the **visible name** of the field. `for="name"` connects it to the input with `id="name"`. **Try it:** clicking the label puts the cursor in the box. The `*` tells the visitor it's required. |
| 114 | `<input>` – a text box (no closing tag). `type="text"` = normal text. `id="name"` = matches the label's `for`. `name="name"` = the **key** the data is sent with (the email will say `name: Karim`). **Without `name`, the value is not sent at all!** `required` = the form **can't be sent** if this is empty. `minlength="3"` = at least 3 characters. `placeholder` = grey hint text inside the box (disappears when typing – it's **not** a replacement for a label). `class="form-input"` = our input style. |
| 115 | `</div>`. |
| 117–120 | The email field. `type="email"` = the browser **checks** that it looks like an email (has `@` and a domain). On phones it shows a keyboard with `@`. |
| 122, 123 | Cell + label for phone (no `*` → optional). |
| 124 | `type="tel"` = phones show the **number keypad**. `pattern="01[3-9][0-9]{8}"` = a **rule** the value must match (a "regular expression"): `01` = starts with 0 and 1, `[3-9]` = then one digit from 3 to 9, `[0-9]{8}` = then exactly 8 more digits. Total = 11 digits, like `01712345678`. |
| 125 | (continues line 124) `title` = the message shown in the error bubble if the pattern doesn't match. |
| 126 | `</div>`. |
| 128, 129 | Cell + label for the client's current website (optional). |
| 130 | `type="url"` = must be a full web address starting with `http://` or `https://`. Phones show a keyboard with `/` and `.com`. |
| 131 | `</div>`. |
| 132 | `</fieldset>`. |

### 7.4 Fieldset 2 – "Your project" (lines 134–190)

```html
134 │ <fieldset class="grid gap-5 sm:grid-cols-2">
135 │   <legend class="mb-4 text-lg font-semibold text-slate-900 dark:text-white">Your project</legend>
136 │
137 │   <div>
138 │     <label for="service">Service *</label>
139 │     <select id="service" name="service" required class="form-input">
140 │       <option value="">-- Choose a service --</option>
141 │       <option value="landing">Landing page</option>
142 │       <option value="business">Business website</option>
143 │       <option value="convert">Design to code</option>
144 │     </select>
145 │   </div>
146 │
147 │   <div>
148 │     <label for="deadline">Deadline</label>
149 │     <input type="date" id="deadline" name="deadline" class="form-input">
150 │   </div>
151 │
152 │   <div>
153 │     <label for="industry">Industry</label>
154 │     <input type="text" id="industry" name="industry" list="industries" placeholder="Start typing..." class="form-input">
155 │     <datalist id="industries">
156 │       <option value="Restaurant"></option>
157 │       <option value="Education"></option>
158 │       <option value="E-commerce"></option>
159 │       <option value="Real estate"></option>
160 │     </datalist>
161 │   </div>
162 │
163 │   <div>
164 │     <label for="budget">Budget (USD)</label>
165 │     <input type="number" id="budget" name="budget" min="50" max="5000" step="10" placeholder="e.g. 120" class="form-input">
166 │   </div>
167 │
168 │   <div class="sm:col-span-2">
169 │     <label for="urgency">How urgent is it?</label>
170 │     <input type="range" id="urgency" name="urgency" min="1" max="5" value="3" class="mt-2 w-full accent-brand-600">
171 │     <div class="flex justify-between text-xs text-slate-500 dark:text-slate-400">
172 │       <span>Flexible</span>
173 │       <span>Very urgent</span>
174 │     </div>
175 │   </div>
176 │
177 │   <div class="sm:col-span-2">
178 │     <p>Package *</p>
179 │     <div class="mt-2 flex flex-wrap gap-6">
180 │       <label class="flex items-center gap-2"><input type="radio" name="package" value="basic" required class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Basic</label>
181 │       <label class="flex items-center gap-2"><input type="radio" name="package" value="standard" class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Standard</label>
182 │       <label class="flex items-center gap-2"><input type="radio" name="package" value="premium" class="text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> Premium</label>
183 │     </div>
184 │   </div>
185 │
186 │   <div class="sm:col-span-2">
187 │     <label for="message">Project details *</label>
188 │     <textarea id="message" name="message" rows="5" required minlength="20" class="form-input"></textarea>
189 │   </div>
190 │ </fieldset>
```

| Line | Explanation |
|------|-------------|
| 134, 135 | Second fieldset with its title. |
| 137, 138 | Cell + label for "Service". |
| 139 | `<select>` – a **dropdown** menu. `required` = must choose something. |
| 140 | `<option value="">` – the first option has an **empty value**. Together with `required`, the visitor **must** pick a real option – they can't send "-- Choose a service --". |
| 141–143 | The real choices. `value="landing"` = what is **sent**; `Landing page` = what the visitor **sees**. |
| 144 | `</select>`. |
| 147–150 | Deadline. `type="date"` = the browser shows a **calendar picker** for free. |
| 152, 153 | Cell + label for "Industry". |
| 154 | A text box with `list="industries"` – it's connected to the `<datalist>` with `id="industries"` (line 155). |
| 155–160 | `<datalist>` – a list of **suggestions** that pop up while typing. The visitor can pick one **or type something else**. (A `<select>` only allows its own options.) Each `<option value="…">` is one suggestion. |
| 163, 164 | Cell + label for "Budget". |
| 165 | `type="number"` = only numbers; phones show the number keypad and desktops show ▲▼ arrows. `min="50"` = smallest allowed, `max="5000"` = biggest allowed, `step="10"` = the allowed "jumps" (50, 60, 70…). The browser blocks other values when sending. |
| 168, 169 | A full-row cell (`sm:col-span-2`) + label for "How urgent is it?". |
| 170 | `type="range"` = a **slider**. `min="1" max="5"` = values 1 to 5, `value="3"` = starts in the middle. `mt-2 w-full` = full width with space above. `accent-brand-600` = the slider uses our brand colour (CSS3 `accent-color`). |
| 171–174 | Two labels under the slider: `flex justify-between` puts "Flexible" on the **left** and "Very urgent" on the **right**. `text-xs` = very small. |
| 175 | `</div>`. |
| 177 | Full-row cell for the package choice. |
| 178 | A `<p>` used as a title for the radio buttons. |
| 179 | A box that puts the radio buttons **in a row** (`flex flex-wrap gap-6`), 8px below the title (`mt-2`). |
| 180 | A **radio button**. Here the `<input>` is **inside** the `<label>` – that also connects them (no `for`/`id` needed). `flex items-center gap-2` = circle and text side by side. `type="radio"` = round button. `name="package"` – all three radios have the **same name**, so only **one** can be selected. `value="basic"` = what is sent if chosen. `required` = one of the group must be chosen (writing it on one radio is enough). `text-brand-600` = the selected dot is blue. |
| 181, 182 | The other two radios – same `name`, different `value`. |
| 183, 184 | Close the row and the cell. |
| 186–189 | The message box. `<textarea>` = **multi-line** text (it has a closing tag, unlike `<input>`). `rows="5"` = 5 lines tall. `required minlength="20"` = at least 20 characters. |
| 190 | `</fieldset>`. |

### 7.5 Consent + Send button (lines 192–197)

```html
192 │       <label class="flex items-center gap-2"><input type="checkbox" name="consent" required class="rounded text-brand-600 dark:border-slate-600 dark:bg-slate-800 dark:text-brand-500"> I agree to be contacted *</label>
193 │
194 │       <button type="submit" class="btn-primary">Send request</button>
195 │     </form>
196 │   </section>
197 │ </main>
```

| Line | Explanation |
|------|-------------|
| 192 | A **checkbox** inside its label. `required` = it **must be ticked** before sending. `rounded` = slightly rounded square. `text-brand-600` = blue tick. |
| 194 | `<button type="submit">` – the **Send** button. Clicking it makes the browser **check every rule** (`required`, `minlength`, `pattern`, `type="email"`…). If anything is wrong, it shows an error bubble and **doesn't send**. If everything is fine, it sends the data to the `action` address. All this works **without JavaScript**. `btn-primary` = our blue button. |
| 195 | `</form>`. |
| 196 | `</section>`. |
| 197 | `</main>`. |

---

## Part 8 – `thank-you.html` and `404.html`

Both pages have a **short head** (no Google Fonts, no description) with the same Tailwind lines and `<style>` block
as the other pages. Below we show only the **visible** part.

### 8.1 `thank-you.html` – shown after the form is sent

```html
61 │ <body>
62 │   <main class="grid min-h-screen place-items-center px-4 text-center">
63 │     <div>
64 │       <p class="text-7xl" aria-hidden="true">✅</p>
65 │       <h1 class="mt-4 text-3xl">Thank you!</h1>
66 │       <p class="mt-2">Your message was sent. I will reply within 24 hours.</p>
67 │       <a href="index.html" class="btn-primary mt-8">Back to home</a>
68 │     </div>
69 │   </main>
70 │ </body>
71 │ </html>
```

| Line | Explanation |
|------|-------------|
| 1–60 | The head: charset, viewport, title, share tags, favicon, the Tailwind CDN + settings (lines 11–12) and our `<style>` block. No Google Fonts here – the page uses the fallback font. |
| 61 | `<body>`. This page has **no header and no footer** – it's a simple message page. |
| 62 | `<main>` with the **perfect-centring trick**: `grid` + `place-items-center` = centre the content horizontally **and** vertically. `min-h-screen` = at least as tall as the screen. `px-4` = side space on phones. `text-center` = centred text. |
| 63 | A `<div>` that holds everything (so it's centred as **one** block). |
| 64 | A big ✅ emoji (`text-7xl`). `aria-hidden="true"` = decoration, screen readers skip it. |
| 65 | The page title. |
| 66 | The message. |
| 67 | A button back to the home page – **never leave the visitor at a dead end**. |
| 68–71 | Close div, main, body, html. |

### 8.2 `404.html` – shown when a page doesn't exist

```html
58 │ <body>
59 │   <main class="grid min-h-screen place-items-center px-4 text-center">
60 │     <div>
61 │       <p class="text-7xl font-bold text-brand-600 dark:text-brand-500">404</p>
62 │       <h1 class="mt-4 text-3xl">Page not found</h1>
63 │       <p class="mt-2">Sorry, this page doesn't exist.</p>
64 │       <a href="index.html" class="btn-primary mt-8">Back to home</a>
65 │     </div>
66 │   </main>
67 │ </body>
68 │ </html>
```

| Line | Explanation |
|------|-------------|
| 1–57 | The head (Tailwind CDN + settings on lines 8–9, then the `<style>` block). |
| 59 | Same perfect-centring `main` as the thank-you page. |
| 61 | A huge blue **404** (`text-7xl font-bold text-brand-600`). 404 is the official code for "page not found". |
| 62–64 | Title, message, and a button back home. |
| 65–68 | Close div, main, body, html. |

> **Vercel automatically shows `404.html`** when someone visits an address that doesn't exist. Try it on your live site: `your-site.vercel.app/abc`.

---

## Part 9 – Practice questions

Answer these without looking. Then find the line in this lesson to check yourself.

**HTML**
1. What is the difference between a **tag**, an **element** and an **attribute**?
2. Why does every page need `<meta name="viewport">`?
3. Why should a page have only **one** `<h1>`?
4. What does `href="#about"` do? Why does `contact.html` use `index.html#about` instead?
5. Why does every `<img>` need `alt`, `width` and `height`?
6. What is the difference between `<section>` and `<article>`?
7. What happens if an `<input>` has no `name` attribute?
8. How do `<label for="email">` and `<input id="email">` work together?
9. Explain `pattern="01[3-9][0-9]{8}"` in your own words.
10. Why do the three radio buttons have the same `name`?
11. How does the FAQ open and close **without JavaScript**?
12. How does the mobile menu open and close **without JavaScript**?

**Tailwind / CSS**
13. What do `px-4`, `py-20` and `mt-8` mean? How many pixels is `p-6`?
14. Read this aloud: `grid gap-6 sm:grid-cols-2 lg:grid-cols-3`.
15. What does `hidden md:flex` do? And `md:hidden`?
16. What is the job of `group` and `group-hover:scale-110`?
17. Why do we use `flex-1` on the description in the project cards?
18. How is the "MOST POPULAR" badge centred? (Two classes.)
19. What does `sr-only` do and why do we need it?
20. What does `type="text/tailwindcss"` on the `<style>` tag do?

**Setup / deploy**
21. What does the Tailwind CDN `<script>` do? What happens if you open the page without internet?
22. Why must `tailwind-config.js` be loaded **after** the CDN script?
23. Why does `vercel.json` say `"outputDirectory": "public"`?
24. Why do we need Web3Forms when the site is on Vercel?
25. What do the three hidden inputs in the form do?

**New in this version**
26. What are `<caption>`, `<thead>`, `<th scope="col">` and `<td>` for? Why is the table inside a `div` with `overflow-x-auto`?
27. What is the difference between a `<datalist>` and a `<select>`?
28. What do `min`, `max` and `step` do on `type="number"`?
29. Explain `srcset="avatar-400.png 400w, avatar-800.png 800w"` and `sizes="400px"`. Which file does a "Retina" phone download?
30. How does the **Case study** modal open and close without JavaScript? Why does each project need its own `id`?
31. What do `<dl>`, `<dt>` and `<dd>` mean?
32. What does `dark:bg-slate-900` do? When is it used?
33. Why is the "How I work" list an `<ol>` and not a `<ul>`?

---

**You made it to the end!** 🎉 If you can answer all 33 questions, you understand every line of your Semester 01 project.
