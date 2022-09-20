# Vue3-TypeScript Template

## 1. Environment

* Vue3 (vite)
* TypeScript
* Docker

## 2. Build

### NPM
**Project Setup**
> npm install

**Compile and Hot-Reload for Development**
> npm run dev

**Type-Check, Compile and Minify for Production**

> npm run build

Visit via http://localhost:5173

### Docker

**Build image**
> docker run -t ***imageName:version*** .

**Tag image**
>docker tag ***imageName:version*** ***imageName:new_version***

**Run image as a container**
>docker run -d -p ***5173:5173*** --name ***containerName*** ***imageName:version***
    >>The port is 5173, which is set in ./vite.config.ts

Visit via http://localhost:5173

**List containers**
>docker ps

**Stop containers**
>docker stop ***containerName***

### Docker Compose

**Build image and run it as a container**
>docker-compose up -d

**Rebuild the image**
>docker-compose up --build -d

## 3. DevLog

**Port problem**
Vue3(Vite) - TypeScript project running within docker container but http://localhost:8080 is out of connect.
**Solution**
configure host within ./vite.config.ts

    import { fileURLToPath, URL } from 'node:url'
    import { defineConfig } from 'vite'
    import vue from '@vitejs/plugin-vue'

    // https://vitejs.dev/config/
    export default defineConfig({
    plugins: [vue()],
    resolve: {
        alias: {
        '@': fileURLToPath(new URL('./src', import.meta.url))
        }
    },
    // localhost:port
    server: {
        host: true,
        port:5173
    }
    })




## 4. Demo 

**Map View**

![map_add_marker](https://user-images.githubusercontent.com/49648985/191279171-60005c1a-2771-4c59-b68c-3d1591150b23.PNG)



