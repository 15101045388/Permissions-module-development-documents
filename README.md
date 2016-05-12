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

###测试用例
######	insertTableInfo向表中插入数据

	@Test
	public void insertDataTable() {
		Object obj = "[{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"}]";
		String res = restTemplate.postForObject(baseUri + "/data/test/zae/_add", obj, String.class);
		assertThat(res, containsString("OK"));// 添加表数据，没有ok，测试错误。
	}
	-------------
  插入成功。
  
  public void insertDataTable() {
		Object obj = "[{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"},{\"name\":\"z\",\"age\":\"12\"}]";
		String res = restTemplate.postForObject(baseUri + "/data/test/zae12/_add", obj, String.class);
		assertThat(res, containsString("OK"));// 添加表数据，没有ok，测试错误。
	}
	-------------
没有zae12这张表，插入失败。

 


