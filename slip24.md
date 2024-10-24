Q.1 Write a C program to accept n integers to be sorted. Main function creates child process using fork system call. Parent process sorts the integers using bubble sort and 
waits for child process using wait system call. Child process sorts the integers using insertion sort.
#include<stdio.h>
#include<sys/types.h>
#include<unistd.h>
#include<stdlib.h>
int main() {
int pid, retnice; 
printf("press DEL to stop process \n"); 
pid = fork();
for(;;)
{
if(pid == (0))
{
retnice = nice (-5); 
printf("child gets higher CPU priority %d\n", retnice);
sleep(1);
}
else{
retnice = nice (4);
printf("Parent gets lower CPU priority %d\n", retnice);
sleep(1);
}
}
}
/* OUTPUT:
press DEL to stop process 
Parent gets lower CPU priority 4
child gets higher CPU priority -1
Parent gets lower CPU priority 8
child gets higher CPU priority -1
child gets higher CPU priority -1
Parent gets lower CPU priority 12
child gets higher CPU priority -1
Parent gets lower CPU priority 16
child gets higher CPU priority -1
Parent gets lower CPU priority 19
child gets higher CPU priority -1
Parent gets lower CPU priority 19
child gets higher CPU priority -1
Parent gets lower CPU priority 19
child gets higher CPU priority -1
Parent gets lower CPU priority 19
child gets higher CPU priority -1
Parent gets lower CPU priority 19*/
Q.2 Write a C program to implement the toy shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by 
creating the child process. Additionally it should interpret the following commands. count c filename :- To print number of characters in the file. count w filename :- To 
print number of words in the file. count l filename :- To print number of lines in the file.
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include <string.h>
void count(char *tok2 ,char *tok3)
{
int l=0,w=0,c=0;
FILE *fp;
fp = fopen(tok3,"r");
if(fp==NULL)
printf("\n file not exist");
else
{
while(!feof(fp))
{
char ch;
ch = fgetc(fp);
if(ch == ' ' )
w++;
else if(ch == '\n')
{
w++;
l++;
}
else
c++;
}
if(strcmp(tok2,"w") == 0)
printf("\n word count :%d",w);
if(strcmp(tok2,"c") == 0)
printf("\n character count :%d",c);
if(strcmp(tok2,"l") == 0)
printf("\n line count :%d",l);
}
}
int main(int argc , char *argv[])
{
char command[30],tok1[30],tok2[30],tok3[30];
while(1)
{
printf("\n MyShell:");
gets(command);
int ch = sscanf(command,"%s%s%s",tok1,tok2,tok3);
if(ch == 3)
{
if(strcmp(tok1,"count")==0)
count(tok2,tok3);
continue;
}
}
}
