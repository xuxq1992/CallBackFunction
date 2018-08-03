# CallBackFunction

//目录  /mytest/
//mylib.h
#include <stdio.h>

typedef int student_id;
typedef int student_age;


typedef struct _Student{
    student_id id;
    student_age age;
}Student;

namespace mylib
{
    typedef bool (*pFun)(Student, Student);

    bool CompareAge(Student stu1,Student stu2);

    bool CompareId(Student stu1,Student stu2);

    void sort(Student stu[],const int num,pFun fun);
}



//目录  /mytest/
//mylib.cpp
#include "mylib.h"

void mylib::sort(Student stu[],const int num,pFun fun)
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


bool mylib::CompareAge(Student stu1,Student stu2)
{
    
    if(stu1.age < stu2.age)
        return true;
    return false;
}

bool mylib::CompareId(Student stu1,Student stu2)
{
   
    if(stu1.id < stu2.id)
        return true;
    return false;
}

//目录  /mytest/test
//main.cpp
#include "./../mylib.h"
#include <stdio.h>
#include <stdlib.h> 
int main()
{
    Student stu[] = 
    {
        {1103,24},
        {1102,23},
        {1104,22},
        {1107,25},
        {1105,21}
    };

    mylib::pFun fun = mylib::CompareAge;
    int size = sizeof(stu)/sizeof(Student);

    mylib::sort(stu,size,fun);

    for(int i = 0; i < size; ++i){
        printf("%d %d\n",stu[i].id,stu[i].age);
    }
    system("pause");
    return 0;
}

//g++ -c mylib.cpp
//生成 mylib.o
//ar cr libmylib.a mylib.o
//生成 libmylib.a
//g++ main.cpp -L/mytest -lmylib -o test.dbg
