
�ӱ�ƪ��ʼ��������¿�������`controller`��E`mber2.0`��ʼԽ��Խ�����ˣ�ְ��Ҳ���ӵ�һ���������߼���

������׼��������
���´���һ��[Ember](http://emberjs.com)��Ŀ���Ծ�ʹ�õ���[Ember CLI](http://ember-cli.com/user-guide)�������
```
ember new chapter5_controllers
cd chapter5_controllers
ember server
```
�������ִ����Ŀ������������Ϣ˵����Ŀ��ɹ���
**Welcome to Ember**��

## 1�����������

������������ǳ����ƣ��ɴˣ���δ�����°汾�к��п������������ȫȡ�����������ܿ�������Ember�汾�ĸ��¿��������˳�[Ember](http://emberjs.com)��Ŀǰ�İ汾�����������ֱ��ͨ��·�ɷ��ʣ���Ҫͨ��ģ����ò���ʹ�����������δ���İ汾����������⣬��ʱ��`controller`���ܾ���Ĵ�[Ember](http://emberjs.com)�˳��ˣ�

������ˣ�ģ�黯��EmberӦ�ú����õ�`controller`��������ʹ����`controller`Ҳ��Ϊ�˴���������������飺

1. `controller`��Ҫ��Ϊ��ά�ֵ�ǰ·��״̬��һ����˵��model�����Իᱣ�浽������������`controller`������ȴ���ᱣ�浽��������
2. ����ϵĶ�����Ҫͨ��`controller`��ת��`route`�㡣

ģ�������ĵ���Ⱦ��ͨ����ǰ`controller`��·�ɴ���ġ�[Ember](http://emberjs.com)��׷��������ǡ�Լ���������á�����Ҳ����ζ�������ֻ��Ҫһ��`controller` ��ʹ���һ����������һ��Ϊ�ˡ����ڹ�������

�������������ʾ·����ʾ`blog post`������ģ��`blog-post`����չʾģ��`blog-post`�����ݣ��������ģ�Ͱ����������ԣ���������`id`����Ϊ��`model`�в���Ҫ�ֶ�ָ��`id`���ԣ���

* title 
* intro
* body
* author

`model`�������£�
```js
//  app/models/blog-post.js

import DS from 'ember-data';

export default DS.Model.extend({
  title: DS.attr('string'),  //  ����Ĭ��Ϊstring���ͣ����Բ�ָ��
  intro: DS.attr('string'),
  body: DS.attr('string'),
  author: DS.attr('string')
});
```
��`route`�����Ӳ������ݣ�ֱ�ӷ���һ��`model`����
```js
//  app/routes/blog-post.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		var blogPost = this.store.createRecord('blog-post', {
			title: 'DEFINING A COMPONENT',  //  ����Ĭ��Ϊstring���ͣ����Բ�ָ��
			intro: "Components must have at least one dash in their name. ",
			body: "Components must have at least one dash in their name. So blog-post is an acceptable name, and so is audio-player-controls, but post is not. This prevents clashes with current or future HTML element names, aligns Ember components with the W3C Custom Elements spec, and ensures Ember detects the components automatically.",
			author: 'ubuntuvim'
		});
		// ֱ�ӷ���һ��model����������Է���promises��
		return blogPost;
	}
});
```
��ʾ��Ϣ��ģ�����£�
```html
<!--  app/templates/blog-post.hbs  -->

<h1>{{model.title}}</h1>
<h2>{{model.author}}</h2>

<div class="intro">
	{{model.intro}}
</div>

<hr>

<div class="body">
	{{model.body}}
</div>
```
�����Ĵ���û�б�д������ôҲ��õ����½����

![���](/content/images/2016/04/131.png)

**Welcome to Ember**����ģ�����Ϣ���������`application.hbs`��ɾ�������Ǽǵò�Ҫɾ��`{{outlet}}`������ʲô��ϢҲ����ʾ��

���������û����ʾ�κ��ض������Ի���ָ���Ķ�����`action`������ʱ����������model���������ݵĽ�ɫ������ģ�����Ե�`pass-through`���������
ע�⣺��������ȡ��`model`�Ǵ�`route`�õ��ġ�

����Ϊ�����������һ�����ܣ��û����Ե�����ⴥ����ʾ��������`post`�����ݡ�ͨ��һ������`isExpanded`���ƣ�����ֱ��޸�ģ��Ϳ������Ĵ��롣
```js
//  app/controllers/blog-post.js

import Ember from 'ember';

export default Ember.Controller.extend({
	isExpanded: false,  //Ĭ�ϲ���ʾbody
	actions: {
		toggleBody: function() {
			this.toggleProperty('isExpanded');
		}
	}
});
```
��`controller`������һ������`isExpanded`������㲻��`controller`�ж����������Ҳ�ǿ��Եġ��������`controller`����Ľ����뿴[Ember.js ����ָ��֮ʮ��{{action}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-wu-action/)��
```html
<!--  app/templates/blog-post.hbs  -->

<h1>{{model.title}}</h1>
<h2>{{model.author}}</h2>

<div class="intro">
	{{model.intro}}
</div>

<hr>
{{#if isExpanded}}
	<button {{action 'toggleBody'}}>hide body</button>
	<div class="body">
		{{model.body}}
	</div>
{{else}}
	<button {{action 'toggleBody'}}>Show body</button>
{{/if}}
```
��ģ����ʹ��`if`�����ж�`isExpanded`��ֵ�����Ϊ`true`����ʾ`body`��������ʾ��

ҳ�����֮�������£������ǲ���ʾ`body`���ݣ������ť��Show body������ʾ���ݣ����Ұ�ť��Ϊ��hide body����Ȼ���ڵ�������ť����ʾ`body`���ݡ�

![����](/content/images/2016/04/132.png)

![չ��](/content/images/2016/04/133.png)

����`controller`��ְ����Ӧ�ô����˽��ˣ�����Ҫ���������߼����жϡ��������������������ж�`body`���ݵ���ʾ�����ʵ��Ҳ���԰�`controller`���еĴ���������`route`����Ҳ����ʵ�����Ч��������Ҫ��Ϊ`model`�����Է��أ���`isExpanded`����`model`�����Դ�����������Լ��������ԣ����ǰ��߼��ŵ�`route`�ֻ�ʹ��`route`��á���רһ���ˣ�`route`����Ҫְ���ǳ�ʼ�����ݵġ�������Ҳ��Ember������`controller`��ԭ��֮һ�ɣ���

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������


