# Ex-5-RECOGNITION-OF-THE-GRAMMAR-anb-where-n-10-USING-YACC
RECOGNITION OF THE GRAMMAR(anb where n>=10) USING YACC
# Date:27-10-2025
# Name: Vedagiri Indu Sree
# Aim:
To write a YACC program to recognize the grammar anb where n>=10.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
# PROGRAM:
expr5.l
```
%{
#include "y.tab.h"
%}

%%
a   { return A; }
b   { return B; }
\n  { return '\n'; }
.   { return yytext[0]; }
%%

int yywrap() {
    return 1;
}
```
expr5.y
```
%{
#include <stdio.h>
#include <stdlib.h>
int count = 0;  // to count number of a's
%}

%token A B

%%
start:
    sequence B '\n' {
        if (count >= 10) {
            printf("Valid string: %d a's followed by b\n", count);
        } else {
            printf("Invalid: Less than 10 a's\n");
        }
        count = 0; // reset for next input
    }
    ;

sequence:
    A { count++; }
  | sequence A { count++; }
  ;
%%

int main() {
    printf("Enter a string (aⁿb where n >= 10):\n");
    return yyparse();
}

void yyerror(const char *msg) {
    printf("Syntax error: %s\n", msg);
}
```
# OUTPUT
C:\Dev-Cpp\TDM-GCC-64\bin>flex expr5.l

C:\Dev-Cpp\TDM-GCC-64\bin>bison -dy expr5.y

C:\Dev-Cpp\TDM-GCC-64\bin>gcc y.tab.c lex.yy.c -w

C:\Dev-Cpp\TDM-GCC-64\bin>a.exe
Enter a string (aΓü┐b where n >= 10):
aaaaaaaaaaaaab
Valid string: 13 a's followed by b
C:\Dev-Cpp\TDM-GCC-64\bin>flex expr5.l

C:\Dev-Cpp\TDM-GCC-64\bin>bison -dy expr5.y

C:\Dev-Cpp\TDM-GCC-64\bin>gcc y.tab.c lex.yy.c -w

C:\Dev-Cpp\TDM-GCC-64\bin>a.exe
Enter a string (aΓü┐b where n >= 10):
aab
Invalid: Less than 10 a's

# RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.
