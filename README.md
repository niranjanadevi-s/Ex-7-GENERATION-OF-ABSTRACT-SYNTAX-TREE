~~~
 Ex-7-GENERATION-OF-ABSTRACT-SYNTAX-TREE
CONVERSION OF THE BNF RULES INTO YACC FORM AND GENERATION OF ABSTRACT SYNTAX TREE
Aim: 
To write a program to convert the BNF rules into YACC form and to generate Abstract Syntax Tree.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords, identifiers and relational operators.
4.	Write a program in the vi editor and save it with .y extension.
5.	In the YACC program, the following tasks are performed:
 PROGRAM
 Program:int.
%{
#include "y.tab.h"
#include <stdio.h>
#include <string.h>
int LineNo=1;
%}
main\(\) { return MAIN; }
if { return IF; }
else { return ELSE; }
while { return WHILE; }
int|char|float { return TYPE; }
%%
~~~
## Program: int.y 
~~~
%{
#include <string.h>
#include <stdio.h>
struct stack {
    int items[100];
    int top;
} stk;
int Index=0, tIndex=0, StNo, Ind, tInd;
extern int LineNo;
void push(int data);
int pop();
void AddQuadruple(char op[5],char arg1[10],char arg2[10],char result[10]);
%}
%union {
    char var[10];
}
%left '-' '+'
%left '*' '/'
DESCT: TYPE VARLIST ;
VARLIST: VAR ',' VARLIST
       | VAR ;
ASSIGNMENT: VAR '=' EXPR {
    strcpy(QUAD[Index].op,"=");
    strcpy(QUAD[Index].arg1,$1);
    strcpy(QUAD[Index].arg2,"");
    strcpy(QUAD[Index].result,$3);
    Index++;
} ;
EXPR: EXPR '+' EXPR
    | EXPR '-' EXPR
    | EXPR '*' EXPR
    | EXPR '/' EXPR
    | '-' EXPR
    | '(' EXPR ')'
    | VAR
    | NUM ;

ELSEST: ELSE BLOCK ;

CONDITION: VAR RELOP VAR
         | VAR
         | NUM ;
WHILEST: WHILELOOP ;
WHILELOOP: WHILE '(' CONDITION ')' BLOCK ;
int main(int argc,char *argv[]) {
   printf("\n File not found");
            exit(0);
        }
}void AddQuadruple(char op[5],char arg1[10],char arg2[10],char result[10]) {
    strcpy(QUAD[Index].op,op);
    strcpy(QUAD[Index].arg1,arg1);
    strcpy(QUAD[Index].arg2,arg2);
    strcpy(QUAD[Index].result,result);
    Index++;
}
void yyerror() {
    printf("\n Error on line no:%d",LineNo);
}
~~~
## Program: test.c
~~~
main() {
    int a, b, c;
    if (a < b) {
        a = a + b;
    }
    while (a < b) { 
        a = a + b;
}
~~~
# Output
![image](https://github.com/niranjanadevi-s/Ex-7-GENERATION-OF-ABSTRACT-SYNTAX-TREE/assets/141748873/32f807d2-6a2f-4a8f-a3c8-12827ecc2059)
# Result
Conversion of the BNF rules into YACC form and to generate Abstract Syntax Tree is implemented.


