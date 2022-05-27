# Basic Express Project Setup
1. Start a new Node project by issuing...
```bash
npm init
```
...with these parameters: (NOTE: )
```json
{
  "name": "<projectName>",
  "version": "1.0.0",
  "description": "<description>",
  "main": "index.js",
  "scripts": {
    "start": "nodemon ./index.js --exec babel-node -e js"
  },
  "author": "<author>",
  "license": "ISC"
}
```
> [!INFO] By default, the single entry under "scripts" is called "test". Change this to "start" after this step is completed.

2. Install necessary packages:
```bash
> npm i bcrypt body-parser express jsonwebtoken mongoose nodemon
```

3. Install necessary dev packages:
```bash
npm i babel-cli babel-preset-env babel-preset-stage-0 --save-dev
```

4. Create .babelrc file at same level as index.js with these contents:
```json
{
    "presets": [
        "env",
        "stage-0"
    ]
}
```

5. Create folder structure:
```bash
mkdir src && cd src && mkdir models & mkdir controllers & mkdir routes && cd ..
```

6. Create index.js at same level as package.json:
```bash
echo newfile > index.js
```

7. Populate index.js:
```js
import express from 'express';
import bodyParser from 'body-parser';
import routes from "./src/routes/routes";

const app = express();
const PORT = 3000;

// bodyParser setup
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// Apply routing to express app
routes(app);

// Serve static files stored in /public
app.use(express.static('public'));

// 
app.get('/', (req, res) => {
    res.json({ message: `Server is running on port ${PORT}.` });
});

// Listen for connections on PORT
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}.`);
});
```

8. Populate src/controllers/controllers.js: 
```js
export const getTest = (req, res) => {
    res.status(200).json({ message: `GET test successful` });
};

export const postTest = (req, res) => {
    res.status(200).json({ message: `POST test successful` });
};

export const putTest = (req, res) => {
    res.status(200).json({ message: `PUT test successful` });
};

export const deleteTest = (req, res) => {
    res.status(200).json({ message: `DELETE test successful` });
};
```

9. Populate src/routes/routes.js:
```js
import { deleteTest, getTest, postTest, putTest } from "../controllers/controllers"

const routes = (app) => {
    app.route("/testRoute")

        .get(getTest)
        .post(postTest)
        .put(putTest)
        .delete(deleteTest);
};

export default routes;
```

10. Verify that folder structure matches:
![[Pasted image 20220527161101.png]]

11. Start app:
```bash
npm start
```

12. Use browser to test GET endpoint. Use Postman to test POST, PUT, and DELETE.

# MongoDB Setup
# JWT Setup