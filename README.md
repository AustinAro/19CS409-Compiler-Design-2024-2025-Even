# Ex. No : 1	
# IMPLEMENTATION OF SYMBOL TABLE 
# Name: Austin Aro A
## Register Number : 212224040038
## Date : 19-11-2026

## AIM   
To write a C program to implement a symbol table.

## ALGORITHM
1.	Start the program.
2.	Get the input from the user with the terminating symbol ‘$’.
3.	Allocate memory for the variable by dynamic memory allocation function.
4.	If the next character of the symbol is an operator then only the memory is allocated.
5.	While reading, the input symbol is inserted into symbol table along with its memory address.
6.	The steps are repeated till ‘$’ is reached.
7.	To reach a variable, enter the variable to be searched and symbol table has been checked for corresponding variable, the variable along with its address is displayed as result.
8.	Stop the program. 

## PROGRAM
```
    #include <stdio.h>
    #include <stdlib.h>
    #include <ctype.h>
    #include <string.h>
    
    #define MAX_EXPRESSION_SIZE 100
    
    int main() {
        int i = 0, j = 0, x = 0, n;
        void *add[20];   // store addresses
        char b[MAX_EXPRESSION_SIZE], d[20], c;
    
        printf("Enter the Expression terminated by $: ");
        while ((c = getchar()) != '$' && i < MAX_EXPRESSION_SIZE - 1) {
            b[i++] = c;
        }
        b[i] = '\0';   // Null terminate
        n = i - 1;
    
        printf("Given Expression: %s\n", b);
    
        printf("\nSymbol Table\n");
        printf("Symbol\taddr\ttype\n");
    
        for (j = 0; j <= n; j++) {
            c = b[j];
            if (isalpha((unsigned char)c)) {
                if (j == n) {
                    void *p = malloc(sizeof(char));
                    add[x] = p;
                    d[x] = c;
                    printf("%c\t%p\tidentifier\n", c, p);
                    x++;
                } else {
                    char ch = b[j + 1];
                    if (ch == '+' || ch == '-' || ch == '*' || ch == '=' || ch == '/' || ch == ';') {
                        void *p = malloc(sizeof(char));
                        add[x] = p;
                        d[x] = c;
                        printf("%c\t%p\tidentifier\n", c, p);
                        x++;
                    }
                }
            }
        }
    
        return 0;
    }
```

## OUTPUT 

<img width="351" height="157" alt="Screenshot 2026-11-19 231114" src="https://github.com/user-attachments/assets/65aad777-a6a6-4339-91cd-d27d93ff72f0" />


## RESULT
The program to implement a symbol table is executed and the output is verified.

-----

# Ex. No : 2	
# GENERATION OF LEXICAL TOKENS LEX/FLEX TOOL
# Name: Austin Aro A
## Register Number :212224040038
## Date : 19/11/26

## AIM   
To write a lex program to implement lexical analyzer to recognize a few patterns.

## ALGORITHM
1.	Start the program.
2.	Lex program consists of three parts.
    a.	Declaration %%
    b.	Translation rules %%
    c.	Auxilary procedure.
3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form
    a.	P1 {action}
    b.	P2 {action}
    c.	…
    d.	…
    e.	Pn {action}
5.	Write a program in the vi editor and save it with .l extension.
6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

