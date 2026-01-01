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

```HTML
<p>{{ userName }}</p>
```

2. **Property binding** — передача значень у властивості
   DOM-елементів/компонентів:

```HTML
<img [src]="avatarUrl" />
```

3. **Event binding** — реакція на події DOM:

```HTML
<button (click)="onSave()">Save</button>
```

4. **Two-way binding** — синхронізація стану між шаблоном і компонентом
   ([(...)]):

```HTML
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

```HTML
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

Коротко: директиви в Angular = спосіб керувати DOM. Найчастіше — `@if`, `@for`,
`ngClass`, `ngStyle`, `ngModel`.

</details>

<details>
<summary>6. Як створити сервіс в Angular і навіщо його використовують?</summary>

#### Angular

Сервіс — це клас із бізнес-логікою або функціоналом, який не пов’язаний напряму
з UI.

#### Використовується для:

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

Dependency Injection (DI) — це механізм Angular, який автоматично створює та
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

#### Використання у компоненті:

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

В Angular події обробляються через event binding, тобто підписку на подію DOM
або кастомної події компонента.

#### Синтаксис:

```HTML
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

```HTML
<app-child (notify)="onNotify($event)"></app-child>
```

Коротко: в Angular події обробляються через `(eventName)="handler()"` для DOM та
через `@Output` + `EventEmitter` для кастомних подій.

</details>

<details>
<summary>10. Що таке двостороннє зв’язування (two-way binding) і як його реалізувати в Angular?</summary>

#### Angular

Двостороннє зв’язування — це синхронізація стану між компонентом і шаблоном,
коли зміни в UI автоматично оновлюють дані компонента і навпаки.

#### Класичний підхід (з ngModel):

```HTML
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

```HTML
<p highlight>Text with highlight</p>
```

Коротко: компонент = директива + шаблон, а директива = поведінка без власного
UI.

</details>

<details>
<summary>12. Що таке пайпи (Pipes) в Angular та де їх варто використовувати?</summary>

#### Angular

Pipe — це клас, який трансформує дані без зміни їхнього оригінального стану.
Використовується у шаблонах для форматування значень.

#### Приклади вбудованих пайпів:

- `date` → форматування дат

- `currency` → вивід валют

- `uppercase` / `lowercase` → зміна регістру

- `async` → робота з Promise / Observable

#### Приклад використання:

```HTML
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

```HTML
<p>{{ 'Hello' | exclaim }}</p>
<!-- Hello! -->
```

Коротко: Pipes потрібні для форматування та трансформації даних у шаблоні, щоб
не захаращувати логіку компонента.

</details>

<details>
<summary>13. Як обробляти надсилання форм (form submissions) в Angular?</summary>

#### Angular

В Angular є два основні підходи:

1. **Template-driven forms** (простий варіант, з `ngModel`):

```HTML
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

**Angular CLI** — це офіційний інструмент командного рядка для створення та
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

В Angular для роботи з HTTP використовується HttpClient, який надає методи get,
post, put, delete тощо.

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

Передача даних відбувається через input-зв’язування (@Input() декоратор).
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

Для передачі подій вгору використовується @Output() разом із EventEmitter.
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

Коротко: передача даних child → parent відбувається через @Output() і (event)
binding. Дитина емітить подію, батько слухає.

</details>

<details>
<summary>18. Які є життєві цикли (lifecycle hooks) компонентів в Angular і що вони означають?</summary>

#### Angular

Lifecycle hooks — це методи, які Angular викликає на різних етапах «життя»
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

Коротко: Lifecycle hooks — це хуки життєвого циклу компонента, які дають змогу
реагувати на створення, оновлення та знищення елемента.

</details>

<details>
<summary>19. Що таке ViewEncapsulation в Angular і для чого воно використовується?</summary>

#### Angular

ViewEncapsulation — це механізм інкапсуляції стилів у Angular, який визначає, як
CSS компоненту впливає на DOM (чи лише на цей компонент, чи на весь застосунок).

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
  templateUrl: './example.component.HTML',
  styleUrls: ['./example.component.css'],
  encapsulation: ViewEncapsulation.ShadowDom
})
export class ExampleComponent {}
```

**Коротко:**

ViewEncapsulation контролює межі застосування CSS — чи стилі “ізольовані”
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

Використовуй `ngClass` для керування класами та `ngStyle` або `[style.prop]` для
динамічних inline-стилів. Це дає повний контроль над виглядом елементів залежно
від стану компонента.

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

Структурні директиви керують тим, що є в DOM, атрибутні директиви — тим, як це
виглядає або поводиться.

</details>

<details>
<summary>22. Як створити власну структурну директиву в Angular?</summary>

#### Angular

Структурна директива змінює DOM (додає або видаляє елементи). Щоб створити
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

```HTML
<p *appUnless="isLoggedIn">You are not logged in!</p>
```

**Коротко:**

Кастомна структурна директива керує DOM через `ViewContainerRef` і
`TemplateRef`. Використовується з `*` синтаксисом у шаблоні.

</details>

<details>
<summary>23. Як зробити сервіс singleton в Angular?</summary>

#### Angular

У Angular singleton-сервіс — це сервіс, який створюється лише один раз і
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

Найкраща практика — `@Injectable({ providedIn: 'root' })`, бо це гарантує
singleton-поведінку і оптимізує tree-shaking.

</details>

<details>
<summary>24. Як використовувати Observables у сервісах для обміну даними між компонентами?</summary>

#### Angular

Observables у сервісах дозволяють реактивно ділитися даними між компонентами —
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

Сервіс з `Subject` або `BehaviorSubject` діє як “shared data channel” — один
компонент надсилає дані, інші підписуються. Це реактивний і чистий спосіб обміну
станом між компонентами.

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

Найчастіше використовується `providedIn: 'root'` — це дає один спільний
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

`providedIn` визначає, де саме Angular створює сервіс і чи буде він спільним
(singleton). У більшості випадків використовують `providedIn: 'root'` — це
просто, ефективно і підтримує tree-shaking.

</details>

<details>
<summary>27. Як у Angular використовувати HttpClient для обробки JSON-даних?</summary>

#### Angular

`HttpClient` — це сервіс Angular для виконання HTTP-запитів. Він автоматично
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

`HttpClient` — це зручний API для роботи з JSON у Angular. Він типізований,
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

Routing в Angular визначає, який компонент відображається при переході на певний
URL. Він налаштовується через масив маршрутів і RouterModule (або
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

**app.component.HTML**

```HTML
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

Так, у сучасному Angular (v16–20) це робиться через **_lazy loading_** з
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

```HTML
<!-- app.component.HTML -->
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
<summary>32. Як у Angular застосовуються route guards (захисники маршрутів)?</summary>

#### Angular

- Route guards — це сервіси, які контролюють доступ до маршрутів. Вони
  реалізують спеціальні інтерфейси (`CanActivate`, `CanDeactivate`, `CanLoad`,
  `CanMatch`, `Resolve`) і використовуються в конфігурації маршрутизатора.

#### Приклад (CanActivate):

```TypeScript
// auth.guard.ts
import { CanActivateFn } from '@angular/router';

export const authGuard: CanActivateFn = (route, state) => {
  const isLoggedIn = !!localStorage.getItem('token');
  return isLoggedIn; // або redirectUrl при потребі
};
```

```TypeScript
// app.routes.ts
export const routes = [
  {
    path: 'dashboard',
    canActivate: [authGuard],
    loadComponent: () =>
      import('./dashboard/dashboard.component').then(c => c.DashboardComponent),
  },
];
```

**Коротко:**

- Guards перевіряють, чи можна активувати, завантажити або покинути маршрут.
- Починаючи з Angular 15+, зручно використовувати функціональні guards
  (`CanActivateFn`) без класів.
- Повертають `true/false`, `UrlTree`, або `Observable/Promise`.

</details>

<details>
<summary>33. Для чого в Angular використовується ActivatedRoute у маршрутизації?</summary>

#### Angular

`ActivatedRoute` дає доступ до інформації про поточний активний маршрут, включно
з параметрами, query-параметрами, фрагментами URL і даними, переданими через
`data`. Використовується всередині компонентів для отримання контексту маршруту.

#### Приклад:

```TypeScript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user',
  template: `<p>User ID: {{ userId }}</p>`
})
export class UserComponent implements OnInit {
  userId!: string;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    // отримати параметр з URL
    this.userId = this.route.snapshot.paramMap.get('id')!;

