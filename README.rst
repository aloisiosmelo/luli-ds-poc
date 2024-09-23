DEPRECATED: All the related functionalities have been integrated and maintained within the `es-pack-js <https://github.com/w3reality/es-pack-js>`__ repository.

es6-esm-boilerplate
===================

Build ES modules from ES6 source code with Webpack.

Starting with this boilerplate, we can develop simple-to-complex
ES Modules targeting the latest browsers, development with Babel, and
Node runtime. At the same time, the ES5-compatible build is also generated for convenience.

Why we do this?

This module building pattern shines especially when we deal with the NPM module ecosystem.
Webpack can bundle any NPM dependencies listed in ``package.json`` regardless of their module types.
So, with Webpack, we can expose any combination of existing NPM packages wrapped as an ES module; and
we can consume them by simply ``import``-ing the ES module while keeping our code base ES6-based.

Input/output structure
----------------------

.. code::

   es6-esm-boilerplate
   ├── package.json
   ├── webpack.config.js
   ├── src                         # ES6 source code
   │   ├── Base.js                 # class 
   │   ├── Foo.js                  # subclass of Base
   │   ├── Bar.js                  # subclass of Base
   │   ├── index.js                # module implementation (export { Foo, Bar })
   │
   ├── lib                         # ES module output
   │   ├── luli-ds.js            # esm
   │   ├── luli-ds.min.js        # esm minified
   │   ├── luli-ds.compat.js     # esm with ES5-compatibility
   │   ├── luli-ds.compat.min.js # esm with ES5-compatibility minified

How it works
------------

.. code::

   ES6 source code          -> var-module             -> luli-ds.js (export default LuliDs;)
   {Base,Foo,Bar,index}.js     (var LuliDs = ...;)  -> luli-ds.compat.js (UMD)

First, bundle ES6 source code into a var-module.  Then, export the var-module using the
ES Module's ``export`` syntax to finally get ``luli-ds.js``.  This module file can be directly
consumed on `relatively new browsers <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Browser_compatibility>`__.  

We also build ``luli-ds.compat.js`` for compatibility with older browsers, development with Babel,
and NodeJS.  This module output conforms to the `UMD <https://github.com/umdjs/umd>`__ patterns that provide the
script-tag loading, Node-require, and AMD compatibilities.

All the "var-to-esm transformation" is performed by a tiny Webpack plugin called
`webpack-var2esm-plugin <https://github.com/w3reality/webpack-var2esm-plugin/blob/master/src/index.js>`__.

Build
-----

.. code::

   # git clone and cd to this repo, then
   $ npm install  # set up build tools
   $ npm run build  # get ES module output in lib/ by Babel
