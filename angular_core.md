---
### 1. **Components**
#### **What is a Component?**
A component is the building block of an Angular application. It controls a portion of the user interface (UI) and defines both the **HTML structure** (template) and **logic** (TypeScript class). Components are reusable and manage data for the views they control.

#### **Why use Components?**
- To create modular, reusable, and maintainable code.
- Each component focuses on a specific part of the UI, making the app easy to understand and scale.

#### **Example Code:**
```typescript
import { Component } from '@angular/core'; // Import the Component decorator.

@Component({
  selector: 'app-hello-world', // Defines the custom HTML tag for this component.
  template: `<h1>{{ message }}</h1>`, // The HTML content displayed in the browser.
  styles: [`h1 { color: green; }`] // CSS styles specific to this component.
})
export class HelloWorldComponent { // The logic for the component.
  message = 'Hello, Angular!'; // A variable used in the template.
}
```

#### **Line-by-Line Explanation:**
1. **`import { Component } from '@angular/core';`**  
   - Import Angular's `Component` decorator to define a class as a component.

2. **`@Component({...})`**  
   - The `@Component` decorator provides metadata about the component:
     - **`selector`**: Defines the custom HTML tag (`<app-hello-world>`) for this component.
     - **`template`**: Inline HTML that will render in the browser.
     - **`styles`**: Inline CSS to style this component.

3. **`export class HelloWorldComponent { ... }`**  
   - This is the class that contains the component's logic.
   - **`message`**: A variable accessible in the template via interpolation (`{{ message }}`).

---

### **Basic Interview Question:**
**Q: What is the purpose of the `@Component` decorator in Angular?**

**A:** The `@Component` decorator marks a class as an Angular component and provides metadata such as the HTML selector, template, and styles that define the component's view.

---

### 2. **Services**
#### **What is a Service?**
A service in Angular is a class that provides business logic, reusable methods, or data that multiple components can share. Services make applications modular by separating logic from UI components.

#### **Why use Services?**
- To share data or logic across multiple components.
- To keep components clean by delegating complex logic to services.
- To make code reusable and testable.

#### **Example Code:**
```typescript
// Service (data.service.ts)
import { Injectable } from '@angular/core'; // Import Injectable to make this class a service.

@Injectable({
  providedIn: 'root', // Makes this service globally available in the app.
})
export class DataService {
  getData() { // Method to fetch data.
    return ['Apple', 'Banana', 'Cherry'];
  }
}

// Component using the service (app.component.ts)
import { Component } from '@angular/core';
import { DataService } from './data.service'; // Import the service.

@Component({
  selector: 'app-root',
  template: `<ul><li *ngFor="let item of items">{{ item }}</li></ul>`, // Displays a list.
})
export class AppComponent {
  items: string[]; // Variable to store data.

  constructor(private dataService: DataService) { // Inject the service into the component.
    this.items = this.dataService.getData(); // Fetch data during initialization.
  }
}
```

#### **Line-by-Line Explanation:**
**Service:**
1. **`@Injectable({...})`**: Declares the class as a service and specifies its scope.
2. **`providedIn: 'root'`**: Automatically registers the service in the root injector, making it available globally.
3. **`getData()`**: A simple method that returns a list of strings.

**Component:**
1. **`constructor(private dataService: DataService)`**: Injects the `DataService` into the component.
2. **`this.dataService.getData()`**: Calls the service method to get data.

---

### **Basic Interview Question:**
**Q: What is the difference between `@Injectable` and `providedIn`?**

**A:**  
- `@Injectable` marks a class as a service that can be injected into other parts of the app.  
- `providedIn` specifies where the service should be available (e.g., `root` makes it globally available).

---

### 3. **Directives**
#### **What is a Directive?**
Directives are instructions that tell Angular how to modify or manipulate the DOM. There are three types:
1. **Structural Directives**: Add or remove elements (e.g., `*ngIf`, `*ngFor`).
2. **Attribute Directives**: Change the behavior or appearance of an element (e.g., `[style]`, `[class]`).
3. **Custom Directives**: Define custom behavior for elements.

#### **Why use Directives?**
- To dynamically control UI elements based on conditions or logic.
- To enhance reusability by abstracting common behavior.

#### **Example Code:**
```html
<div *ngIf="isVisible">Content is visible!</div> <!-- Shown only if isVisible is true. -->
<div [style.color]="isVisible ? 'green' : 'red'">This text changes color.</div> <!-- Color changes dynamically. -->
```

#### **Line-by-Line Explanation:**
1. **`*ngIf="isVisible"`**: Structural directive to conditionally display the `div`. If `isVisible` is `false`, the element is removed from the DOM.
2. **`[style.color]`**: Attribute directive to dynamically set the color of the text.

---

### **Basic Interview Question:**
**Q: What is the difference between structural and attribute directives in Angular?**

**A:**  
- **Structural Directives**: Modify the DOM structure (e.g., `*ngIf`, `*ngFor`).  
- **Attribute Directives**: Modify the behavior or appearance of existing elements (e.g., `[style]`, `[class]`).

---

### 4. **Pipes**
#### **What is a Pipe?**
Pipes transform data before displaying it in the template (e.g., formatting dates, numbers, or strings).

#### **Why use Pipes?**
- To format data directly in the template without modifying the component logic.

#### **Example Code:**
```html
<p>{{ 'hello world' | uppercase }}</p> <!-- Output: HELLO WORLD -->
<p>{{ 12345.678 | number:'1.2-2' }}</p> <!-- Output: 12,345.68 -->
```

#### **Line-by-Line Explanation:**
1. **`| uppercase`**: Converts text to uppercase.
2. **`| number:'1.2-2'`**: Formats the number to 1 digit before the decimal, and 2 digits after it.

---

### **Basic Interview Question:**
**Q: Can we create custom pipes in Angular? How?**

**A:** Yes, by using the `@Pipe` decorator to create reusable transformations.

---
