# vite2.0集成pwa

> 使用vite插件 vite-plugin-pwa https://github.com/antfu/vite-plugin-pwa
>
>
> yarn add vite-plugin-pwa -D
>

## vite.config.ts配置

~~~typescript
export default defineConfig({
  plugins: [
    VitePWA({
      includeAssets: ["favicon.ico", "/images/favicon_192.png","robots.txt"],
      registerType: "autoUpdate",
      mode: 'development',
      srcDir: 'src',
      filename: 'sw.ts',
      base: '/',
      strategies: 'injectManifest',
      workbox: { cleanupOutdatedCaches: true, sourcemap: true },
      manifest: {
        name: "your application name",
        short_name: "short name",
        description: "Description of your app",
        theme_color: "#ffffff",
        //以下为最小配置
        icons: [
          {
            src: "/images/favicon_192.png",
            sizes: "192x192",
            type: "image/png",
          },
          {
            src: "/images/favicon_512.png",
            sizes: "512x512",
            type: "image/png",
          },
          {
            src: "/images/favicon_512.png",
            sizes: "512x512",
            type: "image/png",
            purpose: "any maskable",
          },
        ],
      },
    }),
  ],
});
~~~

## mani.ts文件注册service worker

~~~typescript
import { registerSW } from "virtual:pwa-register";
const updateSW = registerSW();
~~~

## sw.ts文件（service worker具体执行代码）

```typescript
import { precacheAndRoute } from "workbox-precaching";

declare let self: ServiceWorkerGlobalScope;
self.addEventListener("message", (event) => {
  if (event.data && event.data.type === "SKIP_WAITING") self.skipWaiting();
});

//serviceWorker注册成功时触发，主要用于结存资源
//sw.js发生改变，install就会触发
self.addEventListener("install", (event) => {
  console.log("install::", event);
  //self.skipWaiting() 会让serviceWorker跳过等待，直接进入activate状态
  //event.waituntil() 传入一个Promise对像，等Promise执行结束再进入下一个状态，防止浏览器在异步操作时就结束当前生命周期
  event.waitUntil(self.skipWaiting());
});

//serviceWorker激活时触发，主要用于删除旧资源
//在install事件后触发，如果serviceWorker已经存在，就处于等待状态，直到当前serviceWroker终止
self.addEventListener("activate", (event) => {
  console.log("activate11::", event);
});
//发送请求时触发主要用于操作缓存或读取网络资源
self.addEventListener("fetch", (event) => {
  // console.log("fetch::", event);

  //service worker激活后会在下一次刷新页面时生效，以下语句让service worker激活后立即获取控制权
  event.waitUntil(self.clients.claim());
});

// self.__WB_MANIFEST is default injection point
precacheAndRoute(self.__WB_MANIFEST);
```

