### 1��link-to���ֳ���ʹ��
`link-to`���ֱ��ʽ��Ⱦ֮�����һ��`a`��ǩ����`a`��ǩ��`href`���Ե�ֵ�Ǹ���·�����ɵģ���·�ɵ�������ϢϢ��صġ�����ÿ�����õ�·�����ƶ������Ŷ�Ӧ�Ĺ�ϵ�ġ�
Ϊ����ʾЧ����������������һ��`route`�������ֶ������ļ�������ȡ�������ݡ����Ľ��·�����ã���㴮����һЩ·�ɷ����֪ʶ��������ܿ�������ˣ�������Ҳ��Ҫ���������һ���½���·�ɡ�
#### 1, ������·��
```javascript
//  app/routers.js

import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType	
});

Router.map(function() {
  this.route('posts', function() {
  	this.route('detail', {path: '/:post_id'});  //ָ����·�ɣ�:post_id���Զ�ת��Ϊ���ݵ�id
  });
});

export default Router;
```
���������룬��`posts`������һ����·��`detail`������ָ��·����Ϊ`/:post_id`��`:post_id`��һ����̬�ֶΣ�һ�������Ĭ��Ϊ`model`��`id`���ԡ�����ģ����Ⱦ֮���õ�������`posts/1`��`posts/2`������ʽ��·�ɡ�

#### 2, ��route��ʼ������
```javascript
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
	}
});
```
ʹ��Ember�ṩ�ķ���ֱ�Ӵ�Զ�̻�ȡ�������ݡ��������ݵĸ�ʽ�����������ֱ�Ӵ������URL�Ϳ��Կ�����

#### 3�������ʾ��ģ��
```html
<!--  //  app/templates/posts.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-10 col-xs-10">
			<div style="margin-top: 70px;">
				<ul class="list-group">
				{{#each model as |item|}}
					<li class="list-group-item">
						<!--����·�ɣ�·�ɵĲ㼶��router.js�ﶨ���Ҫһ�� -->
                     {{#link-to 'posts.detail' item}}
							{{item.title}}
						{{/link-to}}
					</li>
				{{/each}}
				</ul>
			</div>
		</div>
	</div>
</div>
```
ֱ����`{{#each}}`���������е����ݣ�����ʾ�ڽ����ϣ��������ݱȽ϶������ʾ�ıȽ������ر���ҳ��ˢ��֮�󿴵�һƬ�հף��벻Ҫ����ˢ��ҳ�棬�ȴ�һ�¼��ɡ�������ͼ�ǽ����һ���֣�

![�����ͼ](/content/images/2016/03/24.png)

���ǲ鿴ҳ���Դ���룬���Կ���`link-to`������Ⱦ֮���HTML���룬�Զ�������URL����`router.js`�����õ�`post_id`��Ⱦ֮�󶼱�`model`��`id`����ֵ�����ˡ�

![run result](/content/images/2016/03/25.png)

�����û�в������ݣ��㻹��ֱ�Ӱ�`link-to`���ֵ�`post_id`д��������ֱ�Ӱ����ݵ�`id`ֵ���õ�`link-to`�����ϡ���ģ���ļ���`ul`��ǩ��һ���������´��룬��`link-to`������ָ��`id`Ϊ`1`��
```html
<!-- ����һ��ֱ��ָ��id������ -->
  <li class="list-group-item">
    {{#link-to 'posts.detail' 1}}����һ��ֱ��ָ��id������{{/link-to}}
  </li>
```
��Ⱦ֮���HTML��������:
```html
<li class="list-group-item">
<a id="ember404" href="/posts/1" class="ember-view">����һ��ֱ��ָ��id������
</a>
</li>
```
���Կ�����ǰ��ʹ�ö�̬������Ⱦ֮���`href`�ĸ�ʽ��һ���ġ������������ĳ��`a`��ǩ�Ǽ���״̬�������ֱ���ڱ�ǩ������һ��CSS�ࣨ`class=��active��`����

### 2��link-to�������ö����̬�ֶ�
�����У�·�ɵ�·����������2��ģ�`post/1`��Ҳ�п����Ƕ��εģ�`post/1/comment`��`post/1/2`����`post/1/comment/2`�ȵ���ʽ�����������������ʽ��URL��`link-to`��������Ҫ��ôȥ�����أ�
�����ӣ�����ʾģ��֮ǰ������Ҫ�ȹ����ò��������Լ��޸Ķ�Ӧ��·�����ã���ʱ��·�������Ƕ��ģ���Ϊ`link-to`������Ⱦ֮��õ���href����ֵ���Ǹ���·�����ɵģ������������Ҫ�ǵá���

