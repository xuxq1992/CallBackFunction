#include <stdio.h>

typedef int student_id;
typedef int student_age;
typedef struct _Student{
    student_id id;
    student_age age;
}Student;

//类型重定义：函数指针类型
typedef bool (*pFun)(Student, Student);


//-----------------------------------------------
//冒泡排序法：能够按AGE或ID排序，用同一个函数实现
//-----------------------------------------------
void sort(Student stu[],const int num,pFun fun)
{
    Student temp;
    
    for(int i = 0; i < num; ++i)
　　{
        for(int j = 0; j < num - i -1; ++j)
        {
            if((*fun)(stu[j],stu[j+1]))
            {
                temp = stu[j];
                stu[j] = stu[j+1];
                stu[j+1] = temp;
            }
        }
    }
}

//-----------------------------------------------
//回调函数：比较年龄
//-----------------------------------------------
bool CompareAge(Student stu1,Student stu2)
{
    //更改从大到小还是从小到大的顺序，只需反一下。
    if(stu1.age < stu2.age)
        return true;
    return false;
}
//-----------------------------------------------
//回调函数：比较id
//-----------------------------------------------
bool CompareId(Student stu1,Student stu2)
{
    //更改从大到小还是从小到大的顺序，只需反一下。
    if(stu1.id < stu2.id)
        return true;
    return false;
}

int main()
{
    Student stu[] = {
    {1103,24},
    {1102,23},
    {1104,22},
    {1107,25},
    {1105,21}};
    
    pFun fun = CompareAge;
    int size = sizeof(stu)/sizeof(Student);
    
    sort(stu,size,fun);
    
    for(int i = 0; i < size; ++i){
        printf("%d %d\n",stu[i].id,stu[i].age);
    }
    
    return 0;
}
