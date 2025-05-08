# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:8/05/2025
# AIM:
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM:
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM:
## arth.l
~~~
%{
#include "y.tab.h"
%}

%%

"="          { printf("\nOperator is EQUAL"); return ASSIGN; }
"+"          { printf("\nOperator is PLUS"); return PLUS; }
"-"          { printf("\nOperator is MINUS"); return MINUS; }
"/"          { printf("\nOperator is DIVISION"); return DIVISION; }
"*"          { printf("\nOperator is MULTIPLICATION"); return MULTIPLICATION; }
[a-zA-Z_][a-zA-Z0-9_]*  { printf("\nIdentifier is %s", yytext); return ID; }
[ \t]        { /* Ignore whitespace */ }
\n           { return 0; }
.            { printf("\nUnknown character: %s", yytext); return yytext[0]; }

%%

int yywrap() {
    return 1;
}
~~~

## arth.y
~~~
%{
#include <stdio.h>

/* Declarations for tokens will come from the lexer (e.g., Flex) */
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION ASSIGN

%%

statement:
    ID ASSIGN E {
        printf("\nValid arithmetic expression\n");
    }
;

E:
    E PLUS ID
  | E MINUS ID
  | E MULTIPLICATION ID
  | E DIVISION ID
  | ID
;

%%

extern FILE *yyin;

int main() {
    yyin = stdin; // Use standard input unless redirected
    yyparse();
    return 0;
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);
}
~~~
# OUTPUT
![Screenshot 2025-05-08 113525](https://github.com/user-attachments/assets/ac1ac838-4eb8-48b9-a592-948c0e02ece4)


# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