#### 1. һ��·�����и�����·��
```javascript
//  app/routers.js

import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType	
});

Router.map(function() {
  // this.route('handlebarsConditionsExpRoute');
  // this.route('handlebars-each');
  // this.route('store-categories');
  // this.route('binding-element-attributes');

  //  link-toʵ����������
  // this.route('link-to-helper-example', function() {
  //  this.route('edit', {path: '/:link-to-helper-example_id'});
  // });

  this.route('posts', function() {
      //ָ����·�ɣ�:post_id���Զ�ת��Ϊ���ݵ�id
  	this.route('detail', {path: '/:post_id'}, function() {
      //����һ��comments·��
      this.route('comments');
      // �ڶ�����·��comment������·���Ǹ���̬�ֶ�comment_id
      this.route('comment', {path: '/:comment_id'});
    });
  });
  
});

export default Router;
```

������������ã���Ⱦ֮��õ���·�ɸ�ʽ`posts/detail/comments`�����ڻ�ȡԶ�����ݱȽ���ֱ��ע�͵�`posts.js`���`model`�ص���������ֱ��ʹ��д��id�ķ�ʽ��
ע�⣺���������У���·��`detail`����2����·�ɣ�һ����`comments`��һ����`comment`�����������һ����̬�Ρ��ɴ�ģ����Ⱦ֮��Ӧ������2����ʽ��URL��һ����`posts.detail.comments`��`posts/1/comments`������һ����`posts.detail.comment`��`posts/1/2`�����������������`route`Ƕ�ײ���ٶ�Ӧ��Ҳ�ܿ������ˣ�
```html
<!--  //  app/templates/posts.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-10 col-xs-10">
			<div style="margin-top: 70px;">
				<ul class="list-group">
					<!-- ����һ��ֱ��ָ��id������ -->
					<li class="list-group-item">
						<!��- ע���ʱֻ��һ����̬�Σ�����ֻ��һ������1��Ember�����˳���Զ�ƥ�䵽��̬�ε�λ���ϡ� -->
						{{#link-to 'posts.detail.comments' 1 class='active'}}
						posts.detail.comments��posts/1/comments����ʽ
						{{/link-to}}
					</li>


					<li class="list-group-item">
						<!��-
						ע���ʱ��2����̬�Σ�������2������1��2��Ember�����˳���Զ�ƥ�䵽��̬�ε�λ���ϡ�
						��һ������1��ƥ�䵽��һ����̬��post_id�ϣ��ڶ�������2��ƥ�䵽��̬��comment_id��
						 -->
						{{#link-to 'posts.detail.comment' 1 2 class='active'}}
						posts.detail.comment��posts/1/2����ʽ
						{{/link-to}}
					</li>

				</ul>
			</div>
		</div>
	</div>
</div>
```
��Ⱦ֮��Ľ�����£�

![run result](/content/images/2016/03/26.png)

����Ƕ�̬�ε�һ�㶼��`model`��`id`���棬������Ƕ�̬�ε�ֱ����ʾ���õ�·�����ơ�

#### 2, ���·��Ƕ��

