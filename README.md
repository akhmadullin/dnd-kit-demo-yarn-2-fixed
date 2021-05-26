# DND-kit demo with Yarn 2

This project was created for demonstartion of incorrect work of dnd-kit with yarn 2.

If you run app, you will see, that dnd does not work.

Debugging shows, that the reason of this bug is different `DndContext` in `useDraggable` and `useDroppable` hooks (different from App `DndContext`).
This happens because of Yarn 2 dependencies resolving mechanism - we have 2 different `@dnd-kit/core` instances in our App (check `yarn.lock` file).

It seems like, not core packages in dnd-kit project should use `@dnd-kit/core` as peerDependency.

### Solution for projects, that use @dnd-kit/core and @dnd-kit/sortable in dependencies
To solve problem with dnd-kit dependencies you should define in `.yarnrc.yml`, that `@dnd-kit/core` should be used as peerDependency for `@dnd-kit/sortable`:

```yml
# .yarnrc.yml
packageExtensions:
  "@dnd-kit/sortable@*":
    peerDependencies:
      "@dnd-kit/core": "*"
```

### Live demo

https://akhmadullin.github.io/dnd-kit-demo-yarn-2-fixed/

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

## Learn More

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