    // або підписка на зміни параметрів
    this.route.paramMap.subscribe(params => {
      this.userId = params.get('id')!;
    });
  }
}
```

**Коротко:**

- `ActivatedRoute` — доступ до параметрів маршруту, query-параметрів, fragment і
  data.
- Потрібен для динамічного завантаження даних залежно від маршруту.
- Працює як зі snapshot, так і з Observable для реактивного оновлення.

</details>

<details>
<summary>34. Що таке параметри маршруту в Angular і як до них звертатися?</summary>

#### Angular

Параметри маршруту — це змінні частини URL, які визначаються у маршрутах та
дозволяють передавати дані у компонент.

#### Приклад:

```TypeScript
// app.routes.ts
import { Routes } from '@angular/router';
import { UserComponent } from './user.component';

export const routes: Routes = [
  { path: 'user/:id', component: UserComponent },
];
```

```TypeScript
// user.component.ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user',
  template: `<p>User ID: {{ userId }}</p>`
})
export class UserComponent implements OnInit {
  userId!: string;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    // Через snapshot (одноразово)
    this.userId = this.route.snapshot.paramMap.get('id')!;

    // Через Observable (реактивно при зміні маршруту)
    this.route.paramMap.subscribe(params => {
      this.userId = params.get('id')!;
    });
  }
}
```

**Коротко:**

- Route parameters — частина URL (наприклад, `/user/123` → `id = 123`).
- Доступ через `ActivatedRoute.snapshot.paramMap` або
  `ActivatedRoute.paramMap.subscribe()`.
- Використовуються для динамічного рендерингу контенту.

</details>

<details>
<summary>35. Як у Angular заздалегідь завантажити дані перед переходом на маршрут (resolve data)?</summary>

#### Angular

Для цього використовують **_Route Resolver_** — сервіс, який реалізує інтерфейс
`Resolve<T>`. Angular чекає, поки resolver отримає дані, і передає їх у
компонент через `ActivatedRoute.data`.

#### Приклад:

```TypeScript
// user.resolver.ts
import { Injectable } from '@angular/core';
import { Resolve } from '@angular/router';
import { UserService } from './user.service';

@Injectable({ providedIn: 'root' })
export class UserResolver implements Resolve<any> {
  constructor(private userService: UserService) {}

  resolve() {
    return this.userService.getUser(); // може повертати Observable або Promise
  }
}
```

```TypeScript
// app.routes.ts
import { Routes } from '@angular/router';
import { UserComponent } from './user.component';
import { UserResolver } from './user.resolver';

export const routes: Routes = [
  {
    path: 'user/:id',
    component: UserComponent,
    resolve: { userData: UserResolver }
  }
];
```

```TypeScript
// user.component.ts
ngOnInit() {
  this.route.data.subscribe(data => {
    console.log(data.userData); // доступ до preload-даних
  });
}
```

**Коротко:**

- Resolver завантажує дані перед активацією маршруту.
- Повертає `Observable`, `Promise` або просте значення.
- Дані доступні через `ActivatedRoute.data` у компоненті.

</details>

<details>
<summary>36. Як реалізувати lazy loading модулів або компонентів у Angular?</summary>

#### Angular

Lazy loading дозволяє завантажувати модулі чи компоненти тільки при переході на
відповідний маршрут, щоб зменшити початковий розмір bundle.

#### Приклад для модуля (loadChildren):

```TypeScript
// app.routes.ts
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: 'admin',
    loadChildren: () =>
      import('./admin/admin.module').then(m => m.AdminModule),
  },
];
```

#### Приклад для standalone-компонента (loadComponent):

```TypeScript
{
  path: 'dashboard',
  loadComponent: () =>
    import('./dashboard/dashboard.component').then(c => c.DashboardComponent),
}
```

**Коротко:**

- `loadChildren` — для lazy loading модулів.
- `loadComponent` — для lazy loading standalone-компонентів (Angular 15+).
- Підвищує швидкість старту додатку, завантажуючи код лише за потреби.

</details>

<details>
<summary>37. Поясни різницю між Template-driven та Reactive формами в Angular.</summary>

#### Angular

- **Template-driven форми** будуються переважно у HTML-шаблоні за допомогою
  директив (ngModel, ngForm). Вони простіші, підходять для невеликих форм, але
  менш контрольовані — логіка зосереджена у шаблоні.

- **Reactive форми** створюються в TypeScript-коді за допомогою FormGroup,
  FormControl, FormBuilder. Вони більш предиктивні, масштабовані й краще
  підходять для складних форм, валідації та тестування.

#### Приклад:

**Template-driven:**

```HTML
<form #form="ngForm">
  <input name="email" ngModel required />
</form>
```

**Reactive:**

```TypeScript
form = new FormGroup({
  email: new FormControl('', { nonNullable: true, validators: [Validators.required] })
});
```

```HTML
<form [formGroup]="form">
  <input formControlName="email" />
</form>
```

**Коротко:**

- Template-driven — декларативний підхід у шаблоні.
- Reactive — імперативний підхід у коді, з повним контролем над станом форми.

</details>

<details>
<summary>38. Як виконується валідація користувацького введення у формах Angular?</summary>

#### Angular

В Angular є вбудована, кастомна та асинхронна валідація. Валідація визначається
або через HTML-атрибути (у Template-driven формах), або через `Validators` у
Reactive формах.

**Reactive форма з валідацією:**

```TypeScript
form = new FormGroup({
  email: new FormControl('', {
    nonNullable: true,
    validators: [Validators.required, Validators.email]
  }),
  password: new FormControl('', {
    validators: [Validators.required, Validators.minLength(6)]
  })
});
```

**HTML:**

```HTML
<form [formGroup]="form">
  <input formControlName="email" />
  <div *ngIf="form.controls.email.invalid && form.controls.email.touched">
    Invalid email
  </div>
</form>
```

**Кастомний валідатор (приклад):**

```TypeScript
function forbiddenNameValidator(control: FormControl) {
  return control.value === 'admin' ? { forbiddenName: true } : null;
}
```

**Асинхронний валідатор (приклад):**

```TypeScript
function emailExistsValidator(service: UserService): AsyncValidatorFn {
  return control => service.checkEmail(control.value).pipe(
    map(exists => (exists ? { emailTaken: true } : null))
  );
}
```

**Коротко:**

- Використовуємо Validators (built-in або custom).
- Реактивний підхід дає більше контролю й гнучкості для відображення помилок та
  асинхронних перевірок.

</details>

<details>
<summary>39. Як динамічно додавати або видаляти елементи управління (form controls) у Reactive Forms в Angular?</summary>

#### Angular

- Для динамічної роботи з полями форми використовують `FormArray` або методи
  `addControl()` / `removeControl()` у `FormGroup`.
- Це дозволяє створювати або видаляти поля на льоту — наприклад, динамічні
  списки чи масиви інпутів.

**Приклад із FormArray:**

```TypeScript
form = new FormGroup({
  users: new FormArray<FormControl<string>>([])
});

get users() {
  return this.form.get('users') as FormArray;
}

addUser() {
  this.users.push(new FormControl('', Validators.required));
}

