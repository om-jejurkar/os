Q.1 Write the simulation program for demand paging and show the page scheduling and total number of page faults according the LRU page replacement algorithm. Assume 
the memory of n frames. 
Reference String : 8, 5, 7, 8, 5, 7, 2, 3, 7, 3, 5, 9, 4, 6, 2
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

Q.2 Write a programto implement the shell. It should display the command prompt 
“myshell$”. Tokenize the command line and execute the given command by creating the child process. Additionally it should interpret the following commands. 
myshell$ search f filename pattern :- To display first occurrence of pattern in the file. 
myshell$ search c filename pattern :- To count the number of occurrence 
of pattern in the file.
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
if(strcmp(tok2,"c")==0)//Total number of occurances of pattern
{
while(!feof(fp))
{
fgets(str,50,fp);
if(strstr(str,tok3))
{
count++;
}
}
printf("Total number occurance of pattern(%s) is : %d\n",tok3,count);
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
if
(strcmp
(tok1
,"search")==
0
)
{
search
(tok2
,tok3
,tok4);
continue
;
}
}
}
}
