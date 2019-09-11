# Svelte

The application is set up in **svelte-app** through the `degit` scaffolding tool.

```
npx degit sveltejs/template svelte-app
```

## Gameplay

The game is planned with the following structure:

- [x] the player is greeted by a loader.

- [x] following an arbitrary number of iterations, the animations stops and the loader is removed. The loader is removed in favor of a form which allows to pick between the **x** and **o** signs.

- [x] following a selection, the form is removed in favor of a grid. A grid of 9 buttons in 3 columns and 3 rows.

- [x] upon clicking on the available buttons, the **x** and **o** signs alternate each other, according to the initial selection.

- [x] after every more, the project checks for a victory. Victory consisting of three adjacent signs. In this instance, the victorious buttons are highlighted. Always in this instance and after a brief delay, the game returns to the selection stage.

- [x] after every more and after checking for a victory, the project checks for a tie. If no more buttons are available, the game returns to the selection stage after a brief delay.

## Transitions

It is essential to transition between the different stages of the game to provide apt feedback:

- as the loader is removed, the idea is to include the selection with the same shapes. The transition, while seamless, requires an additional cue to highlight the interactivity of the existing elements;

- as a choice is made, and to get started, the shapes should disappear as the grid then appears.