removeUser(index: number) {
  this.users.removeAt(index);
}
```

**HTML:**

```HTML
<form [formGroup]="form">
  <div formArrayName="users">
    <div *ngFor="let user of users.controls; let i = index">
      <input [formControlName]="i" />
      <button type="button" (click)="removeUser(i)">Remove</button>
    </div>
  </div>
  <button type="button" (click)="addUser()">Add User</button>
</form>
```

**Коротко:**

- Використовуй FormArray для списків контролів.
- Використовуй `addControl()` / `removeControl()` у `FormGroup` для динамічних
  окремих полів.

</details>

<details>
<summary>40. Що таке FormGroup у Angular і як він працює?</summary>

#### Angular

- `FormGroup` — це об’єкт, який об’єднує кілька `FormControl` або навіть інших
  `FormGroup` у єдину структуру. Він дозволяє керувати станом, значеннями та
  валідацією всієї групи як одного цілого.

**Ключові моменти:**

- `FormGroup` зберігає набір контролів у вигляді об’єкта.

- Дозволяє отримати стан (`valid`, `dirty`, `touched`) або значення (`value`)
  всієї групи.

- Може мати групову валідацію (на рівні всієї форми).

**Приклад:**

```TypeScript
form = new FormGroup({ user: new FormGroup({ name: new FormControl('',
Validators.required), email: new FormControl('', Validators.email) }) });
```

**HTML:**

```HTML
<form [formGroup]="form">
  <div formGroupName="user">
    <input formControlName="name" />
    <input formControlName="email" />
  </div>
</form>
```

**Коротко:**

- `FormGroup` = контейнер для контролів → дає змогу керувати групою полів як
  єдиним об’єктом (для валідації, оновлення, сабміту).

</details>

<details>
<summary>41. Як створити власні (custom) валідатори у формах Angular?</summary>

#### Angular

Кастомний валідатор — це функція, яка приймає `FormControl` або
`AbstractControl` і повертає об’єкт помилки `{ [key: string]: any }` або `null`,
якщо помилок немає. Її можна використовувати в Reactive Forms або
Template-driven.

**Синхронний валідатор (приклад):**

```TypeScript
import { AbstractControl, ValidationErrors } from '@angular/forms';

export function forbiddenWordValidator(control: AbstractControl):
ValidationErrors | null { const forbidden = control.value?.toLowerCase() ===
'admin'; return forbidden ? { forbiddenWord: true } : null; }
```

**Використання:**

```TypeScript
form = new FormGroup({ username: new FormControl('', [forbiddenWordValidator])
});
```

**Асинхронний валідатор (приклад):**

```TypeScript
export function uniqueEmailValidator(service: UserService) {
  return (control: AbstractControl) => {
    return service
      .checkEmail(control.value)
      .pipe(map(isTaken => (isTaken ? { emailTaken: true } : null)));
  };
}
```

**Коротко:**

- Кастомний валідатор — це функція, що повертає `{ errorKey: true }` або `null`.
- Може бути синхронним або асинхронним (через Observable).
- Підходить для складної бізнес-логіки, якої немає серед стандартних
  `Validators`.

</details>

<details>
<summary>42. Поясни, як використовувати formArrayName для роботи з полями форми типу масиву в Angular.</summary>

#### Angular

- `formArrayName` використовується в шаблоні для прив’язки до `FormArray`
  усередині Reactive Forms. Це дозволяє відображати та керувати динамічними
  наборами полів (наприклад, списком телефонів, тегів чи користувачів).

**Приклад:**

```TypeScript
form = new FormGroup({
  phones: new FormArray<FormControl<string>>([
    new FormControl('', Validators.required)
  ])
});

get phones() {
  return this.form.get('phones') as FormArray;
}

addPhone() {
  this.phones.push(new FormControl('', Validators.required));
}

removePhone(index: number) {
  this.phones.removeAt(index);
}
```

**HTML:**

```HTML
<form [formGroup]="form">
  <div formArrayName="phones">
    <div *ngFor="let phone of phones.controls; let i = index">
      <input [formControlName]="i" placeholder="Phone number" />
      <button type="button" (click)="removePhone(i)">Remove</button>
    </div>
  </div>

  <button type="button" (click)="addPhone()">Add Phone</button>
</form>
```

**Коротко:**

- `formArrayName` — це директива для доступу до `FormArray` у шаблоні.
- Кожен елемент масиву — окремий FormControl або FormGroup.
- Використовується для динамічних форм, де кількість полів може змінюватися.

</details>

<details>
<summary>43. Як відправити дані форми з Angular-додатку на бекенд-сервіс?</summary>

#### Angular

- У Angular форма зазвичай відправляється через сервіс, який використовує
  `HttpClient` для HTTP-запиту (`POST`, `PUT` тощо). Після сабміту зчитують
  `form.value`, перевіряють `form.valid` і викликають метод сервісу.

**Приклад:**

```TypeScript
// user.service.ts
@Injectable({ providedIn: 'root' })
export class UserService {
  constructor(private http: HttpClient) {}

  submitUser(data: any) {
    return this.http.post('/api/users', data);
  }
}
```

```TypeScript
// component.ts
form = new FormGroup({
  name: new FormControl('', Validators.required),
  email: new FormControl('', Validators.email)
});

constructor(private userService: UserService) {}

onSubmit() {
  if (this.form.valid) {
    this.userService.submitUser(this.form.value).subscribe({
      next: () => console.log('User saved!'),
      error: err => console.error('Error:', err)
    });
  }
}
```

**HTML:**

```HTML
<form [formGroup]="form" (ngSubmit)="onSubmit()">
  <input formControlName="name" />
  <input formControlName="email" />
  <button type="submit">Save</button>
</form>
```

**Коротко:**

- Отримуєш `form.value`.
- Перевіряєш `form.valid`.
- Відправляєш через `HttpClient` (звичайно через сервіс).
- Обробляєш відповідь у `subscribe()`.

</details>

<details>
<summary>44. Що таке виявлення змін (change detection) і як його реалізує Angular?</summary>

#### Angular

Виявлення змін (change detection) — це процес, за допомогою якого Angular
визначає, що дані в компоненті змінились, і оновлює відповідні частини UI.

**Як Angular це реалізує:**

- У сучасному Angular механізм базується на **_Signals_** — Angular відслідковує
  залежності між сигналами та шаблоном і оновлює тільки ті фрагменти DOM, які
  справді змінились (fine-grained reactivity, без глобального циклу).

- Без **_Signals_** Angular використовує **_Zone.js_**, який перехоплює
  async-події і запускає перевірку всього дерева компонентів.

- Для ручного контролю можливе використання `ChangeDetectorRef`.

**Коротко:**

Angular 20+ оновлює UI точково через Signals, а старий підхід (Zone.js +
глобальна перевірка) використовується лише для зворотної сумісності.

</details>

<details>
<summary>45. Які основні способи оптимізації продуктивності Angular-застосунку?</summary>

#### Angular

1. **Використання Signals**

Fine-grained reactivity → оновлюється тільки та частина DOM, яка залежить від
сигналу.

2. **Standalone Components**

Менший бандл, швидший старт, немає модульних оверхедів.

3. **Lazy loading та route-level code splitting**

Завантажувати лише той код, який потрібен на даному маршруті.

4. **OnPush (для legacy компонентів без сигналів)**

Зменшує кількість викликів change detection у старих компонентах.

5. **trackBy у ngFor**

Запобігає перерендеру списків:

```HTML
<li *ngFor="let item of items; trackBy: trackById"></li>
```

6. **Оптимізація RxJS**

takeUntil, shareReplay, уникання непотрібних сабскрипцій.

7. **Async Pipe замість manual subscribe**

Запобігає memory leaks і зайвим CD-циклами.

8. **Оптимізація шаблону**

Мінімізувати важкі обчислення у template (винести в getters або signals).

9. **Preloading strategies**

Оптимізує навігацію між маршрутами (наприклад, PreloadAllModules або custom).

10. **Build-level оптимізації**

ng build --configuration production

minification, treeshaking, локальні i18n-файли

image optimization (WebP/AVIF)

</details>

<details>
<summary>46. Що таке зони (Zones) в Angular і яку роль вони відіграють?</summary>

#### Angular

Зони (Zone.js) — це механізм, який перехоплює всі асинхронні операції (події,
таймери, проміси) і автоматично запускає change detection після їх виконання.

#### Навіщо Angular використовує зони:

Щоб не писати вручну, коли саме оновлювати UI.

Будь-який async виклик → Angular знає, що могли змінитися дані → оновлює вʼю.

#### Як це працює:

Zone.js патчить setTimeout, XHR, addEventListener тощо.

Після завершення async-дії зона викликає Angular change detection.

#### У сучасному Angular 16–20+:

Зони більше не потрібні для реактивного рендерингу (Signals).

Є режим Noop Zone / Zoneless, де Angular оновлює UI точково без глобального CD.

**Коротко:**

Zones — старий механізм для автозапуску change detection. У нових версіях
Angular його замінює сигнал-базована реактивність.

</details>

<details>
<summary>47. Як у Angular налаштувати SSR за допомогою Angular Universal</summary>

#### Angular

1. Увімкнення SSR

```bash
ng add @angular/ssr
```

Автоматично створюється сервер, SSR bootstrap і hydration.

2. Bootstrap

**Browser**

```TypeScript
bootstrapApplication(AppComponent, appConfig);
```

**Server**

```TypeScript
export default () =>
  bootstrapApplication(AppComponent, appConfig);
