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
<summary>14. Що таке Angular CLI і для чого його використовують?</summary>

#### Angular

- **Angular CLI** — це офіційний інструмент командного рядка для створення та
  керування Angular-проєктами.

#### Основні можливості:

- `ng new` → створення нового застосунку

- `ng serve` → локальний дев-сервер з hot reload

- `ng generate (ng g)` → генерація компонентів, сервісів, пайпів, директив

- `ng build` → продакшн-білд з оптимізацією

- `ng test, ng e2e` → запуск тестів

- `ng add` → інтеграція бібліотек (напр. Angular Material)

- `ng update` → оновлення Angular до нової версії

Коротко: Angular CLI = швидкий старт, генерація коду, білд і управління життєвим
циклом проєкту.

</details>

<details>
<summary>15. Як виконувати HTTP-запити в Angular за допомогою HttpClient ?</summary>

#### Angular

- В Angular для роботи з HTTP використовується HttpClient, який надає методи
  get, post, put, delete тощо.

#### Кроки:

1. Імпортувати HttpClientModule у bootstrapApplication.

2. Інжектити HttpClient у сервіс чи компонент.

3. Виконати запит і підписатися (або використовувати async pipe).

#### Приклад сервісу:

```TypeScript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({ providedIn: 'root' })
export class ApiService {
  constructor(private http: HttpClient) {}

  getUsers() {
    return this.http.get('https://jsonplaceholder.typicode.com/users');
  }
}
```

#### Використання у компоненті:

```TypeScript
import { Component, inject } from '@angular/core';
import { AsyncPipe, NgFor } from '@angular/common';
import { ApiService } from './api.service';

@Component({
  selector: 'app-users',
  standalone: true,
  imports: [NgFor, AsyncPipe],
  template: `
    <ul>
      <li *ngFor="let user of users$ | async">{{ user.name }}</li>
    </ul>
  `
})
export class UsersComponent {
  api = inject(ApiService);
  users$ = this.api.getUsers();
}
```

Коротко: в Angular 20 HTTP-запити робляться через HttpClient, а результат часто
обробляється в шаблоні через async pipe.

</details>

<details>
<summary>16. Як передати дані з батьківського компонента до дочірнього?</summary>

#### Angular

- Передача даних відбувається через input-зв’язування (@Input() декоратор).
  Батьківський компонент передає значення дочірньому через атрибут у шаблоні.

#### Приклад:

**child.component.ts**

```TypeScript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  standalone: true,
  template: `<p>Message: {{ message }}</p>`
})
export class ChildComponent {
  @Input() message = '';
}
```

**parent.component.ts**

```TypeScript
import { Component } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'app-parent',
  standalone: true,
  imports: [ChildComponent],
  template: `<app-child [message]="parentMessage"></app-child>`
})
export class ParentComponent {
  parentMessage = 'Hello from Parent!';
}
```

**Коротко:**

- Дані від батька до дитини передаються через @Input() — це property binding
  [property]="value".

</details>

<details>
<summary>17. Як передати подію або дані від дочірнього компонента до батьківського?</summary>

#### Angular

- Для передачі подій вгору використовується @Output() разом із EventEmitter.
  Дочірній компонент «викидає» подію, а батьківський підписується на неї через
  (eventName) у шаблоні.

**child.component.ts**

```TypeScript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  standalone: true,
  template: `<button (click)="sendMessage()">Send</button>`
})
export class ChildComponent {
  @Output() message = new EventEmitter<string>();

  sendMessage() {
    this.message.emit('Hello from Child!');
  }
}
```

**parent.component.ts**

```TypeScript
import { Component } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'app-parent',
  standalone: true,
  imports: [ChildComponent],
  template: `<app-child (message)="onMessage($event)"></app-child>`
})
export class ParentComponent {
  onMessage(data: string) {
    console.log('Received from child:', data);
  }
}
```

- Коротко: передача даних child → parent відбувається через @Output() і (event)
  binding. Дитина емітить подію, батько слухає.

</details>

<details>
<summary>18. Які є життєві цикли (lifecycle hooks) компонентів в Angular і що вони означають?</summary>

#### Angular

- Lifecycle hooks — це методи, які Angular викликає на різних етапах «життя»
  компонента: створення, оновлення, знищення.

