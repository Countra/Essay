# Mybatis 框架实验报告

## 一、实验报告目录

1.1 项目目录结构
src 目录下（com.lanqiao）

- dao 包 -- 数据访问层（接口）
- daolmpl 包 -- 中存在的是接口的具体实现(class)
- test 包 -- 写测试方法
- vo 包 -- value object 值对象。通常用于业务层之间的数据传递，应是抽象出的业务对象,可以和表对应
- mybatis.xml --mysql 映射配置文件

1.2 实验知识点

- Mybatis 框架
- @select
- @insert
- @update
- dalete

## 二、实验代码

> com.lanqiao.dao.Tb_bbsDao.java

```java
package com.lanqiao.dao;

import java.util.List;

import com.lanqiao.vo.Tb_bbs;

public interface Tb_bbsDao {


    //增加
    public int addTb_bbs(Tb_bbs t);

    //删除
    public void deleteTb_bbs(int id);

    //修改
    public int updateTb_bbs(Tb_bbs t);

    //全查询
    public List<Tb_bbs> selectAll();

    //指定查询
    public List<Tb_bbs> selectById(int id);

}
```

> com.lanqiao.daoImpl.Tb_bbsDaolmpl.java

```java
package com.lanqiao.daoImpl;

import java.io.IOException;
import java.io.Reader;
import java.util.List;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import com.lanqiao.dao.Tb_bbsDao;
import com.lanqiao.vo.Tb_bbs;

public class Tb_bbsDaoImpl implements Tb_bbsDao{

    /*
     * (non-Javadoc)
     * @see com.lanqiao.dao.Tb_bbsDao#addTb_bbs(com.lanqiao.vo.Tb_bbs)
     *
     * 1 读取配置文件（连接数据库）
     * 2 建立工厂模式
     * 3打开session
     * 4调用增删改查方法
     * 5提交事务（增删改）  /集合传值
     * 6关闭session
     */
    static SqlSessionFactory sf=null;
    static{
        try {
        	//读取总配置文件
            Reader reader=Resources.getResourceAsReader("mybatis.xml");
            //建立工厂模式
            sf=new SqlSessionFactoryBuilder().build(reader);
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

    //增加
    @Override
    public int addTb_bbs(Tb_bbs t) {
        // TODO Auto-generated method stub
    	//打开session
        SqlSession ss=sf.openSession();
        //调用方法
        int i=ss.insert("Tb_bbs.add", t);
        //提交事务
        ss.commit();
        //关闭session(缓存)
        ss.close();
        return i;
    }

    //删除
    @Override
    public void deleteTb_bbs(int id) {
        // TODO Auto-generated method stub

        SqlSession ss=sf.openSession();

        ss.delete("Tb_bbs.delete", id);

        ss.commit();

        ss.close();
    }

    //修改
    @Override
    public int updateTb_bbs(Tb_bbs t) {
        // TODO Auto-generated method stub

        SqlSession ss=sf.openSession();

        int i=ss.update("Tb_bbs.update", t);

        ss.commit();

        ss.close();
        return i;
    }

    @Override
    public List<Tb_bbs> selectAll() {
        // TODO Auto-generated method stub

        SqlSession ss=sf.openSession();

        List<Tb_bbs> list=ss.selectList("Tb_bbs.selectAll");
        //全查询
        for(Tb_bbs t:list){
            System.out.println(t.getId()+"--"+t.getTitle()
                    +"--"+t.getContent()+"--"+t.getIntime());
        }

        ss.close();
        return list;
    }

    //指定查询
    @Override
    public List<Tb_bbs> selectById(int id) {
        // TODO Auto-generated method stub

        SqlSession ss=sf.openSession();

        List<Tb_bbs> list=ss.selectList("Tb_bbs.selectById",id);

        for(Tb_bbs t:list){
            System.out.println(t.getId()+"--"+t.getTitle()
                    +"--"+t.getContent()+"--"+t.getIntime());
        }

        ss.close();
        return list;
    }

}
```

> com.lanqiao.test.Tb_bbsTest.java

```java
package com.lanqiao.test;

import com.lanqiao.dao.Tb_bbsDao;
import com.lanqiao.daoImpl.Tb_bbsDaoImpl;
import com.lanqiao.vo.Tb_bbs;

public class Tb_bbsTest {


    static Tb_bbsDao td=new Tb_bbsDaoImpl();
    //增加方法
    public static void add(){
        Tb_bbs tb=new Tb_bbs();

        tb.setTitle("Demo03");
        tb.setContent("测试ing");

        td.addTb_bbs(tb);
    }

    //删除方法
    public static void delete(){

        td.deleteTb_bbs(23);
    }

    //修改方法
    public static void update(){
            Tb_bbs tb=new Tb_bbs();

            tb.setId(2);
            tb.setTitle("实习项目");
            tb.setContent("mybatis框架");

            td.updateTb_bbs(tb);
        }

    //全查询方法
    public static void selectAll(){
        td.selectAll();
    }

    //指定方法
    public static void selectById(){
            td.selectById(15);
    }

    public static void main( String[] args) {

        add();

//       delete();

//        update();

        selectAll();


 //       selectById();
    }


}

```

> Tb_bbs.java

```java
package com.lanqiao.vo;

public class Tb_bbs {
    private Integer id;
    private String title;
    private String content;
    private String intime;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    public String getContent() {
        return content;
    }
    public void setContent(String content) {
        this.content = content;
    }
    public String getIntime() {
        return intime;
    }
    public void setIntime(String intime) {
        this.intime = intime;
    }

}
```

> Tb_bbs.xml

```java
<?xml version="1.0" encoding="UTF-8"?>

 <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="Tb_bbs">
<!-- #{id}表示取参数中对象id的属性值 useGeneratedKeys="true"表示自动增一策略-->
    <insert id="add" parameterType="com.lanqiao.vo.Tb_bbs" useGeneratedKeys="true">
        insert into tb_bbs values(id,#{title},#{content},now());
    </insert>
    <delete id="delete" parameterType="com.lanqiao.vo.Tb_bbs">
        delete from tb_bbs where id=#{id};
    </delete>
    <update id="update" parameterType="com.lanqiao.vo.Tb_bbs">
    update tb_bbs set
    <if test="title!=null">
        title=#{title}
    </if>
    <if test="(title!=null) and (content!=null)">
        ,
    </if>
    <if test="content!=null">
        content=#{content}
    </if>
    where id=#{id};
</update>

<select id="selectAll" resultType="com.lanqiao.vo.Tb_bbs">
    select * from tb_bbs;
</select>

<select id="selectById" resultType="com.lanqiao.vo.Tb_bbs">
    select * from tb_bbs where id=#{id};
</select>


</mapper>
```

> mybatis.xml

```java
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="username" value="root"/>
                <property name="password" value="Countra"/>
                <property name="url" value="jdbc:mysql://localhost:3306/goshop?serverTimezone=GMT"/>
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
            </dataSource>
        </environment>
    </environments>
    <!-- mappers元素包含了一组映射器(mapper),这些映射文件包含了SQL代码和映射定义信息 -->
    <mappers>
        <mapper resource="com/lanqiao/vo/Tb_bbs.xml"/>
    </mappers>

</configuration>
```

## 三、实验测试截图

> 增加方法

![增加方法](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/增加方法.png)

> 测试数据

![测试数据](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/测试数据.png)

> 修改方法

![修改方法](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/修改方法.png)

> 修改 id=25 的数据

![修改](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/修改.png)

> 删除 id=21 数据

![删除](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/删除.png)

> 查找指定 id=26 的数据

![查找](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/查找.png)
