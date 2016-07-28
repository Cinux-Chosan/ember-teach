Ember�ṩ�ı�Ԫ�ض��Ǿ�����װ�ģ���װ����`view`���������������Ⱦ֮��ͻ�������ͨ��HTML��ǩ��������ϸ��Ϣ����Բ鿴���ǵ�ʵ��Դ�룺[Ember.TextField](https://github.com/emberjs/ember.js/blob/v2.0.1/packages/ember-views/lib/views/text_field.js#L36)��[Ember.Chechbox](https://github.com/emberjs/ember.js/blob/v2.0.1/packages/ember-views/lib/views/checkbox.js#L10)��[Ember.TextArea](https://github.com/emberjs/ember.js/blob/v2.0.1/packages/ember-views/lib/views/text_area.js#L8)��

���չ������ȴ���һ��`route`��<br>
`ember generate route form-helper`��

### 1��`input`����

```html
{{! //app/templates/form-helper.hbs }}
{{input name="username" placeholder="your name"}}
```

���п���ʹ����`input`�����ϵ������кܶ࣬����`readonly`��`value`��`disabled`��`name`�ȵȣ������йص����Խ������Ʋ�[��������](guides.emberjs.com/v2.0.0/templates/input-helpers/)��
<br>**ע�⣺����ʹ����`input`�����ϵ������ǲ���ʹ��˫������ס��������ġ�����`value='helloworld'`��`value=helloworld`��Ⱦ֮��Ľ���ǲ�һ���ģ���һ��д����ֱ�Ӱ�"helloworld"����ַ�����ֵ���õ�`value`�ϣ��ڶ���д���Ǵ������Ļ�ȡ����helloworld��ֵ�����õ�`value`�ϣ�ͨ������`controller`����`route`���õ�ֵ��**
������2�д������ʾ�����
```html
{{input name="username" placeholder="your name" value="model.helloworld"}}
<br><br>
{{input name="username" placeholder="your name" value=model.helloworld}}
```
�޸Ķ�Ӧ��`route`�࣬��д`model`�ص�������һ���ַ����������������ģ���Ӧ��`controller`�����á���������ĵڶ��δ��루ʹ������`ember generate controller form-helper`�õ�ģ���Ӧ��`controller`�ࡣ
����
```javascript
// app/routes/form-helper.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return { helloworld: 'The value from route...' }
	}
});
```

��`controller`���ʼ���������ݡ�
```javascript
// app/controllers/form-helper.js

import Ember from 'ember';

export default Ember.Controller.extend({
	helloworld: 'The value from route...'
});
```
��Ӧ�ģ������ʹ�õ���`controller`��ʼ���������ݣ���ô���ģ���ȡ���ݵķ�ʽ��Ҫ��΢�޸��¡���Ҫȥ��ǰ׺`model.`��`controller`����Ҫ�ڻص��г�ʼ���������ݣ�����ֱ�Ӷ����`controller`�����ԡ�
```html
{{input name="username" placeholder="your name" value=helloworld}}
```

![���н��](/content/images/2016/03/40.png)

### 2����`input`������ָ�������¼�

����������£�����ƽ��д����javascript���룬���ǿ���ֱ����`input`�������ʹ��javascript�ĺ�����ͬ��ģ�`input`�����Ͽ���ʹ��javascript����������ʹ�÷�ʽ�е����뿴����ʾ�������簴`enter`������ָ�����¼���ʧȥ���㴥���¼��ȵȡ�
���ȱ�д`input`����򣬻�ȡ`input`������ֵ�е㲻������=^=����`controller`���ȡ`input`������ֵ��ͨ������˫���ŵ�`value`���Ի�ȡ�ġ�
```html
��enter������
{{input value=getValueKey enter="getInputValue" name=getByName placeholder="��������Ե�����"}}
```
```javascript
// app/controllers/form-helper.js

import Ember from 'ember';

export default Ember.Controller.extend({
	actions: {
		getInputValue: function() {
			var v = this.get('getValueKey');
			console.log('v = ' + v);

			var v2 = this.get('getByName');
			console.log('v2 = ' + v2);
		}
	}
});
```
����������ݺ�`enter`����

![run result](/content/images/2016/03/41.png)

��������������ôһ������⡣`v`��ֵ����ȷ�ģ�`v2`ȴ��`undefined`���ɼ���`controller`���ȡҳ���ֵ��ͨ��`value`������Զ�����`name`������ԡ�������ƽ��HTML��`input`�е㲻һ���ˣ��������Ҫע���¡�

### 3��`checkbook`����

`checkbox`�����Ԫ��Ҳ�Ǿ���Ember��װ�ˣ���Ϊһ�����ʹ�á�ʹ�ù�����Ҫע���������ǰ���`input`��һ���ģ������ǲ���ʹ��˫��������������ǲ�һ���ġ�
```html
checkbox{{input type="checkbox" checked=isChecked }}
```
�������`controller`����һ������`isChecked`������Ϊ`true`��`checkbox`��Ĭ��Ϊѡ�С�
```javascript
// app/controllers/form-helper.js

import Ember from 'ember';

export default Ember.Controller.extend({
	actions: {
		// ����
	},
	isChecked: true
});
```

![result](/content/images/2016/03/42.png)

### 4��`textarea`����

```html
{{textarea value=key cols="80" rows="3" enter="getValueByV"}}
```
ͬ����Ҳ��ͨ��`value`���Ի�ȡ�����ֵ��

��ƪ�򵥵Ľ����˳��õı�Ԫ�أ�ʹ�õķ�ʽ�Ƚϼ򵥣�Ψһ��Ҫע����ǻ�ȡ�����������ֵ�ķ�ʽ��ƽ��ʹ�õ�HTML��Ԫ���е��������Ļ���������ͨ��HTML��Ԫ��ûʲô���
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
