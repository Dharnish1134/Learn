# TODO using MERN Stack

## Packages to be installed
- node and npm (https://www.geeksforgeeks.org/how-to-download-and-install-node-js-and-npm/) 

## Parts of the application 
- Client (frontend)
- Server (backend)

### Steps in setting up Client:
```
npm create vite@latest 
```
- Enter Project name
- Enter the framework (Eg:React)
- Enter the language choice (Eg: TypeScript)

#### To setup tailwindCSS
- install tailwind
```
npm install tailwindcss @tailwindcss/vite
```
- Set it up in the vite.config.ts
```
import tailwindcss from '@tailwindcss/vite'

plugins:[
    tailwindcss()
]
```
- add the import in the css file
```
@import "tailwindcss";
```

**Note: If Not Working refer https://tailwindcss.com/docs/installation/using-vite**

### Steps in setting up Server
```
 mkdir server && cd server
```
```
 npm init -y
```
```
npm install express cors dotenv mongoose 
```
```
npm install --save-dev typescript ts-node @types/node @types/express @types/cors @types/mongoose nodemon @typegoose/typegoose
```
```
npx tsc --init
```

- Create a src folder and a server.ts file and In the tsconfig file Enable the rootDir as './src' and enable experimentalDecorators and emitDecoratorMetadata
- create a script to start the server which uses nodemon to watch and run the files 
```
// in package.json 
"scripts": {
    "start": "npx ts-node src/server.ts",
    "dev": "nodemon src/server.ts"
  },

```

- to create a simple express server
``` 
//server.ts
import express, { Application, Request, Response } from 'express';
import cors from 'cors';
import dotenv from 'dotenv';
import mongoose from 'mongoose';

dotenv.config();

const app: Application = express();
const PORT = process.env.PORT || 3000;
const mongouri = process.env.MONGO_URI;
if (!mongouri) {
  console.error("Mongo URI is not defined");
  process.exit(1);
}

//connect mongodb
mongoose.connect(mongouri).then(() => {
    console.log("Connected to MongoDB");
  })
  .catch((err) => {
    console.error("Here:",err);
  });


// Middleware
app.use(express.json()); // Parse JSON requests
app.use(cors()); // Enable CORS

// Simple API Route
app.get('/', (req: Request, res: Response) => {
    res.send('Hello, MERN Stack creat TypeScript!');
});


// Start Server
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}/try`);
});

```

**Note: To setup Monogodb connection**
- Create a cluster in monogo atlas.
- Create a connection in that cluster.
- Get the Mongo URI from the connection.
- Create a .env file and paste the Mongo URI in the file 
```
//.env
MONGO_URI = (mongo URI)
```

