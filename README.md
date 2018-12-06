# LIB_LIST

I've created this library as a wrapper around the native array datatype available in VGL. The functions and parameters are modeled after JavaScript's built-in `Array` object.

## Usage

Simply join the library to your VGL program and run `lib_list_define_list_class ( )` before using the class. Simple example:

```vgl
JOIN LIBRARY lib_list

DECLARE plants, animals

lib_list_define_list_class ( )
CREATE OBJECT LIST_CLASS, plants

plants . push ( "oak tree" ) . push ( "mouse" ) . push ( "tulip" )
animals = plants . splice ( 2, 1 ) . push ( "cat" ) . reverse ( )

{
    plants = [ oak tree, tulip ]
    animals = [ cat, mouse ]
}
```

You can see the different class actions available in the [Test Report](#test-report) section below.

## Limitations

* No functions like `map`, `filter`, or `reduce` which take a function as a parameter.
* No `sort`, but you can use the built-in `array_sort ( )` in `STD_ARRAY` on the `list . data` property.
* Changes to `list . data` should be accompanied by an update to `list . length` if applicable.

## Test Report

If you run `lib_list` with no routine specified, it will execute the test suite and display this table (in Markdown format):

| Function                     | Result     | Details                                                                  |
|------------------------------|------------|--------------------------------------------------------------------------|
| create object                |            |                                                                          |
|                              | _OK_       | `( list != EMPTY ) = TRUE`                                               |
| class initialisation         |            |                                                                          |
|                              | _OK_       | `list . length = 0`                                                      |
|                              | _OK_       | `size_of_array ( list . data ) = 0`                                      |
| append                       |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = []`                                               |
|                              | _OK_       | `list . append ( 'x' ) . toString ( ) = [x]`                             |
|                              | _OK_       | `list . append ( 'y' ) . append ( 'z' ) .toString ( ) = [x,y,z]`         |
| clear                        |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [x,y,z]`                                          |
|                              | _OK_       | `list . clear ( ) . length = 0`                                          |
|                              | _OK_       | `list . toString ( ) = []`                                               |
| concat                       |            |                                                                          |
|                              | _OK_       | `i . toString ( ) = [a,b]`                                               |
|                              | _OK_       | `j . toString ( ) = [x,y]`                                               |
|                              | _OK_       | `i . concat ( j ) . toString ( ) = [a,b,x,y]`                            |
| copy                         |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [x,y]`                                            |
|                              | _OK_       | `i = list . copy ( ); i . toString ( ) = [x,y]`                          |
|                              | _OK_       | `i . pop ( ); i . toString ( ) = [x]`                                    |
|                              | _OK_       | `list . toString ( ) = [x,y]`                                            |
| get                          |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b]`                                            |
|                              | _OK_       | `list . get ( 0 ) = EMPTY`                                               |
|                              | _OK_       | `list . get ( 1 ) = a`                                                   |
|                              | _OK_       | `list . get ( 2 ) = b`                                                   |
|                              | _OK_       | `list . get ( 3 ) = EMPTY`                                               |
| inBounds                     |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b]`                                            |
|                              | _OK_       | `list . inBounds ( 0 ) = FALSE`                                          |
|                              | _OK_       | `list . inBounds ( 1 ) = TRUE`                                           |
|                              | _OK_       | `list . inBounds ( 2 ) = TRUE`                                           |
|                              | _OK_       | `list . inBounds ( 3 ) = FALSE`                                          |
|                              | _OK_       | `list . inBounds ( EMPTY ) = FALSE`                                      |
|                              | _OK_       | `list . inBounds ( 'xyz' ) = FALSE`                                      |
| includes                     |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b]`                                            |
|                              | _OK_       | `list . includes ( 'a' ) = TRUE`                                         |
|                              | _OK_       | `list . includes ( 'b' ) = TRUE`                                         |
|                              | _OK_       | `list . includes ( 'x' ) = FALSE`                                        |
|                              | _OK_       | `list . includes ( EMPTY ) = FALSE`                                      |
|                              | _OK_       | `list . append ( EMPTY ) . includes ( EMPTY ) = TRUE`                    |
| indexOf                      |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,a]`                                          |
|                              | _OK_       | `list . indexOf ( 'a' ) = 1`                                             |
|                              | _OK_       | `list . indexOf ( 'b' ) = 2`                                             |
|                              | _OK_       | `list . indexOf ( 'x' ) = 0`                                             |
|                              | _OK_       | `list . indexOf ( EMPTY ) = 0`                                           |
|                              | _OK_       | `list . append ( EMPTY ) . indexOf ( EMPTY ) = 4`                        |
| join                         |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,c]`                                          |
|                              | _OK_       | `list . join ( ', ' ) = a, b, c`                                         |
|                              | _OK_       | `list . join ( '' ) = abc`                                               |
|                              | _OK_       | `list . join ( EMPTY ) = abc`                                            |
| lastIndexOf                  |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,a]`                                          |
|                              | _OK_       | `list . lastIndexOf ( 'a' ) = 3`                                         |
|                              | _OK_       | `list . lastIndexOf ( 'b' ) = 2`                                         |
|                              | _OK_       | `list . lastIndexOf ( 'x' ) = 0`                                         |
|                              | _OK_       | `list . lastIndexOf ( EMPTY ) = 0`                                       |
|                              | _OK_       | `list . append ( EMPTY ) . lastIndexOf ( EMPTY ) = 4`                    |
| pop                          |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,c]`                                          |
|                              | _OK_       | `list . pop ( ) = c`                                                     |
|                              | _OK_       | `list . pop ( ) = b`                                                     |
|                              | _OK_       | `list . toString ( ) = [a]`                                              |
|                              | _OK_       | `list . clear ( ) . pop ( ) = EMPTY`                                     |
| push                         |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = []`                                               |
|                              | _OK_       | `list . push ( 'x' ) . toString ( ) = [x]`                               |
|                              | _OK_       | `list . push ( 'y' ) . push ( 'z' ) .toString ( ) = [x,y,z]`             |
| reverse                      |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,c,d]`                                        |
|                              | _OK_       | `list . reverse ( ) . toString ( ) = [d,c,b,a]`                          |
|                              | _OK_       | `list . append ( 'x' ) . toString ( ) = [d,c,b,a,x]`                     |
|                              | _OK_       | `list . reverse ( ) . toString ( ) = [x,a,b,c,d]`                        |
| set                          |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b]`                                            |
|                              | _OK_       | `list . set ( 1, 'x' ) . toString ( ) = [x,b]`                           |
|                              | _OK_       | `list . set ( 2, 'y' ) . toString ( ) = [x,y]`                           |
|                              | _OK_       | `list . set ( EMPTY, 'z' ) . toString ( ) = [x,y,z]`                     |
|                              | _OK_       | `list . set ( 0, 'foo' ) = EMPTY`                                        |
|                              | _OK_       | `list . set ( 4, 'foo' ) = EMPTY`                                        |
| slice                        |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [1,2,3,4,5,6,7,8]`                                |
|                              | _OK_       | `list . slice ( 2, 4 ) . toString ( ) = [2,3]`                           |
|                              | _OK_       | `list . slice ( 4, 2 ) . toString ( ) = []`                              |
|                              | _OK_       | `list . slice ( -3, EMPTY ) . toString ( ) = [6,7,8]`                    |
|                              | _OK_       | `list . slice ( EMPTY, EMPTY ) . toString ( ) = [1,2,3,4,5,6,7,8]`       |
|                              | _OK_       | `list . slice ( EMPTY, -3 ) . toString ( ) = [1,2,3,4,5]`                |
| splice                       |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [1,2,3,4,5,6,7,8]`                                |
|                              | _OK_       | `list . copy ( ) . splice ( 3, 2 ) . toString ( ) = [3,4]`               |
|                              | _OK_       | `list . copy ( ) . splice ( 5, 100 ) . toString ( ) = [5,6,7,8]`         |
|                              | _OK_       | `list . splice ( -5, 4 ) . toString ( ) = [4,5,6,7]`                     |
|                              | _OK_       | `list . toString ( ) = [1,2,3,8]`                                        |
| toString                     |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [1,2,3]`                                          |
|                              | _OK_       | `list . clear ( ) . append ( '1' ) . toString ( ) = [1]`                 |
|                              | _OK_       | `list . clear ( ) . toString ( ) = []`                                   |
| unshift                      |            |                                                                          |
|                              | _OK_       | `list . toString ( ) = [a,b,c]`                                          |
|                              | _OK_       | `list . unshift ( ) = a`                                                 |
|                              | _OK_       | `list . unshift ( ) = b`                                                 |
|                              | _OK_       | `list . toString ( ) = [c]`                                              |
|                              | _OK_       | `list . clear ( ) . unshift ( ) = EMPTY`                                 |

## Contributions

Pull requests welcome.

## Licensing

This work is licensed under the MIT license. [Here's what this means.](https://choosealicense.com/licenses/mit/)