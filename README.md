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

_**Deploy on cPanel**_

You will have to upload your files on your domain folder. You have 3 possibilities :
-FTP
-Git
-File explorer and zip
⚠️ In any case, always double check you don't forget to add the .next folder !

Add your files in the folder linked to your domain or sub-domain.
In my case, my folder will be /tutorial. 


WORK IN PROGRESS


