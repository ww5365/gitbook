# My Awesome Book

* ## 

  This file file serves as your book's preface, a great place to describe your book's content and ideas.

* afdsfas

|  |  |  |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

在持续撒大法师

啊打发

啊打发


``` c++

void get_left_bottomXY(const std::string map_id, float &lb_x, float &lb_y){

    lb_x = std::atof(map_id.substr(0,4).c_str());//stdlib.h中库函数
    lb_y = std::atof(map_id.substr(4,4).c_str());//把字符类型转成float类型

    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;

    lb_x /= 8.0;
    lb_y /= 12.0;
    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;

    lb_x = (lb_x - 180.0);
    lb_y = (lb_y - 90.0);

    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;
}

```



```
void get_left_bottomXY(const std::string map_id, float &lb_x, float &lb_y)
{

    lb_x = std::atof(map_id.substr(0,4).c_str());//stdlib.h中库函数
    lb_y = std::atof(map_id.substr(4,4).c_str());//把字符类型转成float类型

    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;

    lb_x /= 8.0;
    lb_y /= 12.0;
    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;

    lb_x = (lb_x - 180.0);
    lb_y = (lb_y - 90.0);

    std::cout << "x:y " << lb_x << " " << lb_y << std::endl;
}

```