## PROGRAM
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>
int isKeyword(char buffer[]) {
char keywords[5][10] = {"if", "else", "while", "for", "int"};
for (int i = 0; i < 5; ++i) {
if (strcmp(buffer, keywords[i]) == 0) {
return 1;
}
}
return 0;
}
int main() {
char ch;
char operators[] = "+-*/=;";
char buffer[15];
int i = 0;
printf("Enter your input :\n");
while ((ch = getchar()) != EOF) {
if (strchr(operators, ch) != NULL) {
if (i > 0) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
i = 0;
}
printf("Operator: %c\n", ch);
} else if (isalnum(ch)) {
if (i < 14) {
buffer[i++] = ch;
}
} else if ((ch == ' ' || ch == '\n' || ch == '\t') && i > 0) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
i = 0;
}
if (i > 0 && isalpha(buffer[i-1]) && isdigit(ch)) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
}
i = 0;
buffer[i++] = ch;
}
}
if (i > 0) {
buffer[i] = '\0';
if (isKeyword(buffer)) {
printf("Keyword: %s\n", buffer);
} else if (isalpha(buffer[0]) && strlen(buffer) == 1) {
printf("Identifier: %s\n", buffer);
} else if (isdigit(buffer[0])) {
printf("Number: %s\n", buffer);
}
}
return 0;
}
```
## OUTPUT 

<img width="290" height="193" alt="Screenshot 2026-11-19 231907" src="https://github.com/user-attachments/assets/0edb4421-67bd-4ab8-8553-b617dd2b1d3e" />

## RESULT
The lexical analyzer is implemented using lex and the output is verified.

-----

# Ex. No : 3	
# RECOGNITION OF A VALID ARITHMETIC EXPRESSION THAT USES
# Name: Austin Aro A
## Register Number : 212224040038
## Date :19/11/2026

## AIM   
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.

## PROGRAM
~~~
#include <stdio.h>
#include <ctype.h>
#include <string.h>

char expr[100];
int pos = 0;

int E();
int F();
void error();

int F() {
    if (isdigit(expr[pos])) {
        while (isdigit(expr[pos])) pos++;
        return 1;
    }
    else if (isalpha(expr[pos])) {
        while (isalnum(expr[pos])) pos++;
        return 1;
    }
    else if (expr[pos] == '(') {
        pos++;
        if (E()) {
            if (expr[pos] == ')') {
                pos++;
                return 1;
            }
        }
        return 0;
    }
    return 0;
}

int E() {
    if (!F()) return 0;
    while (expr[pos] == '+' || expr[pos] == '-' || expr[pos] == '*' || expr[pos] == '/') {
        pos++;
        if (!F())
            return 0;
    }
    return 1;
}

void error() {
    printf("\nError: Invalid arithmetic expression\n");
}

int main() {
    printf("Enter the expression:\n");
    fgets(expr, sizeof(expr), stdin);
    expr[strcspn(expr, "\n")] = '\0';
    pos = 0;
    if (E() && expr[pos] == '\0') {
        printf("\nValid arithmetic expression\n");
    } else {
        error();
    }
    return 0;
}
~~~

## OUTPUT 
## Valid Expression
<img width="278" height="103" alt="Screenshot 2026-11-19 232224" src="https://github.com/user-attachments/assets/70328a7a-db36-4c89-96c7-3a8020256647" />

## Invalid Expression
<img width="299" height="116" alt="Screenshot 2026-11-19 232246" src="https://github.com/user-attachments/assets/052b4d91-7477-40a0-8ddc-65f295570f12" />

## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified

-----

# Ex. No : 4	
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
# Name: Austin Aro A
## Register Number : 212224040038
## Date : 19/11/2026

## AIM   
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.

## PROGRAM
variable_test.l
```
%{
#include "variable_test.tab.h"
%}

%%
"int"     { return INT; }
"float"   { return FLOAT; }
"double"  { return DOUBLE; }
","       { return ','; }
";"       { return ';'; }
[a-zA-Z][a-zA-Z0-9]* { printf("\nIdentifier is %s", yytext); return ID; }
[ \t\r\n]     { /* skip whitespace and newlines */ }
.         { /* ignore unrecognized characters */ }
%%

int yywrap() { return 1; }
```
variable_test.y
```
%{
#include <stdio.h>
%}
%token ID INT FLOAT DOUBLE
%%
D : T L ';'    { printf("Valid Declaration\n"); }
  ;
L : L ',' ID   | ID
  ;
T : INT | FLOAT | DOUBLE
  ;
