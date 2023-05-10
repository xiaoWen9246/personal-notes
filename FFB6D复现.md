## Apex库出现报错'IndexError: tuple index out of range' 

bug产生原因：使用了高版本的python或者apex库，导致GPU上运行的pytorch深度学习代码出现'IndexError:tuple index out of range'报错

**解决办法：**  
从github上下载的apex库在正式安装之前，首先修改源代码。修改源代码中的apex-master/apex/amp/utils.py文件  
将97行的

    if cached_x.grad_fn.next_functions[1][0].variable is not x:     
修改为

    if cached_x.grad_fn.next_functions[0][0].variable is not x: 

之后再进入apex-master文件夹执行

    python setup.py install
 
