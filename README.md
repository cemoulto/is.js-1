# is.js

Minimalistic check library.

## Install

Node:

```sh
$ npm install --save @pwn/is
```

Browser:

```html
<script src="path/to/is.js"></script>
```

## Usage

A code sample is worth a thousand words:

```js
is.number( 0 ) // true
is.not.number( 0 ) // false
is.equal( [ 1 , [ 2 , 3 ] ] , [ 1 , [ 2 , 3 ] ] ) // false
is.deepEqual( [ 1 , [ 2 , 3 ] ] , [ 1 , [ 2 , 3 ] ] ) // true
```

All checks, or _predicates_ in `is.js` terminology, takes two general forms:

- __POSITIVE CHECK__: `is.predicate( ...args )` - Checks whether certain condition met.
- __NEGATIVE CHECK__: `is.not.predicate( ...args )` - The inverse of its corresponding _POSITIVE CHECK_.

That's it! What's next?

- [Cheatsheet](#cheatsheet) - List of available predicates.
- [API reference](#api-reference) - Detailed documentation.
- [Writing new predicates](#writing-new-predicates) - Learn how to define new predicates.

## Cheatsheet

TL;DR

__bundle:nil__

- [is.null( value )](#)
- [is.undefined( value )](#)
- [is.nil( value )](#)

__bundle:number__

- [is.number( value )](#)
- [is.nan( value )](#)
- [is.odd( number )](#)
- [is.even( number )](#)
- [is.finite( number )](#)
- [is.infinite( number )](#)
- [is.integer( number )](#)
- [is.safeInteger( number )](#)

__bundle:string__

- [is.string( value )](#)
- [is.emptyString( string )](#)
- [is.stringIncludes( string , substring )](#)
- [is.startsWith( string , prefix )](#)
- [is.endsWith( string , suffix )](#)

__bundle:boolean__

- [is.boolean( value )](#)
- [is.true( value )](#)
- [is.false( value )](#)
- [is.truthy( value )](#)
- [is.falsy( value )](#)

__bundle:primitive__

- [is.primitive( value )](#)

__bundle:object__

- [is.object( value )](#)
- [is.emptyObject( object )](#)
- [is.ownPropertyDefined( object , key )](#)
- [is.propertyDefined( object , key )](#)

__bundle:array__

- [is.array( value )](#)
- [is.arrayLike( value )](#)
- [is.emptyArray( array )](#)
- [is.arrayIncludes( array , member )](#)
- [is.arrayDeepIncludes( array , member )](#)

__bundle:function__

- [is.function( value )](#)

__bundle:date__

- [is.date( value )](#)

__bundle:error__

- [is.error( value )](#)

__bundle:regex__

- [is.regex( value )](#)

__bundle:type__

- [is.sameType( value , other )](#)
- [is.instanceOf( object , constructor )](#)
- [is.prototypeOf( prototype , object )](#)

__bundle:equality__

- [is.equal( value , other )](#)
- [is.deepEqual( value , other )](#)

## API reference

### bundle:nil

#### is.null( value )

Checks whether given value is `null`.

```js
is.null( null ) // true
is.null( undefined ) // false
```

#### is.undefined( value )

Checks whether given value is `undefined`.

```js
is.undefined( null ) // false
is.undefined( undefined ) // true
```

#### is.nil( value )

Checks whether given value is either `null` or `undefined`.

```js
is.nil( null ) // true
is.nil( undefined ) // true
```

### bundle:number

#### is.number( value )

Checks whether given value is a Number.

```js
is.number( 0 ) // true
is.number( Number.NaN ) // true
is.number( Number.POSITIVE_INFINITY ) // true
is.number( Number.NEGATIVE_INFINITY ) // true
is.number( '0' ) // false
is.number( new Number( 0 ) ) // false
```

#### is.nan( value )

Checks whether given value is `NaN`.

```js
is.nan( 0 ) // false
is.nan( Number.NaN ) // true
is.nan( Number.POSITIVE_INFINITY ) // false
is.nan( Number.NEGATIVE_INFINITY ) // false
is.nan( 'one' ) // false
```

#### is.odd( number )

Checks whether given value is an odd number.

```js
is.odd( 1 ) // true
is.odd( 2 ) // false
is.odd( '1' ) // false
is.odd( '2' ) // false
```

#### is.even( number )

Checks whether given value is an even number.

```js
is.even( 1 ) // false
is.even( 2 ) // true
is.even( '1' ) // false
is.even( '2' ) // false
```

#### is.finite( number )

Checks whether given value is a finite number.

```js
is.finite( 0 ) // true
is.finite( '0' ) // false
is.finite( Number.NaN ) // false
is.finite( Number.POSITIVE_INFINITY ) // false
is.finite( Number.NEGATIVE_INFINITY ) // false
```

#### is.infinite( number )

Checks whether given value is an infinite number, i.e, `Number.POSITIVE_INFINITY` or `Number.NEGATIVE_INFINITY`.

```js
is.infinite( 0 ) // false
is.infinite( '0' ) // false
is.infinite( Number.NaN ) // false
is.infinite( Number.POSITIVE_INFINITY ) // true
is.infinite( Number.NEGATIVE_INFINITY ) // true
```

#### is.integer( number )

Checks whether given value is an integer.

```js
is.integer( 0 ) // true
is.integer( 0.1 ) // false
is.integer( Number.NaN ) // false
is.integer( Number.POSITIVE_INFINITY ) // false
is.integer( Number.NEGATIVE_INFINITY ) // false
is.integer( Number.MAX_SAFE_INTEGER ) // true
is.integer( Number.MIN_SAFE_INTEGER ) // true
is.integer( Number.MAX_SAFE_INTEGER + 1 ) // true
is.integer( Number.MIN_SAFE_INTEGER - 1 ) // true
```

#### is.safeInteger( number )

Checks whether given value is a safe integer.

```js
is.safeInteger( 0 ) // true
is.safeInteger( 0.1 ) // false
is.safeInteger( Number.NaN ) // false
is.safeInteger( Number.POSITIVE_INFINITY ) // false
is.safeInteger( Number.NEGATIVE_INFINITY ) // false
is.safeInteger( Number.MAX_SAFE_INTEGER ) // true
is.safeInteger( Number.MIN_SAFE_INTEGER ) // true
is.safeInteger( Number.MAX_SAFE_INTEGER + 1 ) // false
is.safeInteger( Number.MIN_SAFE_INTEGER - 1 ) // false
```

### bundle:function

#### is.function( value )

Checks whether given value is a function.

```js
is.function( function () {} ) // true
is.function( function* () {} ) // true
is.function( () => null ) // true
is.function( new Function() ) // true
```

### bundle:date

#### is.date( value )

Checks whether given value is a `Date` object.

```js
is.date( new Date() ) // true
```

### bundle:error

#### is.error( value )

Checks whether given value is an `Error` object.

```js
is.error( new Error() ) // true
is.error( new TypeError() ) // true
```

### bundle:regex

#### is.regex( value )

Checks whether given value is a `RegExp` object.

```js
is.regex( /^/ ) // true
is.regex( new RegExp() ) // true
```

## Writing new predicates
