# zxyyhc
#通过调用百度语音api  实现文本转语音
import time,os,requests
from tkinter import *
from urllib import *
import urllib.request 
def view():
    #先设计显示界面
    root = Tk()
    #界面名字
    root.title('在线语音合成软件')
    #界面大小，位置
    root.geometry('500x460+450+200')
    #界面宽高是否可变True 可变，False不可变
    root.resizable(width=False,height=False)
    getValue = StringVar()
    viewLabel = Label(root,text='请输入合成文字：') 
    #调用Text（）控件中输入的内容
    def p():
        #定义全局变量leng，与下面参数进行传递
        global leng
        #get（）方式获取，set（）方式进行写入
        leng =  TextArea.get('1.0', "end") 
        print(leng)
    #创建控件并显示
    TextArea = Text(root)
    viewButton = Button(root,text='合成',bg='pink',width=5,height=1,command=p)
    viewButton1 = Button(root,text='提交',bg='pink',width=5,height=1,command=bdApi)
    
    viewLabel.pack()
    TextArea.pack(expand=YES, fill=BOTH)
    #viewInput1.grid(column=0, row=1)
    viewButton.pack()
    viewButton1.pack()   
    root.mainloop()

#合成语音api链接，并下载
def bdApi():
    apiUrl = 'http://tsn.baidu.com/text2audio?'
    #字典操作链接 parse.rlencode()函数转换成url
    data = {'lan':'zh',
            'ctp':1,
            'cuid':11423267,
            'tok':'24.203a93ef5acd089b92a5877de73f83dc.2592000.1532134020.282335-11423267',
            'tex':leng,
            'vol':9,
            'per':0,
            'spd':4,
            'pit':6}      
    urlData = parse.urlencode(data)
    print(leng)
    url = apiUrl + urlData
    #下载合成后MP3 需要用到urlretrieve()函数  注意python 这个函数在URLlib.request库里面，需要导入import urllib.request
    path = 'd:/downMp3/yuyin123.mp3'
    saveMp3 = urllib.request.urlretrieve(url,path) 
#一个python的文件有两种使用的方法，第一是直接作为脚本执行，第二是import到其他的python脚本中被调用（模块重用）执行。因此if __name__ == 'main': 的作用就是控制这两种情况执行代码的过程，
#在if __name__ == 'main': 下的代码只有在第一种情况下（即文件作为脚本直接执行）才会被执行，而import到其他脚本中是不会被执行的。
if __name__=="__main__":
    view()
#总结：目前该软件告一段落了里面有很多不足 ，中间学习了很多，不会的自己百度慢慢的调试后解决。记得从百度语音apiUrl获取合成的语音困扰了两天，
#百度了好多，就是不成功，连续两天一直在解决最终，黄天不负苦心人，让我找到解决办法。想想还是自己学习的不够深入。慢慢成长吧。
#软件功能可以升级:1.自由添加路经及文件名
#                2.不是根目录，路径名不存在会报错
#               3.没有初始化的函数
#              4.界面过于简单，没有布局
#             5.百度语音api的tok值会过期，不能自动更新
#            6.没有打包成可执行文件
#           ..........................
#当前日期：2018-06-25



