��������һƪ����һ���ķ�����ʹ�� `ember generate route handlebars-each` �������һ��·���ļ���һ����Ӧ��ģ���ļ���
��һƪ��Ϊ����ܱ�����ǩ������ı����������κεĳ��õĿ��������ж��ܿ�����Ҳ��ʹ�÷ǳ��㷺��һ�����ܡ������ҽ�Ϊ��ҽ���`handlebars`�ı�����ǩ����ʹ�÷�ʽ��EL���ʽ������һ���ġ������㿴һ�������϶�Ҳ�������ˡ����ϻ���˵������ֱ������ʾ����ɣ���

```javascript
//  app/routes/handlebars.js
import Ember from 'ember';
/**
 * ����һ�����ڲ��ԵĶ�������
 */
export default Ember.Route.extend({
	//  ��дmodel�ص���������ʼ����������
    model: function() {
		return [
			Ember.Object.create({ name: 'chen', age: 25}),
			Ember.Object.create({ name: 'i2cao.xyz', age: 0.2}),
			Ember.Object.create({ name: 'ibeginner.sinaapp.com', age: 1}),
			Ember.Object.create({ name: 'ubuntuvim.xyz', age: 3})
		];
	}
});
```

��������ʾ����`route`���ﹹ����һ�����ڲ��ԵĶ������飬ÿ��������2�����ԣ�`name`��`age`����
��������ʾ���ݵ�ģ�壺
```html
<!-- // app/templates/handlebars.hbs -->

{{! ������route�����õĶ������� }}
<ul>
	{{#each model as |item|}}
		<li>Hello everyone, My name is {{item.name}} and {{item.age}} year old.</li>
	{{/each}}
</ul>
```
��û���������Ƶĸо��أ�����EL���ʽ��`forEach`��ǩ������һ���ġ�����������Ӧ�ÿ��Կ������µĽ����

![run result](/content/images/2016/03/21.png)

**���ѣ��ǵô�ʱ���е�URL�Ǹո��½���route��**
���������ʱ��ע��ʹ�ùٷ�����ķ������磬����ʹ��`pushObject`������`push`�����뿴[ǰ�������](http://blog.ddlisting.com/2016/03/17/ember-js-ru-men-zhi-nan-zhi-liu-mei-ju-enumerables/)��

### 1�����������±�
��Щ������ǿ�����Ҫ��ȡ������±꣬������Щʱ����ܻ��±���Ϊ���ݵ���š��뿴�������ʾ��
```html
<!-- // app/templates/handlebars.hbs -->

{{! ������route�����õĶ������� }}
<ul
	{{#each model as |item index|}}
		<li>{{index}} Hello everyone, My name is {{item.name}} and {{item.age}} year old.</li>
	{{/each}}
</ul>
```
��������±��Ǵ�0��ʼ�ģ����㻹������jstl�е�`forEach`��ǩ��������д`{{index+1}}`��`handlebars`��������ôд���������ĳɴ�1��ʼ��ô����ʹ��helperʵ�֡���������`@��̨ؼ����`��˵�ķ������й�helper�뿴[Ember.js ����ָ��֮ʮ�˹����������](http://blog.ddlisting.com/2016/03/23/ember-js-ru-men-zhi-nan-zhi-shi-ba-gong-ju-lei-de-zhu-shou/)��

### 2�������鴦��
��each��ǩ�ڻ�����ʹ��{{else}}��������Ϊ�յ�ʱ��ͻ�ִ��else����顣
```html
{{! �����鴦�������route���ص�modelΪ�գ����ִ��else�����Ĵ��� }}
{{#each model as |item|}}
	Hello, {{item.name}}
{{else}}
	Sorry, nobody is here.
{{/each}}
```
Ϊ�˲���Ч�������`app/routes/handlebars.js`��`return`���ĳ�`return []`����ʱ���ص�ģ���ϵ���һ�������飬���Ҳ��Ԥ�ڵ�һ�£�ҳ����ʾ���ǡ�Sorry, nobody is here.����

���������ݾ���`handlebars`��`each`����ʹ��ʵ����Ӧ��Ҳ��ûʲô�Ѷȵġ���
<br>

����л��[@��̨ؼ����](http://t.qq.com/falaoyunfeiluan)���顣
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
