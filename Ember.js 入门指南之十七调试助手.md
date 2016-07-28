Ember�����ṩ��ר�����ڵ���Ember����Ĺȸ衢�����������[Ember Inspector](https://github.com/emberjs/ember-inspector)( ��װ���������Ҫ��ǽ�������Ҳ��һ������Ա���뷭ǽ��������˵Ӧ�ò���ʲô���£�����)�����ṩ�����ڵ��Ե�`helper`��
���չ�����������׼���������ֱ�ִ��[Ember CLI](http://ember-cli.com/user-guide)�����`controller`��`route`��ģ�壺
```
ember generate controller dev-helper
ember generate route dev-helper
```

### 1����־����`{{log}}`

`{{log}}`���԰Ѵ�`controller`��`route`�ഫ�ݵ�ҳ���ϵ�ֵ����־����ʽֱ�������������Ŀ���̨�ϡ����������`controller`����Ӳ������ݡ�
```javascript
// app/controllers/dev-helper.js

import Ember from 'ember';

export default Ember.Controller.extend({
	testName: 'This is a testvalue...'
});
```
���ǿ�����ģ����ֱ����ʾ�ַ���`testName`��ֵ��Ҳ����ʹ��`{{log}}`��������־��ʽ����ڿ���̨����Ȼ��Ҳ����ֱ��ʹ��`{{log 'xxx'}}`�ڿ���̨��ӡ"xxxx"���ڶ���ϵ����ֵ�ʾ���н�Ϊ����ʾ`{{log 'xxx'}}`�÷���
```html
<!-- app/templates/dev-helper.hbs -->

ֱ����ʾ��ҳ���ϣ�{{testName}}
{{log testName}}
```
����[http://localhost:4200/dev-helper](http://localhost:4200/dev-helper)֮�����ǿ�����ҳ���Ͽ����ַ���`testName`��ֵ���򿪹ȸ���߻���Ŀ���̨��console��ǩ�£����Կ���Ҳ��ӡ���ַ���ֵ���Ƚϼ��ҾͲ��ٽ�ͼ�ˡ���

### 2���ϵ�����`{{debugger}}`

������Ҫ���Ե�ʱ���������ģ������Ҫ��Ӷϵ�ĵط����������֣����е�ʱ����Զ�ͣ�����������ֵĵط���
```html
{{log '��仰�ڶϵ�ǰ��'}}
{{debugger}}
<br>
{{log '��仰�ڶϵ����'}}
```
������������ͣ����`{{debugger}}`��һ�С�����̨Ӧ�û��ӡ����仰�ڶϵ�ǰ�桱��Ȼ��ͨ�������һ�������ϵ㣬Ȼ�������ӡ����仰�ڶϵ���桱��<br>
���н�����ý�ͼ��������Լ����԰ɣ�����<br>
����ʹ����`{{debugger}}`�����ҳ���ֹͣ����debug״̬��ʱ�������ֱ�������������̨������������`get('key')`����ȡ`controller`���õ�ֵ��

![result](/content/images/2016/03/43.png)

�ڼ�ͷ��ָ��λ������`get('testName')`��Ȼ��`enter`��ִ�С���õ����½����

![result](/content/images/2016/03/44.png)

���Կ�����ȷ�Ļ�ȡ����ǰ����`controller`�������õ�ֵ��
����㲻���ڵ���ģʽ������`get('testName')`��ô����ʾ���´���

![result](/content/images/2016/03/45.png)



�㻹�����ڱ�������`{{each}}`��ʹ��`{{debugger}}`�����һ�Ρ���һ�����ͻ�ִ��һ��ѭ����

������д`route`���`model`�ص�����������Ӳ������ݡ�
```javascript
//  app/routes/dev-helper.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return [
			{ id: 1, name: 'chen', age: 25 },
			{ id: 2, name: 'ibeginner.sinaapp.com', age: 2 }
		];
	}
});
```
��ģ���`each`������ʹ��`{{debugger}}`���֡�
```html
{{#each model as |item|}}
    {{debugger}}
    <li>item</li>
{{/each}}
```

���У�������Զ�����debugģʽ����������Զ�����debugģʽ�����ֶ���`F12`����debug������ʱ����������������̨��������`get('item.name')`����ȡ����ѭ�����������ֵ��Ȼ���㼸�㡰��һ�������߰�`F8`�������Զ����뵽��һ��ѭ����Ȼ����������`get('item.name')`����ʱ�õ����Ǳ���ѭ����������ֵ��Ȼ������һ�����߰�F8���������ѭ��������`route`�����÷��ص�����ֻ��2��Ԫ�أ��������Ѿ�û��Ԫ�ء�������λ��Զ��˳�debugģʽ��
�������������ɻ�õ���ͼ��ʾ�������Ϣ��

![result](/content/images/2016/03/46.png)

�ڵ���״̬���㻹����ֱ�������������̨����������`context`��ȡ��������Ϣ���������ҳ��������������������ԡ�

![result](/content/images/2016/03/47.png)

�������ܵľ���Ember�ṩ�ĵ������ֵ�����ʹ�÷��������㿪��EmberӦ�õ�ʱ��Ӧ���Ǻ����õģ��ر�����`each`ѭ��������ʱ��
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������


