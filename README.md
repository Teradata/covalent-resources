# MarkdownNavigatorComponent

A component for rendering and navigating through markdown, such as documentation. Supports github urls.

## API Summary

#### Inputs
+ items: IMarkdownNavigatorItem[]
  + List of IMarkdownNavigatorItems to be rendered
+ labels?: IMarkdownNavigatorLabels
  + Translated labels
+ toolbarColor?: ThemePalette
  + Color palette for toolbar
  + Defaults to 'primary'

## Setup

```typescript
import { CovalentMarkdownNavigatorModule } from '@covalent/markdown-navigator';
@NgModule({
  imports: [
    CovalentMarkdownNavigatorModule,
    ...
  ],
  ...
})
export class MyModule {}
```

## Usage

```html
  <td-markdown-navigator [items]="items"></td-markdown-navigator>

```

#### Sample items

```typescript
oneItem: IMarkdownNavigatorItem[] = [
  {
    url: 'https://github.com/Teradata/covalent/blob/develop/README.md',
  },
];

itemWithRawMarkdown: IMarkdownNavigatorItem[] = [
  {
    markdownString: '\n\n# Raw markdown example\n \n> Amazing\n\n1. List\n2. of\n3. items\n\n',
  },
];

multipleItems: IMarkdownNavigatorItem[] = [
  {
    url: 'https://raw.githubusercontent.com/Teradata/nodejs-driver/develop/README.md',
    title: 'Node.js Driver for Teradata',
  },
  {
    url: 'https://raw.githubusercontent.com/angular/angular/master/README.md',
    title: 'Angular',
  },
];

oneItemWithAnchor: IMarkdownNavigatorItem[] = [
  {
    url: 'https://raw.githubusercontent.com/Teradata/covalent/develop/docs/DEVELOPER_GUIDE.md',
    anchor: 'Adding a new documentation component',
  },
];

nestedItems: IMarkdownNavigatorItem[] = [
  {
    title: 'Covalent',
    children: [
      {
        title: 'Components',
        children: [
          {
            url: 'https://raw.githubusercontent.com/Teradata/covalent/develop/src/platform/core/loading/README.md',
            title: 'tdLoading',
          },
        ],
      },
    ],
  },
];

```

For reference:
```typescript
interface IMarkdownNavigatorItem {
  title?: string;
  url?: string;
  httpOptions?: object;
  markdownString?: string; // raw markdown
  anchor?: string;
  children?: IMarkdownNavigatorItem[];
}
```

# MarkdownNavigatorWindowService

A service that opens a MarkdownNavigatorWindowComponent inside a draggable dialog. Uses the openDraggable method of the TdDialogService.

## API Summary

#### Methods

+ open: function(config: IMarkdownNavigatorWindowConfig)
  + Opens a MarkdownNavigatorWindowComponent inside a draggable dialog.

For reference:
```typescript
interface IMarkdownNavigatorWindowConfig {
  items: IMarkdownNavigatorItem[];
  dialogConfig?: MatDialogConfig;
  labels?: IMarkdownNavigatorWindowLabels;
  toolbarColor?: ThemePalette;
}
```

## Setup

```typescript
import { CovalentMarkdownNavigatorModule } from '@covalent/markdown-navigator';
@NgModule({
  imports: [
    CovalentMarkdownNavigatorModule,
    ...
  ],
  ...
})
export class MyModule {}
```


## Usage

Example:

```typescript
import {
  MarkdownNavigatorWindowComponent,
  MarkdownNavigatorWindowService,
  IMarkdownNavigatorItem,
} from '@covalent/markdown-navigator';
import { MatDialogRef } from '@angular/material/dialog';

export class SampleComponent{

  constructor(private _markdownNavigatorWindowService: MarkdownNavigatorWindowService) {}

  ngOnInit(): void {
    const ref: MatDialogRef<MarkdownNavigatorWindowComponent> = this._markdownNavigatorWindowService.open({
      items: [{ url: 'https://github.com/Teradata/covalent/blob/develop/README.md' }]
    });
    ref.afterOpened().subscribe(() => {

    });
    ref.afterClosed().subscribe(() => {

    });
  }
}
```


# MarkdownNavigatorWindowDirective

A directive that calls the MarkdownNavigatorWindowService open method on click events.

## API Summary

#### Inputs

+ tdMarkdownNavigatorWindow: IMarkdownNavigatorWindowConfig
  + Config to open window with
+ disabled: boolean
  + Whether disabled or not

For reference:
```typescript
interface IMarkdownNavigatorWindowConfig {
  items: IMarkdownNavigatorItem[];
  dialogConfig?: MatDialogConfig;
  labels?: IMarkdownNavigatorWindowLabels;
  toolbarColor?: ThemePalette;
}
```

## Setup

```typescript
import { CovalentMarkdownNavigatorModule } from '@covalent/markdown-navigator';
@NgModule({
  imports: [
    CovalentMarkdownNavigatorModule,
    ...
  ],
  ...
})
export class MyModule {}
```


## Usage

Example:

```html
<button mat-button [tdMarkdownNavigatorWindow]="{ items: [] }" [disabled]="false">Open window</button>
```