#### Основні хуки Angular:

| Хук                         | Коли викликається                                        | Типове використання                                         |
| --------------------------- | -------------------------------------------------------- | ----------------------------------------------------------- |
| **ngOnChanges(changes)**    | Коли змінюються @Input властивості                       | Реакція на зміни вхідних даних від батьківського компонента |
| **ngOnInit()**              | Один раз після ініціалізації компоненту                  | Ініціалізація даних, запитів до API                         |
| **ngDoCheck()**             | На кожній зміні (детекції)                               | Кастомна логіка перевірки змін                              |
| **ngAfterContentInit()**    | Один раз після вставлення контенту (ng-content)          | Робота з проєктованим контентом                             |
| **ngAfterContentChecked()** | Після кожної перевірки контенту                          | Оновлення після змін у проєктованому контенті               |
| **ngAfterViewInit()**       | Один раз після ініціалізації view (дочірніх компонентів) | Доступ до елементів через ViewChild/ViewChildren            |
| **ngAfterViewChecked()**    | Після кожної перевірки view                              | Оновлення DOM після перевірки                               |
| **ngOnDestroy()**           | Перед знищенням компоненту                               | Очищення підписок, таймерів, ресурсів                       |

#### Приклад:

```TypeScript
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-demo',
  standalone: true,
  template: `<p>Lifecycle demo</p>`
})
export class DemoComponent implements OnInit, OnDestroy {
  ngOnInit() {
    console.log('Component initialized');
  }

  ngOnDestroy() {
    console.log('Component destroyed');
  }
}
```

- Коротко: Lifecycle hooks — це хуки життєвого циклу компонента, які дають змогу
  реагувати на створення, оновлення та знищення елемента.

</details>

<details>
<summary>19. Що таке ViewEncapsulation в Angular і для чого воно використовується?</summary>

#### Angular

- ViewEncapsulation — це механізм інкапсуляції стилів у Angular, який визначає,
  як CSS компоненту впливає на DOM (чи лише на цей компонент, чи на весь
  застосунок).

| Тип інкапсуляції         | Опис                                                                          | Особливість                                     |
| ------------------------ | ----------------------------------------------------------------------------- | ----------------------------------------------- |
| **Emulated** _(default)_ | Angular імітує поведінку Shadow DOM, додаючи унікальні атрибути до елементів. | Стилі діють лише всередині цього компонента.    |
| **ShadowDom**            | Використовує нативний Shadow DOM браузера.                                    | Повна ізоляція стилів, немає витоку назовні.    |
| **None**                 | Без інкапсуляції.                                                             | Стилі поширюються глобально на весь застосунок. |

#### Приклад:

```TypeScript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  styleUrls: ['./example.component.css'],
  encapsulation: ViewEncapsulation.ShadowDom
})
export class ExampleComponent {}
```

**Коротко:**

- ViewEncapsulation контролює межі застосування CSS — чи стилі “ізольовані”
всередині компонента, чи поширюються глобально. У більшості випадків —
використовується Emulated.
</details>

<details>
<summary>20. Як застосовувати умовне (conditional) стилювання в Angular-компонентах?</summary>

#### Angular

- В Angular умовне стилювання реалізується через директиви прив’язки стилів та
  класів — `ngClass` і `ngStyle`.

| Метод                  | Приклад                                                                 | Опис                                                 |
| ---------------------- | ----------------------------------------------------------------------- | ---------------------------------------------------- |
| **[ngClass]**          | `<div [ngClass]="{ 'active': isActive, 'disabled': !isActive }"></div>` | Додає або забирає CSS-класи залежно від умови.       |
| **[ngStyle]**          | `<div [ngStyle]="{ 'color': isActive ? 'green' : 'red' }"></div>`       | Застосовує стилі напряму через об’єкт.               |
| **Класова прив’язка**  | `<div [class.active]="isActive"></div>`                                 | Додає клас, якщо умова `true`.                       |
| **Стильова прив’язка** | `<div [style.backgroundColor]="isActive ? 'blue' : 'gray'"></div>`      | Змінює конкретний CSS-властивість залежно від умови. |

**Коротко:**

- Використовуй `ngClass` для керування класами та `ngStyle` або `[style.prop]`
  для динамічних inline-стилів. Це дає повний контроль над виглядом елементів
  залежно від стану компонента.

