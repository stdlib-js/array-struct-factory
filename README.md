<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# structFactory

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Return a constructor for creating arrays having a fixed-width composite data type.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->



<section class="usage">

## Usage

```javascript
import structFactory from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-struct-factory@deno/mod.js';
```

#### structFactory( arg )

Returns a constructor for creating arrays having a fixed-width composite data type.

```javascript
var schema = [
    {
        'name': 'beep',
        'type': 'float64'
    },
    {
        'name': 'boop',
        'type': 'int32'
    }
];
var StructArray = structFactory( schema );
// returns <Function>
```

The function supports the following parameters:

-   **arg**: [`struct`][@stdlib/dstructs/struct] constructor or a [`struct`][@stdlib/dstructs/struct] schema.

* * *

### Array Constructor

#### StructArray()

TODO: add documentation of constructor

* * *

### Array Properties

<a name="static-prop-bytes-per-element"></a>

#### StructArray.BYTES_PER_ELEMENT

Number of bytes per view element.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var nbytes = StructArray.BYTES_PER_ELEMENT;
// returns 1
```

<a name="static-prop-name"></a>

#### StructArray.name

Array constructor name.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var str = StructArray.name;
// returns 'StructArray'
```

<a name="prop-buffer"></a>

#### StructArray.prototype.buffer

**Read-only** property which returns the [`ArrayBuffer`][@stdlib/array/buffer] referenced by the array.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var arr = new StructArray( 5 );
var buf = arr.buffer;
// returns <ArrayBuffer>
```

<a name="prop-byte-length"></a>

#### StructArray.prototype.byteLength

**Read-only** property which returns the length (in bytes) of the array.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'int32'
    }
];
var StructArray = structFactory( schema );

var arr = new StructArray( 5 );
var byteLength = arr.byteLength;
// returns 20
```

<a name="prop-byte-offset"></a>

#### StructArray.prototype.byteOffset

**Read-only** property which returns the offset (in bytes) of the array from the start of its [`ArrayBuffer`][@stdlib/array/buffer].

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var arr = new StructArray( 5 );
var byteOffset = arr.byteOffset;
// returns 0
```

<a name="prop-bytes-per-element"></a>

#### StructArray.prototype.BYTES_PER_ELEMENT

Number of bytes per view element.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var arr = new StructArray( 5 );
var nbytes = arr.BYTES_PER_ELEMENT;
// returns 1
```

<a name="prop-length"></a>

#### StructArray.prototype.length

**Read-only** property which returns the number of view elements.

```javascript
var schema = [
    {
        'name': 'foo',
        'type': 'bool'
    }
];
var StructArray = structFactory( schema );

var arr = new StructArray( 5 );
var len = arr.length;
// returns 5
```

* * *

### Array Methods

TODO: document methods

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

* * *

## Notes

-   While returned constructors _strive_ to maintain (but do not **guarantee**) consistency with [typed arrays][@stdlib/array/typed], significant deviations from ECMAScript-defined [typed array][@stdlib/array/typed] behavior are as follows:

    -   Constructors do **not** require the `new` operator.
    -   Accessing array elements using bracket syntax (e.g., `X[i]`) is **not** supported. Instead, one **must** use the `.get()` method.
    -   Accessed array elements are a view on underlying memory. Thus, mutation of accessed elements mutates the underlying buffer.

-   Struct arrays share several similarities with generic arrays containing objects (e.g., nested property access); however, the principal difference is that struct arrays are strongly typed and backed by fixed memory. Struct arrays are particularly well-suited for zero-copy transfer of data stored in composite data types when interoperating between JavaScript and C.

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import factory from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-struct-factory@deno/mod.js';

// Define a schema for a composite data type for storing a student's test scores:
var schema = [
    {
        'name': 'test_number',
        'type': 'int16'
    },
    {
        'name': 'pass',
        'type': 'bool'
    },
    {
        'name': 'correct',
        'type': 'int32'
    },
    {
        'name': 'incorrect',
        'type': 'int32'
    },
    {
        'name': 'percentage',
        'type': 'float32'
    }
];

// Create an array constructor for creating composite data type arrays:
var TestScoreArray = factory( schema );
console.log( 'Layout: %s', TestScoreArray.struct.layout );

// Create a new array for storing test scores:
var student1 = new TestScoreArray( 10 );
console.log( 'Byte length: %d', student1.byteLength );
```

</section>

<!-- /.examples -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/array-struct-factory.svg
[npm-url]: https://npmjs.org/package/@stdlib/array-struct-factory

[test-image]: https://github.com/stdlib-js/array-struct-factory/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/array-struct-factory/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/array-struct-factory/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/array-struct-factory?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/array-struct-factory.svg
[dependencies-url]: https://david-dm.org/stdlib-js/array-struct-factory/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/array-struct-factory/tree/deno
[deno-readme]: https://github.com/stdlib-js/array-struct-factory/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/array-struct-factory/tree/umd
[umd-readme]: https://github.com/stdlib-js/array-struct-factory/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/array-struct-factory/tree/esm
[esm-readme]: https://github.com/stdlib-js/array-struct-factory/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/array-struct-factory/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/array-struct-factory/main/LICENSE

[@stdlib/array/typed]: https://github.com/stdlib-js/array-typed/tree/deno

[@stdlib/array/buffer]: https://github.com/stdlib-js/array-buffer/tree/deno

[@stdlib/dstructs/struct]: https://github.com/stdlib-js/dstructs-struct/tree/deno

</section>

<!-- /.links -->
