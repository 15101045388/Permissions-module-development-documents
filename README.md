# Permissions-module-development-documents

#  H1主模块
## controller

### cacheController

<table>
  <tr>
    <th>序号</th>
    <th>方法名称</th>
    <th>方法描述</th>
  </tr>
  <tr>
    <th>1</th>
    <th>insertTableInfo</th>
    <th>向表中插入数据</th>
  </tr>
  <tr>
    <th>2</th>
    <th>updateTableInfo</th>
    <th>修改表中数据</th>
  </tr>
  <tr>
    <th>3</th>
    <th>getDbInfo</th>
    <th>获取数据库信息</th>
  </tr>
  <tr>
    <th>4</th>
    <th>getOneDbInfo</th>
    <th>获取一个数据库信息</th>
  </tr>
  <tr>
    <th>5</th>
    <th>getTableInfo</th>
    <th>获取表数据信息</th>
  </tr>
  <tr>
    <th>6</th>
    <th>deleteTableInfo</th>
    <th>删除表数据</th>
  </tr>  
  <tr>
    <th>6</th>
    <th>getOneTableInfo</th>
    <th>获取表的信息</th>
  </tr>
</table>

1、Controller
CacheController

    1、insertTableInfo向表中插入数据
	  @Test
	  public void insertDataTable() {
	      Object obj = "[{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"}]";
	      String res = restTemplate.postForObject(baseUri + "/data/test/zae/_add", obj, String.class);
	      assertThat(res, containsString("OK"));// 添加表数据，没有ok，测试错误。
	  }
	  插入成功
	  
	  public void insertDataTable() {
	     Object obj = "[{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"}]";
	      String res = restTemplate.postForObject(baseUri + "/data/test/zae12/_add", obj, String.class);
	      assertThat(res, containsString("OK"));// 添加表数据，没有ok，测试错误。
	  }
	  表不存在，插入失败。

	  public void insertDataTable() {
	      Object obj = "[{name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"}]";
	      String res = restTemplate.postForObject(baseUri + "/data/test/zae/_add", obj, String.class);
	      assertThat(res, containsString("OK"));// 添加表数据，没有ok，测试错误。
	  }
	  插入数据格式不正确，插入失败

    2、updateTableInfo 修改表中数据
	  @Test
	  public void updateDataTable() {
	      Object obj = "{\"name\":\"asdf\",\"age\":\"122\"}";
	      String res = restTemplate.postForObject(baseUri + "/data/test/zae/3/_update", obj, String.class);
	      assertThat(res, containsString("OK"));// 修改表数据，没有ok，测试错误。
	  }
	  修改成功

    3、getDbInfo 获取数据库信息
	  @Test
	  public void showDataInfo() {
	      String res = restTemplate.getForObject(baseUri + "/data", String.class);
	      assertThat(res, containsString("OK"));// 显示表中字段，没有ok，测试错误。
	  }
	  显示所有数据库信息

    4、getOneDbInfo 获取一个数据库信息
	  @Test
	  public void showDataTableInfo() {
	      String res = restTemplate.getForObject(baseUri + "/data/test", String.class);
	      assertThat(res, containsString("OK"));// 显示表中字段，没有ok，测试错误。
	  }
	  成功显示所有数据库信息

	  @Test
	  public void showDataTableInfo() {
	  		String res = restTemplate.getForObject(baseUri + "/data/test12x", String.class);
	  		assertThat(res, containsString("OK"));// 显示表中字段，没有ok，测试错误。
	  }
	  test12x表不存在，服务器内部错误

    5、getTableInfo 获取表数据信息
	  @Test
 	  public void DataTable() {
 	      Object obj = "{\"name\":\"asdf\",\"age\":\"122\"}";
 	      String res = restTemplate.getForObject(baseUri + "/data/test/zae/_data?id=1", String.class);
 	      assertThat(res, containsString("OK"));// 修改表数据，没有ok，测试错误。
 	  }
 	  查询zae表中id为1的数据
 	  @Test
	  public void DataTable() {
	      String res = restTemplate.getForObject(baseUri + "/data/test/zae/_data?id=x", String.class);
	      assertThat(res, containsString("OK"));// 修改表数据，没有ok，测试错误
	  }
	  查询失败，没有id为x的数据
	  
 	  @Test
  	public void DataTable() {
  	    String res = restTemplate.getForObject(baseUri + "/data/test/zae/_data?id=498654165", String.class);
  	    assertThat(res, containsString("OK"));// 修改表数据，没有ok，测试错误
  	}
  	查询失败，id不存在

    6、deleteTableInfo 删除表数据
 	  @Test
 	  public void deleteTableInfo() {
  	    String res = restTemplate.getForObject(baseUri + "/data/test/zae/_delete?id=2", String.class);
  	    assertThat(res, containsString("OK"));// 删除表数据，没有ok，测试错误。
  	}
  	成功删除zae表中id为2的数据，

  	@Test
  	public void deleteTableInfo() {
  	    Object obj = "{\"name\":\"asdf\"}";
  	    String res = restTemplate.getForObject(baseUri + "/data/test/zae/_delete?id=X", String.class);
  	    assertThat(res, containsString("OK"));// 删除表数据，没有ok，测试错误。
  	}
  	删除失败。没有id为X的数据

    7、getOneTableInfo 获取表的信息
  	@Test
  	public void showDataTableInfoByColunm() {
  	    String res = restTemplate.getForObject(baseUri + "/data/test/interface", String.class);
  	    assertThat(res, containsString("OK"));// 显示表中字段，没有ok，测试错误。
  	}

	  
二、CreateController

    创建表
  	@Test
  	public void createTable() {
  	    Object obj = "{\"name\":\"t100\",\"fields\":[{\"col_name\":\"id\",\"data_type\":\"int\",\"is_null\":\"true\",\"auto_increment\":\"true\",\"is_pk\":\"true\",\"length\":\"6\"},{\"col_name\":\"name\",\"data_type\":\"varchar\",\"length\":\"50\"},{\"col_name\":\"age\",\"data_type\":\"int\"}],\"comment\":\"注释\",\"account_name\":\"Administrator\"}";
  	    String res = restTemplate.postForObject(baseUri + "/db/test", obj, String.class);
  	    assertThat(res, containsString("ERROR"));
  	}
  	创建成功
  	@Test
  	public void createTable() {
  	    Object obj = "{\"name\":\"t100\",\"fields\":[{\"col_name\":\"id\",\"data_type\":\"int\",\"is_null\":\"true\",\"auto_increment\":\"true\",\"is_pk\":\"true\",\"length\":\"6\"},{\"col_name\":\"name\",\"data_type\":\"varchar\",\"length\":\"50\"},{\"col_name\":\"age\",\"data_type\":\"int\"}],\"comment\":\"注释}";
  	    String res = restTemplate.postForObject(baseUri + "/db/test", obj, String.class);
  	    assertThat(res, containsString("ERROR"));
  	}
  	数据格式不正确，创建失败。