</details>

<details>
<summary>21. У чому різниця між структурними та атрибутними директивами в Angular?</summary>

#### Angular

- Директиви в Angular бувають структурні та атрибутні, і вони впливають на DOM
  по-різному.

| Тип директиви               | Опис                                                           | Приклади                                                                        | Вплив на DOM                                                  |
| --------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **Структурна (Structural)** | Змінює **структуру DOM** — додає, видаляє або змінює елементи. | `*ngIf`, `*ngFor`, `*ngSwitchCase`                                              | Створює або прибирає елементи в дереві DOM.                   |
| **Атрибутна (Attribute)**   | Змінює **вигляд або поведінку** наявного елемента.             | `ngClass`, `ngStyle`, `ngModel`, кастомні директиви (наприклад, `appHighlight`) | Не змінює структуру DOM, лише властивості або стилі елемента. |

**Коротко:**

- Структурні директиви керують тим, що є в DOM, атрибутні директиви — тим, як це
  виглядає або поводиться.

</details>

<details>
<summary>22. Як створити власну структурну директиву в Angular?</summary>

#### Angular

- Структурна директива змінює DOM (додає або видаляє елементи). Щоб створити
  кастомну структурну директиву:

| Крок | Опис                                                                               |
| ---- | ---------------------------------------------------------------------------------- |
| 1    | Створити директиву з декоратором `@Directive` і `standalone: true`.                |
| 2    | Інжектити `TemplateRef` і `ViewContainerRef` для доступу до шаблону та контейнера. |
| 3    | Створити метод або сеттер, який вирішує, коли вставляти або видаляти шаблон.       |
| 4    | Використовувати директиву через `*yourDirective` у шаблоні.                        |

#### Приклад кастомної структурної директиви:

```TypeScript
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appUnless]',
  standalone: true
})
export class UnlessDirective {
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}

  @Input() set appUnless(condition: boolean) {
    this.viewContainer.clear();
    if (!condition) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    }
  }
}
```

#### Використання у шаблоні:

```html
<p *appUnless="isLoggedIn">You are not logged in!</p>
```

**Коротко:**

- Кастомна структурна директива керує DOM через `ViewContainerRef` і
  `TemplateRef`. Використовується з `*` синтаксисом у шаблоні.

</details>

<details>
<summary>23. Як зробити сервіс singleton в Angular?</summary>

#### Angular

- У Angular singleton-сервіс — це сервіс, який створюється лише один раз і
  використовується у всьому застосунку. Для цього потрібно вказати, де він
  надається (provided).

| Спосіб                                      | Приклад                                         | Пояснення                                                                                                     |
| ------------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **1. Через `providedIn: 'root'`**           | `@Injectable({ providedIn: 'root' })`           | Найпоширеніший спосіб. Сервіс реєструється в головному інжекторі, створюється один раз для всього застосунку. |
| **2. Через модуль (deprecated підхід)**     | Додати в `providers` масив модуля (`@NgModule`) | Використовується рідше. Сервіс буде singleton лише в межах цього модуля.                                      |
| **3. Через компонент (локальний інжектор)** | Додати в `providers` масив компонента           | Сервіс не буде singleton — створюється новий екземпляр для кожного компонента.                                |

#### Приклад:

```TypeScript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private token = '';
  setToken(t: string) { this.token = t; }
  getToken() { return this.token; }
}
```

**Коротко:**

- Найкраща практика — `@Injectable({ providedIn: 'root' })`, бо це гарантує
  singleton-поведінку і оптимізує tree-shaking.

</details>

<details>
<summary>24. Як використовувати Observables у сервісах для обміну даними між компонентами?</summary>

#### Angular

- Observables у сервісах дозволяють реактивно ділитися даними між компонентами —
  без прямої передачі через `@Input()` чи `@Output()`.

| Підхід              | Опис                                                                             | Типовий випадок використання                                 |
| ------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Subject**         | Дає змогу як передавати (`next()`), так і підписуватись (`subscribe()`) на дані. | Динамічне оновлення стану між компонентами.                  |
| **BehaviorSubject** | Зберігає останнє значення, яке автоматично отримують нові підписники.            | Поточний стан (наприклад, авторизація, вибраний користувач). |
| **ReplaySubject**   | Передає певну кількість останніх значень новим підписникам.                      | Історія подій або кешування даних.                           |