```

3. Hydration

```TypeScript
provideClientHydration()
```

Angular підхоплює HTML, а не рендерить заново.

4. Сервер (Node / Express)

```TypeScript
renderApplication(bootstrap, { url, document })
```

5. SSR-safe код

```TypeScript
isPlatformBrowser(PLATFORM_ID)
```

без window, document напряму

6. Дані

- API викликаємо **на сервері**

- Передаємо в браузер через `TransferState`

- Signals працюють з SSR без проблем

7. Коли використовувати

SEO, швидкий FCP

8. Коли не використовувати

Адмінки, real-time dashboards

</details>

<details>
<summary>48. У чому різниця між Ahead-of-Time (AOT) та Just-in-Time (JIT) компіляцією в Angular і коли використовується кожна з них?</summary>

#### Angular

#### AOT (Ahead-of-Time)

- Компіляція під час білду

- Angular-шаблони → JS до запуску в браузері

- Швидший старт

- Кращий performance

- Менший бандл

- Ранні compile-time помилки

- Безпека (немає runtime compiler)

**Default у production**

#### JIT (Just-in-Time)

- Компіляція в браузері під час виконання

- Потрібен Angular compiler у runtime

- Повільніший старт

- Більший бандл

- Зручно для dev (швидкий rebuild)

**Використовується в dev-режимі**

</details>

<details>
<summary>49. Опишіть декоратори, доступні в Angular.</summary>

#### Angular

Angular використовує TypeScript-декоратори для опису метаданих компонентів,
директив, сервісів та DI.

1. Класові декоратори

**@Component**

Описує UI-компонент.

```TypeScript
@Component({ selector: 'app-user', standalone: true, template: `{{ name }}` })
export class UserComponent { name = 'Viktor'; }
```

**@Directive**

Створює кастомну директиву (attribute або structural).

```TypeScript
@Directive({ selector: '[appHighlight]' }) export class HighlightDirective {}
```

**@Pipe**

Створює pipe для трансформації даних у шаблонах.

```TypeScript
@Pipe({ name: 'uppercase' }) export class UppercasePipe { transform(value:
string) { return value.toUpperCase(); } }
```

**@Injectable**

Позначає клас як сервіс для DI.

```TypeScript
@Injectable({ providedIn: 'root' }) export class UserService {}
```

2. Property decorators (взаємодія з шаблоном)

**@Input**

Передача даних у компонент.

```TypeScript
@Input() title!: string;
```

**@Output**

Передача подій з компонента.

```TypeScript
@Output() saved = new EventEmitter<void>();
```

**@HostBinding**

Байндінг до властивостей host-елемента.

```TypeScript
@HostBinding('class.active') isActive = true;
```

**@HostListener**

Підписка на події host-елемента.

```TypeScript
@HostListener('click') onClick() {}
```

3. Dependency Injection decorators

**@Inject**

Явна інʼєкція залежності.

```TypeScript
constructor(@Inject(API_URL) private apiUrl: string) {}
```

**@Optional**

Залежність може бути відсутня.

```TypeScript
constructor(@Optional() private logger?: LoggerService) {}
```

**@Self**, **@SkipSelf**

Контроль області пошуку залежностей.

```TypeScript
constructor(@Self() private control: NgControl) {}
```

4. View / Content decorators

**@ViewChild** / **@ViewChildren**

Доступ до елементів власного шаблону.

```TypeScript
@ViewChild('input') input!: ElementRef;
```

**@ContentChild** / **@ContentChildren**

Доступ до проєктованого контенту (ng-content).

```TypeScript
@ContentChild(TemplateRef) tpl!: TemplateRef<any>;
```

5. Стан у Angular 20+

- Декоратори **все ще підтримуються**

- Але часто замінюються:

  - `inject()` замість constructor DI

  - Signals замість `@Input` + `ngOnChanges`

- **Standalone API не скасовує декоратори**, лише спрощує архітектуру

</details>

<details>
<summary>50. Як реалізувати анімаційні переходи в Angular-додатку?</summary>

#### Angular

Angular має вбудовану систему анімацій через `@angular/animations`. У Angular
20+ використовую `provideAnimations()` у конфігурації:

```TypeScript
// app.config.ts
import { provideAnimations } from '@angular/platform-browser/animations';

export const appConfig: ApplicationConfig = {
  providers: [provideAnimations()]
};
```

1. Анімація станів компонента

```TypeScript
typescriptimport { trigger, state, style, transition, animate } from '@angular/animations';

@Component({
  template: `<div [@openClose]="isOpen()">Content</div>`,
  animations: [
    trigger('openClose', [
      state('true', style({ height: '200px', opacity: 1 })),
      state('false', style({ height: '0px', opacity: 0 })),
      transition('false <=> true', animate('300ms ease-in-out'))
    ])
  ]
})
export class MyComponent {
  isOpen = signal(false);
}
```

2. Анімація роутів

```TypeScript
// app.component.ts
@Component({
  template: `
    <div [@routeAnimations]="outlet.activatedRouteData['animation']">
      <router-outlet #outlet="outlet"></router-outlet>
    </div>
  `,
  animations: [
    trigger('routeAnimations', [
      transition('* <=> *', [
        query(':enter', [style({ opacity: 0 })], { optional: true }),
        query(':leave', [animate('200ms', style({ opacity: 0 }))], { optional: true }),
        query(':enter', [animate('300ms', style({ opacity: 1 }))], { optional: true })
      ])
    ])
  ]
})
```

3. Анімація списків (stagger)

```TypeScript
animations: [
  trigger('listAnimation', [
    transition('* => *', [
      query(':enter', [
        style({ opacity: 0, transform: 'translateY(-20px)' }),
        stagger(100, [
          animate('300ms', style({ opacity: 1, transform: 'translateY(0)' }))
        ])
      ], { optional: true })
    ])
  ])
]
```

#### Best Practices

- Використовую `transform` та `opacity` для GPU-acceleration
- `:enter` / `:leave` для появи/зникнення елементів
- Створюю reusable анімації через `animation()` та `useAnimation()`
- Відстежую події: `(@trigger.done)="onAnimationDone($event)"`

</details>

<details>
<summary>51. Як створюються власні директиви в Angular?</summary>

#### Angular

1. Типи директив

- **Attribute directive** — змінює поведінку або вигляд елемента приклад:
  highlight, tooltip

- **Structural directive** — змінює структуру DOM приклад: *ngIf, *ngFor

2. Attribute directive

**Приклад: директива підсвічування**

```TypeScript
import { Directive, ElementRef, Input, effect, signal } from '@angular/core';

