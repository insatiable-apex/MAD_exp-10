# MAD_exp-10

image generation :- https://tools.crawlink.com/tools/pwa-icon-generator/and



sw.js 

-> 

var CACHE_NAME = 'my-site-cache-v1';
var urlsToCache = [
'/',
'index.html',
/* '/styles/main.css',
'/script/main.js' */
];
self.addEventListener('install', function (event) {
    // Perform install steps
    event.waitUntil(
        caches.open(CACHE_NAME)
            .then(function (cache) {
                console.log('Opened cache');
                return cache.addAll(urlsToCache);
            })
    )
});

self.addEventListener('fetch', function(event) {
    event.respondWith(
      caches.match(event.request)
        .then(function(response) {
          // Cache hit - return response
          if (response) {
            return response;
          }
          return fetch(event.request);
        }
      )
    );
});

self.addEventListener('push', function(event) {
    var data = event.data.json();
    event.waitUntil(
      self.registration.showNotification(data.title, {
        body: data.body,
        icon: data.icon
      })
    );
});

self.addEventListener('sync', function(event) {
    if (event.tag === 'my-sync') {
      event.waitUntil(
        // code to sync data with the server
      );
    }
});
