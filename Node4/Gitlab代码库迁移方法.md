# Gitlab代码库迁移方法

------

## 方法一：

用户端将本地代码关联关系从老的GitLab服务器上迁移到新的Gitlab服务器上

1. 显示本地所有的远程仓库地址
   ```shell
   git remote -v
   ```

2. 删除本地代码与老的GitLab分支之间的关系
   ```shell
   git remote remove origin
   ```

3. 本地代码与新的GitLab服务器关联起来
   ```shell
   git remote add origin 106.52.103.94:xxx/xxx.git
   ```

4. 线上线下分支同步
   ```shell
   git pull
   ```

5. 为分支设置跟踪信息
   ```shell
   git branch --set-upstream-to=origin/<yourbranch> yourbranch
   ```

   注意将yourbranch替换成实际要拉取的分支

6. 最后拉取下代码看是否成功即可

------

## 方法二：

直接从新的gitlab地址拉取项目代码到本地，账户密码与原gitlab一致
