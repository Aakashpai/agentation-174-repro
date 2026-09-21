# agentation #174 repro attempt

Minimal Astro 5 project on Vite 6 with `<Agentation client:only="react" />`, built to check
https://github.com/benjitaylor/agentation/issues/174 (settings panel sometimes unstyled on a hard refresh).

```
npm install
npm ls vite --all        # 6.4.3 only
npm run dev              # http://localhost:4321
npm run build && npm run preview
```

Pages: `/` (toolbar via a wrapper component), `/direct` (imported straight in the .astro page),
`/heavy` (a 600ms synchronous script before the island, to try and provoke a race).

To check a load, in the console:

```js
const el = document.querySelector('agentation-toolbar').shadowRoot.querySelector('[class*=toolbarContainer]');
getComputedStyle(el).backgroundColor // rgb(26, 26, 26) when styled
```

On agentation 3.1.0 I could not get an unstyled render: 40 cold loads across dev and preview all styled,
including per-frame sampling from before hydration. Versions used: astro 5.18.2, vite 6.4.3,
@astrojs/react 4.4.2 (pinned, newer versions pull in Vite 8), react 19.3.0, agentation 3.1.0.
