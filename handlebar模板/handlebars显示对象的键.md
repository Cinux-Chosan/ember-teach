��ʵ�ʵĿ�������������п�����Ҫ��ʾ����������ļ�����ֵ���������Ҫͬʱ��ʾ������ļ���ֵ�����ʹ��`{{#each-in}}`��ǩ��<br>
ע�⣺`each-in`��ǩ��`Ember 2.0`���еĹ��ܣ�֮ǰ�İ汾���޷�ʹ�������ǩ�ģ������2.0һ�µİ汾�ᱨ��`Uncaught Error: Assertion Failed: A helper named 'each-in' coulad not be found`<br>
׼��������ʹ��`Ember CLI`����һ��`component`�����ͬʱ������һ����Ӧ��ģ���ļ���<br>
`ember generate component store-categories`<br>
ִ����������õ������3���ļ���
```
app/components/store-categories.js
app/templates/components/store-categories.hbs
tests/integration/components/store-categories-test.js
```
Ȼ����`app/router.js`����һ��·�����ã���`map`���������`this.route('store-categories');`����ʱ����ֱ�ӷ���[http://localhost:4200/store-categories](http://localhost:4200/store-categories);

[http://guides.emberjs.com/v2.0.0/templates/displaying-the-keys-in-an-object/](http://guides.emberjs.com/v2.0.0/templates/displaying-the-keys-in-an-object/)

#### ����������Ӳ�������

```javascript
// app/components/store-categories.js
import Ember from 'ember';

export default Ember.Component.extend({
    // https://guides.emberjs.com/v2.4.0/components/the-component-lifecycle/
	willRender: function() {
		//  ����һ���������ԡ�categories���ϣ��������õ�categories�����ϵĶ���ṹ�ǣ�keyΪ�ַ�����valueΪ����
		this.set('categories', {
	      'Bourbons': ['Bulleit', 'Four Roses', 'Woodford Reserve'],
	      'Ryes': ['WhistlePig', 'High West']
	    });
	}
));
```

`willRender`�����������Ⱦ��ʱ��ִ�У������й�����Ľ��ܻ��ں����½ڡ�������н��ܣ����˽�����й�����Ľ��ܻ��ں����������һһ���ܣ�Ŀǰ�����Ұ����������һ����ȡ�����Ĺ���HTML���롣

���˲�������֮��������ôȥʹ��`each-in`��ǩ����������ļ��أ�

```html
<!-- // app/templates/components/store-categories.hbs -->
<ul>
  {{#each-in categories as |category products|}}
    <li>{{category}}
      <ol>
        {{#each products as |product|}}
          <li>{{product}}</li>
        {{/each}}
      </ol>
    </li>
  {{/each-in}}
</ul>
```

����ģ������е�һ��λ�ò���`category`���ǵ������ļ����ڶ���λ�ò���`product`���Ǽ�����Ӧ��ֵ��

Ϊ����ʾЧ������`application.hbs`�е���������������ĵ��÷ǳ��򵥣�ֱ��ʹ��`{{�����}}`��ʽ���á�

```html
<!-- //app/templates/application.hbs -->
{{store-categories}}
```

��Ⱦ��������ͼ��

![result](/content/images/2016/03/23.png)



### ����Ⱦ

**`{{each-in}}`���ʽ�����������ֵ�仯���Զ����¡�**����ʾ���У�����������`categories`����һ��Ԫ��ֵ��ģ������ʾ�����ݲ����Զ����¡�Ϊ����ʾ������������������һ���������Ա仯�İ�ť��������Ҫ�������`app/components/store-categories.js`������һ��`action`�������й�action���ں�����½ڽ��ܣ���ʱ����������һ����ͨ��js��������Ȼ����`app/templates/components/store-categories.hbs`������һ�������İ�ť��

```javascript
import Ember from 'ember';

export default Ember.Component.extend({
	// willRender�����������Ⱦ��ʱ��ִ�У������й�����Ľ��ܻ��ں����½ڡ���������н���
	willRender: function() {
		//  ����һ���������ԡ�categories���ϣ��������õ�categories�����ϵĶ���ṹ�ǣ�keyΪ�ַ�����valueΪ����
		this.set('categories', {
	      'Bourbons': ['Bulleit', 'Four Roses', 'Woodford Reserve'],
	      'Ryes': ['WhistlePig', 'High West']
	    });
	},
	actions: {
		addCategory: function(category) {
			console.log('�������');
			let categories = this.get('categories');
			// console.log(categories);
			categories['Bourbons'] = [];
			//  �ֶ�ִ������Ⱦ��������domԪ�أ����ǲ�û�дﵽԤ��Ч��
			// ����֪����ʲôԭ��
			this.rerender();
		}
	}
});
```

```html
<!-- // templates/components/store-categories.hbs -->

<ul>
  {{#each-in categories as |category products|}}
    <li>{{category}}
      <ol>
        {{#each products as |product|}}
          <li>{{product}}</li>
        {{/each}}
      </ol>
    </li>
  {{/each-in}}
</ul>

<button onclick={{action 'addCategory'}}>����������</button>
```

���Ǻ��ź�����ʹ���ֶ�������`rerender`����Ҳû�취��������Ⱦ��������ʾ�����ݲ�û�з����仯�������ҵ�ԭ����ٲ��ϣ���

### �����鴦��

�����鴦������ʽ`{{each}}`һ����ͬ�����ж����Բ���`null`��`undefined`��`[]`����ʾ�����ݣ�����ִ��`else`���֡�

```html
{{#each-in people as |name person|}}
  Hello, {{name}}! You are {{person.age}} years old.
{{else}}
  Sorry, nobody is here.
{{/each-in}}
```

���Բο���һƪ��`{{each}}`��ǩ���ԣ����ﲻ��׸����
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
