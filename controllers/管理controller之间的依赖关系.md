����·��Ƕ�׵�����£��������Ҫ��������ͬ��`controller`֮��ͨ�š�
���չ�������׼��������
```
ember g route post
ember g route post/comments
ember g model post
```
���������·�����ã�
```js
//  router.js

import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
  this.route('blog-post');
  this.route('post', { path: '/posts/:post_id' }, function() {
    this.route('comments');
  });
});

export default Router;
```
�������·���������ɵ�·�ɱ��뿴[Ember.js ����ָ��֮ʮ��{{link-to}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-san-link-to/)��
	
����û�����`/posts/1/comments`��ģ��`post`�ͻ���ص�`postController`��������ֱ�Ӽ��ص�`commentsController`��Ȼ�����������һƪ`post`����ʾ`comment`��Ϣ�أ�

Ϊ��ʵ��������ܣ����԰�`postController`ע�뵽`commentController`�С�
```js
//  app/controllers/comments.js

import Ember from 'ember';

export default Ember.Controller.extend({
	postController: Ember.inject.controller('post')
});
```
һ��`comments`·�ɱ����ʣ�`postController`�ͻ��ȡ��������Ӧ��`model`���������`model`��ֻ���ġ�Ϊ���ܻ�ȡ��ģ��`post`����Ҫ����һ������`postController.model`��
```js
//  app/controllers/comments.js

import Ember from 'ember';

export default Ember.Controller.extend({
	postController: Ember.inject.controller('post'),
	post: Ember.computed.reads('postController.model')
});
```
������ֱ����`comment`ģ������ʾģ��`post`��`comment`����Ϣ��
```html
<h1>Comments for {{post.title}}</h1>
<ul>
	{{#each model as |comment|}}
		<li>{{comment.text}}</li>
	{{/each}}
</ul>
```
�йظ�������Ľ������Ʋ�����鿴[API�ĵ�](emberjs.com/api/#method_computed_alias)�Ľ��ܡ���������˽�������ע��������뿴[����](emberjs.com/api/#method_computed_alias)�Ľ̳̣��°�����Ѿ�û�������ַ���ĵ��ˣ���

`controller`���µ����ݵ���Ҳȫ����������ˣ�ֻ�����ȵ�2ƪ�̳̣��ɼ�`controller`��[Ember](http://emberjs.com)δ���汾�ᱻ�������ѳɱ�Ȼ��

��ô��һ�½�Ϊ������ģ�ͣ�ģ�Ͷ���[Ember](http://emberjs.com)��˵��һ��ǳ���Ҫ�����ݣ�����Ҳ�Ƚ϶࣡�һ���9ƪ�������������ģ�ͣ��Ӷ��嵽��ʹ�õȵ����ݡ�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������


