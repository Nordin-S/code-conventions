<style type="text/css">
body {
    counter-reset: h1
}

h1 {
    counter-reset: h2
}

h2 {
    counter-reset: h3
}

h3 {
    counter-reset: h4
}

/* h1:before {
    counter-increment: h1;
    content: counter(h1) ". "
} */

h2:before {
    counter-increment: h2;
    content: counter(h2) ". "
}

h3:before {
    counter-increment: h3;
    content: counter(h2) "." counter(h3) ". "
}
h4:before {
    counter-increment: h4;
    content: counter(h2) "." counter(h3) "."counter(h4) ". "
}

h2 { margin-left: 10px; }
h3 { margin-left: 20px; }
h4 { margin-left: 30px; }
</style>

#Java Conventions
An somewhat condensed but still informative version of [Oracle's Code Conventions for Java](https://www.oracle.com/technetwork/java/codeconventions-150003.pdf), summarized by [Nordin Suleimani](https://github.com/Nordin-S).

---
## Why Code Conventions
*They are important! ¯\\_(ツ)_/¯*

- 80% of the lifetime cost of a piece of software goes to maintenance.
- Hardly any software is maintained for its whole life by the original author.
- Code conventions improve the readability of the software, allowing engineers to
understand new code more quickly and thoroughly.
- If you ship your source code as a product, you need to make sure it is as well packaged
and clean as any other product you create.

---
## File Names
*Commonly used file suffixes and names.*

### File Suffixes
*Used by JavaSoft*
1. source.java
2. bytecode.class

### Common File Names
*Frequently used*
1. GNUmakefile  used to build
2. README used to summarize directory contents

---
## File Content Organization 
*Optionally commented sections seperated by blank lines, no more than 2000 lines!*

### Java Source Files
 *Contains a single public class or interface. If has association with private classes and interfaces, they can be added after public class or interface.*

Ordering of source file content
- Beginning comments
    *c-style comments*
    ``` java
    /*
    * Classname
    * Description
    * Date & Version info
    *
    * Copyright notice
    */
    ```
- Package and import statements
    *First non-comment lines, usually package followed by import statements*
    ``` java
    package java.awt;
    import java.applet.Applet;
    import java.net.*;
    ```
- Class and interface declaration
   *Parts of class or interface declaration, order !important*

    | # | Part of Class/Interface Declaration | Notes |
    | --------- | --------- | -------- |
    | 1 | Class/interface documentation comment ==/\*\*...*/==||
    | 2 | class or interface statement ||
    | 3 | Class/interface implementation ==/\*...*/== comment, if needed | Should contain class- or interface-wide info that was not appropriate in previous comment |
    | 4 | Class(static) variables | Order: public, protected, private. |
    | 5 | Instance variables | Order: public, protected, private.|
    | 6 | Constructors ||
    | 7 | Methods | Should be grouped by functionality, not scope or accessibility. Goal: easier to read/understand. |

---
## Indentation
*Use four spaces for indentation. Tabs every 8 spaces.*

### Line Length
*At most 80 characters. Examples in documentation no more than 70 chars.*

### Wrapping Lines
*General breakage principles:*
- After a comma.
- Before an operator.
- Prefer higher-level breaks to lower-level breaks.
- Align expression line breakage at the same level as beginning of expression.
- If above rules lead to confusing code or squished code to right margin, indent by 8 spaces instead.

---
## Comments
*Two kinds of comments: Implementation comments(like C++) and documentation comments("doc comments", Java-only, can be extracted to HTML using javadoc).*

1. Implementation: ==/\*...*/== (describing particular implementation or commenting out block of code, also used as one liner/trailing), and ==//== (end of line comment)
2. Documentation comments: ==/\*\*...*/== (Specification description)

> Note:
>: Avoid trying to add extra character to make you comments stick out. Code should be self explanatory, if possible consider rewriting code instead of adding comments. Comments should be at the same level as code they are commenting.

### Implementation Comment Formats
*Four styles: block, single-line, trailing and end-of-line.*

#### Block Comments
*Used to provide desription of files, methods, data structures and algorithms. Can also be used within methods, functions, and other places. Indent to the same level of commented code.*

```java
    /**
    * Block comment.
    */
```

#### Single-Line Comments
*Preceded with blank line. Indent to the same level of commented code.*
```java
    if (condition) {
        /* Handle condition. */
        ...
    }
```

#### Trailing Comments
*Keep them short, indent to far right, keep consecutive line comments on the same indent level.*
```java
    if (a == 2) {
        return TRUE;                /* special case */
    } else {
        return isprime(a);          /* works only for odd a */
    }
```

#### End-Of-Line Comments
*==//== can comment out complete line or partially end of line. Can be used for consecutive code commenting out, don't use of consecutive text commenting!*

```java
    if (a == 2) {
        return TRUE; //true
    }//else {
    //     return isprime(a);
    // }
```
### Documentation Comments
*See previous information regarding doc comments and code Examples at the end of this document.*

> Recommendation:
>: Refer to [How to Write Doc Comments for Javadoc](http://java.sun.com/products/jdk/javadoc/writingdoccomments.html) for further details.

---
## Declarations
### Number Per Line
*One declaration per line.*
```java
    int level;  // encourages commenting
    int size;   // next comment
```

> Note:
>: Also accaptable (tabs)
>    ```java 
>    int         level;          // indentation level
>    int         size;           // size of table
>    Object      currentEntry;   // currently selected table entry ```

### Placement
*Put declarations only at the beginning of code blocks =="{" and "}"==*
```java
    void MyMethod() {
        int int1; // beginning of method block

        if (condition) {
            int int2; // beginning of "if" block
            ...
        }
    }
```

Note:
: Avoid hiding higher level declarations using local declarations. Count hidden by if block count declaration.
```java
    int count;
    ...
    func() {
        if (condition) {
            int count; // AVOID!
        ...
        }
        ...
    }
```

### Initialization
*Declare and initialize local variables in one go if not dependent on later computation.*

### Class and Interface Declarations
*Follow following formatting rules*
- No space between method name and =="(" and ")"==
- Open brace =={== on same line as declaration.
- Match closing brace ==}== to open brace indent level on it's own line.
- Methods are seperated by blank lines.

---
## Statements
### Simple Statements
*One statement per line! Also avoid comma seperated statement grouping.*

### Compound Statements
*List of statements =={ statements }==*
- Enclosed statements should be indented on more level than compound statements.
- Opening brace at the of the line that begins compound statement, closing brace on new line at the same indent level as it's opening brace.
- Braces around all statements, even singletons. 

### return statements
*Use parantheses with return statements only when there is an abvious need.*

### if, if-else, if-else-if-else Statements
**Good form:**
```java
    if (condition) {
        statements;
    }
    if (condition) {
        statements;
    } else {
        statements;
    }
    if (condition) {
        statements;
    } else if (condition) {
        statements;
    } else if (condition) {
        statements;
    }
```
Note:
: Do not omit =={ }== even when you have only one line statements.

### for Statements
**Good form:**
```java
    for (initialization; condition; update) {
        statement;
    }
```

*Empty for statement form(keep simple, max three comma seperations):*
```java
    for (init01, init02, init03; condition; update01, update02, update03)
```

### while Statements
**Good form:**
```java
    while (condition) {
        statements;
    }

    while (condition) // empty while form
```
### do-while Statements
**Good form:**
```java
    do {
        statements;
    } while (condition)
```

### switch Statements
**Good form:**
```java
    switch (condition) {
        case ABC:
            statements;
            /* falls through */

        case DEF:
            statements;
            break;

        default:
            statements;
            break;
    }
```
Note:
: Use fall comment when fall through is intended. Do not avoid default: and corresponding break;, this is to avoid possible future bugs.

### try-catch Statements
**Good form:**
```java
    try {
        statements;
    } catch (ExceptionClass e) {
        statements;
    }
```
---
## White Space
### Blank Lines
*Increases readability*

Two blank lines:
: - Between sections of a source file
  - Between class and interface definitions

One blank line:
: - Between methods
  - Between local variables in a method and its first statement
  - Before a block, or single-line comments
  - Between logical sections inside a method to improve readability

### Blank Spaces
**Usage circumstances:**
- Keyword followed by parenthisis should be seperated by a space.
``` java
    while (true)

    method(param) // not space for methods
```
- Blank space after commas in argument lists.
- Binary operators, except for dot operator use space between operands. follow following form
```java
    a += c + d;
    a = (a + b) / (c * d);
    while (d-- != s++) {
        n++;
    }
    prints("size is " + foo + "\n");
```
- Space between for expressions
```java
    for (expr1; expr2; expr3)
```
- Casts followed by a blank space
```java
    myMethod((byte) aNum, (Object) x);
    myFunc((int) (cp + 5), ((int) (i + 3)) + 1);
```

---
## Naming Conventions
| Identifier Type | Rules | Examples |
| --- | --- | --- |
| Classes | Nouns, no acronyms(if not a standard), simple descriptiv, CamelCase with first letter Capitalized | class Raster; class ImageSprite; |
| Interfaces | Like classes | interface RasterDelegate; |
| Methods | Verbs, camelCase with first letter lowercase | run(); runFast(); |
| Variables | Short and descriptive, one letter only for throw away variables(i, n, ...), camelCase | int i; char *cp; float myWidth; |
| Constants | Uppercase with words seperated with "_" | int MIN_WIDTH = 4; |

---
## Programming Practices
### Providing Acces to Instance and Class Variables
*Keep instance and class variables private if you don't have good reason for otherwise.*

### Referring to Class Variables and Methods
*Avoid using object to acces class (static) variable or method.*
```java
    classMethod();          //OK
    AClass.classMethod();   //OK

    anObject.classMethod;   //AVOID!
```

### Constants
*Numerical constants (literals) should not be coded directly, except for -1, 0 amd 1.*

### Variable Assignments
**Avoid:**
```java
    foobar.fChar = barFoo.lChar = 'c'; //AVOID, sharing same value in a single statement

    if (c++ = d++) {            //AVOID, can be confused with equality
        ...
    }

    if ((c++ = d++) != 0) {     //This is better
        ...
    }

    d = (a = b + c) + r;        //AVOID, emedded assignments

    a = b + c;                  //Better!
    d = a + r;                  //Better!
```

### Miscellaneaous Practices
- Parentheses:
```java
    if (a == b && c == d)       //AVOID!
    if ((a == b) && (c == d))   //Better!
```

- Returning Values:
```java
    // What is the intent
    if (booleanExpression) {
        return TRUE;
    } else {
        return FALSE;
    }

    return booleanExpression;   //Aha I understand the intent

    //ok..
    if (condition) {
        return x;
    }
    return y;

    return (condition ? x : y); //Ah, makes sense.
```

- Expression before '?' in Conditional Operator
```java
    (x >= 0) ? x : -x;          //binary operator parenthesized, good!
```

- Special Comments, Use XXX in a comment to flag(FIXME, TODO, ...) something that works but is bogus.
```java
    // Doing something great, it kinda works but is bogus, FIXME
    method() {
        ...
    }
```
---
## Code Examples
*The following example shows how to format a Java source file containing a single public class.
Interfaces are formatted similarly.*
```java
    /*
     * %W% %E% Firstname Lastname
     *
     * Copyright (c) 1993-1996 Sun Microsystems, Inc. All Rights Reserved.
     *
     * This software is the confidential and proprietary information of Sun
     * Microsystems, Inc. ("Confidential Information"). You shall not
     * disclose such Confidential Information and shall use it only in
     * accordance with the terms of the license agreement you entered into
     * with Sun.
     *
     * SUN MAKES NO REPRESENTATIONS OR WARRANTIES ABOUT THE SUITABILITY OF
     * THE SOFTWARE, EITHER EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED
     * TO THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
     * PARTICULAR PURPOSE, OR NON-INFRINGEMENT. SUN SHALL NOT BE LIABLE FOR
     * ANY DAMAGES SUFFERED BY LICENSEE AS A RESULT OF USING, MODIFYING OR
     * DISTRIBUTING THIS SOFTWARE OR ITS DERIVATIVES.
     */

    package java.blah;
    import java.blah.blahdy.BlahBlah;

    /**
     * Class description goes here.
     *
     * @version 1.10 04 Oct 1996
     * @author Firstname Lastname
     */
    public class Blah extends SomeClass {
    /* A class implementation comment can go here. */

        /** classVar1 documentation comment */
        public static int classVar1;

        /** classVar2 documentation comment that happens to be
         * more than one line long
         */
        private static Object classVar2;

        /** instanceVar1 documentation comment */
        public Object instanceVar1;

        /** instanceVar2 documentation comment */
        protected int instanceVar2;

        /** instanceVar3 documentation comment */
        private Object[] instanceVar3;

        /**
         * ...method Blah documentation comment...
         */
        public Blah() {
            // ...implementation goes here...
        }

        /**
         * ...method doSomething documentation comment...
         */
        public void doSomething() {
            // ...implementation goes here...
        }

        /**
         * ...method doSomethingElse documentation comment...
         * @param someParam description
         */
        public void doSomethingElse(Object someParam) {
            // ...implementation goes here...
        }
    }
```