#### Приклад (через BehaviorSubject):

**data.service.ts**

```TypeScript
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({ providedIn: 'root' })
export class DataService {
  private messageSource = new BehaviorSubject<string>('Hello');
  message$ = this.messageSource.asObservable();

  updateMessage(newMsg: string) {
    this.messageSource.next(newMsg);
  }
}
```

**component-a.ts**

```TypeScript
@Component({...})
export class ComponentA {
  constructor(private dataService: DataService) {}
  sendMessage() {
    this.dataService.updateMessage('Message from A');
  }
}
```

**component-b.ts**

```TypeScript
@Component({...})
export class ComponentB {
  message = '';
  constructor(private dataService: DataService) {
    this.dataService.message$.subscribe(msg => this.message = msg);
  }
}
```

**Коротко:**

- Сервіс з `Subject` або `BehaviorSubject` діє як “shared data channel” — один
  компонент надсилає дані, інші підписуються. Це реактивний і чистий спосіб
  обміну станом між компонентами.

</details>

<details>
<summary>25. Які існують способи надання (provide) сервісу в Angular і чим вони відрізняються?</summary>

#### Angular

- У Angular є кілька способів оголосити, де і як створюється сервіс. Від цього
  залежить область його дії (scope) — чи він буде singleton, чи матиме локальний
  екземпляр.

| Спосіб                                           | Як реалізується                                    | Область дії                                                         | Коментар                                          |
| ------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------- |
| **1. `providedIn: 'root'`**                      | У декораторі `@Injectable({ providedIn: 'root' })` | Глобальна (один екземпляр у всьому застосунку)                      | ✅ Найкраща практика. Оптимізується tree-shaking. |
| **2. `providedIn: 'platform'`**                  | Через `@Injectable({ providedIn: 'platform' })`    | Спільний сервіс між кількома Angular застосунками на одній сторінці | Рідко використовується.                           |
| **3. `providedIn: 'any'`**                       | Через `@Injectable({ providedIn: 'any' })`         | Новий екземпляр для кожного lazy-loaded модуля                      | Корисно для ізольованих модулів.                  |
| **4. У `providers` масиві модуля (`@NgModule`)** | Додавання сервісу в `providers`                    | Тільки в межах цього модуля                                         | Використовується в legacy-проєктах.               |
| **5. У `providers` масиві компонента**           | `providers: [MyService]` у декораторі `@Component` | Новий екземпляр для кожного екземпляра компонента                   | Для локального стану або ізольованої логіки.      |

#### Приклад:

```TypeScript
@Injectable({
  providedIn: 'root'
})
export class UserService {}
```

**або**

```TypeScript
@Component({
  selector: 'app-profile',
  providers: [UserService]
})
export class ProfileComponent {}
```

**Коротко:**

- Найчастіше використовується `providedIn: 'root'` — це дає один спільний
  екземпляр (singleton). Інші способи — для lazy-loading, ізоляції або особливих
  випадків.

</details>

<details>
<summary>26. Поясни, що таке providedIn у сервісах Angular і яку роль воно відіграє?</summary>

#### Angular

- `providedIn` — це параметр у декораторі `@Injectable`, який визначає, де
  Angular має зареєструвати сервіс у DI (Dependency Injection) системі. Від
  нього залежить область дії (scope) сервісу та кількість створених екземплярів.

| Значення `providedIn`          | Опис                                                                | Область дії                                | Використання                               |
| ------------------------------ | ------------------------------------------------------------------- | ------------------------------------------ | ------------------------------------------ |
| `'root'`                       | Сервіс реєструється у головному інжекторі застосунку.               | Глобальна (singleton у всьому застосунку). | ✅ Найпоширеніший і рекомендований спосіб. |
| `'platform'`                   | Один інжектор для всієї платформи (кілька Angular app на сторінці). | Спільний між застосунками.                 | Рідкісний випадок використання.            |
| `'any'`                        | Кожен lazy-loaded модуль отримує власний екземпляр.                 | Локальна для модуля або компонента.        | Для незалежних частин застосунку.          |
| Клас або модуль (`SomeModule`) | Сервіс буде створено лише в межах цього модуля.                     | Локальна.                                  | Використовується для модульної ізоляції.   |

