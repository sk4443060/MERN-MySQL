There are 2 parts:
 - backend
 - frontend

| FRONTEND ||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||

[01].Navigate into the frontend (This command generates a file package.json):

    npm create vite@latest .

| NOTE: Follow the questions and it will setup the react frontend
  I am selecting:
  - Framework: React
  - Varient  : Typescript

[02].Now enter this command to install all dependencies

    npm install

[03].Project Structure Clean
frontend/src

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
     |── routes
     |      AppRoutes.tsx
     │
     ├── assets
     │      images
     │
     ├── App.tsx
     └── main.tsx

[04].React Router Installation (Website में pages बनेंगे इसलिए router चाहिए।)

    npm install react-router-dom
