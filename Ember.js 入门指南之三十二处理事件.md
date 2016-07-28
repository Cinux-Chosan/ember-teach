��������������Ӧ�¼��������û���˫������껬�������̵İ��µȵ��¼���ֻ��Ҫ�������������[Ember](http://emberjs.com)�ṩ�Ĵ����¼���Ȼ��[Ember](http://emberjs.com)���Զ��ж��û��Ĳ���ִ����Ӧ���¼���ֻҪ�����������ӵ��¼�����ͻ������һ�������Ӷ���¼����¼�ִ�д�����ݴ����Ĵ���ִ�С�

1�����¼�����
׼��������ʹ��[Ember CLI](http://ember-cli.com/user-guide)������ʾ�����ļ���
```
ember g component handle-events
ember g route component-route
```
���ɵ����ģ�岻���κ��޸ġ�
```html
<!--  app/components/handle-events.hbs -->

{{yield}}
```
ע�⿴������ʵ�֣�
```js
//  app/components/handle-events.js

import Ember from 'ember';

export default Ember.Component.extend({
	click: function() {
		alert('click...');

		return true;  // ����true�����¼�ð�ݵ������
	},
	mouseLeave: function() {
		alert("mouseDown....");

		return true;
	}
});
```
��������������������¼�`click`��`mouseLeaver`��һ���ǵ����¼�һ��������ƿ��¼�������[Ember](http://emberjs.com)֧�ֵ��¼��뿴[handling-events](https://guides.emberjs.com/v2.4.0/components/handling-events/#toc_event-names)��

���������ģ�����£�
```html
<!--  app/templates/component-route.hbs  -->

{{#handle-events}}
<span style="cursor: pointer;">��������Ʈ�����ߵ��Ҷ��ᴥ���¼�~</span>
{{/handle-events}}
```
���û�ֻ�ǰ��������֡���������Ʈ�����ߵ��Ҷ��ᴥ���¼�~���ϻ�����ִֻ��`mouseLeave`�¼������û��������ʱ��ִ��`click`�¼���ִ��`mouseLeave`�¼�����Ϊ�û��������ʱ��껹û�ƿ���

������������ӵ��¼����г�ͻ�Ŀ��ܻ�õ��޷�Ԥ֪�Ľ�����������������������˫���͵����¼�����ʱֻ��ִ�е����¼���˫���¼����޷�������

## 2��������Ϊ

ĳЩ����£���������Ҫ֧���Ϸ��¼��������������Ҫ����һ��`id`��`drop`�¼��С�
```html
{{drop-target action=��didDrop��}}
```
����Զ���������¼�������ȥ����`drop`�¼����������Ҫ����ͨ������`false`��ֹ�¼�ð�ݡ�
```js
//  app/components/drop-target.js

import Ember from 'ember';

export default Ember.Component.extend({
	attribuBindings: ['draggable'],
	draggable: 'true',

	dragOver: function() {
		return false;
	},
	didDrop: function(event) {
		let id = event.dataTransfer.getData('text/data');
		this.sendAction('action', id);
	}
});
```
�������ݲ��࣬�ص��ǵ�һ������ݣ��ڶ�������ݾͼ򵥽��ܣ�������ϸ��Ϣ���Ʋ�[�����ĵ�](guides.emberjs.com/v2.0.0/components/handling-events/)��

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
