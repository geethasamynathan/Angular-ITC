# Reactive Forms Demo
ng g c login-reactive-form

# login-reactive-form.component.html
<form [formGroup]="loginForm1" (ngSubmit)="onSubmit(loginForm1)">
  <div class="form-group">
    <label for="email">Enter the Email</label>
    <input
      type="text"
      name="email"
      formControlName="email"
      class="form-control"
    />
  </div>
  <div class="form-group">
    <label for="email">Enter the Password</label>
    <input
      type="text"
      name="password"
      formControlName="password"
      class="form-control"
    />
  </div>
  <div class="form-group">
    <button type="submit" class="btn btn-success">Login</button>
    <button type="cancel" class="btn btn-danger">Cancel</button>
  </div>
</form>

# login-reactive-form.component.ts
```Typescript
import { Component, inject, Inject } from '@angular/core';
import { FormBuilder, FormsModule, ReactiveFormsModule } from '@angular/forms';
@Component({
  selector: 'app-login-reactive-form',
  standalone: true,
  imports: [ReactiveFormsModule],
  templateUrl: './login-reactive-form.component.html',
  styleUrl: './login-reactive-form.component.scss',
})
export class LoginReactiveFormComponent {
  fb = inject(FormBuilder);
  loginForm1 = this.fb.group({
    email: [''],
    password: [''],
  });

  onSubmit(loginForm1: any) {
    console.log(loginForm1.value);
  }
}
```

#login-reactive.component.html
```html
<form [formGroup]="loginForm1" (ngSubmit)="onSubmit(loginForm1)">
  <div class="form-group">
    <label for="email">Enter the Email</label>
    <input
      type="text"
      name="email"
      formControlName="email"
      class="form-control"
    />
  </div>
  <div class="form-group">
    <label for="password">Enter the Password</label>
    <input
      type="text"
      name="password"
      formControlName="password"
      class="form-control"
    />
  </div>
  <div class="form-group">
    <button type="submit" class="btn btn-success">Login</button>
    <button type="cancel" class="btn btn-danger">Cancel</button>
  </div>
</form>
```


#validation
**login-reactive-component.ts**
```TypeScript

 loginForm1 = this.fb.group({
    email: ['', [Validators.required, Validators.minLength(3)]],
    password: ['', Validators.required],
  });
  ```

  **login-reactive-component.html**
  ```Html
   @if(loginForm1.get('email')?.touched &&
    loginForm1.get('email')?.hasError('required')) {
    <span class="text-danger">Email is required</span>
    } @if(loginForm1.get('email')?.touched &&
    loginForm1.get('email')?.hasError('minlength')) {
    <span class="text-danger">email should have atleast 3 chars</span>
    }

    <button
      type="submit"
      [disabled]="!loginForm1.valid"
      class="btn btn-success"
    >
    ```