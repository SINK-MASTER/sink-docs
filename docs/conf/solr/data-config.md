```xml
<dataConfig>
    <!-- 数据源配置
    	name            数据源名称，随意命名即可
    	type/driver     根据实际连接数据库调整
    	url             数据库链接地址 注意替换地址、端口和数据库名称
    	user/password   数据库用户名及密码
    -->
    <dataSource
        name="OracleDB"
        type="JdbcDataSource"
        driver="oracle.jdbc.driver.OracleDriver"
        url="jdbc.url"
        user="root"
        password="root" />
    <document>
        <!-- 数据实体部分
    		name                实体名称
    		dataSource          指定数据源名称，多数据源时必须指定
    		pk                  主键
    		query               全量查询 SQL
    		deltaQuery          增量查询 SQL
    		                    此处如果数据库内存在 add_time、created_at 一类的字段，且数据类型为 datetime/timestamp，WHERE 条件可直接比较。
    			                如果 add_time 为 10 位 int 时间戳，需要转换后进行比较。
    			                简而言之，增量导入就是用最后一次索引时间 ${dataimporter.last_index_time} 和数据表内新增数据时间进行比较后导入。
    		deltaImportQuery    增量导入 SQL
    		deltaQuery          的作用是查询出哪些 id 为新增数据，然后 deltaImportQuery 再查询出对应 id 的需要导入的数据进行导入。
		-->
        <entity name="answerSynopsis" dataSource="OracleDB" transformer="ClobTransformer" pk="CONTENT_ID"
                query="SELECT D.CONTENT_ID, D.TITLE, D.CONTENT, D.INTEGRAL, D.STAR_NUM, to_char(D.ADD_TIME,'yyyy-MM-dd hh24:mi:ss') as ADD_TIME,
        U.NICK_NAME,U.HEAD_IMG,L.LEVEL_NUM,L.LEVEL_ICON,L.LEVEL_NAME,
                (SELECT COUNT(S.STAR_ID) FROM ANSWER_USER_STAR S WHERE S.PROBLEM_ID = D.CONTENT_ID) AS STARTNUM
        FROM ANSWER_CONTENT_DETAIL D, ANSWER_USER_BASE U, ANSWER_USER_LEVEL L,ANSWER_USER_RELA R
        WHERE U.USER_ID = R.USER_ID
        AND R.USER_LEVEL = L.LEVEL_ID
        AND D.ADD_USER = U.USER_ID
        AND D.APPLY_STATUS = '1'
        AND D.ANSWER_TYPE = '0'
        AND U.IS_ENABLE = '1'
        AND L.IS_DEL = '0'"
        deltaQuery="SELECT D.CONTENT_ID
        FROM ANSWER_CONTENT_DETAIL D, ANSWER_USER_BASE U, ANSWER_USER_LEVEL L,ANSWER_USER_RELA R
        WHERE D.ADD_TIME > TO_DATE('${dataimporter.last_index_time}','yyyy-MM-dd hh24:mi:ss')
        AND U.USER_ID = R.USER_ID
        AND R.USER_LEVEL = L.LEVEL_ID
        AND D.ADD_USER = U.USER_ID
        AND D.APPLY_STATUS = '1'
        AND D.ANSWER_TYPE = '0'
        AND U.IS_ENABLE = '1'
        AND L.IS_DEL = '0'"
        deltaImportQuery="SELECT D.CONTENT_ID, D.TITLE, D.CONTENT, D.INTEGRAL, D.STAR_NUM, to_char(D.ADD_TIME,'yyyy-MM-dd hh24:mi:ss') as ADD_TIME,
        U.NICK_NAME,U.HEAD_IMG,L.LEVEL_NUM,L.LEVEL_ICON,L.LEVEL_NAME,
        (SELECT COUNT(S.STAR_ID) FROM ANSWER_USER_STAR S WHERE S.PROBLEM_ID = D.CONTENT_ID) AS STARTNUM
        FROM ANSWER_CONTENT_DETAIL D, ANSWER_USER_BASE U, ANSWER_USER_LEVEL L,ANSWER_USER_RELA R
        WHERE D.CONTENT_ID = '${dataimporter.delta.CONTENT_ID}'
        AND U.USER_ID = R.USER_ID
        AND R.USER_LEVEL = L.LEVEL_ID
        AND D.ADD_USER = U.USER_ID
        AND D.APPLY_STATUS = '1'
        AND D.ANSWER_TYPE = '0'
        AND U.IS_ENABLE = '1'
        AND L.IS_DEL = '0'">
            <field column="CONTENT_ID" name="contentId"/>
            <field column="TITLE" name="title"/>
            <field column="CONTENT" name="content" clob="true"/>
            <field column="INTEGRAL" name="integral"/>
            <field column="STAR_NUM" name="starNum"/>
            <field column="NICK_NAME" name="nickName"/>
            <field column="HEAD_IMG" name="headImg"/>
            <field column="ADD_TIME" name="addTime"/>
            <field column="LEVEL_NUM" name="levelNum"/>
            <field column="LEVEL_ICON" name="levelIcon"/>
            <field column="LEVEL_NAME" name="levelName"/>
        </entity>
    </document>
</dataConfig>
```