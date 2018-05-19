## C Programming Rules

> A global variable must always start with a capital.
>
> For each pointer indirection __`Ptr`__ has to be added at the end of the name of the variable.
>
> A local variable always starts with a lowercase letter. Local variables that are static are preferably declared first.
>
> Names of functions that are local to the module have to start with a lowercase letter and names of functions that are exported have to start with a capital.
>
> When the return type is a pointer, the pointer asterisk sticks to the function name just as with pointer variables.
>
> The name of the type always starts with a capital and end with Type. An exception to this rule is the __`enum`__ type. The fields in a type definition start with a lower case, since they are _local_ to the type. As well as the exception to this rule is the __`enum`__ type.
>
> The definition must be in full capitals. For readability use underscores to separate words. Grouped definitions have to be ordered correctly and placed in the same positions when indenting.
>
>  A closing bracket is never preceded by a space. An opening bracket is always preceded by a space or another opening bracket.
>
> The beginning of a compound statement **`{`** is always placed on the next line in the same column as the preceding statement.
>
> The name of a function in a function call is always followed by one space and then the opening bracket of the function parameter list. When there are no function parameters to be passed, the closing bracket follows the opening bracket directly __`function ();`__. 