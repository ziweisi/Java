#mifirst java code

```
package com.atguigu.teacher;
 
import org.junit.Test;
 
import java.sql.*;
 
/**
 * Date:2020/12/4
 * Author:ybc
 * Description:
 */
public class SelectTest {
 
    @Test
    public void testSelectMany(){
        Connection conn = null;
        Statement st = null;
        ResultSet resultSet = null;
        try {
            //1、加载驱动
            Class.forName("com.mysql.jdbc.Driver");
            //2、创建连接
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "123456");
            //3、创建预编译对象
            st = conn.createStatement();
            //4、执行SQL，查询所使用的方法executeQuery()
            resultSet = st.executeQuery("select * from t_user");
            //5、处理结果集，获取结果集中的数据
            /**
             * 结果集中有方法next()判断当前的结果集中是否有下一条数据，并将指针指向下一条下一条数据
             * 因此，要想将结果集中所有的数据获取，遍历结果集时，一次循环只能执行一个next()
             * 结果集中有方法getXxx(int columnCount)可以通过列数获取某一列的数据
             * 结果集中有方法getXxx(int columnName)可以通过列名（字段名）获取某一列的数据
             * 以上getXxx()是通过列数或者列名获取与表中数据类型匹配的数据
             * 也可以使用getObject()通过数或者列名统一获取为Object类型的数据
             * 若仅仅是输出，则可以使用getObject()，但是若查询出的数据要进行具体的操作，建议获取与表中数据类型匹配的数据
             */
            while(resultSet.next()){
                resultSet.next();
                //System.out.println("id:"+resultSet.getInt(1)+",username:"+resultSet.getString(2)+",password:"+resultSet.getString(3)+",age:"+resultSet.getInt(4)+",sex:"+resultSet.getString(5));
                System.out.println("id:"+resultSet.getInt("id")+",username:"+resultSet.getString("username")+",password:"+resultSet.getString("password")+",age:"+resultSet.getInt("age")+",sex:"+resultSet.getString("sex"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if(resultSet != null){
                try {
                    resultSet.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(st != null){
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(conn != null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
 
    /**
     * 作业：查询id为1的用户信息的用户名，select username from t_user where id = 1;
     * 作业：查询当前用户表中的总记录数，select count(*) count from t_user;
     */
 
    @Test
    public void testSelectOne(){
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        try {
            Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "123456");
            st = conn.createStatement();
            rs = st.executeQuery("select * from t_user where id = 1");
            //当SQL语句查询出的数据只有一条时，可以使用while或者if
            /*if(rs.next()){
                System.out.println("id:"+rs.getInt(1)+",username:"+rs.getString(2)+",password:"+rs.getString(3)+",age:"+rs.getInt(4)+",sex:"+rs.getString(5));
            }*/
            while(rs.next()){
                System.out.println("id:"+rs.getInt(1)+",username:"+rs.getString(2)+",password:"+rs.getString(3)+",age:"+rs.getInt(4)+",sex:"+rs.getString(6));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if(rs != null){
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(st != null){
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if(conn != null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```