@Directive({
  selector: '[appHighlight]',
  standalone: true,
})
export class HighlightDirective {
  color = signal('yellow');

  constructor(private el: ElementRef) {
    effect(() => {
      this.el.nativeElement.style.backgroundColor = this.color();
    });
  }

  @Input()
  set appHighlight(value: string) {
    this.color.set(value);
  }
}
```

**Використання**

```HTML
<p appHighlight="lightblue">Highlighted text</p>
```

3. Structural directive

**Приклад: кастомний `*appIf`**

```TypeScript
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appIf]',
  standalone: true,
})
export class AppIfDirective {
  constructor(
    private tpl: TemplateRef<unknown>,
    private vcr: ViewContainerRef
  ) {}

  @Input()
  set appIf(condition: boolean) {
    this.vcr.clear();
    if (condition) {
      this.vcr.createEmbeddedView(this.tpl);
    }
  }
}
```

**Використання**

```HTML
<div *appIf="isVisible">Visible content</div>
```

4. Best practices

- Використовуйте standalone директиви

- Для реактивності — signals + effect

- Уникайте прямої роботи з DOM (краще Renderer2, якщо потрібно)

- Мінімізуйте side-effects у constructor

- Structural директиви завжди працюють через TemplateRef + ViewContainerRef

**Коротко**

Власні директиви створюються через @Directive, бувають attribute та structural і
в Angular 20+ зазвичай є standalone з реактивністю на signals.

</details>

<details>
<summary>52. Чи можете ви пояснити використання директив ngClass та ngStyle?</summary>

#### Angular

Використання директив `ngClass` та `ngStyle` в Angular

#### `ngClass`

Директива `ngClass` використовується для **динамічного додавання або видалення
CSS-класів** на елементі.

#### Основні форми використання

1. Обʼєкт (найпоширеніше)

```HTML
<div [ngClass]="{ active: isActive, disabled: isDisabled }"></div>
```

2. Масив

```HTML
<div [ngClass]="['card', isDark ? 'dark' : 'light']"></div>
```

3. Рядок

```HTML
<div [ngClass]="dynamicClass"></div>
```

#### Best practices

- Використовуйте для умовної стилізації

- Працює ефективно з `ChangeDetectionStrategy.OnPush`

- Добре поєднується з signals

```TypeScript
isActive = signal(true);
```

#### `ngStyle`

Директива `ngStyle` використовується для динамічного задання inline-стилів.

#### Приклад

```HTML
<div [ngStyle]="{ color: textColor, fontSize: fontSize + 'px' }"></div>
```

```TypeScript
textColor = 'red';
fontSize = 16;
```

#### Best practices

- Використовуйте лише коли стилі не можна описати класами

- Уникайте великої кількості inline-стилів (performance + maintainability)

#### Angular 20+ рекомендації

- Віддавайте перевагу `ngClass`

- Для складної логіки — computed signals

- Для дизайн-систем — класи + CSS variables

#### Коротке резюме

- `ngClass` — для керування CSS-класами,
- `ngStyle` — для динамічних inline-стилів.

</details>

<details>
<summary>53. Як ви взаємодієте з DOM безпосередньо за допомогою директив?</summary>

#### Angular

Взаємодія з DOM за допомогою директив в Angular

#### Основні способи

1. `ElementRef` (обмежено)

Дає доступ до нативного DOM-елемента.

```TypeScript
constructor(private el: ElementRef) {
  this.el.nativeElement.focus();
}
```

**Недолік:** прямий доступ до DOM Не рекомендовано для SSR та безпеки

2. Renderer2 (рекомендовано)

Абстракція над DOM — безпечна та SSR-friendly.

```TypeScript
constructor(
  private el: ElementRef,
  private renderer: Renderer2
) {}

ngOnInit() {
  this.renderer.setStyle(
    this.el.nativeElement,
    'background-color',
    'yellow'
  );
}
```

- Працює з SSR
- Безпечний (XSS)
- Кросплатформений

3. @HostBinding Біндінг до властивостей host-елемента.

```TypeScript
@HostBinding('class.active') isActive = true;
```

- Чисто
- Без прямого DOM-доступу

4. @HostListener

Підписка на події host-елемента.

```TypeScript
@HostListener('mouseenter')
onHover() {
  this.isActive = true;
}
```

#### Angular 20+ підхід (best practice)

- Уникати nativeElement напряму

- Використовувати Renderer2

- Для стилів і класів — @HostBinding

- Для подій — @HostListener

- Для реактивності — signals + effect

- Перевіряти платформу (isPlatformBrowser) при роботі з DOM API

**Коротко**

У Angular взаємодія з DOM у директивах має відбуватись через Renderer2 або
host-декоратори, а не через прямий доступ до nativeElement.

</details>

<details>
<summary>54. Коли слід використовувати Renderer2 і які його переваги?</summary>

#### Angular

Коли слід використовувати `Renderer2` і які його переваги

#### Коли використовувати `Renderer2`

Використовуйте `Renderer2`, коли потрібно:

- Динамічно змінювати **стилі**, **класи**, **атрибути**
- Додавати або видаляти **DOM-елементи**
- Працювати з **подіями** зсередини директив
- Забезпечити **SSR-сумісність**
- Уникнути **XSS-ризиків**
- Писати **кросплатформений** код (browser / server / web workers)

## Приклад використання

```TypeScript
import { Directive, ElementRef, Renderer2 } from '@angular/core';

