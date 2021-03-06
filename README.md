# CuitJavaEEPractice
**成信大JAVAEE实训课程项目**  
**cuit javaee Training Course Project**  

## 项目简介 Project Description  
**项目名称**：家庭理财管理系统  
**Name**：Family Financial Management System  
  
**项目介绍**：一个能够管理家庭内部各种财务信息的家庭理财管理系统，主要包括用户管理、收支管理、财务管理、报表管理等公共模块。  
**Introduction**：A system that would manage within the family, family finance Financial Information Management System, including user management, budget management, financial management, report management, and other public module.  
  
## 技术选型 Choosing Technology  
**开发技术**：JAVA, JSP, Servlet, JDBC  
**Development technology**：JAVA, JSP, Servlet, JDBC  
  
**开发环境**：IntelliJ idea 2017.1+, jdk 8u91, mysql 5.5, tomcat 8.5.34  
**Development environment**：IntelliJ idea 2017.1+, jdk 8u91, mysql 5.5, tomcat 8.5.34  
  
**开发框架**：Spring、SpringMVC、Mybatis、Jquery、layui  
**Development Framework**：Spring、SpringMVC、Mybatis、Jquery、layui  
  
## 启动方法 Start Up  
**导入项目**：使用IDEA拉取git远端项目，等待项目加载完成。  
**Import Project**：Using the idea of distal pull git project, waiting for the project finishes loading.  
  
**环境配置**：为项目配置tomcat 8.5运行环境，点击运行按钮，可以查看执行情况。  
**Configuring environment**：configuring Tomcat 8.5 Runtime Environment for your project, click the Run button, you can view the status of implementation.  
  
**启动成功**：在浏览器中输入：http://localhost:8080/ 访问项目首页。  
**Start Completed**：In the browser, enter : http://localhost:8080/ to visit the project home page.  

## 开发规范(必读)  Development Specification (important)  
- 在每次编写代码前应该先pull代码，确保本地版本与主要分支一致。  
- 开发代码分工合作，尽量避免修改公共的代码文件，避免出现未知的版本冲突。  
- idea应安装.ignore插件，避免上传不必要的IDE配置文件。本项目中插件所需的'.ignore'文件已经生成。  
  安装请参考：https://blog.csdn.net/ZZY1078689276/article/details/84952858  
- 模块代码应该进行单元测试，确认代码无误后再推送(PUSH)至远端。避免出现冲突造成的难以修复的BUG。
  
- You should pull the code before writing each code to ensure that the local version is consistent with the main branch.  
- Develop code division of work to avoid modifying public code files and avoiding unknown version conflicts.  
- Idea should install the .ignore plug-in to avoid uploading unnecessary IDE profiles.  
  The '.ignore' file required for the plug-in in this project has been generated.    
  Please refer to: https://blog.csdn.net/ZZY1078689276/article/details/84952858  
- The module code should be unit tested to confirm that the code is correct before pushing (PUSH) to the far end. Avoid hard-to-fix BUGS caused by conflict.  

## 页面框架  Page Framework
- 前端框架：layUI  
- layui是一款采用自身模块规范编写的前端 UI 框架，遵循原生 HTML/CSS/JS 的书写与组织形式，门槛极低，拿来即用。  
- 学习教程：https://www.layui.com/doc/  
  
- Front Page frame: layUI  
- Layui is a UI framework written with its own module specification, following the writing and organization of native HTML/CSS/JS, with very low thresholds for ready-to-use.  
- Learning tutorial: https://www.layui.com/doc/  
  
## 编写标准 Writing Standards  

### 1、Controller层编写标准  
  
**按照如下规则编写Controller**  
  
&emsp;&emsp;模板中包含各类请求的映射方法，直接复制模板进行修改即可，模板代码如下：  
  
