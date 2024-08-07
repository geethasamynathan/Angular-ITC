Create new angular project ==> ng new auth-demo

create 3 components
login
layout
dashboard

app.route.ts
```Typescript
import { Routes } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { LayoutComponent } from './layout/layout.component';
import { DashboardComponent } from './dashboard/dashboard.component';
import { authGuard } from './guard/auth.guard';

export const routes: Routes = [
  {
    path: '',
    redirectTo: 'login',
    pathMatch: 'full',
  },
  {
    path: 'login',
    component: LoginComponent,
  },
  {
    path: '',
    component: LayoutComponent,
    children: [
      {
        path: 'dashboard',
        component: DashboardComponent,
        canActivate: [authGuard],
      },
    ],
  },
];

```
create guard folder in app==>
ng g guard auth

select the type
canActivate ==> space bar ==> enter

auth-guard.ts
```Typescript
import { CanActivateFn, Router } from '@angular/router';
import { inject } from '@angular/core';

export const authGuard: CanActivateFn = (route, state) => {
  const router = inject(Router);
  debugger;
  const localData = localStorage.getItem('angular18Login');
  if (localData != null) {
    return true;
  } else {
    router.navigateByUrl('login');
    return false;
  }
};

```

login.component.ts
```Typescript
import { HttpClient } from '@angular/common/http';
import { Component, inject } from '@angular/core';
import { Router } from '@angular/router';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-login',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './login.component.html',
  styleUrl: './login.component.scss',
})
export class LoginComponent {
  loginObj: any = {
    EmailId: '',
    Password: '',
  };

  http = inject(HttpClient);

  constructor(private router: Router) {}
  res: any;
  onLogin() {
    debugger;
    if (
      this.loginObj.EmailId == 'geetha' &&
      this.loginObj.Password == 'admin'
    ) {
      /*this.http
      .post(
        'https://freeapi.miniprojectideas.com/api/User/Login',
        this.loginObj
      )
      .subscribe((res: any) => {
        debugger;)
        */
      // if (res.result) {
      this.res =
        'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c';
      alert('Login Success');
      localStorage.setItem('angular18Login', this.res);
      this.router.navigateByUrl('dashboard');
    } else {
      alert('Check User Name or Password');
    }
  }
}

```

# login.component.html
```html
<div class="parent">
  <div class="card">
    <h2>Login Form</h2>

    <!-- SE CONNECTER / S'INSCRIRE -->
    <div class="login_register">
      <a
        href="
        https://codepen.io/pen?template=gOEqMVq
        "
        class="login"
        target="blank"
        >Login</a
      >
      <a
        href="
        https://codepen.io/pen?template=VwRgKYB
        "
        class="register"
        target="blank"
        >Signup</a
      >
    </div>

    <!-- FORMULAIRE -->
    <form class="form">
      <input
        type="email"
        name="EmailId"
        [(ngModel)]="loginObj.EmailId"
        placeholder="Email Adress"
        class="email"
      />
      <input
        type="password"
        name="Password"
        [(ngModel)]="loginObj.Password"
        placeholder="password"
        class="pass"
      />
    </form>

    <!-- MOT DE PASSE OUBLIE ? -->
    <a href="#" class="fp">Forgot password?</a>

    <!-- BOUTTON LOGIN -->
    <button type="button" (click)="onLogin()" class="login_btn">Login</button>

    <!-- PIED DE LA CARD -->
    <div class="footer_card">
      <p>Not a member?</p>
      <a href="#">Singup now</a>
    </div>
  </div>
</div>



```
# login.component.css
```css
.parent{
    background-color: #282A36;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .card{
      width: auto;
      height: auto;
      background-color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      border-radius: 20px;
  }
  
  .card h2{
    margin-bottom: 10px;
  }
  
  .card a.fp{
    width: 100%;
    display: flex;
    color: #5881D0;
  }
  
  .login_register{
    display: flex;
    width: 100%;
    border: 1px solid rgba(221, 221, 221, 1);
    border-radius: 15px;
    margin: 20px 0;
  }
  
  .login_register a{
    font-size: 1em;
    padding: 10px 55px;
    border: none;
    width: 50%;
  }
  
  .login_register a.login{
    border-radius: 15px;
    background: linear-gradient(90deg, #003A74, #006AD5);
    color: white;
  }
  
  .login_register a.register{
    border-radius: 15px;
    background-color: transparent;
    color: black;
  }
  
  .form{
    display: flex;
    flex-direction: column;
    width: 100%;
  }
  
  .form input{
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #DDDDDD;
    color: #A0A6A3;
    font-family: "Roboto Mono", sans-serif;
    box-shadow: 1px 5px 9px rgba(211, 211, 211, .7);
  }
  
  .form input.email{
    margin-bottom: 15px;
  }
  
  .form input.pass{
    margin-bottom: 5px;
  }
  
  .login_btn{
    font-size: 20px;
    color: white;
    border-radius: 15px;
    border: none;
    background-color: #003A74;
    width: 100%;
    padding: 10px;
    margin-top: 15px;
    margin-bottom: 15px;
    background: linear-gradient(-90deg, #003A74, #006AD5);
    box-shadow: 1px 5px 9px rgba(211, 211, 211, .9);
  }
  
  .footer_card{
    display: flex;
    width: 100%;
    justify-content: center;
  }
  
  .footer_card p{
    margin-right: 10px;
  }
  
  .footer_card a{
    color: #5881D0;
  }
```

# layout.component.ts
```TypeScript
import { Component } from '@angular/core';
import { Route, RouterOutlet } from '@angular/router';
import { Router } from '@angular/router';
@Component({
  selector: 'app-layout',
  standalone: true,
  imports: [RouterOutlet],
  templateUrl: './layout.component.html',
  styleUrl: './layout.component.scss',
})
export class LayoutComponent {
  constructor(private router: Router) {}
  onLogout() {
    localStorage.removeItem('angular18Login');
    this.router.navigateByUrl('/login');
  }
}

```

# layout.component.html
```html
<nav class="navbar navbar-expand-sm navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="javascript:void(0)">Logo</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#mynavbar"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="mynavbar">
      <ul class="navbar-nav me-auto">
        <li class="nav-item" style="margin-top: -12px">
          <a class="nav-link active" href="javascript:void(0)">Link</a>
        </li>
        <li class="nav-item" style="margin-top: -12px">
          <a class="nav-link" href="javascript:void(0)">Link</a>
        </li>
        <li class="nav-item" style="margin-top: -12px">
          <a class="nav-link" (click)="onLogout()" href="javascript:void(0)">Logout</a>
        </li>
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" type="text" placeholder="Search" />
        <button class="btn btn-primary" type="button">Search</button>
      </form>
    </div>
  </div>
</nav>

<router-outlet></router-outlet>
```

# dashboard.component.ts
```Typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-dashboard',
  standalone: true,
  imports: [],
  templateUrl: './dashboard.component.html',
  styleUrl: './dashboard.component.scss'
})
export class DashboardComponent {

}


```
# dashboard.component.html
```html
<p>dashboard works!</p>

```

# app.routes.ts
```TypeScript
 {
    path: '',
    component: LayoutComponent,
    children: [
      {
        path: 'dashboard',
        component: DashboardComponent,
       // canActivate: [authGuard],
      },
    ],
  },
  ```

  in the above scenario
   if i entered url as below it will redirect even without login
   ![alt text](image-44.png)

   but it is not correct .to avoid redirection
`canActivate: [authGuard],` is must  in app.route.ts

![alt text](image-45.png)
