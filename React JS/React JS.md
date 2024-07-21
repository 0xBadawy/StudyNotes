<div style="text-align: center;">
  <h1>React JS</h1>
<br>
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



***


### Install React Router

- ```npm install react-router-dom```

<br>

#### create a new file to use Rounting **AppLayout.jsx**

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
<br>


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

<br>

#### Access URL Parameters in Components


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

<br><br>

---

## Axios HTTP requests

Install Axios

- ```npm install axios```



```js
// src/api.js
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_TOKEN', // Static token
    'x-api-key': 'YOUR_API_KEY' // API key
  }
});

export default api;
```

#### Use the Axios Instance in Components

```js
import React, { useState, useEffect } from 'react';
import api from './api'; // Import the custom Axios instance

const MyComponent = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    api.get('/data')
      .then(response => {
        setData(response.data);
        setLoading(false);
      })
      .catch(error => {
        setError(error);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <div>
      <h1>Data</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </div>
  );
};

export default MyComponent;
 ```




