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

## TODO

While the application works and proves to be a rather teaching project, it can be definitely improved:

- [ ] review the transition between the components and the affordances of each stage. It should be more clear that the form element allows for a selection between the two signs.

- [ ] consider increasing the size of the grid and most importantly animating the path elements for the two signs.

- [ ] to stress a victory, consider adding a stroke on top of the adjacent signs.