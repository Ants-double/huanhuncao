## Docker离线安装镜像

1. 尽量在同平台的系统下拉取镜像

2. 导出

   ``` shell
   docker save -o 文件名.tar 镜像名称
   # 一定要写镜像名，不要写uuid ,不然会生成虚玄镜像
   ```

   

3. 拷贝

   

4. 导入

   ``` shell
   docker load < 文件名.tar
   docker load -i  文件名.tar
   # 如果报错，一定要重新生成tar包再次导入
   ```

   

5. 运行