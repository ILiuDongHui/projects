Web.config配置说明：
<connectionStrings>
    <add name="ConnectionString" connectionString="server=127.0.0.1;uid=sa;pwd=ok;database=PetShop;Max Pool Size =512; Min Pool Size=0; Connection Lifetime = 300;packet size=1000;" providerName="System.Data.SqlClient" />
</connectionStrings>

调用函数示例：
sql = "UPDATE Student set Name = @Name WHERE Id = @Id";

SqlHelper.ExecuteNonQuery(C
	ommandType.Text, 
	sql, 
	new SqlParameter[]{
		new SqlParameter("@Name", name),
		new SqlParameter("@Id", id)
	}
);