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
<summary>6. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>7. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>8. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>9. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>10. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>11. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>12. ???</summary>

#### Angular

- Coming soon...😎

</details>

<details>
<summary>13. ???</summary>

#### Angular

- Coming soon...😎

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
