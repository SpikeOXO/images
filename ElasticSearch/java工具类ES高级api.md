#### 1.测试索引的创建

 Request       相当于es执行 PUT kgc_index

```java
 void testCreateIndex() throws IOException { 
     //        1.创建索引请求        
     CreateIndexRequest request = new CreateIndexRequest("kgc_index"); 
     //        2.客户端执行请求IndicesClient，请求后获得响应        
     CreateIndexResponse createIndexResponse = restHighLevelClient.indices().create(request, RequestOptions.DEFAULT);         
     System.out.println(createIndexResponse);    
 }
```

 

#### 2.测试获取索引

```java
void testExistIndex() throws IOException {    
    GetIndexRequest getIndexRequest = new GetIndexRequest("kgc_index");    
    boolean exists = restHighLevelClient.indices().exists(getIndexRequest, RequestOptions.DEFAULT);    			System.out.println(exists);    
}
```

#### 3.测试删除索引

```java
void testDeleteIndex() throws IOException {    
	DeleteIndexRequest deleteIndexRequest = new DeleteIndexRequest();    
	AcknowledgedResponse delete = restHighLevelClient.indices().delete(deleteIndexRequest, 			RequestOptions.DEFAULT);    
	System.out.println(delete.isAcknowledged()); 
}
```

#### 4.测试添加索引

 

```java
   void testAddDocument() throws IOException { 
       //        创建对象        
       TestUser testUser = new TestUser("我叫什么",1); 
       //        创建请求        
       IndexRequest request = new IndexRequest("kgc_index");
       //        规则=sql语句（PUT /kgc_index/_doc/1）        
       request.id("1");        
       request.timeout("1s"); //设置超时时间，默认可以不写 
       //        将对象放进请求中，转为json        
       IndexRequest source = request.source(JSON.toJSONString(testUser), XContentType.JSON); 
       //        客户端发送请求，获得响应结果        
       IndexResponse index = restHighLevelClient.index(request, RequestOptions.DEFAULT);         
       System.out.println(index.toString());        
       System.out.println(index.status());//返回状态    
   }
```

#### **5.获取文档信息**

   

```java
 void testGetDocument() throws IOException {        
     GetRequest request = new GetRequest("kgc_index","1");        
     GetResponse documentFields = restHighLevelClient.get(request, RequestOptions.DEFAULT);        
     System.out.println(documentFields.getSourceAsString());        
     System.out.println(documentFields);    
 }
```

#### 6.更新文档信息

```java
    void testUpdateRequest() throws IOException {        
        UpdateRequest updateRequest = new UpdateRequest("kgc_index","1");         
        TestUser user =new TestUser("我是更新的名字",18);         
        updateRequest.doc(JSON.toJSONString(user),XContentType.JSON);        
        UpdateResponse update = restHighLevelClient.update(updateRequest, RequestOptions.DEFAULT);        
        System.out.println(update.status());    
    }
```

#### 7.删除文档记录

   

```java
 void testDeleteRequest() throws IOException {        
     DeleteRequest deleteRequest = new DeleteRequest("kgc_index","1");         
     DeleteResponse delete = restHighLevelClient.delete(deleteRequest, RequestOptions.DEFAULT);        
     System.out.println(delete.status());    
 }
```

#### 8.批量处理数据

 

```java
   void testBulkRequest() throws IOException {        
       BulkRequest bulkRequest = new BulkRequest();        
       bulkRequest.timeout("10s");        
       ArrayList list = new ArrayList();        
       list.add(new TestUser("西瓜",18));        
       list.add(new TestUser("中瓜",18));        
       list.add(new TestUser("南瓜",18));        
       list.add(new TestUser("北瓜",18));        
       list.add(new TestUser("冬瓜",18));         
       for (int i = 0; i <list.size() ; i++) {
           //          put  /kgc_index/1/数据            
           bulkRequest.add(new IndexRequest("kgc_index").id(""+(i+1)).source(JSON.toJSONString(list.get(i)),XContentType.JSON));        
       }        
       BulkResponse bulk = restHighLevelClient.bulk(bulkRequest, RequestOptions.DEFAULT);        
       System.out.println(bulk.hasFailures());    
   }
```

#### 9.查询

```java
//    SearchRequest搜索请求 
//    SearchSourceBuilder条件构造 
//    HighLightBuiLder构建高亮 
//    TermQueryBuilder精确查询 
//    MatchALLQueryBuiLder 
//    xxx QueryBuilder对应我们刚才着到的命令!    
	@Test    
	void testSearch() throws IOException {        
        SearchRequest searchRequest = new SearchRequest(); 
        //        构建搜索条件        
        SearchSourceBuilder searchSourceBuilder = new SearchSourceBuilder(); 
        //        查询条件，可以使用QueryBuilders工具        
        TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "瓜");        searchSourceBuilder.query(termQueryBuilder); 
        // 分页     searchSourceBuilder.from();      searchSourceBuilder.size();  
        //         构造搜索放进请求。完成        
        searchRequest.source(searchSourceBuilder);
        //          执行请求后获得数据 
        //         重点 search.getHits().getHits()拿到字段，可以用for循环        
        SearchResponse search = restHighLevelClient.search(searchRequest, RequestOptions.DEFAULT);        
        System.out.println(JSON.toJSONString(search.getHits()));        
        System.out.println("----------------");        
        for (SearchHit searchHit: search.getHits().getHits()) {            
            System.out.println(searchHit.getSourceAsMap());        
        }    
    }
```

