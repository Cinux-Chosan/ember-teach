�������һ����Զ����ĺ��ӡ���ǰ��������н��ܹ��������ôͨ�����Դ��ݲ����������������ֵ�������ģ�����js�����л�ȡ��

���ǵ�ĿǰΪֹ��û���ܹ�������Ӹ�����л�ȡ���飬��[Ember](http://emberjs.com)Ӧ�������֮���ͨ����ͨ��`actions`ʵ�ֵġ�

��������Ĳ�����������һ�����֮��ͨ�ŵ�ʾ����

#### 1���������

��������ķ��������Ҷ�˵��ֱ��ʹ��[Ember CLI](http://ember-cli.com/user-guide)��������ɡ�
```
ember g component button-with-confirmation
ember g component user-profile
ember g route button-with-confirmation-route
```
Ϊ�˲��Է����������һ��·�ɡ�

���������`user-profile`�Ķ��壬�������`button-with-confirmation`����ô��ʱ`user-profile`��Ϊ�������`button-with-confirmation`��Ϊ�������
```html
<!--  app/temlates/components/user-profile.hbs  -->

{{button-with-confirmation text="Click OK to delete your account"}}
```
#### 2��������������action

Ҫ��`action`��ִ����Ҫ������������

* �ڸ�����ж������Ҫ����Ķ�����action��������������и�����Ķ�����Ҫɾ���û��˺Ų�����һ����ʾ��Ϣ����һ�������
* ��������У��жϷ���ʲô�¼�������֪ͨ��Ϣ������������е��û������ȷ�ϡ���ť֮�󴥷�һ���ⲿ�Ķ�����ɾ���˻����߷�����ʾ��Ϣ����

������ʵ�ִ��룺

**ʵ�ָ����������action��**

�ڸ�����У�����õ��û������ȷ�ϡ�֮�󴥷��Ķ���������������еĶ�����`action`�������ҳ��û��˺���ɾ����

��[Ember](http://emberjs.com)Ӧ���У�ÿ���������һ����Ϊ`actions`�����ԡ��������ֵ�Ǻ������ǿ��Ա��û����������ִ�еĺ�����
```js
//  app/components/user-profile.js

import Ember from 'ember';

export default Ember.Component.extend({
	actions: {
		userDidDeleteAccount: function() {
			console.log(��userDidDeleteAccount����);
		}
	}
});
```
�����Ѿ�ʵ���˸�����߼������ǲ�û�и���Ember�������ʲôʱ�򴥷�����һ����ʵ��������ܡ�

**ʵ�������������action��**


��һ�����ǽ�ʵ�ֵ��û������ȷ����֮�󴥷��¼����߼���
```js
//  app/components/button-with-confirmation.js

import Ember from 'ember';

export default Ember.Component.extend({
	tagName: 'button',
	click: function() {
		if (confirm(this.get('text'))) {
			// �������ȡ��������¼������ݣ�������
		}
	}
});
```

#### 3������action�������

����������`user-profile`�����ʹ��`onConfirm()`�����������`button-with-confirmation`���е�`userDidDeleteAccount`�¼���
```html
<!--  app/temlates/components/user-profile.hbs  -->

{{#button-with-confirmation text="Click OK to delete your account" onConfirm=(action 'userDidDeleteAccount')}}
ִ��userDidDeleteAccount����
{{/button-with-confirmation}}
```
��δ������˼�Ǹ��߸������`userDidDeleteAccount`������ͨ��`onConfirm`����ִ�С�

������������������ʹ��`onConfirm`����ִ�и�����Ķ�����
```js
//  app/components/button-with-confirmation.js

import Ember from 'ember';

export default Ember.Component.extend({
	tagName: 'button',
	click: function() {
		if (confirm(this.get('text'))) {
			// �ڸ�����д�������
			this.get('onConfirm')();
		}
	}
});
```
`this.gete(��onConfirm��)`�Ӹ��������һ��ֵ`onConfirm`��Ȼ����`()`��ϳ���һ��������`onConfirm()`��

��ģ��`button-with-confirmation-route.hbs`�е��������
```html
<!--  app/temlates/button-with-confirmation-route.hbs  -->

{{user-profile}}
```

![���](/content/images/2016/04/128.png)

������`button`���ᴥ���¼��������Ի����ٵ����ȷ�ϡ���ִ�з���`userDidDeleteAccount`�����Կ������������̨�����**userDidDeleteAccount��**��δ�����ȷ�ϡ�ǰ���ߵ����ȡ����������������Ϣ��˵����ִ���������`userDidDeleteAccount`��

![�����ͼ](/content/images/2016/04/129.png)

![�����ͼ](/content/images/2016/04/130.png)

����ͨ���ԣ�`actions`���������һ�����ԣ�Ψһ�������ǣ���������Ϊһ����������֪����δ�������Ϊ��

�������`actions`�����ж���ķ����������������ôȥ����һ���¼���������ģ�黯�������������ʡ�


���ˣ������һ�½ڵ�����ȫ����������ˣ���֪���㿴���˶��٣�������������������һ����ѧϰ����ȡ��ֱ��ȥ����ѧϰ�ٷ��̡̳�

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������






