_**Build the Next.js app**_

Create your Next.js app in your terminal

```
npx create-next-app tuto
```


In your project directory, make a **server.js** file and add :

```javascript
const { createServer } = require('http')
const { parse } = require('url')        
const next = require('next')            
     
const dev = process.env.NODE_ENV !== 'production'
const hostname = 'localhost'            
const port = process.env.PORT || 3000;  
const app = next({ dev, hostname, port })
const handle = app.getRequestHandler()  

app.prepare().then(() => {              
  createServer(async (req, res) => {
    try {
      const parsedUrl = parse(req.url, true)   
      const { pathname, query } = parsedUrl    

      if (pathname === '/a') {
        await app.render(req, res, '/a', query)  
      } else if (pathname === '/b') {
        await app.render(req, res, '/b', query)  
      } else {
        await handle(req, res, parsedUrl)        
      }
    } catch (err) {
      console.error('Error occurred handling', req.url, err)
      res.statusCode = 500
      res.end('internal server error')
    }
  }).listen(port, (err) => {
    if (err) throw err
    console.log(`> Ready on http://${hostname}:${port}`)
  })
})
```

In your **package.json** file, add these lines:

```json
        "dev": "node server.js",        
        "build": "next build",          
        "start": "NODE_ENV=production node server.js"
```

Now, you can simply run in your terminal :

```
npm run build
```
⚠️ REMOVE the node_modules folder. Instead, we will use the Node.JS app manager on cpanel.

_**Deploy on cPanel**_

You will have to upload your files on your domain folder. You have 3 possibilities :
####
* FTP
* Git
* File explorer and zip

⚠️ In any case, always double check you don't forget to add the **.next** folder ! Otherwise, the build will be useless.

Add your files in the folder linked to your domain or sub-domain.
In my case, my folder will be /tutorial. 

![4](https://user-images.githubusercontent.com/86530475/213726025-5f829445-423a-4f30-8103-4cd0d13bc6ac.png)

In cPanel, go to "Setup Node.js app" and click on "CREATE APPLICATION"

For now, we use app.js as *Application startup file* to make sure node is running.

![6](https://user-images.githubusercontent.com/86530475/213729485-670ee2e5-e01d-410a-ad35-f316ddd63a2d.png)

Click on *CREATE*

Now you can verify if everything went well before you continue.
![7](https://user-images.githubusercontent.com/86530475/213730013-f6ddb0fd-c6b4-4707-9f1b-a705ff57493f.png)

![8](https://user-images.githubusercontent.com/86530475/213730272-1ea77a51-c7c6-45f0-ae5c-954f63a1cd31.png)

Stop your app and click on *Run NPM Install*. This is why we removed our node_modules folder before.

![9](https://user-images.githubusercontent.com/86530475/213730663-d81fc2d9-4c8f-4120-9ef4-81e0c31ce4d7.png)

Change the *Application startup file* **to server.js**

![10](https://user-images.githubusercontent.com/86530475/213732646-2ed2e1d2-fc04-4eff-891e-3717e095746d.png)

⚠️ Do not forget to save and restart.


![final](https://user-images.githubusercontent.com/86530475/213731542-b583c9f0-26d0-4047-bcbc-323d0aa693a8.png)

Congratulations ! Your Next.js app is now hosted 👽




