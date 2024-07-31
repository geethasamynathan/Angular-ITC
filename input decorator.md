# @Input
Sometimes app development requires you to send data into a component. This data can be used to customize a component or perhaps send information from a parent component to a child component.

Angular uses a concept called Input. This is similar to props in other frameworks. To create an Input property, use the @Input decorator.

user.component.ts

ng g c user

from home(or) app component we shpuld pass the value and
ite recieves the value from app (or) home and display in user component

# user.component.ts

export class UserComponent {
  @Input() occupation = '';
}

# user.component.html
<p>user designation is :{{ occupation }}</p>

app.component.html

<app-user companyName="ITC Infotech"></app-user>
# @Output
When working with components it may be required to notify other components that something has happened. Perhaps a button has been clicked, an item has been added/removed from a list or some other important update has occurred. In this scenario components need to communicate with parent components.

Angular uses the @Output decorator to enable this type of behavior.
`ng g c child-output`