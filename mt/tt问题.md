# 事件管理部分

- 列表搜索

  http://hansolo.rc.test.sankuai.com/risk-container/platform/inflow/search

  ```js
  code: 1
  data: null
  msg: "\n### Error querying database.  Cause: com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Column 'id' in where clause is ambiguous\n### The error may exist in mybatis/mapper/InflowMapper.xml\n### The error may involve com.meituan.rc.hansolo.mapper.InflowMapper.search-Inline\n### The error occurred while setting parameters\n### SQL: SELECT i.id, i.name, i.eventId, i.extraInfo, i.inflowDecision, i.decisionInfo, i.expression, i.creator,date_format(i.createTime,'%Y-%m-%d %H:%i:%s') as createTime,         i.modifier, date_format(i.modTime,'%Y-%m-%d %H:%i:%s') as  modTime, e.name as eventName,e.alias as eventAlias, e.type as eventType         FROM `inflow` i left join `risk_event` e         ON i.eventId = e.id         WHERE 1                                                                                     and (CAST(id as CHAR) LIKE idO
  ```

  