������ʾ�˶����·�ɵ������������Ž���һ��·���ж����Σ��������и������̬�κͷǶ�̬����ɵ������
�����޸�·�����ã���`comments`����Ϊ`detail`����·�ɡ�������`comments`��������һ����̬�ε���·��`comment_id`��
```javascript
//  app/routers.js

import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType	
});

Router.map(function() {
  this.route('posts', function() {
      //ָ����·�ɣ�:post_id���Զ�ת��Ϊ���ݵ�id
    this.route('detail', {path: '/:post_id'}, function() {
      //����һ��comments·��
      this.route('comments', function() {
        // ��comments����������һ����·��comment������·���Ǹ���̬�ֶ�comment_id
        this.route('comment', {path: '/:comment_id'});
      });   
    });
  });
});
export default Router;
```
ģ��ʹ��·�ɵķ�ʽ`posts.detail.comments.comment`���������Ӧ����������`posts/1/comments/2`���ָ�ʽ��URL��
```html
<!--  //  app/templates/posts.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-10 col-xs-10">
			<div style="margin-top: 70px;">
				<ul class="list-group">

					<li class="list-group-item">
						<!--
							һ��������4��·��
						 -->
						{{#link-to 'posts.detail.comments.comment' 1 2 class='active'}}
						posts.detail.comments.comment��posts/1/comments/2����ʽ
						{{/link-to}}
					</li>

				</ul>
			</div>
		</div>
	</div>
</div>
```
��Ⱦ֮��õ���HTML���£�
```html
<ul class="list-group">
  <li class="list-group-item">
  <!-- һ��������4��·�� -->
    <a id="ember473" href="/posts/1/comments/2" class="active ember-view">						posts.detail.comments.comment��posts/1/comments/2����ʽ
    </a>
  </li> 
</ul>
```
�����������Ԥ��������4��·�ɣ�`/posts/1/comment/2`����
�������ݡ�
���������ڶ�����·��Ƕ�׵�����㻹����ʹ������ķ�ʽ����·�ɺ�ģ�壬���ҿ���ͬʱ������`/posts/1/comments`��`/posts/1/comments/2`��
```javascript
  this.route('posts', function() {
      //ָ����·�ɣ�:post_id���Զ�ת��Ϊ���ݵ�id
      this.route('detail', {path: '/:post_id'}, function() {
          //����һ��comments·��
          this.route('comments');
          // ·�ɵ��ã�posts.detail.comment
          // ע��������ǰ������÷�ʽ��detai��Ⱦ֮��ᱻ/:post_id�滻��comment��Ⱦ֮��ֱ�ӱ�comments/:comment_id�滻�ˣ�
          //��õ���posts/1/comments/2������ʽ��URL
          this.route('comment', {path: 'comments/:comment_id'});
    });
  });
```
```html
<!--  //  app/templates/posts.hbs  -->

<div class="container">
	<div class="row">
		<div class="col-md-10 col-xs-10">
			<div style="margin-top: 70px;">
				<ul class="list-group">

					<li class="list-group-item">
						<-- ���õķ�ʽ���� -->
                    {{#link-to 'posts.detail.comments' 1 class='active'}}
						posts.detail.comments��/posts/1/comments����ʽ
						{{/link-to}}
					</li>

					<li class="list-group-item">
						<!--
							һ��������4��·�ɣ���ǰ������÷�ʽһ��
						 -->
						{{#link-to 'posts.detail.comment' 1 2 class='active'}}
						posts.detail.comments.comment��posts/1/comments/2����ʽ
						{{/link-to}}
					</li>


				</ul>
			</div>
		</div>
	</div>
</div>
```

��Ⱦ֮��Ľ�����£�

![��Ⱦ֮��Ľ��](/content/images/2016/03/27.png)

���ַ�ʽ�����·����Ⱦ�Ľ����һ���ģ�������ϲ���ˣ����巽ʽҲ�Ƿǳ����ġ���һ�ֶ��巽ʽ���űȽ��������������֪����һ���ġ�������Ҫд������롣�ڶ��ֶ��巽ʽ���Ӽ�࣬����������Ƕ�׵Ĳ�Ρ�
	��������route������������������Ҳ��Ҫ�����������һ�����ǽ���·�ɵģ�Ȼ�����ܽ��link-to���������·�����ö��ں���route�½ڵ�ѧϰ�Ƿǳ��а����ġ�

#### 3, ��link-to���������Ӷ�������

`handlebars`������ֱ����`link-to`�������Ӷ�������ԣ�����ģ����Ⱦ֮��`a`��ǩ���������ӵĶ��������ˡ�
���������Ϊ`a`��ǩ����CSS��`class`��

```html
{{link-to "show text info" 'posts.detail' 1 class="btn btn-primary"}}

{{#link-to "posts.detail" 1 class="btn btn-primary"}}show text info{{/link-to}}
```
��������д�����ǿ��Եģ���Ⱦ�Ľ��Ҳ��һ���ġ���Ⱦ֮���HTMLΪ��
```html
<a id="ember434" href="/posts/1" class="btn btn-primary ember-view">show text info</a>
```
ע�⣺�������ַ�ʽ��д�������õĲ�����λ�ò��ܵ��������ǹ���û�п����ⷽ���˵�����п������ҵ���ʾʵ�������⣬���������Ŀ��û�ӭ�������ԡ�
��һ�ַ�ʽ����ʾ�����ֱ��������ǰ�棬�����м�Ĳ�����·�����ã�����һ�������Ƕ�����������ã�����㻹Ҫ������������Ҫ������Ȼֻ�ܷ�������档
�ڶ��·�ʽ�Ĳ���λ��Ҳ����Ҫ��ģ���һ������������·�����ã�����Ĳ������ö�������ԡ�
������Ⱦ֮���HTML�����г��ֱ�ǩ`id`Ϊ`ember`������`ember-xxx`����Щ���Զ���EmberĬ�����ɵģ����ǿ�����ʱ����������
�ۺϣ�������ƪ�ǽ���`link-to`�ģ����������漰����`route`�����þ�˳�㽲�����е��Ѷȣ���Ҫ��·�ɵ�Ƕ�����֪ʶ���ϣ����Ƕ��ں����`route`��һ�µ�ѧϰ�Ǻ��а����ģ�`route`�����ü�������ΪURL���õġ��������ǽ��ܹ����ģ�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������



