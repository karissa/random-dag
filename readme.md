# random-dag

Create a random Directed Acyclic Graph as a stream or as a `graphlib` object.

```npm install random-dag```

[![build status](http://img.shields.io/travis/karissa/random-dag.svg?style=flat)](http://travis-ci.org/karissa/random-dag)

## CLI

```
$ npm install -g random-dag
$ random-dag --max_per_rank=5 --max_ranks=100 --probability=.5
{ from: 0, to: 3 }
{ from: 0, to: 4 }
{ from: 2, to: 3 }
{ from: 2, to: 4 }
{ from: 2, to: 10 }
{ from: 2, to: 11 }
etc...
```

## API

### `dag.stream(opts)`

```js
var dag = require('random-dag')
var opts = {
  max_per_rank: 5, // how 'fat' the DAG should be
  min_per_rank: 1,
  max_ranks: 3, // how 'tall' the DAG should be
  min_ranks: 5,
  probability: 0.3 // chance of having an edge
}
var stream = dag.stream(opts)
stream.on('data', function (edge) {
  // e.g, an edge from node with index '0' and index '1'.
  // {from: 0, to: 1}
})
```

### `dag.graphlib(opts, cb)`

Can provide optional options as a first argument, same as above stream.

```js
var graphlib = require('graphlib')
var dag = require('random-dag')
dag.graphlib(function (err, g) {
  // g is a graphlib.Graph object
  console.log(graphlib.alg.isAcyclic(g)) // true
})
```

## License

MIT
