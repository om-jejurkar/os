Q.2 Write a C program to implement the shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating 
the child process. Additionally it should interpret the following ‘list’ commands as
myshell$ list f dirname :- To print names of all the files in current directory. 
myshell$ list n dirname :- To print the number of all entries in the current directory
#include<stdio.h>
#include<unistd.h>
#include<string.h>
#include<stdlib.h>
#include<dirent.h>
void list(char *tok2, char *tok3)
{
DIR *dp;
int c =0;
struct dirent *dir;
dp = opendir(tok3);
if(dp == 0)
printf("%s directory not exit",tok3);
else
{
if(strcmp(tok2,"n")==0)
{
while((dir=readdir(dp))!= NULL)
c++;
printf("no of files directory : %d ",c);
}
if(strcmp(tok2,"f")==0)
{
while((dir=readdir(dp))!= NULL)
printf("%s \n ",dir->d_name);
}
}
} 
int main(int argc , char * argv[])
{
char tok1[20],tok2[20],tok3[20];
int choice,f;
char cmd[40];
while(1)
{
printf("\n Myshell$");
gets(cmd);
if(strcmp(cmd, "exit")==0)
exit(0);
int choice = sscanf(cmd,"%s%s%s",&tok1,&tok2,&tok3);
if(choice==3)
{
if(strcmp(tok1,"list")==0)
list(tok2,tok3);
continue;
}
}
}
