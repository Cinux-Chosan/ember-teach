׼��������
```
ember g route wrapping-content-in-component-route
ember g component wrapping-content-in-component	
```
��Щ����£�����Ҫ����һ����������ģ���ṩ�����ݵ������������������ӣ�
```html
<!--  app/templates/components/wrapping-content-in-component.hbs  -->

<h1>{{title}}</h1>
<div class='body'>{{body}}</div>
```
�������붨����һ����ͨ�������
```html
<!--  app/templates/wrapping-content-in-component-route.hbs  -->

{{wrapping-content-in-component title=model.title body=model.body}}
```
�����������������ָ�����ƵĲ����������й�����������������뿴[Ember.js ����ָ��֮��ʮ�����Դ���](http://blog.ddlisting.com/2016/04/07/ember-js-ru-men-zhi-nan-zhi-er-shi-jiu-shu-xing-chuan-di/)��

������`route`������һЩ�������ݡ�
```js
//  app/routes/wrapping-content-in-component-route.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return { id: 1, title: 'test title', body: 'this is body ...', author: 'ubuntuvim' };
	}
});
```
����������ûд������Ӧ�û���ʾ������Ϣ��

![�����ͼ](/content/images/2016/04/123.png)

���������������������ʾ��`model`�ص��г�ʼ�������ݡ���������㶨��������Ҫ�����Զ����HTML�����أ���

�����������ּ򵥵����ݴ���֮�⣬[Ember](http://emberjs.com)��֧��ʹ��`block form`���鷽ʽ�������仰˵�����ֱ�Ӵ���һ��ģ�嵽����У����������ʹ��`{{yield}}`������ʾ���������ģ�塣

Ϊ����ʹ�ÿ鷽ʽ����ģ�嵽����У��ڵ��������ʱ�����ʹ��`#`��ʼ�ķ�ʽ�����ֵ��÷�ʽ��`{{component-name}}`����`{{#component-name}}����{{/component-name}}`����ע��һ��Ҫ�йرձ�ǩ��

�ԼӸ���ǰ������ӣ���ʱ��ֻ�Ǵ���һ���򵥵����ݣ����Ǵ���һ������HTML��ǩ�ļ�ģ�塣
```html
<!--  app/templates/components/wrapping-content-in-component.hbs  -->

<h1>{{title}}</h1>
<!--  ģ�������Ⱦ֮��{{yield}}���ֻᱻ�����ǩwrapping-content-in-component�����������滻�� -->
<div class='body'>{{yield}}</div>
```
ע���ʱ`div`��ǩ��ʹ�õ���`{{yield}}`���֣�������ֱ��ʹ��`{{body}}`��

�����ǵ��������ģ�塣
```html
<!--  app/templates/wrapping-content-in-component-route.hbs  -->

{{!wrapping-content-in-component title=model.title body=model.body}}
<!--  ��������ķ�ʽ�������Ա�ǩ����ʽ��
	ģ�������Ⱦ֮��small��ǩ��{{body}}�����е����ݻ���Ⱦ�����wrapping-content-in-component��{{yield}}������  -->
{{#wrapping-content-in-component title=model.title}}
	{{model.body}}
	<small>by {{model.author}}</small>
{{/wrapping-content-in-component}}
```
ҳ�����֮��Ч�����£�

![ҳ��Ч��](/content/images/2016/04/125.png)


�鿴ҳ��HTMLԴ���룬���Կ�����`<div class="body">`�����ǩ�ڵ�����ȷʵ�ǵ������`wrapping-content-in-component`��������ļ�HTMLģ�塣����԰�`{{#wrapping-content-in-component}}����{{/wrapping-content-in-component}}`�м�����ݵ�����һ��������⡣

![ҳ��Ч��](/content/images/2016/04/125-1.png)

��������������ݵ�֪ʶ�������ϣ����ݺ���Ҳ�Ƚϼ򵥣������������������Ի���ֱ�ӿ�[�ٷ��̳�](guides.emberjs.com/v2.0.0/components/wrapping-content-in-a-component/)��

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
