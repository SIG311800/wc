#include<stdio.h>
#include<string.h>
#include<stdlib.h>
char az[6],File[66];
int cCount(char file[]);
int wCount(char file[]);
int lCount(char file[]);
int cCount(char file[]){
    FILE *pf=NULL;
    int ccount=0;
    pf=fopen(file,"r");
    if(pf==NULL){printf("寻找失败\n"); exit(-1); }
    char cchar;
    cchar = fgetc(pf);
    while(cchar!=EOF){cchar = fgetc(pf); ccount++;}
    fclose(pf);
    return ccount;
}
int wCount(char file[]){
    FILE *pf=NULL;
    int wcount=0;
    pf=fopen(file,"r");
    if(pf==NULL){ printf("寻找失败\n"); exit(-1);  }
    char wchar;
    wchar = fgetc(pf);
    while(wchar!=EOF){
        if(wchar>='a'&&wchar<='z'||wchar>='A'&&wchar<='Z'||wchar>='0'&&wchar<='9'){
            while(wchar>='a'&&wchar<='z'||wchar>='A'&&wchar<='Z'||wchar>='0'&&wchar<='9'||wchar=='_'){
                wchar=fgetc(pf);
            }
            wcount++;
            wchar=fgetc(pf);
        }
        wchar=fgetc(pf);
    }
    fclose(pf);
    return wcount;
}
int lCount(char file[]){
    FILE *pf=NULL;
    int lcount=0;
    pf=fopen(file,"r");
    if(pf==NULL){ printf("寻找失败(\n");exit(-1);}
    char lchar;
    lchar = fgetc(pf);
    while(lchar!=EOF){
        if(lchar=='\n'){ lcount++; lchar = fgetc(pf); }
        else{lchar = fgetc(pf);}
    } 
    fclose(pf);
    return lcount+1;
}
int main(){
 int c=0,w=0,l=0;
       printf("确定要输入的字母（c为字符数查询,w为词数查询,l为行数查询）\n");
    printf("输入为：");
        scanf("%s",&az);
        if(az[0]=='c'){
           printf("请输入：");
           scanf("%s",&File);
           c=cCount(File);
           printf("文件的字符数为：%d\n",c);    
        }
        if(az[0]=='w'){
            printf("请输入：");
            scanf("%s",&File); 
            w=wCount(File);
            printf("文件的词数为：%d\n",w);  
        }
        if(az[0]=='l'){
            printf("请输入:");
            scanf("%s",&File); 
            l=lCount(File);
            printf("文件的行数为：%d\n",l);               
        }
    system("pause");
    return 0;
}
