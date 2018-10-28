Git is a distributed version control system.
Git is free software.
#include <stdio.h>
#include <string.h>
#include "assignment1.h"
char buff[1000][30], nnew[1000][30];
int i = 0, cnt = 0, last = 0;
char filename[40];
void read_file()
{
    FILE *fp;
    printf("please input a filename:");
    scanf("%s", filename);
    fp = fopen(filename, "r");
    while (fscanf(fp, "%s", buff[i++]) != EOF)
        ;
    fclose(fp);
}
void operate_file()
{
    FILE *fp1;
    fp1 = fopen("output.txt", "w");
    for (int j = 0; j < i; j++)
    {
        int len = strlen(buff[j]);
        int mark = 0;
        int keyword = 0;
        if (buff[j][len - 1] == ',' || buff[j][len - 1] == '.' || buff[j][len - 1] == '!' || buff[j][len - 1] == '?')
        {
            for (int k = 0; k < len - 1; k++)
            {
                nnew[j][k] = buff[j][k];
            }
        }
        else
        {
            for (int k = 0; k < len; k++)
            {
                nnew[j][k] = buff[j][k];
            }
        }
        for (int k = 0; k < 4; k++)
        {
            if (buff[j][len - 1] == p[k])
            {
                mark = 1;
                break;
            }
        }
        for (int k = 0; k < 32; k++)
        {
            if (strcmp(nnew[j], key[k]) == 0)
            {
                keyword = 1;
                break;
            }
        }
        if (mark == 1 && keyword == 0)
        {
            printf("%s\n", buff[j]);
            fprintf(fp1, "%s\n", buff[j]);
            last = 0;
            cnt++;
        }
        else if (keyword == 1)
        {
            if (last == 0)
            {
                printf("%s\n", buff[j]);
                fprintf(fp1, "%s\n", buff[j]);
                last = 0;
                cnt++;
            }
            else
            {
                printf("\n%s\n", buff[j]);
                fprintf(fp1, "\n%s\n", buff[j]);
                last = 0;
                cnt += 2;
            }
        }
        else
        {
            printf("%s ", buff[j]);
            fprintf(fp1, "%s ", buff[j]);
            last = 1;
        }
    }
    printf("Total number of lines is:%2d", cnt);
    fprintf(fp1, "Total number of lines is:%2d", cnt);
    fclose(fp1);
}
int main()
{
    read_file();
    operate_file();
    return 0;
}
https://me.csdn.net/b_i_n_g_o_
