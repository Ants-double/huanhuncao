# springboot读取配置文件的内容

## 配置文件映射为Bean

- 添加配置文件

  ``` properties
  
  statistics.startTime=2019-06-25 00:00:00
  
  # backup
  statistics.endTime=2019-07-25 10:00:00
  statistics.statisticInterval=30
  statistics.checkLidarNum=2
  statistics.useCollectionDate=0
  #sites
  
  statistics.sites[0]=cgz
  
  ```

  

- 读取配置文件

  ``` java
  
  
  import com.everise.lidarstatistic.utils.TimeConvert;
  import lombok.Getter;
  import lombok.Setter;
  import org.springframework.boot.context.properties.ConfigurationProperties;
  import org.springframework.stereotype.Component;
  
  import java.time.LocalDateTime;
  import java.util.List;
  
  /**
   * @author lyy
   * @description
   * @date 2019/5/29
   */
  
  @ConfigurationProperties(prefix = "statistics")
  @Component
  public class StatisticTaskParameter {
  
      @Getter
      @Setter
      private  Integer useCollectionDate;
      @Getter
      private LocalDateTime startTime;
  
      @Getter
      private LocalDateTime endTime;
      @Setter
      @Getter
      private Integer statisticInterval;
  
      @Setter
      @Getter
      private List<String> sites;
      @Getter
      @Setter
      private int  checkLidarNum;
  
      public void setStartTime(String startTime) {
          this.startTime = TimeConvert.stringConvertLocalDateTime(
                  startTime, "yyyy-MM-dd HH:mm:ss"
          );
      }
  
      public void setEndTime(String endTime) {
          this.endTime = TimeConvert.stringConvertLocalDateTime(
                  endTime, "yyyy-MM-dd HH:mm:ss"
          );
      }
  }
  
  ```

  

## 注入配置文件到单个属性

- 添加配置文件

  ``` yml
  services:
    ports:
      user: 7778
      content: 7779
    versions:
      user:
        v1: 1.0.0
      content:
        v1: 1.0.0
  
  ```

  

- 读取配置文件

  ``` java
  
      @Value(value = "${services.ports.user}")
      private String userPort;
      @Value(value = "${services.ports.content}")
      private String contentPort;
  
      @Reference(version = "${services.versions.user.v1}")
      private UserConsumerService userConsumerService;
  
      @Reference(version = "${services.versions.content.v1}")
      private ContentConsumerService contentConsumerService;
  
  ```

  

  