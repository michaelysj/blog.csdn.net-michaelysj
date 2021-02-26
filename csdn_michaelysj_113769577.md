time_t 精确到秒，timeval 精确到微秒，都是以长整数来保存时间
timeval中包含time_t对象: 
tv.tv_sec
毫秒(ms): tv.tv_usec/1000

结构体:

```c
time_t 类型，这本质上是一个长整数，表示从1970-01-01 00:00:00到目前计时时间的秒数，如果需要更精确一点的，可以使用timeval精确到毫秒。

struct timeval {  
         time_t       tv_sec;     /* seconds */  
         suseconds_t   tv_usec; /* microseconds */  
}; 
struct tm {  
        int tm_sec;     /* seconds after the minute - [0,59] */  
        int tm_min;     /* minutes after the hour - [0,59] */  
        int tm_hour;    /* hours since midnight - [0,23] */  
        int tm_mday;    /* day of the month - [1,31] */  
        int tm_mon;     /* months since January - [0,11] */  
        int tm_year;    /* years since 1900 */  
        int tm_wday;    /* days since Sunday - [0,6] */  
        int tm_yday;    /* days since January 1 - [0,365] */  
        int tm_isdst;   /* daylight savings time flag */  
        };
```
常用时间函数

```c
time_t time(time_t *t); //取得从1970年1月1日至今的秒数
char *asctime(const struct tm *tm); //将结构中的信息转换为真实世界的时间，以字符串的形式显示 // Www Mmm dd hh:mm:ss yyyy 其中，Www 表示星期几，Mmm 是以字母表示的月份，dd 表示一月中的第几天，hh:mm:ss 表示时间，yyyy 表示年份。
char *ctime(const time_t *timep); //将timep转换为真实世界的时间，以字符串显示，它和asctime不同就在于传入的参数形式不一样 //  Mon Jan 11 08:23:14 2021
struct tm *gmtime(const time_t *timep); //将time_t表示的时间转换为没有经过时区转换的UTC时间，是一个struct tm结构指针
struct tm *localtime(const time_t *timep); //和gmtime类似，但是它是经过时区转换的时间。
struct tm *localtime_r(const time_t *timep, struct tm *result); //线程安全的
time_t mktime(struct tm *tm); //将struct tm 结构的时间转换为从1970年至今的秒数
int gettimeofday(struct timeval *tv, struct timezone *tz); //返回当前距离1970年的秒数和微妙数，后面的tz是时区，一般不用
double difftime(time_t time1, time_t time2); //返回两个时间相差的秒数
asctime_r(), ctime_r(), gmtime_r() // 时间函数的 _r 版本都是线程安全的。
size_t strftime(char *str, size_t maxsize, const char *format, const struct tm *timeptr); //时间转字符串
char *strptime(const char *str, const char *format, struct tm *timeptr); //字符串转时间
```
