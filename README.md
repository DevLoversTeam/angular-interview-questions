<h1>
  Angular <img src="./assets/angular.svg" width="40" height="40" />
</h1>

<h2>Найпопулярніші запитання та відповіді на співбесіді з Angular</h2>

### Основи Angular

<details>
<summary>1. Що таке Angular та які його ключові особливості?</summary>

#### Angular

- **Angular** — це сучасний фронтенд-фреймворк від Google для побудови SPA та
  масштабованих веб-додатків.

#### Ключові особливості Angular 20:

- **Standalone Components** — більше немає потреби у NgModules.

- **Signals** — новий реактивний підхід до роботи зі станом.

- **Control flow (@if, @for, @switch)** — нативний синтаксис замість *ngIf та
  *ngFor.

- **DI (Dependency Injection)** — гнучка система залежностей із підтримкою
  tree-shaking.

- **Router API** — сучасна маршрутизація без модулів, з lazy loading.

- **TypeScript + строгі типи** — безпечна розробка на TS.

- **Оптимізований рендер** — швидкий change detection, підготовка до zoneless
  архітектури.

Коротко: Angular — це full-fledged фреймворк із вбудованим DI, реактивністю
через signals та сучасними standalone підходами, що дозволяють писати
масштабовані додатки без зайвої складності

</details>

<details>
<summary>2. Поясни, що таке data-binding в Angular та які є його типи?</summary>

#### Angular

- Data-binding — це механізм синхронізації даних між компонентом і шаблоном.

#### Типи data-binding в Angular:

1. **Interpolation** — одностороннє відображення даних у HTML:

```html
<p>{{ userName }}</p>
```

2. **Property binding** — передача значень у властивості
   DOM-елементів/компонентів:

```html
<img [src]="avatarUrl" />
```

3. **Event binding** — реакція на події DOM:

```html
<button (click)="onSave()">Save</button>
```

4. **Two-way binding** — синхронізація стану між шаблоном і компонентом
   ([(...)]):

```html
<input [(ngModel)]="email" />
```

Коротко: в Angular доступні 4 основні типи зв’язування даних — interpolation,
property binding, event binding, two-way binding.

</details>

<details>
<summary>3. Опиши архітектуру Angular-додатку.</summary>

#### Angular

- Архітектура Angular базується на компонентному підході з чітким розділенням
  відповідальностей.

#### Основні елементи:

- **Компоненти (Standalone)** — будівельні блоки UI, кожен має шаблон, стилі,
  логіку.

- **Сервіси** — бізнес-логіка, робота з API, збереження стану; надаються через
  DI.

- **Signals** — сучасний спосіб керування станом і реактивністю.

- **Control flow (@if, @for, @switch)** — керування відображенням у шаблонах.

- **Router** — маршрутизація між екранами без NgModules, з підтримкою lazy
  loading.

- **Dependency Injection** — інжекція залежностей з різними scope (root,
  component, environment).

</details>

<details>
<summary>4. Що таке компонент в Angular та як він використовується?</summary>

#### Angular

- Компонент — це основний будівельний блок Angular-додатку, що відповідає за
  частину UI та пов’язану з нею логіку.

#### Складається з:

- класу (логіка, стан),

- шаблону HTML,

- стилів,

- метаданих (selector, imports тощо).

#### Використання:

```TypeScript
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-user-card',
  standalone: true,
  template: `
    <h3>{{ name() }}</h3>
    <button (click)="changeName()">Change</button>
  `
})
export class UserCardComponent {
  name = signal('Viktor');
  changeName() {
    this.name.set('Updated Name');
  }
}
```

У шаблоні іншого компонента можна підключити:

```html
<app-user-card></app-user-card>
```

Коротко: Компонент = ізольований блок UI + логіка. В Angular він створюється як
standalone, без NgModules.

</details>

<details>
<summary>5. Що таке директиви в Angular та які з них найчастіше використовуються?</summary>

#### Angular

- Директива — це інструкція для DOM-елемента або компонента, яка змінює його
  поведінку чи вигляд.

#### Типи директив:

- **Structural** (змінюють DOM):

  -`@if` (новий синтаксис замість `*ngIf`)

  - `@for` (новий синтаксис замість `*ngFor`)

  - `@switch` (альтернатива `*ngSwitch`)

- **Attribute** (змінюють властивості/стилі елемента):

  - `ngClass`

  - `ngStyle`

  - `ngModel`

- **Custom directives** — можна створювати свої для повторного використання
  логіки.

✅ Коротко: директиви в Angular = спосіб керувати DOM. Найчастіше — `@if`,
`@for`, `ngClass`, `ngStyle`, `ngModel`.

</details>

<details>
<summary>6. Як створити сервіс в Angular і навіщо його використовують?</summary>

#### Angular

- Сервіс — це клас із бізнес-логікою або функціоналом, який не пов’язаний
  напряму з UI.

Використовується для:

- повторного використання коду,

- роботи з API,

- керування станом,

- інкапсуляції логіки поза компонентом.

#### Приклад:

```TypeScript
import { Injectable, signal } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class UserService {
  userName = signal('Guest');

  setUser(name: string) {
    this.userName.set(name);
  }
}
```

#### Використання у компоненті:

```TypeScript
import { Component, inject } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-header',
  standalone: true,
  template: `<h2>Welcome, {{ userService.userName() }}</h2>`
})
export class HeaderComponent {
  userService = inject(UserService);
}
```

Коротко: сервіс створюють через `@Injectable`, а використовують для
бізнес-логіки та спільного стану між компонентами.

</details>

<details>
<summary>7. Поясни, що таке dependency injection (DI) в Angular.</summary>

#### Angular

- Dependency Injection (DI) — це механізм Angular, який автоматично створює та
  надає об’єкти (сервіси, токени) компонентам чи іншим сервісам замість ручного
  створення через new.

#### Навіщо:

- спрощує тестування (можна підмінити залежності mock-ами),

- забезпечує повторне використання сервісів,

- керує життєвим циклом об’єктів (singleton, scoped).

#### Приклад:

```TypeScript
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class ApiService {
  getData() {
    return ['item1', 'item2'];
  }
}
```

Використання у компоненті:

```TypeScript
import { Component, inject } from '@angular/core';
import { ApiService } from './api.service';

@Component({
  selector: 'app-list',
  standalone: true,
  template: `<li *ngFor="let item of data">{{ item }}</li>`
})
export class ListComponent {
  api = inject(ApiService);
  data = this.api.getData();
}
```

Коротко: DI в Angular = автоматичне надання залежностей (наприклад, сервісів)
компонентам без `new`.

</details>

<details>
<summary>8. Що таке модуль в Angular і для чого він використовується?</summary>

#### Angular

- У попередніх версіях Angular (до 15) модулі (NgModule) були обов’язковими для
  структурування застосунку. В Angular 20 модулі більше не потрібні, оскільки
  з’явилися standalone components.

#### Проте модулі ще існують і можуть застосовуватись для:

- сумісності зі старим кодом,

- групування функціоналу (напр. Angular Material ще має модулі),

- поступової міграції на standalone API.

#### Приклад старого підходу:

```TypeScript
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

#### Актуальний підхід (Angular 20, без модуля):

```TypeScript
bootstrapApplication(AppComponent, {
  providers: []
});
```

Коротко: модулі в Angular зараз — це легасі-інструмент, який замінено на
standalone компоненти. Їхня головна роль сьогодні — лише для підтримки старого
коду чи бібліотек.

</details>

<details>
<summary>9. Як обробляти події в Angular?</summary>

#### Angular

- В Angular події обробляються через event binding, тобто підписку на подію DOM
  або кастомної події компонента.

#### Синтаксис:

```html
<button (click)="onClick()">Click me</button>
```

#### У компоненті:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-button',
  standalone: true,
  template: `<button (click)="onClick()">Click me</button>`,
})
export class ButtonComponent {
  onClick() {
    console.log('Button clicked!');
  }
}
```

#### Кастомна подія (для дочірнього компонента):

```TypeScript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  standalone: true,
  template: `<button (click)="notifyParent()">Notify</button>`
})
export class ChildComponent {
  @Output() notify = new EventEmitter<string>();
  notifyParent() {
    this.notify.emit('Hello from child');
  }
}
```

#### У батьківському компоненті:

```html
<app-child (notify)="onNotify($event)"></app-child>
```

Коротко: в Angular події обробляються через `(eventName)="handler()"` для DOM та
через `@Output` + `EventEmitter` для кастомних подій.

</details>

<details>
<summary>10. Що таке двостороннє зв’язування (two-way binding) і як його реалізувати в Angular?</summary>

#### Angular

