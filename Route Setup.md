React Router Installation (Website में pages बनेंगे इसलिए router चाहिए।)

    npm install react-router-dom

Add a folder with name routes as:

    src
     │
     ├── components
     │      Navbar.tsx
     │      Footer.tsx
     │
     ├── pages
     │      Home.tsx
     │      FindTutor.tsx
     │      BecomeTutor.tsx
     |
     |── routes                 <- Notice here
     |      AppRoutes.tsx
     │
     ├── assets
     │      images
     │
     ├── App.tsx
     └── main.tsx

AppRoutes.tsx

    import { Routes, Route } from "react-router-dom";
    import Home from "../pages/Home";
    
    const AppRoutes = () => {
      return (
        <Routes>
          <Route path="/" element={<Home />} />
        </Routes>
      );
    };
    
    export default AppRoutes;

Register AppRoutes.tsx in App.tsx as:

    import { BrowserRouter } from "react-router-dom";
    import AppRoutes from "./routes/AppRoutes";
    
    function App() {
      return (
        <BrowserRouter>
          <AppRoutes />
        </BrowserRouter>
      );
    }
    
    export default App;

Create a test page

    src
     │
     ├── components
     │      Navbar.tsx
     │      Footer.tsx
     │
     ├── pages
     │      Home.tsx

Run the command

    npm rund dev

Test the Home URL
