
create a new folder in app ==>pages
==> ng g c login
==> ng g c layout
==> ng g c dashboard

app.route.ts
```Typescript
import { Routes } from '@angular/router';
import { Component } from '@angular/core';
import { LoginComponent } from './pages/login/login.component';
import { LayoutComponent } from './pages/layout/layout.component';
import path from 'path';
import { DashboardComponent } from './pages/dashboard/dashboard.component';

export const routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: '', redirectTo: '/login', pathMatch: 'full' },
  {    path: '',    component: LayoutComponent,
    children: [{ path: 'dashboard', component: DashboardComponent }],
  },
];
```
# logintoken.Service.ts

```Typescript

create services folder in app ==>Service
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { text } from 'stream/consumers';

@Injectable({
  providedIn: 'root'
})
export class LoginTokenService {

  constructor(private http:HttpClient) { }

  validateCredentials(data:any):Observable<any>{
    return  this.http
    .post(`https://localhost:7113/api/token`, data, {
      responseType: 'text',
    });
  }
}
```
# login.component.ts
```Typescript
import { Component } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { FormsModule } from '@angular/forms';
import { Router } from '@angular/router';
import { LoginTokenService } from '../../services/login-token.service';
@Component({
  selector: 'app-login',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './login.component.html',
  styleUrl: './login.component.scss',
})
export class LoginComponent {
  loginobj: any = {
    displayName: 'Geetha',
    userName: 'Admin',
    email: '',
    password: '',
  };
  token = '';
  constructor(
    private http: HttpClient,
    private route: Router,
    private tokenService: LoginTokenService
  ) {}
  onLogin() {
    this.tokenService
      .validateCredentials(this.loginobj)
      .subscribe((res: any) => {
        if (res) {
          this.token = res;
          // alert('login success');
          localStorage.setItem('loginToken', res);
          this.route.navigateByUrl('/dashboard');
          alert(this.token);
        } else {
          alert('login failed');
        }
      });
  }
}

```
login.component.html
```html
<div class="parent">
  <div class="main">
    <input type="checkbox" id="chk" aria-hidden="true" />

    <div class="signup">
      <form>
        <label for="chk" aria-hidden="true">Sign up</label>
        <input type="text" name="txt" placeholder="User name" required="" />
        <input type="email" name="email" placeholder="Email" required="" />
        <input
          type="number"
          name="broj"
          placeholder="BrojTelefona"
          required=""
        />
        <input type="password" name="pswd" placeholder="Password" required="" />
        <button>Sign up</button>
      </form>
    </div>

    <div class="login">
      <form>
        <label for="chk" aria-hidden="true">Login</label>
        <input
          type="email"
          name="email"
          [(ngModel)]="loginobj.email"
          placeholder="Email"
          required=""
        />
        <input
          type="password"
          name="password"
          placeholder="Password"
          required=""
          [(ngModel)]="loginobj.password"
        />
        <button (click)="onLogin()">Login</button>
      </form>
    </div>
  </div>
</div>

```
layout.html
```html
<p>layout works!</p>

<textarea cols="250" rows="8">    {{ token }}</textarea>

```
layout.component.ts
```TypeScript
token=localstorage.getItem('loginToken')
```