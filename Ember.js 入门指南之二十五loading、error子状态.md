��ǰ���[Ember.js ����ָ��֮��ʮ·�ɶ���](http://blog.ddlisting.com/2016/03/25/ember-js-ru-men-zhi-nan-zhi-er-shi-lu-you-ding-yi/)���`loading`��`error`��·�ɣ�������[Ember](http://emberjs.com/)Ĭ�ϴ����ģ�����`beforeModel`��`model`��`afterModel`�������ص�ִ�����֮ǰ������Ⱦ��ǰ·�ɵ�`loading`��`error`ģ�塣
```js
Router.map(function() {
  this.route('posts', function() {
      this.route('post', { path: '/:post_id'});
  });
});
```
����������·������[Ember](http://emberjs.com/)���������µ�·���б�

![·��ӳ��ͼ](/content/images/2016/03/64.png)

ÿ��·�ɶ����Զ�����һ��`loading`��`error`·�ɣ������ҽ�һһ��ʾ������·�ɵ����á�
ͼƬǰ��`loading`��`error`·�ɶ�Ӧ��`application`·�ɡ�`posts_loading`��`posts_error`��Ӧ����`posts`·�ɡ�
	
### 1��loading��״̬

[Ember](http://emberjs.com/)�������ݷ���`beforeModel`��`model`��`afterModel`�ص��л�ȡ�����ݵ�ģ����ʾ������ֻҪ�Ǽ������ݾ���Ҫʱ�䣬����[Ember](http://emberjs.com/)Ӧ����˵����`model`�Ȼص��м��������ݲŻ���Ⱦģ�壬����������ݱȽ�����ô�û�������ҳ�����һ���հ׵�ҳ�棬�û�����ܲ

[Ember](http://emberjs.com/)�ṩ�Ľ���취�ǣ���`beforeModel`��`model`��`afterModel`�ص���û����ǰ�Ƚ���һ����`loading`����״̬��Ȼ����Ⱦһ����`routeName-loading`��ģ�壨�����`application`·�����Ӧ��ֱ����`loading`��`error`����Ҫǰ׺����

Ϊ����ʾ��Ч����`app/templates`�´���һ��`posts-loading`ģ�塣�����������������Ⱦģ��`posts`֮ǰ������Ⱦ���ģ�塣
```html
<!-- app/templates/posts-loading.hbs -->

<img src="assets/images/loading/loading.gif" />
```
Ȼ���޸�·��`posts.js`����`model`�ص�ִ��ʱ�����һЩ��
```js
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function() {
		//  ģ��һ����ʱ������
		for (var i = 0; i < 10000000;i++) {

		}
		return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
	}
});
```
ִ��[http://localhost:4200/posts](http://localhost:4200/posts)�����Ȼῴ��ִ�е�`loading`ģ������ݣ�Ȼ��ſ�������Ҫ��ʾ�����ݡ���һ�����ع��̣�������2��ͼƬ��ʾ��

![ͼ1](/content/images/2016/03/65.png)

![ͼ2](/content/images/2016/03/67.png)

### 2��loading�¼�

��`beforeModel`��`model`��`afterModel`�ص�û����������֮ǰ������ִ��һ����Ϊloading���¼���
```js
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function() {
		//  ģ��һ����ʱ������
		for (var i = 0; i < 10000000;i++) {

		}
		return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
	},
	actions: {
		loading: function(transition, originRoute) {
			alert("Sorry this is taking so long to load!!");
		}
	}
});
```
ҳ��ˢ�º�ᵯ��һ����ʾ���Ȳ������ȷ��������������ġ������� -> �����߹��ߡ����л���Network��ǩ�¡��ҵ���pulls��������󣬵������

![result](/content/images/2016/03/69.png)

��ͼ�п��Կ�����ʱ`model`�ص���û�з��ء���ʱ��Ӧ�������ǿյģ�˵��`loading`�¼�ʵ��`model`�ص�����֮ǰִ���ˡ�

Ȼ����������ġ�ȷ��������ʱ���Կ���Response�������ˡ�˵��`model`�ص��Ѿ�ִ����ϡ�
ע�⣺�����ǰ��·��û����ʾ����`loading`�¼������ʱ���ð�ݵ���·�ɣ������·��Ҳû����ʾ����`loading`�¼�����ô���������ð�ݣ�һֱ����˵�·��`application`��

### 3��error��״̬

��`loading`��״̬���ƣ�`error`��״̬����`beforeModel`��`model`��`afterModel`�ص�ִ�й����г��ִ����ʱ�򴥷���

������ʽ��`loading`��״̬Ҳ�����Ƶġ����ڶ���һ����Ϊ`posts-error.hbs`��ģ�塣
```html
<!--  app/templates/posts-error.hbs -->

<p style="color: red;">
posts�ص���������������
</p>
```
Ȼ����`model`�ص����ֶ����һ��������롣
```js
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function() {
		//  ģ��һ����ʱ������
		for (var i = 0; i < 10000000;i++) {

		}
		var e = parseInt(value);
		return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
	}
});
```
ע��`var e = parseInt(value);`�����룬����`value`û�ж�������Ӧ�ûᱨ����ô��ʱҳ�����ʾʲô�أ���

![result](/content/images/2016/03/70.png)

��������ʾ����û������������ô��Ҳ��õ���ͼ�Ľ�����������û�ж������ģ�壬��ô�����Ͻ���ʲô������ʾ��

���������`xxx-error.hbs`ģ���Ͽ�����ʲô������Ϣ���������ģ���ϴ�ӡ`model`��ֵ�����£�
```html
<!--  app/templates/posts-error.hbs -->

<p style="color: red;">
posts�ص���������������
<br>
{{model}}
</p>
```
��ʱҳ�����ʾ����Ĵ�����ʲô����

![result](/content/images/2016/03/71.png)

������������������̨��ӡ�Ĵ�����Ϣ�򵥺ܶ࣡����

### 4��error�¼�

`error`�¼����һ�㽲��loading�¼�Ҳ�����Ƶġ�ʹ�÷�ʽ��`loading`һ�������˾�������¼��ǳ����ã����ǿ���������¼��и���`error`״̬��Ĳ�ִͬ�в�ͬ���߼���������ת����ͬ��·���ϡ�
```js
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function() {
		return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls____');
	},
	
	actions: {
		error: function(error, transition) {
			console.log('error = ' + error.status);
			//  ��ӡerror��������������Ժͷ�����
			for(var name in error){         
	           console.log(name); 
	           // console.log('����ֵ���߷�����==��' + error[name]);
	        }    
	        alert(names); 
			if (error && error.status === 400) {
				return this.transitionTo("about");
			} else if (error.status === 404) {
				return this.transitionTo("form");
			} else {
				console.log('else......');
			}
		}
	}
});
```
ע��`getJSON`�������URL������URL�����������һЩ�ַ���Ŀ���������URL�����ڡ���ʱ����Ӧ�û��Ҳ��������ַ`error`����Ӧ��Ӧ����404��Ȼ��ֱ����ת��`form`���·���ϡ�
����[http://localhost:4200/posts](http://localhost:4200/posts)֮�����������̨��ӡ��Ϣ���£�

![result](/content/images/2016/03/72.png)

ҳ��Ҳ����ת��`form`��

![result](/content/images/2016/03/73.png)

����·�ɼ������ݹ������漰������״̬`loading`��`error`������ȫ�������꣬������״̬���Ż��û����鷽���Ƿǳ����õģ�ϣ����ѧϰ[Ember](http://emberjs.com/)��ͬѧ�ú����գ�����=^=

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
