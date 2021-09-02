# Glob Cheat Sheet
Glob Cheat Sheet with the most needed stuff..


<br><br><br><br>



## Node.js
- https://www.npmjs.com/package/glob
```javascript
/**
 * Get all file paths for specific glob expression
 * @param expression {string} - Glob expression
 * @returns {array} - All absolute file paths
 * @private
 */
_getFilePaths(expression) {
    return new Promise((resolve, reject) => {
        glob(expression, (e, filePaths) => {
            if(e){
                reject(e)
            }

            const finalFilePaths = []

            for (const filePath of filePaths) {
                const finalFilePath = path.join('../../../', filePath)
                finalFilePaths.push(finalFilePath)
            }

            resolve(finalFilePaths)
        })
    })
}

const routesPaths = await this._getFilePaths('**/*.routes.js')
```

<br><br>

#### Exclude node_modules folder
```javascript
const routesPaths = await this._getFilePaths('{,!(node_modules)/**/}*.routes.js')
```

