ǰһƪ�����˲�ѯ��������ƪ�����½������¡�ɾ����¼�ķ�����
��ƪ��ʾ�����봴������һƪ�Ļ����ϡ���������[firebase](http://www.firebase.com)������`route`��`template`��ο���һƪ������һ��controller��`ember g controller articles`��

## 1���½���¼

�����µļ�¼ʹ��`createRecord()`��������������Ĵ����½���һ��`aritcle`��¼���޸�ģ�壬��ģ�������Ӽ���`input`�������������`article`��Ϣ��
```html
<!--  app/templates/articles.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-4 col-xs-4">
			<ul class="list-group">
			{{#each model as |item|}}
				<li class="list-group-item">
					<!--����·�ɣ�·�ɵĲ㼶��router.js�ﶨ���Ҫһ�� -->
                 	{{#link-to 'articles.article' item.id}}
						{{item.title}} -- <small>{{item.category}}</small>
					{{/link-to}}
				</li>
			{{/each}}
			</ul>


			<div>
				title��{{input value=title}}<br>
				body�� {{textarea value=body cols="80" rows="3"}}<br>
				category: {{input value=category}}<br>
				<button {{ action "saveItem"}}>����</button>
				<font color='red'>{{tipInfo}}</font>
			</div>
		</div>

		<div class="col-md-8 col-xs-8">
		{{outlet}}
		</div>
	</div>
</div>
```
ҳ����ֶηֱ��Ӧ��ģ��`article`�����ԡ���������桱���ύ��`controller`���������ǻ�ȡ���ݱ������ݵ�`controller`��
```js
//   app/controllers/articles.js

import Ember from 'ember';

export default Ember.Controller.extend({

	actions: {

		//  ���ύ���������ݵ�Store��Store���Զ����µ�firebase
		saveItem: function() {
			var title = this.get('title');
			if ('undefined' === typeof(title) || '' === title.trim()) {
				this.set('tipInfo', "title����Ϊ��");
				return ;
			}

			var body = this.get('body');
			if ('undefined' === typeof(body) || '' === body.trim()) {
				this.set('tipInfo', "body����Ϊ��");
				return ;
			}
			var category = this.get('category');
			if ('undefined' === typeof(category) || '' === category.trim()) {
				this.set('tipInfo', "category����Ϊ��");
				return ;
			}

			//  �������ݼ�¼
			var article = this.store.createRecord('article', {
				title: title,
				body: body,
				category: category,
				timestamp: new Date().getTime()
			});
			article.save();  //�������ݵĵ�Store
			//  ���ҳ���input�����
			this.set('title', "");
			this.set('body', "");
			this.set('category', "");
		}
	}
});
```
��Ҫ��`createRecord`��������һ��������ģ�����ơ��ڶ��������Ǹ���ϣ���ڹ�ϣ������ģ������ֵ��������`article.save()`���������ݱ��浽`Store`������`Store`���浽firebase������Ч������ͼ��

![�����ͼ](/content/images/2016/04/170.png)

������Ϣ����������桱���������̻���ʾ���б�no form -- java��֮��Ȼ������Ե�������ѯ��ϸ��Ϣ��body����Ϣ����ҳ������ʾ��

ͨ������ʵ��������Ӧ�ö���ȥʹ��`createRecord()`�����ˣ��������������ģ�����й�����ϵ����ķ���������ô�����أ�����������һ��ģ�͡�
```
ember g model users
```
Ȼ����ģ�������ӹ�����
```js
//   app/models/article.js

import DS from 'ember-data';

export default DS.Model.extend({
	title: DS.attr('string'),
	body: DS.attr('string'),
	timestamp: DS.attr('number'),
	category: DS.attr('string'),
	author: DS.belongsTo('user')  //����user
});


//  app/models/user.js
import DS from 'ember-data';

export default DS.Model.extend({
  	username: DS.attr('string'),
  	timestamp: DS.attr('number'),
  	articles: DS.hasMany('article')  //����article
});
```
�޸�ģ��`articles.hbs`�ڽ���������¼��������Ϣ�ֶΡ�
```html
����ʡ����������
<div>
	title��{{input value=title}}<br>
	body�� {{textarea value=body cols="80" rows="3"}}<br>
	category: {{input value=category}}<br>
	<br>
	author: {{input value=username}}<br>
	<button {{ action "saveItem"}}>����</button>
	<font color='red'>{{tipInfo}}</font>
</div>
����ʡ����������
```
���濴����ô��`controller`������������ģ�͵Ĺ�����ϵ��һ�������ַ�ʽ���ã�һ����ֱ����`createRecord()`���������ã���һ�����ڷ��������á�
```js
//   app/controllers/articles.js

import Ember from 'ember';

export default Ember.Controller.extend({

	actions: {

		//  ���ύ���������ݵ�Store��Store���Զ����µ�firebase
		saveItem: function() {
			//  ��ȡ��Ϣ��У�����ʡ�ԡ���

			// ����user
			var user = this.store.createRecord('user', {
				username: username,
				timestamp: new Date().getTime()
			});
			//  ����Ҫִ�������룬����user���ݲ��ܱ��浽Store��
			//  ����articleͨ��user��id���Ҳ���user
			user.save();

			//  ����article
			var article = this.store.createRecord('article', {
				title: title,
				body: body,
				category: category,
				timestamp: new Date().getTime(),
				author: user   //���ù���
			});

			article.save();  //�������ݵĵ�Store
			//  ���ҳ���input�����
			this.set('title', "");
			this.set('body', "");
			this.set('category', "");
			this.set('username', "");
		}
	}
});
```

![�����ͼ](/content/images/2016/04/171.png)

����������ʾ��Ϣ����������桱������firebase�ĺ�̨�������µ����ݹ�����ϵ��

![firebase���ݽ�ͼ](/content/images/2016/04/172.png)

ע��㣺�����������ݵĹ�����ͨ�����ݵ�`id`ά���ġ�
��ô�����Ҫͨ��`article`��ȡ`user`����ϢҪ��ô��ȡ�أ�

ֱ�����������ķ�ʽ��ȡ�ȿɡ�
```html
{{#each model as |item|}}
	<li class="list-group-item">
		<!--����·�ɣ�·�ɵĲ㼶��router.js�ﶨ���Ҫһ�� -->
     	{{#link-to 'articles.article' item.id}}
			{{item.title}} -- <small>{{item.category}}</small> -- <small>{{item.author.username}}</small>
		{{/link-to}}
	</li>
{{/each}}
```
ע�⿴����`{{ item.author.username }}`������EL���ʽ�ɣ���
ǰ���ᵽ����������ʽ��������ģ�͵Ĺ�����ϵ������Ĵ����ǵڶ��ַ�ʽ��
```js
//  ��������ʡ�ԡ���
//  ����article
var article = this.store.createRecord('article', {
	title: title,
	body: body,
	category: category,
	timestamp: new Date().getTime()
	// ,
	// author: user   //���ù���
});

// �ڶ������ù�����ϵ���������ⲿ�ֶ�����set��������
article.set('author', user);
//  ��������ʡ�ԡ���
```
���У�����¼����Ϣ���õ��Ľ����һ�µġ����������ֱ����`createRecord`��������÷�������������ģ�͵Ĺ�ϵ����������Ĵ���Σ�
```js
var store = this.store;  // �������������⣬��createRecord�����ڲ�����ʹ��this.store
var article = this.store.createRecord('article', {
	title: title,
	// ����
	// ,
	// author: store.findRecord('user', 1)   //���ù���
});

// �ڶ������ù�����ϵ���������ⲿ�ֶ�����set��������
article.set('author', store.findRecord('user', 1));
```
���ַ�ʽ����ֱ�Ӷ�̬����user��id����ֵ��ȡ����¼�������ù�����ϵ�������������ˣ����Ž��ܼ�¼�ĸ��¡�

##2�����¼�¼

���������������˵�ǳ����ơ��뿴����Ĵ���Σ�
������ģ�������Ӹ��µ����ô��룬�޸���ģ��`articles/article.hbs`��
```html
<!--  app/templates/articles/article.hbs  -->

<h1>{{model.title}}</h1>
<div class = "body">
{{model.body}}
</div>

<div>
<br><hr>
���²���<br>
title: {{input value=model.title}}<br>
body��<br> {{textarea value=model.body cols="80" rows="3"}}<br>
<button {{action 'updateArticleById' model.id}}>����������Ϣ</button>
</div>
```
����һ��`controller`���û�������ģ���ύ���޸���Ϣ��
```
ember g controller articles/article
```
```js
//  app/controllers/articles/article.js

import Ember from 'ember';

export default Ember.Controller.extend({
	actions: {
		// ��������id����
		updateArticleById: function(params) {
			var title = this.get('model.title');
			var body = this.get('model.body');
			this.store.findRecord('article', params).then(function(art) {
				art.set('title', title);
				art.set('body', body);

				//  ������µ�ֵ��Store
				art.save();
			});
		}
	}
});
```
�����ѡ����Ҫ���µ����ݣ�Ȼ�����Ҳ���������޸���Ҫ���µ����ݣ����޸Ĺ����п��Կ������޸ĵ���Ϣ��������Ӧ�������ϣ��������ΪEmber�Զ�����Store�е����ݣ����ǵúܾ�ǰ�����Ĺ۲��ߣ�observer���𣿣���

![�����ͼ](/content/images/2016/04/173-1.png)

�����û�е��������������Ϣ���ύ�����޸ĵ���Ϣ������µ�firebase��ҳ��ˢ�º���ԭ�����ӣ���������ˡ�����������Ϣ�����ݽ���Ѹ��µ���Ϣ�ύ��firebase��

����`save`��`findRecord`��������ֵ��һ��`promises`���������㻹������Գ���������д�����������Ĵ��룺
```js
var user = this.store.createRecord('user', {
	//  ����
});
user.save().then(function(fulfill) {
	//  ����ɹ�
}).catch(function(error) {
	//  ����ʧ��
});

this.store.findRecord('article', params).then(function(art) {
	//  ����
}).catch(function(error) {
	//  ���������
});
```
��������ҾͲ���ʾ�ˣ�������Լ���д���԰ɣ���

##3��ɾ����¼

��Ȼ����������ôͨ���ͻ���ɾ������¼��ɾ�����޸ķǳ����ƣ�Ҳ�����Ȳ�ѯ��Ҫɾ�������ݣ�Ȼ��ִ��ɾ����
```js
//   app/controllers/articles.js

import Ember from 'ember';

export default Ember.Controller.extend({

	actions: {

		//  ���ύ���������ݵ�Store��Store���Զ����µ�firebase
		saveItem: function() {
			// ʡ��
		},
		//  ����id����ֵɾ������
		delById : function(params) {

	    	//  �����ȡһ����Ϊ�жϱ�����ֵ
	        if (params && confirm("��ȷ��Ҫɾ������������?")) {
	            //  ִ��ɾ��
	            this.store.findRecord('article', params).then(function(art) {
	            	art.destroyRecord();
	            	alert('ɾ���ɹ���');
	            }, function(error) {
	            	alert('ɾ��ʧ�ܣ�');
	            });
	        } else {
	            return;
	        }

		}
	}
});
```
�޸���ʾ���ݵ�ģ�壬����ɾ����ť�����������ݵ�`id`ֵ��`controller`��
```html
<!--  app/templates/articles.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-4 col-xs-4">
			<ul class="list-group">
			{{#each model as |item|}}
				<li class="list-group-item">
					<!--����·�ɣ�·�ɵĲ㼶��router.js�ﶨ���Ҫһ�� -->
                 	{{#link-to 'articles.article' item.id}}
						{{item.title}} -- <small>{{item.category}}</small> -- <small>{{item.author.username}}</small>
					{{/link-to}}
					<button {{action 'delById' item.id}}>ɾ��</button>
				</li>
			{{/each}}
			</ul>
        // ����ʡ����������
	</div>
</div>
```

![��ͼ](/content/images/2016/04/174.png)

�������ͼ������ڶ�������ɾ����ť��������ʾ���ڣ������ȷ����֮��ɹ�ɾ�����ݣ���������ɾ���ɹ���������firebase��̨�鿴���ݣ�ȷʵ�Ѿ�ɾ���ɹ���
Ȼ����˹�����userȴû��ɾ�������������ҲӦ���ǲ�ɾ��������user���ݵġ�
���ս��ֻʣ��һ�����ݣ�

![��ͼ](/content/images/2016/04/175.png)

���ˣ��й����������¡�ɾ���ķ���������ϡ��Ѿ���������ϸ����ʾʵ���������ţ������Ҳ�������Լ�����Ŀ��ʵ��������ô�����⼸�������Ǻ����׵ģ�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
