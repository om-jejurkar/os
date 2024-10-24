Q.2 Write a programto implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating the 
child process. Additionally it should interpret the following commands. 
myshell$ search f filename pattern :- To display first occurrence of pattern in the file.
#include<stdio.h>
#include<unistd.h>
#include<string.h>
#include<stdlib.h>
void search(char *tok2,char *tok3,char *tok4)//tok2:command tok3:pattern tok4:Textfilename
{
FILE *fp;
int lineno=0,count=0;
char str[50];
fp=fopen(tok4,"r");
if(fp==NULL)
{
printf("File does not exist");
exit(0);
}
else
{
if(strcmp(tok2,"f")==0)//First occurance of pattern
{
while(!feof(fp))
{
fgets(str,50,fp);
lineno++;
if(strstr(str,tok3))
{
printf("First occurance of '%s' is on line : %d\n",tok3,lineno);
break;
}
}
}
}
}
void main(int argc,char *argv[])
{
char cmd[20],tok1[20],tok2[20],tok3[20],tok4[20];
while(1)
{
printf("\nMyShell$:");
gets(cmd);
if(strcmp(tok1,"exit")==0)
exit(0);
int ch=sscanf(cmd,"%s%s%s%s",tok1,tok2,tok3,tok4);
if(ch==4)
{
if(strcmp(tok1,"search")==0)
{
search(tok2,tok3,tok4);
continue;
}
}
}
}
