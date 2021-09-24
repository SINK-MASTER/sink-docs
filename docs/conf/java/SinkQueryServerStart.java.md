```java
public class SinkQueryServerStart {
    private static ClassPathXmlApplicationContext context;

    private void start() {
        long beginTime = new Date().getTime();
        if (null != context) {
            System.out.println("系统已启用，若需要重启请选择reload参数");
            return;
        }

        context = new ClassPathXmlApplicationContext("applicationContext.xml");
        context.start();
        System.out.println("Dubbo 服务启动完成!耗时:" + (new Date().getTime() - beginTime) + "毫秒");
        Main.main(new String[]{});
    }

    public static void main(String[] args) {
        String env_tag = "local";
        if (args.length >= 1) {
            env_tag = args[0];
        }
        // 设置环境变量用于读取配置
        System.setProperty("env_tag",env_tag);
        SinkQueryServerStart qStart = new SinkQueryServerStart();
        qStart.start();
    }
}
```