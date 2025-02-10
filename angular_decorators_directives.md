# **🚀 Angular 16+ Decorators & Directives – Complete Guide**  

Angular 16+ provides **decorators** and **directives** to enhance functionality and modularity.  

---

# **📌 1. Decorators in Angular 16+**
Decorators **add metadata** to classes, methods, properties, and parameters in Angular.

| **Decorator** | **Purpose** | **Use Case** |
|--------------|------------|-------------|
| `@Component` | Defines an Angular component. | Creating UI components (`app-header`, `app-footer`). |
| `@Directive` | Defines a custom directive. | Creating a custom attribute (`[highlight]`) to change styles. |
| `@Pipe` | Defines a custom pipe. | Creating a `capitalize` pipe to transform text. |
| `@Injectable` | Marks a service as injectable. | Creating a `UserService` to fetch data from an API. |
| `@Input` | Passes data from parent to child component. | Sending a `title` from `app.component` to `header.component`. |
| `@Output` | Sends events from child to parent component. | Sending a button click event from `child.component` to `parent.component`. |
| `@ViewChild` | Gets a reference to an HTML element or child component. | Getting an input field reference to focus dynamically. |
| `@ViewChildren` | Gets references to multiple elements. | Getting all buttons in a form. |
| `@HostListener` | Listens to events on the host element. | Detecting `mouseenter` and `mouseleave` for hover effects. |
| `@HostBinding` | Binds a class or style to the host element. | Changing background color dynamically. |

---

### **🔹 Example 1: `@Component` (Defines a Component)**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<h1>Hello, {{ name }}!</h1>`,
  styles: ['h1 { color: blue; }']
})
export class HelloComponent {
  name: string = 'Angular 16+';
}
```
✅ **Use Case**: When creating reusable UI components.

---

### **🔹 Example 2: `@Input` & `@Output` (Parent-Child Communication)**
#### **Parent Component (`app.component.ts`)**
```typescript
@Component({
  selector: 'app-root',
  template: `<app-child [message]="parentMessage" (messageEvent)="receiveMessage($event)"></app-child>`
})
export class AppComponent {
  parentMessage = "Hello from Parent!";
  
  receiveMessage(childMessage: string) {
    console.log("Received from child:", childMessage);
  }
}
```

#### **Child Component (`child.component.ts`)**
```typescript
@Component({
  selector: 'app-child',
  template: `
    <h2>{{ message }}</h2>
    <button (click)="sendMessage()">Send Message to Parent</button>
  `
})
export class ChildComponent {
  @Input() message!: string;
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit("Hello from Child!");
  }
}
```
✅ **Use Case**: When passing data between components.

---

### **🔹 Example 3: `@ViewChild` (Get a DOM Element)**
```typescript
import { Component, ElementRef, ViewChild, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `<input #inputField type="text" placeholder="Type here..." />`
})
export class ExampleComponent implements AfterViewInit {
  @ViewChild('inputField') inputElement!: ElementRef;

  ngAfterViewInit() {
    this.inputElement.nativeElement.focus();
  }
}
```
✅ **Use Case**: When manipulating DOM elements directly.

---

### **🔹 Example 4: `@HostListener` & `@HostBinding` (Detect Events & Style Changes)**
```typescript
import { Directive, HostListener, HostBinding } from '@angular/core';

@Directive({
  selector: '[hoverHighlight]'
})
export class HoverHighlightDirective {
  @HostBinding('style.backgroundColor') bgColor: string = 'transparent';

  @HostListener('mouseenter') onMouseEnter() {
    this.bgColor = 'yellow';
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.bgColor = 'transparent';
  }
}
```
✅ **Use Case**: When applying custom hover effects.

---

# **📌 2. Directives in Angular 16+**
Directives **add behavior** to elements.

## **🔹 2.1. Built-in Directives**
| **Directive** | **Type** | **Purpose** | **Example Use Case** |
|--------------|---------|-------------|----------------------|
| `*ngIf` | Structural | Conditionally render elements. | Show/hide login button if user is logged in. |
| `*ngFor` | Structural | Loop over an array. | Display a list of products. |
| `*ngSwitch` | Structural | Switch case for elements. | Display content based on user role. |
| `[ngClass]` | Attribute | Dynamically assign CSS classes. | Change button color based on status. |
| `[ngStyle]` | Attribute | Apply inline styles dynamically. | Change text color on user input. |

---

### **🔹 Example 5: `*ngIf` (Conditional Rendering)**
```html
<p *ngIf="isLoggedIn; else loginMessage">Welcome, User!</p>
<ng-template #loginMessage><p>Please log in.</p></ng-template>
```
✅ **Use Case**: Show content only when the user is logged in.

---

### **🔹 Example 6: `*ngFor` (Loop Over Data)**
```html
<ul>
  <li *ngFor="let item of items">{{ item }}</li>