#### Приклад:

```TypeScript
@Injectable({
  providedIn: 'root'
})
export class LoggerService {
  log(message: string) {
    console.log(`[LOG]: ${message}`);
  }
}
```

**Коротко:**

- `providedIn` визначає, де саме Angular створює сервіс і чи буде він спільним
  (singleton). У більшості випадків використовують `providedIn: 'root'` — це
  просто, ефективно і підтримує tree-shaking.

</details>

<details>
<summary>27. Як у Angular використовувати HttpClient для обробки JSON-даних?</summary>

#### Angular

- `HttpClient` — це сервіс Angular для виконання HTTP-запитів. Він автоматично
  перетворює JSON-відповіді в об’єкти JavaScript, тому додаткового парсингу не
  потрібно.

| Крок | Опис                                                              |
| ---- | ----------------------------------------------------------------- |
| 1    | Імпортуй `HttpClientModule` у кореневий або standalone компонент. |
| 2    | Інжектуй `HttpClient` у сервіс або компонент.                     |
| 3    | Використовуй методи `get()`, `post()`, `put()`, `delete()` тощо.  |
| 4    | Angular автоматично обробляє JSON через RxJS `Observable`.        |

#### Приклад:

```TypeScript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

export interface User {
  id: number;
  name: string;
  email: string;
}

@Injectable({ providedIn: 'root' })
export class UserService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/users';

  constructor(private http: HttpClient) {}

  getUsers(): Observable<User[]> {
    return this.http.get<User[]>(this.apiUrl);
  }

  addUser(user: User): Observable<User> {
    return this.http.post<User>(this.apiUrl, user);
  }
}
```

**component.ts**

```TypeScript
@Component({...})
export class AppComponent {
  users$ = this.userService.getUsers();

  constructor(private userService: UserService) {}
}
```

#### Особливості:

- `HttpClient` автоматично парсить JSON у JS-об’єкти.

- Можна вказати generic тип (`<User[]>`), щоб отримати типізовану відповідь.

- Повертає Observable, тому можна застосовувати оператори RxJS (`map`,
  `catchError`, тощо).

**Коротко:**

- `HttpClient` — це зручний API для роботи з JSON у Angular. Він типізований,
  реактивний і не потребує ручного `JSON.parse()`.

</details>

<details>
<summary>28. Як обробляти REST API-запити та помилки у сервісах Angular?</summary>

#### Angular

- REST-запити в Angular виконуються через `HttpClient`, а обробка помилок —
  через RxJS оператор `catchError`. Усе це зазвичай інкапсулюється в окремому
  сервісі, щоб компоненти залишалися “чистими”.

| Крок | Опис                                                             |
| ---- | ---------------------------------------------------------------- |
| 1    | Створи сервіс (`@Injectable`) і підключи `HttpClient`.           |
| 2    | Використовуй методи `get()`, `post()`, `put()`, `delete()`.      |
| 3    | Обгорни запити у `pipe()` з `catchError()` для обробки помилок.  |
| 4    | Поверни типізований `Observable`, щоб компонент міг підписатися. |

#### Приклад:

```TypeScript
import { Injectable } from '@angular/core';
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { catchError, throwError, Observable } from 'rxjs';

export interface Product {
  id: number;
  name: string;
  price: number;
}

@Injectable({ providedIn: 'root' })
export class ProductService {
  private apiUrl = 'https://api.example.com/products';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<Product[]> {
    return this.http.get<Product[]>(this.apiUrl).pipe(
      catchError(this.handleError)
    );
  }

  addProduct(product: Product): Observable<Product> {
    return this.http.post<Product>(this.apiUrl, product).pipe(
      catchError(this.handleError)
    );
  }

  private handleError(error: HttpErrorResponse) {
    if (error.status === 0) {
      console.error('Network error:', error.error);
    } else {
      console.error(`API returned code ${error.status}:`, error.error);
    }
    return throwError(() => new Error('Something went wrong; please try again.'));
  }
}
```

#### Пояснення:

- `catchError()` — RxJS оператор для перехоплення помилок.

- `throwError()` — створює новий стрім з помилкою.

