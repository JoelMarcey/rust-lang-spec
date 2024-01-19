An array is a numbered, fixed-size sequence of elements of a single [type](link to type spec), called the element type. The element type of an array can be any Rust [type](link to type spec). 

The size of an array must evaluate to a non-negative constant expression represented by at value of type `usize`.

Arrays are stored in contiguous memory.

Arrays can be mutable, insofar as their elements can change, but the size and type are always immutable.

## Array Type Specification

```
array-type:
    : '[' any-type ; array-size ']' '=' array-initializer 
    ;

any-type:
    : [type](link to type spec)
    ;

array-size:
    : ['usize'](link to usize spec)
    ;

array-initializer:
    : '[' array-element-list ']'
    | '[' *repeat-expression ']'
    ;

array-element-list*:
    : array-element
    | array-element-list ',' array-element
    ;

array-element:
    : expression
    ;

repeat-expression:
    : expression ; ['usize'](link to usize spec)
    ;
```

### Examples

```
let mut _spec_a: [i32; 3] = [3; 3]; // repeat expression
let _spec_b: [String; 2] = [String::from("hi"), String::from("bye")];
let _spec_c: [[i32; 2]; 3] = [[1, 2], [3, 4], [5, 6]];
let _spec_d: [u64; 0] = [];
```


## Array Creation

There are two ways to initialize an array at the time of its declaration:
1. a list of specific elements whose type matches the element type of the array being declared; or
2. a repeat expression whose expression has the same type as the element type of the array being declared.

```
array-initializer:
    : '[' array-element-list ']'
    | '[' *repeat-expression ']'
    ;

array-element-list*:
    : array-element
    | array-element-list ',' array-element
    ;

array-element:
    : expression
    ;

repeat-expression:
    : expression ; ['usize'](link to usize spec)
    ;
```

### Examples

#### List

```
let _cre_a: [i32; 2] = [3, 3];
let _cre_b: [String; 2] = [String::from("hi"), String::from("bye")];
```

#### Repeat Expression

```
let _cre_c = [0; 3];
let _cre_d = ["repeat"; 10];
```

## Array Access

Arrays are accessed by index, with the first element of the array having an index of 0. Thus, the range of indices for an array in Rust is `0..(array-size - 1)`. 

Using an index `i` of type `usize` and value `i > (array-size - 1)` will result in an `index out of bounds` compilation error.

```
array-access-expression:
    : array '[' array-index ']'
    ;

array-index:
    : usize
    ;
```

## Array Updates

If the array is mutable, as defined by the `mut` keyword, the array elements can be updated. The size and type of the array can never change.

Updating the value of an array element is performed by specifying the index of the element to be changed and setting it to the new value.

```
array-update-expression:
    : array-access-expression '=' expression
    ;

array-access-expression:
    : array '[' array-index ']'
    ;

array-index:
    : usize
    ;
```

### Examples

```
let mut upd_a: [i32; 3] = [1, 2, 4];
upd_a[2] = 3;

let mut upd_b: [[i32; 2]; 3] = [[1, 2], [3, 4], [5, 6]];
upd_b[0] = [0, 0];
```
