<div style="text-align: center;">
  <h1>React JS</h1>
</div>


### Create a New Project

- ```npm create vite@latest my-vite-app```
- ```cd my-vite-app```
- ```npm install```
- ```npm run dev```


### Install Bootstrap

- ```npm install react-bootstrap bootstrap```

   Import Bootstrap CSS:

   ``` JS
   import 'bootstrap/dist/css/bootstrap.min.css'; 
   ```


### Install React Router

```npm install react-router-dom```



> create a new file to use Rounting **AppLayout.jsx**

```JS
// src/AppLayout.jsx

import { Outlet } from "react-router-dom";
import Footer from "../Footer/Footer";
import Header from "../Header/Header";

const AppLayout = () => {
    return <>
        <Header />
        <Outlet/>
        <Footer/>
    </>
}

export default AppLayout;
```


``` JS
// src/App.jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

const router = createBrowserRouter([

  {path: "/",element: <Home />,},
  {path: "about",element: <About />,},
  {path: "contact",element: <Contact />,},
  {path: "item/:id",element: <ItemDetail />,},  // Route with a parameter `id`
  {path: "dashboard",element: <Dashboard />,
    children: [
        {path: "overview",element: <Overview />,},
      {path: "settings",element: <Settings />,},
    ],
  },
  {path: "*",element: <NotFound />,},

]);



function App() {
    return <RouterProvider router={route1r} />
}

export default App
```


##### Access URL Parameters in Components


```js
// src/ItemDetail.jsx
import React from 'react';
import { useParams } from 'react-router-dom';

const ItemDetail = () => {
  const { id } = useParams();
  return (
    <div>
      <h2>Item Details</h2>
      <p>Item ID: {id}</p>
    </div>
  );
};

export default ItemDetail;
```