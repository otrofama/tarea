%{
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int dir;
void newDir();

void yyerror();
extern FILE* yyin;
%}

%union
{
//	char* sval;
	char sval[100];
	struct
	{
//		char* code;
		char code[100];
		int type;
		int val;
	}num;
	struct
	{
//		char* code;
		char code[100];
	}type;
}

%token<sval> ID
%token LPAR RPAR NL
%token<num> NUM

%left MAS
%left MUL

%type<type> exp term fac

%start program

%%

program: program list {
			printf("P->PL\n");
			} | list {
				printf("P->L\n");
			};

list: exp NL{
		printf("L->E NL\n");
		};

exp:	exp MAS term {
		newDir();
//		$$.code=(char*)realloc($$.code,2*sizeof(char));
		strcpy($$.code,"t");
		char dr[100];
		sprintf(dr,"%d",dir);
		strcat($$.code,dr);
		printf("%s = %s + %s", $$.code,$1.code,$3.code);
		printf("E->E+T\n");
		}
		| term {
			$$ = $1;
			printf("E->T\n");
		};

term:	term MUL fac{
		newDir();
//		$$.code=(char*)realloc($$.code,2*sizeof(char));
		strcpy($$.code,"t");
		char dr[100];
		sprintf(dr,"%d",dir);
		strcat($$.code,dr);
		printf("%s = %s * %s", $$.code,$1.code,$3.code);
		printf("T->T*F\n");
		}
		| fac{
			$$=$1;
			printf("T->F\n");
		};

fac: LPAR exp RPAR{
		$$=$2;
		printf("F->(E)\n");
		}
		| ID{
			strcpy($$.code,$1);			
			printf("F->id\n");
		} |NUM {
//			$$.code=(char*)realloc($$.code,2*sizeof(char));
			strcpy($$.code,$1.code);
			printf("F->num\n");
		}
%%

void yyerror()
{
	printf("Error sintáctico.\n");
}
void newDir()
{
	dir++;
}
		

int main(int argc, char** argv)
{
	FILE* file;
	if(argc>1)
	{
		file = fopen(argv[1],"r");
		if(!file)
		{
			perror("No se pudo abrir el archivo");
			exit(0);
		}
		else
		{
			yyin = file;
			yyparse();
			
		}
		fclose(yyin);
	}
	else
		printf("No se ingresó archivo.\n");
	return 0;
}





