- Двостороннє зв’язування — це синхронізація стану між компонентом і шаблоном,
  коли зміни в UI автоматично оновлюють дані компонента і навпаки.

#### Класичний підхід (з ngModel):

```html
<input [(ngModel)]="name" />
<p>Hello, {{ name }}</p>
```

```TypeScript
import { Component } from '@angular/core';

@Component({
  selector: 'app-input',
  standalone: true,
  template: `<input [(ngModel)]="name" />`
})
export class InputComponent {
  name = 'Viktor';
}
```

#### Сучасний Angular 20 з signals:

```TypeScript
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-input',
  standalone: true,
  template: `<input [value]="name()" (input)="name.set($any($event.target).value)" />`
})
export class InputComponent {
  name = signal('Viktor');
}
```

Коротко: two-way binding = синхронізація стану між UI та компонентом. В Angular
20 можна робити через [(ngModel)] або signals для сучасної реактивності.

</details>

<details>
<summary>11. Поясни різницю між компонентом і директивою в Angular?</summary>

#### Angular

- Компонент

  - це спеціальний тип директиви, який має шаблон (HTML) + стилі + логіку;

  - використовується для створення UI-елементів;

  - приклад: `@Component({ selector: 'app-user', template: '<p>User</p>' })`.

- Директива

  - не має власного шаблону;

  - змінює поведінку або вигляд існуючих елементів/компонентів;

  - може бути structural (`@if`, `@for`) або attribute (`ngClass`, `ngStyle`).

#### Приклад кастомної директиви (attribute):

```TypeScript
import { Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[highlight]',
  standalone: true
})
export class HighlightDirective {
  constructor(el: ElementRef, r: Renderer2) {
    r.setStyle(el.nativeElement, 'background', 'yellow');
  }
}
```

Використання у шаблоні:

```html
<p highlight>Text with highlight</p>
```

Коротко: компонент = директива + шаблон, а директива = поведінка без власного
UI.

</details>

<details>
<summary>12. Що таке пайпи (Pipes) в Angular та де їх варто використовувати?</summary>

#### Angular

- Pipe — це клас, який трансформує дані без зміни їхнього оригінального стану.
  Використовується у шаблонах для форматування значень.

#### Приклади вбудованих пайпів:

- `date` → форматування дат

- `currency` → вивід валют

- `uppercase` / `lowercase` → зміна регістру

- `async` → робота з Promise / Observable

#### Приклад використання:

```html
<p>{{ today | date:'dd/MM/yyyy' }}</p>
<p>{{ price | currency:'USD' }}</p>
```

#### Кастомний pipe:

```TypeScript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'exclaim',
  standalone: true
})
export class ExclaimPipe implements PipeTransform {
  transform(value: string): string {
    return value + '!';
  }
}
```

У шаблоні:

```html
<p>{{ 'Hello' | exclaim }}</p>
<!-- Hello! -->
```

Коротко: Pipes потрібні для форматування та трансформації даних у шаблоні, щоб
не захаращувати логіку компонента.

</details>

<details>
<summary>13. Як обробляти надсилання форм (form submissions) в Angular?</summary>

#### Angular

- В Angular є два основні підходи:

1. **Template-driven forms** (простий варіант, з `ngModel`):

```html
<form #form="ngForm" (ngSubmit)="onSubmit(form.value)">
  <input name="email" [(ngModel)]="email" required />
  <button type="submit">Send</button>
</form>
```

```TypeScript
onSubmit(value: any) {
  console.log('Form submitted:', value);
}
```

2. **Reactive forms** (рекомендований для складних кейсів):

```TypeScript
import { Component } from '@angular/core';
import { FormControl, FormGroup, ReactiveFormsModule } from '@angular/forms';

@Component({
  selector: 'app-login',
  standalone: true,
  imports: [ReactiveFormsModule],
  template: `
    <form [formGroup]="form" (ngSubmit)="onSubmit()">
      <input formControlName="email" />
      <button type="submit">Login</button>
    </form>
  `
})
export class LoginComponent {
  form = new FormGroup({
    email: new FormControl('')
  });

  onSubmit() {
    console.log(this.form.value);
  }
}
```

Коротко: форми в Angular обробляються через (`ngSubmit`) і бувають
template-driven та reactive. Для простих форм можна брати `ngModel`, для великих
і складних — reactive forms.

</details>

<details>
<summary>14. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>15. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>16. ???</summary>

#### Angular

- Coming soon...😎

</details>