> @Controller  
> @RequestMapping(value = {"/Demo"})  
> public class DemoController {  
> &nbsp;&nbsp;&nbsp;&nbsp;//自动注入Service层  
> &nbsp;&nbsp;&nbsp;&nbsp;@Autowired  
> &nbsp;&nbsp;&nbsp;&nbsp;private DemoService demoService;  

> &nbsp;&nbsp;&nbsp;&nbsp;/**  
> &nbsp;&nbsp;&nbsp;&nbsp; * 直接字符串映射样例  
> &nbsp;&nbsp;&nbsp;&nbsp; * @return  
> &nbsp;&nbsp;&nbsp;&nbsp; */  
>> &nbsp;&nbsp;&nbsp;&nbsp;@RequestMapping(value = {"/StrDemo"})  
> &nbsp;&nbsp;&nbsp;&nbsp;// 使用ResponseBody可以让返回的数据变为字节流  
> &nbsp;&nbsp;&nbsp;&nbsp;@ResponseBody  
> &nbsp;&nbsp;&nbsp;&nbsp;public String returnStr() {  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 直接给前台返回一个字符串，一般用于AJAX交互。  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return "hello,这是第一个映射";  
> &nbsp;&nbsp;&nbsp;&nbsp;}  

> &nbsp;&nbsp;&nbsp;&nbsp;/**  
> &nbsp;&nbsp;&nbsp;&nbsp; * 单对象获取样例  
> &nbsp;&nbsp;&nbsp;&nbsp; * @return  
> &nbsp;&nbsp;&nbsp;&nbsp; */  
>> &nbsp;&nbsp;&nbsp;&nbsp;@RequestMapping(value = {"/BeanDemo"})  
> &nbsp;&nbsp;&nbsp;&nbsp;@ResponseBody  
> &nbsp;&nbsp;&nbsp;&nbsp;public DemoBean returnEntify() {  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DemoBean testBean = new DemoBean();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;testBean.setDemostr("测试实体");  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;testBean.setDemoint(12);  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 会自动将Bean封装为JSON格式数据返回给前端  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return testBean;  
> &nbsp;&nbsp;&nbsp;&nbsp;}  

> &nbsp;&nbsp;&nbsp;&nbsp;/**  
> &nbsp;&nbsp;&nbsp;&nbsp; * 多对象获取样例Demo  
> &nbsp;&nbsp;&nbsp;&nbsp; * @param orderAndRole  
> &nbsp;&nbsp;&nbsp;&nbsp; * @return Json数据  
> &nbsp;&nbsp;&nbsp;&nbsp; * @throws Exception  
> &nbsp;&nbsp;&nbsp;&nbsp; */  
>> &nbsp;&nbsp;&nbsp;&nbsp;@RequestMapping(value = { "/getMoreObjectDemo" }, method = { RequestMethod.POST }, consumes = {  
> &nbsp;&nbsp;&nbsp;&nbsp;		"application/json" }, produces = { "application/json" })  
> &nbsp;&nbsp;&nbsp;&nbsp;@ResponseBody  
> &nbsp;&nbsp;&nbsp;&nbsp;public Object addEmpGetStu(@RequestBody VODemo orderAndRole) throws Exception {  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 同时获取两个前端的数据，需要在VO层封装两个对象，并添加get方法，注意参数样式。  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Order order = orderAndRole.getOrder();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Role role = orderAndRole.getRole();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;order.setInfoAssessmentdate(new Date());  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;order.setInfoRemarks("这是生成的");  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 返回order对象的json数据。  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JSONObject responseObj = (JSONObject) JSONObject.toJSON(order);  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return responseObj;  
> &nbsp;&nbsp;&nbsp;&nbsp;}  

> &nbsp;&nbsp;&nbsp;&nbsp;/**  
> &nbsp;&nbsp;&nbsp;&nbsp; * service调用样例Demo  
> &nbsp;&nbsp;&nbsp;&nbsp; */  
>> &nbsp;&nbsp;&nbsp;&nbsp;@RequestMapping(value = {"/ServiceDemo"})  
> &nbsp;&nbsp;&nbsp;&nbsp;@ResponseBody  
> &nbsp;&nbsp;&nbsp;&nbsp;public String getUsers() {  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 调用service中的方法。  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;List<User> users = demoService.getUsersByExample();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;System.out.print(users.get(0).getSex());  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return "请在控制台查看输出！";  
> &nbsp;&nbsp;&nbsp;&nbsp;} 

> }  


### 2、Service层编写标准  
  
**使用Example进行数据库存取操作**  
  
&emsp;&emsp;项目使用Example类进行数据库交互，在Service层直接调用Example类即可，具体查询数据的样例代码如下：
  
> // 这是一个Demo样例的服务层实现  
> @Service  
> public class DemoServiceImpl implements DemoService {  
> &nbsp;&nbsp;&nbsp;&nbsp;//自动注入userMapper
> &nbsp;&nbsp;&nbsp;&nbsp;@Autowired  
> &nbsp;&nbsp;&nbsp;&nbsp;private UserMapper userMapper;  

> &nbsp;&nbsp;&nbsp;&nbsp;// 根据Example查询用户  
>> &nbsp;&nbsp;&nbsp;&nbsp;@Override  
> &nbsp;&nbsp;&nbsp;&nbsp;public List<User> getUsersByExample() {  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 首先申明一个users对象用于接收查询结果（用户列表）  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;List<User> users = null;  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 新建用户样例  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UserExample example = new UserExample();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 获取一个criteria对象，criteria对象用于设置查询条件  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Criteria criteria = example.createCriteria();  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 这句话等同于 WHERE username LIKE '%a%'  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;criteria.andUsernameLike("%a%");   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 这句话等同于 ORDER BY username ASC   
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;example.setOrderByClause("username asc");  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 执行select查询，参数就是example  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;users = userMapper.selectByExample(example);  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 返回查询结果给controller  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return users;  
> &nbsp;&nbsp;&nbsp;&nbsp;}  

> }  

**具体用法请参考：https://blog.csdn.net/biandous/article/details/65630783**

### 3、Dao层编写标准  
**Mapper文件不需要手动编写**  
&emsp;&emsp;mapper.xml、mapper、entity都已经通过Maven工具Mybatis Generator自动生成， 如果无特殊需要，无须再手动编写。
  
### 4、VO层编写标准
**VO全称Value Object，值对象。主要用于数据交互中，非entity数据的封装。**  
&emsp;&emsp;例：将用户和订单对象组合，成为用户订单对象。
>// 封装用户订单对象  
>public class UserAndOrder {  

>>	&nbsp;&nbsp;&nbsp;&nbsp;private Order order;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;private User user;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;public Order getOrder() {  
>>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return order;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;}  
>>	&nbsp;&nbsp;&nbsp;&nbsp;public void setOrder(Order order) {  
>>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.order = order;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;}  
>>	&nbsp;&nbsp;&nbsp;&nbsp;public User getUser() {  
>>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return user;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;}  
>>	&nbsp;&nbsp;&nbsp;&nbsp;public void setUser(User user) {  
>>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;this.user = user;  
>>	&nbsp;&nbsp;&nbsp;&nbsp;}  

>}  
