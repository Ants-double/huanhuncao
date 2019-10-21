# Mybatis使用自定义类型转换Postgresql

## 主要目的

``` wiki
为了解决从数据库取出来之后再手动转换为javaBean的问题。
主要用mybatis提供的Handler来把处理前置

```

- 添加转换类

  ``` java
  
  
  
  import com.fasterxml.jackson.core.JsonProcessingException;
  import com.fasterxml.jackson.databind.ObjectMapper;
  import org.apache.ibatis.logging.Log;
  import org.apache.ibatis.logging.LogFactory;
  import org.apache.ibatis.type.BaseTypeHandler;
  import org.apache.ibatis.type.JdbcType;
  
  import java.io.IOException;
  import java.sql.CallableStatement;
  import java.sql.PreparedStatement;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  
  /**
   * @author lyy
   * @description
   * @date 2019/5/28
   */
  public class MyStateTypeHandler<T> extends BaseTypeHandler<T> {
      private final static Log log = LogFactory.getLog(MyStateTypeHandler.class);
      private static ObjectMapper objectMapper;
      private Class<T> type;
      static {
          objectMapper = new ObjectMapper();
      }
      public MyStateTypeHandler(Class<T> type) {
          if(log.isTraceEnabled()) {
              log.trace("JsonTypeHandler(" + type + ")");
          }
          if (type == null) {
              throw new IllegalArgumentException("Type argument cannot be null");
          }
          this.type = type;
      }
  
      private  T parse(String json) {
          try {
              if(json == null || json.length() == 0) {
                  return null;
              }
              return objectMapper.readValue(json, type);
          } catch (IOException e) {
              throw new RuntimeException(e);
          }
      }
  
      private String toJsonString(Object obj) {
          try {
              return objectMapper.writeValueAsString(obj);
          } catch (JsonProcessingException e) {
              throw new RuntimeException(e);
          }
      }
      @Override
      public void setNonNullParameter(PreparedStatement preparedStatement, int i, T t, JdbcType jdbcType) throws SQLException {
          preparedStatement.setString(i, toJsonString(t));
      }
  
      @Override
      public T getNullableResult(ResultSet resultSet, String s) throws SQLException {
          return (T) parse(resultSet.getString(s));
      }
  
      @Override
      public T getNullableResult(ResultSet resultSet, int i) throws SQLException {
          return (T) parse(resultSet.getString(i));
  
      }
  
      @Override
      public T getNullableResult(CallableStatement callableStatement, int i) throws SQLException {
  
          return (T) parse(callableStatement.getString(i));
      }
  }
  
  ```

  

- 引用转换类

  ``` xml
    <resultMap id="overlapsail" type="com.javaBean">
          <result column="id" property="id"/>
          <result column="site_code" property="siteCode" jdbcType="VARCHAR"/>
          <result column="car_code" property="carCode" jdbcType="VARCHAR"/>
          <result column="sail_time" property="sailTime"/>
          <result column="height" property="height"/>
  
          <result column="para_value" property="sailOverlapDto" jdbcType="OTHER"
                  javaType="JavaBean"
                  typeHandler="MyStateTypeHandler"/>
      </resultMap>
  ```

  

- 其它的与正常的调用结果相同

- 附一个Blob到Bean的转换

  ``` java
  
  
  import org.apache.ibatis.type.BaseTypeHandler;
  import org.apache.ibatis.type.JdbcType;
  import org.apache.ibatis.type.MappedJdbcTypes;
  import org.apache.ibatis.type.MappedTypes;
  
  import javax.sql.rowset.serial.SerialBlob;
  import java.io.UnsupportedEncodingException;
  import java.sql.*;
  
  /**
   * @author lyy
   * @description
   * @date 2019/6/11
   */
  @MappedJdbcTypes(JdbcType.OTHER) // 可有可无
  @MappedTypes(Blob.class)
  public class MyBlobTypeHander extends BaseTypeHandler<Object> {
      @Override
      public void setNonNullParameter(PreparedStatement preparedStatement, int i, Object o, JdbcType jdbcType) throws SQLException {
  
      }
  
      @Override
      public Object getNullableResult(ResultSet resultSet, String s) throws SQLException {
          return null;
      }
  
      @Override
      public Object getNullableResult(ResultSet resultSet, int i) throws SQLException {
          return null;
      }
  
      @Override
      public Object getNullableResult(CallableStatement callableStatement, int i) throws SQLException {
  
          try {
              return  new SerialBlob( callableStatement.getString(i).getBytes("utf-8"));
          } catch (UnsupportedEncodingException e) {
              return  null;
          }
  
      }
  }
  
  ```

  

- 附一个特殊json到Bean的转换

  ``` java
  
  import java.sql.CallableStatement;
  import java.sql.PreparedStatement;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  
  import com.alibaba.fastjson.JSON;
  import org.apache.ibatis.type.BaseTypeHandler;
  import org.apache.ibatis.type.JdbcType;
  import org.apache.ibatis.type.MappedJdbcTypes;
  import org.apache.ibatis.type.MappedTypes;
  import org.postgresql.util.PGobject;
  
  @MappedJdbcTypes(JdbcType.OTHER) // 可有可无
  @MappedTypes(Object.class)
  public class JsonTypeHandler extends BaseTypeHandler<Object> {
      private static final PGobject jsonObject = new PGobject();
  
      @Override
      public void setNonNullParameter(PreparedStatement ps, int i, Object parameter, JdbcType jdbcType) throws SQLException {
          jsonObject.setType("jsonb");
          if (parameter instanceof String) {
              jsonObject.setValue((String) parameter);
          } else {
              jsonObject.setValue(JSON.toJSONString(parameter));
          }
          ps.setObject(i, jsonObject);
      }
  
      @Override
      public Object getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
  
          return JSON.parseObject(rs.getString(columnIndex), Object.class);
      }
  
      @Override
      public Object getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
          return JSON.parseObject(cs.getString(columnIndex), Object.class);
      }
  
      @Override
      public Object getNullableResult(ResultSet rs, String columnName) throws SQLException {
          return JSON.parseObject(rs.getString(columnName), Object.class);
      }
  }
  
  ```

  

  