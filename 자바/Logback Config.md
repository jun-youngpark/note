# Logback에서 Configuration 설정하기 


## 1. JoranConfigurator (Source 에서)
```
      LoggerContext loggerContext = (LoggerContext) LoggerFactory.getILoggerFactory();
        loggerContext.reset();
        JoranConfigurator configurator = new JoranConfigurator();
        try {
            String path = System.getProperty("wiseu.home") + "/conf/web/web-logback.xml";
            InputStream config = new FileInputStream(path);
            configurator.setContext(loggerContext);
            configurator.doConfigure(config);
            config.close();
        } catch (JoranException | IOException e) {
            e.printStackTrace();
        }
```
         
## 2. System.setProperty (시스템 속성을 통해 구성 파일의 위치 설정, (Source 에서))
```
   System.setProperty(ContextInitializer.CONFIG_FILE_PROPERTY, m_pConfig.getProperty("log.conf"));
        System.setProperty("log" , m_pConfig.getProperty("log"));

        // added by parkhj 2019.05.27 logback load
        LoggerContext loggerContext = (LoggerContext) LoggerFactory.getILoggerFactory();
        loggerContext.reset();
        new ContextInitializer(loggerContext).autoConfig();
``` 

## 3. java 옵션을 활용한 방법
java -Dlogback.configurationFile= /path/to/config. xml 
