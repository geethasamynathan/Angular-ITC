# Data Bininding
Data binding in Angular is a powerful feature that helps synchronize the data between the model and the view, making it easier to manage and display dynamic data.

1. One-Way Data Binding
2. Two-Way Data Binding
3. Interpolation
4. Property Binding
5. Event Binding
6. 
# Interpolation
It is used to one way binding data from a component to your view

Normally Interpolation is denoted as double curly braces ( Example: { { } } )

Imagine you want to show a name on your site. With interpolation, you can put your code directly into the web page using double curly braces shown in the following example:

Example: app.component.html
<h1>{{ title }}</h1>
Example: app.component.html
app.component.ts

```TypeScript
 export class AppComponent {
  title = 'first-app';
}
```
output:
![alt text](image-9.png)