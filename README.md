# Rollup

## Creating your first bundle

```
npm install rollup --global # or `npm i rollup -g` for short
```

Let's create a simple project:

```
mkdir -p my-rollup-project/src
cd my-rollup-project
```

First, we need an entry point:

```
echo "import foo from './foo.js';" >> src/main.js
echo "export default function () {\n  console.log(foo);\n}" >> src/main.js
```

Then, let's create the foo.js module that our entry point imports:

```
echo "export default 42;" > src/foo.js
```

Now we're ready to create a bundle:

```
rollup src/main.js
```

This will print the bundle straight to `stdout`:

```
var foo = 42;
​
function main () {
  console.log(foo);
}
​
export default main;
```

You can save the bundle as a file like so:

```
rollup src/main.js --output bundle.js # or rollup main.js -o bundle.js
```

---

create a CommonJS module

```
rollup src/main.js --output bundle.js --format cjs
# or rollup src/main.js -o bundle.js -f cjs
```

Try running the code:

```
node
> var myBundle = require('./bundle.js');
> myBundle();
```

## Using config files

Create a file in the project root called `rollup.config.js`, and add the following code:

```
export default {
  entry: 'src/main.js',
  format: 'cjs',
  dest: 'bundle.js' // equivalent to --output
};
```

To use the config file, we use the `--config` or `-c` flag:

```
rm bundle.js # so we can check the command works!
rollup -c
```

You can override any of the options in the config file with the equivalent command line options:

```
rollup -c -o bundle-2.js # --output is equivalent to dest
```

You can, if you like, specify a different config file from the default `rollup.config.js`:

```
rollup --config rollup.config.dev.js
rollup --config rollup.config.prod.js
```
