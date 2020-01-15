# Como criar um PWA com CRA (create-react-app)

Seguindo esse tutorial, você será capaz de criar um **Progressive Web App** do zero.

## 1. No arquivo `src/index.js` altere a seguinte linha de código:

`serviceWorker.unregister();`

para

`serviceWorker.register();`

## 2. No arquivo `src/serviceWorker.js` faça as seguintes alterações:

Remova a checakgem do NODE_ENV como mostra a o exemplo a seguir:

`if (process.env.NODE_ENV === 'production' && 'serviceWorker' in navigator) {`

para:

`if ('serviceWorker' in navigator) {`

Altere o nome do service worker para `sw.js`:

`const swUrl = ${process.env.PUBLIC_URL}/service-worker.js;`

para 

`const swUrl = ${process.env.PUBLIC_URL}/sw.js;`

## 3. Crie o seu service worker (sw.js) na pasta `public` com o seguinte conteúdo:

```
// install
self.addEventListener('install', evt => {
  evt.skipWaiting();
});

// activate
self.addEventListener('activate', evt => {
  evt.skipWaiting();
});

// fetch
self.addEventListener('fetch', evt => {
  evt.respondWith(
    fetch(evt.request)
      .then(fetchResponse => {
        return fetchResponse;
      })
      .catch(() => {
        caches.match(evt.request)
          .then(cacheResponse => {
            return cacheResponse;
          })
      })
  );
});
```

## 4. Verifique as informações contidas no arquivo `manifest.json`, como abaixo:

O [**Manifest**](https://developers.google.com/web/fundamentals/web-app-manifest) é um arquivo no formato JSON que funciona como uma "etiqueta" para o navegador com informações sobre sua aplicação. <br>

```
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    },
    {
      "src": "logo192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "logo512.png",
      "type": "image/png",
      "sizes": "512x512"
    }
  ],
  "start_url": ".",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```

## 5. Verifique se existe a referência para o arquivo manifest.json no seu index.html:

`<link rel="manifest" href="%PUBLIC_URL%/manifest.json" />`

#### Outras tags para o index.html

Para otimizar seu PWA, você pode também adicionar as seguintes tags:<br>

`<meta name="theme-color" content="#000000" />` <br>

Para iOS:

```
<link rel="apple-touch-icon" href="/icons/icons-96x96.png">
<meta name="apple-mobile-web-app-status-bar" content="#aa7700">
```