@Directive({
  selector: '[appHighlight]',
  standalone: true,
})
export class HighlightDirective {
  constructor(
    private el: ElementRef,
    private renderer: Renderer2
  ) {
    this.renderer.setStyle(
      this.el.nativeElement,
      'background-color',
      'yellow'
    );
  }
}
```

#### Переваги `Renderer2`

1. Безпека

- Захищає від XSS
- Не дозволяє небезпечні DOM-операції напряму

2. SSR-friendly

- Працює коректно при Server-Side Rendering
- Не ламається через відсутність window / document

3. Абстракція над DOM

- Angular вирішує як саме застосувати зміни
- Підтримує різні платформи

4. Краща підтримка Angular lifecycle

- Інтегрується з change detection
- Менше побічних ефектів

#### Коли НЕ варто використовувати `Renderer2`

- Для простого керування класами → краще ngClass
- Для обробки подій → краще @HostListener
- Для стилів → @HostBinding
- Для читання значень (read-only) → допустимо ElementRef

#### Angular 20+ рекомендації

- Не використовувати nativeElement напряму
- Renderer2 — стандарт для директив
- Поєднувати з signals для реактивності
- Перевіряти платформу при складних DOM-операціях

**Коротко**

Renderer2 — це безпечний, SSR-сумісний та кросплатформений спосіб взаємодії з
DOM, який слід використовувати замість прямого доступу до nativeElement.

</details>

<details>
<summary>55. Як створити власний канал в Angular?</summary>

#### Angular

Як створити власний Pipe (канал) в Angular

1. Створення pipe

Приклад: простий pipe для форматування імені

```TypeScript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'capitalize',
  standalone: true,
})
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    if (!value) return '';
    return value[0].toUpperCase() + value.slice(1);
  }
}
```

2. Використання в шаблоні

```HTML
<p>{{ 'angular' | capitalize }}</p>
```

3. Pure vs Impure pipes

**Pure pipe (за замовчуванням)**

- Викликається лише при зміні input

- Краща продуктивність

```TypeScript
@Pipe({ name: 'myPipe', pure: true })
```

**Impure pipe**

- Викликається на кожен change detection

- Використовувати обережно

```TypeScript
@Pipe({ name: 'myPipe', pure: false })
```

4. Pipe з параметрами

```TypeScript
@Pipe({ name: 'truncate', standalone: true })
export class TruncatePipe implements PipeTransform {
  transform(value: string, limit = 10): string {
    return value.length > limit ? value.slice(0, limit) + '…' : value;
  }
}
```

```HTML
<p>{{ text | truncate:20 }}</p>
```

5. Best practices (Angular 20+)

- Використовуйте standalone pipes

- Тримайте pipes pure

- Без side-effects

- Не використовуйте pipes для складної бізнес-логіки

- Для реактивних сценаріїв — signals або computed values

**Коротко**

Pipe в Angular створюється через @Pipe, реалізує PipeTransform і
використовується для декларативної трансформації даних у шаблоні.

</details>

<details>
<summary>56. Опишіть чисті та нечисті канали.</summary>

#### Angular

Чисті (Pure) та нечисті (Impure) канали в Angular

#### Чисті канали (Pure Pipes)

#### Характеристики

- Викликаються **лише тоді**, коли змінюється **посилання на input**
- Значення кешується Angular
- Висока продуктивність
- Повністю детерміновані (без side-effects)

```TypeScript
@Pipe({
  name: 'uppercase',
  standalone: true,
  pure: true, // default
})
export class UppercasePipe {}
```

#### Приклад використання

```HTML
<p>{{ name | uppercase }}</p>
```

#### Коли використовувати

- Форматування рядків

- Обчислення на основі immutable-даних

- 99% кейсів

#### Нечисті канали (Impure Pipes)

#### Характеристики

- Викликаються на кожен цикл change detection
- Не кешуються
- Значно гірша продуктивність
- Можуть мати side-effects (небажано)

```TypeScript
Копіювати код
@Pipe({
  name: 'timeAgo',
  standalone: true,
  pure: false,
})
export class TimeAgoPipe {}
```

#### Приклад використання

```HTML
<p>{{ timestamp | timeAgo }}</p>
```

#### Angular 20+ рекомендації

- Завжди починайте з pure pipe

- Уникайте impure pipes

- Для реактивних сценаріїв:

  - Signals (`computed`)

  - RxJS + `async`

- Impure pipe — останній варіант

**Коротко**

Pure pipes — швидкі та безпечні, Impure pipes — повільні й використовуються лише
у виняткових випадках.

</details>

<details>
<summary>57. Що таке асинхронний канал і як він використовується?</summary>

#### Angular

Асинхронний канал (`AsyncPipe`) в Angular

#### Що таке `async` pipe

`async` — це **вбудований Angular pipe**, який:

- підписується на `Observable` або `Promise`
- автоматично оновлює шаблон при нових значеннях
- **сам відписується** при знищенні компонента

#### Приклад з `Observable`

```TypeScript
users$ = this.userService.getUsers();
```

```HTML
<ul>
  <li *ngFor="let user of users$ | async">
    {{ user.name }}
  </li>
</ul>
```

#### Приклад з Promise

```TypeScript
dataPromise = fetchData();
```

```HTML
<p>{{ dataPromise | async }}</p>
```

#### Як працює під капотом

- Підписується на джерело даних
- Тригерить change detection при нових значеннях
- Відписується автоматично при destroy компонента

Усунення memory leaks без ngOnDestroy

#### Переваги async pipe

- Менше коду
- Немає ручних subscribe / unsubscribe
- Краще читається шаблон
- Ідеально працює з OnPush
- SSR та signals-friendly

#### async pipe + signals (Angular 20+)

```TypeScript
import { toSignal } from
'@angular/core/rxjs-interop';

users = toSignal(this.userService.getUsers()); html Копіювати код
```

```HTML
<li *ngFor="let user of users()">
```

#### Коли використовувати

- Для роботи з HTTP-запитами
- Для стрімів даних (RxJS)
- Для реактивних UI-станів

#### Коли НЕ використовувати

- Якщо значення потрібне лише в TS, а не в шаблоні
- Для складної бізнес-логіки (краще в сервісах)

**Коротко**

async pipe — стандартний і безпечний спосіб роботи з асинхронними даними в
шаблонах Angular без memory leaks.

</details>

<details>
<summary>58. Що таке NgRx і як він допомагає в управлінні станом?</summary>

#### Angular

Що таке NgRx і як він допомагає в управлінні станом

#### Що таке NgRx

**NgRx** — це бібліотека для **state management** в Angular, побудована на:

- патерні **Redux**
- **RxJS**
- односпрямованому потоці даних (unidirectional data flow)

NgRx забезпечує **єдине джерело правди (single source of truth)** для стану
застосунку.

#### Основні складові NgRx

1. Store

Глобальний immutable-стан застосунку.

```TypeScript
export interface AppState {
  users: User[];
}
```

2. Actions

Описують що сталося.

```TypeScript
export const loadUsers = createAction('[Users] Load');
```

3. Reducers

Описують як змінюється стан.

```TypeScript
export const usersReducer = createReducer( [],
on(loadUsersSuccess, (\_, { users }) => users) );
```

4. Selectors

Ефективне отримання даних зі store.

```TypeScript
export const selectUsers = createSelector( selectUsersState,
users => users );
```

5. Effects

Робота з side-effects (HTTP, storage, navigation).

```TypeScript
loadUsers$ = createEffect(() => this.actions$.pipe(
ofType(loadUsers), switchMap(() => this.api.getUsers()) ) );
```

#### Як NgRx допомагає керувати станом

- Централізує стан
- Робить змінюваність передбачуваною
- Полегшує debugging (Redux DevTools)
- Спрощує тестування
- Добре масштабується для великих команд

#### Коли використовувати NgRx

- Великі застосунки
- Складний shared-state
- Багато асинхронних side-effects
- Потрібен time-travel debugging

#### Коли НЕ використовувати NgRx

- Маленькі застосунки
- Простий локальний стан
- Overhead без потреби

#### Angular 20+ контекст

- NgRx не замінює signals

- Часто комбінується:

  - NgRx Store → глобальний стан

  - Signals → локальний UI-стан

- Для простіших кейсів:

  - Signals

  - Component Store

  - Services + RxJS

**Коротко**

NgRx — це потужний, але важкий інструмент для управління станом, який варто
використовувати лише тоді, коли складність застосунку цього вимагає.

</details>

<details>
<summary>59. Поясніть концепції дій, редукторів та ефектів у NgRx.</summary>

#### Angular

Дії, редуктори та ефекти в NgRx

1. Actions (Дії)

**Actions** описують **що сталося** в застосунку.  
Це прості обʼєкти з обовʼязковим полем `type`.

```TypeScript
export const loadUsers = createAction('[Users] Load');
export const loadUsersSuccess = createAction(
  '[Users] Load Success',
  props<{ users: User[] }>()
);
```

####Призначення

- Тригерять зміну стану
- Сигналізують про події (UI, API, router)

2. Reducers (Редуктори)

Reducers — чисті функції, які визначають як змінюється стан у відповідь на
action.

```TypeScript
export const usersReducer = createReducer( initialState,
on(loadUsersSuccess, (state, { users }) => ({ ...state, users, })) );
```

#### Ключові правила

- Без side-effects
- Без мутацій
- Повертають новий immutable-стан

3. Effects (Ефекти)

Effects обробляють side-effects (HTTP, storage, navigation) і працюють поза
reducer.

```TypeScript
loadUsers$ = createEffect(() => this.actions$.pipe(
ofType(loadUsers), switchMap(() => this.api.getUsers().pipe( map(users =>
loadUsersSuccess({ users })) ) ) ) );
```

#### Призначення

- Асинхронні операції
- Взаємодія з зовнішніми API
- Dispatch нових actions

#### Angular 20+ рекомендації

- Reducers — максимально прості
- Вся асинхронність — тільки в Effects
- Signals можна використовувати поверх select
- Для локального стану — ComponentStore

**Коротко**

**Actions** описують події, **Reducers** — змінюють стан, **Effects** —
обробляють побічні ефекти, разом утворюючи передбачуваний односпрямований потік
даних.

</details>

<details>
<summary>60. Як би ви зберігали стан програми після оновлення сторінки?</summary>

#### Angular

Основний підхід: Persist + Rehydrate

#### Зберігати стан у browser storage

- `localStorage` — довготривалий стан
- `sessionStorage` — лише на сесію
- `IndexedDB` — великі обʼєми даних

#### Варіант 1: NgRx + Meta-Reducers (рекомендовано)

Persist + Rehydrate через `ngrx-store-localstorage`

```TypeScript
import { localStorageSync } from 'ngrx-store-localstorage';

