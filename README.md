# vue2-starter

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Run your unit tests
```
yarn test:unit
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### How to use the Chart component
This starter provides a Chart component to visualize on a timeline the performance evolution.

Under the hood it uses a minimal setup of billboard.js (feel free to restyle it if the default appearence is too ugly), to pass your data to the component you must use the `dataset` prop, it expects the following format
```
[
  { date: '2000-01-01', performance: 1 },
  { date: '2000-01-02', performance: 2 },
  { date: '2000-01-03', performance: 3 },
  ...
  { date: '2000-01-04', performance: 4 },
  { date: '2000-01-05', performance: 5 },
  { date: '2000-01-06', performance: 6 }
]
```
This property is already reactive, so to show another dataset you just need to update the binded value.
