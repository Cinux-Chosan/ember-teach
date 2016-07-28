`action`��������ʵ�Ĺ�����`javascript`����¼������Ƶģ�����ͨ���û����Ԫ�ش���������Ԫ���ϵ��¼���Ember��action���ֻ������㴫�ݲ�������Ӧ��`controller`��`component`�࣬��`controller`����`component`�ϴ����¼����߼���
׼������������ʹ��[Ember CLI](http://ember-cli.com/user-guide)�����һ������Ϊ`myaction`��`controller`��ͬ����`route`������㲻֪����ôʹ��Ember CLI�뿴ǰ�������[Ember.js ����ָ��֮�ߵ�һ�¶���ģ��С��](http://blog.ddlisting.com/2016/03/18/ember-js-ru-men-zhi-nan-zhi-qi-di-zhang-dui-xiang-mo-xing-xiao-jie/)����ƪ�ļ���������ôʹ��Ember CLI����һ���򵥵�Ember��Ŀ��

### 1��actionʹ��ʵ��
#### 1����route�����Ӳ�������
```javascript
//  apap/routes/myaction.js


import Ember from 'ember';

export default Ember.Route.extend({
	//  ���ز������ݵ�ҳ��
	model: function() {
		return { id:1, title: 'ACTIONS', body: "Your app will often need a way to let users interact with controls that change application state. For example, imagine that you have a template that shows a blog title, and supports expanding the post to show the body.If you add the {{action}} helper to an HTML element, when a user clicks the element, the named event will be sent to the template's corresponding component or controller." };
	}
});
```
��д`model`�ص���ֱ�ӷ���һ���������ݡ�

#### 2����дactionģ��
```html
<!--  //  app/templates/myaction.hbs  -->

<!-- showDetailInfo����¼������ֱ���Ҫ��controller��ķ�������һ�� -->
<h2 {{action ' showDetailInfo '}} style="cursor: pointer;">{{model.title}}</h2>
{{#if isShowingBody}}
<p>
{{model.body}}
</p>
{{/if}}
```
Ĭ����ֻ��ʾ���µı��⣬���û���������ʱ�򴥷��¼�`toggleBody`��ʾ���µ���ϸ��Ϣ��

#### 3����дaction��controllerʵ��ģ������Ҫ���߼�
```javascript
// app/controllers/myaction.js

import Ember from 'ember';

export default Ember.Controller.extend({

	//  ����ҳ��������ϸ�����Ƿ���ʾ
	isShowingBody: false,
	actions: {
		showDetailInfo: function() {
			// toggleProperty����ֱ�Ӱ�isShowingBody����Ϊ�෴ֵ
			// toggleProperty�������飺http://devdocs.io/ember/classes/ember.observable#method_toggleProperty
			this.toggleProperty('isShowingBody');
		}
	}
});
```
����`controller`�Ĵ����߼��㻹����ֱ�ӱ�д�������жϡ�
```javascript
actions: {
		showDetailInfo: function() {
			// toggleProperty����ֱ�Ӱ�isShowingBody����Ϊ�෴ֵ
			// toggleProperty�������飺http://devdocs.io/ember/classes/ember.observable#method_toggleProperty
			// this.toggleProperty('isShowingBody');
			
			// ��������������
			var isShowingBody = this.get('isShowingBody');
			if (isShowingBody) {
				this.set('isShowingBody', false);	
			} else {
				this.set('isShowingBody', true);
			}
		}
	}
```
����㲻ʹ��`toggleProperty`�����ı�`isShowingBody`��ֵ����Ҳ����ֱ�ӱ�д�����޸�����ֵ��
���ִ��URL��[http://localhost:4200/myaction](http://localhost:4200/myaction)��Ĭ�������ҳ�����ǲ���ʾ���µ���ϸ��Ϣ�ģ�������������ᴥ���¼�����ʾ��ϸ��Ϣ������2��ͼƬ�ֱ�չʾ����Ĭ������͵������֮�󡣵������ٴε�����⣬��ϸ�����ֱ�Ϊ���ء�

![ͼƬ1](/content/images/2016/03/35.png)

![ͼƬ2](/content/images/2016/03/36-1.png)

ͨ��������С���ӿ��Կ���`action`����ʹ������Ҳ�Ƿǳ��򵥵ġ���Ҫע����ģ���ϵ�`action`��ָ�����¼�����Ҫ��`controller`��ķ�������һ�¡�

### 2��action����

�������`javascript`�ķ���һ������Ҳ����Ϊ`action`�������ӱ�Ҫ�Ĳ�����ֻҪ��`action`���ֺ��������Ĳ������ɡ�
```html
<p>
<!-- modelֱ����Ϊ�������ݵ�controller -->
<button {{action 'hitMe' model}}>����Ұ�</button>
</p>
```
��Ӧ����`controller`���Ӵ���ķ���`selected`���ڴ˷����ڴ�ӡ��ȡ���Ĳ���ֵ��
```javascript
// app/controllers/myaction.js

import Ember from 'ember';

export default Ember.Controller.extend({

	//  ����ҳ��������ϸ�����Ƿ���ʾ
	isShowingBody: false,
	actions: {
		showDetailInfo: function() {
			//  ����ͬ���������
		},
		hitMe: function(model) {   //  ���������ֿ�������
			console.log('The title is ' + model.title);
			console.log('The body is ' + model.body);
		}
	}
});
```

Ember�涨���Ǳ�д�Ķ�������ķ������Ƿ���`actions`�����ϣ�ڡ���ϣ�ļ����Ƿ���������`controller`�����ϵĲ�������Ҫ����ģ���ϴ��ݵ�����һ�£���������ⶨ�塣���緽��`hitMe`�Ĳ���`model`��Ҳ����ʹ��`m`��Ϊ`hitMe`�����Ĳ�����

���û������ť������Ұɡ��ͻᴥ������`hitMe`��Ȼ��ִ��`controller`��ͬ�������������������������`console`�¿������µĴ�ӡ��Ϣ��

![run result](/content/images/2016/03/37.png)

������Щ��ӡ����ܺõ�˵���˻�ȡ�Ĳ�������ȷ�ġ�

### 3��ָ��action�������¼�����
Ĭ�������`action`��������`click`�¼��������ָ�������¼���������̰����¼�`keypress`���¼���������`javascript`�ṩ�����������Ƶģ�Ψһ��ͬ����Ember��ʶ�����¼�����������ɲ�ͬ������ɵ���Ҫ���л��߷ָ�������`keypress`�¼���Emberģ��������Ҫд��`key-press`��
ע�⣺��ָ���¼���ʱ��Ҫ���¼���������Ϊ`on`�����ԡ�����`on='key-press'`��
```html
<a href="#/myaction" {{action 'triggerMe' on="mouse-over"}}>����Ƶ������ϴ���</a>
```
```javascript
triggerMe: function() {
	console.log('����mouseover�¼���������');
}
```

### 4��ָ��`action`�����¼��ĸ�������

�����㻹����ָ�����¼���ĳ���������Ŵ���`action`��ָ�����¼������簴�¼��̵�`Alt`�ٵ���Żᴥ���¼���ʹ��`allowedkeys`����ָ�����µ����Ǹ�����
```html
<br><br>
<button {{action 'pressALTKeyTiggerMe' allowedkeys='alt'}}>����Alt���������</button>
```

### 5����ֹ��ǩĬ����Ϊ

��`action`������ʹ������`preventDefault=false`���Խ�ֹ��ǩ��Ĭ����Ϊ�����������a��ǩ�����`action`������û�ж������������ô��������ʱֻ��ִ��ִ�е�`action`������`a`��ǩĬ�ϵ���Ϊ���ᱻ������
```html
<a href="http://www.baidu.com" {{action "showDetailInfo" preventDefault=false}}>
������ת
</a>
```

### 6�����԰Ѵ������¼���Ϊ�������ݵ�`controller`

`handlebars`��`action`��������Ƿǳ�ǿ�����������԰Ѵ������¼���Ϊ`action`�Ĳ���ֱ�Ӵ��ݵ�`controller`����������Ҫ��`action`���ַ���`javascript`���¼����������Ĵ��뵱ʧȥ����ʱ����������ͨ��`action`ָ����`dandDidChange`�Ѵ������¼�`blur`���ݵ�`controller`��
```html
<label>ʧȥ����ʱ�򴥷�</label>
<input type="text" value={{textValue}} onblur={{action 'bandDidChange'}} />
```
```javascript
// app/controllers/myaction.js

import Ember from 'ember';

export default Ember.Controller.extend({

	actions: {
		bandDidChange: function(event) {
			console.log('event = ' + event);
		}
	}
	
});
```

![result](/content/images/2016/03/38.png)

�ӿ���̨������������`event`��ֵ��һ����������һ��`focus`�¼���
�����������`action`����������һ������`value='target.value'`(��д��ֻ����`target.value`)֮�󣬴��ݵ�`controller`�����������������ݡ��������¼�������
```html
<input type="text" value={{textValue}} onblur={{action 'bandDidChange' value="target.value"}} />
```

![result](/content/images/2016/03/39.png)

����Ƚ�����˼��ʵ�ֵĹ�����ǰ��Ĳ����������Ƶġ�

### 7��`action`�������ڷǵ��Ԫ����
	`action`���ֿ��������κε�`DOM`Ԫ���ϣ��������������ܵ����Ԫ���ϣ�����`a`��`button`�����������������ǵ����Ԫ����Ĭ��������ǲ����õģ�Ҳ����˵���Ҳ����Ч�ġ���������`div`��ǩ�ϣ���������`div`Ԫ����û�з�Ӧ�ġ��������Ҫ��`div`Ԫ��Ҳ�ܴ��������¼�����Ҫ��Ԫ�����һ��CSS��'cursor:pointer;`��

�ܵ���˵Ember��`action`��������ͨ��javascript���¼��ǲ��ġ��÷���������javascript���¼����ơ�

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
