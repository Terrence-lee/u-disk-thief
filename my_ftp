from ftplib import FTP

#配置所需的基本参数
host = '47.106.235.000'
username = ''
password = ''
file = '1.txt'
port = 20

#建立ftp链接
ftp = FTP()
ftp.connect(host, port)
ftp.login(username, password)
ftp.set_pasv(True)

#ftp.cwd('/home/udisk')
# print(ftp.nlst())
# print(ftp.pwd())

#进行上传；两个参数分别是：文件的完整目录（包含文件），文件名（含扩展名）；无返回值
def upload(localdir, filename):
    fp = open(localdir, 'rb')
    cmd = 'STOR /XinBu/%s' % filename  #可以在文件夹这里包含打印社位置+时间信息
    ftp.storbinary(cmd, fp)
