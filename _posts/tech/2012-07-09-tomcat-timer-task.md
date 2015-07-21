---
layout:     post
categories: "tech"
title:      "Java Web定时执行任务"
subtitle:   "Tomcat Timer Task"
author:     "Charles"
---

这是前阵子在做交大数字校园项目时候遇到的一个问题。
**需求:** 需要每天定时如凌晨3点执行一次采集数据的任务。
**解决方案:**
* 第一步：在web.xml配置文件中加了一个监听器
`
<!– 配置定时任务监听器 –> 
<listener> 
     <listener-class>bjtu.wap.service.AcquistionTaskManager</listener-class> 
     <description>Atuo Task To Acquiste</description> 
</listener>
`
* 第二步：写一个实现ServletContextListener接口的监听器类。
{% highlight java %}
public class AcquistionTaskManager implements ServletContextListener {
     public static final long PERIOD_DAY = 24 * 60 * 60 * 1000; 
     private Timer timer; 
     // 在Web应用启动时初始化任务 
      public void contextInitialized(ServletContextEvent event) { 
         // 第二天的03:00:00开始执行，执行频率为1天 
         Calendar curtime = Calendar.getInstance(); 
         //curtime.set(Calendar.DATE, curtime.get(Calendar.DATE) + 1); 
         int y = curtime.get(Calendar.YEAR); 
         int m = curtime.get(Calendar.MONTH); 
         int d = curtime.get(Calendar.DAY_OF_MONTH); </p> <p>        
         /** 定制每日3:00执行方法 */ 
         curtime.set(y, m, d, 3, 30, 0); 
         Date date = curtime.getTime(); 
         Timer timer = new Timer(); 
         AcquTask task = new AcquTask(); 
         // 安排指定的任务在指定的时间开始进行重复的固定延迟执行。 
         timer.schedule(task, date, PERIOD_DAY); 
      } 
      
      // 在Web应用结束时停止任务 
      public void contextDestroyed(ServletContextEvent event) { 
          if (timer != null) { 
              timer.cancel(); // 定时器销毁 
          } 
       } 
} 
{% endhighlight %}

* 第三步：写一个继承TimerTask的任务类，将要执行的任务放在run方法中
{% highlight java %}
public class BackTimerTask extends TimerTask {
    // 在run()方法中调用对数据库的备份操作
    public void run() {
        this.doit();
    }
    
    private void doit() { 
        System.out.println("———————"};
    }
{% endhighlight %}

**问题：** run方法中的内容，每次都会执行两次。

**问题解决：**
由于我是在tomcat中调试运行的，tomcat默认的appBase是“Webapps”，他会将timer加载到容器中，我们后面又单独设置了一个 <Context path="" docBase="../webapps/wap" /> 相当于将icms里面的配置加载了两次，导致每次timer执行两次。
将项目移到与webapp是同级的目录中即可。docBase="../wap"