</ul>
```
```typescript
items = ['Apple', 'Banana', 'Cherry'];
```
✅ **Use Case**: Displaying a dynamic list.

---

### **🔹 Example 7: `*ngSwitch` (Switch Case)**
```html
<div [ngSwitch]="userRole">
  <p *ngSwitchCase="'admin'">Welcome, Admin!</p>
  <p *ngSwitchCase="'user'">Welcome, User!</p>
  <p *ngSwitchDefault>Guest Access</p>
</div>
```
```typescript
userRole = 'admin';
```
✅ **Use Case**: Rendering content based on conditions.

---

### **🔹 Example 8: `[ngClass]` (Dynamic Classes)**
```html
<p [ngClass]="{'active': isActive, 'inactive': !isActive}">Status</p>
```
```typescript
isActive = true;
```
✅ **Use Case**: Changing styles dynamically.

---

### **🔹 Example 9: `[ngStyle]` (Dynamic Styling)**
```html
<p [ngStyle]="{'color': textColor, 'font-size': '20px'}">Styled Text</p>
```
```typescript
textColor = 'blue';
```
✅ **Use Case**: Applying inline styles dynamically.

---

## **🔥 Summary**
✔ **Decorators** provide metadata and behavior to classes, methods, and properties.  
✔ **Directives** modify the behavior of HTML elements.  
✔ **Use `@Component`, `@Directive`, `@Input`, `@Output`, `@ViewChild`, `@HostListener`, and `@HostBinding`** based on UI needs.  
✔ **Use `*ngIf`, `*ngFor`, `*ngSwitch`, `[ngClass]`, and `[ngStyle]`** to control element behavior.  

🚀 **Mastering these decorators and directives will help you build scalable Angular 16+ applications!**
Good question! In **Angular 16+**, the `@NgModule` decorator is **less emphasized** because Angular is moving towards a **standalone component-based approach**, reducing the need for modules in many cases. However, `@NgModule` is still relevant for large-scale applications, backward compatibility, and managing shared dependencies.

---

## **🛠 `@NgModule` in Angular 16+**
The `@NgModule` decorator is used to **define Angular modules**, grouping components, directives, pipes, and services together.

### **📌 When to Use `@NgModule`?**
1. **For backward compatibility** with older Angular versions.
2. **For organizing large applications** with multiple feature modules.
3. **For lazy loading** to improve performance.
4. **For sharing common functionalities** (e.g., custom pipes, directives, UI components).

---

## **📌 `@NgModule` Syntax**
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [AppComponent], // Declare components, directives, and pipes
  imports: [BrowserModule, FormsModule, HttpClientModule], // Import other modules
  providers: [], // Provide services
  bootstrap: [AppComponent] // Define the root component
})
export class AppModule {}
```

✅ **Use Case**: When bootstrapping a traditional Angular application.

---

## **🔹 Standalone Components (New in Angular 16+)**
Angular 16+ allows components to be **standalone**, removing the need for `@NgModule`.

### **🚀 Example: Standalone Component (`@Component` without `@NgModule`)**
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<h1>Hello, Angular 16+ Standalone!</h1>`,
  standalone: true
})
export class HelloComponent {}
```

### **🚀 Bootstrapping a Standalone Component (Without `@NgModule`)**
```typescript
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app.component';

bootstrapApplication(AppComponent);
```

✅ **Use Case**: When developing a modern Angular 16+ application with fewer dependencies.

---

## **🔍 Should You Still Use `@NgModule` in Angular 16+?**
- **YES** ✅ if working with older applications or structured enterprise-level apps.
- **NO** ❌ if starting a fresh Angular 16+ app, where standalone components are preferred.

---

## **🔥 Summary**
- `@NgModule` is still **useful for large applications**, lazy loading, and compatibility.
- **Standalone components** (`standalone: true`) **replace the need** for `@NgModule` in many cases.
- **For new projects**, prefer **standalone components** unless modularization is necessary.

🚀 **Angular 16+ is more flexible! You can mix both approaches as needed.**