%%
extern FILE *yyin;
int main() {
    do {
        yyparse();
    } while (!feof(yyin));
    return 0;
}
void yyerror(char *s) { fprintf(stderr, "Error: %s\n", s); }
```

## OUTPUT 

<img width="389" height="205" alt="Screenshot 2025-11-21 103124" src="https://github.com/user-attachments/assets/cf1e5d80-752b-494b-988c-31143df89c34" />

## RESULT
A  YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.

-----

# Ex. No : 5	
# RECOGNITION OF THE GRAMMAR (a<sup>n</sup>b where n>=10) USING YACC
# Name: Austin Aro A
## Register Number : 212224040038
## Date :19/11/2026

## AIM   
To write a YACC program to recognize the grammar a<sup>n</sup>b where n>=10.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
 
## PROGRAM
~~~
#include <stdio.h>
#include <string.h>
int main() {
    char str[100];
    int i = 0;
    printf("Enter the string: ");
    scanf("%s", str);
    if (str[0] != 'a') {
        printf("Invalid: string must start with 'a'\n");
        return 0;
    }
    for (i = 1; str[i] != '\0'; i++) {
        if (str[i] != 'b') {
            printf("Invalid: all characters after 'a' must be 'b'\n");
            return 0;
        }
    }
    int b_count = strlen(str) - 1;
    if (b_count >= 10) {
        printf("Valid string: matches anb where n >= 10\n");
    } else {
        printf("Invalid: number of 'b's is less than 10 (found %d)\n", b_count);
    }
    return 0;
}
~~~

## OUTPUT 
![443595619-52a983bc-e57e-402b-89d4-b07580e3553a](https://github.com/user-attachments/assets/2d87c6a2-6642-41e3-b78d-edf8c894f75c)

## RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.

-----

# Ex. No : 6	
# IMPLEMENTATION OF THE BACK END OF THE COMPILER 
## Register Number : 212224040038
## Date : 19/11/2026

## AIM   
To write a program to implement the back end of the compiler.

# ALGORITHM
1. Start the program.
2. Get the three variables from statements and stored in the text file k.txt.
3. Compile the program and give the path of the source file.
4. Execute the program.
5. Target code for the given statement is produced.
6. Stop the program.

# PROGRAM

## cd6.c
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int main() {
    char line[100], var[10], op1[10], op2[10], res[10], op;
    char filename[50];
    FILE *fp;
    int reg = 0;

    printf("Enter the filename of the intermediate code: ");
    scanf("%s", filename);

    fp = fopen(filename, "r");
    if (fp == NULL) {
        printf("Error: Could not open file.\n");
        return 1;
    }

    printf("\nIntermediate Code:\n\n");

    while (fgets(line, sizeof(line), fp)) {
        printf("\t\t%s", line);
    }

    rewind(fp);

    printf("\n\n\tStatement\t\tTarget Code\n\n");

    while (fgets(line, sizeof(line), fp)) {
        // Remove newline if exists
        line[strcspn(line, "\n")] = 0;

        // Example format: t1 = a + b
        if (sscanf(line, "%s = %s %c %s", res, op1, &op, op2) == 4) {
            printf("\t%s\t\tMOV %s, R%d\n", line, op2, reg);
            printf("\t\t\t\t");

            if (op == '+')
                printf("ADD ");
            else if (op == '-')
                printf("SUB ");
            else if (op == '*')
                printf("MUL ");
            else if (op == '/')
                printf("DIV ");
            else
                printf("OP? ");

            printf("%s, R%d\n\n", op1, reg);
            reg++;
        }
    }

    fclose(fp);
    return 0;
}
```

## cd6.txt

```
t1 = a + b
t2 = t1 - c
```

# OUTPUT

<img width="536" height="488" alt="ex6op" src="https://github.com/user-attachments/assets/96f86230-17ed-494b-b5fd-d399378abfc1" />

# Result
The back end of the compiler is implemented successfully, and the output is verified.
