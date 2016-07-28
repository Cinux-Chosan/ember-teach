·������һ������Ҫ��ְ����Ǽ����ʺϵ�`model`����ʼ�����ݣ�Ȼ����ģ������ʾ���ݡ�

### 1����ͨmodel����

```javascript
//  app/router.js

//  ����

Router.map(function() {
    this.route('posts');
});

export default Router;
```
����`posts`���·�����Ҫ������Ϊ`post`��`model`Ҫ��ô���أ�����ʵ�ֺܼ򵥣���ʵ��ǰ��Ĵ���Ҳ�Ѿ�д���ˡ���ֻ��Ҫ��д`model`�ص����ڻص��з��ػ�ȡ����`model`���ɡ�
```javascript
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		// return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
		// ����post����һ��model��
		return this.store.query('post');
	}
});
```
`model`�ص����Է���һ��[Ember Data](http://emberjs.com/api/data/)��¼�����߷����κε�[promise](http://liubin.org/promises-book/)����[Ember Data](http://emberjs.com/api/data/)Ҳ��`promise`���󣩣��ֻ����Ƿ���һ���򵥵�javascript�������鶼���ԡ�������Ҫ�ȴ����ݼ�����ɲŻ���Ⱦģ�壬�����������ʹ��`Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');`��ȡԶ������ҳ���ϻ���һ��ʱ���ǿհ׵ģ���ʵ�����ڼ������ݣ������������û����鲢���ã�������Ҳ����Ҫ����������⣬Ember�Ѿ��ṩ�˽���취�����ǵ���һƪ�Ľ�ͼ��·�ɱ����ǲ���ÿ��·�ɶ���һ��`xxx_loading`·�ɣ����·�ɾ��������ݼ��ص�ʱ��ִ�еģ��й�`xxx_loading`������ϸ����Ϣ�ں���Ĳ��Ľ��ܡ�

### 2����̬model

һ��`route`��ʱ��ֻ����ͬһ��`model`������·��`/photos`��ͨ���Ǽ���ģ��`photo`������û��뿪���������½������·��ģ��Ҳ����ı䡣
Ȼ������Щ�����·�������ص�`model`�Ǳ仯�ġ�������һ��ͼƬչʾ��APP�У�·��`/photos`�����һ��`photo`ģ�ͼ��ϲ���Ⱦ��ģ��`photos`�ϡ����û��������һ��ͼƬ��ʱ��·��ֻ���ر������`model`���ݣ����û��������һ��ͼƬ��ʱ����ص���������һ��`model`������Ⱦ��ģ���ϣ����������μ��ص�`model`�����ǲ�һ���ġ�

�����������£����ʵ�URL�Ͱ����˺���Ҫ����Ϣ������·�ɺ�ģ�͡�

��EmberӦ���п���ͨ�����嶯̬��ʵ�ּ��ز�ͬ��ģ�͡��йض�̬�ε�֪ʶ��ǰ���[Ember.js ����ָ��֮ʮ��{{link-to}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-san-link-to/)��[Ember.js ����ָ��֮��ʮ·�ɶ���](http://blog.ddlisting.com/2016/03/25/ember-js-ru-men-zhi-nan-zhi-er-shi-lu-you-ding-yi/)�Ѿ��������ܡ�

һ����·���ж����˶�̬��Ember�ͻ��URL����ȡ��̬�ε�ֵ��Ϊ`model`�ص��ĵ�һ��������
```javascript
//  app/router.js
// ����

Router.map(function() {
    this.route('posts', function() {
        this.route('post', { path: '/:post_id'});
    }); 
});

export default Router;
```
��δ��붨����һ����̬��`:post_id`���ǵö�̬������`:`����ͷ��Ȼ����`model`�ص���ʹ�ö�̬�λ�ȡ���ݡ�
```javascript
//  app/routes/posts.js

import Ember from 'ember';
export default Ember.Route.extend({
	model: function(params) {
		return this.store.findRecord('post', params.post_id);
	}
});
```
���Կ�����`model`�ص���Ҳ��ʹ����·���ж���Ķ�̬�Σ����������̬����Ϊ�������ݸ�Ember�ķ���`findRecord`��Ember���URL��Ӧλ���ϵ����ݽ����������̬���ϡ�

**ע��**����`model`�еĶ�̬��ֻ��ͨ��URL���ʵ�ʱ��Żᱻ�������������ͨ��������ʽ������ʹ��`link-to`����·�ɣ�ת��·�ɵģ���ô·����`model`�ص�������Ķ�̬���ᱻ����������������ݻ�ֱ�Ӵ��������л�ȡ������԰������������ember�Ļ��棩������Ĵ��뽫Ϊ����ʾ���˵����

#### 1�����ȴ���һ��model��ember g model post

```javascript
import DS from 'ember-data';

export default DS.Model.extend({
	title: DS.attr('string'),
	body: DS.attr('string'),
	timestamp: DS.attr('number')
});
```
������3�����ԣ�`id`���Բ���Ҫ��ʾ���壬ember��Ĭ�ϼ��ϡ�

#### 2����posts������һ����·��

```javascript
Router.map(function() {
    this.route('posts', function() {
        this.route('post', { path: '/:post_id'});
    }); 
});
```
Ȼ����[Ember CLI](http://ember-cli.com/user-guide)���`ember g route posts/post`���ڴ���·��`post`��ͬʱҲ���Զ���������ģ��`post.hbs`���������֮���õ����������ļ���
```
1.app/routes/posts/post.js
2.app/templates/posts/post.hbs
```
�޸�·��`posts.js`����`model`�ص��з����趨�����ݡ�
```javascript
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function(params) {
		return [
		    {
		    	"id":"-JzySrmbivaSSFG6WwOk",
		        "body" : "testsssss",
		        "timestamp" : 1443083287846,
		        "title" : "test"
		    },
		    {
		    	"id":"-JzyT-VLEWdF6zY3CefO",
		        "body" : "33333333",
		        "timestamp" : 1443083323541,
		        "title" : "test33333"
		    },
		    {
		    	"id":"-JzyUqbJcT0ct14OizMo" ,
		        "body" : "body.....",
		        "timestamp" : 1443083808036,
		        "title" : "title1231232132"
		    }
		];
	}
});
```
�޸�`posts.hbs`��������ʾ���е����ݡ�
```html
<ul>
	{{#each model as |item|}}
		<li>
			{{#link-to 'posts.post' item}}{{item.title}}{{/link-to}}
		</li>	
	{{/each}}
</ul>

<hr>
{{outlet}}
```
�޸���·��`post.js`��ʹ����·�ɸ��ݶ�̬�η���ƥ������ݡ�
```javascript
// app/routes/posts/post.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function(params) {
		console.log('params = ' + params.post_id);
		return this.store.findRecord('post', params.post_id);
	}
});
```
ע���ӡ��Ϣ���`console.log()`;��Ȼ������޸���ģ��`post.hbs`��
```html
<!-- app/templates/posts/post.hbs -->

<h2>{{model.title}}</h2>
<p>{{model.body}}</p>
```
���ˣ�ȫ������Ĳ������ݺʹ����Ѿ���д��ϡ�����ִ��[http://localhost:4200/posts](http://localhost:4200/posts)�����Կ�����������ʾ��������·��posts��model�ص������õĲ������ݡ��鿴ҳ���HTML���룺

![html](/content/images/2016/03/60.png)

���Կ���ÿ�����ӵĶ�̬�ζ��������������ݵ�id����ֵ��
ע�⣺���������һ����ע�⿴���������̨��ӡ����Ϣ��
�ҵ�����Ե�һ�����ӣ��������URL��Ϊ

![html](/content/images/2016/03/61.png)

��������Ŀ���̨�ǲ��ǲ�û�д�ӡ��`params = -JzySrmbivaSSFG6WwOk`���ڵ�����������ӽ��Ҳ��һ���ģ����������̨û�д�ӡ���κ���Ϣ��

����������ֱ�����������ַ�������룺[http://localhost:4200/posts/-JzyUqbJcT0ct14OizMo](http://localhost:4200/posts/-JzyUqbJcT0ct14OizMo)Ȼ��enterִ�У�ע�⿴���������̨��ӡ����Ϣ��������ʱ��ӡ��`params = -JzyUqbJcT0ct14OizMo`���������ͬ���ķ�ʽִ�������������ӵĵ�ַ��ͬ��Ҳ���ӡ��`params = xxx`��`xxx`Ϊ���ݵ�`id`ֵ����

�����������Ӧ���ܺܺõĽ�����Ember��ʾ�û���Ҫ��ע������⡣
ֻ��ֱ���ù���������ʲŻ�ִ�а����˶�̬�ε�`model`�ص������򲻻�ִ�а����ж�̬�εĻص������û�а�����̬�ε�`model`�ص�������ͨ��URL���ʻ���ͨ��`link-to`���ʶ���ִ�С��������·��`posts`��`model`�ص������һ���ӡ��־�Ĵ��룬Ȼ��ͨ�������ҳ�ϵ�`about`��`posts`�л�·�ɣ�����Կ�������̨��ӡ��������`model`�ص�����ӵ���־��Ϣ��


### 3����ģ��

������һ��`mode`l�ص���ͬʱ���ض��ģ�͵����Ҳ��ʱ�����ڵġ����������������Ҫ��`model`�ص����޸ķ���ֵΪ`Ember.RSVP.hash`�������͡���������Ĵ������ͬʱ����������ģ�͵����ݣ�һ����`song`��һ����`album`��

```javascript
//  app/routes/favorites.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return Ember.REVP.hash({
			songs: this.store.find('song'),
			albums: this.store.find('slbum')
		});
	}
});
```
Ȼ����ģ��`favorites.hbs`�оͿ���ʹ��`{{#each}}`���������ݼ����������������ķ�ʽ����ͨ�ı�����ʽһ����
```html
<!--  app/templates/favorites.hbs -->

<h2>Song list</h2>
<ul>
{{#each model.songs as |item|}}
	<li>{{item.name}}</li>
{{/each}}
</ul>
<hr>
<h2>Album list</h2>
<ul>
{{#each model.albums as |item|}}
	<li>{{item.name}}</li>
{{/each}}
</ul>
```
��������·�ɵ�`model`�ص������������ϣ�`model`�ص���ʵ���ǰ�ģ�Ͱ󶨵�·���ϡ�ʵ�����ݵĳ�ʼ����Ȼ���������Ⱦ��ģ������ʾ����Ҳ��Ember�Ƽ���ô���ġ������ǰѲ���������صĴ������`route`�����Ƿ���`controller`��
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