export const metaReducer: MetaReducer = reducer =>
  localStorageSync({
    keys: ['auth', 'settings'],
    rehydrate: true,
  })(reducer);
```

- Автоматичне відновлення
- Контроль, які slice зберігати
- Production-ready

#### Варіант 2: NgRx вручну (simple case)

```TypeScript
const savedState = JSON.parse(localStorage.getItem('appState') || '{}');
```

```TypeScript
StoreModule.forRoot(reducers, {
  initialState: savedState,
});
```

#### Варіант 3: Без NgRx (Signals + Service)

```TypeScript
@Injectable({ providedIn: 'root' })
export class AppStateService {
  theme = signal(
    localStorage.getItem('theme') ?? 'light'
  );

  constructor() {
    effect(() => {
      localStorage.setItem('theme', this.theme());
    });
  }
}
```

- Мінімальний оверхед
- Підходить для невеликого стану

#### Що зберігати / не зберігати

**Зберігати**

- Auth / refresh tokens
- User preferences
- Filters, feature state

**Не зберігати**

- Derived / computed state
- Тимчасовий UI-стан
- Великі API-колекції

#### Angular 20+ best practices

- Persist тільки потрібні slices
- Не зберігати sensitive data без шифрування
- Для SSR — використовувати isPlatformBrowser
- Signals — для локального стану
- NgRx — для глобального

**Коротко**

Я зберігаю стан через persisting у browser storage та rehydration при старті,
використовуючи NgRx meta-reducers або signals + services залежно від складності
застосунку.

</details>

<details>
<summary>61. Чи можете ви обговорити концепцію незмінності в управлінні станами?</summary>

#### Angular

Концепція незмінності (Immutability) в управлінні станами

#### Що таке незмінність

**Незмінність** означає, що стан **не змінюється напряму**.  
Кожна зміна створює **новий обʼєкт стану**, а старий залишається незмінним.

```TypeScript
// Мутація
state.count++;

// Незмінно
{ ...state, count: state.count + 1 }
```

#### Чому це важливо

1. **Передбачуваність**

- Один action → один новий стан
- Без прихованих побічних ефектів

2. **Продуктивність**

- Angular використовує reference checks
- Ефективна робота з OnPush та signals

3. **Debugging**

- Time-travel debugging (NgRx DevTools)
- Легко відстежувати зміни стану

4. **Тестування**

- Reducers — чисті функції
- Просте unit-тестування

#### Незмінність у NgRx

```TypeScript
on(updateUser, (state, { user }) => ({
  ...state,
  user: { ...state.user, ...user }
}))
```

Заборонено:

```TypeScript
state.user.name = user.name;
```

#### Angular 20+ контекст

- Signals реагують на зміну посилань
- computed() перевиконується лише при новому reference
- Immutability = краща продуктивність UI

#### Типові помилки

- Мутація вкладених обʼєктів
- Використання .push() / .splice()
- Зміни state поза reducer / сервісом

**Коротко**

Незмінність — основа надійного state management: вона забезпечує
передбачуваність, продуктивність і зручне тестування.

</details>

<details>
<summary>62. Як тестувати компоненти Angular?</summary>

#### Angular

Основні типи тестування

1. Unit-тести (основні)

Тестують **ізольовану логіку компонента**.

**Інструменти:**

- `TestBed`
- Jasmine / Jest
- Karma (або Vite + Vitest)

```TypeScript
beforeEach(() => {
  TestBed.configureTestingModule({
    imports: [MyComponent], // standalone
  });
});

it('should create component', () => {
  const fixture = TestBed.createComponent(MyComponent);
  expect(fixture.componentInstance).toBeTruthy();
});
```

2. Тестування шаблону (DOM)

Перевірка рендерингу та binding’ів.

```TypeScript
it('should render title', () => {
  const fixture = TestBed.createComponent(MyComponent);
  fixture.componentInstance.title = 'Hello';
  fixture.detectChanges();

  const el = fixture.nativeElement.querySelector('h1');
  expect(el.textContent).toContain('Hello');
});
```

3. Тестування взаємодії (events)

```TypeScript
it('should emit event on click', () => {
  spyOn(component.saved, 'emit');

  const button = fixture.nativeElement.querySelector('button');
  button.click();

  expect(component.saved.emit).toHaveBeenCalled();
});
```

#### Mock залежностей

**Mock сервісів**

```TypeScript
providers: [
  { provide: UserService, useValue: mockUserService }
]
```

**HttpClient**

```TypeScript
import { provideHttpClientTesting } from '@angular/common/http/testing';

providers: [provideHttpClientTesting()]
```

#### Signals у тестах (Angular 20+)

```TypeScript
it('should update signal value', () => {
  component.count.set(1);
  expect(component.count()).toBe(1);
});
```

#### Що тестувати, а що ні

**Тестувати**

- Бізнес-логіку компонента
- Взаємодію з сервісами
- Binding’и та events

**Не тестувати**

- Внутрішню реалізацію Angular
- CSS / стилі
- Простий boilerplate

**Best practices**

- Використовуйте standalone components у тестах
- Мінімізуйте TestBed конфіг
- Mock тільки зовнішні залежності
- Один тест — одна відповідальність
- Для UI-флоу — e2e (Cypress / Playwright)

**Коротко**

Компоненти Angular тестуються переважно unit-тестами через TestBed, з моками
залежностей та перевіркою DOM і взаємодій; у Angular 20+ тести простіші завдяки
standalone та signals.

</details>

<details>
<summary>63. Поясніть, що таке TestBed та його роль у тестуванні Angular.</summary>

#### Angular

#### Що таке TestBed

**TestBed** — це **основний тестовий API Angular**, який:

- створює **ізольоване тестове середовище**
- емулює Angular **DI, change detection та lifecycle**
- дозволяє конфігурувати залежності так само, як у реальному застосунку

#### Основні можливості TestBed

1. Конфігурація тестового модуля

```TypeScript
TestBed.configureTestingModule({
  imports: [MyComponent], // standalone
  providers: [MyService],
});
```

2. Створення компонента

```TypeScript
const fixture = TestBed.createComponent(MyComponent);
const component = fixture.componentInstance;
```

3. Керування change detection

```TypeScript
fixture.detectChanges();
```

4. Доступ до DI

```TypeScript
const service = TestBed.inject(MyService);
```

#### TestBed у Angular 20+

- Підтримує standalone components
- Не потребує NgModule
- Працює з signals
- Сумісний з SSR і zoneless режимом
- Менше boilerplate, ніж у старих версіях

#### Коли використовувати TestBed

**Використовувати**

- Для тестування компонентів
- Для інтеграційних unit-тестів
- Коли потрібні DI та lifecycle

**Не обовʼязково**

- Для простих pure-функцій
- Для логіки без Angular-залежностей

#### Best practices

- Мінімізуйте конфігурацію TestBed
- Імпортуйте лише тестований standalone-компонент
- Mock зовнішні залежності
- Не тестуйте Angular internals

**Коротко**

TestBed — це тестовий інструмент Angular, який створює середовище, максимально
наближене до реального застосунку, і є основою тестування компонентів та
сервісів.

</details>

<details>
<summary>64. Як ви створюєте імітаційний імітаційний код сервісу Angular для цілей тестування?</summary>

#### Angular

#### Навіщо потрібні mock-сервіси

- Ізолювати тест від реальних залежностей (HTTP, storage, API)
- Зробити тести **швидкими та детермінованими**
- Тестувати **поведінку**, а не реалізацію

#### Основні способи створення mock-сервісів

1. Простий mock-обʼєкт (найчастіше)

```TypeScript
const userServiceMock = {
  getUsers: () => of([{ id: 1, name: 'Test User' }]),
};
```

```TypeScript
TestBed.configureTestingModule({
  imports: [MyComponent],
  providers: [
    { provide: UserService, useValue: userServiceMock },
  ],
});
```

- Просто
- Швидко
- Ідеально для unit-тестів

2. Mock-клас

```TypeScript
class UserServiceMock {
  getUsers() {
    return of([]);
  }
}
```

```TypeScript
providers: [
  { provide: UserService, useClass: UserServiceMock }
]
```

- Краще для складної логіки
- Більше boilerplate

3. Spy-обʼєкти (Jasmine / Jest)

**Jasmine**

```TypeScript
const userServiceSpy = jasmine.createSpyObj('UserService', ['getUsers']);
userServiceSpy.getUsers.and.returnValue(of([]));
```

**Jest**

```TypeScript
const userServiceMock = {
  getUsers: jest.fn().mockReturnValue(of([])),
};
```

- Перевірка викликів
- Контроль поведінки

4. HttpClient mock (для API)

```TypeScript
import { provideHttpClientTesting } from '@angular/common/http/testing';

