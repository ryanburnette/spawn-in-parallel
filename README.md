# [spawn-in-parallel][1]

[![repo](https://img.shields.io/badge/repository-Github-black.svg?style=flat-square)](https://github.com/ryanburnette/spawn-in-parallel) [![npm](https://img.shields.io/badge/package-NPM-green.svg?style=flat-square)](https://www.npmjs.com/package/@ryanburnette/spawn-in-parallel)

Spawn your development tasks in parallel. When you kill your script, the
spawned processes also die. Works on macOS, Linux, and Windows. This makes use
of [Node.js][2] and [child_process.spawn][3] with helpful defaults.

## Usage

Let's say you have two things you want spinning when you're in development.

```
hugo server -D -p 3000
```

```
npx webpack --config webpack.development.js --watch
```

Make a `scripts/development` file like this.

Simple...

```js
#!/usr/bin/env node
require('@ryanburnette/spawn-in-parallel')([
  'hugo server -D -p 3000',
   'npx webpack --config webpack.development.js --watch'
]);
```

This demonstrates all the available options...

```js
#!/usr/bin/env node
require('@ryanburnette/spawn-in-parallel')([
  'hugo server -D -p 3000',
  {
    cmd: 'npx webpack --config webpack.development.js --watch',
    opts: {
      // per cmd opts for spawn here
    }
  } 
], {
  // put custom opts for spawn here
});
```

Make it executable.

```
chmod +x scripts/development
```

Get to work.

```
scripts/development
```

[1]: https://github.com/ryanburnette/spawn-in-parallel
[2]: https://nodejs.org
[3]: https://nodejs.org/dist/latest-v12.x/docs/api/child_process.html#child_process_child_process_spawn_command_args_options