- Обробку логіки (`try again`, `notify user`, `log error`) краще робити
  всередині сервісу, не в компоненті.

**Коротко:**

- REST API виклики обробляються у сервісі через `HttpClient`. Для помилок
  використовуй `catchError()` у поєднанні з власним `handleError()` методом — це
  робить код чистим і передбачуваним.

</details>

<details>
<summary>29. Як налаштовується маршрутизація (routing) в Angular-застосунках?</summary>

#### Angular

- Routing в Angular визначає, який компонент відображається при переході на
  певний URL. Він налаштовується через масив маршрутів і RouterModule (або
  `provideRouter` для standalone API).

| Крок | Опис                                                                                            |
| ---- | ----------------------------------------------------------------------------------------------- |
| 1    | Створити масив маршрутів (`Routes[]`), де кожен об’єкт описує шлях і компонент.                 |
| 2    | Імпортувати `RouterModule.forRoot(routes)` або використати `provideRouter(routes)` у `main.ts`. |
| 3    | Додати `<router-outlet>` у шаблон, щоб рендерити активний маршрут.                              |
| 4    | Використовувати директиви `[routerLink]` для навігації.                                         |

#### Приклад (standalone routing):

**app.routes.ts**

```TypeScript
import { Routes } from '@angular/router';
import { HomeComponent } from './home.component';
import { AboutComponent } from './about.component';

export const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', redirectTo: '' } // catch-all
];
```

**main.ts**

```TypeScript
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter } from '@angular/router';
import { AppComponent } from './app.component';
import { routes } from './app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)]
});
```

**app.component.html**

```html
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>

<router-outlet></router-outlet>
```

#### Додаткові можливості:

- **Route Guards** (`canActivate`, `canDeactivate`) — для захисту маршрутів.

- **Lazy Loading** — динамічне підвантаження модулів або компонентів.

- **Route Parameters** (`:id`) — для передачі динамічних значень у маршруті.

**Коротко:**

Маршрутизація в Angular конфігурується через масив `Routes` і `RouterModule` або
provideRouter(). Компоненти рендеряться у `<router-outlet>`, а переходи
виконуються через `[routerLink]`.

</details>

<details>
<summary>30. Як у Angular створити маршрут, який динамічно завантажує модуль лише під час доступу до нього (lazy loading)?</summary>

#### Angular

- Так, у сучасному Angular (v16–20) це робиться через **_lazy loading_** з
  використанням динамічного `import()` у файлі маршрутизації. Це дозволяє не
  включати модуль у основний bundle, а завантажувати його лише при навігації.

#### Приклад:

```TypeScript
// app.routes.ts (Angular 17+ standalone API)
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: 'admin',
    loadChildren: () =>
      import('./admin/admin.routes').then(m => m.ADMIN_ROUTES),
  },
];
```

У випадку standalone-компонентів:

```TypeScript
{
  path: 'dashboard',
  loadComponent: () =>
    import('./dashboard/dashboard.component').then(c => c.DashboardComponent),
}
```

**Коротко:**

- `loadChildren` або `loadComponent` використовуються для lazy loading.
- Модуль/компонент завантажується лише при першому переході на відповідний
  маршрут.
- Це оптимізує стартову швидкість застосунку.

</details>

<details>
<summary>31. Що таке RouterOutlet в Angular і як його використовують?</summary>

#### Angular

- `<router-outlet>` — це директива, яка визначає місце у шаблоні, куди Angular
  підставляє компонент, що відповідає активному маршруту. Вона є “контейнером”
  для відображення контенту згідно з конфігурацією маршрутизатора.

#### Приклад:

```html
<!-- app.component.html -->
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>

<router-outlet></router-outlet>
```

```TypeScript
// app.routes.ts
import { Routes } from '@angular/router';
import { HomeComponent } from './home.component';
import { AboutComponent } from './about.component';

export const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
];
```

**Коротко:**

- `RouterOutlet` — точка вставки для компонентів маршруту.
- Підтримує вкладені маршрути (може бути кілька `router-outlet`).
- Без нього маршрути не відображаються у DOM.

</details>

<details>
<summary>32. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>33. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>34. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>35. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>36. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>37. ???</summary>

#### Angular

- Coming soon...😎

</details>
