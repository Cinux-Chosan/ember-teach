��ƪ֮ǰ��6ƪ���¶��ǵ�һ�µ����ݣ���һ�½���Ҫ������`Ember`�Ķ���ģ�͡���������Ҫ���Ǽ������Ժ�ö����2�£��ǳ�֮��Ҫ��һ��Ҫ�ú����գ�

��һ�½��ǵڶ���ģ�壬`Ember`Ӧ��ʹ�õ�ģ�����`handlebar`��[���Ҳ鿴�����йش�ģ��Ľ���](http://handlebarsjs.com/)�������ģ��⹦��ǿ���зḻ�ı�ǩ�������жϱ�ǩ`if`��`if else`,�Լ�������ǩ`each`�ȵȡ�

���⣬����һ�¿�ʼ�����ǲ����Լ��ֶ��`Ember`��Ŀ��Ҳ�����ֶ�����`Ember`���ļ�������ʹ�ùٷ��ṩ��һ���ǳ����Ĺ������ߡ���`Ember CLI`��Ҫʹ����������������Ȱ�װ�����á�����������ַ�ǽ��ܰ�װ�����õģ��Ƽ���һ������

1. [http://www.ember-cli.com/user-guide/](http://www.ember-cli.com/user-guide/)
2. [https://guides.emberjs.com/v2.4.0/getting-started/](https://guides.emberjs.com/v2.4.0/getting-started/)

`Ember CLI`��һ���ǳ���Ҫ�Ĺ������ߣ�������Ϊ�����ߴ����ļ�����ʼ�����̶ֹ��Ĵ��롣�����������С����������`Ember`Ӧ�á�

����ʹ��������ߴ���һ���µ�`Ember`��Ŀ`chapter2_tempalte`��

1. �½���Ŀ����: 
`ember new chapter2_tempalte`
2. ������ĿĿ¼�������������� 
`cd chapter2_template`<br>
`ember server`
3. ������Ŀ���������������ӣ�[http://localhost:4200/](http://localhost:4200/)��������ܿ���������Ϣ˵����װ�ɹ��ˡ�

![run proj](/content/images/2016/03/14-1.png)

�����Ŀ�����ɹ�����Լ������¿��������Ŀ�������ɹ������ԣ���Ϊ����Ĵ��붼���������Ŀ����ʾ�ģ��������ڴ�����Ŀ��õ���ÿ���ļ���Ŀ¼���㿴�����ĵ���������зǳ���ϸ��˵����Ϊ�˷��������ڴ˾ͼ򵥽������м�������Ҫ���ļ���Ŀ¼��
<table border="1" style="border: 1px solid #ccc !important;">
  <tr bgcolor="#ccc" style="border: 1px solid #ccc !important;">
<td>Ŀ¼</td>	<td>˵��</td>
</tr>
<tr>
<td>app	</td>	<td>��Ŀ����Ҫ���붼�Ƿ������Ŀ¼��</td>
</tr>
<tr>
<td>app/controllers</td>	<td>���C��MVC���㣨controller���Ĵ����ļ�</td>
</tr>
<tr>
<td>app/helpers</td>	<td>	����Զ����helper�����ļ�</td>
</tr>
<tr>
<td>app/models	</td>	<td>���M��MVC���㣨model�������ļ�</td>
</tr>
<tr>
<td>app/routes</td>	<td>	�����Ŀ·�����ô����ļ�</td>
</tr>
<tr>
<td>app/templates	</td>	<td>�����Ŀģ������ļ�</td>
</tr>
<tr>
<td>bower_components</td>	<td>���ʹ��bower���װ�ĵ����������</td>
</tr>
<tr>
<td>bower.json</td>	<td>����ʹ��bower���װ�ĵ������������</td>
</tr>
<tr>
<td>package.json</td>	<td>����ʹ��npm���װ�ĵ������������</td>
</tr>
<tr>
<td>node_modules</td>	<td>���ʹ��npm���װ�ĵ����������</td>
</tr>
<tr>
<td>ember-cli-build.js	</td>	<td>���ù����淶�������������</td>
</tr>
<tr>
<td>dist	</td>	<td>��ű����������Ŀ�ļ�������ֱ�Ӹ��Ƶ�������������</td>
</tr>
</table>
������Щ�ļ�����Ŀ¼�Ǻ��濪�����̾������õ����������Ŀ¼���ļ���˵��ЩĿ¼���ļ��Ǻ���Ҫ�ģ�ֻҪ����ʹ��`ember new appName`�������ɵ���Ŀ�������������ЩĿ¼�����ļ�����������Ҫ�ľ���`app`Ŀ¼�µ��ļ���Ŀ¼�ˣ���`app`�����Ŀ¼�����Ϳ��Ժ�����Ŀ������Ǹ�`MVC`��ܵ���Ŀ��`Ember`֮�������ҵ�`controller`��Ӧ��`template`Ҳ�Ǹ���Ŀ¼���ļ��������ҵ��ģ�`Ember`�����Լ���һ����������ģ���������˽�����й���Ϣ���Ʋ�[folder-layout](http://ember-cli.com/user-guide/#folder-layout)��

��û���֮��ʼ���ǵ�`Ember`֮�ðɣ�����
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������

