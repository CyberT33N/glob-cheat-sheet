# Glob Cheat Sheet
Glob Cheat Sheet with the most needed stuff..


<br><br><br><br>



## Node.js
- https://www.npmjs.com/package/glob
```javascript
/**
 * Get all routers
 * @param {string} expression - Glob expression
 * @returns {array} - All absolute file paths
 */
const getRouters = expression => {
    return new Promise((resolve, reject) => {
        glob(expression, (e, routerPaths) => {
            if (e) {
                reject(new Error(e))
            }

            const routers = []

            for (const path of routerPaths) {
                const finalPath = `${process.env.PWD}/${path}`
                const router = require(finalPath)
                routers.push(router)
            }

            resolve(routers)
        })
    })
}

(async() => {
    const routers = await getRouters('src/**/routes.js')

    // load all routes
    for (const router of routers){
        app.use(router)
    }

    await app.listen(port)
})()


```

<br><br>

#### Exclude node_modules folder
```javascript
const routesPaths = await getRouters('{,!(node_modules)/**/}*.routes.js')
```

