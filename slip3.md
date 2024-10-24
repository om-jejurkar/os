Q.1 Write the simulation program to implement demand paging and show the page scheduling and total number of page faults according to the LRU (using counter method) 
page replacement algorithm. Assume the memory of n frames. 
Reference String : 3,5,7,2,5,1,2,3,1,3,5,3,1,6,2
#include<stdio.h>
int pf=0,pg;
int f,frame[5],ref[50],victim=0,time[50];
int searchpage(int p)
{
int i;
for(i=0;i<f;i++)
if(frame[i]==p)
return i;
return -1;
}
int selectvictim()
{
int min=0,i;
for(i=1;i<f;i++)
{
if(time[i]<time[min])
min=i;
}
return min;
}
void main()
{
int i;
printf("\n Enter the no. of frames -: ");
scanf("%d",&f);
for(i=0;i<f;i++)
frame[i]=-1;
for(i=0;i<f;i++)
time[i]=-1;
printf("\n Enter the no. of pages -: ");
scanf("%d",&pg);
printf("\n Enter the page(reference string) -: ");
for(i=0;i<pg;i++)
scanf("%d",&ref[i]);
for(i=0;i<pg;i++)
{
int k,j;
k=searchpage(ref[i]);
if(k==-1)
{
pf++;
k=selectvictim();
frame[k]=ref[i];
}
time[k]=i;
printf("\n pg=%d |",ref[i]);
for(j=0;j<f;j++)
printf("\t%d",frame[j]);
}
printf("\n Page Fault is -:%d",pf);
}

Q.2 Write a programto implement the toy shell. It should display the command prompt “myshell$”. Tokenize the command line and execute the given command by creating 
the child process. Additionally it should interpret the following commands.
count c filename :- To print number of characters in the file.
count w filename :- To print number of words in the file. 
count l filename :- To print number of lines in the file.
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