TestBed.configureTestingModule({
  providers: [provideHttpClientTesting()],
});
```

```TypeScript
httpMock.expectOne('/api/users').flush([]);
```

#### Angular 20+ рекомендації

- Mock через useValue — default вибір
- Не використовуйте реальні HTTP-запити
- Mock тільки зовнішні залежності
- Один mock = один тестовий сценарій
- Для signals — просто викликайте .set()

#### Типові помилки

- Мокати приватні методи
- Тестувати реалізацію замість поведінки
- Підміняти весь Store замість slice

**Коротко**

Mock-сервіси в Angular створюються через useValue, useClass або spy-обʼєкти і
дозволяють ізольовано та надійно тестувати компоненти й сервіси.

</details>

<details>
<summary>65. Чи можна виконувати наскрізне тестування в Angular?</summary>

#### Angular

#### Коротка відповідь

**Так, Angular повністю підтримує E2E (end-to-end) тестування**, але не має
вбудованого інструмента — використовується зовнішній тест-раннер.

#### Рекомендовані інструменти

**Playwright (рекомендовано)**

- Сучасний стандарт
- Швидкий і стабільний
- Працює з SSR та SPA
- Підтримує multiple browsers

```bash
npm init playwright@latest
```

```TypeScript
test('login flow', async ({ page }) => {
  await page.goto('/');
  await page.fill('#email', 'test@mail.com');
  await page.click('button[type=submit]');
  await expect(page).toHaveURL('/dashboard');
});
```

#### Cypress

- Простий у використанні
- Чудовий dev experience
- Менш стабільний для складних SSR-сценаріїв

```TypeScript
cy.visit('/');
cy.get('input').type('test@mail.com');
cy.contains('Submit').click();
```

#### Protractor

- Deprecated
- Не рекомендується у сучасних Angular-проєктах

#### Що тестує E2E

- Реальні користувацькі флоу
- Навігацію
- Інтеграцію з бекендом
- Авторизацію
- SSR + hydration (якщо є)

#### Best practices

- Мінімізувати кількість E2E-тестів
- Не тестувати дрібну логіку (для цього unit)
- Використовувати test IDs (data-testid)
- Мокати бекенд або використовувати test environment
- Запускати E2E у CI

#### Angular 20+ контекст

- E2E працює з standalone та signals без проблем
- SSR тестується через Playwright
- Zoneless режим не впливає на E2E

**Коротко**

Angular не має власного E2E-фреймворку, але відмінно працює з Playwright і
Cypress для повноцінного наскрізного тестування.

</details>

<details>
<summary>66. Які відмінності між Jasmine та Karma в контексті тестування Angular?</summary>

#### Angular

#### Коротко

- **Jasmine** — це **фреймворк для написання тестів**
- **Karma** — це **тест-раннер**, який запускає ці тести в браузерах

Вони **доповнюють**, а не замінюють одне одного.

#### Jasmine

**Що це**

**BDD-тестовий фреймворк**, який надає:

- `describe`, `it`, `beforeEach`
- `expect`, matchers
- spies (`spyOn`)

```TypeScript
describe('Counter', () => {
  it('should increment', () => {
    expect(1 + 1).toBe(2);
  });
});
```

**Відповідає за**

- Синтаксис тестів
- Assertions
- Mock / Spy логіку

#### Karma

**Що це**

**Test runner**, який:

- Запускає тести
- Відкриває браузери (Chrome, Firefox, Headless)
- Відслідковує файли та перезапускає тести
- Репортує результати

```bash
ng test
```

#### Відповідає за

- Середовище виконання
- Інтеграцію з браузером
- CI-запуск

#### Angular 20+ контекст

- Jasmine + Karma — legacy default
- Все частіше замінюються на:
  - Jest
  - Vitest (Vite)
- Karma повільніший, але стабільний
- Jasmine простий, але менш гнучкий за Jest

#### Best practices

- Для нових проєктів:
  - Vitest / Jest
- Для legacy Angular:
  - Jasmine + Karma — ок
- Не змішувати відповідальності інструментів

**Коротко**

Jasmine пише тести, Karma запускає тести, разом вони утворюють класичний стек
тестування Angular.

</details>

<details>
<summary>67. Які стратегії ви б використали для зменшення часу завантаження програми Angular?</summary>

#### Angular

1. Lazy Loading (критично важливо)

**Lazy routes**

```TypeScript
{
  path: 'admin',
  loadComponent: () =>
    import('./admin/admin.component').then(m => m.AdminComponent),
}
```

- Менший initial bundle
- Швидший старт

2. Standalone + Tree Shaking

- Використовувати standalone components
- Імпортувати тільки необхідні залежності

```TypeScript
@Component({ standalone: true, imports: [CommonModule], })
```

3. Change Detection Optimization

- ChangeDetectionStrategy.OnPush
- Signals замість зайвого RxJS

```TypeScript
changeDetection: ChangeDetectionStrategy.OnPush
```

4. SSR + Hydration (якщо є SEO)

- SSR для швидкого First Contentful Paint
- Hydration для уникнення повторного рендеру

```TypeScript
provideClientHydration()
```

5. Code Splitting & Dynamic Imports

- Динамічно завантажувати важкі бібліотеки

```TypeScript
const chart = await import('chart.js');
```

6. Оптимізація Assets

- Lazy loading зображень

```HTML
<img src="img.png" loading="lazy" />
```

- Стиснення (gzip / brotli)
- Мінімізація шрифтів

7. Zoneless Angular (Angular 20+)

```TypeScript
provideExperimentalZonelessChangeDetection()
```

- Менше runtime overhead
- Потрібна дисципліна в реактивності

8. Preloading стратегія

```TypeScript
withPreloading(PreloadAllModules)
```

Завантажує lazy-модулі після старту

9. Видалення зайвого

- Не імпортувати CommonModule без потреби
- Не використовувати impure pipes
- Мінімізувати глобальні стилі

**Коротко**

Найбільший ефект дають lazy loading, standalone + OnPush, SSR з hydration та
code splitting; дрібні оптимізації мають сенс лише після цього.

</details>

<details>
<summary>68. </summary>

#### Angular

</details>

<details>
<summary>69. </summary>

#### Angular

</details>

<details>
<summary>70. </summary>

#### Angular

</details>
```
