### NDOE系统命令 : spawn /  exec / execFile

**spwan** 可使用系统进程观察内存使用情况：

```javascript
const { spawn } = require('child_process')
const ls = spawn('ls', ['-lh', '/usr'])

// 捕获标准输出并将其打印到控制台
ls.stdout.on('data', function (data) {
    console.log('standard output:\n' + data)
})

// 捕获标准错误输出并将其打印到控制台
ls.stderr.on('data', function (data) {
    console.log('standard error output:\n' + data)
})

// 注册子进程关闭事件
ls.on('exit', function (code, signal) {
    console.log('child process exit, exit:' + code)
})
```

```javascript
Debugger attached.
standard output:
process.js:6
total 0
lrwxr-xr-x    1 root  wheel     8B Apr 25  2018 X11 -> /opt/X11
lrwxr-xr-x    1 root  wheel     8B Apr 25  2018 X11R6 -> /opt/X11
drwxr-xr-x  978 root  wheel    31K Feb 11 00:44 bin
drwxr-xr-x  267 root  wheel   8.3K Nov  8 09:26 include
drwxr-xr-x  313 root  wheel   9.8K Feb 11 00:44 lib
drwxr-xr-x  240 root  wheel   7.5K Feb 11 00:44 libexec
drwxr-xr-x   25 root  wheel   800B Jul  4  2018 local
drwxr-xr-x  248 root  wheel   7.8K Feb 11 00:44 sbin
drwxr-xr-x   47 root  wheel   1.5K Jul  4  2018 share
drwxr-xr-x    5 root  wheel   160B Oct 26  2017 standalone
child process exit, exit:0
process.js:16

```



**exec** 可执行linux命令

```javascript
const { exec } = require('child_process')
const cmdstr = 'curl http://www.weather.com.cn/data/sk/101010100.html'

exec(cmdstr, function (err, stdout, stderr) {
    if (err) {
        console.log(err)
    } else {
        const data = JSON.parse(stdout)
        console.log(data)
    }
})
```

```javascript
Debugger attached.

"{"weatherinfo":{"city":"北京","cityid":"101010100","temp":"27.9","WD":"南风","WS":"小于3级","SD":"28%","AP":"1002hPa","njd":"暂无实况","WSE":"<3","time":"17:55","sm":"2.1","isRadar":"1","Radar":"JC_RADAR_AZ9010_JB"}}"

```

**execFile** 执行脚本文件

```javascript
var callfile = require('child_process'); 
var ip = '1.1.1.1';
var username = 'test';
var password = 'pwd';
var newpassword = 'newpwd';

callfile.execFile('change_password.sh',['-H', ip, '-U', username, '-P', password, '-N', newpassword],null,function (err, stdout, stderr) {
    callback(err, stdout, stderr);
});
```

```shell
#!/bin/sh

IP=""
NAME=""
PASSWORD=""
NEWPASSWORD=""

while getopts "H:U:P:N:" arg #选项后面的冒号表示该选项需要参数
do
        case $arg in
             H)
                IP=$OPTARG
                ;;
             U)
                NAME=$OPTARG
                ;;
             P)
                PASSWORD=$OPTARG
                ;;
             N)
                NEWPASSWORD=$OPTARG
                ;;
             ?)  #当有不认识的选项的时候arg为?
            echo "含有未知参数"
        exit 1
        ;;
        esac
done

#先获取userid
USERID=`/usr/bin/ipmitool -I lanplus -H $IP -U $NAME -P $PASSWORD user list | grep root | awk '{print $1}'`
# echo $USERID
#根据userid来修改密码
/usr/bin/ipmitool -I lanplus -H $IP -U $NAME -P $PASSWORD user set password $USERID $NEWPASSWORD
```

