《The AWK Programming Language》中文翻译

###1. [The 1st chapter](https://github.com/FromPointer/The-AWK-Book-cn/blob/master/chapter-one.rst)

###2. [The 2nd chapter](https://github.com/FromPointer/The-AWK-Book-cn/blob/master/chapter-two.rst)

###3. Pattern

Patterns are arbitrary Boolean combinations (with ! || &&)  of  regular expressions  and  relational  expressions.

#####3.1 Regular Expression
 
    1. /re/ is  a  constant regular  expression; 
    2. any string (constant or variable) may be used as a regular expression, except in  the  position  of  an  isolated  regular expression in a pattern.
    3. Search Patterns:
    Simple Patterns: 
      /The/ -- This searches for any line that contains the string "The"
      /^The/ -- This matches any line that begins with the string "The"
      /The$/ -- This matches any line that ends with the string "The"
    
    Character Sets Pattern:
      /[Tt]he/ -- This matches any line that contains the string "The" or "the". And `[]` can indicate a range. For example, `[A-Z]` means contains characters from `A` to `Z`.
      /[^Tt]he/ -- This matches any line that doesn't contain the string "The" or "the". `^` in `[]` means except for all characters in `[]`.
      | -- A vertical bar allows regular expression to be logically OR'ed.
      . -- A dot(.) allows "wildcard" matching, meaning it can be used to specify any arbitrary character.
      * -- It matches zero or more repetions of the previous character or expression.
      ? -- It exactly matches zero or one occurences of the previous regular expression.
      {num1, num2} -- The brackets matches the occurences from num1 to num2 of the previuos regular expression

 

#####3.2 Relational Expression

A relational expression is one of the following:

1. expression matchop regular-expression,   where a matchop is either ~ (matches) or !~ (does not match)
2. expression relop expression,   where  a  relop  is  any  of  the  six relational operators in C
3. expression in array-name
4. (expr,expr,...) in array-name

A conditional is an  arithmetic expression, a relational expression, or a Boolean combination of these.


###4. Action

 An  action  is a sequence of statements.  A statement can be one of the following:

              if( expression ) statement [ else statement ]
              while( expression ) statement
              for( expression ; expression ; expression ) statement
              for( var in array ) statement
              do statement while( expression )
              break
              continue
              { [ statement ... ] }
              expression              # commonly var = expression
              print [ expression-list ] [ > expression ]
              printf format [ , expression-list ] [ > expression ]
              return [ expression ]
              next                    # skip remaining patterns on this input line
              nextfile                # skip rest of this file, open next, start at top
              delete array[ expression ]# delete an array element
              delete array            # delete all elements of array
              exit [ expression ]     # exit immediately; status is expression

       Statements are terminated by semicolons, newlines or right braces.   An
       empty  expression-list stands for $0.  String constants are quoted " ",
       with the usual C escapes recognized within.  Expressions take on string
       or numeric values as appropriate, and are built using the operators + -
       * / % ^ (exponentiation), and concatenation (indicated by white space).
       The  operators  !  ++  -- += -= *= /= %= ^= > >= < <= == != ?: are also
       available in expressions.  Variables may  be  scalars,  array  elements
       (denoted  x[i])  or  fields.   Variables  are  initialized  to the null
       string.  Array subscripts may be any string, not  necessarily  numeric;
       this allows for a form of associative memory.  Multiple subscripts such
       as [i,j,k] are permitted; the constituents are concatenated,  separated
       by the value of SUBSEP.

       The  print statement prints its arguments on the standard output (or on
       a file if >file or >>file is present or on a pipe if |cmd is  present),
       separated  by the current output field separator, and terminated by the
       output record separator.  file and cmd may be literal names  or  paren-
       thesized  expressions;  identical string values in different statements
       denote the same open file.  The printf statement formats its expression
       list  according  to  the format (see printf(3)).  The built-in function
       close(expr) closes the  file  or  pipe  expr.   The  built-in  function
       fflush(expr) flushes any buffered output for the file or pipe expr.



###5. Special Variable

 Variable names with special meanings:

       CONVFMT
              conversion format used when converting numbers (default %.6g)

       FS     regular expression used to separate  fields;  also  settable  by
              option -Ffs.

       NF     number of fields in the current record

       NR     ordinal number of the current record

       FNR    ordinal number of the current record in the current file

       FILENAME
              the name of the current input file

       RS     input record separator (default newline)

       OFS    output field separator (default blank)

       ORS    output record separator (default newline)

       OFMT   output format for numbers (default %.6g)

       SUBSEP separates multiple subscripts (default 034)

       ARGC   argument count, assignable

       ARGV   argument  array, assignable; non-null members are taken as file-
              names

       ENVIRON
              array of environment variables; subscripts are names.
              
  
  ###7. Functions
  
  The  mathematical  functions  exp,  log,  sqrt, sin, cos, and atan2 are
       built in.  Other built-in functions:

       length the length of its argument taken as a string, or  of  $0  if  no
              argument.

       rand   random number on (0,1)

       srand  sets seed for rand and returns the previous seed.

       int    truncates to an integer value

       substr(s, m, n)
              the n-character substring of s that begins at position m counted
              from 1.

       index(s, t)
              the position in s where the string t occurs, or  0  if  it  does
              not.

       match(s, r)
              the position in s where the regular expression r occurs, or 0 if
              it does not.  The variables RSTART and RLENGTH are  set  to  the
              position and length of the matched string.

       split(s, a, fs)
              splits  the  string s into array elements a[1], a[2], ..., a[n],
              and returns n.  The separation is done with the regular  expres-
              sion  fs  or with the field separator FS if fs is not given.  An
              empty string as field separator splits the string into one array
              element per character.

       sub(r, t, s)
              substitutes t for the first occurrence of the regular expression
              r in the string s.  If s is not given, $0 is used.

       gsub   same as sub except that all occurrences of the  regular  expres-
              sion  are  replaced;  sub and gsub return the number of replace-
              ments.

       sprintf(fmt, expr, ... )
              the string resulting from formatting expr ...  according to  the
              printf(3) format fmt

       system(cmd)
              executes cmd and returns its exit status

       tolower(str)
              returns  a copy of str with all upper-case characters translated
              to their corresponding lower-case equivalents.

       toupper(str)
              returns a copy of str with all lower-case characters  translated
              to their corresponding upper-case equivalents.
